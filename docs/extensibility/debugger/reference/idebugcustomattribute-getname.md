---
description: Obtém o nome do atributo personalizado.
title: 'IDebugCustomAttribute:: GetName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetName
helpviewer_keywords:
- IDebugCustomAttribute::GetName
ms.assetid: ba509cc5-5816-4925-a094-4c72d88c360c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 313408639b0a93faef0c63c0add92dc1ca2e947b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102163051"
---
# <a name="idebugcustomattributegetname"></a>IDebugCustomAttribute::GetName
Obtém o nome do atributo personalizado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetName( 
   BSTR* bstrName
);
```

```csharp
int GetName(
   out string bstrName
);
```

## <a name="parameters"></a>Parâmetros
`bstrName`\
fora Retorna uma cadeia de caracteres que contém o nome do atributo personalizado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará S_OK; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O nomeado retornado por esse método corresponde ao nome da classe usada para declarar o atributo. Isso pode não corresponder exatamente ao nome da própria classe de atributo personalizado, pois C# permite que o sufixo "Attribute" seja Descartado de um nome de atributo personalizado quando ele é usado em uma declaração.

## <a name="see-also"></a>Confira também
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
