---
title: Método marker_series::write_flag | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- cvmarkersojb/Concurrency::diagnostic::marker_series::write_flag
helpviewer_keywords:
- Concurrency::diagnostic::marker_series::write_flag method
ms.assetid: ca07f388-e5d5-46fd-b991-fe6e9029a68f
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b44c7cf2d2eb0f538b3819265298f1ca4166e6be
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68200756"
---
# <a name="markerserieswriteflag-method"></a>Método marker_series::write_flag
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Grava um sinalizador para o arquivo de rastreamento da Visualização Simultânea.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
void write_flag(  
   _In_ LPCTSTR _Format,  
   ...  
);  
void write_flag(  
   marker_importance _Importance,  
   _In_ LPCTSTR _Format,  
   ...  
);  
void write_flag(  
   int _Category,  
   _In_ LPCTSTR _Format,  
   ...  
);  
void write_flag(  
   marker_importance _Importance,  
   int _Category,  
   _In_ LPCTSTR _Format,  
   ...  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `_Format`  
 Uma cadeia de caracteres de formato de composição, que contém texto intercalado com zero ou mais itens de formato correspondentes a objetos na lista de argumentos.  
  
 `_Importance`  
 Nível de importância.  
  
 `_Category`  
 Categoria.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** cvmarkersobj.h  
  
 **Namespace:** Concurrency::diagnostic  
  
## <a name="see-also"></a>Veja também  
 [Classe marker_series](../profiling/marker-series-class.md)
