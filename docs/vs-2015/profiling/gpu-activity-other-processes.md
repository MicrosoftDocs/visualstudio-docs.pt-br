---
title: Atividade de GPU (outros processos) | Microsoft Docs
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
- vs.cv.threads.timeline.gpuother
- vs.cv.threads.timeline.gpuactivity
ms.assetid: 8a68df65-eb63-452f-9285-fb4ffc92f2b2
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a5b38423bd629dee0f518e0f62eedcf7c55c1db0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51789831"
---
# <a name="gpu-activity-other-processes"></a>Atividade de GPU (outros processos)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os segmentos **Atividade de GPU (outros processos)** na exibição Threads na Visualização Simultânea representam o tempo durante o qual a GPU estava processando solicitações em nome de outros processos no sistema. Essas solicitações são enviadas à GPU como pacotes de DMA (acesso direto à memória).  O tamanho de um segmento representa o tempo durante o qual o pacote foi processado pela GPU.  
  
 Quando você seleciona este tipo de segmento, o relatório na guia **Atual** exibe informações sobre o pacote que foi processado.  As informações incluem a quantidade de tempo que o pacote esperou na fila de hardware associada ao mecanismo do DirectX, o processo que enviou o pacote e o tempo necessário para processar o pacote.



