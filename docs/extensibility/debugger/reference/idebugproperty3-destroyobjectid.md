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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fa3712a12440f5d177f54544110bc8fa5d2e03ac
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166691"
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
