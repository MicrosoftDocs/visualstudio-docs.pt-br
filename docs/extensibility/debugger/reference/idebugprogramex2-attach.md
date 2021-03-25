---
description: Anexe uma sessão a um programa.
title: 'IDebugProgramEx2:: Attach | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramEx2::Attach
helpviewer_keywords:
- IDebugProgramEx2::Attach
ms.assetid: 33b22b2f-431e-4205-9441-d28a9c928c97
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f4f7f6a083c37ece73be488ab0c4f6d4c25ce24c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084149"
---
# <a name="idebugprogramex2attach"></a>IDebugProgramEx2::Attach
Anexe uma sessão a um programa.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Attach( 
   IDebugEventCallback2* pCallback,
   DWORD                 dwReason,
   IDebugSession2*       pSession
);
```

```csharp
int Attach( 
   IDebugEventCallback2 pCallback,
   uint                 dwReason,
   IDebugSession2       pSession
);
```

## <a name="parameters"></a>Parâmetros
`pCallback`\
no Um objeto [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) que representa a função de retorno de chamada à qual o mecanismo de depuração anexado envia eventos.

`dwReason`\
no Um valor da enumeração [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) que descreve o motivo da operação de anexação.

`pSession`\
no Um valor que identifica exclusivamente a sessão que está anexando ao programa.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro. Esse método deve retornar `E_ATTACH_DEBUGGER_ALREADY_ATTACHED` se o programa já estiver anexado.

## <a name="remarks"></a>Comentários
 A porta que contém o programa pode usar o valor em `pSession` para determinar qual sessão está tentando anexar ao programa. Por exemplo, se uma porta permitir que apenas uma sessão de depuração seja anexada a um processo por vez, a porta poderá determinar se a mesma sessão já está anexada a outros programas no processo.

> [!NOTE]
> A interface passada deve `pSession` ser tratada apenas como um cookie, um valor que identifica exclusivamente o Gerenciador de depuração de sessão que está anexando a este programa; nenhum dos métodos na interface fornecida é funcional.

## <a name="see-also"></a>Confira também
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
