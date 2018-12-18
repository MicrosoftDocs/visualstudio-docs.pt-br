---
title: IDebugProgram3::ExecuteOnThread | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- IDebugProgram3::ExecuteOnThread
ms.assetid: 2f5211e3-7a3f-47bf-9595-dfc8b4895d0d
caps.latest.revision: 7
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 4e183d9d55c8527cdead0d7108c12ac3fd527e94
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51788622"
---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

Executa o programa do depurador. O thread é retornado para fornecer as informações do depurador em qual thread o usuário está exibindo ao executar o programa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
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

