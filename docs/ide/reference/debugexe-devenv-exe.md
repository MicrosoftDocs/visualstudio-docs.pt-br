---
title: -DebugExe (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /DebugExe switch
- DebugExe switch
- /DebugExe [devenv.exe]
- debugging executables
ms.assetid: cd700006-1648-418f-924b-4b1e5c1412ab
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bb4eb1eb49cd6b29740fb6d365a98a51cc28387e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72661673"
---
# <a name="debugexe-devenvexe"></a>/DebugExe (devenv.exe)

Abre o arquivo executável especificado a ser depurado.

## <a name="syntax"></a>Sintaxe

```shell
devenv /DebugExe ExecutableFile
```

## <a name="arguments"></a>Arguments

- *ExecutableFile*

  Necessário. O caminho e o nome de um arquivo `.exe`. Se o arquivo `.exe` não for encontrado ou não existir, não será exibido nenhum aviso ou erro, e o Visual Studio iniciará normalmente.

## <a name="remarks"></a>Comentários

Quaisquer cadeias de caracteres após o parâmetro *ExecutableFile* são passadas para esse arquivo como argumentos.

## <a name="example"></a>Exemplo

O exemplo a seguir abre o arquivo `MyApplication.exe` para depuração.

```shell
devenv /debugexe MyApplication.exe
```

## <a name="see-also"></a>Consulte também

- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)