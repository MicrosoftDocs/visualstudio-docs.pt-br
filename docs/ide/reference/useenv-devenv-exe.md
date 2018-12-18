---
title: -UseEnv (devenv.exe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- VC.Project.UseEnvVars.ExcludePath
- VC.Project.UseEnvVars.LibraryPath
- VC.Project.UseEnvVars.SourcePath
- VC.Project.UseEnvVars.Include
- VC.Project.UseEnvVars.Path
- VC.Project.UseEnvVars.ReferencePath
helpviewer_keywords:
- UseEnv switch
- /UseEnv Devenv switch
- Devenv, /UseEnv
ms.assetid: 2dd14603-a61b-42d2-ba31-427a0ee8a799
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0a11d8eceec682e37f9bf34c79980c37880bdbe6
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948485"
---
# <a name="useenv-devenvexe"></a>/UseEnv (devenv.exe)

Inicia o Visual Studio e carrega variáveis de ambiente para a caixa de diálogo **Diretórios do VC++**.

> [!NOTE]
> Essa opção é instalada com a carga de trabalho de **Desenvolvimento para desktop com C++**.

## <a name="syntax"></a>Sintaxe

```shell
Devenv /useenv
```

## <a name="example"></a>Exemplo

O exemplo a seguir inicia o Visual Studio e carrega variáveis de ambiente para a caixa de diálogo **Diretórios do VC++**.

```shell
Devenv.exe /useenv
```

## <a name="see-also"></a>Consulte também

* [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)