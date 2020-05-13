---
title: IDebugPortSupplier2:AddPort | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortSupplier2::AddPort
helpviewer_keywords:
- IDebugPortSupplier2::AddPort
ms.assetid: df491161-6bf3-4fcc-b478-b9ec88ec995f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 00954ceaa0ddd750a3d08e372d1edaa1905f01c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724741"
---
# <a name="idebugportsupplier2addport"></a>IDebugPortSupplier2::AddPort
Adiciona um porto.

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

## <a name="parameters"></a>parâmetros
`pRequest`\
[em] Um objeto [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md) que descreve a porta a ser adicionada.

`ppPort`\
[fora] Retorna um objeto [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) que representa a porta.

## <a name="return-value"></a>Valor retornado
 Se for `S_OK`bem sucedido, retorna; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método realmente cria a porta solicitada, bem como a adiciona à lista interna de portas ativas do fornecedor de portas. O método [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md) pode ser chamado primeiro para evitar possíveis atrasos demorados.

## <a name="see-also"></a>Confira também
- [IDebugPortSupplier2](../../../extensibility/debugger/reference/idebugportsupplier2.md)
- [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
- [CanAddPort](../../../extensibility/debugger/reference/idebugportsupplier2-canaddport.md)
