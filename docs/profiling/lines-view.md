---
title: Exibição de Linhas | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.view.lines
helpviewer_keywords:
- profiling tools reports, Line view
- profiling tools, Line view
- Lines view
ms.assetid: 71ec0781-6031-4e17-af09-f50226018437
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 5c298f6801b5c66a978ac39953eb2edc92838c30
ms.sourcegitcommit: ce154aee5b403d5c1c41da42302b896ad3cf8d82
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2018
ms.locfileid: "34844151"
---
# <a name="lines-view"></a>Exibição de linhas
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
 [Exibição de linhas – amostragem](../profiling/lines-view-dotnet-memory-sampling-data.md)   
 [Exibição de Linhas](../profiling/lines-view-contention-data.md)