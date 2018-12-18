---
title: Exibir ouvintes de eventos DOM | Microsoft Docs
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
- DOM events, viewing [Windows Store apps]
- event listeners, viewing [Windows Store apps]
ms.assetid: d5b679e7-87dd-4cec-9176-883db6ff0781
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: f1e0cf0abc35c87de3c7caa3ed00e57cb07cf987
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51727374"
---
# <a name="view-dom-event-listeners"></a>Exibir ouvintes de eventos DOM
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows e Windows Phone] (... /Image/windows_and_phone_content.png "windows_and_phone_content")  
  
 O **eventos** guia do Explorador do DOM mostra os eventos que estão associados um elemento DOM. Cada nó superior a **eventos** guia representa um evento que tem assinantes ativos. O nó superior contém subnós que representam os ouvintes registrados do evento específico. Além de exibir os ouvintes de eventos, você pode usar essa guia para navegar até o local do ouvinte de eventos no código JavaScript. As informações contidas neste tópico se aplicam a aplicativos da Windows Store que usam HTML e JavaScript.  
  
 Lista os **eventos** guia é dinâmica. Se você adicionar um ouvinte de evento enquanto o aplicativo está em execução, o novo ouvinte de evento será exibido lá. Para obter informações sobre adição ou remoção de ouvintes de eventos, consulte [dicas para resolver problemas com ouvintes de eventos](#Tips) neste tópico.  
  
> [!NOTE]
>  Ouvintes de eventos para elementos de código que não são elementos DOM, como `xhr`, não aparecem na **eventos** guia.  
  
## <a name="view-event-listeners-for-dom-elements"></a>Visualizar ouvintes de evento para elementos DOM  
 Este exemplo mostra um aplicativo da Windows Phone Store. O recurso Explorador do DOM descrito aqui também tem suporte para aplicativos da Windows Store.  
  
#### <a name="to-view-event-listeners"></a>Para exibir os ouvintes de eventos  
  
1.  No Visual Studio, crie um aplicativo em JavaScript que use o modelo de projeto do Aplicativo Dinâmico do Windows Phone.  
  
2.  Com o modelo aberto no Visual Studio, selecione **Emulator 8.1 WVGA 4 na 512MB** na lista suspensa na barra de ferramentas de depuração no depurador:  
  
     ![Selecionando um destino de depuração](../debugger/media/js-dom-debug-target-emu.png "JS_DOM_Debug_Target_Emu")  
  
3.  Pressione F5 para executar o aplicativo no modo de depuração.  
  
4.  No aplicativo em execução, vá para o **seção 3** item dinâmico.  
  
5.  Alterne para o Visual Studio (Alt+Tab ou F12).  
  
6.  No Explorador do DOM, escolha `Find` no canto superior direito.  
  
7.  Digite `ListView`e pressione Enter.  
  
8.  Se necessário, escolha o **próxima** botão para localizar o `DIV` elemento que representa o `ListView` controle (esse elemento tem um `data-win-control` valor de `WinJS.UI.ListView`).  
  
     Agora o elemento `DIV` deve ser selecionado no Explorador do DOM.  
  
9. Escolha o **eventos** guia no painel à direita do Explorador do DOM.  
  
     Agora você pode ver os eventos que têm assinantes ativos para o elemento `DIV`, conforme mostrado aqui.  
  
     ![Guia de eventos do Explorador do DOM](../debugger/media/js-dom-events.png "JS_DOM_Events")  
  
10. Para localizar os ouvintes desses eventos, escolha os links dos arquivos JavaScript associados.  
  
11. Para identificar rapidamente os ouvintes de eventos para elementos pai na hierarquia de DOM, escolha o elemento pai na lista de hierarquias na parte inferior do Explorador do DOM.  
  
     ![Selecionando elementos pai na hierarquia de DOM](../debugger/media/js-dom-breadcrumbs.png "JS_DOM_Breadcrumbs")  
  
     O **eventos** guia mostra os ouvintes de eventos para qualquer elemento que você escolher na lista de hierarquia.  
  
###  <a name="Tips"></a> Dicas para resolver problemas com ouvintes de eventos  
 Em alguns cenários de aplicativo, ouvintes de eventos devem ser removidos explicitamente usando [removeEventListener](http://msdn.microsoft.com/library/ie/ff975250\(v=vs.85\).aspx). Use o **eventos** guia no Explorador do DOM para testar se os ouvintes de evento foram removidos dos elementos DOM durante a execução de código. Aqui estão algumas dicas para ajudar a resolver esses tipos de problemas:  
  
-   Para aplicativos que usam o modelo de navegação de página única implementado no Visual Studio [modelos de projeto](http://msdn.microsoft.com/library/windows/apps/hh758331.aspx), não é geralmente necessário remover os ouvintes de evento registrados para objetos, como elementos DOM, que fazem parte de uma página. Neste cenário, um elemento DOM e seus ouvintes de evento associados têm a mesma duração e podem ser coletados como lixo.  
  
-   Se a duração do elemento DOM ou objeto for diferente do ouvinte de evento associado, pode ser necessário chamar o método `removeEventListener`. Por exemplo, se você usar o evento `window.onresize`, pode ser necessário remover o ouvinte de evento se você navegar para fora da página em que manipula o evento.  
  
-   Se o `removeEventListener` falhar ao remover o ouvinte especificado, ele pode estar sendo chamado em uma instância do objeto diferente. Você pode usar o [método bind (Function)](~/E:/Repos/visualstudio-docs-pr/scripting-docs/javascript/reference/bind-method-function-javascript.md) método para resolver esse problema quando você adiciona o ouvinte.  
  
-   Para remover um ouvinte de evento que foi adicionado usando o [método bind (Function)](~/E:/Repos/visualstudio-docs-pr/scripting-docs/javascript/reference/bind-method-function-javascript.md) ou usando uma função anônima, armazene uma instância da função quando você adiciona o ouvinte. Aqui está uma maneira de usar este padrão com segurança:  
  
    ```javascript  
    // You could use the following code within the constructor function of an object, or  
    // in the ready function of a PageControl object (Store app).  
    this.storedHandler = this._handlerFunc.bind(this);  
    elem.addEventListener('mouseup', this.storedHandler);  
  
    // In this example, add the following code in the PageControl object's unload function.  
    elem.removeEventListener('mouseup', this.storedHandler);  
  
    ```  
  
     Se você usar o código a seguir em vez de armazenar uma referência à função associada, você não conseguirá remover explicitamente o ouvinte de evento:  
  
    ```javascript  
    // Avoid this pattern. No reference to the bound function is available.  
    elem.addEventListener('mouseup', this._handlerFunc.bind(this));  
    ```  
  
-   Você não pode remover um ouvinte de evento usando `removeEventListener` se ele foi adicionado com o atributo `obj.on<eventname>`, por exemplo, `window.onresize = handlerFunc`.  
  
-   Usar o analisador de memória JavaScript [memória JavaScript](../profiling/javascript-memory.md) em seu aplicativo. Os ouvintes de evento que devem ser explicitamente removidos podem aparecer como perda de memória.  
  
## <a name="see-also"></a>Consulte também  
 [Guia de início rápido: Depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md)   
 [Depurar estilos CSS usando o Explorador do DOM](../debugger/debug-css-styles-using-dom-explorer.md)   
 [Depurar o layout usando o Explorador do DOM](../debugger/debug-layout-using-dom-explorer.md)



