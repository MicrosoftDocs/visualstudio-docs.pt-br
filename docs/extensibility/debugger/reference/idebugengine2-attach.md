---
title: IDebugEngine2::Attach | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugEngine2::Attach
helpviewer_keywords:
- IDebugEngine2::Attach
ms.assetid: 173dcbda-5019-4c5e-bca9-a071838b5739
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 4de13e9763cfed74c2b7dbbbb58ac80610501ace
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49926079"
---
# <a name="idebugengine2attach"></a>IDebugEngine2::Attach
Anexa um mecanismo de depuração (DE) para um programa ou programas. Chamado pelo Gerenciador de depuração de sessão (SDM) quando o DE estiver em execução no processo para o SDM.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Attach(   
   IDebugProgram2**      pProgram,  
   IDebugProgramNode2**  rgpProgramNodes,  
   DWORD                 celtPrograms,  
   IDebugEventCallback2* pCallback,  
   ATTACH_REASON         dwReason  
);  
```  
  
```csharp  
int Attach(   
   IDebugProgram2[]     pProgram,  
   IDebugProgramNode2[] rgpProgramNodes,  
   uint                 celtPrograms,  
   IDebugEventCallback2 pCallback,  
   Enum_ATTACH_REASON   dwReason  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pProgram`  
 [in] Uma matriz de [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) objetos que representam os programas a serem anexados à. Esses são programas de porta.  
  
 `rgpProgramNodes`  
 [in] Uma matriz de [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) objetos que representam nós de programa, um para cada programa. Os nós de programa nesta matriz representam os mesmos programas como em `pProgram`. Os nós de programa são fornecidos para que o DE possa identificar os programas para anexar a.  
  
 `celtPrograms`  
 [in] Número de programas e/ou nós de programa na `pProgram` e `rgpProgramNodes` matrizes.  
  
 `pCallback`  
 [in] O [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) objeto a ser usado para enviar eventos de depuração para o SDM.  
  
 `dwReason`  
 [in] Um valor a partir de [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md) enumeração que especifica o motivo para anexar a esses programas. Para obter mais informações, consulte a seção Comentários.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Há três razões para anexar a um programa, da seguinte maneira:  
  
- `ATTACH_REASON_LAUNCH` indica que o DE é anexar ao programa porque o usuário iniciou o processo que o contém.  
  
- `ATTACH_REASON_USER` indica que o usuário explicitamente solicitou o DE anexar a um programa (ou o processo que contém um programa).  
  
- `ATTACH_REASON_AUTO` indica que o DE é anexar a um determinado programa porque ele já está sendo depurado outros programas em um determinado processo. Isso também é chamado a anexação automática.  
  
  Quando este método é chamado, o DE precisa enviar esses eventos em sequência:  
  
1. [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md) (se ele não já foi enviado para uma determinada instância do mecanismo de depuração)  
  
2. [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)  
  
3. [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)  
  
   Além disso, se for o motivo para anexação `ATTACH_REASON_LAUNCH`, o DE que precisa enviar o [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md) eventos.  
  
   Uma vez o obtém do [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) do objeto correspondente para o programa que está sendo depurado, ela pode ser consultada para qualquer interface privada.  
  
   Antes de chamar os métodos de um nó de programa na matriz fornecida pelo `pProgram` ou `rgpProgramNodes`, representação, se necessário, deve ser habilitada no `IDebugProgram2` interface que representa o nó do programa. Normalmente, no entanto, essa etapa não é necessária. Para obter mais informações, consulte [problemas de segurança](../../../extensibility/debugger/security-issues.md).  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [ATTACH_REASON](../../../extensibility/debugger/reference/attach-reason.md)   
 [IDebugEngineCreateEvent2](../../../extensibility/debugger/reference/idebugenginecreateevent2.md)   
 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)   
 [IDebugLoadCompleteEvent2](../../../extensibility/debugger/reference/idebugloadcompleteevent2.md)   
 [IDebugEntryPointEvent2](../../../extensibility/debugger/reference/idebugentrypointevent2.md)