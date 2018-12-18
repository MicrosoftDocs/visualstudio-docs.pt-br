---
title: IDebugSyncOperation::InProgressAbort | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugSyncOperation.InProgressAbort
apilocation:
- jscript.dll
helpviewer_keywords:
- IDebugSyncOperation::InProgressAbort
ms.assetid: bfd0889c-b627-4843-b1c6-b6b918f42d61
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1df0b0ca1d775d4d99e1da5f88a207bd4f78f99b
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728256"
---
# <a name="idebugsyncoperationinprogressabort"></a>IDebugSyncOperation::InProgressAbort
Cancela uma operação em andamento em outro thread.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT InProgressAbort();  
```  
  
#### <a name="parameters"></a>Parâmetros  
 Esse método não usa nenhum parâmetro.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
|`E_NOTIMPL`|A operação não pode ser cancelada.|  
|`E_ABORT`|Não foi possível concluir a operação.|  
  
## <a name="remarks"></a>Comentários  
 O Gerenciador de depuração do processo chama esse método a partir do thread do depurador para cancelar uma operação que está em andamento em outro thread.  
  
 Se o `InProgressAbort` método não pode concluir a operação, ele retorna `E_ABORT` assim que possível. Esse método pode retornar `E_NOTIMPL` se a operação não pode ser cancelada.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugSyncOperation](../../winscript/reference/idebugsyncoperation-interface.md)