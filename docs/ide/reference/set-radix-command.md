---
title: Comando Definir Base
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.setradix
helpviewer_keywords:
- Set Radix command
- Debug.SetRadix command
ms.assetid: 6ffd1554-7530-4da4-b5f5-e276a5034f3b
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e88dc1318e29ddf35073b78218eb113fe8952aac
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769643"
---
# <a name="set-radix-command"></a>Comando Definir Base
Define ou retorna a base numérica usada para exibir valores inteiros.

## <a name="syntax"></a>Sintaxe

```cmd
Debug.SetRadix [10 | 16 | hex | dec]
```

## <a name="arguments"></a>Argumentos
`10` ou `16` ou `hex` ou `dec`

Opcional. Indica o decimal (10 ou dez) ou hexadecimal (16 ou hexa). Se um argumento for omitido, o valor base atual será retornado.

## <a name="example"></a>Exemplo
Este exemplo define o ambiente para exibir valores inteiros em formato hexadecimal.

```cmd
>Debug.SetRadix hex
```

## <a name="see-also"></a>Confira também

- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela de comando](../../ide/reference/command-window.md)
- [Caixa Localizar/comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)