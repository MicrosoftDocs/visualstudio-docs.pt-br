---
title: Depurar estilos CSS usando o Explorador do DOM | Microsoft Docs
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
- CSS styles [Windows Store apps], debugging
- CSS rules [Windows Store apps], debugging
- CSS debugging [Windows Store apps]
- debugging, CSS rules [Windows Store apps]
- HTML debugging [Windows Store apps]
ms.assetid: 2dfef7c6-7db2-4550-b694-783b0e535cea
caps.latest.revision: 47
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1f5a2c8ef6792403628430cb9881b24e6e279f02
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51750146"
---
# <a name="debug-css-styles-using-dom-explorer"></a>Depurar estilos CSS com o Explorador do DOM
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows e Windows Phone] (... /Image/windows_and_phone_content.png "windows_and_phone_content")  
  
 Quando você estiver depurando aplicativos Windows Store, Windows Phone Store de aplicativos e aplicativos criados usando ferramentas do Visual Studio para Apache Cordova, você pode exibir e alterar regras de CSS para elementos DOM selecionados e seus elementos filho.  
  
 O **estilos** e **computado** guias no Explorador do DOM mostram as regras de CSS que se aplicam a um elemento selecionado. As regras são exibidas na ordem de sua especificidade de acordo com as regras de precedência de CSS. As regras na parte superior de um seletor ou estilo de uma guia (as regras mais específicas) são as últimas a serem aplicadas ao elemento selecionado, e as regras na parte inferior de um seletor ou estilo são as primeiras a serem aplicadas. Quando as regras são aplicadas, elas substituem as regras aplicadas anteriormente.  
  
 O **estilos**, **calculado**, e **alterações** guias fornecem exibições diferentes de informações de estilo.  
  
-   Use o **estilos** guia para exibir as regras organizadas por nome de seletor CSS, como `html, body`. Você também pode usar essa guia para habilitar ou desabilitar estilos específicos, editar valores manualmente e ver os resultados imediatos dessas alterações.  
  
-   Use o **computado** guia para exibir os valores calculados de um estilo. Por exemplo, se você definir um tamanho para 1em, o valor calculado pelo Internet Explorer poderá ser 16px. Os estilos nessa guia estão organizados por nome de estilo, como `height`. Você também pode usar essa guia para habilitar ou desabilitar estilos específicos, editar valores manualmente e ver os resultados imediatos dessas alterações.  
  
    > [!NOTE]
    >  No Visual Studio 2013 atualização 2, as informações fornecidas na **rastreamento** guia foi mesclada com o **calculado** guia e o **rastreamento** guia foi removida.  
  
-   Use o **alterações** tab (somente para aplicativos Windows Store e Windows Phone Store) para identificar e rastrear estilos CSS que você alterou durante uma sessão de depuração.  
  
> [!TIP]
>  As alterações feitas nos estilos na **estilos** e **computado** guias não são permanentes. Elas são perdidas quando você interrompe a depuração. Para alterar o código-fonte e recarregar páginas sem interromper e reiniciar o depurador, atualize seu aplicativo usando o ![botão de aplicativo do Windows de atualização](../debugger/media/js-refresh.png "JS_Refresh") botão (**Windows atualizar aplicativo** ) sobre o **depurar** barra de ferramentas (somente para aplicativos Windows Store e Windows Phone Store). Para obter mais informações, consulte [atualizar um aplicativo (JavaScript)](../debugger/refresh-an-app-javascript.md).  
  
## <a name="example-of-fixing-a-css-rule"></a>Exemplo de correção de uma regra de CSS  
 Este exemplo mostra como inspecionar regras de CSS e depurar um problema de estilo. Por exemplo, vamos supor que você mude a cor de uma fonte usada para exibir títulos de grupo no modelo de [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] Aplicativo de Separação.  
  
> [!NOTE]
>  Este exemplo mostra um aplicativo da Windows Store, mas todos os recursos do Explorador do DOM mostrados também se aplicam a um aplicativo do Windows Phone Store e, com exceção da guia de alterações, um aplicativo criado usando ferramentas do Visual Studio para Apache Cordova.  
  
#### <a name="to-view-and-change-css-rules"></a>Para exibir e alterar regras de CSS  
  
1.  No Visual Studio, crie um novo aplicativo [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] usando JavaScript e HTML no modelo de projeto de Aplicativo de Separação.  
  
2.  Na **Gerenciador de soluções**, abra Items. CSS. (Você pode encontrar o arquivo items.css na pasta de páginas.)  
  
3.  Substitua o código de CSS a seguir:  
  
    ```css  
    .itemspage .itemslist .item {  
        -ms-grid-columns: 1fr;  
        -ms-grid-rows: 1fr 90px;  
        display: -ms-grid;  
        height: 250px;  
        width: 250px;  
    }  
    ```  
  
     com isso:  
  
    ```css  
    .itemspage .itemslist .item {  
        -ms-grid-columns: 1fr;  
        -ms-grid-rows: 1fr 90px;  
        display: -ms-grid;  
        height: 250px;  
        width: 250px;  
        color: #ff6a00;  
    }  
    ```  
  
     Isso adiciona um estilo que especifica a cor #ff6a00 (laranja) para cada item na lista. O seletor de CSS, `.itemspage .itemslist .item`, indica um conjunto de nomes de classe para elementos DIV em items.html, que aparecem como elementos aninhados em DOM ativos. O elemento DIV `item` especifica os itens de lista.  
  
4.  Selecione **simulador** na lista suspensa a **Debug** barra de ferramentas (**Máquina Local** é o valor padrão).  
  
     ![Lista de destino de depuração Select](../debugger/media/js-select-target.png "JS_Select_Target")  
  
5.  Pressione F5 para executar o aplicativo no modo de depuração.  
  
     Quando o aplicativo termina de carregar, procure nos títulos dos itens da lista, como **título do grupo: 1**. A cor não foi alterada. Assim, a tentativa de aplicar uma cor laranja aos títulos não funcionou. Vamos entender o que deu errado e corrigir usando as guias CSS no Explorador de DOMs.  
  
    > [!TIP]
    >  Depois que o aplicativo aparecer no Simulador, posicione o Simulador ao lado da janela do Visual Studio para que seja possível ver imediatamente os resultados das seleções e alterações feitas em estilos CSS.  
  
6.  Alterne para o Visual Studio e clique em **selecionar elemento** no Explorador do DOM (ou pressione Ctrl + B). O modo de seleção muda, permitindo que você selecione um item clicando nele, e o aplicativo é colocado em primeiro plano. O modo é revertido após um único clique. Aqui está o **selecionar elemento** botão. ![Selecione o botão de elemento no Explorador do DOM](../debugger/media/js-dom-select-element-button.png "JS_DOM_Select_Element_Button")  
  
    > [!TIP]
    >  Você também pode selecionar elementos HTML diretamente no Explorador de DOMs. Para obter mais informações sobre como selecionar elementos, consulte [guia de início rápido: depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md).  
  
7.  No simulador, focalize o título do primeiro item na lista, **título do grupo: 1**, no painel esquerdo da home page. O título é realçado, conforme mostrado aqui:  
  
     ![Usando o botão Selecionar elemento](../debugger/media/js-css-select-element.png "JS_CSS_Select_Element")  
  
    > [!NOTE]
    >  O Emulador do Windows Phone só permite destacar os elementos parcialmente ao focalizá-los.  
  
8.  Clique no título destacado. O Explorador de DOMs seleciona automaticamente o elemento HTML correspondente, que é semelhante a este:  
  
    ```html  
    <h4 class="item-title">Group Title: 1</h4>  
    ```  
  
     Quando você seleciona o elemento H4 no Explorador do DOM, as guias do Explorador do DOM mostram as regras associadas ao elemento H4. O **computado** guia é mostrada aqui, com o `color` propriedade aberta:  
  
     ![Guia de estilos de rastreamento no Explorador do DOM](../debugger/media/js-css-styles.png "JS_CSS_Styles")  
  
     Essa exibição fornece informações úteis sobre as regras que estão associadas ao estilo de `color`, como indicado a seguir:  
  
    -   O seletor de CSS que alteramos no items.css, `.itemspage .itemslist .item`, não está sendo usado no cálculo de estilo final (aparece como texto tachado). Várias outras ocorrências do estilo de `color` também não estão sendo usadas.  
  
        > [!TIP]
        >  No caso de nomes mais extensos do seletor, o nome completo aparece em uma dica de ferramenta.  
  
    -   O valor computado de CSS final, `rgba(255, 255, 255, 0.87)`, é definido especialmente para o seguinte seletor de CSS: `.itemspage .itemslist .item .item-overlay .item-title`, que também é definido em items.css.  
  
        > [!TIP]
        >  Agora que sabemos onde a cor do título está definida, também sabemos onde podemos alterá-la. No entanto, também podemos testar as alterações no Explorador do DOM sem atualizar o aplicativo, como mostrado nas etapas restantes.  
  
9. Desmarque a caixa de seleção da primeira ocorrência do estilo de `color`, que é para o seletor `.itemspage .itemslist .item .item-overlay .item-title`. Agora, no Simulador, você verá que a cor dos títulos dos itens mudará para laranja, como pretendíamos, e o seletor que modificamos no CSS, `.itemspage .itemslist .item`, não será mais substituído (isto é, não terá mais texto tachado aplicado). Aqui está o **computado** guia depois que desmarcamos a caixa de seleção.  
  
     ![A guia calculado depois de atualizar o estilo CSS](../debugger/media/js-css-styles-fixed.png "JS_CSS_Styles_Fixed")  
  
10. Selecione o **alterações** guia.  
  
     Use o **alterações** guia para identificar e rastrear alterações de estilo que você realizou durante uma sessão de depuração. A ilustração a seguir mostra a `.itemspage .itemslist .item .item-overlay .item-title` seletor em de **alterações** guia, que foi substituído.  
  
     ![Guia de alterações do Explorador do DOM](../debugger/media/js-css-styles-changes.png "JS_CSS_Styles_Changes")  
  
11. Você pode editar valores de estilo CSS também manualmente e ver o resultado imediato usando o **estilos** guia.  
  
12. Selecione o **estilos** guia.  
  
13. Abra o seletor de estilo de `.itemspage .itemslist .item .item-overlay .item-title`.  
  
14. Selecione a primeira ocorrência do estilo de `color` e clique duas vezes no valor de propriedade `rgb(255, 255, 255, 0.87)`.  
  
15. Use o teclado para modificar esse valor. Altere-o para `rgb(255, 255, 0, 0.87)` e pressione Enter. As cores dos títulos do item no Simulador mudam para amarelo.  
  
16. Para fazer alterações no arquivo CSS de origem, clique o **Items** no link a **estilos** guia. Isso abre o arquivo items.css, no qual é possível alterar o valor do estilo de `color` no código do aplicativo. Para atualizar o aplicativo sem interromper e reiniciar o depurador, clique o ![botão de aplicativo do Windows de atualização](../debugger/media/js-refresh.png "JS_Refresh") (**aplicativo atualizar Windows**) botão o **Depurar** barra de ferramentas.  
  
## <a name="see-also"></a>Consulte também  
 [Guia de início rápido: Depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md)   
 [Depurar o layout usando o Explorador do DOM](../debugger/debug-layout-using-dom-explorer.md)   
 [Exibir ouvintes de eventos DOM](../debugger/view-dom-event-listeners.md)   
 [Acessibilidade e suporte ao produto](http://go.microsoft.com/fwlink/?LinkId=253502)



