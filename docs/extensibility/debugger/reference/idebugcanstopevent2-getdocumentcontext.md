---
description: Obtém o contexto do documento que descreve o local desse evento.
title: 'IDebugCanStopEvent2:: GetDocumentContext | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetDocumentContext
helpviewer_keywords:
- IDebugCanStopEvent2::GetDocumentContext
ms.assetid: 936a6c4e-30c5-4c7e-9ad5-910cc605a4b5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 44e1f2aa918547d8b3b0b1bea1940072fe2d8f84
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085072"
---
# <a name="idebugcanstopevent2getdocumentcontext"></a>IDebugCanStopEvent2::GetDocumentContext
Obtém o contexto do documento que descreve o local desse evento.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetDocumentContext ( 
   IDebugDocumentContext2** ppDocCxt
);
```

```csharp
int GetDocumentContext ( 
   out IDebugDocumentContext2 ppDocCxt
);
```

## <a name="parameters"></a>Parâmetros
`ppDocCxt`\
fora Retorna a interface [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) que representa uma posição em um documento de arquivo de origem correspondente ao local do código atual.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Em geral, o contexto do documento pode ser considerado como uma posição em um arquivo de origem.

 Para obter o contexto do código, que é orientado para instruções de código, chame o método [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md) .

## <a name="see-also"></a>Confira também
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)
