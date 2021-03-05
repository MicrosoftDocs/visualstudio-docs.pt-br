---
description: Adiciona uma porta.
title: 'IDebugPortSupplier2:: AddPort | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::AddPort
helpviewer_keywords:
- IDebugPortSupplier2::AddPort
ms.assetid: df491161-6bf3-4fcc-b478-b9ec88ec995f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 14232ac49b3862c635a41c25e79c7ab166fa24ef
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169230"
---
# <a name="idebugportsupplier2addport"></a>IDebugPortSupplier2::AddPort
Adiciona uma porta.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT AddPort( 
   IDebugPortRequest2* pRequest,
   IDebugPort2**       ppPort
);
```

```csharp
int AddPort( 
   IDebugPortRequest2 pRequest,
   out IDebugPort2    ppPort
);
```

## <a name="parameters"></a>Parâmetros
`pRequest`\
no Um objeto [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) que descreve a porta a ser adicionada.

`ppPort`\
fora Retorna um objeto [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) que representa a porta.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método cria, na verdade, a porta solicitada, além de adicioná-la à lista interna de portas ativas do fornecedor da porta. O método [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) pode ser chamado primeiro para evitar possíveis atrasos demorados.

## <a name="see-also"></a>Confira também
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)
