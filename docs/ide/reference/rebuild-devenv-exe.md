---
title: -Rebuild (devenv.exe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /rebuild switch
- rebuild Devenv switch (/rebuild)
- projects [Visual Studio], rebuilding
- /rebuild Devenv switch
- applications [Visual Studio], rebuilding
ms.assetid: c5a8a4bf-0e2b-46eb-a44a-8aeb29b92c32
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b0946137cb259386648b7b3ac2883c33f5724352
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948603"
---
# <a name="rebuild-devenvexe"></a>/Rebuild (devenv.exe)
Limpa e, em seguida, compila a configuração de solução especificada.

## <a name="syntax"></a>Sintaxe

```cmd
devenv SolutionName /rebuild SolnConfigName [/project ProjName] [/projectconfig ProjConfigName]
```

## <a name="arguments"></a>Arguments
 `SolnConfigName`

 Necessário. O nome da configuração de solução que será usada para recompilar a solução nomeada no `SolutionName`.

 `SolutionName`

 Necessário. O caminho completo e o nome do arquivo de solução.

 /project `ProjName`

 Opcional. O caminho e o nome de um arquivo de projeto na solução. É possível inserir um caminho relativo da pasta `SolutionName` para o arquivo de projeto ou o nome de exibição do projeto ou o caminho completo e o nome do arquivo de projeto.

 /projectconfig `ProjConfigName`

 Opcional. O nome da configuração de build do projeto a ser usado para recompilar o `/project` nomeado.

## <a name="remarks"></a>Comentários

-   Essa opção executa a mesma função que o comando de menu **Recompilar Solução** dentro do IDE (ambiente de desenvolvimento integrado).

-   Coloque as cadeias de caracteres que incluem espaços entre aspas duplas.

-   As informações de resumo para limpezas e builds, incluindo erros, podem ser exibidas na janela **Comando** ou em qualquer arquivo de log especificado com a opção `/out`.

## <a name="example"></a>Exemplo
 Este exemplo limpa e recompila o projeto `CSharpWinApp`, usando a configuração de build de projeto `Debug` dentro da configuração da solução `Debug` de `MySolution`.

```cmd
devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /rebuild Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>Consulte também

- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)