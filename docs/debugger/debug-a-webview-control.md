---
title: Depurar um controle WebView (UWP) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 7d105907-8b39-4d07-8762-5c5ed74c7f21
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- uwp
ms.openlocfilehash: a96e4db66ec26870ac92c52209d7aa6f22225b21
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350635"
---
# <a name="debug-a-webview-control-in-a-uwp-app"></a>Depurar um controle WebView em um aplicativo UWP

 Para inspecionar e depurar os controles do `WebView` em um aplicativo do Windows Runtime, você pode configurar o Visual Studio para anexar o Depurador de Scripts quando iniciar seu aplicativo. Você tem duas maneiras de interagir com `WebView` controles usando o depurador:

- Abra o [Explorador do DOM](../debugger/quickstart-debug-html-and-css.md) para uma instância do `WebView` e inspecione os elementos de DOM, investigue os problemas de estilo de CSS e teste dinamicamente as mudanças renderizadas nos estilos.

- Selecione a página da Web ou o `iFrame` exibido na instância `WebView` como alvo na janela [Console do JavaScript](../debugger/javascript-console-commands.md?view=vs-2017), em seguida, interaja com a página da Web usando os comandos do console. O console dá acesso ao contexto de execução do script atual.

### <a name="attach-the-debugger-c-visual-basic-c"></a>Anexar o depurador (C#, Visual Basic, C++)

1. No Visual Studio, adicione um controle `WebView` ao seu aplicativo de Windows Runtime.

2. No Gerenciador de Soluções, abra as propriedades do projeto, escolhendo **Propriedades** do menu de atalho do projeto.

3. Escolha **Depurar**. Na lista **Processo do aplicativo**, escolha **Script**.

     ![Anexar o depurador de script](../debugger/media/js_dom_webview_script_debugger.png "JS_DOM_WebView_Script_Debugger")

4. (Opcional) No caso de versões não Expressas do Visual Studio, desabilite a depuração JIT (Just-In-Time) escolhendo **Ferramentas, Opções, Depuração, Just-In-Time**, em seguida, desabilite a depuração JIT para o Script.

    > [!NOTE]
    > Desabilitando a depuração JIT, você pode ocultar caixas de diálogo para exceções não tratadas que ocorrem em algumas páginas da Web. No Visual Studio Express, a depuração JIT sempre fica desabilitada.

5. Pressione F5 para iniciar a depuração.

### <a name="use-the-dom-explorer-to-inspect-and-debug-a-webview-control"></a>Use o Explorador do DOM para inspecionar e depurar um controle WebView

1. (C#, Visual Basic, C++) Anexe o depurador do script ao seu aplicativo. Veja a primeira seção para obter instruções.

2. Se ainda não o fez, adicione um controle `WebView` ao seu aplicativo e pressione F5 para iniciar a depuração.

3. Navegue até a página que contém os controles `Webview`.

4. Abra a janela do Explorador do DOM do controle `WebView` escolhendo **Depuração**, **Windows**, **Explorador do DOM** e escolha a URL do `WebView` que deseja inspecionar.

     ![Abrindo o explorador do DOM](../debugger/media/js_dom_webview.png "JS_DOM_WebView")

     O Explorador do DOM associado ao `WebView` aparece como uma nova guia no Visual Studio.

5. Exiba e modifique elementos DOM e estilos CSS em tempo real, conforme descrito em [depurar estilos CSS usando o explorador do dom](quickstart-debug-html-and-css.md).

### <a name="use-the-javascript-console-window-to-inspect-and-debug-a-webview-control"></a>Usar a janela Console do JavaScript para inspecionar e depurar um controle WebView

1. (C#, Visual Basic, C++) Anexe o depurador do script ao seu aplicativo. Veja a primeira seção para obter instruções.

2. Se ainda não o fez, adicione um controle `WebView` ao seu aplicativo e pressione F5 para iniciar a depuração.

3. Abra a janela Console do JavaScript para o controle `WebView` escolhendo **Depurar**, **Windows**, **Console do JavaScript**.

     A janela Console do JavaScript aparece.

4. Navegue até a página que contém os controles `Webview`.

5. Na janela Console, selecione a página da Web ou um `iFrame` exibido pelo controle `WebView` na lista **Destino**.

     ![Seleção de destino na janela do console do JavaScript](../debugger/media/js_console_target.png "JS_Console_Target")

    > [!NOTE]
    > Usando o console, você pode interagir com um único `WebView`, `iFrame`, compartilhar o contrato ou web worker por vez. Cada elemento requer uma instância separada do host da plataforma web (WWAHost.exe). Você pode interagir com um host por vez.

6. Exiba e modifique variáveis em seu aplicativo ou use comandos de console, conforme descrito em [início rápido: Depurar JavaScript](../debugger/quickstart-debug-javascript-using-the-console.md) e [comandos de console JavaScript](../debugger/javascript-console-commands.md?view=vs-2017).

## <a name="see-also"></a>Veja também

- [Guia de início rápido: depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md)