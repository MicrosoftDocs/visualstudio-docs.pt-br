---
title: -DebugExe (devenv.exe)
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /DebugExe switch
- DebugExe switch
- /DebugExe [devenv.exe]
ms.assetid: cd700006-1648-418f-924b-4b1e5c1412ab
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 1badcaba6f6461f6a2c6b73580d8d12c50481c2b
ms.sourcegitcommit: 54c65f81a138fc1e8ff1826f7bd9dcec710618cc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/19/2018
ms.locfileid: "51948771"
---
# <a name="debugexe-devenvexe"></a>/DebugExe (devenv.exe)
Abre o arquivo executável especificado a ser depurado.

## <a name="syntax"></a>Sintaxe

```cmd
Devenv /debugexe ExecutableFile
```

## <a name="arguments"></a>Arguments
 `ExecutableFile`

 Necessário. O caminho e o nome de um arquivo .exe.

 Se o arquivo .exe não for encontrado ou não existir, nenhum aviso nem erro será exibido, e [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] iniciará normalmente.

## <a name="remarks"></a>Comentários
 Quaisquer cadeias de caracteres após o parâmetro `ExecutableFile` são passadas para esse arquivo como argumentos.

## <a name="example"></a>Exemplo
 O exemplo a seguir abre o arquivo `MyApplication.exe` para depuração.

```cmd
Devenv.exe /debugexe MyApplication.exe
```

## <a name="see-also"></a>Consulte também

- [Opções de linha de comando do Devenv](../../ide/reference/devenv-command-line-switches.md)