---
title: -DebugExe (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /DebugExe switch
- DebugExe switch
- /DebugExe [devenv.exe]
ms.assetid: cd700006-1648-418f-924b-4b1e5c1412ab
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f472add6b821693d1d48397e878db19e707e2868
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660799"
---
# <a name="debugexe-devenvexe"></a>/DebugExe (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Abre o arquivo executável especificado a ser depurado.

## <a name="syntax"></a>Sintaxe

```
Devenv /debugexe ExecutableFile
```

## <a name="arguments"></a>Arguments
 `ExecutableFile` Necessário. O caminho e o nome de um arquivo .exe.

 Se o arquivo .exe não for encontrado ou não existir, nenhum aviso nem erro será exibido, e [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] iniciará normalmente.

## <a name="remarks"></a>Comentários
 Quaisquer cadeias de caracteres após o parâmetro `ExecutableFile` são passadas para esse arquivo como argumentos.

## <a name="example"></a>Exemplo
 O exemplo a seguir abre o arquivo `MyApplication.exe` para depuração.

```
Devenv.exe /debugexe MyApplication.exe
```

## <a name="see-also"></a>Veja também
 [Opções de linha de comando devenv](../../ide/reference/devenv-command-line-switches.md)
