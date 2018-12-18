---
title: IDebugProgram2::Terminate | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IDebugProgram2::Terminate
helpviewer_keywords:
- IDebugProgram2::Terminate
ms.assetid: 4d3127d3-b1e9-4b28-ac22-2f2eea255f86
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 88fcbf0667c026cbbfc449936f92d440590e9a8f
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49834260"
---
# <a name="idebugprogram2terminate"></a>IDebugProgram2::Terminate
Encerra o programa.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT Terminate(   
   void   
);  
```  
  
```csharp  
int Terminate();  
```  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Se possível, o programa será encerrado e descarregado do processo; Caso contrário, o mecanismo de depuração (DES) executará qualquer limpeza necessária.  
  
 Esse método ou o [Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md) método é chamado pelo IDE, geralmente em resposta ao usuário interrompendo a depuração de todos os. A implementação desse método Idealmente, deve, encerrar o programa dentro do processo. Se isso não for possível, o DE deve impedir que o programa em execução mais nesse processo (e fazer qualquer limpeza necessária). Se o `IDebugProcess2::Terminate` método foi chamado pelo IDE, todo o processo será encerrado em algum momento depois o `IDebugProgram2::Terminate` método é chamado.  
  
## <a name="see-also"></a>Consulte também  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)   
 [Terminar](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)