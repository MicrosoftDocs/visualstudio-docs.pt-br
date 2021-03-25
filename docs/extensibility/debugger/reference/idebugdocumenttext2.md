---
description: Essa interface representa um documento de texto.
title: IDebugDocumentText2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2
helpviewer_keywords:
- IDebugDocumentText2 interface
ms.assetid: e85f50a3-211c-4220-a9f4-789950ba2782
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 557ae68e63280348ab315c3240e05dbfc38a8d4d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066276"
---
# <a name="idebugdocumenttext2"></a>IDebugDocumentText2
Essa interface representa um documento de texto.

## <a name="syntax"></a>Sintaxe

```
IDebugDocumentText2 : IDebugDocument2
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um mecanismo DE depuração (DE) implementa essa interface quando o código-fonte que ele precisa fornecer está na forma de texto. Como esse é o caso mais comum, se um DE implementa a interface [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) , ele também deve implementar a `IDebugDocumentText2` interface.

## <a name="notes-for-callers"></a>Observações para chamadores
 Use o `QueryInterface` método para obter essa interface de uma `IDebugDocument2` interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos na `IDebugDocument2` interface, essa interface implementa os seguintes métodos:

|Método|Descrição|
|------------|-----------------|
|[GetSize](../../../extensibility/debugger/reference/idebugdocumenttext2-getsize.md)|Recupera o tamanho do texto nesta posição no documento.|
|[GetText](../../../extensibility/debugger/reference/idebugdocumenttext2-gettext.md)|Recupera o texto da posição especificada no documento.|

## <a name="remarks"></a>Comentários
 Um objeto que implementa essa interface também deve implementar a <xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer> interface, que fornece a <xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint> interface para um objeto [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md) .

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [IDebugDocumentTextEvents2](../../../extensibility/debugger/reference/idebugdocumenttextevents2.md)
