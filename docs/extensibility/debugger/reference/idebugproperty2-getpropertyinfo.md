---
description: Obtém a estrutura de DEBUG_PROPERTY_INFO que descreve uma propriedade.
title: 'IDebugProperty2:: GetPropertyInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetPropertyInfo
helpviewer_keywords:
- IDebugProperty2::GetPropertyInfo
ms.assetid: 39d6e942-df72-4c84-a5d9-a386d112714c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f0a897071453886f16fd5e40e2f27b7bd100616b
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064731"
---
# <a name="idebugproperty2getpropertyinfo"></a>IDebugProperty2::GetPropertyInfo
Obtém a estrutura de [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) que descreve uma propriedade.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetPropertyInfo ( 
   DEBUGPROP_INFO_FLAGS dwFields,
   DWORD                nRadix,
   DWORD                dwTimeout,
   IDebugReference2**   rgpArgs,
   DWORD                dwArgCount,
   DEBUG_PROPERTY_INFO* pPropertyInfo
);
```

```cpp
int GetPropertyInfo ( 
   enum_DEBUGPROP_INFO_FLAGS dwFields,
   uint                      nRadix,
   uint                      dwTimeout,
   IDebugReference2[]        rgpArgs,
   uint                      dwArgCount,
   DEBUG_PROPERTY_INFO[]     pPropertyInfo
);
```

## <a name="parameters"></a>Parâmetros
`dwFields`\
no Uma combinação de valores da enumeração [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md) que especifica quais campos devem ser preenchidos na `pPropertyInfo` estrutura.

`nRadix`\
no Base a ser usada na formatação de qualquer informação numérica.

`dwTimeout`\
no Especifica o tempo máximo, em milissegundos, a aguardar antes de retornar desse método. Use `INFINITE` para aguardar indefinidamente.

`rgpArgs`\
[entrada, saída] Reservado para uso futuro; Defina como um valor nulo.

`dwArgCount`\
no Reservado para uso futuro; definido como zero.

`pPropertyInfo`\
fora Uma estrutura de [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md) que é preenchida com a descrição da propriedade.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna o código de erro.

## <a name="see-also"></a>Confira também
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [DEBUGPROP_INFO_FLAGS](../../../extensibility/debugger/reference/debugprop-info-flags.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
