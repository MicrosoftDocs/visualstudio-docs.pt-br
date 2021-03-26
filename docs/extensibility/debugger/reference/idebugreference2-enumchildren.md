---
description: Obter uma lista de filhos selecionados de uma referência.
title: 'IDebugReference2:: EnumChildren | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::EnumChildren
helpviewer_keywords:
- IDebugReference2::EnumChildren
ms.assetid: 35b3c2f3-69f4-4013-b555-f847221f62e8
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 92f55f511a68cca6685579eeb6d686108bf70799
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105071448"
---
# <a name="idebugreference2enumchildren"></a>IDebugReference2::EnumChildren
Obter uma lista de filhos selecionados de uma referência. Reservado para uso futuro.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT EnumChildren ( 
   DEBUGREF_INFO_FLAGS        dwFields,
   DWORD                      dwRadix,
   DBG_ATTRIB_FLAGS           dwAttribFilter,
   LPCOLESTR                  pszNameFilter,
   DWORD                      dwTimeout,
   IEnumDebugReferenceInfo2** ppEnum
);
```

```csharp
int EnumChildren ( 
   enum_DEBUGREF_INFO_FLAGS     dwFields,
   uint                         dwRadix,
   enum_DBG_ATTRIB_FLAGS        dwAttribFilter,
   string                       pszNameFilter,
   uint                         dwTimeout,
   out IEnumDebugReferenceInfo2 ppEnum
);
```

## <a name="parameters"></a>Parâmetros
`dwFields`\
no Uma combinação de sinalizadores da enumeração [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md) que especifica quais campos nas estruturas de [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) enumeradas devem ser preenchidos.

`dwRadix`\
no A base a ser usada na formatação de qualquer informação numérica.

`dwAttribFilter`\
no Uma combinação de sinalizadores da enumeração [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) que é usada como um filtro em combinação com o `pszNameFilter` parâmetro para selecionar quais estruturas devem ser enumeradas.

`pszNameFilter`\
no Uma cadeia de caracteres que especifica um filtro, como "MyX", usada em combinação com o `dwAttribFilter` parâmetro para selecionar as estruturas a serem enumeradas.

`dwTimeout`\
no Tempo máximo, em milissegundos, a aguardar antes de retornar deste método. Use `INFINITE` para aguardar indefinidamente.

`ppEnum`\
fora Retorna um objeto [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md) que contém uma lista das propriedades filho solicitadas.

## <a name="return-value"></a>Valor Retornado
 Sempre retorna `E_NOTIMPL`.

## <a name="see-also"></a>Confira também
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)
- [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
