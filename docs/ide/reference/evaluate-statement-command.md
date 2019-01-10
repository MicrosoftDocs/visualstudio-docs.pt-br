---
title: Comando Avaliar Instrução
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
f1_keywords:
- debug.evaluatestatement
helpviewer_keywords:
- Debug.EvaluateStatement command
- Evaluate Statement command
ms.assetid: 032039bc-9477-4f93-9b9d-66d4be0e90f4
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b0be6e57c0c741420006d20c0945b9b8c8b77d51
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53864119"
---
# <a name="evaluate-statement-command"></a>Comando Avaliar Instrução
Avalia e exibe a instrução fornecida.

## <a name="syntax"></a>Sintaxe

```cmd
Debug.EvaluateStatement text
```

## <a name="arguments"></a>Arguments
 `text` Necessário. A instrução a ser avaliada.

## <a name="remarks"></a>Comentários
 A janela usada para inserir o comando **EvaluateStatement** determina se um sinal de igual (=) é interpretado como um operador de comparação ou um operador de atribuição.

 Na janela **Comando**, um sinal de igual (=) é interpretado como um operador de comparação. Dessa forma, por exemplo, se os valores das variáveis `a` e `b` forem diferentes, o comando

```cmd
>Debug.EvaluateStatement(a=b)
```

 retornará um valor de `false`.

 Na janela **Imediato**, por outro lado, um sinal de igual (=) é interpretado como um operador de atribuição. Assim, por exemplo, o comando

```cmd
>Debug.EvaluateStatement(a=b)
```

 atribuirá à variável `a` o valor da variável `b`.

## <a name="example"></a>Exemplo

```cmd
>Debug.EvaluateStatement(a+b)
```

## <a name="see-also"></a>Consulte também

- [Comando Print](../../ide/reference/print-command.md)
- [Comandos do Visual Studio](../../ide/reference/visual-studio-commands.md)
- [Janela Comando](../../ide/reference/command-window.md)
- [Caixa Localizar/Comando](../../ide/find-command-box.md)
- [Aliases de comando do Visual Studio](../../ide/reference/visual-studio-command-aliases.md)