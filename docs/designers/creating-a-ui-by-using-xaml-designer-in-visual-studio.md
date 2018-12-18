---
title: Criando uma interface do usuário usando o Designer XAML
ms.date: 11/05/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
f1_keywords:
- VS.XamlDesigner
- VS.DevicePanel
- VS.XamlEditor
- VS.DocumentOutline
ms.assetid: c54969a7-d75a-4a35-9b37-af7a596a7c24
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: b991b50ab2ee329adaaff7a31c2dbb4f2d5bb806
ms.sourcegitcommit: bccb05b5b4e435f3c1f7c36ba342e7d4031eb398
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51220990"
---
# <a name="create-a-ui-by-using-xaml-designer-in-visual-studio"></a>Criar uma interface do usuário usando o Designer XAML no Visual Studio

O Designer XAML no Visual Studio fornece uma interface visual para ajudá-lo a criar aplicativos Web e Windows baseados em XAML. Você pode criar interfaces do usuário para seus aplicativos arrastando controles da **Caixa de Ferramentas** e configurando propriedades na janela **Propriedades**. Você também pode editar XAML diretamente no modo de exibição XAML.

Para tarefas avançadas de design XAML como animações e comportamentos, consulte [Criando uma interface do usuário usando o Blend for Visual Studio](../designers/creating-a-ui-by-using-blend-for-visual-studio.md). Confira também [Design XAML no Visual Studio e no Blend para Visual Studio](../designers/designing-xaml-in-visual-studio.md) para obter uma comparação entre as ferramentas.

## <a name="xaml-designer-workspace"></a>Workspace do Designer XAML

O workspace no Designer XAML consiste em vários elementos da interface visual. Isso inclui as janelas **Prancheta**, **Editor de XAML**, **Dispositivo**, **Estrutura de Tópicos de Documento** e **Propriedades**. Para abrir o Designer XAML, clique com o botão direito do mouse em um arquivo XAML no **Gerenciador de Soluções** e selecione **Exibir Designer**.

## <a name="authoring-views"></a>Criando modos de exibição

O Designer XAML fornece um modo de exibição XAML e um modo Design sincronizado de marcação XAML renderizada de seu aplicativo. Com um arquivo XAML aberto no Visual Studio, você pode mudar o modo de exibição de Design e a exibição XAML usando as guias **Design** e **XAML**. Você pode usar o botão **Alternar Painéis** para mudar qual janela é exibida no topo: a prancheta ou o Editor XAML.

No modo de exibição de Design, a janela que contém a *prancheta* é a janela ativa e você pode usá-la como superfície de trabalho primária. Você pode usá-la para criar visualmente uma página em seu aplicativo adicionando ou desenhando elementos e depois modificando-os. Para obter mais informações, consulte [Trabalhando com elementos no Designer XAML](../designers/working-with-elements-in-xaml-designer.md). Esta ilustração mostra o artboard no modo Design.

![Modo de exibição de Design do Designer XAML](../designers/media/xaml_editor_design_view.png)

Estas funcionalidades estão disponíveis no artboard:

**Guias de alinhamento**

As guias de alinhamento são *limites de alinhamento* que são exibidos como linhas vermelho-tracejadas para mostrar quando as bordas dos controles estão alinhadas ou quando as linhas de base de texto estão alinhadas. Os limites de alinhamento só são exibidos quando a opção de **ajuste a guias de alinhamento** está habilitada.

**Rails de grade**

Rails de `Grid` são usados para gerenciar linhas e colunas em um painel de [Grade](/uwp/api/Windows.UI.Xaml.Controls.Grid). Você pode criar e excluir linhas e colunas, bem como ajustar suas larguras e alturas relativas. O rail de Grade vertical, exibido à esquerda da planilha, é usado para linhas e a linha horizontal, exibida na parte superior, é usada para colunas.

**Adornos de grade**

Um adorno de Grade é exibido como um triângulo que tem uma linha vertical ou horizontal anexada a ele no trilho da Grade. Quando você arrasta um adorno de Grade, as larguras ou alturas das linhas ou colunas adjacentes são atualizadas conforme você move o mouse.

Os adornos de Grade são usados para controlar a largura e a altura de linhas e colunas de uma Grade. Você pode adicionar uma nova coluna ou linha clicando nos trilhos da Grade. Quando você adiciona uma nova linha ou linha de coluna a um painel de Grade com duas ou mais colunas ou linhas, uma minibarra de ferramentas exibida fora do trilho permite definir explicitamente a largura e a altura. A minibarra de ferramentas permite que você defina opções de dimensionamento para as linhas e colunas da Grade.

**Alças de redimensionamentos**

As alças de redimensionamento são exibidas em controles selecionados e permitem redimensionar o controle. Quando você redimensiona um controle, os valores de largura e altura geralmente são exibidos para ajudar a dimensionar o controle. Para obter mais informações sobre a manipulação de controles no modo de exibição de **Design**, confira [Trabalhando com elementos no Designer XAML](../designers/working-with-elements-in-xaml-designer.md).

**Margens**

As margens representam o espaço fixo entre a borda de um controle e a borda do respectivo contêiner. Você pode definir as margens de um controle usando as propriedades [Margem](/uwp/api/windows.ui.xaml.frameworkelement.margin) em **Layout** na janela Propriedades.

**Adornos de margem**

Você pode usar adornos de margem para alterar as margens de um elemento relativo ao respectivo contêiner de layout. Quando um adorno de margem está aberto, uma margem não está definida, e o adorno de margem exibe uma cadeia quebrada. Quando a margem não está definida, os elementos permanecem em vigor quando o contêiner de layout é redimensionado no tempo de execução. Quando um adorno de margem está fechado, ele exibe uma cadeia ininterrupta, e os elementos são movidos com a margem enquanto o contêiner de layout é redimensionado no tempo de execução (a margem permanece fixa).

**Alças do elemento**

Você pode modificar um elemento usando as alças do elemento que são exibidas no artboard ao mover o ponteiro sobre os cantos da caixa azul que circunda um elemento. Essas alças permitem girar, redimensionar, inverter, mover ou adicionar um radiano do canto ao elemento. O símbolo da alça do elemento varia por função e altera dependendo do local exato do ponteiro. Se você não vir as alças do elemento, verifique se o elemento está selecionado.

No modo de exibição de **Design**, os comandos adicionais da prancheta estão disponíveis na área inferior esquerda da tela, como é mostrado aqui:

![Comandos do modo de exibição de Design](../designers/media/xaml_editor_design_controls.png)

Estes comandos estão disponíveis na barra de ferramentas:

**Zoom**

O zoom permite dimensionar a superfície de design. Você pode aplicar zoom de 12,5% a 800% ou selecionar opções, como **Ajustar à Seleção** e **Ajustar a Tudo**.

**Exibir/Ocultar grade de ajuste**

Exibe ou oculta a grade de ajuste que mostra as linhas de grade. As linhas de grade são usadas quando a opção de **ajuste às linhas de grade** ou de **ajuste às guias de alinhamento** está habilitada.

**Ativar/desativar ajuste às linhas de grade**

Se a opção de **ajuste às linhas de grade** estiver habilitada quando você arrastar um elemento na prancheta, a tendência será o elemento alinhar-se às linhas de grade horizontais e verticais mais próximas.

**Ativar/desativar ajuste às guias de alinhamento**

As guias de alinhamento ajudam a alinhar os controles relativos uns aos outros. Se a opção de **ajuste às guias de alinhamento** estiver habilitada, quando você arrastar um controle relativo a outros controles, os limites de alinhamento serão exibidos quando as margens e o texto de alguns controles estiverem alinhados horizontal ou verticalmente. Um limite de alinhamento é exibido como uma linha vermelho-tracejada.

No modo de exibição **XAML**, a janela que contém o editor de XAML é a janela ativa, e o editor de XAML é a ferramenta de criação principal. A linguagem XAML fornece um vocabulário declarativo, com base em XML, para especificar a interface do usuário de um aplicativo. O modo de exibição XAML inclui o IntelliSense, formatação automática, realce de sintaxe e navegação de marcação. Esta ilustração mostra o modo de exibição XAML:

![Exibição XAML](../designers/media/xaml_editor.png)

**Barra do modo divisão**

A barra do modo divisão é exibida na parte superior do modo de exibição XAML quando o editor XAML está na janela inferior. A barra do modo de exibição de divisão permite controlar os tamanhos relativos do modo de exibição de **Design** e do modo de exibição **XAML**. Você também pode trocar os locais das exibições (usando o botão **Alternar Painéis**), especificar se as exibições são organizadas horizontal ou verticalmente e recolher a exibição.

**Zoom de Marcação**

O zoom de marcação permite dimensionar o modo de exibição **XAML**. Você pode aplicar zoom de 20% a 400%.

## <a name="device-window"></a>Janela Dispositivo

> [!NOTE]
> Se a versão da plataforma de destino (`TargetPlatformVersion`) de um aplicativo UWP for 10.0.16299.0 ou superior, a janela **Dispositivo** não estará disponível.

A janela **Dispositivo** no Designer XAML permite simular no tempo de design vários modos de exibição, vídeos e opções de exibição para o projeto. A janela **Dispositivo** fica disponível no menu **Design** quando você está trabalhando no Designer XAML. Veja como ela se parece:

![Janela Dispositivo](../designers/media/xaml_editor_device_panel.png)

Estas são as opções disponíveis na janela Dispositivo:

**Vídeo**

Especifica diferentes resoluções e tamanhos de exibição para o aplicativo.

**Orientação**

Especifica diferentes orientações para o aplicativo: **Paisagem** ou **Retrato**.

**Borda**

Especifica diferentes alinhamentos de borda para o aplicativo: **Ambos**, **Esquerda**, **Direita** ou **Nenhum**.

**Alto Contraste**

Visualize o aplicativo com base na configuração de contraste selecionada. Essa configuração, quando definida como um valor diferente do **Padrão**, substitui a propriedade `RequestedTheme` definida no arquivo *App.xaml*.

**Substituir colocação em escala**

Ativa e desativa a emulação da colocação de documento em escala na superfície de design. Isso permite aumentar o percentual de colocação em escala por um fator. Marque a caixa de seleção para ativar a emulação. Por exemplo, se o percentual de colocação em escala for de 100%, o documento na superfície de design será dimensionado em até 140%. Essa opção será desabilitada se o percentual de colocação em escala atual for de 180.

**Largura mínima**

Especifica a configuração de largura mínima. A largura mínima pode ser alterada em *App.xaml*.

**Tema**

Especifica o tema do aplicativo. Por exemplo, você pode alternar entre um tema **Escuro** e **Claro**.

**Mostrar cromado**

Ativa ou desativa o quadro de tablet simulado em torno do aplicativo no modo Design. Marque a caixa de seleção para mostrar o quadro.

**Recortar para exibir**

Especifica o modo de exibição. Marque a caixa de seleção para recortar o tamanho do documento de acordo com o tamanho do vídeo.

## <a name="document-outline-window"></a>Janela Estrutura de Tópicos de Documento

A janela Estrutura de Tópicos de Documento no Designer XAML ajuda a executar estas tarefas:

- Exibir a estrutura hierárquica de todos os elementos no artboard.

- Selecionar elementos para que você possa modificá-los (movê-los na hierarquia, modificá-los no artboard, definir suas propriedades na janela Propriedades e assim por diante). Para obter mais informações, confira [Trabalhando com elementos no Designer XAML](../designers/working-with-elements-in-xaml-designer.md)

- Criar e modificar modelos para elementos que são controles.

- Usar o menu de contexto para elementos selecionados. O mesmo menu também está disponível para os elementos selecionados no artboard.

Para exibir a janela **Estrutura de Tópicos do Documento**, na barra de menus escolha **Exibir** > **Outras Janelas** > **Estrutura de Tópicos do Documento**.

![Janela Estrutura de Tópicos de Documento](../designers/media/xaml_editor_doc_outline.png)

Estas são as opções disponíveis na janela **Estrutura de Tópicos do Documento**:

**Estrutura de Tópicos do Documento**

O modo de exibição principal na janela **Estrutura de Tópicos de Documento** exibe a hierarquia de um documento em uma estrutura de árvore. Você pode usar a natureza hierárquica da estrutura de tópicos de documento para examinar o documento em vários níveis de detalhes, bem como para bloquear e ocultar os elementos individualmente ou em grupos.

**Mostrar/ocultar**

Exibe ou oculta os elementos da prancheta que correspondem aos itens na estrutura de tópicos de documento. Use os botões **Mostrar/ocultar**, que exibem um símbolo de olho quando mostrados ou pressione **Ctrl**+**H** para ocultar elementos e **Shift**+**Ctrl**+**H** para exibi-los.

**Bloquear/desbloquear**

Bloqueia ou desbloqueia os elementos do artboard que correspondem aos itens na Estrutura de Tópicos de Documento. Os elementos bloqueados não podem ser modificados. Use os botões **Bloquear/desbloquear**, que exibem um símbolo de cadeado quando bloqueados ou pressione **Ctrl**+**L** para bloquear elementos e **Shift**+**Ctrl**+**L** para desbloqueá-los.

**Retornar escopo para pageRoot**

A opção na parte superior da janela **Estrutura de Tópicos de Documento**, que mostra um símbolo de seta para cima, retorna a estrutura de tópicos de documento ao escopo anterior. O controle de escopo só é aplicável quando você está no escopo de um estilo ou modelo.

## <a name="properties-window"></a>Janela de Propriedades

A janela **Propriedades** permite definir valores de propriedade em controles. Veja como ela se parece:

![Janela de Propriedades](../designers/media/xaml_editor_prop_window.png)

Há várias opções na parte superior da janela **Propriedades**. Você pode alterar o nome do elemento atualmente selecionado usando a caixa **Nome**. No canto esquerdo superior, há um ícone que representa o elemento atualmente selecionado. Para organizar as propriedades por categoria ou em ordem alfabética, clique em **Categoria**, **Nome** ou **Fonte** na lista **Organizar por**. Para ver a lista de eventos de um controle, clique no botão **Eventos**, que exibe um símbolo de relâmpago. Para pesquisar uma propriedade, comece a digitar o nome da propriedade na caixa **Propriedades de Pesquisa**. A janela **Propriedades** exibe as propriedades que correspondem à pesquisa à medida que você digita. Algumas propriedades permitem que você defina propriedades avançadas selecionando um botão de seta para baixo. Para obter mais informações de como usar propriedades e manipular eventos, confira [Introdução a controles e padrões](/windows/uwp/design/controls-and-patterns/controls-and-events-intro)

À direita de cada valor da propriedade, está um *marcador de propriedade* que é exibido como símbolo de caixa. A aparência do marcador da propriedade indica se existe uma associação de dados ou um recurso aplicado à propriedade. Por exemplo, um símbolo de caixa branca indica um valor padrão, um símbolo de caixa preta normalmente indica que um recurso local foi aplicado, e uma caixa laranja geralmente indica que uma associação de dados foi aplicada. Quando você clica no marcador da propriedade, pode navegar para a definição de um estilo, abrir o construtor da associação de dados ou abrir o selecionador de recurso.

## <a name="see-also"></a>Consulte também

- [Trabalhando com elementos no Designer XAML](../designers/working-with-elements-in-xaml-designer.md)
- [Como criar e aplicar um recurso](../designers/how-to-create-and-apply-a-resource.md)
- [Passo a passo: associando dados no XAML Designer](../designers/walkthrough-binding-to-data-in-xaml-designer.md)