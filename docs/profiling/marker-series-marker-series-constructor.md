---
title: Construtor marker_series::marker_series | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::marker_series::marker_series
helpviewer_keywords:
- Concurrency::diagnostic::marker_series constructor
ms.assetid: 042c7d23-f1d8-4e09-9e76-a21c30243790
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: bbc397fa88c722f6a7f16ac92f4388525073c0fa
ms.sourcegitcommit: ce154aee5b403d5c1c41da42302b896ad3cf8d82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34845617"
---
# <a name="markerseriesmarkerseries-constructor"></a>Construtor marker_series::marker_series
Inicializa uma nova instância da classe `marker_series`.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
marker_series();  
marker_series(  
   _In_ LPCTSTR _SeriesName  
);  
marker_series(  
   _In_ const GUID* _ProviderGuid  
);  
marker_series(  
   _In_ const GUID* _ProviderGuid,  
   _In_ LPCTSTR _SeriesName  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `_SeriesName`  
 O nome da série a ser criada.  
  
 `_ProviderGuid`  
 O GUID do provedor da série.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** *cvmarkersobj.h*  
  
 **Namespace:** Concurrency::diagnostic  
  
## <a name="see-also"></a>Consulte também  
 [Classe marker_series](../profiling/marker-series-class.md)