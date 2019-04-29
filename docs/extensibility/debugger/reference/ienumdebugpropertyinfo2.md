---
title: IEnumDebugPropertyInfo2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugPropertyInfo2
helpviewer_keywords:
- IEnumDebugPropertyInfo2
ms.assetid: fdea8262-40b8-473e-88ba-639e4c4648e6
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0fb43da8cf5d9ce361dd3eeff2a76b2ed092e67e
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62914114"
---
# <a name="ienumdebugpropertyinfo2"></a>IEnumDebugPropertyInfo2
Essa interface enumera [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) estruturas.

## <a name="syntax"></a>Sintaxe

```
IEnumDebugPropertyInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>Observações para implementadores
 O mecanismo de depuração (DES) implementa essa interface para representar informações para uma determinada propriedade.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) para obter essa interface que representa os filhos de uma propriedade específica. Chame [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md) para obter essa interface que representa as propriedades de um registro de ativação específico.

## <a name="methods-in-vtable-order"></a>Métodos na ordem de Vtable
 A tabela a seguir mostra os métodos de `IEnumDebugPropertyInfo2`.

|Método|Descrição|
|------------|-----------------|
|[Avançar](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-next.md)|Recupera um número especificado de [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) estruturas em uma sequência de enumeração.|
|[Skip](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-skip.md)|Ignora um número especificado de [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) estruturas em uma sequência de enumeração.|
|[Reiniciar](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-reset.md)|Redefine uma sequência de enumeração para o início.|
|[Clonar](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração que o enumerador atual.|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)|Obtém o número de [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) estruturas em um enumerador.|

## <a name="remarks"></a>Comentários
 Em geral, uma propriedade é uma hierarquia de informações que podem incluir um nome, o valor, o endereço e o tipo, bem como quaisquer outras informações apropriadas para o quadro de pilha ou objeto de propriedade associada. Ver [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md) para obter mais detalhes.

## <a name="requirements"></a>Requisitos
 Header: msdbg.h

 Namespace: Microsoft.VisualStudio.Debugger.Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Consulte também
- [Principais interfaces](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
- [EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)