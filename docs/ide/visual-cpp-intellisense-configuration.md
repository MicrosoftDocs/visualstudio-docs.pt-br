---
title: Configurar um projeto do C++ para o IntelliSense
ms.date: 10/08/2018
ms.technology: vs-ide-general
ms.topic: conceptual
author: mblome
ms.author: mblome
manager: wpickett
ms.workload:
- cplusplus
ms.openlocfilehash: 3772c2c910188aacb675f267d20f5e0f16565001
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49836628"
---
# <a name="configure-a-c-project-for-intellisense"></a>Configurar um projeto do C++ para o IntelliSense

Em alguns casos, pode ser necessário configurar manualmente o projeto do C++ para fazer com que o IntelliSense funcione corretamente. Para projetos do MSBuild (com base em arquivos .vcxproj), é possível ajustar as configurações nas propriedades do projeto. Para projetos não MSBuild, as configurações são ajustadas no arquivo CppProperties.json no diretório raiz do projeto. Em alguns casos, pode ser preciso criar um arquivo de dicas para ajudar o IntelliSense a entender as definições de macro. O ambiente de desenvolvimento integrado (IDE) do Visual Studio ajuda a identificar e corrigir problemas do IntelliSense.



## <a name="single-file-intellisense"></a>IntelliSense de arquivo único

Ao abrir um arquivo que não está incluído em um projeto, o Visual Studio fornece um certo suporte IntelliSense, mas por padrão, nenhum rabisco de erro é mostrado. Se a **Barra de Navegação** exibir *Arquivos Diversos*, esse é o possível motivo de você não estar vendo rabiscos de erros na opção código incorreto, ou pode ser porque um macro pré-processador não foi definido.

## <a name="check-the-error-list"></a>Verificar a Lista de Erros

Se um arquivo não for aberto no modo de arquivo único e o IntelliSense não estiver funcionando corretamente, o primeiro lugar a verificar é a janela de Lista de Erros. Para ver todos os erros de IntelliSense para o arquivo de origem atual, junto com todos os arquivos de cabeçalho incluídos, escolha **Compilação + IntelliSense** na lista suspensa:

![VC++ IntelliSense na Lista de Erros](media/vcpp-intellisense-error-list.png)

O IntelliSense produz um máximo de 1.000 erros. Se houver mais de 1.000 erros nos arquivos de cabeçalho incluídos por um arquivo de origem, este mostrará apenas um rabisco de erro único no início do arquivo de origem.

## <a name="ensure-include-paths-are-correct"></a>Certificar-se de que os caminhos de #include estão corretos

### <a name="msbuild-projects"></a>Projetos do MSBuild

Se você executar suas compilações fora do ambiente de desenvolvimento integrado (IDE) do Visual Studio e elas estiverem tendo êxito, mas o IntelliSense está incorreto, é possível que sua linha de comando esteja fora de sincronia com as configurações de projeto para uma ou mais configurações. Clique com o botão direito do mouse no nó do projeto no **Gerenciador de Soluções** e certifique-se de que todos os caminhos de **#include** estejam adequados para a configuração e a plataforma atual. Se os caminhos forem idênticos em todas as configurações e plataformas, você pode selecionar **Todas as configurações** e **Todas as plataformas** e depois verificar se os caminhos estão corretos.

![Diretórios de inclusão VC++](media/vcpp-intellisense-include-paths.png)

 Para ver os valores atuais para a compilação de macros, como **VC_IncludePath**, selecione a linha de Diretórios de Inclusão e clique na lista suspensa à direita. Depois escolha **\<Editar>** e clique no botão **Macros**.

### <a name="makefile-projects"></a>Projetos Makefile

Para projetos Makefile baseados no modelo de projeto NMake, escolha **NMake** no painel esquerdo e **caminho de pesquisas de inclusão** na categoria **IntelliSense**:

![Caminhos de inclusão no projeto Makefile](media/vcpp-intellisense-makefile-include-paths.png)

Para saber mais, confira [Como habilitar o IntelliSense para projetos Makefile](/cpp/ide/how-to-enable-intellisense-for-makefile-projects).

### <a name="open-folder-projects"></a>Projetos de pasta aberta

Para projetos CMake, certifique-se de que os caminhos de #include estejam especificados corretamente para todas as configurações em CMakeLists.txt. Outros tipos de projeto podem exigir um arquivo CppProperties.json. Para saber mais, confira [Configurar o IntelliSense com CppProperties.json](/cpp/ide/non-msbuild-projects#cppproperties). Os caminhos devem estar corretos para cada configuração definida no arquivo.

Se houver um erro de sintaxe no arquivo CppProperties.json, o IntelliSense ficará incorreto nos arquivos afetados. O Visual Studio exibirá o erro na Janela de Saída.

## <a name="tag-parser-issues"></a>Problemas do analisador de marca

O analisador de marca é um analisador de C++ “difuso” usado para navegação. Ele é muito rápido, mas não tenta entender completamente cada constructo de código.

Por exemplo, ele não avalia os macros de pré-processador e, portanto, pode analisar incorretamente o código que faz uso intenso deles. Quando o Analisador de Marca encontra um constructo de código não familiar, ele pode ignorar toda aquela região do código.

Há duas maneiras comuns em que esse problema se manifesta no Visual Studio:

1. Se a Barra de Navegação mostrar um macro mais interno, a definição da função atual foi ignorada:

   ![O Analisador de Marca ignora a definição da função](media/vcpp-intellisense-tag-parser-macro.png)

1. O IDE se oferece para criar uma definição de função para uma função já definida:

   ![O Analisador de Marca se oferece para definir uma função existente](media/vcpp-intellisense-tag-parser-function.png)

Para corrigir esses tipos de problemas, adicione um arquivo chamado **cpp.hint** na raiz do diretório de soluções. Para saber mais, confira [Arquivos de dicas](/cpp/ide/hint-files).

Os erros do Analisador de Marca do **Visual Studio 2017 versão 15.7** são exibidos na janela de Lista de Erros.

## <a name="validate-project-settings-with-diagnostic-logging"></a>Validar configurações do projeto com o log de diagnóstico

Para verificar se o compilador do IntelliSense está usando as opções adequadas do compilador, incluindo os caminhos de inclusão e os macros pré-processadores, ative o Log de diagnóstico das linhas de comando do IntelliSense em **Ferramentas > Opções > Editor de texto > C/C++ > Avançado > Log de diagnóstico**. Defina como True **Habilitar registro em log**, 5 (mais detalhado) para **Nível de log** e 8 (registro em log do IntelliSense) para **Filtro de registro em log**.

A Janela de Saída passará a mostrar as linhas de comando que são passadas para o compilador do IntelliSense. Veja um exemplo de saída:

```output
 [IntelliSense] Configuration Name: Debug|Win32
 [IntelliSense] Toolset IntelliSense Identifier:
 [IntelliSense] command line options:
 /c
 /I.
 /IC:\Repo\Includes
 /DWIN32
 /DDEBUG
 /D_DEBUG
 /Zc:wchar_t-
 /Zc:forScope
 /Yustdafx.h
```

Essas informações podem ajudar você a entender por que o IntelliSense está fornecendo informações imprecisas. Por exemplo, se o diretório de inclusão do seu projeto contiver **$(MyVariable)\Include** e o log de diagnóstico mostrar **/I\Include** como um caminho de inclusão, quer dizer que **$(MyVariable)** não foi avaliada e foi removida do caminho de inclusão final.

## <a name="about-the-intellisense-build"></a>Sobre a compilação do IntelliSense

O Visual Studio usa um compilador de C++ dedicado para criar e manter o banco de dados que sustenta todos os recursos do IntelliSense. Para manter o banco de dados do IntelliSense em sincronia com o código, o Visual Studio inicia automaticamente as compilações somente IntelliSense como tarefas em segundo plano em resposta a determinadas alterações feitas nas configurações de projetos ou em arquivos de origem.

No entanto, em alguns casos o Visual Studio pode não atualizar o banco de dados do IntelliSense de maneira oportuna. Por exemplo, quando você executa um comando de **pull do git** ou **check-out do git**, o Visual Studio pode levar até uma hora para detectar alterações nos arquivos. Você pode forçar um novo exame de todos os arquivos em uma solução clicando com o botão direito do mouse no nó do projeto no **Gerenciador de Soluções** e escolhendo **Examinar novamente a solução**.

## <a name="troubleshooting-intellisense-build-failures"></a>Como solucionar problemas de falhas de compilação do IntelliSense

Uma compilação do IntelliSense não produz binários, mas ainda assim poderá falhar. Uma possível causa de falha são os arquivos personalizados .props ou .targets. No Visual Studio 2017 versão 15.6, os erros de compilação somente IntelliSense são registrados na Janela de Saída. Para vê-los, defina **Mostrar saída de** a **Solução**:

![Janela de Saída para erros de solução](media/vcpp-intellisense-output-window.png)

A mensagem de erro pode instruir você a habilitar o rastreamento de tempo de design:

```output
 error: Designtime build failed for project 'E:\src\MyProject\MyProject.vcxproj',
 configuration 'Debug|x64'. IntelliSense might be unavailable.
 Set environment variable TRACEDESIGNTIME=true and restart
 Visual Studio to investigate.
```

Se você definir a variável de ambiente TRACEDESIGNTIME como true e reiniciar o Visual Studio, verá um arquivo de log no diretório %TEMP%, que pode ajudar a diagnosticar a falha de compilação.

Saiba mais sobre a variável de ambiente TRACEDESIGNTIME em [Roslyn](https://github.com/dotnet/roslyn/wiki/Diagnosing-Project-System-Build-Errors) e [Common Project System](https://github.com/dotnet/project-system/blob/master/docs/design-time-builds.md). As informações neste artigo são relevantes para projetos do C++.

## <a name="see-also"></a>Consulte também

- [Visual C++ IntelliSense](visual-cpp-intellisense.md)
