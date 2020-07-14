---
title: Editor de código XAML
description: Faça um tour pelo editor de código XAML no Visual Studio
ms.date: 06/16/2020
ms.topic: overview
monikerRange: vs-2019
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 6421fd0139b04262ac5f1e835f010c1372c034ee
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85329183"
---
# <a name="xaml-code-editor"></a>Editor de código XAML

O editor de código XAML no [IDE do Visual Studio](../get-started/visual-studio-ide.md) inclui todas as ferramentas necessárias para criar aplicativos WPF e UWP para a plataforma Windows e para [Xamarin. Forms](/xamarin/xamarin-forms/user-interface/text/editor/). Este artigo descreve a função que o editor de código desempenha quando você desenvolve aplicativos baseados em XAML e os recursos que são exclusivos para o editor de código XAML no Visual Studio 2019.

Para começar, vamos dar uma olhada no IDE (ambiente de desenvolvimento integrado) com um projeto do WPF aberto. A imagem a seguir mostra várias das principais ferramentas do IDE que você usará junto com o editor de código XAML.

:::image type="content" source="media/xaml-code-editor-overview-sml.png" alt-text="O IDE do Visual Studio 2019 com um projeto do WPF aberto em XAML" lightbox="media/xaml-code-editor-overview-lrg.png":::

Na parte inferior esquerda da imagem em sentido horário, as principais ferramentas do IDE são as seguintes:

- A janela do **[Editor de código XAML](#xaml-code-editor-ui)** &mdash; o assunto deste artigo &mdash; em que você cria e edita seu código.
- A janela de **[Designer XAML](creating-a-ui-by-using-xaml-designer-in-visual-studio.md)** , onde você projeta sua interface do usuário.
- A janela da **[caixa de ferramentas](../ide/reference/toolbox.md)** encaixáveis, em que você adiciona controles à sua interface do usuário.
- O botão de **[depuração](../debugger/debugger-feature-tour.md)** , onde você executa o código e o depura. <br>(Você também pode editar seu código em tempo real enquanto estiver Depurando com o [Hot recarregamento de XAML](xaml-hot-reload.md).)
- A janela de **[Gerenciador de soluções](../ide/solutions-and-projects-in-visual-studio.md)** , onde você gerencia seus arquivos, projetos e soluções.
- A janela **[Propriedades](../ide/reference/properties-window.md)** , onde você altera a aparência da sua interface do usuário e como os controles da interface do usuário funcionam.

Para continuar, vamos saber mais sobre o editor de código XAML.

## <a name="xaml-code-editor-ui"></a>Interface do usuário do editor de código XAML

Embora a janela do editor de código para aplicativos XAML compartilhasse alguns elementos da interface do usuário (UI) que também aparecem em nosso IDE padrão, ela também inclui alguns recursos exclusivos que facilitam o desenvolvimento de aplicativos XAML.

Aqui está uma olhada na própria janela do editor de código XAML.

![A janela do editor de código XAML no Visual Studio](media/xaml-code-editor-window.png "Captura de tela da janela do editor de código XAML no Visual Studio 2019")

Em seguida, vamos dar uma olhada nas funções de cada um dos elementos da interface do usuário no editor de código.

### <a name="first-row"></a>Primeira linha

Na primeira linha na parte superior da janela de código XAML, à esquerda, há uma guia **design** , um botão **alternar painéis** , uma guia **XAML** e um botão **pop-up XAML** .

![A primeira das duas linhas superiores da janela do editor de código XAML no Visual Studio, com o lado esquerdo da primeira linha realçada](media/xaml-code-editor-top-row-left.png "Captura de tela da primeira das duas linhas superiores da janela do editor de código XAML no Visual Studio 2019, na qual os elementos da interface do usuário à esquerda são realçados")

Veja como eles funcionam:

- A guia **design** altera o foco do editor de código XAML para a designer XAML.
- O botão **alternar painéis** inverte o local do designer XAML e o editor de código XAML no IDE.
- A guia **XAML** altera o foco de volta para o editor de código XAML.
- O botão **pop-out XAML** cria uma janela separada do editor de código XAML que está fora do IDE.

Continuando à direita, há um botão de **divisão vertical** , um botão de **divisão horizontal** e um botão **recolher painéis** .

![A primeira das duas linhas superiores da janela do editor de código XAML no Visual Studio, com o lado direito da primeira linha realçada](media/xaml-code-editor-top-row-right.png "Captura de tela da primeira das duas linhas superiores da janela do editor de código XAML no Visual Studio 2019, na qual os elementos da interface do usuário à direita são realçados")

Veja como eles funcionam:

- O botão **divisão vertical** altera o local do designer XAML e o editor de código XAML no IDE de um alinhamento horizontal para um alinhamento vertical.
- O botão de **divisão horizontal** altera o local do designer XAML e o editor de código XAML no IDE de um alinhamento vertical para um alinhamento horizontal.
- O botão **recolher painel** permite que você recolha o que está no painel inferior, seja ele o editor de código ou o designer. (Para restaurar o painel inferior, escolha o mesmo botão novamente, que agora é chamado de botão **expandir painel** .)

<!-- [!TIP]
> You can run two parallel instances of the XAML code editor concurrently by using both the **Pop Out XAML** button and the **Expand Pane** button.
>
> You might find it useful to have one larger window open that reveals more of your code in context and a smaller pane open that has its focus directly on the code that you're working on. -->

### <a name="second-row"></a>Segunda linha

Na segunda linha na parte superior da janela de código XAML, há duas listas suspensas de janela. No entanto, se você exibir a dica de ferramenta para esses elementos da interface do usuário, ele os identificará como o "elemento: janela" e a "membro: janela".

![A segunda das duas linhas superiores da janela do editor de código XAML no Visual Studio, onde ambas as listas suspensas de janela são visíveis](media/xaml-code-editor-top-row-windows.png "Captura de tela da segunda das duas linhas principais da janela do editor de código XAML no Visual Studio 2019, em que ambas as listas suspensas de janela são visíveis")

As listas suspensas de janela têm funções diferentes, da seguinte maneira:

- A **janela element:** à esquerda ajuda a exibir e navegar para elementos irmãos ou pai.

  Especificamente, ele mostra uma exibição de estrutura de tópicos que revela a estrutura de marca do seu código. Quando você seleciona na lista, seu foco no editor de código se ajustará à linha de código que inclui o elemento selecionado.

    ![A lista suspensa elemento: janela no Visual Studio](media/xaml-element-window-dropdown.png "Captura de tela da lista suspensa do elemento: janela no Visual Studio 2019")

- A **janela membro:** à direita ajuda a exibir e navegar para atributos ou elementos filho.

    Especificamente, ele mostra uma lista das propriedades em seu código. Quando você seleciona na lista, seu foco no editor de código se ajustará à linha de código que inclui a propriedade selecionada.

    ![A lista suspensa de membros: janela no Visual Studio](media/xaml-member-window-dropdown.png "Captura de tela da lista suspensa de membros: janela no Visual Studio 2019")

### <a name="middle-pane-code-editor"></a>Painel central, editor de código

O painel central é a parte "código" do editor de código XAML. Ele inclui a maioria dos recursos que você encontrará no [Editor de código do IDE](../get-started/tutorial-editor.md). Vamos abordar vários dos recursos do universal IDE que podem ajudá-lo a desenvolver seu código XAML. Também destacaremos os recursos de Unique-to-XAML no IDE.

![O editor de código XAML, somente painel central, no Visual Studio](media/xaml-code-editor-middle.png "Captura de tela do editor de código XAML, somente painel central, no Visual Studio 2019")

#### <a name="quick-actions"></a>Ações Rápidas

Você pode usar [ações rápidas](../ide/quick-actions.md) para refatorar, gerar ou modificar código de outra forma com uma única ação.

Por exemplo, uma tarefa útil que você pode executar usando ações rápidas é remover o **uso desnecessário** do código C# na guia **MainWindow.XAML.cs** .

Veja como:

1. Passe o mouse sobre uma instrução using, escolha o ícone de lâmpada e, em seguida, escolha **Remover usos desnecessários** na lista suspensa.

    ![A opção "remover using desnecessários" do editor de IDE no menu de ações rápidas](media/xaml-code-editor-remove-usings.png "Captura de tela da opção remover uso desnecessário do editor do IDE do menu ações rápidas")

1. Escolha se deseja corrigir todas as ocorrências no **documento**, no **projeto**ou na **solução**.
1. Exiba a caixa de diálogo **Visualizar** e, em seguida, escolha **aplicar**.

Você também pode acessar esse recurso na barra de menus. Para fazer isso, escolha **Editar**o  >  **IntelliSense**  >  **remover e classificar usando**.

Para obter mais informações sobre como usar configurações, consulte a página [classificar usando](../ide/reference/sort-usings.md) . Para obter mais informações sobre o IntelliSense, consulte a página [IntelliSense no Visual Studio](../ide/using-intellisense.md) . E, para obter mais informações sobre algumas das maneiras típicas de os desenvolvedores usarem ações rápidas, consulte a página [ações rápidas comuns](../ide/common-quick-actions.md) .

#### <a name="change-tracking"></a>Change tracking

A cor da margem esquerda permite que você mantenha o controle das alterações feitas em um arquivo. Veja como as cores se relacionam às ações tomadas:

- As alterações feitas desde que o arquivo foi aberto, mas não salvas, são indicadas por uma barra **amarela** na margem esquerda (conhecida como margem de seleção).

    ![Edição do editor de código com barra amarela](media/code-editor-edit-yellow.png "Captura de tela do editor de código com uma alteração marcada com uma barra amarela na margem de seleção.")

- Depois de salvar as alterações (mas antes de fechar o arquivo), a barra fica **verde**.

    ![Editor de código editar com barra verde](media/code-editor-edit-green.png "Captura de tela do editor de código com uma alteração marcada com uma barra verde na margem de seleção.")

Para desativar e ativar esse recurso, altere a opção **Controlar Alterações** nas configurações **Editor de Texto** (**Ferramentas** > **Opções** > **Editor de Texto**).

Para obter mais informações sobre o controle de alterações &mdash; para incluir as linhas onduladas (também conhecidas como "rabiscos") que aparecem em cadeias de caracteres de código, &mdash; consulte a seção **[recursos do editor](../ide/writing-code-in-the-code-and-text-editor.md#editor-features)** dos [recursos da página Editor de código do Visual Studio](../ide/writing-code-in-the-code-and-text-editor.md) .

#### <a name="right-click-context-menu"></a>Clique com o botão direito do mouse em menu de contexto

Quando você está editando seu código no editor de código XAML, há vários recursos que você pode acessar usando o menu de contexto de clique com o botão direito do mouse. A maioria desses recursos está disponível universalmente no IDE do Visual Studio, enquanto outros são específicos ao uso de um editor de código junto com uma janela de design.

![O menu de contexto de clique com o botão direito do mouse no editor de código XAML no Visual Studio](media/xaml-code-editor-right-click-menu.png "Captura de tela do menu de contexto de clique com o botão direito do mouse no editor de código XAML no Visual Studio 2019")

Veja o que cada recurso faz e como ele é útil:

- **Exibir código** – abre a janela de código da linguagem de programação, que geralmente é tabulada ao lado do modo de exibição padrão que inclui a janela de design e o editor de código XAML.
- **Designer de exibição** -abre a exibição padrão que inclui a janela de design e o editor de código XAML. (Se você já estiver no modo de exibição padrão, ele não fará nada.)
- **Ações rápidas e refatoração** – refactores, gera ou modifica o código de outra forma com uma única ação. Ao passar o mouse sobre o código, você verá um ícone de lâmpada quando uma ação ou refatoração rápida estiver disponível. <br>Consulte também: [ações rápidas](../ide/quick-actions.md) e [código de refatoração](../ide/refactoring-in-visual-studio.md).
- **Renomear...** -Renomeia somente namespaces. Se você não tiver um namespace para renomear, receberá uma mensagem de erro dizendo "somente os prefixos de namespace podem ser renomeados."
- **Remover e classificar namespaces** – remove namespaces não utilizados e, em seguida, classifica os namespaces que permanecem.
- **Inspecionar definição** – visualiza a definição de um tipo sem sair do local atual no editor. <br>Consulte também: [inspecionar a definição](../ide/go-to-and-peek-definition.md#peek-definition) e [Exibir e editar o código usando a definição de Peek](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md).
- **Ir para definição** – navega para a origem de um tipo ou membro e abre o resultado em uma nova guia. <br>Consulte também: [ir para definição](../ide/go-to-and-peek-definition.md#go-to-definition).
- **Circundar com...** -Use trechos de código surround, que são adicionados em torno de um bloco de código selecionado. <br>Consulte também: [trechos de expansão e trechos surround](../ide/code-snippets.md#expansion-snippets-and-surround-with-snippets).
- **Inserir trecho** -insere um trecho de código no local do cursor.
- **Recortar** -auto-explicativo
- **Cópia** -auto-explicativa
- **Colar** -auto-explicativo
- **Estrutura de tópicos** – expandir e recolher seções de código. <br>Consulte também: [estrutura de tópicos](../ide/outlining.md).
- **Controle de origem** -exiba o histórico de contribuições de código para um repositório de código-fonte aberto.

### <a name="middle-pane-scroll-bar"></a>Painel central, barra de rolagem

A barra de rolagem pode fazer mais do que rolar pelo código. Você também pode usá-lo para abrir outro painel do editor de códigos. E você pode usar a barra de rolagem para ajudá-lo a codificar com mais eficiência Adicionando anotações a ele ou usando modos de exibição diferentes.

#### <a name="split-the-code-window"></a>Dividir a janela de código

Na barra de rolagem do editor de código, há um botão de **divisão** no canto superior direito. Ao escolher, você pode abrir outro painel do editor de código. Isso é útil porque eles operam independentemente um do outro, para que você possa usá-los para trabalhar em código em locais diferentes.

![O editor de código XAML, somente painel central, no Visual Studio](media/code-editor-split-window-button.png "Captura de tela do editor de código XAML, somente painel central, no Visual Studio 2019")

Para obter mais informações sobre como dividir uma janela do editor, consulte a página [gerenciar o editor do Windows](../ide/how-to-manage-editor-windows.md) .

#### <a name="use-annotations-or-map-mode"></a>Usar anotações ou modo de mapa

Você também pode alterar a aparência da barra de rolagem e quais recursos adicionais ela contém. Por exemplo, muitas pessoas gostam de incluir *anotações* na barra de rolagem, que fornecem indicações visuais, como alterações de código, pontos de interrupção, indicadores, erros e posição de cursor.

Outros apreciam o uso do *modo de mapa*, que exibe linhas de código em miniatura na barra de rolagem. Os desenvolvedores que têm muitos códigos em um arquivo podem descobrir que o modo de mapa rastreia para linhas de código com mais eficiência do que a barra de rolagem padrão.

Para obter mais informações sobre como alterar as configurações padrão da barra de rolagem, consulte a página [Personalizar a barra de rolagem](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md) .

## <a name="xaml-specific-features"></a>Recursos específicos do XAML

A maioria dos recursos a seguir está disponível universalmente no IDE do Visual Studio, mas há dimensões adicionadas a algumas delas que facilitam a codificação para desenvolvedores XAML.

### <a name="xaml-code-snippets"></a>Trechos de código XAML

Os trechos de código são pequenos blocos de código reutilizáveis que você pode inserir em um arquivo de código usando o comando de menu de contexto de clique com o botão direito do mouse **Inserir trecho** ou uma combinação de atalhos de teclado (**Ctrl** + **K**, **Ctrl** + **X**). Aprimoramos o [IntelliSense](../ide/using-intellisense.md) para que ele dê suporte à exibição de trechos de código XAML, que funcionam para trechos de código internos e quaisquer trechos de código personalizados que você adicionar manualmente. Alguns trechos de código XAML prontos para uso incluem,, `#region` , `Column definition` `Row definition` `Setter` e `Tag` .

![O editor de código XAML com opções de trecho de código XAML mostradas no IntelliSense](media/xaml-code-snippets.png "Captura de tela do editor de código XAML com opções de trecho de código XAML mostradas no IntelliSense")

Para obter mais informações, consulte as páginas [trechos de código](../ide/code-snippets.md) e [trechos de código C#](../ide/visual-csharp-code-snippets.md) .

### <a name="xaml-region-support"></a>Suporte a #region XAML

A partir do Visual Studio 2015, disponibilizamos #region suporte para desenvolvedores XAML no WPF e no UWP, e mais recentemente no [Xamarin. Forms](/xamarin/xamarin-forms/user-interface/text/editor/). No Visual Studio 2019, continuamos a fazer melhorias incrementais no suporte a #region. Por exemplo, na [versão 16,4](/visualstudio/releases/2019/release-notes-v16.4/) e posteriores, #region opções são mostradas conforme você começa a digitar `<!` .

![O editor de código XAML com #region opções mostradas no IntelliSense](media/code-editor-xaml-region.png "Captura de tela do editor de código XAML com #region opções exibidas no IntelliSense")

Você pode usar regiões quando desejar agrupar seções do código que você também deseja expandir ou recolher.

```xaml
    <!--#region NameOfRegion-->
    Your code is here
    <!--#endregion-->
```

Para obter mais informações sobre regiões, consulte a página [#region (referência C#)](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region/) . Para obter mais informações sobre como expandir e recolher seções de código, consulte a página de [estrutura de tópicos](../ide/outlining.md) .

### <a name="xaml-comments"></a>Comentários XAML

Os desenvolvedores geralmente preferem documentar seu código usando comentários. Você pode adicionar comentários ao código XAML que está na guia **MainWindow. XAML** das seguintes maneiras:

- Insira `<!--` antes de um comentário e depois adicione `-->` após o comentário.
- Insira `<!` e, em seguida, escolha `!--` na lista de opções.

  ![O editor de código XAML clique com o botão direito do mouse em adicionar comentários](media/xaml-code-editor-comments.png "Captura de tela do menu de contexto do clique com o botão direito do mouse para adicionar comentários no editor de código XAML")

- Selecione o código que você deseja envolver com um comentário e, em seguida, escolha o botão de **Comentário** na barra de ferramentas no IDE. Para reverter a ação, escolha o botão **Remover comentário** .

  ![O botão de comentário e o botão Remover comentário na barra de ferramentas do IDE](media/comment-undo-comment-buttons.png "Captura de tela do botão de comentário e o botão Remover comentário na barra de ferramentas do IDE")

- Selecione o código que você deseja envolver com um comentário e pressione **Ctrl** + **K**, **Ctrl** + **C**. Para remover o comentário do código selecionado, pressione **Ctrl** + **K**, **Ctrl** + **U**.

Para obter mais informações sobre como usar comentários no código C# que está na guia **MainWindow.XAML.cs** , consulte a página [comentários da documentação](/dotnet/csharp/language-reference/language-specification/documentation-comments/) .

### <a name="xaml-lightbulbs"></a>Lâmpadas XAML

Ícones de lâmpada que aparecem no código XAML fazem parte das [ações rápidas](../ide/quick-actions.md) que você pode usar para refatorar, gerar ou modificar o código.

Aqui estão alguns exemplos de como eles podem beneficiar sua experiência de codificação XAML:

- **Remover namespaces desnecessários**. No editor de código XAML, os namespaces desnecessários aparecem no texto esmaecido. Se você passar o cursor do mouse sobre um uso desnecessário, uma lâmpada será exibida. Ao escolher a opção **remover namespaces desnecessários** na lista suspensa, você verá uma visualização do que pode ser removida.

  ![A opção remover namespaces desnecessários do editor de código XAML da lâmpada de ações rápidas](media/xaml-code-editor-dimmed-namespaces-preview.png "Captura de tela da opção remover namespaces desnecessários do editor de código XAML que aparece usando a lâmpada de ações rápidas")

- **Renomear namespace**. Esse recurso, disponível no menu de contexto do clique com o botão direito do mouse depois de realçar um namespace, facilita a alteração de várias instâncias de uma configuração ao mesmo tempo. Você também pode acessar esse recurso usando a barra de menus, **Editar**  >  **refatoração**  >  **renomear**ou pressionando **Ctrl** + **r**e, em seguida, **Ctrl** + **r** novamente.

  ![A opção renomear namespace do editor de código XAML no menu de contexto de clique com o botão direito do mouse](media/code-editor-rename-namespace.png "Captura de tela da opção namespace de renomeação do editor de código XAML que aparece usando o menu de contexto de clique com o botão direito do mouse")

  Para obter mais informações, consulte a página [renomear um símbolo de código de refatoração](../ide/reference/rename.md) .

### <a name="conditional-xaml-for-uwp"></a>XAML condicional para UWP

A XAML condicional fornece uma forma de usar o método [ApiInformation.IsApiContractPresent](/uwp/api/windows.foundation.metadata.apiinformation.isapicontractpresent/) na marcação XAML. Com isso, você pode definir propriedades e instanciar objetos na marcação com base na presença de uma API sem a necessidade de usar code-behind.

Para obter mais informações, consulte a página [XAML condicional](/windows/uwp/debug-test-perf/conditional-xaml/) e os [controles XAML do UWP do host na página de aplicativos da área de trabalho (Ilhas XAML)](/windows/apps/desktop/modernize/xaml-islands/) .

### <a name="xaml-structure-visualizer"></a>Visualizador de estrutura XAML

O recurso Visualizador de estrutura no editor de código mostra as linhas de guia de estrutura, que são linhas tracejadas verticais que indicam elementos de marca abertos e fechados correspondentes em seu código. Essas linhas verticais facilitam a visualização de onde os blocos lógicos começam e terminam.

Para obter mais informações, consulte a página de [código de navegação](../ide/navigating-code.md) .

### <a name="intellicode-for-xaml"></a>IntelliCode para XAML

Quando você adiciona uma marca XAML ao seu código, normalmente começa com um colchete angular esquerdo `<` . Quando você digita esse colchete angular, um menu IntelliCode é exibido e lista várias das marcas XAML mais populares. Escolha aquela que você deseja adicionar rapidamente ao seu código.

Você pode reconhecer as seleções de IntelliCode porque elas aparecem na parte superior da lista e são estrelado.

![A lista de IntelliCode para o editor de texto XAML](media/xaml-intellicode-selection.png "Captura de tela da lista de IntelliCode para o editor de texto XAML")

Para obter mais informações, consulte a [visão geral da página IntelliCode](/visualstudio/intellicode/overview/) .

### <a name="settings"></a>Configurações

Para obter mais informações sobre *todas* as configurações no IDE do Visual Studio, consulte os [recursos da página Editor de código](../ide/writing-code-in-the-code-and-text-editor.md) .

## <a name="xaml-optional-settings"></a>Configurações opcionais XAML

Você pode usar a caixa de diálogo [Opções](../ide/reference/options-dialog-box-visual-studio.md) para alterar as configurações padrão do editor de código XAML. Para exibir as configurações, escolha **ferramentas**  >  **Opções**  >  **Editor de texto**  >  **XAML**.

![A lista de opções para o editor de texto XAML](media/xaml-tools-options.png "Captura de tela da lista de opções para o editor de texto XAML")

> [!NOTE]
> Você também pode usar atalhos de teclado para acessar a caixa de diálogo opções. Veja como: pressione **Ctrl** + **Q** para pesquisar o IDE, digite **Options**e pressione **Enter**. Em seguida, **pressione CTRL** + **E** para pesquisar a caixa de diálogo opções, digite **Editor de texto**, pressione **Enter**, digite **XAML**e pressione **Enter**.
>  
> Para obter mais informações sobre atalhos de teclado, consulte a página [dicas de atalho para o Visual Studio](../ide/productivity-shortcuts.md#code-editor) .

### <a name="universal-text-editor-options"></a>Opções do editor de texto universal

Na caixa de diálogo [Opções](../ide/reference/options-text-editor-xaml-formatting.md) para XAML, os três primeiros itens a seguir são universais para todas as linguagens de programação às quais o IDE do Visual Studio dá suporte. Visite as informações vinculadas na tabela a seguir para saber mais sobre essas opções e como usá-las.

|Nome  |Obter mais informações  |
|---------|---------|
|Geral  | [Caixa de diálogo opções: editor de texto > todos os idiomas](../ide/reference/options-text-editor-all-languages.md) |
|Barras de rolagem | [Opções, Editor de Texto, Todas as Linguagens, Barras de Rolagem](../ide/reference/options-text-editor-all-languages-scroll-bars.md) |
|Tabulações  |  [Opções, Editor de Texto, Todas as Linguagens, Guias](../ide/reference/options-text-editor-all-languages-tabs.md) |

### <a name="xaml-specific-text-editor-options"></a>Opções do editor de texto específico para XAML

A tabela a seguir lista as configurações na caixa de diálogo [Opções](../ide/reference/options-text-editor-xaml-formatting.md) que podem aprimorar sua experiência de edição quando você desenvolve aplicativos baseados em XAML. Visite as informações vinculadas para saber mais sobre essas opções e como usá-las.

|Nome  |Obter mais informações  |
|---------|---------|
|Formatação | [Opções, Editor de Texto, XAML, Formatação](../ide/reference/options-text-editor-xaml-formatting.md) |
|Diversos |  [Opções, Editor de texto, XAML, Diversos](../ide/reference/options-text-editor-xaml-miscellaneous.md) |

> [!TIP]
> A configuração de **nome do método do manipulador de eventos de capitalização** na seção **diversos** é especialmente útil para os desenvolvedores XAML. Essa configuração está *desativada* por padrão porque é nova, mas sugerimos que você a defina como *ativada* para dar suporte a maiúsculas e minúsculas no seu código.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre como editar seu código em tempo real enquanto você estiver executando seu aplicativo no modo de depuração, consulte a página de [Hot recarregamento de XAML](xaml-hot-reload.md) .

## <a name="see-also"></a>Veja também

- [Recursos do editor de código do Visual Studio](../ide/writing-code-in-the-code-and-text-editor.md)
- [XAML em aplicativos UWP](/windows/uwp/xaml-platform/xaml-overview/)
- [XAML em aplicativos do Xamarin.Forms](/xamarin/xamarin-forms/xaml/)
- [Desenvolvimento de aplicativo móvel Xamarin (Mac)](/visualstudio/mac/xamarin/)
- [Visual Studio 2019 para Mac-Tour do IDE (Mac)](/visualstudio/mac/ide-tour/)
