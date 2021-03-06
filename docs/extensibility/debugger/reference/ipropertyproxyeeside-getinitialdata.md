---
description: Retorna os dados iniciais deste objeto.
title: 'IPropertyProxyEESide:: GetInitialData | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::GetInitialData
helpviewer_keywords:
- IPropertyProxyEESide::GetInitialData
ms.assetid: 36cceb19-2604-4ef9-b42b-5dd30cbe24b1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 433354dc4dd5c62ffb544e2e05a1ceae76d0335e
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102225715"
---
# <a name="ipropertyproxyeesidegetinitialdata"></a>IPropertyProxyEESide::GetInitialData
Retorna os dados iniciais deste objeto.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetInitialData(
   IEEDataStorage** dataOut
);
```

```csharp
int GetInitialData(
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>Parâmetros
`dataOut`\
fora Retorna um objeto [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) que contém os dados iniciais deste objeto.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
