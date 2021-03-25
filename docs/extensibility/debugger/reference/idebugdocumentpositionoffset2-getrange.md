---
description: Recupera o intervalo para a posição atual do documento.
title: 'IDebugDocumentPositionOffset2:: GetRange | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugDocumentPositionOffset2::GetRange
ms.assetid: 27da7130-0932-4f97-abde-05e6fb018606
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 66184ba67dd0623a886ca37e28d311aebc6633bd
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066341"
---
# <a name="idebugdocumentpositionoffset2getrange"></a>IDebugDocumentPositionOffset2::GetRange
Recupera o intervalo para a posição atual do documento.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetRange(
   DWORD* pdwBegOffset,
   DWORD* pdwEndOffset
);
```

```csharp
public int GetRange(
   ref uint pdwBegOffset,
   ref uint pdwEndOffset
);
```

## <a name="parameters"></a>Parâmetros
`pdwBegOffset`\
[entrada, saída] Deslocamento da posição inicial do intervalo. Defina esse parâmetro como um valor nulo se essas informações não forem necessárias.

`pdwEndOffset`\
[entrada, saída] Deslocamento da posição final do intervalo. Defina esse parâmetro como um valor nulo se essas informações não forem necessárias.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O intervalo especificado em uma posição de documento para um ponto de interrupção de local é usado pelo mecanismo de depuração (DE) para pesquisar antecipadamente por uma instrução que realmente contribui com código. Por exemplo, considere o seguinte código:

```
Line 5: // comment
Line 6: x = 1;
```

 A linha 5 contribui com nenhum código para o programa que está sendo depurado. Se o depurador que define o ponto de interrupção na linha 5 desejar que o DE Pesquisar em um determinado valor para a primeira linha que contribui com o código, o depurador especificaria um intervalo que inclui linhas candidatas adicionais em que um ponto de interrupção pode ser colocado corretamente. Em seguida, a pesquisa avançará essas linhas até encontrar uma linha que poderia aceitar um ponto de interrupção.

## <a name="see-also"></a>Confira também
- [IDebugDocumentPositionOffset2](../../../extensibility/debugger/reference/idebugdocumentpositionoffset2.md)
- [GetRange](../../../extensibility/debugger/reference/idebugdocumentposition2-getrange.md)
