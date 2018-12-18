---
title: 'Passo a passo: Usando diagnóstico de gráficos para depurar um sombreador de cálculo | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 69287456-644b-4aff-bd03-b1bbb2abb82a
caps.latest.revision: 15
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 55f0b9de879011110d8df46c0e4d738265b0fa34
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730650"
---
# <a name="walkthrough-using-graphics-diagnostics-to-debug-a-compute-shader"></a>Instruções passo a passo: usando diagnóstico de gráficos para depurar um sombreador computado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo demonstra como usar as ferramentas de diagnóstico de gráficos do Visual Studio para investigar um sombreador de cálculo que produz resultados incorretos.  
  
 Este passo a passo ilustra essas tarefas:  
  
-   Usando o **lista de eventos gráficos** para localizar fontes potenciais do problema.  
  
-   Usando o **pilha de chamadas do evento de gráficos** para determinar qual computador sombreador é executado por um DirectCompute `Dispatch` eventos.  
  
-   Usando o **estágios de Pipeline gráficos** janela e HLSL do depurador para examinar o sombreador de cálculo que é a origem do problema.  
  
## <a name="scenario"></a>Cenário  
 Nesse cenário, você escreveu uma simulação de dinâmica de fluidos que usa DirectCompute para executar as partes de computação mais intensa da atualização de simulação. Quando o aplicativo é executado, o processamento do conjunto de dados e da interface do usuário estiverem corretas, mas a simulação não se comportar conforme o esperado. Usando o diagnóstico de gráficos, você pode capturar o problema para um log de gráficos para que você possa depurar o aplicativo. O problema se parece com isso no aplicativo:  
  
 ![O fluido simulado se comportar incorretamente. ](../debugger/media/gfx-diag-demo-compute-shader-fluid-problem.png "gfx_diag_demo_compute_shader_fluid_problem")  
  
 Para obter informações sobre como capturar problemas de gráficos no log de gráficos, consulte [capturando informações de gráficos](../debugger/capturing-graphics-information.md).  
  
## <a name="investigation"></a>Investigação  
 Você pode usar as ferramentas de diagnóstico de gráficos para carregar o arquivo de log de gráficos para que você possa inspecionar os quadros capturados.  
  
#### <a name="to-examine-a-frame-in-a-graphics-log"></a>Para examinar um quadro no log de gráficos  
  
1. No Visual Studio, carregue um log de gráficos que contém um quadro que exibe os resultados da simulação incorretos. Uma nova guia de diagnóstico de gráficos aparece no Visual Studio. Na parte superior dessa guia é a saída de destino de renderização do quadro selecionado. Na parte inferior é parte do **lista de quadros**, que exibe uma miniatura de cada quadro capturado.  
  
2. No **lista de quadros**, selecione um quadro que demonstra o comportamento de simulação incorretos. Mesmo que o erro parece estar em código de simulação e não o código de renderização, você precisa escolher um quadro porque os eventos de DirectCompute são capturados em uma base quadro a quadro, juntamente com eventos do Direct3D. Nesse cenário, os gráficos de log guia semelhante ao seguinte:  
  
    ![Documento de log de gráficos no Visual Studio. ](../debugger/media/gfx-diag-demo-compute-shader-fluid-step-1.png "gfx_diag_demo_compute_shader_fluid_step_1")  
  
   Depois de selecionar um quadro que demonstra o problema, você pode usar o **lista de eventos gráficos** para diagnosticá-lo. O **lista de eventos gráficos** contém um evento para cada chamada de DirectCompute e a chamada à API do Direct3D que foi feita durante o quadro ativo — por exemplo, chamadas de API para executar uma computação na GPU, ou para processar o conjunto de dados ou a interface do usuário. Nesse caso, estamos interessados em `Dispatch` eventos que representam partes da simulação que são executados na GPU.  
  
#### <a name="to-find-the-dispatch-event-for-the-simulation-update"></a>Para localizar o evento de distribuição da atualização de simulação  
  
1. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **lista de eventos** para abrir o **lista de eventos gráficos** janela.  
  
2. Inspecione o **lista de eventos gráficos** para o evento de desenho que renderiza o conjunto de dados. Para facilitar essa tarefa, digite `Draw` no **pesquisa** caixa no canto superior direito dos **lista de eventos gráficos** janela. Isso filtra a lista para que ele contenha somente os eventos que possuam "Desenho" em seus títulos. Nesse cenário, você descobre que esses eventos de desenho ocorreram:  
  
    ![A lista de eventos &#40;EL&#41; mostra eventos de desenho. ](../debugger/media/gfx-diag-demo-compute-shader-fluid-step-2.png "gfx_diag_demo_compute_shader_fluid_step_2")  
  
3. Percorrer cada evento de desenho enquanto assiste o destino de renderização na guia de documento de log de gráficos.  
  
4. Pare quando o destino de renderização exibe o dataset processado primeiro. Nesse cenário, o conjunto de dados é renderizado no primeiro evento de desenho. O erro na simulação é mostrado:  
  
    ![Isso desenhar evento processa o conjunto de dados de simulação. ](../debugger/media/gfx-diag-demo-compute-shader-fluid-step-3.png "gfx_diag_demo_compute_shader_fluid_step_3")  
  
5. Inspecione agora a **lista de eventos gráficos** para o `Dispatch` eventos que atualiza a simulação. Porque é provável que a simulação é atualizada para que ele seja processado, você pode concentrar-se primeiro `Dispatch` eventos que ocorrem antes do evento de desenho que renderiza os resultados. Para facilitar essa tarefa, modifique a **pesquisa** caixa para ler `Draw;Dispatch;CSSetShader(`. Isso filtra a lista para que ele também contém `Dispatch` e `CSSetShader` eventos além dos eventos de desenho. Nesse cenário, você descobre que vários `Dispatch` eventos ocorridos antes do evento de desenho:  
  
    ![Mostra o EL eventos de desenho, expedição e CSSetShader](../debugger/media/gfx-diag-demo-compute-shader-fluid-step-4.png "gfx_diag_demo_compute_shader_fluid_step_4")  
  
   Agora que você sabe que provavelmente alguns de muitos `Dispatch` eventos poderiam corresponder ao problema, você pode examiná-los mais detalhadamente.  
  
#### <a name="to-determine-which-compute-shader-a-dispatch-call-executes"></a>Para determinar a qual uma chamada de expedição do sombreador de cálculo é executado.  
  
1. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **pilha de chamadas do evento** para abrir o **pilha de chamadas do evento de gráficos** janela.  
  
2. A partir do evento de desenho que renderiza os resultados da simulação, retroceder cada anterior `CSSetShader` eventos. Em seguida, nos **pilha de chamadas do evento de gráficos** janela, escolha a função principal para navegar até o site de chamada. No site de chamada, você pode usar o primeiro parâmetro do [CSSetShader](http://msdn.microsoft.com/library/ff476402.aspx) chamada de função para determinar qual computador sombreador é executado pelo próximo `Dispatch` eventos.  
  
   Nesse cenário, há três pares de `CSSetShader` e `Dispatch` eventos em cada quadro. Trabalhando com versões anteriores, a terceiro par representa a integração de etapa (onde as partículas fluidas são movidas realmente), o segundo par representa a etapa de cálculo por força (onde as forças que afetam cada partícula são calculadas) e o primeiro par representa o etapa de cálculo por densidade.  
  
#### <a name="to-debug-the-compute-shader"></a>Para depurar o sombreador de cálculo  
  
1. Sobre o **diagnóstico de gráficos** barra de ferramentas, escolha **estágios de Pipeline** para abrir o **estágios de Pipeline gráficos** janela.  
  
2. Selecione o terceiro `Dispatch` evento (aquele que precede imediatamente o evento de desenho) e, em seguida, no **estágios de Pipeline gráficos** janela, sob o **sombreador de cálculo** estágio, escolha  **Iniciar a depuração**.  
  
    ![Selecionando o terceiro evento de expedição no EL.](../debugger/media/gfx-diag-demo-compute-shader-fluid-step-6.png "gfx_diag_demo_compute_shader_fluid_step_6")  
  
    O depurador de HLSL é iniciado no sombreador que executa a etapa de integração.  
  
3. Examine o código-fonte do sombreador de cálculo a etapa de integração pesquisar a origem do erro. Quando você usa o diagnóstico de gráficos para depurar o código de sombreador de cálculo do HLSL, você pode percorrer o código e usar outras ferramentas de depuração familiares, como janelas de inspeção. Nesse cenário, você determinar que não parece haver um erro no computador sombreador que executa a etapa de integração.  
  
    ![Depurar o sombreador de cálculo IntegrateCS. ](../debugger/media/gfx-diag-demo-compute-shader-fluid-step-7.png "gfx_diag_demo_compute_shader_fluid_step_7")  
  
4. Para parar a depuração do sombreador de cálculo na **Debug** barra de ferramentas, escolha **parar depuração** (teclado: Shift + F5).  
  
5. Em seguida, selecione o segundo `Dispatch` evento e inicie a depuração do sombreador de cálculo, exatamente como você fez na etapa anterior.  
  
    ![Selecionar o segundo evento de expedição no EL.](../debugger/media/gfx-diag-demo-compute-shader-fluid-step-8.png "gfx_diag_demo_compute_shader_fluid_step_8")  
  
    O depurador de HLSL é iniciado no sombreador que calcula os pontos que atuam em cada partícula fluida.  
  
6. Examine o código de origem do sombreador de computação para a etapa de cálculo por força. Nesse cenário, você determinar que a origem do erro está aqui.  
  
    ![Depurando o ForceCS&#95;sombreador de cálculo simples. ](../debugger/media/gfx-diag-demo-compute-shader-fluid-step-9.png "gfx_diag_demo_compute_shader_fluid_step_9")  
  
   Depois de determinar o local do erro, você pode parar a depuração e modificar o código de origem do sombreador de cálculo para calcular corretamente a distância entre as partículas em interação. Nesse cenário, você altera apenas a linha `float2 diff = N_position + P_position;` para `float2 diff = N_position - P_position;`:  
  
   ![A computação corrigida&#45;código de sombreador. ](../debugger/media/gfx-diag-demo-compute-shader-fluid-step-10.png "gfx_diag_demo_compute_shader_fluid_step_10")  
  
   Nesse cenário, porque os computadores sombreadores são compilados em tempo de execução, você pode simplesmente reiniciar o aplicativo depois de fazer as alterações para observar como eles afetam a simulação. Você não precisa recompilar o aplicativo. Quando você executa o aplicativo, você descobre que a simulação agora se comporta corretamente.  
  
   ![O fluido simulado se comporta corretamente. ](../debugger/media/gfx-diag-demo-compute-shader-fluid-resolution.png "gfx_diag_demo_compute_shader_fluid_resolution")



