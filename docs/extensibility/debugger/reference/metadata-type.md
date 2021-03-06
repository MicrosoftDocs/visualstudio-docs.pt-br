---
description: Essa estrutura especifica informações sobre um tipo de campo extraído dos metadados.
title: METADATA_TYPE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- METADATA_TYPE
helpviewer_keywords:
- METADATA_TYPE structure
ms.assetid: 2d8b78f6-0aef-4d79-809a-cff9b2c24659
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c8f0c8341213dfbe15dcf9a6f5a5fc421c0ebab3
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102225481"
---
# <a name="metadata_type"></a>METADATA_TYPE
Essa estrutura especifica informações sobre um tipo de campo extraído dos metadados.

## <a name="syntax"></a>Sintaxe

```cpp
typedef struct _tagTYPE_METADATA {
   ULONG32  ulAppDomainID;
   GUID     guidModule;
   _mdToken tokClass;
} METADATA_TYPE;
```

```csharp
public struct METADATA_TYPE {
   public uint ulAppDomainID;
   public Guid guidModule;
   public int  tokClass;
};
```

## <a name="parameters"></a>Parâmetros
 `ulAppDomainID`\
 ID do aplicativo do qual o símbolo veio. Isso é usado para identificar exclusivamente uma instância do aplicativo.

 `guidModule`\
 O GUID do módulo que contém este campo.

 `tokClass`\
 A ID do token de metadados deste tipo.

 [C++] `_mdToken` é um `typedef` para um de 32 bits `int` .

## <a name="remarks"></a>Comentários
 Essa estrutura aparece como parte da União na estrutura [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) quando o `dwKind` campo da `TYPE_INFO` estrutura é definido como `TYPE_KIND_METADATA` (um valor da enumeração [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) ).

 O `tokClass` valor é um token de metadados que identifica exclusivamente um tipo. Para obter detalhes sobre como interpretar os bits superiores da ID do token de metadados, consulte a `CorTokenType` enumeração no arquivo corhdr. h no SDK do .NET Framework.

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Estruturas e uniões](../../../extensibility/debugger/reference/structures-and-unions.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
- [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
