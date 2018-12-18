---
title: ISimpleConnectionPoint::DescribeEvents | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISimpleConnectionPoint.DescribeEvents
apilocation:
- pdm.dll
helpviewer_keywords:
- ISimpleConnectionPoint::DescribeEvents
ms.assetid: 659ea05f-d41e-424a-bb38-df7672b2d135
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 42dab9558d46eae0fbb640c60264a79877708321
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734016"
---
# <a name="isimpleconnectionpointdescribeevents"></a>ISimpleConnectionPoint::DescribeEvents
Retorna o DISPID e o nome para cada evento em um intervalo especificado de eventos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT DescribeEvents(  
   ULONG    iEvent,  
   ULONG    cEvents,  
   DISPID*  prgid,  
   BSTR*    prgbstr,  
   ULONG*   pcEventsFetched  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `iEvent`  
 [in] Índice do primeiro evento para recuperar.  
  
 `cEvents`  
 [in] Número de eventos para recuperar.  
  
 `prgid`  
 [out] Matriz de valores DISPID de evento.  
  
 `prgbstr`  
 [out] Matriz de nomes de evento.  
  
 `pcEventsFetched`  
 [out] O número real de eventos buscados.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
|`S_FALSE`|Eventos mais foram solicitados que estavam disponíveis. Os eventos disponíveis são representados por DISPID_NULL e um BSTR nulo.|  
|`E_INVALIDARG`|Nenhum elemento pôde ser obtido.|  
  
## <a name="remarks"></a>Comentários  
 Esse método retorna o DISPID e o nome para cada evento em um intervalo especificado de eventos.  
  
## <a name="see-also"></a>Consulte também  
 [Interface ISimpleConnectionPoint](../../winscript/reference/isimpleconnectionpoint-interface.md)