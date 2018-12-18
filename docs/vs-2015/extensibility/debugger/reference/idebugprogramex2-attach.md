---
title: IDebugProgramEx2::Attach | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugProgramEx2::Attach
helpviewer_keywords:
- IDebugProgramEx2::Attach
ms.assetid: 33b22b2f-431e-4205-9441-d28a9c928c97
caps.latest.revision: 14
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: ea96fab360df7b23090ba93918a5bff60a31ea32
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51751098"
---
# <a name="idebugprogramex2attach"></a>IDebugProgramEx2::Attach
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Anexe uma sessão em um programa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT Attach(   
   IDebugEventCallback2* pCallback,  
   DWORD                 dwReason,  
   IDebugSession2*       pSession  
);  
```  
  
```  
[C#]  
int Attach(   
   IDebugEventCallback2 pCallback,  
   uint                 dwReason,  
   IDebugSession2       pSession  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pCallback`  
 [in] Uma [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) objeto que representa a função de retorno de chamada que o mecanismo de depuração anexado envia eventos para.  
  
 `dwReason`  
 [in] Um valor a partir de [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) enumeração que descreve o motivo para a operação de anexação.  
  
 `pSession`  
 [in] Um valor que identifica exclusivamente a sessão que está sendo anexado ao programa.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retornará um código de erro. Esse método deverá retornar `E_ATTACH_DEBUGGER_ALREADY_ATTACHED` se o programa já está anexado.  
  
## <a name="remarks"></a>Comentários  
 A porta que contém o programa pode usar o valor em `pSession` para determinar qual sessão está tentando anexar ao programa. Por exemplo, se uma porta permite que a sessão de depuração somente uma anexar a um processo por vez, a porta pode determinar se a mesma sessão já está anexada a outros programas no processo.  
  
> [!NOTE]
>  A interface passado `pSession` deve ser tratada apenas como um cookie, um valor que identifica exclusivamente o Gerenciador de sessão de depuração anexar a este programa; nenhum dos métodos na interface fornecido são funcionais.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)

