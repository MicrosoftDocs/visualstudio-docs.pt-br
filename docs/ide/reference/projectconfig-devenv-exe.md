---
title: Opção ProjectConfig do DevEnv
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /projectconfig Devenv switch
- configurations, rebuilding
- deployment projects, creating
- configurations, cleaning
- deployment projects, specifying
- deployment projects, adding
- build configurations, specifying
- Devenv, /projectconfig switch
- projectconfig Devenv switch (/projectconfig)
- projects [Visual Studio], build configuration
- projects [Visual Studio], cleaning
ms.assetid: 6b54ef59-ffed-4f62-a645-1279ede97ebf
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 44f5d4479658b450074ba35f2759a273bb584e0a
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34764648"
---
# <a name="projectconfig-devenvexe"></a>/ProjectConfig (devenv.exe)

Especifica uma configuração de build do projeto a ser aplicada durante o build, a limpeza, a recompilação ou a implantação do projeto nomeado no argumento **/project**.

## <a name="syntax"></a>Sintaxe

```cmd
devenv SolutionName {/build|/clean|/rebuild|/deploy} SolnConfigName [/project ProjName] [/projectconfig ProjConfigName]
```

## <a name="arguments"></a>Arguments

|||
|-|-|
|/build|Compila o projeto especificado pelo argumento **/project**.|
|/clean|Limpa todos os arquivos intermediários e diretórios de saída criados durante um build.|
|/rebuild|Limpa e, em seguida, compila o projeto especificado pelo argumento **/project**.|
|/deploy|Especifica que o projeto será implantado após um build ou uma recompilação.|
|*SolnConfigName*|Necessário. O nome da configuração da solução que será aplicado à solução nomeada em *SolutionName*. Se várias plataformas de solução estiverem disponíveis, você também precisará especificar a plataforma, por exemplo, **"Debug\|Win32"**.|
|*SolutionName*|Necessário. O caminho completo e o nome do arquivo de solução.|
|/project *ProjName*|Opcional. O caminho e o nome de um arquivo de projeto na solução. Insira um caminho relativo da pasta *SolutionName* para o arquivo de projeto, o nome de exibição do projeto ou o caminho completo e o nome do arquivo de projeto.|
|/projectconfig *ProjConfigName*|Opcional. O nome de uma configuração de build do projeto a ser aplicado ao projeto especificado pelo argumento **/project**. Se várias plataformas de solução estiverem disponíveis, você também precisará especificar a plataforma, por exemplo, **"Debug\|Win32"**.|

## <a name="remarks"></a>Comentários

A opção **/projectconfig** precisa ser usada com a opção **/project** como parte de um comando **/build**, **/clean**, **/rebuild** ou **/deploy**.

Coloque as cadeias de caracteres que incluem espaços entre aspas duplas.

As informações de resumo para builds, incluindo erros, podem ser exibidas na janela Comando ou em qualquer arquivo de log especificado com a opção **/out**.

## <a name="example"></a>Exemplo

O seguinte comando compila o projeto "CSharpConsoleApp" usando a configuração de build do projeto "Debug" dentro da configuração da solução "Debug" de "MySolution":

```cmd
devenv "C:\Visual Studio Projects\MySolution\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>Consulte também

- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)
- [/Project (devenv.exe)](../../ide/reference/project-devenv-exe.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Deploy (devenv.exe)](../../ide/reference/deploy-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)