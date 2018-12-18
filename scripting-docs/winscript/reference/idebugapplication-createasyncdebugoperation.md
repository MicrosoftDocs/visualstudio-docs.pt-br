---
title: IDebugApplication::CreateAsyncDebugOperation | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugApplication.CreateAsyncDebugOperation
apilocation:
- pdm.dll
helpviewer_keywords:
- IDebugApplication::CreateAsyncDebugOperation
ms.assetid: bc32b101-6364-4498-8458-bd5f3ab5ad94
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 8714f4401249d73cf09d241ebf4c2b2115911d6b
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725526"
---
# <a name="idebugapplicationcreateasyncdebugoperation"></a>IDebugApplication::CreateAsyncDebugOperation
Fornece acesso assíncrono a uma operação de depuração síncrona determinado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT CreateAsyncDebugOperation(  
   IDebugSyncOperation*    psdo,  
   IDebugAsyncOperation**  ppado  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `psdo`  
 [in] O objeto de operação síncrona de depuração.  
  
 `ppado`  
 [out] O objeto de operação de depuração assíncrona.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Esse método permite que os mecanismos de linguagem avaliar expressões de forma assíncrona sem sincronização explicitamente com o thread do depurador. Para obter mais informações, consulte [IDebugSyncOperation Interface](../../winscript/reference/idebugsyncoperation-interface.md) e [IDebugAsyncOperation Interface](../../winscript/reference/idebugasyncoperation-interface.md).  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugApplication](../../winscript/reference/idebugapplication-interface.md)   
 [Interface IDebugSyncOperation](../../winscript/reference/idebugsyncoperation-interface.md)   
 [IDebugAsyncOperation Interface](../../winscript/reference/idebugasyncoperation-interface.md)