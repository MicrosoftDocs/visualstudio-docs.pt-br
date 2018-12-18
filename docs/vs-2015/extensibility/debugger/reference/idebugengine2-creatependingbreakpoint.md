---
title: IDebugEngine2::CreatePendingBreakpoint | Microsoft Docs
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
- IDebugEngine2::CreatePendingBreakpoint
helpviewer_keywords:
- IDebugEngine2::CreatePendingBreakpoint
ms.assetid: 92e85b90-a931-48d9-89a7-a6edcb83ae5a
caps.latest.revision: 11
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 28123ed555cc54d8ca307cca020fe7b101f73087
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51777221"
---
# <a name="idebugengine2creatependingbreakpoint"></a>IDebugEngine2::CreatePendingBreakpoint
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Cria um ponto de interrupção pendente no mecanismo de depuração (DES).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT CreatePendingBreakpoint(   
   IDebugBreakpointRequest2*  pBPRequest,  
   IDebugPendingBreakpoint2** ppPendingBP  
);  
```  
  
```csharp  
int CreatePendingBreakpoint(   
   IDebugBreakpointRequest2     pBPRequest,  
   out IDebugPendingBreakpoint2 ppPendingBP  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pBPRequest`  
 [in] Uma [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md) objeto que descreve o ponto de interrupção pendente para criar.  
  
 `ppPendingBP`  
 [out] Retorna um [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md) objeto que representa o ponto de interrupção pendente.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro. Normalmente retorna `E_FAIL` se o `pBPRequest` parâmetro não corresponde a qualquer linguagem compatível com o dos se o `pBPRequest` parâmetro é inválido ou incompleto.  
  
## <a name="remarks"></a>Comentários  
 Um ponto de interrupção pendente é essencialmente uma coleção de todas as informações necessárias para associar um ponto de interrupção no código. O ponto de interrupção pendente retornado desse método não está associado ao código até que o [associar](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md) método é chamado.  
  
 Para cada pendente do ponto de interrupção conjuntos de dados do usuário, o Gerenciador de sessão de depuração (SDM) chama esse método em cada DE anexado. É responsabilidade DE verificar se o ponto de interrupção é válido para programas em execução em que DE.  
  
 Quando o usuário define um ponto de interrupção em uma linha de código, a Alemanha é gratuita associar o ponto de interrupção para a linha mais próxima do documento que corresponde a esse código. Isso torna possível para o usuário definir um ponto de interrupção na primeira linha de uma instrução de várias linha, mas associá-lo na última linha (em que todo o código é atribuído nas informações de depuração).  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como implementar esse método para um simples `CProgram` objeto. Implementação do `IDebugEngine2::CreatePendingBreakpoint` poderia, em seguida, encaminhar todas as chamadas para essa implementação do método em cada programa.  
  
```  
HRESULT CProgram::CreatePendingBreakpoint(IDebugBreakpointRequest2* pBPRequest, IDebugPendingBreakpoint2** ppPendingBP)     
{    
  
   // Create and initialize the CPendingBreakpoint object.  
   CComObject<CPendingBreakpoint> *pPending;    
   CComObject<CPendingBreakpoint>::CreateInstance(&pPending);    
   pPending->Initialize(pBPRequest, m_pInterp, m_pCallback, m_pEngine);    
   return pPending->QueryInterface(ppPendingBP);    
}    
```  
  
## <a name="see-also"></a>Consulte também  
 [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)   
 [associar](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)   
 [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)   
 [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)

