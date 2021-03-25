---
description: Cria uma cópia de um objeto de dados específico para o avaliador de expressão (EE).
title: 'IPropertyProxyEESide:: ReplaceObject | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::CreateReplacementObject
helpviewer_keywords:
- IPropertyProxyEESide::CreateReplacementObject
ms.assetid: 0cfe79b8-c3f1-48b0-a225-e39dee2c92fe
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 460052ceb9f2f90a5123f4cc646682919f96dc94
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082576"
---
# <a name="ipropertyproxyeesidecreatereplacementobject"></a>IPropertyProxyEESide::CreateReplacementObject
Cria uma cópia de um objeto de dados específico para o avaliador de expressão (EE).

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CreateReplacementObject(
   IEEDataStorage*  dataIn,
   IEEDataStorage** dataOut
);
```

```csharp
int CreateReplacementObject(
   IEEDataStorage     dataIn,
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>Parâmetros
`dataIn`\
no Um objeto [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) que contém os dados a serem copiados.

`dataOut`\
fora Retorna um novo `IEEDataStorage` objeto.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método recebe um objeto [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) que representa uma matriz de bytes. Esse objeto de dados de entrada normalmente não é implementado pelo EE. No entanto, o objeto retornado por esse método é sempre implementado pelo EE, o que permite que o EE implemente a `IEEDataStorage` interface em qualquer classe desejada.

 Observe que os dados fornecidos pelo objeto de entrada `IEEDataStorage` devem ser os mesmos dados no objeto de saída `IEEDataStorage` .

## <a name="see-also"></a>Confira também
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
