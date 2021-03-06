---
description: Essa estrutura representa um valor de retorno de um método ou função.
title: METADATA_ADDRESS_RETVAL | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_RETVAL
helpviewer_keywords:
- METADATA_ADDRESS_RETVAL structure
ms.assetid: 5b0ec0fb-84b3-4ce7-8e24-becf3d881d7d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d727771128e161eed77bf78091c8e0dadcc20ee6
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102225544"
---
# <a name="metadata_address_retval"></a>METADATA_ADDRESS_RETVAL
Essa estrutura representa um valor de retorno de um método ou função.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _tagMETADATA_ADDRESS_RETVAL {
   _mdToken tokMethod;
   DWORD    dwCorType;
   DWORD    dwSigSize;
   BYTE     rgSig[10];
} METADATA_ADDRESS_RETVAL;
```

```csharp
public struct METADATA_ADDRESS_RETVAL {
   public int    tokMethod;
   public uint   dwCorType;
   public uint   dwSigSize;
   public byte[] rgSig;
}
```

## <a name="members"></a>Membros
 `tokMethod`\
 A ID do método para o qual esse valor de retorno é.

 `dwCorType`\
 O tipo base do valor de retorno. Esse é um valor da `CorElementType` Enumeração definida no arquivo .NET Framework SDK CorHdr. h.

 `dwSigSize`\
 O tamanho da assinatura do valor de retorno (como armazenado em `rgSig` ).

 `rgSig`\
 Uma matriz de bytes que formam a assinatura do valor de retorno.

## <a name="remarks"></a>Comentários
 Essa estrutura faz parte da União na estrutura de [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) quando o `dwKind` campo da `DEBUG_ADDRESS_UNION` estrutura é definido como `ADDRESS_KIND_RETVAL` (um valor da enumeração [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) ).

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
- [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
