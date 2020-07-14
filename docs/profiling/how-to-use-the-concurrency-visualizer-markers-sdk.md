---
title: Como usar o SDK de marcadores do Visualizador de simultaneidade | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 19a45032-f8a7-4137-890e-2ceeec938b8d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0782744236777fb84a6d87f93f59697275df1c11
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85331387"
---
# <a name="how-to-use-the-concurrency-visualizer-markers-sdk"></a>Como usar o SDK de marcadores de Visualização Simultânea
Este tópico mostra como usar o SDK da Visualização Simultânea para criar intervalos e gravar sinalizadores, mensagens e alertas.

### <a name="to-use-c"></a>Para usar o C++

1. Adicione o suporte ao SDK da Visualização Simultânea ao seu aplicativo. Para obter mais informações, consulte [SDK da Visualização Simultânea](../profiling/concurrency-visualizer-sdk.md).

2. Adicione uma instrução `include` e uma instrução `using` para o SDK.

    ```cpp
    #include <cvmarkersobj.h>
    using namespace Concurrency::diagnostic;
    ```

3. Adicione o código para criar três intervalos na série de marcador padrão e gravar um sinalizador, uma mensagem e um alerta, um para cada intervalo. Os métodos para gravar sinalizadores, mensagens e alertas são membros da classe [marker_series](../profiling/marker-series-class.md). O construtor para a classe [span](../profiling/span-class.md) requer um objeto `marker_series`, de modo que cada intervalo seja associado a uma série de marcador específica. Um `span` termina quando ele é excluído.

    ```cpp
    marker_series series;
    span *flagSpan = new span(series, 1, _T("flag span"));
    series.write_flag(_T("Here is the flag."));
    delete flagSpan;

    span *messageSpan = new span(series, 2, _T("message span"));
    series.write_flag(_T("Here is the message."));
    delete messageSpan;

    span *alertSpan = new span(series, 3, _T("alert span"));
    series.write_flag(_T("Here is the alert."));
    delete alertSpan;
    ```

4. Na barra de menus, escolha **Analisar**, **Visualização Simultânea**, **Iniciar com Projeto Atual** para executar o aplicativo e exibir a Visualização Simultânea. A ilustração a seguir mostra os três intervalos e os três marcadores na Visualização Simultânea.

     ![Visualizador de simultaneidade com 3 marcadores e alertas](../profiling/media/cvmarkersnative.png "CvMarkersNative")

5. Adicione código para criar a série de marcador personalizada adicional chamando o construtor para `marker_series` que aceita um nome de cadeia de caracteres para uma série de marcadores.

    ```cpp
    marker_series flagSeries(_T("flag series"));
    span *flagSeriesSpan = new span(flagSeries, 1, _T("flag span"));
    flagSeries.write_flag(1, _T("flag"));
    // Sleep to even out the display in the Concurrency Visualizer.
    Sleep(50);
    delete flagSeriesSpan;

    marker_series messageSeries(_T("message series"));
    span *messageSeriesSpan = new span(messageSeries, 1, _T("message span"));
    messageSeries.write_message(1, _T("message"));
    // Sleep to even out the display in the Concurrency Visualizer.
    Sleep(50);
    delete messageSeriesSpan;
    ```

6. Inicie o projeto atual para exibir Visualização Simultânea. As duas séries de marcador aparecem em suas próprias pistas na Exibição de Threads. A ilustração a seguir mostra os dois novos intervalos.

     ![Visualizador de simultaneidade com 3 séries de marcador personalizado](../profiling/media/cvmarkerseriesnative.png "CvMarkerSeriesNative")

### <a name="to-use-visual-basic-or-c"></a>Para usar o Visual Basic ou o C\#

1. Adicione o suporte ao SDK da Visualização Simultânea ao seu aplicativo. Para obter mais informações, consulte [SDK da Visualização Simultânea](../profiling/concurrency-visualizer-sdk.md).

2. Adicione uma instrução `using` ou `Imports` ao SDK.

    ```vb
    Imports Microsoft.ConcurrencyVisualizer.Instrumentation
    ```

    ```csharp
    using Microsoft.ConcurrencyVisualizer.Instrumentation;
    ```

3. Adicione o código para criar três intervalos na série de marcador padrão e gravar um sinalizador, uma mensagem e um alerta, um para cada intervalo. Você cria um objeto [Span](/previous-versions/hh694189(v=vs.140)) chamando o método estático `EnterSpan`. Para escrever a série padrão, use os métodos estáticos de escrita da classe [Marcadores](/previous-versions/hh694099(v=vs.140)).

    ```vb
    Dim flagSpan As Span = Markers.EnterSpan("flag span")
    Markers.WriteFlag("Here is the flag.")
    flagSpan.Leave()

    Dim messageSpan As Span = Markers.EnterSpan("message span")
    ' Sleep for a millisecond to even out the display in the Concurrency Visualizer.
    System.Threading.Thread.Sleep(1)
    Markers.WriteMessage("Here is a message")
    messageSpan.Leave()

    Dim alertSpan As Span = Markers.EnterSpan("alert span")
    ' Sleep for a millisecond to even out the display in the Concurrency Visualizer.
    System.Threading.Thread.Sleep(1)
    Markers.WriteAlert("Here is an alert")
    alertSpan.Leave()
    ```

    ```csharp
    Span flagSpan = Markers.EnterSpan("flag span");
    Markers.WriteFlag("Here is the flag.");
    flagSpan.Leave();

    Span messageSpan = Markers.EnterSpan("message span");
    // Sleep for a millisecond to even out the display in the Concurrency Visualizer.
    System.Threading.Thread.Sleep(1);
    Markers.WriteMessage("Here is a message");
    messageSpan.Leave();

    Span alertSpan = Markers.EnterSpan("alert span");
    // Sleep for a millisecond to even out the display in the Concurrency Visualizer.
    System.Threading.Thread.Sleep(1);
    Markers.WriteAlert("Here is an alert");
    alertSpan.Leave();
    ```

4. Na barra de menus, escolha **Analisar**, **Visualização Simultânea**, **Iniciar com Projeto Atual** para executar o aplicativo e exibir a Visualização Simultânea. A ilustração a seguir mostra os três intervalos e os três marcadores na Exibição de Threads da Visualização Simultânea.

     ![Visualizador de simultaneidade com marcadores e alertas](../profiling/media/cvmarkersmanaged.png "CvMarkersManaged")

5. Adicione código para criar a série de marcador do cliente usando o método estático [CreateMarkerSeries](/previous-versions/hh694171(v=vs.140)). A classe [MarkerSeries](/previous-versions/hh694127(v=vs.140)) contém métodos para criar spans e escrever sinalizadores, mensagens e alertas.

    ```VB

    Dim flagSeries As MarkerSeries = Markers.DefaultWriter.CreateMarkerSeries("flag series")
    Dim flagSeriesSpan As Span = flagSeries.EnterSpan("flag span")
    System.Threading.Thread.Sleep(1)
    flagSeries.WriteFlag(1, "flag")
    System.Threading.Thread.Sleep(1)
    flagSeriesSpan.Leave()

    Dim messageSeries As MarkerSeries = Markers.DefaultWriter.CreateMarkerSeries("message series")
    Dim messageSeriesSpan As Span = messageSeries.EnterSpan("message span")
    messageSeries.WriteMessage("message")
    System.Threading.Thread.Sleep(1)
    messageSeriesSpan.Leave()
    ```

    ```csharp

    MarkerSeries flagSeries = Markers.DefaultWriter.CreateMarkerSeries("flag series");
    Span flagSeriesSpan = flagSeries.EnterSpan("flag span");
    System.Threading.Thread.Sleep(1);
    flagSeries.WriteFlag(1, "flag");
    System.Threading.Thread.Sleep(1);
    flagSeriesSpan.Leave();

    MarkerSeries messageSeries = Markers.DefaultWriter.CreateMarkerSeries("message series");
    Span messageSeriesSpan = messageSeries.EnterSpan("message span");
    messageSeries.WriteMessage("message");
    System.Threading.Thread.Sleep(1);
    messageSeriesSpan.Leave();
    ```

6. Inicie o projeto atual para exibir Visualização Simultânea. As três séries de marcador aparecem em suas próprias pistas na Exibição de Threads. A ilustração a seguir mostra os três novos intervalos.

     ![Visualizador de simultaneidade com 3 séries de marcador personalizado](../profiling/media/cvmarkerseriesmanaged.png "CvMarkerSeriesManaged")

## <a name="see-also"></a>Veja também
- [SDK do Visualizador de Simultaneidade](../profiling/concurrency-visualizer-sdk.md)
