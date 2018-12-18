---
title: Marcadores de mensagem | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.markers.message
ms.assetid: 721f40ca-5af2-4a01-b8b6-2b90f6cb7f89
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 72b93d497a68ba09237c28fc56159c379b50c9c1
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35254557"
---
# <a name="message-markers"></a>Marcadores de mensagem
Um marcador de mensagem representa a saída de log. Uma mensagem é uma cadeia de caracteres emitida por um thread específico em um momento específico. Você pode exportar as mensagens para um arquivo de texto para usar com outras ferramentas. Você pode deixar o ponteiro em uma mensagem na Visualização Simultânea para exibir a cadeia de caracteres de mensagem. E você pode exibir todos os marcadores de mensagem no [Relatório de marcadores](../profiling/markers-report.md).  A ilustração a seguir mostra um marcador de mensagem.  
  
## <a name="message-aggregation-markers"></a>Marcadores de agregação de mensagem  
 Às vezes, ocorrem várias mensagens tão próximas entre si na Visualização Simultânea que elas não podem ser desenhadas individualmente. Quando isso ocorre, um *marcador de agregação de mensagem* que representa as mensagens subjacentes é mostrado. Quando você posiciona o ponteiro em desses ícones, uma dica de ferramenta exibe o número de mensagens subjacentes representadas. Para exibir as mensagens, amplie.  Se ampliar completamente e ainda obtiver um sinalizador de agregação, você poderá exibir as mensagens subjacentes no [Relatório de Marcadores](../profiling/markers-report.md).  
  
## <a name="see-also"></a>Consulte também  
 [Marcadores de Visualização Simultânea](../profiling/concurrency-visualizer-markers.md)   
 [SDK da Visualização Simultânea](../profiling/concurrency-visualizer-sdk.md)