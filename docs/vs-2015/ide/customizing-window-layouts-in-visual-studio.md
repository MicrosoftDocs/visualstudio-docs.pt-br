---
title: Personalizando layouts de janela no Visual Studio | Microsoft Docs
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
caps.latest.revision: 30
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: f1702a2b25bd0489814473f3ae2fc0073dab8497
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49911625"
---
# <a name="customizing-window-layouts-in-visual-studio"></a>Personalização de layouts de janela no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Visual Studio, é possível personalizar a posição, tamanho e comportamento de janelas para criar layouts de janela que funcionam melhor para vários fluxos de trabalho de desenvolvimento. Quando você personaliza o layout, o IDE se lembra dele. Por exemplo, se você alterar o local de encaixe do **Gerenciador de Soluções** e fechar o Visual Studio, na próxima vez que o iniciar, mesmo que estiver trabalhando em outro computador, o **Gerenciador de Soluções** será encaixado no mesmo local. Também é possível dar um nome ao layout personalizado e salvá-lo e, em seguida, mudar entre layouts com um único comando. Por exemplo, é possível criar um layout para edição e outro para depuração e mudar entre eles usando o comando de menu **Janela &#124; Aplicar Layout de Janela**.  
  
## <a name="kinds-of-windows"></a>Tipos de janelas  
  
### <a name="tool-and-document-windows"></a>Ferramenta e o Windows de documento  
 O IDE tem dois tipos básicos de janela, *janelas de ferramentas* e *janelas do documento*. As janelas de ferramentas incluem o Gerenciador de Soluções, Gerenciador de Servidores, Janela de Saída, Lista de Erros, os designers, as janelas do depurador e assim por diante. As janelas do documento contêm arquivos de código-fonte, arquivos de texto arbitrário, arquivos de configuração e assim por diante. As janelas de ferramentas podem ser redimensionadas e arrastadas por sua barra de título. As janelas do documento podem ser arrastadas por sua guia. Clique com o botão direito do mouse na guia ou barra de título para definir outras opções na janela.  
  
 O menu **Janela** mostra opções para encaixar, flutuar e ocultar janelas no IDE. Clique com o botão direito do mouse na guia de janela ou na barra de título para ver outras opções para essa janela específica. É possível exibir mais de uma instância de determinadas janelas de ferramentas por vez. Por exemplo, é possível exibir mais de uma janela do navegador da Web e é possível criar outras instâncias de algumas janelas de ferramentas escolhendo **Nova Janela** no menu **Janela**.  
  
### <a name="preview-tab-document-windows"></a>Guia Visualização (janelas do documento)  
 Na guia Visualização, é possível exibir arquivos no editor sem abri-los. É possível visualizar arquivos escolhendo-os no **Gerenciador de Soluções**, durante a depuração quando você intervém nos arquivos, com Ir para Definição e quando você navega pelos resultados de uma pesquisa. Os arquivos de visualização são exibidos em uma guia à direita da caixa de guias de documentos. O arquivo será aberto para edição se você modificá-lo ou escolher **Abrir**.  
  
### <a name="tab-groups"></a>Grupos de guias  
 Os grupos de guias ampliam sua capacidade de gerenciar o workspace limitado ao trabalhar com dois ou mais documentos abertos no IDE. É possível organizar várias janelas do documento e de ferramentas em grupos de guias verticais ou horizontais e embaralhar os documentos de um grupo de guias em outro.  
  
### <a name="split-windows"></a>Divisão do Windows  
 Quando é necessário exibir ou editar dois locais ao mesmo tempo em um documento, é possível dividir as janelas. Para dividir seu documento em duas seções de rolagem independente, clique em **Dividir** no menu **Janela**. Clique em **Remover Divisão** no menu **Janela** para restaurar o modo de exibição único.  
  
### <a name="toolbars"></a>Barras de ferramentas  
 As barras de ferramentas podem ser organizadas arrastando ou usando a caixa de diálogo **Personalizar**. Para obter mais informações sobre como posicionar e personalizar barras de ferramentas, consulte [How to: Customize Menus and Toolbars (Como: personalizar menus e barras de ferramentas)](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md).  
  
## <a name="arranging-and-docking-windows"></a>Organizando e encaixe Windows  
 As duas janelas do documento e de ferramentas podem ser *encaixadas* para que elas tenham uma posição e um tamanho dentro do quadro de janela do IDE ou flutuando como uma janela separada independente do IDE. As janelas de ferramentas podem ser encaixadas em qualquer lugar dentro do quadro do IDE; algumas janelas de ferramentas podem ser encaixadas como janelas com guias no quadro do editor. As janelas do documento podem ser encaixadas dentro do quadro do editor e podem ser fixadas em sua posição atual na ordem de tabulação. É possível encaixar várias janelas para que elas flutuem juntas em um “raft” no IDE ou fora dele. As janelas de ferramentas também podem ser ocultadas ou minimizadas.  
  
 É possível organizar janelas das seguintes maneiras:  
  
- Fixe as janelas do documento à esquerda da caixa de guias.  
  
- Encaixe janelas de guias no quadro de edição.  
  
- Encaixe janelas de ferramentas na borda de um quadro no IDE.  
  
- Faça janelas do documento ou de ferramentas flutuar no IDE ou fora dele.  
  
- Oculte as janelas de ferramentas ao longo da borda do IDE.  
  
- Exiba janelas em monitores diferentes.  
  
- Redefina o posicionamento da janela para o layout padrão ou para um layout personalizado salvo.  
  
  As janelas de ferramentas e do documento podem ser organizadas arrastando-as, usando comandos no menu **Janela** e clicando com o botão direito do mouse na barra de título da janela a ser organizada.  
  
> [!NOTE]
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).  
  
### <a name="docking-windows"></a>Encaixe o Windows  
 Quando você clica e arrasta a barra de título de uma janela de ferramentas ou a guia da janela do documento, um losango do guia é exibido. Durante a operação de arrastar, quando o cursor do mouse está sobre uma das setas no losango, será exibida uma área sombreada que mostra onde a janela será encaixada se você soltar o botão do mouse no momento.  
  
 Para mover uma janela encaixável sem ajustá-la no local, escolha a tecla Ctrl enquanto você arrasta a janela.  
  
 Para retornar uma janela do documento ou de ferramentas para seu local encaixado mais recente, pressione **CTRL** enquanto você clica duas vezes na barra de título ou na guia da janela.  
  
 A ilustração a seguir mostra o losango do guia para janelas de documentos, que só podem ser encaixadas dentro do quadro de edição:  
  
 ![Losango do guia da janela do documento](../ide/media/documentwindowguidediamonds.png "Documentwindowguidediamonds")  
  
 As janelas de ferramentas podem ser fixadas em um lado de um quadro no IDE ou dentro do quadro de edição. Um guia do losango será exibido quando você arrastar uma janela de ferramentas para outro lugar para ajudá-lo a reencaixar a janela facilmente.  
  
 Losango do guia para janelas de ferramentas  
  
 ![Losangos do guia da janela de ferramentas](../ide/media/vs10guidediamond.png "VS10GuideDiamond")  
  
 A ilustração a seguir mostra o Gerenciador de Soluções que está sendo encaixado em um novo local, mostrado pela área sombreada azul:  
  
 ![Gerenciador de soluções em uma nova posição de encaixe](../ide/media/vs2015-dock-diamond.png "VS2015_Dock_diamond")  
  
### <a name="closing-and-auto-hiding-tool-windows"></a>Fechando e ocultar automaticamente janelas de ferramentas  
 É possível fechar uma janela de ferramentas clicando no X na parte superior da barra de título; para reabrir a janela, use seu atalho de teclado ou o comando de menu. As janelas de ferramentas dão suporte a um recurso denominado Ocultar Automaticamente, o que faz com que uma janela saia da frente quando você usa uma janela diferente. Quando uma janela é ocultada automaticamente, o nome dela é exibido em uma guia na borda do IDE. Para usar a janela novamente, aponte para a guia para que a janela volte a ser exibida.  
  
 ![Ocultar automaticamente](../ide/media/vs2015-auto-hide.png "vs2015_auto_hide")  
  
> [!NOTE]
>  Para definir se o Ocultar Automaticamente é operado nas janelas de ferramentas individualmente ou como grupos encaixados, selecione ou desmarque **O botão Ocultar Automaticamente afeta somente janelas de ferramentas ativas** na caixa de diálogo **Opções**. Para obter mais informações, consulte [Geral, Ambiente, Caixa de diálogo Opções](../ide/reference/general-environment-options-dialog-box.md).  
  
> [!NOTE]
>  As janelas de ferramentas que têm Ocultar Automaticamente habilitado poderão ser exibidas temporariamente quando a janela estiver em foco. Para ocultar a janela novamente, selecione um item fora da janela atual. Quando a janela perde o foco, ela não é mais exibida.  
  
### <a name="specifying-a-monitor"></a>Especificando um Monitor  
 Se você tiver um segundo monitor e seu sistema operacional der suporte a ele, será possível escolher qual monitor exibirá uma janela. É possível até mesmo agrupar várias janelas em “rafts” em outros monitores.  
  
> [!TIP]
>  É possível criar várias instâncias do **Gerenciador de Soluções** e movê-las para outro monitor. Clique com o botão direito do mouse na janela e escolha **Novo Modo de Exibição do Gerenciador de Soluções**. É possível voltar todas as janelas para o monitor original clicando duas vezes enquanto pressiona a tecla Ctrl.  
  
### <a name="reset-name-and-switch-between-window-layouts"></a>Redefinir, nomear e mudar entre layouts de janela  
 É possível voltar o IDE para o layout de janela original para sua coleção de configurações usando o comando **Redefinir Layout de Janela**. Quando você executar esse comando, as seguintes ações ocorrerão:  
  
-   Todas as janelas serão movidas para as posições padrão.  
  
-   As janelas fechadas no layout de janela padrão serão fechadas.  
  
-   As janelas abertas no layout de janela padrão serão abertas.  
  
### <a name="create-and-save-custom-layouts"></a>Criar e salvar layouts personalizados  
 Visual Studio 2015 permite que você salvar até 10 layouts de janela personalizados e alternar rapidamente entre elas. As etapas a seguir mostram como criar, salvar, invocar e gerenciar layouts personalizados que usam vários monitores com janelas de ferramentas encaixadas e flutuantes.  
  
 Primeiro, crie uma solução de teste que tem dois projetos, cada um com um layout ideal diferente.  
  
##### <a name="create-a-ui-project-and-customize-the-layout"></a>Criar um projeto de interface do usuário e personalizar o layout  
  
1.  Na caixa de diálogo **Novo Projeto**, crie um Aplicativo de Área de Trabalho WPF em Visual C#. Suponhamos que esse é o projeto em que trabalharemos na interface do usuário. Portanto, queremos maximizar o espaço da janela de designer e tirar outras janelas de ferramenta do caminho.  
  
2.  Se você tiver vários monitores, leve a janela **Gerenciador de Soluções** e o janela **Propriedades** sobre o segundo monitor. Em um sistema de monitor único, tente fechar todas as janelas exceto o designer.  
  
3.  Pressione **Ctrl + Alt + X** para exibir a caixa de ferramentas. Se a janela estiver encaixada, arraste-a para que ela flutue em algum lugar que você gostaria de posicioná-la em qualquer monitor.  
  
4.  Pressione F5 para colocar o Visual Studio em modo de depuração. Ajuste a posição das janelas de depuração Carros, Pilha de Chamadas e Saída da maneira como você as desejar. O layout que você está prestes a criar será aplicado ao modo de edição e ao modo de depuração.  
  
5.  Quando seus layouts no modo de depuração e de edição estiverem da maneira como você os deseja, no menu principal, escolha **Janela > Salvar Layout de Janela**. Chame esse layout de "Designer."  
  
     Observe que o próximo atalho de teclado da lista reservada de Ctrl + Alt + 1...0 foi atribuído ao seu novo layout.  
  
##### <a name="create-a-database-project-and-layout"></a>Criar um layout e um projeto de banco de dados  
  
1.  Adicione um novo projeto de **Banco de Dados do SQL Server** à solução.  
  
2.  Clique com o botão direito do mouse no novo projeto no Gerenciador de Soluções e escolha **Exibir no Gerenciador de Objetos**. Isso exibe a janela **Gerenciador de Objetos do SQL Server**, que permite acessar tabelas, modos de exibição e outros objetos em seu banco de dados. É possível fazer essa janela flutuar ou deixá-la encaixada. Ajuste as outras janelas de ferramentas da maneira como você as desejar. Para obter maior realismo, é possível adicionar um banco de dados real, mas não é necessário para esse passo a passo.  
  
3.  Quando o layout estiver da maneira como você deseja, no menu principal, escolha **Janela > Salvar Layout de Janela**. Chame esse layout de "Projeto de Banco de Dados." (Não nos preocuparemos com um layout de modo de depuração para este projeto.)  
  
##### <a name="switch-between-the-layouts"></a>Mudar entre os layouts  
  
1.  Para mudar entre layouts, use os atalhos de teclado ou, no menu principal, escolha **Janela > Aplicar Layout de Janela**.  
  
     ![Aplicar menu de layout de janela](../ide/media/vs2015-applywindowlayout.png "VS2015_ApplyWindowLayout")  
  
     Depois de aplicar o layout da interface do usuário, observe como ele é preservado tanto no modo de edição quanto no modo de depuração.  
  
     Se você tiver vários monitores no trabalho e um laptop de um só monitor em casa, será possível criar layouts otimizados para cada computador.  
  
     Observação: se você aplicar um layout de vários monitor em um sistema de monitor único, as janelas flutuantes inseridas no segundo monitor ficarão ocultas agora atrás da janela do Visual Studio. É possível trazer essas janelas para frente pressionando Alt + Tab. Se você abrir o Visual Studio posteriormente com vários monitores, será possível restaurar as janelas para suas posições especificadas reaplicando o layout.  
  
##### <a name="manage-and-roam-your-layouts"></a>Gerenciar e usar perfil móvel nos seus layouts  
  
1.  É possível remover, renomear ou reordenar seu layout personalizado escolhendo **Janela > Gerenciar Layouts de Janela**. Se você mover um layout, a associação de teclas será ajustada automaticamente para refletir a nova posição na lista. Do contrário, as associações não poderão ser modificadas e, assim, será possível armazenar, no máximo, 10 layouts por vez.  
  
     ![Gerenciar layouts de janela](../ide/media/managewindowlayouts.png "ManageWindowLayouts")  
  
     Para se lembrar de qual atalho de teclado foi atribuído a qual layout, escolha **Janela > Aplicar Layout de Janela**.  
  
     Esses layouts usam perfis móveis automaticamente entre edições do Visual Studio e também entre instâncias do Blend em computadores separados e de qualquer edição Express para qualquer outra organização Express. No entanto, os layouts não usam perfis móveis entre o Visual Studio, o Blend e o Express.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Tipos de Janelas](../misc/kinds-of-windows.md)|Aborda as diferenças entre janelas de ferramenta e janelas de documento no IDE.|  
|[Como organizar e encaixar janelas](../misc/how-to-arrange-and-dock-windows.md)|Descreve como encaixar, ocultar automaticamente e colocar lado a lado as janelas, além de como redefinir o layout da janela.|  
|[How to: Move Around in the IDE (Como mover-se no IDE)](../ide/how-to-move-around-in-the-visual-studio-ide.md)|Descreve como você pode alternar entre as janelas abertas no IDE, por ordem de uso. Também descreve como é possível pular para documentos específicos.|  
|[Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3)|Contém informações sobre combinações de configurações e como as configurações afetam os layouts da janela, os atalhos do teclado e outros elementos no IDE.|



