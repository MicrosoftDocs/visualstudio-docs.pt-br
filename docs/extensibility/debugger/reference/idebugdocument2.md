---
description: Essa interface representa um documento de origem.
title: IDebugDocument2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocument2
helpviewer_keywords:
- IDebugDocument2 interface
ms.assetid: 1bc58426-dbf5-4471-9aad-9d66cd80eef0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 96bf5821cb463b8a99f7376cb99b81ab8cae2206
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167341"
---
# <a name="idebugdocument2"></a>IDebugDocument2
Essa interface representa um documento de origem.

## <a name="syntax"></a>Sintaxe

```
IDebugDocument2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] normalmente implementa essa interface. Um mecanismo DE depuração (DE) também pode implementar essa interface quando precisa fornecer o código-fonte e a origem não existe no disco.  Nesses casos, o DE também implementará as interfaces [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) e [IDebugActivateDocumentEvent2](../../../extensibility/debugger/reference/idebugactivatedocumentevent2.md) , bem como alguns métodos adicionais nas interfaces [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) e [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md) .

## <a name="notes-for-callers"></a>Observações para chamadores
 Os métodos nas `IDebugDocumentContext2` interfaces,, `IDebugDisassemblyStream2` `IDebugDocumentPosition2` e `IDebugActivateDocumentEvent2` retornam essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugDocument2` .

|Método|Descrição|
|------------|-----------------|
|[GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)|Obtém o nome do documento em uma de várias formas.|
|[GetDocumentClassID](../../../extensibility/debugger/reference/idebugdocument2-getdocumentclassid.md)|Obtém o identificador de classe do documento.|

## <a name="remarks"></a>Comentários
 Essa interface é implementada somente quando a DE fornece o código-fonte. Por exemplo, quando você está depurando o script em uma página HTML, o DE fornece o código-fonte, pois a origem é baixada ou gerada dinamicamente e não existe como um arquivo de disco. Ao depurar linguagens tradicionais, como C++, essa interface não precisa ser implementada.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IsPositionInDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-ispositionindocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugactivatedocumentevent2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentcontext2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdocumentposition2-getdocument.md)
- [GetDocument](../../../extensibility/debugger/reference/idebugdisassemblystream2-getdocument.md)
