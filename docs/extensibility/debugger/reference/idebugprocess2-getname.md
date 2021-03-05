---
description: Obtém o título, o nome amigável ou o nome do arquivo do processo.
title: 'IDebugProcess2:: GetName | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetName
helpviewer_keywords:
- IDebugProcess2::GetName
ms.assetid: a2f66ab5-53e5-4cdc-a1b5-3b8afa8ee646
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 418da1be71b0299c93f2813397c28144425f81a4
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102164755"
---
# <a name="idebugprocess2getname"></a>IDebugProcess2::GetName
Obtém o título, o nome amigável ou o nome do arquivo do processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetName( 
   GETNAME_TYPE  gnType,
   BSTR*         pbstrName
);
```

```csharp
int GetName( 
   enum_GETNAME_TYPE  gnType,
   out string         pbstrName
);
```

## <a name="parameters"></a>Parâmetros
`gnType`\
no Um valor da enumeração [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md) que especifica o tipo de nome a ser retornado.

`pbstrName`\
fora Retorna o nome do processo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [GETNAME_TYPE](../../../extensibility/debugger/reference/getname-type.md)
