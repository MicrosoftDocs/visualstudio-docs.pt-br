---
title: Marcadores de período | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.markers.span
ms.assetid: 736b7765-9c71-44d7-85e5-79787d13d91c
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 37f2dd735b7deb2d4fed1232c2ba690b26a9fde0
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35668161"
---
# <a name="span-markers"></a>Marcadores de período
Um marcador de período representa uma fase significativa de um aplicativo. Por exemplo, você pode usar um período para representar um intervalo de tempo durante o qual um item de trabalho específico está sendo processado. Seu comprimento representa a duração da fase de aplicativo correspondente. Esta ilustração mostra um período na Visualização Simultânea:  
  
 ![Um marcador de extensão no Visualizador de simultaneidade](../profiling/media/cvmarkerspan.png "CVMarkerSpan")  
Um marcador de período na Visualização Simultânea  
  
## <a name="span-category"></a>Categoria de período  
 Um marcador de período pode ser exibido em cinco cores diferentes, dependendo de sua categoria. As cores são repetidas se há mais de cinco categorias. A categoria pode ser qualquer inteiro. Esta ilustração mostra as cinco cores possíveis:  
  
 ![Cinco extensões em categorias diferentes](../profiling/media/cvmarkerspancategory.png "CVMarkerSpanCategory")  
As cores das cinco primeiras categorias de período  
  
## <a name="span-aggregation-markers"></a>Marcadores de agregação de período  
 Às vezes, os marcadores de período ocorrem tão próximos uns dos outros na Visualização Simultânea que não podem ser desenhados individualmente. Quando isso ocorre, um *marcador de agregação de período* cinza que representa os períodos subjacentes é mostrado. Quando você posiciona o ponteiro em desses ícones, uma dica de ferramenta exibe o número de períodos subjacentes representados. Para exibir os períodos, amplie. Se você ampliar completamente e ainda obtiver um marcador de agregação de período, você poderá exibir os marcadores de período subjacentes no [Relatório de Marcadores](../profiling/markers-report.md). Esta ilustração mostra um marcador de agregação de período:  
  
 ![Um marcador de extensão agregado no Visualizador de simultaneidade](../profiling/media/cvmarkerspanaggregate.png "CVMarkerSpanAggregate")  
Um marcador de agregação de período  
  
## <a name="see-also"></a>Consulte também  
 [Marcadores de Visualização Simultânea](../profiling/concurrency-visualizer-markers.md)   
 [SDK da Visualização Simultânea](../profiling/concurrency-visualizer-sdk.md)