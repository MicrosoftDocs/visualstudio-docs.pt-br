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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c5ad25fe6461f1df89ada83623ab4e28194ca207
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076323"
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
