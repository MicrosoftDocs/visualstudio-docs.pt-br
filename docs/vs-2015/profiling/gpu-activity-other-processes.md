---
title: Atividade de GPU (outros processos) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.cv.threads.timeline.gpuother
- vs.cv.threads.timeline.gpuactivity
ms.assetid: 8a68df65-eb63-452f-9285-fb4ffc92f2b2
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a3b0e97d82d67916aa71f932038930dba48c17e4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "62434131"
---
# <a name="gpu-activity-other-processes"></a>Atividade de GPU (outros processos)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os segmentos **Atividade de GPU (outros processos)** na exibição Threads na Visualização Simultânea representam o tempo durante o qual a GPU estava processando solicitações em nome de outros processos no sistema. Essas solicitações são enviadas à GPU como pacotes de DMA (acesso direto à memória).  O tamanho de um segmento representa o tempo durante o qual o pacote foi processado pela GPU.  
  
 Quando você seleciona este tipo de segmento, o relatório na guia **Atual** exibe informações sobre o pacote que foi processado.  As informações incluem a quantidade de tempo que o pacote esperou na fila de hardware associada ao mecanismo do DirectX, o processo que enviou o pacote e o tempo necessário para processar o pacote.
