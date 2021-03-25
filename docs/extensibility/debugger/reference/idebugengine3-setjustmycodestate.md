---
description: Esse método informa ao mecanismo de depuração sobre as informações de estado do JustMyCode.
title: 'IDebugEngine3:: SetJustMyCodeState | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::SetJustMyCodeState
helpviewer_keywords:
- IDebugEngine3::SetJustMyCodeState
ms.assetid: 8ec17fbf-df93-424a-b2ed-fd1e5ee51256
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6e527dbaeb9c04171bf26ea00e550eac336ac6a8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105066111"
---
# <a name="idebugengine3setjustmycodestate"></a>IDebugEngine3::SetJustMyCodeState
Esse método informa ao mecanismo de depuração sobre as informações de estado do JustMyCode.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetJustMyCodeState(
   BOOL           fUpdate,
   DWORD          dwModules,
   JMC_CODE_SPEC* rgJMCSpec
);
```

```csharp
int SetJustMyCodeState(
   int             fUpdate,
   uint            dwModules,
   JMC_CODE_SPEC[] rgJMCSpec
);
```

## <a name="parameters"></a>Parâmetros
`fUpdate`\
no Diferente de zero ( `TRUE` ) para atualizar as informações atuais, zero ( `FALSE` ) para redefinir todas as informações (ignorando qualquer coisa definida anteriormente).

`dwModules`\
no Número de estruturas de informações em `rgJMCSpec.`

`rgJMCSpec`\
no Matriz de estruturas de [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md) a serem usadas.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna o código de erro.

## <a name="remarks"></a>Comentários
 JustMyCode é o conceito de depuração apenas do código que pertence a um usuário e ignorando todo o código intermediário, como código do sistema, mesmo se o código-fonte estiver disponível para esse código do sistema.

## <a name="see-also"></a>Confira também
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
- [JMC_CODE_SPEC](../../../extensibility/debugger/reference/jmc-code-spec.md)
