---
title: Função CvCreateMarkerSeries | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- cvmarkers/CvCreateMarkerSeriesA
- cvmarkers/CvCreateMarkerSeriesW
helpviewer_keywords:
- CvCreateMarkerSeriesA method
- CvCreateMarkerSeriesW method
ms.assetid: e280530b-137a-43a7-8643-aa514ab86ed7
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 9395f576e942e799312dad2e22be79942110a8ae
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53967794"
---
# <a name="cvcreatemarkerseries-function"></a>Função CvCreateMarkerSeries
Cria a série de marcador para determinado provedor.  
  
## <a name="syntax"></a>Sintaxe  
  
```C  
_Check_return_ HRESULT CvCreateMarkerSeriesW(  
    _In_ PCV_PROVIDER  pProvider,  
    _In_ LPCWSTR pSeriesName,  
    _Out_ PCV_MARKERSERIES* ppMarkerSeries);  
  
_Check_return_ HRESULT CvCreateMarkerSeriesA(  
    _In_ PCV_PROVIDER  pProvider,  
    _In_ LPCSTR pSeriesName,  
    _Out_ PCV_MARKERSERIES* ppMarkerSeries);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pProvider`  
 Objeto de provedor inicializado anteriormente por CvInitProvider. Não pode ser NULL.  
  
 `pSeriesName`  
 Nome da série de marcador. Não pode ser NULL, mas uma cadeia de caracteres vazia é permitida.  
  
 `ppMarkerSeries`  
 Endereço de uma variável de saída que armazenará o contexto de série de marcador. Não pode ser NULL.  
  
## <a name="return-value"></a>Valor retornado  
 S_OK quando a série de marcador é criada com êxito ou código de erro no caso de erros. Use as macros SUCCEEDED/FAILED para verificar a condição de erro.  
  
## <a name="requirements"></a>Requisitos  
 **Cabeçalho:** *cvmarkers.h*  
  
 **Unicode:** CvCreateMarkerSeriesW  
  
 **ANSI:** CvCreateMarkerSeriesA  
  
## <a name="see-also"></a>Consulte também  
 [Referência de biblioteca C++](../profiling/cpp-library-reference.md)