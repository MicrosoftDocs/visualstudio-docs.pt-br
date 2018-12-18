---
title: PerfTips | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 509d2d4f-48a5-4cdf-acad-6f7b75421303
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2933f29cb3668e12731e79151ba17480dda96ea5
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220549"
---
# <a name="perftips"></a>PerfTips
O depurador do Visual Studio *PerfTips* e as **Ferramentas de Diagnóstico** integradas ao depurador ajudam a monitorar e analisar o desempenho de seu aplicativo durante a depuração.  
  
 Embora as ferramentas de diagnóstico integradas ao depurador sejam uma ótima maneira de descobrir problemas de desempenho durante o desenvolvimento, o depurador pode exercer um impacto significativo sobre o desempenho do seu aplicativo. Para coletar dados de desempenho mais precisos, considere usar também as ferramentas de diagnóstico do Visual Studio que são executados fora do depurador como uma parte adicional das suas investigações de desempenho. Consulte [Executar Ferramentas de Criação de Perfil com ou sem o depurador](../profiling/running-profiling-tools-with-or-without-the-debugger.md).  
  
## <a name="perftips"></a>PerfTips  
 Quando o depurador interrompe a execução em um ponto de interrupção ou operação passo a passo, o tempo decorrido entre a interrupção e o ponto de interrupção anterior aparece como uma dica na janela do editor. Para obter mais informações, consulte [PerfTips: informações de desempenho imediatas durante a depuração com o Visual Studio](https://blogs.msdn.microsoft.com/devops/2014/08/18/perftips-performance-information-at-a-glance-while-debugging-with-visual-studio/).  
  
 ![PerfTip](../profiling/media/dbgdiag_perf_perftip.png "DBGDIAG_PERF_PerfTip")  
  
## <a name="diagnostics-tools-window"></a>Janela Ferramentas de Diagnóstico  
 Pontos de interrupção e dados de tempo associados são registrados na janela **Ferramentas de Diagnóstico**.  
  
 O gráfico a seguir mostra a janela **Ferramentas de Diagnóstico** no Visual Studio 2015 Atualização 1:  
  
 ![DiagnosticTools&#45;Update1](../profiling/media/diagnostictools-update1.png "DiagnosticTools-Update1")  
  
-   A linha do tempo **Eventos de Interrupção** marca os pontos de interrupção atingidos na sessão de depuração. Clique em um evento para selecioná-lo na lista de detalhes do **Depurador**.  
  
-   O gráfico **Utilização de CPU** mostra a alteração na utilização da CPU entre todos os núcleos de processador na sessão de depuração.  
  
-   A lista **Eventos** do painel de detalhes **Depurador** inclui itens para cada evento de interrupção.  
  
-   A coluna **Duração** de um evento de interrupção exibe o tempo decorrido entre o evento e o ponto de interrupção anterior.  
  
## <a name="turn-perftips-on-or-off"></a>Ativar ou desativar PerfTips  
 Para habilitar ou desabilitar PerfTips:  
  
1.  No menu **Depurar**, escolha **Opções**.  
  
2.  Marque ou desmarque **Mostrar tempo decorrido PerfTip durante a depuração**.  
  
## <a name="turn-the-diagnostic-tools-window-on-or-off"></a>Ativar ou desativar a janela de Ferramentas de Diagnóstico  
 Para habilitar ou desabilitar a janela de Ferramentas de Diagnóstico:  
  
1.  No menu **Depurar**, escolha **Opções**.  
  
2.  Marque ou desmarque **Habilitar ferramentas de diagnóstico durante a depuração**.

## <a name="see-also"></a>Consulte também
 [Criação de perfis no Visual Studio](../profiling/index.md)  
 [Introdução às ferramentas de criação de perfil](../profiling/profiling-feature-tour.md)
