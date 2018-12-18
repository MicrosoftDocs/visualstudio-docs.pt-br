---
title: Atividade de GPU (este processo) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.gpuexecution
- vs.cv.threads.timeline.gpuactivity
ms.assetid: 0956edbf-9bcd-4afe-9287-fda628648ca0
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d7fe5512cf131dfede701fb47df2ef956c01437d
ms.sourcegitcommit: 42ea834b446ac65c679fa1043f853bea5f1c9c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/19/2018
ms.locfileid: "31570379"
---
# <a name="gpu-activity-this-process"></a>Atividade de GPU (este processo)
Os segmentos **Atividade de GPU (este processo)** na exibição Threads na Visualização Simultânea representam o tempo durante o qual a GPU estava processando solicitações em nome do processo atual. Essas solicitações são enviadas à GPU como pacotes de DMA (acesso direto à memória). O tamanho de um segmento representa o tempo durante o qual a GPU estava processando um pacote de DMA em nome do processo atual.  
  
 Quando você seleciona o segmento de atividade de GPU, o relatório na guia **Atual** exibe informações sobre o pacote de DMA que foi processado. Essas informações incluem a quantidade de tempo que o pacote esperou na fila de hardware associada ao mecanismo do DirectX, o processo que enviou o pacote e o tempo necessário para processar o pacote. Um processo diferente do processo atual pode ter enviado fisicamente o pacote de DMA à GPU. A Visualização Simultânea pode detectar quando outro processo enviou trabalho à GPU em nome do processo atual.