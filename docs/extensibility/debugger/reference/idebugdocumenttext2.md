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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: eb1c5928362616466985a6f88102ffcbf4377444
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102154204"
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
