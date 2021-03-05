---
description: Esse método informa ao processo que uma sessão não está mais Depurando o processo.
title: IDebugProcessEx2::D Etach | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::Detach
helpviewer_keywords:
- IDebugProcessEx2::Detach method
ms.assetid: 66d54c2c-9302-47c8-9975-f30ed988ab29
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3140da647b46a1cbc3b60691e820238c2c6c83eb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102166249"
---
# <a name="idebugprocessex2detach"></a>IDebugProcessEx2::Detach
Esse método informa ao processo que uma sessão não está mais Depurando o processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Detach( 
   IDebugSession2* pSession
);
```

```csharp
int Detach(
   IDebugSession2 pSession
);
```

## <a name="parameters"></a>Parâmetros
`pSession`\
no Um valor que identifica exclusivamente a sessão da qual desanexar esse processo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 A interface passada deve `pSession` ser tratada apenas como um cookie, um valor que identifica exclusivamente o Gerenciador de depuração de sessão que foi anexado originalmente a esse processo; nenhum dos métodos na interface fornecida é funcional.

## <a name="see-also"></a>Confira também
- [IDebugProcessEx2](../../../extensibility/debugger/reference/idebugprocessex2.md)
