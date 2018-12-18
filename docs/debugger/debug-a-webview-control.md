---
title: Depurar um controle WebView (UWP) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 7d105907-8b39-4d07-8762-5c5ed74c7f21
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 4576cfa5724869aba86842c5debb4df685559879
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31465454"
---
# <a name="debug-a-webview-control-in-a-uwp-app"></a>Depurar um controle WebView em um aplicativo de UWP
  
 Para inspecionar e depurar os controles do `WebView` em um aplicativo do Tempo de Execução do Windows, você pode configurar o Visual Studio para anexar o Depurador de Scripts quando iniciar seu aplicativo. Você tem duas formas de interagir com `WebView` controla usando o depurador:  
  
-   Abra o [Explorador do DOM](../debugger/quickstart-debug-html-and-css.md) para um `WebView` de instância e inspecione os elementos de DOM, investigue os problemas de estilo CSS e teste dinamicamente as mudanças renderizadas nos estilos.  
  
-   Selecione a página da Web ou `iFrame` exibido no `WebView` instância como um destino no [Console do JavaScript](../debugger/javascript-console-commands.md) janela e, em seguida, interaja com a página da Web usando comandos do console. O console dá acesso ao contexto de execução do script atual.  
  
### <a name="attach-the-debugger-c-visual-basic-c"></a>Anexar o depurador (C#, Visual Basic, C++)  
  
1.  No Visual Studio, adicione um controle `WebView` ao seu aplicativo de Tempo de Execução do Windows.  
  
2.  No Solution Explorer, abra as propriedades do projeto, escolhendo **propriedades** no menu de atalho para o projeto.  
  
3.  Escolha **depurar**. No **processo do aplicativo** , escolha **Script**.  
  
     ![Anexar o depurador de script](../debugger/media/js_dom_webview_script_debugger.png "JS_DOM_WebView_Script_Debugger")  
  
4.  (Opcional) Para versões não expressas do Visual Studio, desabilite a depuração just-in-time (JIT) escolhendo **Ferramentas > Opções > Depuração > Just-In-Time**, e, em seguida, desabilite a depuração JIT para Script.  
  
    > [!NOTE]
    >  Desabilitando a depuração JIT, você pode ocultar caixas de diálogo para exceções não tratadas que ocorrem em algumas páginas da Web. No Visual Studio Express, a depuração JIT sempre fica desabilitada.  
  
5.  Pressione F5 para iniciar a depuração.  
  
### <a name="use-the-dom-explorer-to-inspect-and-debug-a-webview-control"></a>Use o Explorador do DOM para inspecionar e depurar um controle WebView  
  
1.  (C#, Visual Basic, C++) Anexe o depurador do script ao seu aplicativo. Veja a primeira seção para obter instruções.  
  
2.  Se ainda não o fez, adicione um controle `WebView` ao seu aplicativo e pressione F5 para iniciar a depuração.  
  
3.  Navegue até a página que contém os controles `Webview`.  
  
4.  Abra a janela Explorador do DOM para o `WebView` controle escolhendo **depurar**, **Windows**, **Explorador do DOM**e, em seguida, escolha a URL do `WebView` que você deseja inspecionar.  
  
     ![Abrir o Explorador do DOM](../debugger/media/js_dom_webview.png "JS_DOM_WebView")  
  
     O Explorador do DOM associado ao `WebView` aparece como uma nova guia no Visual Studio.  
  
5.  Exibir e modificar elementos de DOM ativos e estilos CSS, conforme descrito em [estilos de CSS depurar usando o Explorador do DOM](../debugger/debug-css-styles-using-dom-explorer.md).  
  
### <a name="use-the-javascript-console-window-to-inspect-and-debug-a-webview-control"></a>Usar a janela Console do JavaScript para inspecionar e depurar um controle WebView  
  
1.  (C#, Visual Basic, C++) Anexe o depurador do script ao seu aplicativo. Veja a primeira seção para obter instruções.  
  
2.  Se ainda não o fez, adicione um controle `WebView` ao seu aplicativo e pressione F5 para iniciar a depuração.  
  
3.  Abra a janela do Console do JavaScript para o `WebView` controle escolhendo **depurar**, **Windows**, **Console do JavaScript**.  
  
     A janela Console do JavaScript aparece.  
  
4.  Navegue até a página que contém os controles `Webview`.  
  
5.  Na janela do Console, selecione a página da Web ou um `iFrame` exibido pelo `WebView` controlar o **destino** lista.  
  
     ![Destino de seleção na janela do console JavaScript](../debugger/media/js_console_target.png "JS_Console_Target")  
  
    > [!NOTE]
    >  Usando o console, você pode interagir com um único `WebView`, `iFrame`, compartilhar o contrato ou web worker por vez. Cada elemento requer uma instância separada do host da plataforma web (WWAHost.exe). Você pode interagir com um host por vez.  
  
6.  Visualize e modifique variáveis em seu aplicativo ou usar comandos do console, conforme descrito em [início rápido: depurar JavaScript](../debugger/quickstart-debug-javascript-using-the-console.md) e [comandos do JavaScript Console](../debugger/javascript-console-commands.md).  
  
## <a name="see-also"></a>Consulte também  
 [Guia de início rápido: depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md)