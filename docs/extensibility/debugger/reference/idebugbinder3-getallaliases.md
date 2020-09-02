---
title: 'IDebugBinder3:: GetAllAliases | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetAllAliases
helpviewer_keywords:
- IDebugBinder3::GetAllAliases method
ms.assetid: 1f9ab2ee-2ab3-4a61-8b99-95dd7fdf3511
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2d512fa6eb7529e11c766d7c173b318aa6f8f2f5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80735812"
---
# <a name="idebugbinder3getallaliases"></a>IDebugBinder3::GetAllAliases
Esse método recupera uma lista de aliases do programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetAllAliases(
   UINT          uRequest,
   IDebugAlias** ppAliases,
   UINT*         puFetched
);
```

```csharp
int GetAllAliases(
   uint          uRequest,
   IDebugAlias[] ppAliases,
   out uint      puFetched
);
```

## <a name="parameters"></a>Parâmetros
`uRequest`\
no O número máximo de aliases a serem retornados (especifica o comprimento da matriz passada `ppAliases` ).

`ppAliases`\
[entrada, saída] Matriz para preencher com aliases (se esse for um valor nulo e `uRequest` for 0, a contagem de aliases que podem ser retornados será retornada por `puFetched` ).

`puFetched`\
fora Retorna o número de aliases obtidos.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
