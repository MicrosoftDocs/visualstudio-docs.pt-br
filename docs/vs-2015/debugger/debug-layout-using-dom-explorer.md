---
title: Depurar o layout usando o Explorador do DOM | Microsoft Docs
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
- box model [Windows Store apps], viewing
- debugging layout [Windows Store apps]
- layout, debugging [Windows Store apps]
ms.assetid: ded6566d-fc29-49a7-8029-dee8e50fe733
caps.latest.revision: 36
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ba06e6a8ba95887c0cc6b6acfd14cef10ff03798
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787738"
---
# <a name="debug-layout-using-dom-explorer"></a>Depurar o layout com o Explorador do DOM
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows e Windows Phone] (... /Image/windows_and_phone_content.png "windows_and_phone_content")  
  
 O **Layout** guia do Explorador do DOM mostra o [modelo de caixa CSS](http://go.microsoft.com/fwlink/?LinkID=238778) para o elemento selecionado em um [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] app, aplicativo do Windows Phone Store ou um aplicativo criado usando ferramentas do Visual Studio para Apache Cordova. Você pode usar essa representação visual do modelo de caixa para identificar e modificar os valores relacionados a layout que afetam a aparência dos elementos.  
  
> [!TIP]
>  As alterações feitas na **Layout** guia não são permanentes. Você pode fazer mudanças permanentes no seu código-fonte e, em seguida, atualize seu aplicativo usando o **Windows atualizar aplicativo** botão (somente para aplicativos Windows Store e Windows Phone Store) na barra de ferramentas Depurar. Dessa maneira, você pode evitar reiniciar o depurador.  
  
 Para usar o Explorador do DOM para modificar os aspectos do layout que não são mostrados no modelo de caixa, consulte [guia de início rápido: depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md) e [estilos de CSS depurar usando o Explorador do DOM](../debugger/debug-css-styles-using-dom-explorer.md).  
  
## <a name="example-of-fixing-a-layout-issue"></a>Exemplo de correção de um problema de layout  
 Este exemplo mostra como selecionar um elemento de lista no modelo Hub/dinâmico, interpretar os valores do modelo de caixa que estão na **Layout** guia e, em seguida, alterar um dos valores de propriedade para corrigir um problema de layout.  
  
#### <a name="to-fix-the-layout-issue"></a>Para corrigir o problema de layout  
  
1.  No Visual Studio, crie um novo aplicativo Windows Store que use o modelo de projeto Hub/Dinâmico.  
  
2.  Na pasta shared pages\hub, abra hub.css.  
  
3.  Substitua o código de CSS a seguir:  
  
    ```css  
    .hubpage .hub .section4 .sub-image-row img {  
        height: 95px;  
        width: 130px;  
    }  
    ```  
  
     com este código CSS:  
  
    ```css  
    .hubpage .hub .section4 .sub-image-row img {  
        height: 95px;  
        width: 130px;  
        margin-left: 5em;  
    }  
    ```  
  
4.  Selecione o projeto Windowsphone ou o projeto appname no Gerenciador de soluções e, em seguida, escolha **definir como projeto de inicialização** no menu de atalho para o projeto.  
  
5.  Dependendo do seu projeto de inicialização, escolha **Emulator 8.1 WVGA 4 inch 512MB** ou **simulador** na lista suspensa na barra de ferramentas Depurar (**Máquina Local** é o padrão valor).  
  
     ![Selecionando um destino de depuração](../debugger/media/js-dom-debug-target-emu.png "JS_DOM_Debug_Target_Emu")  
  
6.  Pressione F5 para executar o aplicativo no modo de depuração.  
  
7.  Abra a Seção 4 rolando ou movendo.  
  
    > [!TIP]
    >  Posicione o Simulador ou o Emulador do Windows Phone bem ao lado da janela do Visual Studio, para que você possa ver imediatamente os resultados das seleções e mudanças feitas em estilos de CSS.  
  
     Quando a Seção 4 for carregada, você poderá ver que as imagens inferiores não aparecem corretamente. Cada imagem de item aparece cortada ao meio (com a metade esquerda ausente).  
  
8.  Alterne para o Visual Studio e escolha **selecionar elemento** no Explorador do DOM (ou pressione Ctrl + B). O modo de seleção muda, permitindo que você selecione um item clicando nele, e o aplicativo é colocado em primeiro plano. O modo é revertido após um único clique.  
  
    > [!TIP]
    >  Você também pode usar as teclas de seta ou outros métodos para selecionar os elementos HTML diretamente no Explorador do DOM. Para obter mais informações sobre como selecionar elementos, consulte [guia de início rápido: depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md).  
  
9. No Simulador ou Emulador do Windows Phone, selecione a metade cinza à direita de uma das imagens que estão cortadas ao meio. Aparecem realces ao redor do elemento selecionado, como mostrado aqui no Emulador do Windows Phone:  
  
     ![Selecionando um elemento DOM](../debugger/media/js-css-layout-select.png "JS_CSS_Layout_Select")  
  
    > [!TIP]
    >  O Simulador suporta focalizar os elementos para exibir realces da caixa ao redor dos elementos DOM antes de selecionar um. O Emulador do Windows Phone não tem suporte a isso.  
  
     Quando você seleciona um elemento DOM, o Explorador do DOM seleciona automaticamente o elemento IMG correspondente no Visual Studio. O elemento selecionado no Explorador de DOMs tem esta aparência:  
  
    ```html  
    <img src="ms-appx://guid/images/gray.png>   
    </img>  
    ```  
  
10. Clique o **Layout** guia. Esta guia mostra o modelo de caixa do elemento selecionado, como mostrado aqui no Emulador do Windows Phone.  
  
     ![Guia de layout do Explorador do DOM](../debugger/media/js-css-layout.png "JS_CSS_Layout")  
  
     Essa exibição fornece algumas informações úteis sobre o elemento:  
  
    -   As cores correspondem ao realce da caixa que aparece no Simulador ao focalizar os elementos. A cor azul representa o \<img > dimensões do elemento. A cor marrom-claro representa os valores de margem.  
  
    -   A margem esquerda (margin-left) é definida, o que sugere a causa do problema, pois corresponde ao sintoma (preto no lado esquerdo das imagens).  
  
    -   As caixas que mostram valores de 0 pixels (por exemplo, Borda e Preenchimento) sugerem que as propriedades de CSS correspondentes provavelmente não estão definidas.  
  
11. Para ver como a regra margin-left é aplicada, escolha o **computado** guia e procure a regra margin-left. Você pode ver que essa regra está definida com o valor 5em, mas o valor computado é 66,66 px ou 146,66 px, dependendo do dispositivo de destino.  
  
    > [!TIP]
    >  O **computado** guia mostra que a regra margin-left é definida `..hubpage .hub. section4 .sub-image-row img` seletor de CSS, encontrado no CSS. Neste aplicativo de demonstração, é aqui que você precisa fazer a correção.  
  
     Você também pode usar o **Layout** guia para testar as modificações de valores de layout.  
  
12. No **Layout** guia, escolha o **66,66** ou **146,66**, que aparece no **margem** caixa, no lado esquerdo da caixa.  
  
13. Tipo `0` e pressione Enter. (Você também pode usar as teclas de seta para cima e para baixo para alterar o valor.)  
  
14. Selecione os outros \<img > elementos no Explorador do DOM e altere os valores de sua margem esquerda como 0.  
  
15. Alterne para Simulador ou Emulador do Windows Phone. Os valores margin-left atualizados foram aplicados às imagens da Seção 4. Esses valores também são atualizados na **computado** guia sob a regra margin-left.  
  
## <a name="see-also"></a>Consulte também  
 [Guia de início rápido: Depurar HTML e CSS](../debugger/quickstart-debug-html-and-css.md)   
 [Depurar estilos CSS usando o Explorador do DOM](../debugger/debug-css-styles-using-dom-explorer.md)   
 [Exibir ouvintes de eventos DOM](../debugger/view-dom-event-listeners.md)



