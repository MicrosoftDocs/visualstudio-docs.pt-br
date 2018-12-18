---
title: IDebugAsyncOperation::Abort | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugAsyncOperation.Abort
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugAsyncOperation::Abort
ms.assetid: 232541c6-81b8-4eb7-96a7-a8e5fe087b31
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 274f09ae2a8851b897a825c32f18091c2f4250d0
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726026"
---
# <a name="idebugasyncoperationabort"></a>IDebugAsyncOperation::Abort
Cancela uma operação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT Abort();  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Esse método não usa nenhum parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|S_OK|O método foi bem-sucedido.|  
|E_NOTIMPL|As operações não podem ser canceladas.|  
  
## <a name="remarks"></a>Comentários  
 Normalmente, este método é chamado de dentro do thread do depurador para cancelar uma operação sem resposta. Este método faz com que o `InProgressAbort` método o `IDebugSyncOperation` objeto a ser chamado.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugAsyncOperation](../../winscript/reference/idebugasyncoperation-interface.md)   
 [IDebugAsyncOperation::Start](../../winscript/reference/idebugasyncoperation-start.md)   
 [IDebugSyncOperation::InProgressAbort](../../winscript/reference/idebugsyncoperation-inprogressabort.md)