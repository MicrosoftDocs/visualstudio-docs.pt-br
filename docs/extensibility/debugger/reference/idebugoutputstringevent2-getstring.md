---
title: IDebugOutputStringEvent2::GetString | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugOutputStringEvent2::GetString
helpviewer_keywords:
- IDebugOutputStringEvent2::GetString
ms.assetid: f059f8e0-ad44-49ac-ba90-73576ada5e06
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c38b091a3a69752a31625d111cdc6725e806e7b1
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66317171"
---
# <a name="idebugoutputstringevent2getstring"></a>IDebugOutputStringEvent2::GetString
Obtém a mensagem que pode ser exibida.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetString( 
   BSTR* pbstrString
);
```

```csharp
int GetString( 
   out string pbstrString
);
```

## <a name="parameters"></a>Parâmetros
`pbstrString`\
[out] Retorna a mensagem que pode ser exibida.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Consulte também
- [IDebugOutputStringEvent2](../../../extensibility/debugger/reference/idebugoutputstringevent2.md)