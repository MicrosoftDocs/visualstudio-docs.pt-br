---
description: Atualiza os dados do objeto com o objeto de dados fornecido e retorna um novo objeto de dados que representa os novos dados do objeto.
title: 'IPropertyProxyEESide:: InPlaceUpdateObject | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
helpviewer_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
ms.assetid: abf89411-1853-4f23-b244-d5e0afa197b1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6fb6c098d26148db39493b25f199c6819fb81d27
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105082407"
---
# <a name="ipropertyproxyeesideinplaceupdateobject"></a>IPropertyProxyEESide::InPlaceUpdateObject
Atualiza os dados do objeto com o objeto de dados fornecido e retorna um novo objeto de dados que representa os novos dados do objeto.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT InPlaceUpdateObject(
   [in] IEEDataStorage*   dataIn,
   [out] IEEDataStorage** dataOut
);
```

```csharp
int InPlaceUpdateObject(
   IEEDataStorage     dataIn,
   out IEEDataStorage dataOut
);
```

## <a name="parameters"></a>Parâmetros
`dataIn`\
no Um objeto [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) que contém os novos dados.

`dataOut`\
fora Retorna um novo `IEEDataStorage` objeto que contém os dados substituídos.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método, na verdade, atualiza os dados do objeto. Os dados no objeto [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md) retornado não precisam ser iguais aos dados no objeto de entrada `IEEDataStorage` , mas o objeto retornado deve refletir o valor atual da propriedade.

 O objeto de dados de entrada normalmente não é implementado pelo EE. No entanto, o objeto retornado por esse método é sempre implementado pelo EE, o que permite que o EE implemente a `IEEDataStorage` interface em qualquer classe desejada.

 O método [ReplaceObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md) cria um objeto de dados com base no objeto de dados de entrada, mas não afeta os dados originais da propriedade.

## <a name="see-also"></a>Confira também
- [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)
- [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
- [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)
