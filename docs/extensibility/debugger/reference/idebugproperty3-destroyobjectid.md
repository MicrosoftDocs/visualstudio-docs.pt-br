---
description: Destrói a ID exclusiva associada a essa propriedade, indicando que o chamador não se importa mais para identificar essa propriedade exclusivamente de todas as outras propriedades.
title: IDebugProperty3::D estroyObjectID | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty3::DestroyObjectID
helpviewer_keywords:
- IDebugProperty3::DestroyObjectID
ms.assetid: bd08f356-cc67-4717-98c9-c3d00cad2040
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 071af90af5fe22d6f6cfa662458be660edc5d39f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064820"
---
# <a name="idebugproperty3destroyobjectid"></a>IDebugProperty3::DestroyObjectID
Destrói a ID exclusiva associada a essa propriedade, indicando que o chamador não se importa mais para identificar essa propriedade exclusivamente de todas as outras propriedades.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT DestroyObjectID(
   void
);
```

```csharp
int DestroyObjectID();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Se o mecanismo de depuração não precisar dar suporte a IDs exclusivas para uma propriedade (porque ela já as acompanha exclusivamente internamente), ela poderá simplesmente retornar `E_NOTIMPL` para esse método.

 As IDs exclusivas são criadas com uma chamada para o método [Createobjectid](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md) quando o chamador deseja certificar-se de que essa propriedade é identificada exclusivamente entre todas as outras propriedades.

## <a name="see-also"></a>Confira também
- [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)
- [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)
