---
title: Marcadores de período | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.markers.span
ms.assetid: 736b7765-9c71-44d7-85e5-79787d13d91c
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8f733ccec12e422a11532b8012836422d14d93b9
ms.sourcegitcommit: a83c60bb00bf95e6bea037f0e1b9696c64deda3c
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/19/2019
ms.locfileid: "54798027"
---
# <a name="span-markers"></a>Marcadores de período
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um marcador de período representa uma fase significativa de um aplicativo. Por exemplo, você pode usar um período para representar um intervalo de tempo durante o qual um item de trabalho específico está sendo processado. Seu comprimento representa a duração da fase de aplicativo correspondente. Esta ilustração mostra um período na Visualização Simultânea:  
  
 ![Um marcador de extensão no Visualizador de simultaneidade](../profiling/media/cvmarkerspan.png "CVMarkerSpan")  
Um marcador de período na Visualização Simultânea  
  
## <a name="span-category"></a>Categoria Período  
 Um marcador de período pode ser exibido em cinco cores diferentes, dependendo de sua categoria. As cores são repetidas se há mais de cinco categorias. A categoria pode ser qualquer inteiro. Esta ilustração mostra as cinco cores possíveis:  
  
 ![Cinco extensões em categorias diferentes](../profiling/media/cvmarkerspancategory.png "CVMarkerSpanCategory")  
As cores das cinco primeiras categorias de período  
  
## <a name="span-aggregation-markers"></a>Marcadores de agregação de período  
 Às vezes, marcadores de período ocorrem tão próximos uns dos outros na Visualização Simultânea que não podem ser desenhados individualmente. Quando isso ocorre, um *marcador de agregação de período* cinza que representa os períodos subjacentes é mostrado. Quando você posiciona o ponteiro em desses ícones, uma dica de ferramenta exibe o número de períodos subjacentes representados. Para exibir os períodos, amplie. Se você ampliar completamente e ainda obtiver um marcador de agregação de período, você poderá exibir os marcadores de período subjacentes no [Relatório de Marcadores](../profiling/markers-report.md). Esta ilustração mostra um marcador de agregação de período:  
  
 ![Um marcador de extensão agregado no Visualizador de simultaneidade](../profiling/media/cvmarkerspanaggregate.png "CVMarkerSpanAggregate")  
Um marcador de agregação de período  
  
## <a name="see-also"></a>Consulte também  
 [Marcadores da Visualização Simultânea](../profiling/concurrency-visualizer-markers.md)   
 [SDK da Visualização Simultânea](../profiling/concurrency-visualizer-sdk.md)
