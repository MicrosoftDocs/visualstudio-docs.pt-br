---
description: Esta interface descreve uma porta.
title: IDebugPortRequest2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2
helpviewer_keywords:
- IDebugPortRequest2 interface
ms.assetid: 556e610d-7c4b-44a8-965a-76a9d02b601a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 2ca2d1d59c66c87c2dbb0fc256481d35ad590dbe
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102142615"
---
# <a name="idebugportrequest2"></a>IDebugPortRequest2
Esta interface descreve uma porta. Essa descrição é usada para adicionar a porta a um fornecedor de porta.

## <a name="syntax"></a>Sintaxe

```
IDebugPortRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O Visual Studio normalmente implementa essa interface no processo de obter uma porta de depuração de um fornecedor de porta.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é passada em [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md) para criar uma porta de depuração. Uma chamada para [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md) retorna essa interface, representando a solicitação usada para criar a porta em primeiro lugar.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugPortRequest2` .

|Método|Descrição|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugportrequest2-getportname.md)|Obtém o nome da porta a ser criada.|

## <a name="remarks"></a>Comentários
 Um mecanismo de depuração normalmente não interage com um fornecedor de porta e não terá uso para essa interface.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
- [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)
