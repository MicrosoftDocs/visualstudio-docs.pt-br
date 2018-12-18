---
title: 'Passo a passo: Localizar uma perda de memória (JavaScript) | Microsoft Docs'
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
- memory leaks, JavaScript example
ms.assetid: f595412f-776b-49a2-8433-ea0062c6904d
caps.latest.revision: 36
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e2b84adac23547f42cca6113c5f5a7090f224e8c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51744946"
---
# <a name="walkthrough-find-a-memory-leak-javascript"></a>Instruções passo a passo: localizar uma perda de memória (JavaScript)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows e Windows Phone] (... /Image/windows_and_phone_content.png "windows_and_phone_content")  
  
 Este passo a passo o orienta pelo processo de identificar e corrigir um problema simples de memória usando o analisador de memória de JavaScript. O analisador de memória de JavaScript está disponível no Visual Studio para aplicativos da Windows Store criados para o Windows usando JavaScript. Neste cenário, você cria um aplicativo que retém incorretamente elementos DOM na memória, em vez de descartar os elementos na mesma proporção em que eles são criados.  
  
 Embora a causa da perda de memória deste aplicativo seja bastante específica, as etapas mostradas aqui indicam um fluxo de trabalho que geralmente funciona para isolar objetos com perda de memória.  
  
### <a name="running-the-javascript-memory-analyzer-test-app"></a>Executando o aplicativo de teste do analisador de memória de JavaScript  
  
1.  No Visual Studio, escolha **Arquivo**, **Novo** e **Projeto**.  
  
2.  Escolha **JavaScript** no painel esquerdo e escolha **Windows**, **Windows 8** e, em seguida, **aplicativos Universal** ou **Windows Phone**.  
  
    > [!IMPORTANT]
    >  Os resultados do uso de memória mostrados neste tópico são testados em relação a um aplicativo do Windows 8.  
  
3.  Escolha o modelo de projeto **Aplicativo em Branco** no painel central.  
  
4.  Na caixa **Nome**, especifique um nome como `JS_Mem_Tester` e escolha **OK**.  
  
5.  No **Gerenciador de Soluções**, abra default.html e cole o seguinte código entre as marcas \<body>:  
  
    ```html  
    <div class="wrapper">  
        <div id="item"></div>  
        <button class="memleak" style="display: block" >Leak Memory</button>  
    </div>  
    ```  
  
    > [!IMPORTANT]
    >  Se estiver usando um modelo de aplicativo universal do Windows 8.1, será necessário atualizar os códigos HTML e CSS nos projetos .Windows e .WindowsPhone.  
  
6.  Abra default.css e adicione o seguinte código CSS:  
  
    ```css  
    .memleak {  
        position: absolute; top: 100px; left: 100px;  
    }  
    ```  
  
7.  Abra default.js e substitua todo o código por este:  
  
    ```javascript  
    (function () {  
        "use strict";  
  
        var app = WinJS.Application;  
        var activation = Windows.ApplicationModel.Activation;  
  
        var wrapper;  
        var elem;  
  
        app.onactivated = function (args) {  
            if (args.detail.kind === activation.ActivationKind.launch) {  
                if (args.detail.previousExecutionState !== activation.ApplicationExecutionState.terminated) {  
                } else {  
                }  
                args.setPromise(WinJS.UI.processAll());  
  
                elem = document.getElementById("item");  
                wrapper = document.querySelector(".wrapper");  
                var btn = document.querySelector(".memleak");  
                btn.addEventListener("click", btnHandler);  
                run();  
            }  
        };  
  
        app.oncheckpoint = function (args) {  
        };  
  
        app.start();  
  
        function run() {  
            initialize();  
            load();  
        }  
  
        function initialize() {  
  
            if (wrapper != null) {  
                elem.removeNode(true);  
            }  
        }  
  
        function load() {  
  
            var newDiv = document.createElement("div");  
  
            newDiv.style.zIndex = "-1";  
            newDiv.id = "item";  
  
            wrapper.appendChild(newDiv);  
        }  
  
        function btnHandler(args) {  
            run();  
        }  
  
    })();  
    ```  
  
8.  Pressione a tecla F5 para iniciar a depuração. Verifique se o botão **Provocar perda de memória** aparece na página.  
  
9. Volte para o Visual Studio (Alt+Tab) e pressione Shift+F5 para parar a depuração.  
  
     Agora que verificamos que o aplicativo funciona, é possível examinar o uso de memória.  
  
### <a name="analyzing-the-memory-usage"></a>Analisando uso de memória  
  
1. Na barra de ferramentas **Depurar**, na lista **Iniciar Depuração**, escolha o destino de depuração para o projeto atualizado: um dos Emuladores ou **Simulator** do Windows Phone.  
  
   > [!TIP]
   >  Para um aplicativo da Windows Store, você também pode escolher **Computador Local** ou **Computador Remoto** nesta lista. Entretanto, a vantagem de usar o emulador ou o simulador é que você pode colocá-lo ao lado do Visual Studio e facilmente alternar entre o aplicativo em execução e o analisador de memória JavaScript. Para obter mais informações, consulte [Executar aplicativos do Visual Studio](../debugger/run-store-apps-from-visual-studio.md) e [Executar aplicativos da Windows Store em um computador remoto](../debugger/run-windows-store-apps-on-a-remote-machine.md).  
  
2. No menu **Depurar**, escolha **Criador de Perfil de Desempenho...**.  
  
3. Em **Ferramentas Disponíveis**, escolha **Memória JavaScript** e, em seguida, **Iniciar**.  
  
    Neste tutorial, você anexará o analisador de memória ao projeto de inicialização. Para obter informações sobre outras opções, por exemplo, como anexar o analisador de memória a um aplicativo instalado, consulte [Memória JavaScript](../profiling/javascript-memory.md).  
  
    Ao iniciar o analisador de memória, você poderá ver o Controle de Conta de Usuário solicitando sua permissão para executar o arquivo VsEtwCollector.exe. Escolha **Sim**.  
  
4. Escolha o botão **Provocar perda de memória** quatro vezes consecutivas.  
  
    Quando você escolhe o botão, o código de manipulação de eventos em default.js faz um trabalho que resultará em um vazamento de memória. Você usará isso para fins de diagnóstico.  
  
   > [!TIP]
   >  Repetir o cenário que você quer testar em termos de vazamento de memória facilita a filtragem de informações que não interessam, como objetos adicionados ao heap durante a inicialização do aplicativo ou ao carregar uma página.  
  
5. No aplicativo em execução, alterne para o Visual Studio (Alt+Tab).  
  
    O analisador de memória de JavaScript exibe informações em um nova guia no Visual Studio.  
  
    O gráfico de memória nessa exibição resumida mostra o uso de memória do processo ao longo do tempo. A exibição também fornece comandos como **Obter uma imagem instantânea do heap**. Um instantâneo fornece informações detalhadas sobre o uso de memória em um horário específico. Para obter mais informações, consulte [Memória JavaScript](../profiling/javascript-memory.md).  
  
6. Escolha **Obter uma imagem instantânea do heap**.  
  
7. Mude para o aplicativo e escolha **Perda de Memória**.  
  
8. Mude para o Visual Studio e escolha **Obter uma imagem instantânea do heap** novamente.  
  
    Esta ilustração mostra o instantâneo da linha de base (1) e o Instantâneo 2.  
  
    ![A linha de base do instantâneo e o instantâneo 2](../profiling/media/js-mem-app-snapshot2.png "JS_Mem_App_Snapshot2")  
  
   > [!NOTE]
   >  O Emulador do Windows Phone não mostra a captura de tela do aplicativo na hora em que o instantâneo é capturado.  
  
9. Mude para o aplicativo e escolha o botão **Provocar perda de memória** novamente.  
  
10. Mude para o Visual Studio e escolha **Obter uma imagem instantânea do heap** pela terceira vez.  
  
    > [!TIP]
    >  Ao colocar um terceiro instantâneo nesse fluxo de trabalho, você pode filtrar as alterações do instantâneo de linha de base para o segundo instantâneo que não estejam associadas a vazamentos de memória. Por exemplo, pode haver alterações previstas, como atualização de cabeçalhos e rodapés em uma página, que criarão algumas alterações no uso de memória, mas poderão não estar relacionadas a vazamentos.  
  
     Esta ilustração mostra o Instantâneo 2 e o Instantâneo 3.  
  
     ![Instantâneo 2 e instantâneo 3](../profiling/media/js-mem-app-snapshot3.png "JS_Mem_App_Snapshot3")  
  
11. No Visual Studio, escolha **Parar** para interromper a criação de perfil.  
  
12. No Visual Studio, compare os instantâneos. O instantâneo 2 mostra o seguinte:  
  
    - O tamanho do heap (mostrado pela seta para cima vermelha à esquerda) aumentou em vários KB em comparação com o Instantâneo 1.  
  
      > [!IMPORTANT]
      >  Os valores exatos de uso da memória para o tamanho do heap dependem do destino de depuração.  
  
    - O número de objetos no heap (mostrado pela seta para cima vermelha à direita) aumentou em comparação com o Instantâneo 1. Um objeto foi adicionado (+1) e nenhum objeto foi removido (-0).  
  
      O instantâneo 3 mostra o seguinte:  
  
    - O tamanho do heap aumentou novamente em centenas de bytes em comparação com o Instantâneo 2.  
  
    - O número de objetos no heap aumentou novamente em comparação com o Instantâneo 2. Um objeto foi adicionado (+1) e nenhum objeto foi removido (-0).  
  
13. No Instantâneo 3, escolha o texto do link à direita, que mostra um valor de +1 / -0 ao lado da seta vermelha para cima.  
  
     ![Link para uma exibição diferente de objetos de heap](../profiling/media/js-mem-app-link.png "JS_Mem_App_Link")  
  
     Isso abre uma exibição diferencial dos objetos no heap, denominada **Instantâneo 3 – Instantâneo 2**, com a exibição Tipos sendo mostrada por padrão. Por padrão, você verá uma lista de objetos adicionados ao heap entre Instantâneo 2 e Instantâneo 3.  
  
14. No filtro **Escopo**, escolha **Objetos restantes do Instantâneo 2**.  
  
15. Abra o objeto HTMLDivElement na parte superior da árvore de objetos como é mostrado aqui.  
  
     ![Exibição diferente da contagem de objetos no heap](../profiling/media/js-mem-app-typesdiff.png "JS_Mem_App_TypesDiff")  
  
     Essa exibição mostra informações úteis sobre o vazamento de memória, como as seguintes:  
  
    - Essa exibição mostra o elemento DIV com ID de `item`, o tamanho retido para o objeto é de várias centenas de bytes (o valor exato pode variar).  
  
    - Esse objeto é uma sobra do objeto de Instantâneo 2 e representa um vazamento de memória em potencial.  
  
      Algum conhecimento dos aplicativos ajuda neste ponto; a escolha do botão **Provocar perda de memória** deve remover um elemento DIV e adicionar um elemento, portanto o código não parece estar funcionando corretamente (ou seja, está vazando memória). A próxima seção explica como corrigir isso.  
  
    > [!TIP]
    >  Às vezes, localizar um objeto em relação ao objeto `Global` pode ajudar a identificar esse objeto. Para isso, abra o menu de atalho do identificador e escolha **Mostrar na exibição de raiz**.  
  
##  <a name="FixingMemory"></a> Corrigindo o problema de memória  
  
1. Usando os dados revelados pelo criador de perfis, você examina o código que é responsável por remover elementos DOM com ID de "item". Isso ocorre na função `initialize()`.  
  
   ```javascript  
   function initialize() {  
  
       if (wrapper != null) {  
           elem.removeNode(true);  
       }  
   }  
   ```  
  
    `elem.removeNode(true)` talvez não esteja funcionando corretamente. Você examina como o código está armazenando em cache o elemento DOM e encontra um problema; a referência ao elemento em cache não está sendo atualizada.  
  
2. Em default.js, adicione a seguinte linha de código à função de carregamento imediatamente antes de chamar `appendChild`:  
  
   ```javascript  
   elem = newDiv;  
   ```  
  
    Esse código atualiza a referência ao elemento armazenado em cache, para que seja removido corretamente quando você escolher o botão **Provocar perda de memória**. O código completo para a função de carregamento agora tem esta aparência:  
  
   ```javascript  
   function load() {  
  
       wrapper = document.querySelector(".wrapper");  
  
       var newDiv = document.createElement("div");  
  
       newDiv.style.zIndex = "-1";  
       newDiv.id = "item";  
       elem = newDiv;  
  
       wrapper.appendChild(newDiv);  
   }  
   ```  
  
3. No menu **Depurar** escolha **Desempenho e Diagnóstico**.  
  
4. Em **Ferramentas Disponíveis**, escolha **Memória JavaScript** e, em seguida, **Iniciar**.  
  
5. Siga o mesmo procedimento anterior para obter três instantâneos. As etapas são resumidas aqui:  
  
   1. No aplicativo, escolha o botão **Provocar perda de memória** quatro vezes consecutivas.  
  
   2. Mude para o Visual Studio e escolha **Obter uma imagem instantânea do heap** para o instantâneo da linha de base.  
  
   3. No aplicativo, escolha o botão **Provocar perda de memória**.  
  
   4. Mude para o Visual Studio e escolha **Obter uma imagem instantânea do heap** para o segundo instantâneo.  
  
   5. No aplicativo, escolha o botão **Provocar perda de memória**.  
  
   6. Mude para o Visual Studio e escolha **Obter uma imagem instantânea do heap** para o terceiro instantâneo.  
  
      O Instantâneo 3 agora mostra o tamanho do heap como **Sem aumento** do Instantâneo 2 e da contagem de objetos como +1/-1, o que indica que um objeto foi adicionado e outro removido. Esse é o comportamento desejado.  
  
      A ilustração a seguir mostra o Instantâneo 2 e o Instantâneo 3.  
  
      ![Instantâneos mostrando a perda de memória fixa](../profiling/media/js-mem-app-fixed-snapshot3.png "JS_Mem_App_Fixed_Snapshot3")  
  
## <a name="see-also"></a>Consulte também  
 [Memória JavaScript](../profiling/javascript-memory.md)



