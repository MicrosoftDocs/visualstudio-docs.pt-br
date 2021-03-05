---
description: Obtém o nome do documento em uma de várias formas.
title: 'IDebugDocument2:: GetName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocument2::GetName
helpviewer_keywords:
- IDebugDocument2::GetName
ms.assetid: 6f09ff09-b0cf-4472-8fc8-143991f0ceb1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1b68fb60cb13d88941b21f6625e6cc0e38ceeda4
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166535"
---
# <a name="idebugdocument2getname"></a>IDebugDocument2::GetName
Obtém o nome do documento em uma de várias formas.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetName( 
   GETNAME_TYPE gnType,
   BSTR*        pbstrFileName
);
```

```csharp
int GetName( 
   enum_GETNAME_TYPE gnType,
   out string        pbstrFileName
);
```

## <a name="parameters"></a>Parâmetros
`gnType`\
no Um valor da enumeração [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md) que determina o tipo de nome a ser retornado.

`pbstrFileName`\
fora Retorna uma cadeia de caracteres que contém o nome do documento.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método pode, por exemplo, retornar o nome do documento como um título ou um nome de arquivo ou até mesmo parte de um nome de arquivo.

## <a name="see-also"></a>Confira também
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
- [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md)
