---
title: 'Passo a passo: Melhorando a capacidade de resposta da interface do usuário (HTML) | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- performance tools, JavaScript [Store apps]
- performance, JavaScript [Store apps]
- performance, HTML [Store apps]
- performance tools, HTML [Store apps]
ms.assetid: 7e5a2524-dbf5-4a40-b5d6-2d1ed7fff3de
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f0cf1b080a0e803beda6682265dc383dc43a33d0
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51791131"
---
# <a name="walkthrough-improving-ui-responsiveness-html"></a>Passo a passo: Melhorando a capacidade de resposta da interface de usuário (HTML)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo o orienta no processo de identificação e correção de um problema de desempenho usando o [Criador de perfil de capacidade de resposta de interface do usuário em HTML](../profiling/html-ui-responsiveness.md). O criador de perfil está disponível no Visual Studio para aplicativos universais do Windows e os aplicativos da Windows Store usando JavaScript. Neste cenário, você cria um aplicativo de teste de desempenho que atualiza os elementos DOM com muita frequência e usa o criador de perfil para identificar e corrigir esse problema.  
  
### <a name="creating-and-running-the-performance-test-app"></a>Criando e executando o aplicativo de teste de desempenho  
  
1.  No Visual Studio, crie um novo projeto de JavaScript universal do Windows. (Selecione **Arquivo/Novo/Projeto**. Escolha **JavaScript** no painel esquerdo e depois escolha **Windows**, **Windows 10**, em seguida, **Universal** ou **Windows Phone**.  
  
2.  > [!IMPORTANT]
    >  Os resultados do diagnóstico mostrados neste tópico são mostrados para um aplicativo do Windows 8.  
  
3.  Escolha um dos modelos de projeto em branco no painel central, como **Aplicativo em Branco**.  
  
4.  Na caixa **Nome**, especifique um nome como `JS_Perf_Tester` e escolha **OK**.  
  
5.  No **Gerenciador de Soluções**, abra default.html e cole o seguinte código entre as marcas \<body>:  
  
    ```html  
    <div class="wrapper">  
        <button id="content">Waiting for values</button>  
    </div>  
    ```  
  
6.  Abra default.css e adicione o seguinte código CSS:  
  
    ```css  
    #content {  
        margin-left: 100px;  
        margin-top: 100px;  
    }  
    ```  
  
7.  Abra default.js e substitua todo o código por este:  
  
    ```javascript  
    (function () {  
        "use strict";  
  
        var app = WinJS.Application;  
        var activation = Windows.ApplicationModel.Activation;  
  
        var content;  
        var wrapper;  
  
        app.onactivated = function (args) {  
            if (args.detail.kind === activation.ActivationKind.launch) {  
                if (args.detail.previousExecutionState !== activation.ApplicationExecutionState.terminated) {  
  
                    content = document.getElementById("content");  
                    wrapper = document.querySelector(".wrapper");  
  
                    content.addEventListener("click", handler);  
  
                } else {  
                }  
  
                args.setPromise(WinJS.UI.processAll());  
            }  
        };  
  
        app.oncheckpoint = function (args) {  
        };  
  
        app.start();  
  
        var idx = 0;  
        var count = 0;  
        var max = 5000;  
        var text = ["what", "is", "the", "Matrix?"];  
        var color = ["red", "crimson", "maroon", "purple"];  
  
        function increment() {  
  
            setTimeout(function () {  
  
                idx++;  
                count++;  
  
                if (idx > 3) { idx = 0; }  
                if (count < max) { increment(); }  
  
            }, 1000);  
        }  
  
        function setValues() {  
  
            content = document.getElementById("content");  
            content.removeNode(true);  
  
            var newNode = document.createElement("button");  
            newNode.id = "content";  
            newNode.textContent = text[idx];  
            //newNode.textContent = getData();  
            newNode.style.backgroundColor = color[idx];  
            //newNode.style.animationName = "move";  
            //count++;  
  
            wrapper.appendChild(newNode);  
  
        }  
  
        function update() {  
  
            setTimeout(function () {  
  
                setValues();  
                if (count < max) { update(); }  
            });  
        }  
  
        function handler(args) {  
  
            content.textContent = "eenie";  
            increment();  
            update();  
        }  
  
    })();  
  
    ```  
  
8.  Pressione a tecla F5 para iniciar a depuração. Verifique se o botão **Aguardando valores** aparece na página.  
  
9. Escolha **Aguardando valores** e verifique se o texto e a cor do botão são atualizados aproximadamente a cada segundo. Esse comportamento é esperado.  
  
10. Volte para o Visual Studio (Alt+Tab) e pressione Shift+F5 para parar a depuração.  
  
     Agora que você verificou que o aplicativo funciona, pode examinar seu desempenho usando o criador de perfil.  
  
### <a name="analyzing-performance-data"></a>Analisando dados de desempenho  
  
1. Na barra de ferramentas **Depurar**, na lista **Iniciar Depuração**, escolha um dos Emuladores ou **Simulador** do Windows Phone.  
  
2. No menu **Depurar** escolha **Desempenho e Diagnóstico**.  
  
3. Em **Ferramentas Disponíveis**, escolha **Capacidade de Resposta de interface do usuário em HTML** e escolha **Iniciar**.  
  
    Neste tutorial, você anexará o criador de perfil ao projeto de inicialização. Para obter informações sobre outras opções, como, por exemplo, anexar o criador de perfil a um aplicativo instalado, consulte [Capacidade de Resposta de interface do usuário em HTML](../profiling/html-ui-responsiveness.md).  
  
    Ao iniciar o criador de perfil, você poderá ver o Controle de Conta de Usuário solicitando sua permissão para executar o arquivo VsEtwCollector.exe. Escolha **Sim**.  
  
4. No aplicativo em execução, escolha **Aguardando valores** e espere cerca de 10 segundos. Verifique se o texto e a cor do botão são atualizados aproximadamente a cada segundo.  
  
5. No aplicativo em execução, alterne para o Visual Studio (Alt+Tab).  
  
6. Escolha **Parar de coletar**.  
  
    O criador de perfil exibe informações em um nova guia no Visual Studio. Ao examinar os dados de utilização da CPU e produtividade visual (FPS), é possível identificar facilmente algumas tendências:  
  
   - A utilização da CPU aumenta expressivamente após cerca de 3 segundos (quando você pressionou o botão **Aguardando valores**) e mostra um padrão claro de eventos (uma mistura consistente de eventos de scripts, estilos e renderização) desse ponto em diante.  
  
   - A produtividade visual não é afetada, e o FPS permanece em 60 o tempo todo (ou seja, não há quadros removidos).  
  
     Vamos examinar uma seção típica do gráfico de utilização da CPU para descobrir o que o aplicativo está fazendo nesse período de alta atividade.  
  
7. Selecione uma parte de um a dois segundos no meio do gráfico de utilização da CPU (ou clique e arraste, ou use as teclas Tab e de direção). A ilustração a seguir mostra o gráfico de utilização da CPU depois de ser feita uma seleção. A área não sombreada é a seleção.  
  
    ![Gráfico de utilização de CPU](../profiling/media/js-htmlviz-app-cpu.png "JS_HTMLViz_App_CPU")  
  
8. Escolha **Ampliar**.  
  
    O gráfico muda para mostrar mais detalhadamente o período selecionado. A ilustração a seguir mostra o gráfico de utilização da CPU após a ampliação. (Os dados específicos podem variar, mas o padrão geral será aparente.)  
  
    ![Exibição ampliada](../profiling/media/js-htmlviz-app-zoom.png "JS_HTMLViz_App_Zoom")  
  
    Os Detalhes da linha do tempo no painel inferior mostram um exemplo de detalhes para o período selecionado.  
  
    ![Detalhes da linha do tempo](../profiling/media/js-htmlviz-app-details.png "JS_HTMLViz_App_Details")  
  
    Os eventos nos Detalhes de linha do tempo confirmam tendências visíveis no gráfico de utilização da CPU: há muitos eventos ocorrendo em curtos períodos de tempo. A exibição dos Detalhes de linha do tempo mostra que esses eventos são `Timer`, `Layout` e `Paint`.  
  
9. Use o menu de contexto (ou clique com o botão direito do mouse) em um dos eventos `Timer` no painel inferior e escolha **Filtrar para evento**. A ilustração a seguir mostra um exemplo dos detalhes típicos para um dos eventos `Timer` nesse aplicativo de teste.  
  
     ![Evento de timer](../profiling/media/js-htmlviz-app-timer.png "JS_HTMLViz_App_Timer")  
  
     Diversos fatos podem ser obtidos nos dados. Por exemplo:  
  
    -   Cada evento `Timer`, codificado por cor para identificar um evento de script, inclui uma chamada para `document.createElement`, seguida por um cálculo de estilo e uma chamada para `style.backgroundColor` e `appendChild()`.  
  
    -   No curto período de tempo selecionado (cerca de um a dois segundos), há um grande número de eventos `Timer`, `Layout` e `Paint` ocorrendo. Os eventos `Timer` ocorrem com muito mais frequência do que uma atualização por segundo, o que é visível depois que você executa o aplicativo e escolhe o botão **Aguardando valores**.  
  
10. Para investigar, escolha o link da função anônima para um dos eventos `Timer` no painel inferior esquerdo. A seguinte função é aberta em default.js:  
  
    ```javascript  
    function update() {  
  
        setTimeout(function () {  
  
            setValues();  
            if (count < max) { update(); }  
        });  
    }  
    ```  
  
     Essa função recursiva configura um loop que chama a função `setValues()`, que atualiza o botão na interface do usuário. Por examinar os diferentes eventos de temporizador no criador de perfil, você descobre que a maioria ou todos os eventos de temporizador resultam nesse código, que é executado com muita frequência, parecendo que o problema se origina ali.  
  
### <a name="fixing-the-performance-issue"></a>Corrigindo o problema de desempenho  
  
1.  Substitua a função `update()` pelo seguinte código:  
  
    ```javascript  
    function update() {  
  
        setTimeout(function () {  
  
            setValues();  
            if (count < max) { update(); }  
        }, 1000 );  
    }  
    ```  
  
     Essa versão fixa do código inclui um atraso de 1000 milissegundos, que é omitido da versão anterior do código, resultando no uso de um valor de atraso padrão. Pelos dados do criador de perfis, parece que o valor padrão é zero milissegundos, o que faz com que a função `setValues()` seja executada com muita frequência.  
  
2.  Execute o criador de perfil de capacidade de resposta de IU em HTML novamente e verifique o gráfico de utilização da CPU. Você descobrirá que os eventos excessivos acabaram, e a utilização da CPU caiu para perto de zero. Corrigido!  
  
## <a name="see-also"></a>Consulte também  
 [Capacidade de Resposta de interface do usuário em HTML](../profiling/html-ui-responsiveness.md)



