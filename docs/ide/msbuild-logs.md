---
title: Solucionar problemas e criar logs para problemas do MSBuild
ms.date: 06/27/2019
ms.technology: vs-ide-compile
ms.topic: troubleshooting
helpviewer_keywords:
- msbuild logs"
author: corob-msft
ms.author: corob
manager: jillfra
dev_langs:
- CSharp
- VB
- CPP
ms.workload:
- multiple
ms.description: Generate build logs for msbuild projects to collect helpful information when troubleshooting issues.
ms.openlocfilehash: ae91f7b9c90f0b06c449d26f67fe4fcc3434518e
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768696"
---
# <a name="troubleshoot-and-create-logs-for-msbuild-problems"></a>Solucionar problemas e criar logs para problemas do MSBuild

Os procedimentos a seguir podem ajudá-lo a diagnosticar problemas de compilação no projeto do Visual Studio e, se necessário, crie um log para enviar à Microsoft para investigação.

## <a name="a-property-value-is-ignored"></a>Um valor da propriedade é ignorado

Se uma propriedade de projeto parece estar definida como um valor específico, mas não tem nenhum efeito na compilação, siga estas etapas:

1. Abra o Prompt de Comando do Desenvolvedor do Visual Studio que corresponde à sua versão do Visual Studio.
1. Execute o comando a seguir, depois de substituir os valores com o caminho de solução, a configuração e o nome do projeto:

    ```cmd
    msbuild /p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /pp:out.xml MyProject.vcxproj
    ```

    Esse comando gera um arquivo de projeto msbuild "pré-processado" (out.xml). Você pode pesquisar esse arquivo por uma propriedade específica para ver onde ela está definida.

A última definição de uma propriedade é o que é consumido na compilação. Se a propriedade estiver definida duas vezes, o segundo valor substitui o primeiro. Além disso, o MSBuild avalia o projeto em vários passos:

- PropertyGroups e importações
- ItemDefinitionGroups
- ItemGroups
- Destinos

Portanto, dada a seguinte ordem:

```xml
<PropertyGroup>
   <MyProperty>A</MyProperty>
</PropertyGroup>
<ItemGroup>
   <MyItems Include="MyFile.txt"/>
</ItemGroup>
<ItemDefinitionGroup>
  <MyItems>
      <MyMetadata>$(MyProperty)</MyMetadata>
  </MyItems>
</ItemDefinitionGroup>
<PropertyGroup>
   <MyProperty>B</MyProperty>
</PropertyGroup>
```

O valor de "MyMetadata" do item "Myfile.txt" será avaliado como "B" durante a compilação (não como "A" e vazio)

## <a name="incremental-build-is-building-more-than-it-should"></a>A compilação incremental está compilando mais do que deveria

Se o MSBuild está recompilando desnecessariamente um projeto ou item de projeto, crie um log de compilação detalhado ou binário. Você pode pesquisar no log pelo arquivo que foi criado ou compilado desnecessariamente. A saída é parecida com esta:

```output
  Task "CL"

  Using cached input dependency table built from:

  F:\test\Project1\Project1\Debug\Project1.tlog\CL.read.1.tlog

  Outputs for F:\TEST\PROJECT1\PROJECT1\PROJECT1.CPP:
  F:\TEST\PROJECT1\PROJECT1\DEBUG\PROJECT1.OBJ
  Project1.cpp will be compiled because F:\TEST\PROJECT1\PROJECT1\PROJECT1.H was modified at 6/5/2019 12:37:09 PM.

  Outputs for F:\TEST\PROJECT1\PROJECT1\PROJECT1.CPP:
  F:\TEST\PROJECT1\PROJECT1\DEBUG\PROJECT1.OBJ

  Write Tracking Logs:
  Debug\Project1.tlog\CL.write.1.tlog
```

Se você estiver compilando no IDE do Visual Studio (com detalhamento de janela de saída detalhada), a **Janela de Saída** exibe a razão pela qual cada projeto não está atualizado:

```output
1>------ Up-To-Date check: Project: Project1, Configuration: Debug Win32 ------

1>Project is not up-to-date: build input 'f:\test\project1\project1\project1.h' was modified after the last build finished.
```

## <a name="create-a-binary-msbuild-log"></a>Criar um log msbuild binário

1. Abrir o Prompt de Comando do Desenvolvedor da sua versão do Visual Studio
1. No prompt de comando, execute um dos seguintes comandos. (Lembre-se de usar seus valores reais de projeto e configuração.):

    ```cmd
    Msbuild /p:Configuration="MyConfiguration";Platform="x86" /bl MySolution.sln
    ```

    ou o

    ```cmd
    Msbuild /p:/p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /bl MyProject.vcxproj
    ```

Um arquivo Msbuild.binlog será criado no diretório que você executou o MSBuild. Você pode exibi-lo e pesquisá-lo usando o [Visualizador de log estruturado do Msbuild](http://www.msbuildlog.com/).

## <a name="create-a-detailed-log"></a>Criar um log detalhado

1. No menu principal do Visual Studio, vá para **ferramentas**  >  **Opções**  >  **projetos e soluções**  > **Compilar e executar**.
1. Configure o **Detalhamento de compilação do projeto Msbuild** como **Detalhado** nas duas caixas de combinação. A parte superior controla o detalhamento de compilação no **janela de saída** e o segundo controla o detalhamento da compilação no \<projectname\> arquivo. log que é criado no diretório intermediário de cada projeto durante a compilação.
2. Em um prompt de comando do desenvolvedor do Visual Studio, digite um desses comandos, substituindo o caminho real e os valores de configuração:

    ```cmd
    Msbuild /p:Configuration="MyConfiguration";Platform="x86" /fl MySolution.sln
    ```

    ou o

    ```cmd
    Msbuild /p:/p:SolutionDir="c:\MySolutionDir\";Configuration="MyConfiguration";Platform="Win32" /fl MyProject.vcxproj
    ```

    Um arquivo Msbuild.log será criado no diretório a partir do qual você executou o msbuild.
