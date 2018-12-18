---
title: Método marker_series::write_alert | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic:marker_series::write_alert
helpviewer_keywords:
- Concurrency::diagnostic:marker_series::write_alert method
ms.assetid: 9d5465c7-f862-47a7-b249-4116605075a6
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: b980939627cb770e27d01d1413bdee877ab1bcb1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51722533"
---
# <a name="markerserieswritealert-method"></a>Método marker_series::write_alert
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Grava um alerta para o arquivo de rastreamento da Visualização Simultânea.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
void write_alert(  
   _In_ LPCTSTR _Format,  
   ...  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `_Format`  
 Uma cadeia de caracteres de formato de composição, que contém texto intercalado com zero ou mais itens de formato correspondentes a objetos na lista de argumentos.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** cvmarkersobj.h  
  
 **Namespace:** Concurrency::diagnostic  
  
## <a name="see-also"></a>Consulte também  
 [Classe marker_series](../profiling/marker-series-class.md)



