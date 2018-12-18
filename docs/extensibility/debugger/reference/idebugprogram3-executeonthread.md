---
title: IDebugProgram3::ExecuteOnThread | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- IDebugProgram3::ExecuteOnThread
ms.assetid: 2f5211e3-7a3f-47bf-9595-dfc8b4895d0d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: afca4a97380d010897ca1dfb7c6229f3f1897ef9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49865930"
---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
Executa o programa do depurador. O thread é retornado para fornecer as informações do depurador em qual thread o usuário está exibindo ao executar o programa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ExecuteOnThread(  
   [in] IDebugThread2* pThread)  
```  
  
```csharp  
int ExecuteOnThread(  
   IDebugThread2 pThread  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pThread`  
 [in] Uma [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) objeto.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Há três maneiras diferentes que um depurador pode retomar a execução após a interrupção:  
  
- Execute: Cancelar qualquer etapa anterior e executar até o próximo ponto de interrupção e assim por diante.  
  
- Etapa: Cancelar qualquer etapa antiga e executar até que a nova etapa seja concluída.  
  
- Continuar: Executar novamente e deixar qualquer etapa antiga ativa.  
  
  O thread é passado para `ExecuteOnThread` é útil ao decidir qual etapa para cancelar. Se você não souber o thread em execução executar cancela todas as etapas. Com conhecimento do thread, você só precisará cancelar a etapa no thread ativo.  
  
## <a name="see-also"></a>Consulte também  
 [Executar](../../../extensibility/debugger/reference/idebugprogram2-execute.md)   
 [IDebugProgram3](../../../extensibility/debugger/reference/idebugprogram3.md)