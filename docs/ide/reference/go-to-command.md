---
title: Comando Ir para
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- edit.goto
helpviewer_keywords:
- Debug.Goto command
- Go To command
ms.assetid: 201e1dd2-6701-467d-8cc1-faec2ef20511
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5782f5e7dba8d18f9d6f48f345d5e133138e6eea
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72748745"
---
# <a name="go-to-command"></a>Comando Ir para
Move o cursor para a linha especificada.

## <a name="syntax"></a>Sintaxe

```cmd
Edit.GoTo [linenumber]
```

## <a name="arguments"></a>Arguments
`linenumber`\
Opcional. Um inteiro que representa o número da linha para a qual ir.

## <a name="remarks"></a>Comentários
A numeração de linha começa em um. Se o valor de `linenumber` for menor que um, a primeira linha será exibida. Se o valor de `linenumber` for maior que o número da última linha, a última linha será exibida.

Se um valor para `linenumber` não for especificado, a caixa de diálogo **Ir para a Linha** será exibida.

O alias para esse comando é GoToLn.

## <a name="example"></a>Exemplo

```cmd
>Edit.GoTo 125
```

## <a name="see-also"></a>Consulte também

- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela Comando](../../ide/reference/command-window.md)
- [Caixa Localizar/Comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)