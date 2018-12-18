---
title: Relatório de Marcadores | Microsoft Docs
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
- vs.cv.threads.report.markers
ms.assetid: 829ce099-172e-4c7e-bbd0-578b110c59bd
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 044df49c466c98466e15078b38e6240420b0a6fe
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809708"
---
# <a name="markers-report"></a>Relatório de marcadores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Relatório de Marcadores lista os marcadores no período de tempo exibido.  A movimentação panorâmica, a aplicação de zoom ou a ocultação de pistas pode fazer com que os marcadores apareçam ou desapareçam. O relatório contém informações sobre cada marcador:  
  
- A hora em que ele foi iniciado, com relação ao começo do rastreamento.  
  
- Sua duração. A duração é zero para mensagens e sinalizadores porque eles representam um instante.  
  
- A ID do thread que o gerou.  
  
- O provedor ETW (Acompanhamento de Eventos para Windows) que o gerou.  
  
- A série de marcadores da qual ele foi escrito.  
  
- A categoria de eventos à qual ele pertence.  
  
- Seu nível de importância.  
  
- Seu tipo (extensão, sinalizador ou mensagem).  
  
- Uma descrição detalhada do que ele representa  
  
  Escolha o botão **Exportar** para salvar o Relatório de Marcadores como um arquivo CSV. Você pode usar os dados no arquivo CSV com outros aplicativos ou ferramentas.  
  
> [!NOTE]
>  O Relatório de Marcadores pode exibir 1.000 marcadores. Para ver todos os marcadores, exporte o relatório completo para um arquivo CSV.



