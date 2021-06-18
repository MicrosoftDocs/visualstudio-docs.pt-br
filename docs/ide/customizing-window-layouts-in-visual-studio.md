---
title: Personalizar layouts de janela
description: Saiba como personalizar as características que o Windows exibe para criar layouts que funcionam melhor para vários fluxos de trabalho de desenvolvimento.
ms.custom: SEO-VS-2020
ms.date: 03/02/2021
ms.topic: conceptual
f1_keywords:
- vs.windows
- vs.environment
helpviewer_keywords:
- windows [Visual Studio], managing
- custom window configurations
- layout [Visual Studio], window management
- document windows [Visual Studio]
- interface modes
- AutoHide windows
- MDI, window interface modes
- multiple monitors
- Tabbed Document mode
- debug mode
- custom layouts
ms.assetid: 7517ff13-76de-4ecf-9c1b-eb9b7ff4d718
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: be11db364d0505833e722d3db308b41a18ccbb9d
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308123"
---
# <a name="customize-window-layouts-in-visual-studio"></a>Personalizar layouts de janela no Visual Studio

No Visual Studio, é possível personalizar a posição, tamanho e comportamento de janelas para criar layouts de janela que funcionam melhor para vários fluxos de trabalho de desenvolvimento. Quando você personaliza o layout, o IDE se lembra dele. Por exemplo, se você alterar o local de encaixe do **Gerenciador de Soluções** e fechar o Visual Studio, na próxima vez que o abrir, mesmo que estiver trabalhando em outro computador, o **Gerenciador de Soluções** estará encaixado no mesmo local.

Também é possível dar um nome ao layout personalizado e salvá-lo e, em seguida, mudar entre layouts com um único comando. Por exemplo, você pode criar um layout para edição e um layout para depuração e alternar entre eles usando o comando de menu Aplicar  >  **Janela** Layout da Janela.

## <a name="tool-and-document-windows"></a>Janelas de ferramentas e do documento

O IDE tem dois tipos básicos de janela, *janelas de ferramentas* e *janelas do documento*. As janelas **de ferramentas Gerenciador de Soluções**, **Gerenciador de Servidores**, Janela de Saída **,** Lista de Erros , os designers, as janelas do depurador e assim por diante.  As janelas do documento contêm arquivos de código-fonte, arquivos de texto arbitrário, arquivos de configuração e assim por diante. As janelas de ferramentas podem ser redimensionadas e arrastadas por sua barra de título. As janelas de documentos podem ser arrastadas por sua guia. Clique com o botão direito do mouse na guia ou na barra de título para definir outras opções na janela.

O menu **Janela** mostra opções para encaixar, flutuante e ocultar janelas no IDE. Clique com o botão direito do mouse na guia de janela ou na barra de título para ver outras opções para essa janela específica. É possível exibir mais de uma instância de determinadas janelas de ferramentas por vez. Por exemplo, é possível exibir mais de uma janela do navegador da Web e é possível criar outras instâncias de algumas janelas de ferramentas escolhendo **Nova Janela** no menu **Janela**.

### <a name="split-windows"></a>Dividir janelas

Quando é necessário exibir ou editar dois locais ao mesmo tempo em um documento, é possível dividir as janelas. Para dividir seu documento em duas seções de rolagem independente, clique em **Dividir** no menu **Janela**. Clique em **Remover Divisão** no menu **Janela** para restaurar o modo de exibição único.

### <a name="tabs"></a>Guias

Você pode usar guias para organizar seu layout de várias maneiras diferentes. Por exemplo, você pode exibir uma visualização de um arquivo no editor sem abrir o arquivo, agrupar suas guias e muito mais.

#### <a name="preview-tab-document-windows"></a>Guia Visualização (janelas do documento)

Na guia **Visualização,** você pode exibir arquivos no editor sem abri-los. Você pode visualizar arquivos escolhendo-os no Gerenciador de Soluções **,** durante a depuração quando você entra em arquivos, com Ir para Definição **e** quando navega pelos resultados de uma pesquisa. Os arquivos de visualização são exibidos em uma guia à direita da caixa de guias de documentos. O arquivo será aberto para edição se você modificá-lo ou escolher **Abrir**.

::: moniker range=">=vs-2019"

#### <a name="vertical-document-tabs"></a>Guias verticais do documento

Novidade na versão **[16.4:](/visualstudio/releases/2019/release-notes-v16.4/)** adicionamos uma das principais solicitações de [recursos,](https://developercommunity.visualstudio.com/idea/467369/vertical-group-tab.html)guias verticais de documento, na versão Visual Studio 2019 versão 16.4. Agora, você pode gerenciar suas guias de documento em uma lista vertical no lado esquerdo ou direito do editor.

Você pode aplicar guias verticais de documento das seguintes maneiras:

- Escolha **Ferramentas**  >  **Opções**  >  **Guias de** Ambiente e  >  **Janelas** na barra de menus. Em seguida, no **controle de layout** da guia Definir, escolha **Superior,** **Esquerda** ou **Direita** na lista lista listada.

- Clique com o botão direito do mouse em uma guia, **escolha Definir Layout** da Guia e escolha **Esquerda** ou **Direita.** (Para retornar as guias para sua posição padrão, escolha **Top**.)

    :::image type="content" source="./media/vs-2019/vertical-tabs.gif" alt-text="Uma animação que mostra guias verticais do documento em ação":::

::: moniker-end

#### <a name="tab-groups"></a>Grupos de guias

Os grupos de guias estendem sua capacidade de gerenciar o workspace limitado enquanto você está trabalhando com dois ou mais documentos abertos no IDE. É possível organizar várias janelas do documento e de ferramentas em grupos de guias verticais ou horizontais e embaralhar os documentos de um grupo de guias em outro.

### <a name="toolbars"></a>Barras de ferramentas

Você pode organizar barras de ferramentas arrastando-as para onde quiser ou usando a **caixa de** diálogo Personalizar. Para obter mais informações sobre como posicionar e personalizar barras de ferramentas, consulte [Como personalizar menus e barras de ferramentas](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md).

## <a name="arrange-and-dock-windows"></a>Organizar e encaixar janelas

Uma janela de documento ou janela de ferramentas pode *ser* encaixada, de modo que ela tenha uma posição e um tamanho dentro do quadro de janela do IDE. Você também pode posicioná-lo como uma janela flutuante separada que está fora do IDE.

Você pode encaixar uma janela de ferramentas em qualquer lugar dentro do quadro do IDE. Você também pode encaixar algumas janelas de ferramentas como janelas com guias no quadro do editor. Além disso, você pode encaixar janelas de documentos no quadro do editor e fixá-las na posição atual na ordem de tabulação.

Você também pode encaixar várias janelas para flutuar juntas em *uma área de* trabalho ou fora do IDE. As janelas de ferramentas também podem ser ocultadas ou minimizadas.

É possível organizar janelas das seguintes maneiras:

- Fixe as janelas do documento à esquerda da caixa de guias.

- Encaixe janelas de guias no quadro de edição.

- Encaixe janelas de ferramentas na borda de um quadro no IDE.

- Faça janelas do documento ou de ferramentas flutuar no IDE ou fora dele.

- Oculte as janelas de ferramentas ao longo da borda do IDE.

- Exiba janelas em monitores diferentes.

- Redefina o posicionamento da janela para o layout padrão ou para um layout personalizado salvo.

Para organizar janelas de ferramentas e documentos, você pode colocar o cursor na barra de título de uma janela e, em seguida, arrastá-lo para onde você deseja. Como alternativa, você pode clicar com o botão direito do mouse na barra de título da janela para usar seu menu de contexto ou pode usar os comandos no menu **Janela.**

### <a name="dock-windows"></a>Encaixar janelas

Quando você clica e arrasta a barra de título de uma janela de ferramentas ou a guia da janela do documento, um losango do guia é exibido. Durante a operação de arrastar, quando o cursor do mouse está sobre uma das setas no losango, será exibida uma área sombreada que mostra onde a janela será encaixada se você soltar o botão do mouse no momento.

Para mover uma janela encaixável sem ajustá-la no local, pressione a tecla **Ctrl** enquanto você arrasta a janela.

Para retornar uma janela de ferramentas ou uma janela de documento para seu local encaixado mais recente, pressione **Ctrl** enquanto clica duas vezes na barra de título ou na guia da janela.

A ilustração a seguir mostra o losango do guia para janelas de documentos, que só podem ser encaixadas dentro do quadro de edição:

![Losango do guia da janela do documento](../ide/media/documentwindowguidediamonds.png)

As janelas de ferramentas podem ser fixadas em um lado de um quadro no IDE ou dentro do quadro de edição. Um guia do losango será exibido quando você arrastar uma janela de ferramentas para outro lugar para ajudá-lo a reencaixar a janela facilmente.

![Losangos do guia da janela de ferramentas](../ide/media/vs10guidediamond.png)

A ilustração a seguir mostra o **Gerenciador de Soluções** que está sendo encaixado em um novo local que é delimitado pela área sombreada azul:

![Encaixando o Gerenciador de Soluções em uma nova posição](../ide/media/vs2015_dock_diamond.png)

### <a name="close-and-auto-hide-tool-windows"></a>Fechar e ocultar automaticamente janelas de ferramentas

Você pode fechar uma janela de ferramentas clicando no **X** no canto superior direito da barra de título. Para reabrir a janela, use o respectivo atalho de teclado ou comando de menu. As janelas de ferramentas suportam um recurso chamado *ocultar* automaticamente , o que faz com que uma janela deslize para fora do caminho quando você usa uma janela diferente. Quando uma janela é ocultada automaticamente, o nome dela é exibido em uma guia na borda do IDE. Para usar a janela novamente, aponte para a guia para que a janela volte a ser exibida.

![Ocultar automaticamente](../ide/media/vs2015_auto_hide.png)

> [!NOTE]
> Para definir se a ocultação automática opera em janelas de ferramentas individualmente ou como grupos encaixados, selecionar ou limpar Ocultar Automaticamente botão afeta apenas as **janelas** de ferramentas ativas na **caixa de** diálogo Opções. Para obter mais informações, consulte [Geral, Ambiente, Caixa de diálogo Opções](../ide/reference/general-environment-options-dialog-box.md).

> [!NOTE]
> As janelas de ferramentas que têm ocultar automaticamente habilitado poderão ser exibidas temporariamente quando a janela estiver em foco. Para ocultar a janela novamente, selecione um item fora da janela atual. Quando a janela perde o foco, ela não é mais exibida.

### <a name="use-a-second-monitor"></a>Usar um segundo monitor

Se você tiver um segundo monitor e seu sistema operacional der suporte a ele, será possível escolher qual monitor exibirá uma janela. Você pode até mesmo agrupar várias *janelas em remos* em outros monitores.

> [!TIP]
> É possível criar várias instâncias do **Gerenciador de Soluções** e movê-las para outro monitor. Clique com o botão direito do mouse na janela e escolha **Novo Modo de Exibição do Gerenciador de Soluções**. Você pode retornar todas as janelas de volta para o monitor original clicando duas vezes ao escolher a **tecla Ctrl.**

### <a name="reset-name-and-switch-between-window-layouts"></a>Redefinir, nomear e mudar entre layouts de janela

É possível voltar o IDE para o layout de janela original para sua coleção de configurações usando o comando **Redefinir Layout de Janela**. Quando você executar esse comando, as seguintes ações ocorrerão:

- Todas as janelas serão movidas para as posições padrão.

- As janelas fechadas no layout de janela padrão serão fechadas.

- As janelas abertas no layout de janela padrão serão abertas.

### <a name="create-and-save-custom-layouts"></a>Criar e salvar layouts personalizados

O Visual Studio permite salvar até 10 layouts de janela personalizados e mudar rapidamente entre eles. As etapas a seguir mostram como criar, salvar, invocar e gerenciar layouts personalizados que usam vários monitores com janelas de ferramentas encaixadas e flutuantes.

Primeiro, crie uma solução de teste que tem dois projetos, cada um com um layout ideal diferente.

#### <a name="create-a-ui-project-and-customize-the-layout"></a>Criar um projeto de interface do usuário e personalizar o layout

::: moniker range="vs-2017"

1. Crie um projeto de **Aplicativo do WPF** do C#. Imagine que, neste projeto, você vai estar desenvolvendo uma interface do usuário. Você deseja maximizar o espaço da janela de designer e tirar outras janelas de ferramentas do caminho.

::: moniker-end

::: moniker range=">=vs-2019"

1. Crie um novo projeto de aplicativo **WPF em** C#. Imagine que, neste projeto, você vai estar desenvolvendo uma interface do usuário. Você deseja maximizar o espaço da janela de designer e tirar outras janelas de ferramentas do caminho.

::: moniker-end

2. Se você tiver vários monitores, escareça a janela **Gerenciador de Soluções** e a **janela** Propriedades para o segundo monitor. Em um sistema de monitor único, tente fechar todas as janelas exceto o designer.

3. Pressione **Ctrl** + **Alt** + **X para** exibir a janela Caixa **de** Ferramentas. Se a janela estiver encaixada, arraste-a para que ela flutue em algum lugar que você gostaria de posicioná-la.

4. Pressione **F5** para colocar o Visual Studio em modo de depuração. Ajuste a posição das **janelas Autos,** **Pilha de Chamada** e Depuração de Saída da maneira que você deseja.  O layout que você está prestes a criar será aplicado ao modo de edição e ao modo de depuração.

5. Quando os layouts no modo de depuração e no modo de edição são como você deseja, escolha **Janela**  >  **Salvar Layout da Janela**. Chame esse layout de "Designer".

     Observe que o novo layout recebe o próximo atalho de teclado da lista reservada **ctrl** + **Alt** + **1...0**.

#### <a name="create-a-database-project-and-layout"></a>Criar um layout e um projeto de banco de dados

1. Adicione um novo projeto de **Banco de Dados do SQL Server** à solução.

2. Clique com o botão direito do mouse no novo projeto **no Gerenciador de Soluções** e escolha Exibir **no Pesquisador de Objetos**. Isso exibe a janela **Gerenciador de Objetos do SQL Server**, que permite acessar tabelas, modos de exibição e outros objetos em seu banco de dados. É possível fazer essa janela flutuar ou deixá-la encaixada. Ajuste as outras janelas de ferramentas da maneira como você as desejar. Para obter maior realismo, é possível adicionar um banco de dados real, mas isso não é necessário para esse passo a passo.

3. Quando o layout for como você deseja, no menu principal, escolha **Janela Salvar** Layout  >  **da Janela**. Chame esse layout de “Projeto de Banco de Dados”. (Não nos preocuparemos com um layout de modo de depuração para este projeto.)

#### <a name="switch-between-the-layouts"></a>Mudar entre os layouts

Para alternar entre layouts, use os atalhos de teclado ou, no menu principal, **escolha Janela Aplicar** Layout da  >  **Janela**.

![Aplicar menu de layout de janela](../ide/media/vs2015_applywindowlayout.png)

Depois de aplicar o layout da interface do usuário, observe como ele é preservado tanto no modo de edição quanto no modo de depuração.

Se você tiver vários monitores no trabalho e um laptop de um só monitor em casa, será possível criar layouts otimizados para cada computador.

> [!NOTE]
> Se você aplicar um layout de vários monitor em um sistema de monitor único, as janelas flutuantes inseridas no segundo monitor ficarão ocultas agora atrás da janela do Visual Studio. Você pode trazer essas janelas para a frente pressionando **Alt + Tab**. Se você abrir o Visual Studio com vários monitores, poderá restaurar as janelas para suas posições especificadas aplicando o layout.

#### <a name="manage-and-roam-your-layouts"></a>Gerenciar e usar perfil móvel nos seus layouts

Você pode remover, renomear ou reordenar seu layout personalizado escolhendo **Janela**  >  **Gerenciar Layouts de Janela .** Se você mover um layout, a associação de teclas será ajustada automaticamente para refletir a nova posição na lista. As vinculações não podem ser modificadas de outra forma e, portanto, você pode armazenar um máximo de 10 layouts por vez.

![Gerenciar layouts de janelas](../ide/media/managewindowlayouts.png)

Para se lembrar qual atalho de teclado é atribuído a qual layout, escolha **Janela Aplicar** Layout  >  **da Janela**.

Esses layouts usam perfis móveis automaticamente entre edições do Visual Studio e também entre instâncias do Blend em computadores separados e de qualquer edição Express para qualquer outra organização Express. No entanto, os layouts não se Visual Studio, Blend e Express.

## <a name="see-also"></a>Confira também

- [Como mover-se no IDE](../ide/how-to-move-around-in-the-visual-studio-ide.md)
