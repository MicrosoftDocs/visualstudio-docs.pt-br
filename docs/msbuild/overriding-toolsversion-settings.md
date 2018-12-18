---
title: Substituindo as configurações de ToolsVersion | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, overriding ToolsVersion setting
- MSBuild, building solutions with
ms.assetid: ccd42c07-0fb6-4e8b-9ebb-a6a6db18aa2e
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0f0abe9db7178678c4ffda7f4179117817b3add6
ms.sourcegitcommit: 71218ffc33da325cc1b886f69ff2ca50d44f5f33
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48879287"
---
# <a name="override-toolsversion-settings"></a>Substituir as configurações de ToolsVersion
Você pode alterar o conjunto de ferramentas para projetos e soluções de uma entre três maneiras:  
  
1.  Usando a opção `-ToolsVersion` (ou `-tv`, de forma abreviada) quando você compila o projeto ou solução por meio da linha de comando.  
  
2.  Configurando o parâmetro `ToolsVersion` na tarefa MSBuild.  
  
3.  Configurando a propriedade `$(ProjectToolsVersion)` em um projeto dentro de uma solução. Isso permite criar um projeto em uma solução com a versão do conjunto de ferramentas que difere daquela de outros projetos.  
  
## <a name="override-the-toolsversion-settings-of-projects-and-solutions-on-command-line-builds"></a>Substituir as configurações de ToolsVersion de projetos e soluções em builds da linha de comando  
 Embora os projetos do Visual Studio normalmente sejam compilados com o ToolsVersion especificado no arquivo de projeto, você pode usar a opção `-ToolsVersion` (ou `-tv`) na linha de comando para substituir esse valor e compilar todos os projetos e suas dependências de projeto para o projeto com um conjunto de ferramentas diferente. Por exemplo:  
  
```cmd  
msbuild.exe someproj.proj -tv:12.0 -p:Configuration=Debug  
```  
  
 Neste exemplo, todos os projetos são compilados usando ToolsVersion 12.0. (No entanto, consulte a seção [Ordem de precedência](#order-of-precedence) posteriormente neste tópico).  
  
 Ao usar a opção `-tv` na linha de comando, você pode usar a propriedade `$(ProjectToolsVersion)` em projetos individuais para compilá-los com um valor de ToolsVersion diferente dos outros projetos na solução.  
  
## <a name="override-the-toolsversion-settings-using-the-toolsversion-parameter-of-the-msbuild-task"></a>Substituir as configurações de ToolsVersion usando o parâmetro ToolsVersion da tarefa MSBuild  
 A tarefa do MSBuild é o principal meio para um projeto compilar outro. Para habilitar a tarefa do MSBuild para criar um projeto com um ToolsVersion diferente daquele especificado no projeto, ela fornece um parâmetro de tarefa opcional chamado `ToolsVersion`. O exemplo a seguir demonstra como usar esse parâmetro:  
  
1.  Crie um arquivo chamado *projectA.proj* que contém o código a seguir:  
  
    ```xml  
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
    ToolsVersion="12.0">  
  
        <Target Name="go" >   
            <Message Text="projectA.proj" />  
            <Message Text="MSBuildToolsVersion: $(MSBuildToolsVersion)" />  
            <Message Text="MSBuildToolsPath:    $(MSBuildToolsPath)" />  
  
            <MSBuild Projects="projectB.proj"  
                ToolsVersion="2.0"  
                Targets="go" />  
        </Target>  
    </Project>  
    ```  
  
2.  Crie outro arquivo chamado *projectB.proj* que contém o código a seguir:  
  
    ```xml  
    <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003"  
    ToolsVersion="12.0">  
  
        <Target Name="go">  
            <Message Text="projectB.proj" />  
            <Message Text="MSBuildToolsVersion: $(MSBuildToolsVersion)" />  
            <Message Text="MSBuildToolsPath:    $(MSBuildToolsPath)" />  
        </Target>  
    </Project>  
    ```  
  
3.  Em um prompt de comando, digite o seguinte comando:  
  
    ```cmd  
    msbuild projectA.proj -t:go -toolsversion:3.5  
    ```  
  
4.  A saída a seguir aparece. Para `projectA`, a configuração `-toolsversion:3.5` na linha de comando substitui a configuração `ToolsVersion=12.0` na marca `Project`.  
  
     `ProjectB` é chamado por uma tarefa em `projectA`. Essa tarefa tem `ToolsVersion=2.0`, que substitui as outras configurações `ToolsVersion` para `projectB`.  
  
    ```  
    Output:  
      projectA.proj  
      MSBuildToolsVersion: 3.5  
      MSBuildToolsPath:    C:\Windows\Microsoft.NET\Framework\v3.5  
  
      projectB.proj  
      MSBuildToolsVersion: 2.0  
      MSBuildToolsPath:    C:\Windows\Microsoft.NET\Framework\v2.0.50727  
    ```  
  
## <a name="order-of-precedence"></a>Ordem de precedência  
 A ordem de precedência, em ordem decrescente, usada para determinar a `ToolsVersion` é:  
  
1.  O atributo `ToolsVersion` na tarefa MSBuild usado para compilar o projeto, se houver.  
  
2.  A opção `-toolsversion` (ou `-tv`) que é usado no comando msbuild.exe, se houver.  
  
3.  Se a variável de ambiente `MSBUILDTREATALLTOOLSVERSIONSASCURRENT` estiver definida, use o `ToolsVersion` atual.  
  
4.  Se a variável de ambiente `MSBUILDTREATHIGHERTOOLSVERSIONASCURRENT` estiver definida e a `ToolsVersion` definida no arquivo de projeto for maior que a `ToolsVersion` atual, use a `ToolsVersion` atual.  
  
5.  Se a variável de ambiente `MSBUILDLEGACYDEFAULTTOOLSVERSION` estiver definida ou se `ToolsVersion` não estiver definida, as etapas a seguir serão usadas:  
  
    1.  O atributo `ToolsVersion` do elemento [Project](../msbuild/project-element-msbuild.md) do arquivo de projeto. Se esse atributo não existir, será considerado que se trata da versão atual.  
  
    2.  A versão padrão das ferramentas no arquivo *MSBuild.exe.config*.  
  
    3.  A versão das ferramentas padrão no Registro. Para saber mais, confira [Configurações padrão e personalizadas do Conjunto de Ferramentas](../msbuild/standard-and-custom-toolset-configurations.md).  
  
6.  Se a variável de ambiente `MSBUILDLEGACYDEFAULTTOOLSVERSION` não estiver definida, as etapas a seguir serão usadas:  
  
    1.  Se a variável de ambiente `MSBUILDDEFAULTTOOLSVERSION` estiver definida para um `ToolsVersion` que existe, use-a.  
  
    2.  Se `DefaultOverrideToolsVersion` estiver definida em *MSBuild.exe.config*, use-a.  
  
    3.  Se `DefaultOverrideToolsVersion` estiver definida no Registro, use-a.  
  
    4.  Caso contrário, use a `ToolsVersion` atual.  
  
## <a name="see-also"></a>Consulte também  
 [Multiplataforma](../msbuild/msbuild-multitargeting-overview.md)   
 [Conceitos do MSBuild](../msbuild/msbuild-concepts.md)   
 [Conjunto de Ferramentas (ToolsVersion)](../msbuild/msbuild-toolset-toolsversion.md)   
 [Configurações padrão e personalizadas do Conjunto de Ferramentas](../msbuild/standard-and-custom-toolset-configurations.md)