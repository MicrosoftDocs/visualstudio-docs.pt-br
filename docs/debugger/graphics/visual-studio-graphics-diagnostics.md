---
title: Diagnóstico de gráficos | Microsoft Docs
description: Visual Studio Diagnóstico de Gráficos é um conjunto de ferramentas para registrar em log e analisar a atividade do Direct3D. Use-os para solucionar problemas de renderização e desempenho.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.graphics
ms.assetid: fa69c550-62a7-41b5-bb1f-7eb04af1a6e8
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b6b769131831a0f1f94aa4fcc8e94a9a88bf9890
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386118"
---
# <a name="visual-studio-graphics-diagnostics"></a>Diagnóstico de gráficos do Visual Studio
>[!NOTE]
> Visual Studio recomendaMOS o PIXEL no Windows para jogos do DirectX 12. [OJUST no Windows](https://aka.ms/PIXonWindows) é uma ferramenta de depuração e ajuste de desempenho que dá suporte total ao DirectX 12. [Saiba mais ou baixe](visual-studio-graphics-diagnostics-directx-12.md) [aqui](https://aka.ms/downloadPIX).

Visual Studio *Diagnóstico de Gráficos* é um conjunto de ferramentas para gravação e análise de problemas de renderização e desempenho em aplicativos Direct3D. Diagnóstico de Gráficos pode ser usado em aplicativos que estão sendo executados localmente em seu computador Windows, em um emulador de dispositivo Windows ou em um computador remoto ou dispositivo.

 O Diagnóstico de Gráficos de trabalho começa capturando um registro de como seu aplicativo usa o Direct3D , ao vivo, conforme ele é executado, para que seu comportamento possa ser analisado imediatamente, compartilhado ou salvo para uso posterior. As sessões de captura podem ser iniciadas e controladas manualmente Visual Studio ou com a ferramenta de captura de linha de **comandodxcap.exe**. As sessões de captura também podem ser iniciadas e controladas programaticamente usando as APIs Diagnóstico de Gráficos de captura.

 Depois que uma sessão de captura tiver sido registrada, seu conteúdo poderá ser interpretado pelo Visual Studio *Graphics Analyzer* a qualquer momento, recriando os quadros capturados usando exatamente os mesmos recursos e comandos de renderização usados pelo aplicativo. Em seguida, usando as ferramentas fornecidas na janela Analisador de Gráficos, qualquer um dos quadros capturados pode ser analisado em detalhes. Essas ferramentas podem ser usadas para examinar qualquer chamada à API direct3D, recurso, objeto de estado de pipeline, estágio de pipeline ou até mesmo o histórico completo de qualquer pixel em um quadro capturado. Usando essas ferramentas em conjunto, um problema de renderização pode ser explorado intuitivamente, começando pela forma como ele aparece em um quadro capturado e fazendo drill down até sua causa raiz no código-fonte, sombreadores ou ativos gráficos do aplicativo.

 Para diagnosticar problemas de desempenho, um quadro capturado pode ser analisado usando a ferramenta *Análise de* Quadros. Essa ferramenta explora possíveis otimizações de desempenho alterando automaticamente a maneira como o aplicativo usa o Direct3D e avaliando todas as variações para você. No passado, você poderia ter feito e feito o parâmetro de comparação desses tipos de alterações manualmente apenas para descobrir quais delas fizeram a diferença. Com a Análise de Quadro, você só precisa fazer as alterações que já sabe que serão pagas.

 Diagnóstico de Gráficos ajuda seu aplicativo Direct3D graficamente rico a procurar e executar o melhor.

 Continue para [Visão geral](overview-of-visual-studio-graphics-diagnostics.md) para saber mais sobre o que Visual Studio Diagnóstico de Gráficos oferece.

## <a name="in-this-section"></a>Nesta seção
 [Visão geral](overview-of-visual-studio-graphics-diagnostics.md) Apresenta o fluxo de Diagnóstico de Gráficos e as ferramentas.

 [Ponto de Partida](getting-started-with-visual-studio-graphics-diagnostics.md) Nesta seção, você aprenderá a instalar o Visual Studio Diagnóstico de Gráficos e a começar a usar Diagnóstico de Gráficos seu aplicativo Direct3D.

 [Capturando informações de elementos gráficos](capturing-graphics-information.md) Para usar Diagnóstico de Gráficos examinar um problema de renderização em seu aplicativo, primeiro você registra informações sobre como o aplicativo usa o DirectX. Durante a sessão de gravação, enquanto o aplicativo é executado normalmente, você *captura* (ou seja, seleciona) os quadros de interesse. A captura contém informações detalhadas sobre como os quadros são renderizados. É possível salvar as informações capturadas como um documento de log de gráficos para examinar mais tarde ou compartilhar com outros membros da equipe.

 [Uso de GPU](../../profiling/gpu-usage.md) Para usar Diagnóstico de Gráficos perfil do aplicativo, use a ferramenta Uso de GPU. O uso da GPU pode ser usado em conjunto com outras ferramentas de criação de perfil, como o Uso da CPU, para correlacionar a atividade de CPU e GPU que pode contribuir para problemas de desempenho em seu aplicativo.

 [Documento de log de gráficos](graphics-log-document.md) Para iniciar o exame de um log de gráficos gravado, use a janela do documento Log de Gráficos para selecionar um quadro capturado , ou até mesmo um pixel específico, para que você possa examinar detalhadamente os eventos *(ou* seja, as chamadas à API do DirectX) que o afetam.

 [Análise de quadro](graphics-frame-analysis.md) Depois de selecionar um quadro, use o Análise de Quadros de Gráficos para examinar e ajustar o desempenho de renderização.

 [Lista de eventos](graphics-event-list.md) Depois de selecionar um quadro, use a Lista de Eventos **gráficos** para examinar seus eventos para determinar se eles estão relacionados ao problema de renderização.

 [Estado](graphics-state.md) A janela Estado ajuda você a entender o estado gráfico que está ativo no momento do evento atual.

 [Estágios de pipeline](graphics-pipeline-stages.md) Na janela **Estágios** do Pipeline de Gráficos, investigue como o evento selecionado no momento é processado por cada estágio do pipeline de gráficos para que você possa identificar onde o problema de renderização aparece pela primeira vez. Examinar os estágios do pipeline é especialmente útil quando um objeto não aparece devido a uma transformação incorreta ou quando um dos estágios produz uma saída que não corresponde ao que o próximo estágio espera.

 [Pilha de Chamada de Evento](graphics-event-call-stack.md) Use a **Pilha de** Chamada de Evento gráfico para examinar a pilha de chamada do evento selecionado no momento para que você possa navegar até o código do aplicativo relacionado ao problema de renderização.

 [Histórico de pixels](graphics-pixel-history.md) Usando a janela Histórico de **Pixels Gráficos** para analisar como o pixel selecionado no momento é afetado pelos eventos que o influenciaram, você pode identificar o evento ou a combinação de eventos que causam determinados tipos de problemas de renderização. O histórico de pixel é especialmente útil quando um objeto é renderizado incorretamente porque a saída do sombreador de pixel está incorreta ou foi combinada incorretamente com o buffer de quadro, ou quando um objeto não aparece porque seus pixels foram descartados antes de atingir o buffer de quadro.

 [Tabela de objetos](graphics-object-table.md) Use a **Tabela de Objetos Gráficos** para examinar as propriedades e o conteúdo de objetos e recursos específicos do Direct3D que estão em vigor para o evento selecionado no momento. A tabela de objetos pode ajudar a determinar o contexto do dispositivo gráfico que está ativo durante um evento e examinar os conteúdos de recursos gráficos, como buffers constantes, buffers de vértices e texturas.

 [Depurador HLSL](hlsl-shader-debugger.md) Para examinar como o código de sombreador para o estágio de pipeline de eventos e gráficos selecionados no momento se comporta, use o **Depurador HLSL** para passar pelo código, examinar o conteúdo das variáveis e executar outras tarefas típicas de depuração. Também é possível usar o depurador HLSL para examinar o código do sombreador de computação, independente de os resultados serem processados mais pelo pipeline de gráficos ou apenas relidos pelo aplicativo.

 [Ferramenta de captura de linha de comando](command-line-capture-tool.md) Use a ferramenta de captura de linha de comando para capturar e reproduzir rapidamente informações gráficas sem usar Visual Studio ou captura programática. Em particular, você pode usar a ferramenta de captura de linha de comando para automação ou em um ambiente de teste.

 [Exemplos](graphics-diagnostics-examples.md) Vários exemplos demonstram como usar as ferramentas Diagnóstico de Gráficos para diagnosticar diferentes tipos de problemas de renderização.

## <a name="related-sections"></a>Seções relacionadas

| Título | Descrição |
| - | - |
| [Tour de recursos do depurador](../debugger-feature-tour.md) | Apresenta a funcionalidade de depuração no [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. |
| [Elementos gráficos e jogos do DirectX](/windows/win32/directx) | Fornece artigos que discutem as tecnologias de gráficos do DirectX. |
| [Suporte ao DirectX 12 no Visual Studio](visual-studio-graphics-diagnostics-directx-12.md) | Saiba mais sobre o suporte ao DirectX 12 Visual Studio |
