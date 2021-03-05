---
description: Essa interface representa uma coleção de objetos que implementam a interface IDebugAddress.
title: IEnumDebugAddresses | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugAddresses
helpviewer_keywords:
- IEnumDebugAddresses interface
ms.assetid: 5f6f6751-e6d8-4c5a-8e81-414b6e5d8cc5
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ea9e4115c1664e1dcd05041f7ece056b5de01dae
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222634"
---
# <a name="ienumdebugaddresses"></a>IEnumDebugAddresses
Essa interface representa uma coleção de objetos que implementam a interface [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) .

## <a name="syntax"></a>Sintaxe

```
IEnumDebugAdresses : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada pelo provedor de símbolos para fornecer conjuntos de objetos que implementam a interface [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) . Observe que essa não é uma enumeração COM padrão devido à presença do método [GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md) .

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é retornada por [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md) e [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md).

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Essa interface implementa os métodos a seguir.

|Método|Descrição|
|------------|-----------------|
|[Próximo](../../../extensibility/debugger/reference/ienumdebugaddresses-next.md)|Recupera o próximo conjunto de objetos [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) da enumeração.|
|[Skip](../../../extensibility/debugger/reference/ienumdebugaddresses-skip.md)|Ignora um número especificado de entradas.|
|[Redefinir](../../../extensibility/debugger/reference/ienumdebugaddresses-reset.md)|Redefine a enumeração para a primeira entrada.|
|[8i](../../../extensibility/debugger/reference/ienumdebugaddresses-clone.md)|Recupera uma cópia da enumeração atual.|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugaddresses-getcount.md)|Recupera o número de entradas na enumeração.|

## <a name="remarks"></a>Comentários
 Essa interface é normalmente usada pelo mecanismo de depuração para ajudar a determinar o endereço apropriado para dar ao avaliador de expressão.

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces de provedor de símbolos](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
- [GetAddressesFromContext](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromcontext.md)
- [GetAddressesFromPosition](../../../extensibility/debugger/reference/idebugsymbolprovider-getaddressesfromposition.md)
