---
title: Criando uma interface de usuário usando o Designer XAML
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
- VS.XamlDesigner
- VS.DevicePanel
- VS.XamlEditor
- VS.DocumentOutline
ms.assetid: c54969a7-d75a-4a35-9b37-af7a596a7c24
caps.latest.revision: 31
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 8928f725e144c980d3e625d557a71047959b8b9b
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53058815"
---
# <a name="creating-a-ui-by-using-xaml-designer-in-visual-studio"></a>Criando uma interface de usuário usando o XAML Designer no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Designer XAML no Visual Studio fornece uma interface visual para ajudá-lo a criar aplicativos da Windows Store, Windows Phone, WPF e Silverlight baseados em XAML. Você pode criar interfaces do usuário para seus aplicativos arrastando controles da **Caixa de Ferramentas** e configurando propriedades na janela **Propriedades**. Você também pode editar XAML diretamente no modo de exibição XAML.

 Para tarefas avançadas de design XAML como animações e comportamentos, consulte [Criando uma interface do usuário usando o Blend for Visual Studio](../designers/creating-a-ui-by-using-blend-for-visual-studio.md).

## <a name="xaml-designer-workspace"></a>Workspace do Designer XAML
 O workspace no Designer XAML consiste em vários elementos da interface visual. Esses elementos incluem a prancheta, o Editor XAML, a janela Dispositivo, a janela Estrutura de Tópicos de Documento e a janela Propriedades. Para abrir o Designer XAML, clique com o botão direito do mouse em um arquivo XAML no **Gerenciador de Soluções** e selecione **Exibir Designer**.

## <a name="authoring-views"></a>Criando modos de exibição
 O Designer XAML fornece um modo de exibição XAML e um modo Design sincronizado de marcação XAML renderizada de seu aplicativo. Com um arquivo XAML aberto no Visual Studio, você pode mudar o modo de exibição de Design e a exibição XAML usando as guias **Design** e **XAML**. Você pode usar o botão **Alternar Painéis** para mudar qual janela é exibida no topo: a prancheta ou o Editor XAML.

 No modo de exibição de Design, a janela que contém a *prancheta* é a janela ativa e você pode usá-la como superfície de trabalho primária. Você pode usá-la para criar visualmente uma página em seu aplicativo adicionando ou desenhando elementos e depois modificando-os. Para obter mais informações, consulte [Trabalhando com elementos no Designer XAML](../designers/working-with-elements-in-xaml-designer.md). Esta ilustração mostra o artboard no modo Design.

 ![Modo de Exibição de Design do Designer XAML](../designers/media/xaml-editor-design-view.png "xaml_editor_design_view")

 Estas funcionalidades estão disponíveis no artboard:

 **Guias de alinhamento** As guias de alinhamento são *limites de alinhamento* que são exibidos como linhas vermelhas tracejadas para mostrar quando as bordas dos controles estão alinhadas ou quando as linhas de base de texto estão alinhadas. Os limites de alinhamento só são exibidos quando a opção de **ajuste a guias de alinhamento** está habilitada.

 **Trilhos de grade** Trilhos `Grid` são usados para gerenciar linhas e colunas em um painel de [Grade](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.grid.aspx). Você pode criar e excluir linhas e colunas, bem como ajustar suas larguras e alturas relativas. O rail de Grade vertical, exibido à esquerda da planilha, é usado para linhas e a linha horizontal, exibida na parte superior, é usada para colunas.

 **Adornos de grade** Um adorno `Grid` é exibido como um triângulo que tem uma linha vertical ou horizontal anexada a ele no trilho `Grid`. Quando você arrasta um adorno `Grid`, as larguras ou alturas das linhas ou colunas adjacentes são atualizadas enquanto o mouse é movimentado.

 Os adornos `Grid` são usados para controlar a largura e altura das linhas e colunas de uma `Grid`. Você pode adicionar uma nova coluna ou linha clicando nos rails de `Grid`. Quando você adiciona uma nova linha ou linha de coluna a um painel `Grid` que possui duas ou mais colunas ou linhas, uma minibarra de ferramentas exibida fora do rail permite definir explicitamente a largura e a altura. A minibarra de ferramentas permite que você defina opções de dimensionamento para linhas e colunas de `Grid`.

 **Alças de redimensionamento** As alças de redimensionamento são exibidas em controles selecionados e permitem redimensionar o controle. Quando você redimensiona um controle, os valores de largura e altura geralmente são exibidos para ajudar a dimensionar o controle. Para obter mais informações sobre a manipulação de controles no modo de exibição de Design, consulte [Trabalhando com elementos no Designer XAML](../designers/working-with-elements-in-xaml-designer.md).

 **Margens** As margens representam o espaço fixo entre a borda de um controle e a borda do respectivo contêiner. Você pode definir as margens de um controle usando as propriedades [Margem](http://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.frameworkelement.margin.aspx) em **Layout** na janela Propriedades.

 **Adornos de margem** Você pode usar adornos de margem para alterar as margens de um elemento relativo ao respectivo contêiner de layout. Quando um adorno de margem está aberto, uma margem não está definida, e o adorno de margem exibe uma cadeia quebrada. Quando a margem não está definida, os elementos permanecem no lugar quando o contêiner de layout é redimensionado em tempo de execução. Quando um adorno de margem está fechado, um adorno de margem exibe uma cadeia ininterrupta, e os elementos são movidos com a margem enquanto o contêiner de layout é redimensionado em tempo de execução (a margem permanece fixa).

 **Alças do elemento** Você pode modificar um elemento usando as alças do elemento que são exibidas na planilha ao mover o ponteiro sobre os cantos da caixa azul que circunda um elemento. Essas alças permitem girar, redimensionar, inverter, mover ou adicionar um radiano do canto ao elemento. O símbolo da alça do elemento varia por função e altera dependendo do local exato do ponteiro. Se você não vir as alças do elemento, verifique se o elemento está selecionado.

 No modo Design, os comandos adicionais do artboard estão disponíveis na área esquerda inferior da tela, como mostrado aqui:

 ![Comandos do modo de exibição de Design](../designers/media/xaml-editor-design-controls.png "xaml_editor_design_controls")

 Estes comandos estão disponíveis na barra de ferramentas:

 **Zoom** O zoom permite dimensionar a superfície de design. Você pode aplicar zoom de 12,5% a 800% ou selecionar opções, como **Ajustar à Seleção** e **Ajustar a Tudo**.

 **Exibir/Ocultar grade de ajuste** Exibe ou oculta a grade de ajuste que mostra as linhas de grade. As linhas de grade são usadas quando a opção de **ajuste a linhas de grade** ou de **ajuste a guias de alinhamento** está habilitada.

 **Ativar/desativar ajuste às linhas de grade** Se a opção de **ajuste às linhas de grade** estiver habilitada quando você arrastar um elemento na prancheta, a tendência será o elemento alinhar-se às linhas de grade horizontais e verticais mais próximas.

 **Ativar/desativar ajuste às guias de alinhamento** As guias de alinhamento ajudam a alinhar os controles relativos uns aos outros. Se a opção de **ajuste às guias de alinhamento** estiver habilitada, quando você arrastar um controle relativo a outros controles, os limites de alinhamento serão exibidos quando as margens e o texto de alguns controles estiverem alinhados horizontal ou verticalmente. Um limite de alinhamento é exibido como uma linha vermelho-tracejada.

 No modo de exibição XAML, a janela que contém o editor XAML é a janela ativa, e o editor XAML é a ferramenta de criação primária. A linguagem XAML fornece um vocabulário declarativo, com base em XML, para especificar a interface do usuário de um aplicativo. O modo de exibição XAML inclui o IntelliSense, formatação automática, realce de sintaxe e navegação de marcação. Esta ilustração mostra o modo de exibição XAML:

 ![Exibição XAML](../designers/media/xaml-editor.png "xaml_editor")

 **Barra do modo divisão** A barra do modo divisão é exibida na parte superior do modo de exibição XAML quando o editor XAML está na janela inferior. A barra do modo divisão permite controlar os tamanhos relativos do modo Design e do modo de exibição XAML. Você também pode trocar os locais das exibições (usando o botão **Alternar Painéis**), especificar se as exibições são organizadas horizontal ou verticalmente e recolher a exibição.

 **Zoom de marcação** O zoom de marcação permite dimensionar o modo de exibição XAML. Você pode aplicar zoom de 20% a 400%.

## <a name="device-window"></a>Janela Dispositivo
 A janela Dispositivo no Designer XAML permite simular em tempo de design vários modos de exibição, vídeos e opções de exibição para seu projeto da Windows Store ou do Windows Phone. A janela Dispositivo está disponível no menu **Design** quando você estiver trabalhando no Designer XAML. Veja como ela se parece:

 ![Janela Dispositivo](../designers/media/xaml-editor-device-panel.png "xaml_editor_device_panel")

 Estas são as opções disponíveis na janela Dispositivo:

 **Exibição** Especifica diferentes resoluções e tamanhos de exibição para o aplicativo.

 **Orientação** Especifica diferentes orientações para o aplicativo: **Paisagem** ou **retrato**.

 **Borda** Especifica diferentes alinhamentos de borda para seu aplicativo: **Ambos**, **esquerda**, **direita**, ou **nenhum**.

 **Alto Contraste** Visualize o aplicativo com base na configuração de contraste selecionada. Essa configuração, quando definida como um valor diferente do valor **Padrão**, substituirá a propriedade `RequestedTheme` definida no arquivo App.xaml.

 **Substituir colocação em escala** Ativa e desativa a emulação da colocação de documento em escala na superfície de design. Isso permite aumentar o percentual de colocação em escala por um fator. Marque a caixa de seleção para ativar a emulação. Por exemplo, se o percentual de colocação em escala for de 100%, o documento na superfície de design será dimensionado em até 140%. Essa opção será desabilitada se o percentual de colocação em escala atual for de 180.

 **Largura mínima** Especifica a configuração de largura mínima. A largura mínima pode ser alterada em App.xaml.

 **Tema** Especifica o tema do aplicativo. Por exemplo, você pode mudar entre um tema escuro e um tema claro.

 **Exibir cromado** Ativa ou desativa o quadro de tablet simulado em torno do aplicativo no modo Design. Marque a caixa de seleção para mostrar o quadro.

 **Recortar para exibir** Especifica o modo de exibição. Marque a caixa de seleção para recortar o tamanho do documento de acordo com o tamanho do vídeo.

## <a name="document-outline-window"></a>Janela Estrutura de Tópicos de Documento
 A janela Estrutura de Tópicos de Documento no Designer XAML ajuda a executar estas tarefas:

- Exibir a estrutura hierárquica de todos os elementos no artboard.

- Selecionar elementos para que você possa modificá-los (movê-los na hierarquia, modificá-los no artboard, definir suas propriedades na janela Propriedades e assim por diante). Para obter mais informações, consulte [Trabalhando com elementos no Designer XAML](../designers/working-with-elements-in-xaml-designer.md)

- Criar e modificar modelos para elementos que são controles.

- Usar o menu de contexto para elementos selecionados. O mesmo menu também está disponível para os elementos selecionados no artboard.

  Para exibir a janela de Estrutura de tópicos do documento na barra de menus, escolha **Exibição**, **Outras Janelas**, **Estrutura de Tópicos do Documento**.

  ![Janela de Estrutura de tópicos do documento](../designers/media/xaml-editor-doc-outline.png "xaml_editor_doc_outline")

  Estas são as opções disponíveis na janela Estrutura de Tópicos de Documento:

  **Estrutura de Tópicos do Documento** O modo de exibição principal na janela Estrutura de Tópicos de Documento exibe a hierarquia de um documento em uma estrutura de árvore. Você pode usar a natureza hierárquica da estrutura de tópicos de documento para examinar o documento em vários níveis de detalhes, bem como para bloquear e ocultar os elementos individualmente ou em grupos.

  **Mostrar/ocultar** Exibe ou oculta os elementos da prancheta que correspondem aos itens na Estrutura de Tópicos de Documento. Use os botões **Mostrar/ocultar**, que exibem um símbolo de olho quando mostrados ou pressione CTRL+H para ocultar elementos e SHIFT+CTRL+H para exibi-los.

  **Bloquear/desbloquear** Bloqueia ou desbloqueia os elementos da prancheta que correspondem aos itens na Estrutura de Tópicos de Documento. Os elementos bloqueados não podem ser modificados. Use os botões **Bloquear/desbloquear**, que exibem um símbolo de cadeado quando bloqueados ou pressione CTRL+L para bloquear elementos e SHIFT+CTRL+L para desbloqueá-los.

  **Retornar escopo para pageRoot** A opção na parte superior da janela Estrutura de Tópicos de Documento, que mostra um símbolo de seta para cima, retorna a estrutura de tópicos de documento ao escopo anterior. O controle de escopo só é aplicável quando você está no escopo de um estilo ou modelo.

## <a name="properties-window"></a>Janela de Propriedades
 A janela Propriedades permite definir valores de propriedade em controles. Veja como ela se parece:

 ![Janela Propriedades](../designers/media/xaml-editor-prop-window.png "xaml_editor_prop_window")

 Há várias opções na parte superior da janela Propriedades. Você pode alterar o nome do elemento atualmente selecionado usando a caixa **Nome**. No canto esquerdo superior, há um ícone que representa o elemento atualmente selecionado. Para organizar as propriedades por categoria ou em ordem alfabética, clique em **Categoria**, **Nome** ou **Fonte** na lista **Organizar por**. Para ver a lista de eventos de um controle, clique no botão **Eventos**, que exibe um símbolo de relâmpago. Para pesquisar uma propriedade, comece a digitar o nome da propriedade na caixa **Propriedades de Pesquisa**. A janela Propriedades exibe as propriedades que correspondem à pesquisa à medida que você digita. Algumas propriedades permitem que você defina propriedades avançadas selecionando um botão de seta para baixo. Para obter mais informações sobre como usar propriedades e manipular eventos, veja o artigo sobre [Guia de início rápido: adicionando controles e manipulando eventos](http://go.microsoft.com/fwlink/?LinkID=247983)

 À direita de cada valor da propriedade, está um *marcador de propriedade* que é exibido como símbolo de caixa. A aparência do marcador da propriedade indica se existe uma associação de dados ou um recurso aplicado à propriedade. Por exemplo, um símbolo de caixa branca indica um valor padrão, um símbolo de caixa preta normalmente indica que um recurso local foi aplicado, e uma caixa laranja geralmente indica que uma associação de dados foi aplicada. Quando você clica no marcador da propriedade, pode navegar para a definição de um estilo, abrir o construtor da associação de dados ou abrir o selecionador de recurso.

## <a name="see-also"></a>Consulte também
 [Trabalhando com elementos no Designer XAML](../designers/working-with-elements-in-xaml-designer.md) [como criar e aplicar um recurso](../designers/how-to-create-and-apply-a-resource.md) [passo a passo: Associação de dados no Designer XAML](../designers/walkthrough-binding-to-data-in-xaml-designer.md)
