---
title: Criando uma interface do usuário usando o Blend
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- Blend.Start.Dev12
ms.assetid: efd12263-cc2d-4081-a2bb-9a2cc17c442c
caps.latest.revision: 33
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f77fba9ed184d5def85aa7ca260b7c552dddbfd1
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53054535"
---
# <a name="creating-a-ui-by-using-blend-for-visual-studio"></a>Criando uma interface de usuário usando o Blend para Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Blend for Visual Studio ajuda a criar aplicativos da área de trabalho do Windows baseados em XAML, Web, [Windows Phone](http://msdn.microsoft.com/library/windowsphone/develop/jj683071.aspx) e da [Windows Store](http://msdn.microsoft.com/library/windows/apps/jj129478.aspx). Ele fornece a mesma experiência básica de design XAML que o Visual Studio e adiciona designers visuais para tarefas avançadas, como animações e comportamentos.

 Como o Blend for Visual Studio é incluído como parte do Visual Studio, não é necessário baixá-lo. No entanto, você precisa selecioná-lo no instalador do Visual Studio para que ele seja instalado no sistema.

 Se estiver conhecendo o Blend for Visual Studio agora, reserve algum tempo para se familiarizar com os recursos exclusivos do workspace. Este tópico apresenta um tour rápido.

> [!NOTE]
>  Para fazer um tour pelos recursos de design compartilhados, como a prancheta, a janela Estrutura de Tópicos do Documento e a janela Dispositivo, consulte [Criando uma interface do usuário usando o Designer XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md).

 **Neste tópico**:

-   [Tour pelo painel Ferramentas](#Tools)

-   [Tour pelo painel Ativos](#Assets)

-   [Tour pelo painel Objetos e Linha do Tempo](#Objects)

-   [Tour pelo painel Propriedades](#Properties)

##  <a name="Tools"></a> Tour pelo painel Ferramentas
 É possível usar o painel **Ferramentas** no Blend for Visual Studio para criar e modificar objetos no aplicativo. Você cria os objetos selecionando uma ferramenta e desenhando na prancheta com o mouse.

 ![Painel Ferramentas](../designers/media/blend5toolspanel.png "Blend5Toolspanel")

|||||
|-|-|-|-|
|![](../designers/media/b1-1.png "B1_1")|**Ferramentas Seleção** Selecione objetos e demarcadores.<br /><br /> Use a ferramenta **Seleção Direta** para selecionar objetos aninhados e segmentos de caminho.|![Texto explicativo A](../designers/media/b5-label-a.png "b5_label_A")|**Ferramentas gradiente e pincel**|
|![](../designers/media/b1-2.png "B1_2")|**Ferramentas de exibição** Ajuste a prancheta, como para zoom e movimento panorâmico.|![Texto explicativo B](../designers/media/b5-label-b.png "b5_label_B")|**Ferramentas de caminho**|
|![](../designers/media/b1-3.png "B1_3")|**Ferramentas pincel** Trabalhe com os atributos visuais de um objeto, como transformar um pincel, pintar um objeto ou selecionar os atributos de um objeto para aplicação em outro objeto.|![Texto explicativo C](../designers/media/b5-label-c.png "b5_label_C")|**Ferramentas Forma**|
|![](../designers/media/b1-4.png "B1_4")|**Ferramentas de objeto** Desenhe os objetos mais comuns na prancheta, como demarcadores, formas, painéis de layout, texto e controles.|![Texto explicativo D](../designers/media/b5-label-d.png "b5_label_D")|**Painéis de layout**|
|![](../designers/media/b1-5.png "B1_5")|**Ferramentas de ativos** Acesse o painel **Ativos** e mostre o ativo usado mais recentemente na biblioteca.|![Texto explicativo E](../designers/media/b5-label-e.png "b5_label_E")|**Controles de texto**|
|||![Texto explicativo F](../designers/media/b5-label-f.png "b5_label_F")|**Controles comuns**|

 Assista a um breve vídeo ![Configurar recursos instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [a barra de ferramentas](https://www.youtube.com/watch?v=VkdUJcvoo54&list=PLBDF977B2F1DAB358&index=4).

##  <a name="Assets"></a> Tour pelo painel Ativos
 É possível encontrar todos os controles no painel **Ativos**, semelhante à **Caixa de ferramentas** no Visual Studio. Além dos controles, você encontrará tudo o que pode adicionar à sua prancheta no painel **Ativos**, incluindo estilos, mídia, comportamentos e efeitos.

 ![Painel Ativos](../designers/media/blend5-assets-panel.png "Blend5_Assets_panel")

|||
|-|-|
|![](../designers/media/b1-1.png "B1_1")|**Caixa de pesquisa** Digite na caixa **Pesquisar** para filtrar a lista de ativos.|
|![](../designers/media/b1-2.png "B1_2")|**Modo de grade e Modo de lista** Mude entre as exibições **Modo de grade** e **Modo de lista** dos ativos.|
|![](../designers/media/b1-3.png "B1_3")|**Categorias de ativos** Clique em uma categoria ou subcategoria para exibir a lista de ativos nessa categoria.|
|![](../designers/media/b1-4.png "B1_4")|**Estilos** Mostre todos os estilos contidos no dicionário de recursos.|
|![](../designers/media/b1-5.png "B1_5")|**Descrição** Exiba uma descrição da categoria ou subcategoria de ativos selecionada.|

##  <a name="Objects"></a> Tour pelo painel Objetos e Linha do Tempo
 Use esse painel para organizar os objetos na prancheta e, se quiser, para animá-los.

 ![Painel Objetos e Linha do Tempo no modo de animação](../designers/media/b5-object-timeline-animation.png "b5_object_timeline_animation")

|||
|-|-|
|![](../designers/media/b1-1.png "B1_1")|**Exibição Objetos** Exiba uma árvore visual de um documento. É possível fazer uma busca detalhada em vários níveis de detalhamento. Você também pode adicionar camadas para organizar ainda mais os objetos na prancheta. Dessa forma, é possível bloqueá-los e ocultá-los como um grupo.|
|![](../designers/media/b1-2.png "B1_2")|**Indicador do modo de registro** Veja se você está registrando as alterações de propriedade em uma linha do tempo.|
|![](../designers/media/b1-3.png "B1_3")|**Seletor de storyboard** Exiba uma lista dos storyboards criados.|
|![](../designers/media/b1-4.png "B1_4")|**Fechar storyboard** Feche o storyboard atual.|
|![](../designers/media/b1-5.png "B1_5")|**Opções de storyboard** Crie, duplique, inverta, exclua, renomeie ou feche um storyboard.|
|![](../designers/media/b1-6.png "B1_6")|**Controles de reprodução** Navegue pela linha do tempo. Também é possível arrastar o playhead para navegar pela linha do tempo (ou *remover*).|
|![](../designers/media/b1-7.png "B1_7")|**Retornar escopo para** Defina o escopo da exibição Objetos de volta ao objeto raiz anterior ou ao escopo anterior. Você poderá fazer isso somente quando estiver modificando um estilo ou um modelo.|
|![](../designers/media/b1-8.png "B1_8")|**Registrar um quadro chave** Registre um instantâneo das propriedades do objeto selecionado no ponto no tempo atual.|
|![](../designers/media/b1-9.png "B1_9")|**Opções de ajuste** Defina o ajuste da linha do tempo, a resolução de ajuste e desligue o ajuste da linha do tempo.|
|![](../designers/media/97fa60b9-0caf-4387-9225-b57510d32209.png "97fa60b9-0caf-4387-9225-b57510d32209")|**Mostrar/ocultar**, **Bloquear/desbloquear** Mostre ou oculte opções de visibilidade e bloqueio para a exibição Objetos.|
|![](../designers/media/b1-11.png "B1_11")|**Posição do playhead na linha do tempo** Mostre o tempo atual em milissegundos. Você também pode inserir um valor de tempo diretamente nesse campo para saltar até um ponto no tempo específico. A precisão depende da resolução de ajuste definida nas **Opções de Ajuste**.|
|![](../designers/media/b1-12.png "B1_12")|**Playhead** Determine em qual ponto no tempo a animação está. É possível arrastar o playhead na linha do tempo para visualizar a animação.|
|![](../designers/media/b1-13.png "B1_13")|**Quadros chave definidos em linhas do tempo** Altere um valor da propriedade em um ponto no tempo específico.|
|![](../designers/media/d839d12c-07a1-4127-a830-4a8e7069f4fe.png "d839d12c-07a1-4127-a830-4a8e7069f4fe")|**Alterar a ordem dos objetos** Defina a ordem de exibição dos objetos. Clique neste botão para organizar os objetos na exibição de estrutura pela ordem Z (de frente para trás) ou pela ordem de marcação (a ordem na qual eles aparecem na exibição **XAML**).|
|![](../designers/media/b1-15.png "B1_15")|**Zoom da linha do tempo** Defina a resolução de zoom da linha do tempo. Aumentar o zoom permite editar uma animação com mais detalhes e diminuir o zoom mostra mais uma visão geral do que está acontecendo no decorrer de períodos de tempo mais longos. Se você aumentar o zoom, mas não conseguir definir um quadro chave na posição de tempo desejada, verifique se a resolução de ajuste está definida com um valor suficientemente alto.|
|![Texto explicativo 16](../designers/media/b5-label-16.png "b5_label_16")|**Área de composição da linha do tempo** Exiba a linha do tempo e mova quadros chave arrastando-os ou usando os menus de atalho.|

##  <a name="Properties"></a> Tour pelo painel Propriedades
 Use esse painel para exibir e modificar as propriedades de um objeto. Você também pode defini-las diretamente na prancheta. Nesse caso, as alterações na propriedade serão refletidas no painel **Propriedades**.

 ![Painel Propriedades](../designers/media/blend5-properties-panel.png "Blend5_properties_panel")

 **Categorias** Expanda e recolha categorias de propriedades. Clique em **Expandir** ![](../designers/media/6375953d-074c-421a-bbb3-6f5055b67b64.png "6375953d-074c-421a-bbb3-6f5055b67b64") e **Recolher** ![Recolher](../designers/media/b5-collapse-button.png "b5_collapse_button") para mostrar ou ocultar detalhes da categoria.


|                                                                                                         |                                                                                                                                                                                                                                  |
|---------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                 ![](../designers/media/b1-1.png "B1_1")                                 |                                                                              **Nome e Tipo** Exiba o ícone, o nome e o tipo do objeto selecionado.                                                                              |
|                                 ![](../designers/media/b1-2.png "B1_2")                                 |                                                                          **Organizar por** Organize as propriedades em ordem alfabética por nome, origem ou categoria.                                                                          |
|                                 ![](../designers/media/b1-3.png "B1_3")                                 |                                                        **Propriedades do pincel** Defina as propriedades visuais de pincéis, como pincel de Preenchimento, pincel de Traço e pincel de Primeiro Plano.                                                        |
|                                 ![](../designers/media/b1-4.png "B1_4")                                 |                                                                                    **Editor de cor** Use para cor sólida e pincéis de gradiente.                                                                                    |
|                                 ![](../designers/media/b1-5.png "B1_5")                                 |                                                                                                 **Seletor de cor** Selecione uma cor.                                                                                                 |
|                                 ![](../designers/media/b1-6.png "B1_6")                                 |                                                                              **Chips de cor** Exiba a cor inicial, a cor atual e a última cor                                                                               |
|                                 ![](../designers/media/b1-7.png "B1_7")                                 | **Conta-gotas** Use a cor de qualquer elemento na tela. O **Conta-gotas de cor** fica disponível quando o **Pincel de cor sólida** é selecionado. O **Conta-gotas de gradiente** fica disponível quando o **Pincel de gradiente** é selecionado. |
|                                 ![](../designers/media/b1-8.png "B1_8")                                 |                                                                        **Propriedades e Eventos** Defina as propriedades ou escolha os eventos de um elemento selecionado.                                                                         |
|                                 ![](../designers/media/b1-9.png "B1_9")                                 |                                                         **Caixa de pesquisa** Pesquise propriedades. Filtre as propriedades exibidas digitando na caixa **Pesquisar**.                                                          |
| ![](../designers/media/97fa60b9-0caf-4387-9225-b57510d32209.png "97fa60b9-0caf-4387-9225-b57510d32209") |                                **Guias do editor de pincel** Use-as para selecionar um editor de pincel. Você pode escolher **Sem pincel**, **Pincel de cor sólida**, **Pincel de gradiente**, **Pincel de bloco** ou **Recurso pincel**.                                |
|                                ![](../designers/media/b1-11.png "B1_11")                                |                                    **Recursos de cor** Aplique exatamente a mesma cor a propriedades diferentes. A guia **Recursos de Cor** inclui **Recursos Locais** e **Recursos do Sistema**.                                    |
|                                ![](../designers/media/b1-12.png "B1_12")                                |                                                 **Espaço de cores RGB** Modifique a cor ajustando os valores para os editores de número **R**, **G** ou **B** (vermelho, verde, azul).                                                  |
|                                ![](../designers/media/b1-13.png "B1_13")                                |                                                                        **Canal alfa** Modifique o valor Alfa usando o editor de número ao lado de **A**.                                                                        |
| ![](../designers/media/d839d12c-07a1-4127-a830-4a8e7069f4fe.png "d839d12c-07a1-4127-a830-4a8e7069f4fe") |                                       **Converter cor em recurso** Converta a cor selecionada em um recurso de cor. Os recursos de cor ficam disponíveis ao clicar na guia Recursos de cor.                                        |
|                                ![](../designers/media/b1-15.png "B1_15")                                |                                                                                 **Valor hexadecimal** Exibe o valor hexadecimal da cor exibida.                                                                                 |
|                     ![Texto explicativo 16](../designers/media/b5-label-16.png "b5_label_16")                     |                                                                                **Controle deslizante de gradiente** É exibido somente se um pincel de gradiente é selecionado.                                                                                 |
| ![](../designers/media/d50027a1-6824-4ad8-8b4e-558b0756dcf8.png "d50027a1-6824-4ad8-8b4e-558b0756dcf8") |                                                                     **Mostrar propriedades avançadas** Exiba categorias das propriedades menos usadas.                                                                      |

 Assista a um breve vídeo ![Configurar recursos instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [painel de propriedades](https://www.youtube.com/watch?v=HCqQfiobdag&list=PLBDF977B2F1DAB358&index=7).

## <a name="see-also"></a>Consulte também
 [Inserir controles e modificar seu comportamento](../designers/insert-controls-and-modify-their-behavior-in-xaml-designer.md) [animar objetos](../designers/animate-objects-in-xaml-designer.md) [desenhar formas e demarcadores](../designers/draw-shapes-and-paths.md) [projetar XAML no Visual Studio e no Blend para Visual Studio](../designers/designing-xaml-in-visual-studio.md)
