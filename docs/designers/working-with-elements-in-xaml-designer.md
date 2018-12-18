---
title: Trabalhando com elementos no Designer XAML
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: a29690bf-f212-4ac6-a77a-adc53d14102e
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 47f6a975488adacbeffbdf0f04771131cd9a0ff9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49926937"
---
# <a name="working-with-elements-in-xaml-designer"></a>Trabalhando com elementos no Designer XAML
Você pode adicionar elementos - controles, layouts e formas - ao seu aplicativo no XAML, no código ou usando o XAML Designer. Este tópico descreve como trabalhar com elementos no Designer XAML no Visual Studio ou Blend for Visual Studio.

## <a name="adding-an-element-to-a-layout"></a>Adicionando um elemento a um layout
 *Layout* é o processo de redimensionar e posicionar elementos em uma interface do usuário. Para posicionar elementos visuais, você deve colocá-los em um layout [Panel](/uwp/api/Windows.UI.Xaml.Controls.Panel). Um `Panel` tem uma propriedade filho, que é uma coleção de tipos [FrameworkElement](/uwp/api/Windows.UI.Xaml.FrameworkElement). Você pode usar vários elementos filho `Panel`, como [Canvas](/uwp/api/Windows.UI.Xaml.Controls.Canvas), [StackPanel](/uwp/api/Windows.UI.Xaml.Controls.StackPanel) e [Grid](/uwp/api/Windows.UI.Xaml.Controls.Grid), para servir como contêineres de layout e posicionar e organizar os elementos em uma página.

 Por padrão, um painel `Grid` é usado como o contêiner de layout de nível superior em uma página ou formulário. Você pode adicionar painéis de layout, controles ou outros elementos dentro do layout de página de nível superior.

#### <a name="to-add-an-element-to-a-layout"></a>Para adicionar um elemento a um layout

-   No Designer XAML, siga um destes procedimentos:

    -   Clique duas vezes em um elemento na **Caixa de Ferramentas** (ou selecione um elemento na Caixa de Ferramentas e pressione **Enter**).

    -   Arraste um elemento da **Caixa de Ferramentas** para a prancheta.

    -   Na **Caixa de Ferramentas**, selecione uma das ferramentas de desenho (por exemplo, [Elipse](/uwp/api/Windows.UI.Xaml.Shapes.Ellipse) ou [Retângulo](/uwp/api/Windows.UI.Xaml.Shapes.Rectangle)) e desenhe um elemento no painel ativo.

## <a name="changing-the-layering-order-of-elements"></a>Alterando a ordem das camadas de elementos
 Quando houver dois elementos na prancheta do XAML Designer, um dos elementos será exibido na frente do outro na ordem de camadas. No final da lista de elementos, na janela Estrutura de Tópicos do Documento se encontra o elemento mais à frente (exceto quando a propriedade **ZIndex** de um elemento está definida). Quando você inserir um elemento em uma página, formulário ou contêiner de layout, o elemento será automaticamente colocado na frente de outros elementos no elemento de contêiner ativo. Para alterar a ordem dos elementos, você pode usar os comandos **Ordem** ou arrastar os elementos na árvore de objetos na janela Estrutura de Tópicos de Documento.

#### <a name="to-change-the-layering-order"></a>Para alterar a ordem das camadas

- Realize um dos seguintes procedimentos:

  - Na janela **Estrutura de Tópicos de Documento**, arraste os elementos para cima ou para baixo para criar a ordem das camadas desejada.

  - Na janela Estrutura de Tópicos de Documento ou na prancheta, clique com o botão direito do mouse no elemento cuja ordem de camadas você deseja alterar, selecione **Ordem** e clique em uma destas opções:

    -   **Trazer para a Frente** para colocar o elemento na parte da frente da ordem.

    -   **Avançar** para avançar o elemento um nível na ordem.

    -   **Recuar** para recuar o elemento um nível na ordem.

    -   **Enviar para Trás** para enviar o elemento para a parte posterior da ordem.

    Altere a propriedade **ZIndex** na seção **Layout** na janela Propriedades. Para sobrepor elementos, a propriedade **ZIndex** tem precedência sobre a ordem de elementos mostrada na janela Estrutura de Tópicos de Documento. Um elemento com um valor **ZIndex** superior será exibido na frente quando houver sobreposição de elementos.

## <a name="changing-the-alignment-of-an-element"></a>Alterando o alinhamento de um elemento
 Você pode alinhar elementos na prancheta usando comandos de menu ou arrastando os elementos para guias de alinhamento.

 Uma *guia de alinhamento* é uma indicação visual que ajuda você a alinhar um elemento em relação a outros elementos no aplicativo.

#### <a name="to-align-two-or-more-elements-by-using-menu-commands"></a>Para alinhar dois ou mais elementos usando comandos de menu

1.  Selecione os elementos que deseja alinhar. Selecione mais de um elemento mantendo a tecla **Ctrl** pressionada enquanto seleciona os elementos.

2.  Selecione uma das seguintes propriedades em **HorizontalAlignment** na seção **Layout** da janela Propriedades: **Esquerda**, **Centralizar**, **Direita** ou **Alongar**.

3.  Selecione uma das seguintes propriedades em **VerticalAlignment** na seção **Layout** da janela Propriedades: **Superior**, **Centralizar**, **Inferior** ou **Alongar**.

#### <a name="to-align-two-or-more-elements-by-using-snaplines"></a>Para alinhar dois ou mais elementos usando guias de alinhamento

-   No XAML Designer, em um layout que contenha, pelo menos, dois elementos, arraste ou redimensione um dos elementos de forma que a borda seja alinhada a outro elemento.

     Quando as bordas estão alinhadas, um *limite de alinhamento* é exibido para indicar o alinhamento. O limite de alinhamento é exibido como uma linha vermelha tracejada. Os limites de alinhamento só são exibidos quando a opção de **ajuste a guias de alinhamento** está habilitada. Para ver uma ilustração da prancheta que mostra um limite de alinhamento, consulte [Criando uma interface do usuário usando o Designer XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md).

## <a name="changing-an-elements-margins"></a>Alterar as margens de um elemento
 As margens no XAML Designer determinam o espaço vazio ao redor de um elemento na prancheta. Por exemplo, as margens especificam o espaço entre as bordas externas de um elemento e os limites de um painel `Grid` que contém o elemento. As margens também especificam o espaço entre os elementos que estão contidos em um `StackPanel`.

#### <a name="to-change-an-elements-margins-in-the-properties-window"></a>Para alterar as margens de um elemento na janela Propriedades

1.  Selecione o elemento cujas margens você deseja alterar.

2.  Em **Layout**, na janela Propriedades, altere o valor (em pixels ou em unidades independentes de dispositivos, de aproximadamente 1/96 polegada) de qualquer propriedade **Margem** (**Superior**, **Esquerda**, **Direita** ou **Inferior**).

#### <a name="to-change-an-elements-margins-in-the-artboard"></a>Para alterar as margens de um elemento na prancheta

-   Para alterar as margens de um elemento relativo ao respectivo contêiner de layout, clique nos *adornos de margem* exibidos ao redor do elemento na prancheta quando o elemento for selecionado e estiver em um contêiner de layout. Para obter uma ilustração que mostra adornos de margem, consulte [Criando uma interface do usuário usando o Designer XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md).

     Se um adorno de margem estiver aberto, vertical ou horizontalmente, essa margem não estará definida. Se um adorno de margem está fechado, essa margem está definida.

     Quando você abre um adorno de margem, e a margem oposta não está definida, a margem oposta é definida como o valor correto de acordo com o local do elemento na prancheta. Para margens opostas, como as margens **Esquerda** e **Direita**, pelo menos uma propriedade sempre será definida.

    > [!IMPORTANT]
    >  Elementos colocados dentro de alguns contêineres de layout, como <xref:Windows.UI.Xaml.Controls.Canvas>, não têm adornos de margem. Elementos colocados dentro de um <xref:Windows.UI.Xaml.Controls.StackPanel> têm adornos para as margens esquerda e direita ou para as margens superior e inferior, dependendo da orientação do `StackPanel`.

## <a name="grouping-and-ungrouping-elements"></a>Agrupando e desagrupando elementos
 O agrupamento de dois ou mais elementos no XAML Designer cria um novo contêiner de layout e coloca esses elementos dentro do contêiner. A colocação de dois ou mais elementos juntos em um contêiner de layout permite que você selecione, mova e transforme facilmente o grupo como se os elementos nesse grupo fossem um único elemento. O agrupamento também é útil para identificar elementos relacionados entre si de alguma forma, como os botões que compõem um elemento de navegação. Ao desagrupar elementos, você simplesmente exclui o contêiner de layout que continha os elementos.

#### <a name="to-group-elements-into-a-new-layout-container"></a>Para agrupar elementos em um novo contêiner de layout

1.  Selecione os elementos que você deseja agrupar. (Para selecionar vários elementos, pressione e segure a tecla **Ctrl** pressionada enquanto clica neles.)

2.  Clique com o botão direito do mouse nos elementos selecionados, aponte para **Agrupar em** e clique no tipo de contêiner de layout no qual deseja que o grupo resida.

    > [!TIP]
    >  Se você selecionar <xref:Windows.UI.Xaml.Controls.Viewbox>, <xref:Windows.UI.Xaml.Controls.Border> ou <xref:Windows.UI.Xaml.Controls.ScrollViewer> para agrupar os elementos, os elementos serão colocados em um novo painel de <xref:Windows.UI.Xaml.Controls.Grid> dentro de <xref:Windows.UI.Xaml.Controls.Viewbox>, <xref:Windows.UI.Xaml.Controls.Border> ou <xref:Windows.UI.Xaml.Controls.ScrollViewer>. Se você desagrupar elementos em um desses contêineres de layout, apenas <xref:Windows.UI.Xaml.Controls.Viewbox>, <xref:Windows.UI.Xaml.Controls.Border> ou <xref:Windows.UI.Xaml.Controls.ScrollViewer> será excluído, e o painel <xref:Windows.UI.Xaml.Controls.Grid> permanecerá. Para excluir o painel `Grid`, desagrupe os elementos novamente.

#### <a name="to-ungroup-elements-and-delete-the-layout"></a>Para desagrupar elementos e excluir o layout

- Clique com o botão direito do mouse no grupo que você deseja desagrupar e clique em **Desagrupar**.

  Você também pode agrupar ou desagrupar elementos clicando com o botão direito do mouse em itens selecionados na janela Estrutura de Tópicos de Documento e clicando em **Agrupar em** ou **Desagrupar**.

## <a name="resetting-the-element-layout"></a>Redefinindo o layout do elemento
 Você pode restaurar valores padrão de propriedades de layout específicas de um elemento usando o comando Redefinir Layout. Ao usar esse comando, você pode redefinir a margem, o alinhamento, a largura, a altura e o tamanho de um elemento, individual ou coletivamente.

#### <a name="to-reset-the-element-layout"></a>Para redefinir o layout do elemento

-   Na janela Estrutura de Tópicos do Documento ou na prancheta, clique com o botão direito do mouse no elemento, escolha **Layout** > **Redefinir** *NomePropriedade*, em que *NomePropriedade* é a propriedade que você deseja redefinir (ou escolha **Layout** > **Redefinir Tudo** para redefinir todas as propriedades de layout do elemento).

## <a name="see-also"></a>Consulte também

- [Criando uma interface do usuário usando o Designer XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md)
