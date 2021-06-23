---
title: Criar UIs com o Visual Studio Designer XAML
description: Saiba mais sobre a interface do usuário do espaço de trabalho e os recursos do Designer XAML no Blend para Visual Studio que fornece uma interface visual para ajudá-lo a criar aplicativos baseados em XAML.
ms.date: 03/03/2020
ms.topic: conceptual
ms.custom: contperf-fy21q4, SEO-VS-2020
f1_keywords:
- VS.XamlDesigner
- VS.DevicePanel
- VS.DocumentOutline
- Blend.Start.Dev12
ms.devlang: CSharp
ms.assetid: c54969a7-d75a-4a35-9b37-af7a596a7c24
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.openlocfilehash: ef7d94acbb558ef2a8a3c557051e6dea16be916c
ms.sourcegitcommit: 809fff25b7701882c899c639eeb6da38ad4fb88a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2021
ms.locfileid: "112550682"
---
# <a name="create-a-ui-by-using-xaml-designer"></a>Criar uma interface do usuário usando o Designer XAML

O Designer XAML no Visual Studio e Blend para Visual Studio fornece uma interface visual para ajudá-lo a criar aplicativos baseados em XAML, como o WPF e o UWP. Você pode criar interfaces do usuário para seus aplicativos arrastando controles da janela Caixa de Ferramentas (janela Ativos no Blend para Visual Studio) e configurando propriedades na janela Propriedades. Você também pode editar XAML diretamente no modo de exibição XAML.

Para usuários avançados, é possível até mesmo [personalizar o Designer XAML](https://github.com/microsoft/xaml-designer-extensibility/blob/master/documents/xaml-designer-extensibility-migration.md).

> [!NOTE]
> O Xamarin. Forms não dá suporte a um designer XAML. Para exibir as UIs do XAML do Xamarin. Forms e editá-las enquanto o aplicativo estiver em execução, use o Hot recarregamento XAML para Xamarin. Forms. Para obter mais informações, consulte a página o [recarregamento de XAML para Xamarin. Forms (versão prévia)](/xamarin/xamarin-forms/xaml/hot-reload/) .

## <a name="xaml-designer-workspace"></a>Workspace do Designer XAML

O workspace no Designer XAML consiste em vários elementos da interface visual. Isso inclui a *prancheta* (que é a superfície de design visual), o editor XAML, a janela Estrutura de Tópicos do Documento (janela Objetos e Linha do Tempo no Blend para Visual Studio) e a janela Propriedades. Para abrir o Designer XAML, clique com o botão direito do mouse em um arquivo XAML no **Gerenciador de Soluções** e selecione **Exibir Designer**.

O Designer XAML fornece um modo de exibição XAML e um modo Design sincronizado de marcação XAML renderizada de seu aplicativo. Com um arquivo XAML aberto no Visual Studio ou no Blend para Visual Studio, você pode mudar o modo de exibição de Design e a exibição XAML usando as guias **Design** e **XAML**. Você pode usar o botão **Alternar Painéis**![botão Alternar Painéis no Designer XAML](media/swap-panes.PNG) para mudar qual janela é exibida na parte superior: a prancheta ou o Editor XAML.

### <a name="design-view"></a>Modo de exibição de Design

No modo de exibição de Design, a janela ativa é a que contém a prancheta, e você pode usá-la como a principal superfície de trabalho. É possível usá-la para criar visualmente uma página em seu aplicativo ao adicionar, desenhar ou modificar elementos. Para obter mais informações, confira [Trabalhar com elementos no Designer XAML](../xaml-tools/working-with-elements-in-xaml-designer.md). Esta ilustração mostra o artboard no modo Design.

![Modo de exibição de Design do Designer XAML](media/xaml-artboard.png)

Estas funcionalidades estão disponíveis no artboard:

**Guias de alinhamento**

As guias de alinhamento são *limites de alinhamento* exibidos como linhas tracejadas vermelhas para mostrar quando as bordas dos controles estão alinhadas ou quando as linhas de base de texto estão alinhadas. Os limites de alinhamento só são exibidos quando a opção de **ajuste a guias de alinhamento** está habilitada.

**Rails de grade**

Linhas de grade são usadas para gerenciar linhas e colunas em um painel de [Grade](xref:Windows.UI.Xaml.Controls.Grid). Você pode criar e excluir linhas e colunas, bem como ajustar suas larguras e alturas relativas. O rail de Grade vertical, exibido à esquerda da planilha, é usado para linhas e a linha horizontal, exibida na parte superior, é usada para colunas.

**Adornos de grade**

Um adorno de Grade é exibido como um triângulo que tem uma linha vertical ou horizontal anexada a ele no trilho da Grade. Quando você arrasta um adorno de Grade, as larguras ou alturas das linhas ou colunas adjacentes são atualizadas conforme você move o mouse.

Os adornos de Grade são usados para controlar a largura e a altura de linhas e colunas de uma Grade. Você pode adicionar uma nova coluna ou linha clicando nos trilhos da Grade. Quando você adiciona uma nova linha ou linha de coluna a um painel de Grade com duas ou mais colunas ou linhas, uma minibarra de ferramentas exibida fora do trilho permite definir explicitamente a largura e a altura. A minibarra de ferramentas permite que você defina opções de dimensionamento para as linhas e colunas da Grade.

![Adorno de grade no Designer XAML](media/grid-adorner.png)

**Alças de redimensionamentos**

As alças de redimensionamento são exibidas em controles selecionados e permitem redimensionar o controle. Quando você redimensiona um controle, os valores de largura e altura geralmente são exibidos para ajudar a dimensionar o controle. Para obter mais informações sobre a manipulação de controles no modo de exibição de **Design**, confira [Trabalhar com elementos no Designer XAML](../xaml-tools/working-with-elements-in-xaml-designer.md).

**Margens**

As margens representam o espaço fixo entre a borda de um controle e a borda do respectivo contêiner. Você pode definir as margens de um controle usando as propriedades [Margem](xref:Windows.UI.Xaml.FrameworkElement.Margin) em **Layout** na janela **Propriedades**.

**Adornos de margem**

Use adornos de margem para alterar as margens de um elemento relativo ao respectivo contêiner de layout. Quando um adorno de margem está aberto, uma margem não está definida, e o adorno de margem exibe uma cadeia quebrada. Quando a margem não está definida, os elementos permanecem em vigor quando o contêiner de layout é redimensionado no tempo de execução. Quando um adorno de margem está fechado, ele exibe uma cadeia ininterrupta, e os elementos são movidos com a margem enquanto o contêiner de layout é redimensionado no tempo de execução (a margem permanece fixa).

**Alças do elemento**

Você pode modificar um elemento usando as alças do elemento que são exibidas no artboard ao mover o ponteiro sobre os cantos da caixa azul que circunda um elemento. Essas alças permitem girar, redimensionar, inverter, mover ou adicionar um radiano do canto ao elemento. O símbolo da alça do elemento varia de acordo com a função e é alterado dependendo do local exato do ponteiro. Se você não vir as alças do elemento, verifique se o elemento está selecionado.

No modo de exibição de **Design**, os comandos adicionais da prancheta estão disponíveis na área inferior esquerda da janela, como mostrado aqui:

![Comandos do modo de exibição de Design](media/xaml-design-view-controls.png)

Estes comandos estão disponíveis na barra de ferramentas:

**Zoom**

O zoom permite dimensionar a superfície de design. Você pode aplicar zoom de 12,5% a 800% ou selecionar opções como **Ajustar à seleção** e **Ajustar tudo**.

**Exibir/Ocultar grade de ajuste**

Exibe ou oculta a grade de ajuste que mostra as linhas de grade. As linhas de grade são usadas quando a opção de **ajuste às linhas de grade** ou de **ajuste às guias de alinhamento** está habilitada.

**Ativar/desativar ajuste às linhas de grade**

Se o **ajuste para linhas de grade** estiver habilitado, um elemento tende a se alinhar com as linhas de grade horizontais e verticais mais próximas ao arrastá-lo para a prancheta.

**Alternar plano de fundo da prancheta**

Alterna entre um plano de fundo claro ou escuro.

**Ativar/desativar ajuste às guias de alinhamento**

As guias de alinhamento ajudam a alinhar os controles relativos uns aos outros. Se a opção de **ajuste às guias de alinhamento** estiver habilitada, quando você arrastar um controle relativo a outros controles, os limites de alinhamento serão exibidos quando as margens e o texto de alguns controles estiverem alinhados horizontal ou verticalmente. Um limite de alinhamento é exibido como uma linha vermelho-tracejada.

**Desabilitar código do projeto**

Desabilita o [código do projeto](debugging-or-disabling-project-code-in-xaml-designer.md), como controles personalizados e conversores de valor, e recarrega o designer.

### <a name="xaml-view"></a>Exibição XAML

No modo de exibição **XAML**, a janela que contém o editor de XAML é a janela ativa, e o editor de XAML é a ferramenta de criação principal. A linguagem XAML fornece um vocabulário declarativo, com base em XML, para especificar a interface do usuário de um aplicativo. O modo de exibição XAML inclui o IntelliSense, formatação automática, realce de sintaxe e navegação de marcação. A imagem a seguir mostra o modo de exibição XAML com um menu IntelliSense aberto:

![Exibição XAML](media/xaml-editor.png)

## <a name="document-outline-window"></a>Janela Estrutura de Tópicos de Documento

A janela Estrutura de Tópicos do Documento no Visual Studio é semelhante à janela [Objetos e Linha do Tempo](creating-a-ui-by-using-blend-for-visual-studio.md#objects-and-timeline-window) no Blend para Visual Studio. A Estrutura de Tópicos do Documento ajuda a executar estas tarefas:

- Exibir a estrutura hierárquica de todos os elementos no artboard.

- Selecione elementos para que você possa modificá-los. Por exemplo, você pode movê-los na hierarquia ou definir suas propriedades na janela Propriedades. Para obter mais informações, confira [Trabalhar com elementos no Designer XAML](../xaml-tools/working-with-elements-in-xaml-designer.md).

- Criar e modificar modelos para elementos que são controles.

- [Criar animações](animate-objects-in-xaml-designer.md) (somente no Blend para Visual Studio).

Para exibir a janela de estrutura de tópicos do documento no Visual Studio, na barra de menus, selecione **Exibir**  >  **outra**  >  **estrutura de tópicos do documento** do Windows.
Para exibir a janela de objetos e linha do tempo no Blend para Visual Studio, na barra de menus, selecione **Exibir**  >  **estrutura de tópicos do documento**.

![Janela Estrutura de Tópicos do Documento no Visual Studio](media/document-outline-window.png)

O modo de exibição principal nas janelas Estrutura de Tópicos do Documento/Objetos e Linha do Tempo exibe a hierarquia de um documento em uma estrutura de árvore. Você pode usar a natureza hierárquica da estrutura de tópicos de documento para examinar o documento em vários níveis de detalhes, bem como para bloquear e ocultar os elementos individualmente ou em grupos. As opções a seguir estão disponíveis na janela estrutura de tópicos/Objetos e Linha do Tempo do documento:

**Mostrar/ocultar**

Exibe ou oculta elementos da prancheta. Aparece como um símbolo de olho quando exibida. Você também pode pressionar **Ctrl** + **h** para ocultar um elemento e **Shift** + **Ctrl** + **h** para mostrá-lo.

**Bloquear/desbloquear**

Bloqueia ou desbloqueia elementos da prancheta. Os elementos bloqueados não podem ser modificados. Aparece como um símbolo de cadeado quando bloqueado. Você também pode pressionar **Ctrl** + **L** para bloquear um elemento e **Shift** + **Ctrl** + **L** para desbloqueá-lo.

**Retornar escopo para pageRoot**

A opção na parte superior das janelas Estrutura de Tópicos do Documento/Objetos e Linha do Tempo, que mostra um símbolo de seta para cima, retorna ao escopo anterior. O controle de escopo só é aplicável quando você está no escopo de um estilo ou modelo.

## <a name="properties-window"></a>Janela de Propriedades

A janela **Propriedades** permite definir valores de propriedade em controles. Esta é a aparência dele:

![Janela de Propriedades](media/xaml-designer-properties-window.png)

Há várias opções na parte superior da janela **Propriedades**:

- Altere o nome do elemento atualmente selecionado usando a caixa **Nome**.
- No canto esquerdo superior, há um ícone que representa o elemento atualmente selecionado.
- Para organizar as propriedades por categoria ou em ordem alfabética, clique em **Categoria**, **Nome** ou **Fonte** na lista **Organizar por**.
- Para ver a lista de eventos de um controle, clique no botão **Eventos**, que exibe um símbolo de relâmpago.
- Para procurar uma propriedade, comece a digitar o nome da propriedade na caixa de pesquisa. A janela **Propriedades** exibe as propriedades que correspondem à pesquisa à medida que você digita.

Algumas propriedades permitem que você defina propriedades avançadas selecionando um botão de seta para baixo.

À direita de cada valor da propriedade, está um *marcador de propriedade* que é exibido como símbolo de caixa. A aparência do marcador da propriedade indica se existe uma associação de dados ou um recurso aplicado à propriedade. Por exemplo, um símbolo de caixa branca indica um valor padrão, um símbolo de caixa preta normalmente indica que um recurso local foi aplicado, e uma caixa laranja geralmente indica que uma associação de dados foi aplicada. Quando você clica no marcador da propriedade, pode navegar para a definição de um estilo, abrir o construtor da associação de dados ou abrir o selecionador de recurso.

Para obter mais informações sobre como usar propriedades e manipular eventos, confira [Introdução a controles e padrões](/windows/uwp/design/controls-and-patterns/controls-and-events-intro).

## <a name="see-also"></a>Confira também

- [Trabalhar com elementos no Designer XAML](../xaml-tools/working-with-elements-in-xaml-designer.md)
- [Como criar e aplicar um recurso](../xaml-tools/how-to-create-and-apply-a-resource.md)
- [Explicação passo a passo: associar dados no Designer XAML](../xaml-tools/walkthrough-binding-to-data-in-xaml-designer.md)
