---
title: IBindEventHandler::BindHandler | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IBindEventHandler.BindHandler
apilocation:
- scrobj.dll
helpviewer_keywords:
- IBindEventHandler::BindHandler
ms.assetid: 87909828-2224-4bb1-a6c9-dfe715ac4c9b
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 66de7cba8181ce9f3d683a90e4d7dd51e63d4779
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725186"
---
# <a name="ibindeventhandlerbindhandler"></a>IBindEventHandler::BindHandler
Associa um evento para um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT BindHandler(  
   LPCOLESTR   pstrEvent,  
   IDispatch*  pdisp  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pstrEvent`  
 [in] Especifica o evento para manipular.  
  
 `pdisp`  
 [in] Especifica o objeto para manipular o evento.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
 Esse método associa um evento para um objeto.  
  
## <a name="see-also"></a>Consulte também  
 [IBindEventHandler Interface](../../winscript/reference/ibindeventhandler-interface.md)