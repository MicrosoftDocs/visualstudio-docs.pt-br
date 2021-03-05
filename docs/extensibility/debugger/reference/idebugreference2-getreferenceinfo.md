---
description: Obtém a estrutura de DEBUG_REFERENCE_INFO que descreve uma referência.
title: 'IDebugReference2:: GetReferenceInfo | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReference2::GetReferenceInfo
helpviewer_keywords:
- IDebugReference2::GetReferenceInfo
ms.assetid: ae611714-f114-4cf2-b5bb-37461e6ff289
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ef953ccde844ac7a2fb5289affaf381f56af8719
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168918"
---
# <a name="idebugreference2getreferenceinfo"></a>IDebugReference2::GetReferenceInfo
Obtém a estrutura de [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) que descreve uma referência. Reservado para uso futuro.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetReferenceInfo ( 
   DEBUGREF_INFO_FLAGS   dwFields,
   DWORD                 nRadix,
   DWORD                 dwTimeout,
   IDebugReference2**    rgpArgs,
   DWORD                 dwArgCount,
   DEBUG_REFERENCE_INFO* pReferenceInfo
);
```

```csharp
int GetReferenceInfo ( 
   enum_DEBUGREF_INFO_FLAGS  dwFields,
   uint                      nRadix,
   uint                      dwTimeout,
   IDebugReference2[]        rgpArgs,
   uint                      dwArgCount,
   DEBUG_REFERENCE_INFO[]    pReferenceInfo
);
```

## <a name="parameters"></a>Parâmetros
`dwFields`\
no Uma combinação de sinalizadores da enumeração de [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md) que determinam os campos a serem preenchidos na estrutura de [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) .

`nRadix`\
no A base a ser usada na formatação de qualquer informação numérica.

`dwTimeout`\
no Tempo máximo, em milissegundos, a aguardar antes de retornar deste método. Use `INFINITE` para aguardar indefinidamente.

`rgpArgs`\
no Uma matriz de objetos [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) . Reservado para uso futuro; Defina como um valor nulo.

`dwArgCount`\
no O número de argumentos de referência na `rgpArgs` matriz. Reservado para uso futuro; Defina como 0.

`pReferenceInfo`\
fora Uma estrutura de [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) que é preenchida com uma descrição da propriedade.

## <a name="return-value"></a>Valor Retornado
 Sempre retorna `E_NOTIMPL`.

## <a name="see-also"></a>Confira também
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
