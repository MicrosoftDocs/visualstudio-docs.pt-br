---
title: Comandos de navegação de código
ms.date: 08/14/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code editor, navigation
- code editor, go to
- code editor, go to definition
- code editor, go to line
- code editor, peek definition
- code editor, navigation bar
- go to definition
- peek definition
- go to line
- go to
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6ac6fb3ae1f8c4e7fb48c9cd9a0d2b77cb875094
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49894463"
---
# <a name="navigate-code"></a>Navegue pelos códigos

O Visual Studio fornece várias maneiras de navegar no código usando o editor. Este tópico resume as diferentes maneiras de navegar no código e fornece links para tópicos com mais detalhes.

## <a name="navigate-backward-and-navigate-forward-commands"></a>Comandos Navegar para trás e Navegar para frente

Você pode usar os botões **Navegar para Trás** (**Ctrl**+**-**) e **Navegar para Frente** (**Ctrl**+**Shift**+**-**) na barra de ferramentas para mover o ponto de inserção para locais anteriores ou para retornar para um local mais recente do que um local anterior. Esses botões retém os últimos 20 locais do ponto de inserção. Esses comandos também estão disponíveis no menu **Exibir**, em **Navegar para Trás** e **Navegar para Frente**.

![Botões de navegação para frente e para trás](../ide/media/vs2017_nav_buttons.png)

## <a name="navigation-bar"></a>Barra de navegação

Você pode usar a **barra de navegação** (as caixas suspensas na parte superior da janela de código) para navegar para o código em uma base de código. É possível escolher um tipo ou membro para ir diretamente a ele. A barra de navegação é exibida ao editar códigos no Visual Basic, C# ou base de código C++. Em uma classe parcial, os membros definidos fora do arquivo de código atual podem estar desabilitados (aparecendo em cinza).

 ![Barra de navegação de código](../ide/media/vside_navigation_bar.png)

Você pode navegar nas caixas suspensas da seguinte maneira:

- Para navegar para outro projeto ao qual o arquivo atual pertence, escolha-o na lista suspensa à esquerda.

- Para navegar para uma classe ou um tipo, escolha-o no menu suspenso central.

- Para navegar diretamente para um procedimento ou para outro membro de uma classe, escolha-o no menu suspenso à direita.

- Para mudar o foco da janela de código para a barra de navegação, pressione a combinação de teclas de atalho **Ctrl**+**F2**.

- Para mudar o foco de caixa para caixa na barra de navegação, pressione a tecla **Tab**.

- Para selecionar o item da barra de navegação que tem o foco e retornar à janela de código, pressione a tecla **Enter**.

- Para retornar o foco da barra de navegação para o código sem selecionar nada, pressione a tecla **Esc**.

Para ocultar a barra de navegação, altere a opção **Barra de navegação** nas configurações **Todas as Linguagens do Editor de Texto** (**Ferramentas** > **Opções** > **Editor de Texto** > **Todas as Linguagens**) ou altere as configurações das linguagens individualmente.

## <a name="find-all-references"></a>Localizar todas as referências

Localiza todas as referências ao elemento selecionado na solução. Você pode usar isso para verificar possíveis efeitos colaterais de uma refatoração grande ou para verificar código "morto". Pressione **F8** para pular entre os resultados. Para obter mais informações, confira [Localizar referências no código](finding-references.md).

Entrada | Função
------------ | ---
**Teclado** | Coloque o cursor de texto em algum lugar dentro do nome do tipo e pressione **Shift**+**F12**
**Mouse** | Selecione **Localizar Todas as Referências** no menu de contexto

## <a name="reference-highlighting"></a>Realce de referência

Quando você clica em um símbolo no código-fonte, todas as instâncias desse símbolo são realçadas no documento. Os símbolos realçados podem incluir declarações e referências e muitos outros símbolos que **Localizar Todas as Referências** retornaria. Isso inclui os nomes de classes, objetos, variáveis, métodos e propriedades. No código do Visual Basic, as palavras-chave de muitas estruturas de controle também são realçadas. Para passar para o próximo símbolo realçado ou para o anterior, pressione **Ctrl**+**Shift**+**Seta para Baixo** ou **Ctrl**+**Shift**+**Seta para Cima**. Você pode alterar a cor de realce em **Ferramentas** > **Opções** > **Ambiente** > **Fontes e Cores** > **Referência Realçada**.

## <a name="go-to-commands"></a>Comandos Ir Para

Ir Para tem os seguintes comandos que estão disponíveis no menu **Editar** em **Ir Para**:

- **Ir Para Linha** (**Ctrl**+**G**): mover para o número de linha especificado no documento ativo.

- **Ir para Todos** (**Ctrl**+**T** ou **Ctrl**+**,**): mover para a linha, o tipo, o arquivo, o membro ou o símbolo especificado.

- **Ir para Arquivo** (**Ctrl**+**1**, **Ctrl**+**F**): mover para o arquivo especificado na solução.

- **Ir para Arquivo Recente** (**Ctrl**+**1**, **Ctrl**+**R**): mover para o arquivo visitado recentemente na solução especificado (novo no Visual Studio 2017 versão 15.8).

- **Ir para Tipo** (**Ctrl**+**1**, **Ctrl**+**T**): mover para o tipo especificado na solução.

- **Ir para Membro** (**Ctrl**+**1**, **Ctrl**+**M**): mover para o membro especificado na solução.

- **Ir para Símbolo** (**Ctrl**+**1**, **Ctrl**+**S**): mover para o símbolo especificado na solução.

No Visual Studio 2017 versão 15.8 e posteriores, os seguintes comandos de navegação **Ir Para** também estão disponíveis:

- **Ir para Próximo Problema no Arquivo** (**Alt**+**PgDn**) e **Ir para o Problema Anterior no Arquivo** (**Alt**+**PgUp**)

- **Ir para Local da Última Edição** (**Ctrl**+**Shift**+**Backspace**)

Veja mais informações sobre esses comandos no tópico [Localizar código usando os comandos Ir Para](../ide/go-to.md).

## <a name="go-to-definition"></a>Ir para definição

Ir para Definição leva para a definição do elemento selecionado. Para saber mais, veja [Ir para Definição e Inspecionar Definição](../ide/go-to-and-peek-definition.md).

Entrada | Função
------------ | ---
**Teclado** | Coloque o cursor de texto em algum lugar dentro do nome do tipo e pressione **F12**
**Mouse** | Clique com o botão direito do mouse no nome do tipo e selecione **Ir para Definição** ou pressione **Ctrl** e clique no nome do tipo (novo no Visual Studio 2017 versão 15.4)

## <a name="peek-definition"></a>Inspecionar Definição

Espiar Definição exibe a definição do elemento selecionado em uma janela sem sair do local atual no editor de código. Para obter mais informações, confira [Como exibir e editar o código usando Espiar Definição](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md) e [Ir para Definição e Espiar Definição](../ide/go-to-and-peek-definition.md).

Entrada | Função
------------ | ---
**Teclado** | Coloque o cursor de texto em algum lugar dentro do nome do tipo e pressione **Alt**+**F12**
**Mouse** | Clique com o botão direito do mouse no nome do tipo e selecione **Espiar Definição** ou pressione **Ctrl** e clique no nome do tipo (se a opção **Abrir definição na exibição de espiada** estiver marcada)

## <a name="go-to-implementation"></a>Ir Para Implementação

Usando Ir para Implementação, você pode navegar de uma classe ou tipo base para suas implementações. Se houver várias implementações, você as verá listadas na janela **Localizar Resultados de Símbolos**:

Entrada | Função
------------ | ---
**Teclado** | Coloque o cursor de texto em algum lugar dentro do nome do tipo e pressione **Ctrl**+**F12**
**Mouse** | Clique com o botão direito do mouse no nome do tipo e selecione **Ir Para Implementação**

## <a name="call-hierarchy"></a>Hierarquia de chamadas

Você pode exibir as chamadas de e para um método na [Janela Hierarquia de Chamada](../ide/reference/call-hierarchy.md):

Entrada | Função
------------ | ---
**Teclado** | Coloque o cursor de texto em algum lugar dentro do nome do tipo e pressione **Ctrl**+**K**, **Ctrl**+**T**
**Mouse** | Clique com o botão direito do mouse no nome do membro e selecione **Exibir Hierarquia de Chamadas**

## <a name="next-method-and-previous-method-commands-visual-basic"></a>Comandos Próximo Método e Método Anterior (Visual Basic)

Nos arquivos de código Visual Basic, use esses comandos para mover o ponto de inserção para diferentes métodos. Escolha **Editar** > **Próximo Método** ou **Editar** > **Método Anterior**.

## <a name="structure-visualizer"></a>Visualizador de Estrutura

O recurso Visualizador de Estrutura no editor de códigos mostra as *linhas guias da estrutura* – linhas verticais tracejadas que indicam a correspondência de chaves em sua base de código. Isso facilita ver onde os blocos lógicos começam e terminam.

![Visualizador de Estrutura](../ide/media/vside_structure_visualizer.png)

Para desabilitar as linhas da guia da estrutura, acesse **Ferramentas** > **Opções** > **Editor de Texto** > **Geral** e limpe a caixa **Mostrar linhas da guia da estrutura**.

## <a name="enhanced-scroll-bar"></a>Barra de rolagem avançada

Você pode usar a barra de rolagem avançada em uma janela de código para obter uma visão geral do seu código. No modo de mapa, você pode acessar visualizações do código ao mover o cursor para cima e para baixo na barra de rolagem. Para obter mais informações, confira [Como acompanhar o código personalizando a barra de rolagem](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md).

## <a name="codelens-information"></a>Informações do CodeLens

Você pode localizar informações sobre o código específico, como alterações e quem fez essas alterações, referências, bugs, itens de trabalho, revisões de código e status de teste de unidade ao usar o CodeLens no editor de código. O CodeLens funciona como uma exibição de alerta quando você usa o Visual Studio Enterprise com o Team Foundation Server. Consulte [Localizar alterações de código e outros históricos](../ide/find-code-changes-and-other-history-with-codelens.md).

## <a name="see-also"></a>Consulte também

- [Recursos do Editor de Códigos](../ide/writing-code-in-the-code-and-text-editor.md)
- [Exibir a hierarquia de chamada](../ide/reference/call-hierarchy.md)
