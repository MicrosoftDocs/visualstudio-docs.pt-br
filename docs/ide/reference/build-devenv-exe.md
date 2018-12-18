---
title: Opção Build do DevEnv
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- builds, command-line
- /build Devenv switch
- Devenv, /build switch
- build Devenv switch
- command-line builds
ms.assetid: ced21627-7653-455b-8821-3e31c6a448cf
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: cdd510e523aaabc468c1f01626593e51d0ad1558
ms.sourcegitcommit: 9571742f4a808c75b1034aa72fc24b54bc50692e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2018
ms.locfileid: "49410956"
---
# <a name="build-devenvexe"></a>/Build (devenv.exe)

Compila uma solução usando um arquivo de configuração de solução especificado.

## <a name="syntax"></a>Sintaxe

```cmd
Devenv SolutionName /build SolnConfigName [/project ProjName [/projectconfig ProjConfigName]]
```

## <a name="arguments"></a>Arguments

|||
|-|-|
|*SolutionName*|Necessário. O caminho completo e o nome do arquivo de solução.|
|*SolnConfigName*|Necessário. O nome da configuração de solução que será usado para compilar a solução nomeada em *SolutionName*. Se várias plataformas de solução estiverem disponíveis, você também precisará especificar a plataforma, por exemplo, **"Debug\|Win32"**.|
|/project *ProjName*|Opcional. O caminho e o nome de um arquivo de projeto na solução. Insira um caminho relativo da pasta *SolutionName* para o arquivo de projeto, o nome de exibição do projeto ou o caminho completo e o nome do arquivo de projeto.|
|/projectconfig *ProjConfigName*|Opcional. O nome de uma configuração de build do projeto a ser usada ao compilar o projeto nomeado. Se várias plataformas de projeto estiverem disponíveis, você também precisará especificar a plataforma, por exemplo, **"Debug\|Win32"**.|

## <a name="remarks"></a>Comentários

- A opção **/build** executa a mesma função que o comando de menu **Compilar Solução** no IDE (ambiente de desenvolvimento integrado).

- Coloque as cadeias de caracteres que incluem espaços entre aspas duplas.

- As informações de resumo para builds, incluindo erros, podem ser exibidas na janela Comando ou em qualquer arquivo de log especificado com a opção **/out**.

- A opção **/build** compila somente projetos que foram alterados desde o último build. Para compilar todos os projetos de uma solução, use [/rebuild](../../ide/reference/rebuild-devenv-exe.md).

- Se você receber uma mensagem de erro que informa **Configuração de projeto inválida**, verifique se você especificou uma plataforma de solução ou de projeto, por exemplo, **"Debug\|Win32"**.

## <a name="example"></a>Exemplo

O comando a seguir compila o projeto "CSharpConsoleApp" usando a configuração de build do projeto "Debug" dentro da configuração da solução "Debug" de "MySolution".

```cmd
devenv "C:\Visual Studio Projects\MySolution\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>Consulte também

- [Criar e limpar projetos e soluções](../../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md)
- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)