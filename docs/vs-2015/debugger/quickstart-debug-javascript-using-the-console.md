---
title: 'Início rápido: Depurar JavaScript usando o console | Microsoft Docs'
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
- VS.WebClient.JavaScriptConsole
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- JavaScript Console
- JavaScript debugging
- debugging, JavaScript
ms.assetid: ea7adb71-52b6-4a5a-9346-98ca94b06bd7
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 61f36594b4158c95621ec240fd7a883accd259a8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51802585"
---
# <a name="quickstart-debug-javascript-using-the-console"></a>Guia de início rápido: depurar o JavaScript usando o console
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows e Windows Phone] (... /Image/windows_and_phone_content.png "windows_and_phone_content")  
  
 Você pode usar a janela Console do JavaScript para interagir e depurar aplicativos da Windows Store criados com JavaScript. Esses recursos têm suporte para [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] aplicativos, Windows Phone Store de aplicativos e aplicativos criados usando ferramentas do Visual Studio para Apache Cordova. Para a referência de comandos do console, consulte [comandos do JavaScript Console](../debugger/javascript-console-commands.md).  
  
 A janela Console do JavaScript permite que você:  
  
- Envie objetos, valores e mensagens de seu aplicativo para a janela do console.  
  
- Exiba e modifique os valores das variáveis local e global no aplicativo em execução.  
  
- Exiba visualizadores de objetos.  
  
- Execute o código JavaScript, que é executado no contexto do script atual.  
  
- Exiba erros e exceções de JavaScript, além de exceções de DOM (Document Object Model) e do Windows Runtime .  
  
- Realizar outras tarefas, como limpar a tela. Ver [comandos do JavaScript Console](../debugger/javascript-console-commands.md) para a lista completa de comandos.  
  
  Neste tópico:  
  
- [Depurar usando a janela do Console do JavaScript](#InteractiveConsole)  
  
- [Modo de depuração e quebra interativo](#InteractiveDebuggingBreakMode)  
  
- [Modo de linha única e modo multilinha na janela do Console do JavaScript](#SinglelineMultilineMode)  
  
- [Alternar o contexto de execução do script](#Switching)  
  
> [!TIP]
>  Se a janela do Console do JavaScript estiver fechada, escolha **Debug**>**Windows** > **Console do JavaScript** para abri-la novamente. A janela só aparece durante uma sessão de depuração de script.  
  
 Usando a janela Console do JavaScript, você pode interagir com seu aplicativo sem parar e reiniciar o depurador. Para obter mais informações, consulte [atualizar um aplicativo (JavaScript)](../debugger/refresh-an-app-javascript.md). Para obter informações sobre outro recursos, como usando o Explorador do DOM e configuração de pontos de interrupção, de depuração de JavaScript, consulte [guia de início rápido: depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md) e [depuração de aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md).  
  
##  <a name="InteractiveConsole"></a> Depurar usando a janela do Console do JavaScript  
 As seguintes etapas criam um aplicativo `FlipView` e mostram como depurar interativamente um erro de codificação JavaScript.  
  
> [!CAUTION]
>  O aplicativo de exemplo é um aplicativo da Windows Store. No entanto, os recursos de console descritos aqui também se aplicam a aplicativos criados usando ferramentas do Visual Studio para Apache Cordova.  
  
#### <a name="to-debug-javascript-code-in-the-flipview-app"></a>Para depurar o código JavaScript no aplicativo FlipView  
  
1.  Crie uma nova solução no Visual Studio escolhendo **arquivo** > **novo projeto**.  
  
2.  Escolher **JavaScript** > **aplicativos da Store**, escolha **aplicativos Windows** ou **aplicativos do Windows Phone**e, em seguida, escolha  **Aplicativo em branco**.  
  
3.  Digite um nome para o projeto, como `FlipViewApp`e escolha **Okey** para criar o aplicativo.  
  
4.  No elemento BODY de default.html, substitua o código HTML existente por este código:  
  
    ```html  
    <div id="flipTemplate" data-win-control="WinJS.Binding.Template"  
             style="display:none">  
        <div class="fixedItem" >  
            <img src="#" data-win-bind="src: flipImg" />  
        </div>  
    </div>  
    <div id="fView" data-win-control="WinJS.UI.FlipView" data-win-options="{  
        itemDataSource: Data.items.dataSource, itemTemplate: flipTemplate }">  
    </div>  
    ```  
  
5.  Abra default.css e adicione o seguinte CSS para o seletor `#fView`:  
  
    ```css  
    #fView {  
        background-color:#0094ff;  
        height: 500px;  
        margin: 25px;  
    }  
    ```  
  
6.  Abra default.js e substitua o código pelo seguinte código JavaScript:  
  
    ```javascript  
    (function () {  
        "use strict";  
  
        var app = WinJS.Application;  
        var activation = Windows.ApplicationModel.Activation;  
  
        var myData = [];  
        for (var x = 0; x < 4; x++) {  
            myData[x] = { flipImg: "/images/logo.png" }  
        };  
  
        var pages = new WinJS.Binding.List(myData, { proxy: true });  
  
        app.onactivated = function (args) {  
            if (args.detail.kind === activation.ActivationKind.launch) {  
                if (args.detail.previousExecutionState !==  
                activation.ApplicationExecutionState.terminated) {  
                    // TODO: . . .  
                } else {  
                    // TODO: . . .  
                }  
                args.setPromise(WinJS.UI.processAll());  
  
                updateImages();  
            }  
        };  
  
        function updateImages() {  
  
            pages.push(0, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223195" });  
            pages.push(1, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223196" });  
            pages.push(2, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223197" });  
  
        };  
  
        app.oncheckpoint = function (args) {  
        };  
  
        app.start();  
  
        var publicMembers = {  
            items: pages  
        };  
  
        WinJS.Namespace.define("Data", publicMembers);  
  
    })();  
    ```  
  
7.  Se um destino de depuração não estiver selecionado, escolha **simulador** ou, para Windows Phone, **Emulator 8.1 WVGA 4 inch 512MB** na lista suspensa lista ao lado de **dispositivo** botão de **depurar** barra de ferramentas:  
  
     ![Lista de destino de depuração Select](../debugger/media/js-select-target.png "JS_Select_Target")  
  
8.  Pressione F5 para iniciar o depurador.  
  
     O aplicativo será executado, mas não haverá imagens. Erros APPHOST na janela Console do JavaScript indicam que não há imagens.  
  
9. Com o `FlipView` aplicativo em execução no simulador ou emulador de telefone, o tipo `Data.items` no prompt de entrada da janela do console (ao lado de ">>" símbolo) e pressione Enter.  
  
     Um visualizador para o objeto `items` aparece na janela do console. Isso indica que foi criada uma instância do objeto `items` e está disponível no contexto do script atual. Na janela do console, você pode clicar nos nós de um objeto para ver os valores de propriedade (ou usar as teclas de direção). Se você clicar na seta para baixo do objeto `items._data`, como mostra esta ilustração, verá que suas referências da origem das imagens estão incorretas, como esperado. As imagens padrão (logo.png) ainda estão presentes no objeto e há imagens ausentes intercaladas com as imagens esperadas.  
  
     ![Janela do Console do JavaScript](../debugger/media/js-console-window.png "JS_Console_Window")  
  
     Note também que há muito mais itens no objeto `items._data` do que o esperado.  
  
10. No prompt, digite `Data.items.push` e pressione Enter. A janela do console mostra um visualizador para a função `push`, que é implementada em um arquivo de projeto [!INCLUDE[winjs_long](../includes/winjs-long-md.md)]. Neste aplicativo, estamos usando `push` para adicionar os itens corretos. Com uma rápida investigação usando o IntelliSense, descobrimos que devemos usar `setAt` para substituir as imagens padrão.  
  
11. Para corrigir esse problema interativamente, sem interromper a sessão de depuração, abra default.js e selecione esse código da função `updateImages`:  
  
    ```javascript  
    pages.push(0, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223195" });  
    pages.push(1, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223196" });  
    pages.push(2, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223197" });  
    ```  
  
     Copie e cole esse código no aviso de entrada do console JavaScript.  
  
    > [!TIP]
    >  Quando você cola um código de várias linhas no prompt de entrada do Console do JavaScript, o prompt de entrada do console alterna automaticamente para o modo de várias linhas. Você pode pressionar Ctrl+Alt+M para ativar e desativar o modo de várias linhas. Para executar um script no modo de várias linhas, pressione Ctrl+Enter ou escolha o símbolo de seta no canto inferior direito da janela. Para obter mais informações, consulte [modo de linha única e modo multilinha na janela do Console do JavaScript](#SinglelineMultilineMode).  
  
12. Corrija as chamadas de função `push` no prompt, substituindo `pages.push` por `Data.items.setAt`. O código corrigido deve ter esta aparência:  
  
    ```javascript  
    Data.items.setAt(0, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223195" });  
    Data.items.setAt(1, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223196" });  
    Data.items.setAt(2, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223197" });  
    ```  
  
    > [!TIP]
    >  Se você quiser usar o objeto `pages` em vez de `Data.items`, será necessário definir um ponto de interrupção em seu código para manter o objeto `pages` no escopo.  
  
13. Escolha o símbolo de seta verde para executar o script.  
  
14. Pressione Ctrl + Alt + M para alternar o prompt de entrada do console para modo de linha única e, em seguida, escolha **limpar entrada** (o "X" vermelho) para excluir o código do prompt de entrada.  
  
15. Tipo `Data.items.length = 3` no prompt e pressione Enter. Isso remove os elementos extrínsecos aos dados.  
  
16. Verifique o Simulador ou o Emulador do Windows Phone novamente: você verá que as imagens corretas estão nas páginas corretas de `FlipView`.  
  
17. No Explorador de DOMs, você pode ver o elemento DIV atualizado e pode navegar na subárvore para localizar os elementos IMG esperados.  
  
18. Parar a depuração, escolhendo **Debug** > **parar depuração** ou pressionar Shift + F5 e, em seguida, corrija o código-fonte.  
  
     Para a página Default. HTML completa que contém código de exemplo corrigido, consulte [código de exemplo depurar HTML, CSS e JavaScript](../debugger/debug-html-css-and-javascript-sample-code.md).  
  
##  <a name="InteractiveDebuggingBreakMode"></a> Modo de depuração e quebra interativo  
 Você pode usar pontos de interrupção e fazer step-into do código enquanto está usando ferramentas de depuração JavaScript como a janela Console do JavaScript. Quando um programa que está sendo executado no depurador encontra um ponto de interrupção, o depurador suspende temporariamente a execução do programa. Quando a execução é suspensa, o programa alterna do modo de execução para o modo de interrupção. Você pode retomar a execução a qualquer momento.  
  
 Quando um programa está no modo de interrupção, você pode usar a janela Console do JavaScript para executar scripts e comandos válidos no contexto de execução do script atual. Neste procedimento, você usará a versão corrigida do aplicativo `FlipView` que você criou anteriormente para demonstrar o uso do modo de interrupção.  
  
#### <a name="to-set-a-breakpoint-and-debug-the-app"></a>Para definir um ponto de interrupção e depurar o aplicativo  
  
1.  No arquivo default. HTML da `FlipView` aplicativo que você criou anteriormente, abra o menu de atalho para o `updateImages()` de função e, em seguida, escolha **ponto de interrupção** > **Inserir ponto de interrupção**.  
  
2.  Escolha **computador Local** ou **Emulator 8.1 WVGA 4 inch 512MB** na lista suspensa lista ao lado de **iniciar depuração** botão o **depurar** barra de ferramentas.  
  
3.  Escolher **Debug** > **iniciar depuração**, ou pressione F5.  
  
     O aplicativo entra no modo de interrupção quando a execução atinge a função `updateImages()`, e a linha atual de execução do programa é realçada em amarelo.  
  
     ![Usando o modo de interrupção com o Console do JavaScript](../debugger/media/js-breakmode.png "JS_BreakMode")  
  
     Você pode alterar os valores das variáveis para afetar imediatamente o estado do programa sem finalizar a sessão de depuração atual.  
  
4.  Tipo `updateImages` no prompt e pressione Enter. Será exibido um visualizador para a função na janela do console.  
  
5.  Selecione a função na janela do console para mostrar a implementação da função.  
  
     A ilustração a seguir mostra a janela do console nesse ponto.  
  
     ![A janela do Console do JavaScript mostrando um visualizador](../debugger/media/js-console-function-visualizer.png "JS_Console_Function_Visualizer")  
  
6.  Copie uma linha da função da janela de saída para o prompt de entrada e altere o valor de índice para 3:  
  
    ```javascript  
    pages.setAt(3, { flipImg: "http://go.microsoft.com/fwlink/?LinkID=223197" });  
    ```  
  
7.  Pressione Enter para executar a linha de código.  
  
     Se quiser percorrer o código linha por linha, pressione F11, ou pressione F5 para continuar a execução do programa.  
  
8.  Pressione F5 para continuar a execução do programa. O aplicativo `FlipView` é exibido, e agora todas as quatro páginas mostram uma das imagens não padrão.  
  
     Para alternar de volta para o Visual Studio, pressione F12 ou Alt+Tab.  
  
##  <a name="SinglelineMultilineMode"></a> Modo de linha única e modo multilinha na janela do Console do JavaScript  
 O aviso de entrada na janela Console do JavaScript oferece suporte ao modo de linha única e ao modo de várias linhas. O procedimento de depuração interativa neste tópico fornece um exemplo de como usar os dois modos. Você pode pressionar Ctrl+Alt+M para alternar entre os modos.  
  
 O modo de linha única fornece um histórico de entrada. Você pode navegar por esse histórico usando as teclas de seta para cima e seta para baixo. O modo de linha única limpa o aviso de entrada quando você executa scripts. Para executar um script no modo de linha única, pressione Enter.  
  
 O modo de várias linhas não limpa o aviso de entrada quando você executa scripts. Quando você alternar para modo de linha única de modo de várias linhas, você pode limpar a linha de entrada pressionando **limpar entrada** (o "X" vermelho). Para executar um script no modo de várias linhas, pressione Ctrl+Enter ou escolha o símbolo de seta no canto inferior direito da janela.  
  
##  <a name="Switching"></a> Alternar o contexto de execução do script  
 A janela Console do JavaScript permite que você interaja com um único contexto de execução, que representa uma única instância da plataforma host da Web (WWAHost.exe) de cada vez. Em alguns cenários, seu aplicativo pode iniciar outra instância do host, por exemplo, quando você usa um `iframe`, um contrato compartilhado, um web worker ou um controle `WebView`. Se outra instância do host está em execução, você pode selecionar um contexto de execução diferente enquanto executa o aplicativo selecionando o contexto de execução no **destino** lista.  
  
 A ilustração a seguir mostra a lista de destino na janela Console do JavaScript.  
  
 ![Destino de seleção na janela do console JavaScript](../debugger/media/js-console-target.png "JS_Console_Target")  
  
 Você também pode alternar o contexto de execução usando o comando `cd`, mas você precisa saber o nome do outro contexto de execução e a referência que será usada deve estar no escopo. O **destino** lista fornece melhor acesso a outros contextos de execução.  
  
##  <a name="BrowserSupport"></a> Suporte de plataforma e navegador  
 A janela Console do JavaScript tem suporte nas seguintes plataformas:  
  
-   [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] e aplicativos da Windows Phone Store que usam JavaScript e HTML  
  
-   Internet Explorer 11 em execução no [!INCLUDE[win81](../includes/win81-md.md)]  
  
-   Internet Explorer 10 em execução no [!INCLUDE[win8](../includes/win8-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Depurar aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md)   
 [Comandos do Console do JavaScript](../debugger/javascript-console-commands.md)   
 [Atualizar um aplicativo (JavaScript)](../debugger/refresh-an-app-javascript.md)   
 [Atalhos de teclado](../debugger/keyboard-shortcuts-html-and-javascript.md)   
 [Depurar o código de exemplo HTML, CSS e JavaScript](../debugger/debug-html-css-and-javascript-sample-code.md)   
 [Guia de início rápido: Depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md)   
 [Depurar um controle WebView](../debugger/debug-a-webview-control.md)   
 [Acessibilidade e suporte ao produto](http://msdn.microsoft.com/library/tzbxw1af\(VS.120\).aspx)



