---
title: Analisar o uso de memória no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 01/02/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d8971f26881e522c81f2c111098f09a94133072d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49948909"
---
# <a name="analyze-memory-usage"></a>Analisar o uso de memória
Use a ferramenta de diagnóstico **Uso de Memória** integrada no depurador para localizar perdas de memória e uso de memória ineficiente. A ferramenta Uso de Memória permite que você tire um ou mais *instantâneos* do heap de memória gerenciada e do heap de memória nativa. Você pode coletar instantâneos de aplicativos .NET, ASP.NET, nativos ou mistos (.NET e nativos).  
  
-   É possível analisar um único instantâneo para compreender o impacto relativo dos tipos de objeto sobre o uso da memória e encontrar o código no aplicativo que usa a memória de maneira ineficiente.  
  
-   Também é possível comparar (diff) dois instantâneos de um aplicativo para encontrar áreas no código que causam o aumento do uso da memória com o passar do tempo.  

Para obter instruções detalhadas, consulte o tutorial [Analisar o uso de memória](../profiling/memory-usage.md).  Atualmente, para medir o uso de memória de um aplicativo .NET Core, é necessário usar a ferramenta com o depurador anexado. Para outros aplicativos gerenciados e nativos, é possível usar a ferramenta com ou sem o depurador anexado.

Você pode usar as ferramentas de criação de perfil sem o depurador com o Windows 7 e posteriores. O Windows 8 ou posterior é necessário para executar ferramentas de criação de perfil com o depurador (janela **Ferramentas de Diagnóstico**).
  
## <a name="blogs-and-videos"></a>Blogs e vídeos  

| | |
|---------|---------|
| ![ícone de câmera para vídeo](../install/media/video-icon.png "Assistir a um vídeo") | [Assista a um vídeo](https://mva.microsoft.com/en-US/training-courses-embed/getting-started-with-visual-studio-2017-17798/Profiling-with-Diagnostics-Tools-in-Visual-Studio-2017-daHnzMD6D_9211787171) sobre como usar as ferramentas de diagnóstico que mostra como analisar o uso de memória e o uso de CPU no Visual Studio 2017. |

 [Analisar a CPU e a memória durante a depuração](https://blogs.msdn.microsoft.com/visualstudio/2016/02/15/analyze-cpu-memory-while-debugging/)  
  
 [Blog do Visual C++: Criação de perfil de memória no Visual C++ 2015](https://blogs.msdn.microsoft.com/vcblog/2015/10/21/memory-profiling-in-visual-c-2015/)  

## <a name="see-also"></a>Consulte também
 [Criação de perfis no Visual Studio](../profiling/index.md)  
 [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)