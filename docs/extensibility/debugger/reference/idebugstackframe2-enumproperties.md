---
description: Cria um enumerador para propriedades associadas ao registro de ativação, como variáveis locais.
title: 'IDebugStackFrame2:: EnumProperties | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2::EnumProperties
helpviewer_keywords:
- IDebugStackFrame2::EnumProperties
ms.assetid: 334bb95e-c7e0-4008-9f06-8c3999e47ee8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: bd9494434a8dc3fa2cff9eb28ddea8fb48302ca6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071149"
---
# <a name="idebugstackframe2enumproperties"></a>IDebugStackFrame2::EnumProperties
Cria um enumerador para propriedades associadas ao registro de ativação, como variáveis locais.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumProperties ( 
   DEBUGPROP_INFO_FLAGS      dwFieldSpec,
   UINT                      nRadix,
   REFIID                    refiid,
   DWORD                     dwTimeout,
   ULONG*                    pcelt,
   IEnumDebugPropertyInfo2** ppEnum
);
```

```csharp
int EnumProperties ( 
   enum_DEBUGPROP_INFO_FLAGS   dwFieldSpec,
   uint                        nRadix,
   ref Guid                    refiid,
   uint                        dwTimeout,
   out uint                    pcelt,
   out IEnumDebugPropertyInfo2 ppEnum
);
```

## <a name="parameters"></a>Parâmetros
`dwFieldSpec`\
no Uma combinação de sinalizadores da enumeração [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) que especifica quais campos nas estruturas de [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) enumeradas devem ser preenchidos.

`nRadix`\
no A base a ser usada na formatação de qualquer informação numérica.

`refiid`\
no Um GUID de um filtro usado para selecionar quais estruturas de [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) devem ser enumeradas, como `guidFilterLocals` .

`dwTimeout`\
no Tempo máximo, em milissegundos, a aguardar antes de retornar deste método. Use `INFINITE` para aguardar indefinidamente.

`pcelt`\
fora Retorna o número de propriedades enumeradas. Isso é o mesmo que chamar o método [GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md) .

`ppEnum`\
fora Retorna um objeto [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md) que contém uma lista das propriedades desejadas.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Como esse método permite que todas as propriedades selecionadas sejam recuperadas com uma única chamada, ela é mais rápida do que chamar sequencialmente os métodos [Getdebugproperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md) e [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md) .

## <a name="see-also"></a>Confira também
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IEnumDebugPropertyInfo2](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2.md)
- [GetCount](../../../extensibility/debugger/reference/ienumdebugpropertyinfo2-getcount.md)
- [GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
