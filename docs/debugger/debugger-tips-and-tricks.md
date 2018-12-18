---
title: Dicas e truques no depurador
description: Saiba mais sobre alguns dos recursos menos conhecidos suportados pelo depurador do Visual Studio
ms.custom: seodec18
ms.date: 06/15/2017
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- stepping
- debugging [Visual Studio], execution control
- execution, controlling in debugger
ms.assetid: 5262d8b1-2648-429e-85d5-90fcaadfb362
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 238236df48adab491cd8a1f9282a8f6a440c5321
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53055219"
---
# <a name="learn-productivity-tips-and-tricks-for-the-debugger-in-visual-studio"></a>Aprender dicas de produtividade e truques do depurador no Visual Studio

Leia este tópico para aprender algumas dicas de produtividade e truques para o depurador do Visual Studio. Para ver os recursos básicos do depurador, consulte [tour pelos recursos do depurador](../debugger/debugger-feature-tour.md). Neste tópico, abordaremos algumas áreas que não estão incluídas no tour do recurso.

## <a name="pin-data-tips"></a>Dicas de dados do PIN

Se você passar com frequência sobre dicas de dados durante a depuração, você talvez queira fixar a dica de dados para a variável para lhe dar acesso rápido. A variável permanece fixada mesmo após a reinicialização. Para fixar a dica de dados, clique no ícone de pino ao passar o mouse sobre ele. Você pode fixar diversas variáveis.

![A fixação de uma dica de dados](../debugger/media/dbg-tips-data-tips-pinned.png "PinningDataTip")

## <a name="edit-your-code-and-continue-debugging-c-vb-c"></a>Editar seu código e continuar a depuração (c#, VB, C++)

Na maioria dos idiomas com suporte do Visual Studio, você pode editar seu código no meio de uma sessão de depuração e continuar a depuração. Para usar esse recurso, clique em seu código com o seu cursor enquanto estiver em pausa no depurador, editar e pressione **F5**, **F10**, ou **F11** para continuar a depuração.

![Editar e continuar a depuração](../debugger/media/dbg-tips-edit-and-continue.gif "EditAndContinue")

Para obter mais informações sobre como usar o recurso e limitações de recursos, consulte [editar e continuar](../debugger/edit-and-continue.md).

## <a name="debug-issues-that-are-hard-to-reproduce"></a>Problemas de depuração que são difíceis de reproduzir

Se for difícil ou demorado recriar um estado específico em seu aplicativo, considere se o uso de um ponto de interrupção condicional pode ajudar. Você pode usar [pontos de interrupção condicionais](../debugger/using-breakpoints.md#BKMK_Specify_a_breakpoint_condition_using_a_code_expression) e filtrar pontos de interrupção para evitar a interrupção no código do aplicativo até que o aplicativo entra em um estado desejado (por exemplo, um estado em que uma variável está armazenando dados incorretos). Você pode definir condições usando expressões, filtros, contagens de ocorrências e assim por diante.

#### <a name="to-create-a-conditional-breakpoint"></a>Para criar um ponto de interrupção condicional

1. Um ícone de ponto de interrupção (a bola vermelha) com o botão direito e escolha **condições**.

2. No **configurações de ponto de interrupção** janela, digite uma expressão.

    ![Ponto de interrupção condicional](../debugger/media/dbg-multithreaded-conditional-breakpoint.png "ConditionalBreakpoint")

3. Se você estiver interessado em outro tipo de condição, selecione **filtro** em vez de **expressão condicional** no **configurações de ponto de interrupção** caixa de diálogo e, em seguida, siga o dicas de filtro.

## <a name="change-the-execution-flow"></a>Alterar o fluxo de execução

Com o depurador em pausa em uma linha de código, use o mouse para captar o ponteiro de seta amarela à esquerda. Mova o ponteiro de seta amarela para um ponto diferente no caminho de execução do código. Em seguida, use F5 ou um comando de etapa para continuar a execução do aplicativo.

![Mova o ponteiro de execução](../debugger/media/dbg-tour-move-the-execution-pointer.gif "mover o ponteiro de execução")

Alterando o fluxo de execução, você pode fazer coisas como testar caminhos de execução de código diferentes ou executar novamente o código sem reiniciar o depurador.

> [!WARNING]
> Geralmente, você precisa ter cuidado com esse recurso. Um aviso é exibido na dica de ferramenta. Outros avisos também podem ser exibidos. Movendo o ponteiro não é possível reverter o seu aplicativo para um estado anterior do aplicativo.

## <a name="track-an-out-of-scope-object-c-visual-basic"></a>Controlar um objeto fora do escopo (c#, Visual Basic)

É fácil exibir variáveis usando as janelas do depurador, como o **inspeção** janela. No entanto, quando uma variável sai do escopo na **inspeção** janela, você pode perceber que está esmaecido. Em alguns cenários de aplicativo, o valor de uma variável pode ser alterada até mesmo quando a variável está fora do escopo, e talvez você queira estar atento a ele (por exemplo, uma variável pode obter coleta de lixo). Você pode acompanhar a variável, criando uma ID de objeto para ele na **inspeção** janela.

#### <a name="to-create-an-object-id"></a>Para criar uma ID de objeto

1.  Defina um ponto de interrupção perto de uma variável que você deseja controlar.

2.  Inicie o depurador (**F5**) e interromperá no ponto de interrupção.

3. Localize a variável na **Locals** janela (**Depurar > Windows > Locals**), a variável com o botão direito e selecione **criar ID de objeto**.

    ![Criar uma ID de objeto](../debugger/media/dbg-tips-watch-create-object-id.png "CreateObjectID")
  
4.  Você deve ver uma **$** além de um número no **locais** janela. Essa variável é a ID de objeto.
  
5.  A variável de ID de objeto com o botão direito e escolha **Adicionar inspeção**.

Para obter mais informações, consulte [criar uma ID de objeto](../debugger/watch-and-quickwatch-windows.md#bkmk_objectIds).

## <a name="view-return-values-for-functions"></a>Modo de exibição de valores de retorno para funções

Para exibir valores de retorno para suas funções, examinar as funções que aparecem na **automóveis** janela enquanto estiver depurando seu código. Para ver o valor de retorno para uma função, certifique-se de que a função que você está interessado já foi executada (pressione **F10** uma vez se você estiver parado no momento na chamada de função). Se a janela for fechada, use **Depurar > Windows > Autos** para abrir o **Autos** janela.

![Janela de automóveis](../debugger/media/dbg-tips-autos-window.png "AutosWindow")

Além disso, você pode inserir funções na **imediato** janela para exibir valores de retorno. (Abri-lo usando **Depurar > Windows > imediato**.)

![Janela imediata](../debugger/media/dbg-tips-immediate-window.png "ImmediateWindow")

Você também pode usar [pseudovariáveis](../debugger/pseudovariables.md) na **inspeção** e **imediato** janela, tal como `$ReturnValue`.

## <a name="string_visualizer"></a>Inspecione as cadeias de caracteres em um visualizador

Ao trabalhar com cadeias de caracteres, ele pode ser útil exibir a cadeia de caracteres formatada inteira. Para exibir um texto sem formatação, a cadeia de caracteres JSON, HTML ou XML, clique no ícone de lupa ![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "ícone do visualizador") ao focalizar uma variável que contém um valor de cadeia de caracteres.

![Abrir um visualizador de cadeia de caracteres](../debugger/media/dbg-tips-string-visualizers.png "OpenStringVisualizer")

Um visualizador de cadeia de caracteres pode ajudá-lo a descobrir se uma cadeia de caracteres está malformada, dependendo do tipo de cadeia de caracteres. Por exemplo, um espaço em branco **valor** campo indica a cadeia de caracteres não é reconhecida pelo tipo de visualizador. Para obter mais informações, consulte [caixa de diálogo do Visualizador de cadeia de caracteres](../debugger/string-visualizer-dialog-box.md).

![Visualizador de cadeia de caracteres JSON](../debugger/media/dbg-tips-string-visualizer-json.png "JSONStringVisualizer")

Para alguns outros tipos como objetos do WPF que aparecem nas janelas do depurador, você também pode abrir os visualizadores.

## <a name="break-into-code-on-handled-exceptions"></a>Entrar no código em exceções manipuladas

O depurador interrompe no seu código em exceções sem tratamento. Exceções tratadas no entanto, (como exceções que ocorrem dentro de um `try/catch` bloco) também pode ser uma fonte de bugs e talvez você queira investigar quando eles ocorrem. Você pode configurar o depurador para entrar no código para exceções controladas também Configurando opções na **configurações de exceção** caixa de diálogo. Abra essa caixa de diálogo, escolhendo **Depurar > Windows > configurações de exceção**.

O **configurações de exceção** caixa de diálogo permite que você conte o depurador para entrar no código em exceções específicas. Na ilustração abaixo, o depurador interrompe no seu código sempre que um `System.NullReferenceException` ocorre. Para obter mais informações, consulte [Gerenciando exceções](../debugger/managing-exceptions-with-the-debugger.md).

![Caixa de diálogo de configurações de exceção](../debugger/media/dbg-tips-exception-settings.png "ExceptionSettingsDialogBox")

## <a name="debug-deadlocks-and-race-conditions"></a>Depurar deadlocks e condições de corrida

Se você precisar depurar os tipos de problemas que são comuns a aplicativos multithreaded, geralmente é útil para exibir o local de threads durante a depuração. Você pode fazer isso facilmente usando o **Mostrar Threads em origem** botão.

#### <a name="to-show-threads-in-your-source-code"></a>Mostrar threads em seu código-fonte

1.  Durante a depuração, clique o **Mostrar Threads em origem** botão ![Mostrar Threads em origem](../debugger/media/dbg-multithreaded-show-threads.png "ThreadMarker") no **depurar** barra de ferramentas.
  
2.  Examine a medianiz no lado esquerdo da janela. Nessa linha, você verá uma *marcador de thread* ícone ![marcador de Thread](../debugger/media/dbg-thread-marker.png "ThreadMarker") que se parece com dois threads de pano. O marcador de thread indica que um thread está parado nesse local.

    Observe que um marcador de thread pode ser escondido parcialmente por um ponto de interrupção.
  
3.  Passe o ponteiro sobre o marcador de thread. Um DataTip aparece. O DataTip mostra o nome e o número de ID do thread para cada thread parado.

    Você também pode exibir o local de threads na [janela pilhas paralelas](../debugger/get-started-debugging-multithreaded-apps.md).

## <a name="examine-payloads-for-web-services-and-network-resources-uwp"></a>Examine as cargas de recursos de rede (UWP) e serviços da web

Em aplicativos UWP, você pode analisar as operações de rede executadas usando o `Windows.Web.Http` API. Você pode usar essa ferramenta para ajudar a depurar serviços da web e recursos de rede. Para usar a ferramenta, selecione **Depurar > desempenho Profiler**. Selecione **rede**e, em seguida, escolha **iniciar**. No aplicativo, percorra o cenário que usa `Windows.Web.Http` e escolha **Parar coleta** para gerar o relatório.

![Uso da ferramenta de criação de perfil de rede](../profiling/media/prof-tour-network-usage.png "NetworkUsageProfTool")

Selecione uma operação na exibição de resumo para exibir mais detalhes.

![Mais informações na ferramenta de uso de rede](../profiling/media/prof-tour-network-usage-details.png "DetailedViewNetworkUsage")

Para obter mais informações, consulte [Uso de rede](../profiling/network-usage.md).

## <a name="modules_window"></a> Se familiarizar mais com como o depurador se anexa ao aplicativo (C#, C++, Visual Basic, F#)

Para anexar a seu aplicativo em execução, o depurador carrega arquivos de símbolo (. PDB) gerados para o mesmo build exato do aplicativo que você está tentando depurar. Em alguns cenários, um pouco conhecimento dos arquivos de símbolo pode ser útil. Você pode examinar como o Visual Studio carrega os arquivos de símbolo usando o **módulos** janela.

Abra o **módulos** janela durante a depuração, selecionando **Depurar > Windows > módulos**. O **módulos** janela pode informar quais módulos que o depurador está tratando como o código do usuário, ou [ *meu código*](../debugger/just-my-code.md)e o status para o módulo de carregamento de símbolos. Na maioria dos cenários, o depurador encontra automaticamente os arquivos de símbolo para código do usuário, mas se você quiser depurar (ou depurar) código do .NET framework, o código do sistema ou o código da biblioteca de terceiros, etapas adicionais são necessárias para obter os arquivos de símbolo correto.

![Exibir informações de símbolo na janela de módulos](../debugger/media/dbg-tips-modules-window.png "ViewSymbolInformation")

Você pode carregar informações de símbolo diretamente a partir de **módulos** janela clicando com botão direito e escolhendo **carregar símbolos**.

Às vezes, os desenvolvedores de aplicativo envie aplicativos sem os símbolo arquivos correspondentes (para reduzir a superfície), mas mantenha uma cópia do símbolo correspondente de arquivos para a compilação para que ele podem depurar uma versão de lançamento mais tarde.

Para descobrir como o depurador classifica o código como código de usuário, consulte [Just My Code](../debugger/just-my-code.md). Para obter mais informações sobre arquivos de símbolo, consulte [especificar o símbolo (. PDB) e arquivos de origem no depurador do Visual Studio](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="learn-more"></a>Saiba mais

Para obter mais dicas e truques e informações mais detalhadas, consulte essas postagens de blog:

- [7 menos conhecidos de hackers para depuração no Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2017/06/26/7-lesser-known-hacks-for-debugging-in-visual-studio/)
- [7 gems ocultas no Visual Studio](https://blogs.msdn.microsoft.com/visualstudio/2017/10/05/7-hidden-gems-in-visual-studio-2017/)

## <a name="see-also"></a>Consulte também
[Atalhos de teclado](../ide/tips-and-tricks-for-visual-studio.md)
