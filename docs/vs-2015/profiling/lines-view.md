---
title: Exibição de Linhas | Microsoft Docs
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
- vs.performance.view.lines
helpviewer_keywords:
- profiling tools reports, Line view
- profiling tools, Line view
- Lines view
ms.assetid: 71ec0781-6031-4e17-af09-f50226018437
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 829db9b1f8e4826ea9761a4433e6ee1adaab49e2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51749973"
---
# <a name="lines-view"></a>Exibição de linhas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A exibição de Linhas está disponível somente para dados de criador de perfil coletados por meio do método de amostragem. A exibição não está disponível para dados coletados por meio de instrumentação.  
  
 Para dados de perfil de amostragem, as exibições de Linhas identificam a instrução em uma função que foi diretamente executada quando a amostra foi coletada. Para dados da memória do .NET, as exibições de Linhas identificam as instruções que alocam memória.  
  
 Em um arquivo de origem, uma instrução pode abranger mais de uma linha em um arquivo de origem e uma única linha pode incluir mais de uma instrução.  
  
 Uma instrução é identificada pelo seguinte:  
  
-   O arquivo de origem que contém a instrução da função.  
  
-   A função que contém a instrução.  
  
-   A linha de origem em que a instrução se inicia.  
  
-   O caractere na linha de origem em que a instrução se inicia.  
  
-   A linha de origem em que a instrução termina.  
  
-   O caractere na linha de origem em que a instrução termina.  
  
## <a name="see-also"></a>Consulte também  
 [Exibição de Linhas](../profiling/lines-view-sampling-data.md)   
 [Exibição de Linhas – Amostragem](../profiling/lines-view-dotnet-memory-sampling-data.md)   
 [Exibição de Linhas](../profiling/lines-view-contention-data.md)



