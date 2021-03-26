---
description: Cria um objeto que representa um tipo primitivo.
title: 'IDebugTypeFieldBuilder:: createprimitive | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- CreatePrimitive
- IDebugTypeFieldBuilder::CreatePrimitive
ms.assetid: 512c6ff0-97c5-409f-939f-4cc969bc4bb9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 60c095080770837b8afe50898cd570894a1130ed
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083551"
---
# <a name="idebugtypefieldbuildercreateprimitive"></a>IDebugTypeFieldBuilder::CreatePrimitive
Cria um objeto que representa um tipo primitivo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT CreatePrimitive (
   DWORD          dwElementType,
   IDebugField ** pTypeField
);
```

```csharp
int CreatePrimitive (
   uint            dwElementType,
   out IDebugField pTypeField
);
```

## <a name="parameters"></a>Parâmetros
`dwElementType`\
no Valor da [enumeração CorElementType](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration) que representa o tipo primitivo.

`pTypeField`\
fora Retorna a interface IDebugField para o novo tipo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugTypeFieldBuilder](../../../extensibility/debugger/reference/idebugtypefieldbuilder.md)
