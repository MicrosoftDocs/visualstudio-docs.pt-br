---
title: Dicas de produtividade para o Visual Studio
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 362004cba4792fe2405d6cc009a0ae918fdd535e
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50671294"
---
# <a name="productivity-tips-for-visual-studio"></a>Dicas de produtividade para o Visual Studio

Este tópico contém várias dicas para ajudar você a escrever, navegar e depurar seu código com mais rapidez e eficiência.

Para saber mais sobre os atalhos de teclado comuns, confira [Dicas de teclado](../ide/tips-and-tricks-for-visual-studio.md). Ou, para obter uma lista completa de atalhos de teclado, confira [Identificar e personalizar atalhos de teclado](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md) e [Atalhos de teclado padrão](../ide/default-keyboard-shortcuts-in-visual-studio.md).

## <a name="write-code"></a>Escrever código

Escreva código mais rapidamente usando os seguintes recursos.

- **Usar comandos de conveniência**. O Visual Studio contém vários comandos para ajudar você a realizar tarefas comuns de edição mais rapidamente. Por exemplo, no **Visual Studio 2017 versão 15.6** e posterior, você pode escolher um comando para duplicar facilmente uma linha de código sem a necessidade de copiá-lo, reposicionar o cursor e, depois, colá-lo. Escolha **Editar** > **Duplicar** ou pressione **Ctrl**+**E**,**V**. Você também pode expandir ou recolher uma seleção de texto escolhendo **Editar** > **Avançado** > **Expandir Seleção** ou **Editar** > **Avançado** > **Reduzir Seleção** ou pressionando **Shift**+**Alt**+**=** ou **Shift**+**Alt**+**-** (disponível no **Visual Studio 2017 versão 15.5** e posterior).

- **Use o IntelliSense**. À medida que você inserir código no editor, informações do IntelliSense, como Membros da Lista, Informações do Parâmetro, Informações Rápidas, Ajuda de Assinatura e Completar Palavras, serão exibidas. Esses recursos dão suporte à correspondência difusa de texto; por exemplo, as listas de resultados para Membros da Lista incluem não só entradas que começam com os caracteres que você inseriu, como também entradas que contêm a combinação de caracteres em qualquer lugar de seus nomes. Para obter mais informações, confira [Usar o IntelliSense](../ide/using-intellisense.md).

- **Altere a inserção automática de opções do IntelliSense à medida que você insere o código**. Ao alternar o IntelliSense para o modo de sugestão, você pode especificar que opções do IntelliSense será inseridas somente se você as escolher explicitamente.

     Para habilitar o modo de sugestão, escolha as teclas **Ctrl**+**Alt**+**Barra de espaço** ou, na barra de menus, escolha **Editar** > **IntelliSense** > **Ativar/Desativar Modo de Preenchimento**.

- **Use snippets de código**. Você pode usar snippets internos ou criar seus próprios snippets.

     Para inserir um snippet, na barra de menus, escolha **Editar** > **IntelliSense** > **Inserir Snippet** ou **Cercar com**, ou abra o menu de atalho em um arquivo e escolha **Trecho** > **Inserir Snippet** ou **Cercar com**. Para obter mais informações, consulte [Snippets de Código](../ide/code-snippets.md).

- **Corrija erros de código embutidos**. As Ações Rápidas permitem refatorar, gerar ou, de outro modo, modificar o código de maneira fácil com uma única ação. Essas ações podem ser aplicadas usando os ícones de chave de fenda ![ícone de chave de fenda](media/screwdriver-icon.png) ou de lâmpada ![ícone de lâmpada](media/light-bulb-icon.png) ou pressionando **Alt**+**Enter** ou **Ctrl**+**.** quando o cursor estiver sobre a linha de código apropriada. Consulte [Ações Rápidas](quick-actions.md) para obter mais informações.

- **Exibir e editar a definição de um elemento de código**. Você pode exibir e editar rapidamente o módulo no qual um elemento de código, como um membro, uma variável ou um local, é definido.

    Para abrir uma definição em uma janela pop-up, realce o elemento e escolha as teclas **Alt**+**F12**, ou abra o menu de atalho do elemento e, em seguida, escolha **Inspecionar Definição**. Para abrir uma definição em uma janela de código separada, abra o menu de atalho para o elemento de código e então escolha **Ir Para Definição**.

- **Use aplicativos de exemplo**. É possível acelerar o desenvolvimento de aplicativos baixando e instalando aplicativos de exemplo do [Microsoft Developer Network](https://code.msdn.microsoft.com/). Você também pode aprender uma tecnologia em particular ou um conceito baixando e explorando um Sample Pack para essa área.

## <a name="navigate-within-your-code"></a>Navegar em seu código

 Você pode usar várias técnicas para localizar e mover para locais específicos em seu código com mais rapidez.

- **Usar indicadores em linhas de código**. Você pode usar indicadores para navegar rapidamente para linhas específicas do código em um arquivo.

    Para definir um indicador, na barra de menus, escolha **Editar** > **Indicadores** > **Ativar/Desativar Indicador**. Você pode exibir todos os indicadores para uma solução na janela **Indicadores**. Para obter mais informações, confira [Definir indicadores no código](../ide/setting-bookmarks-in-code.md).

- **Pesquisar definições de símbolo em um arquivo**. Você pode pesquisar em uma solução para localizar definições de símbolos e nomes de arquivos, mas os resultados da pesquisa não incluirão os namespaces ou as variáveis locais.

   Para acessar esse recurso, na barra de menus, escolha **Editar** > **Navegar até**.

- **Procure a estrutura geral do seu código**. No **Gerenciador de Soluções**, você pode pesquisar e procurar classes e seus tipos e membros em seus projetos. Você também pode pesquisar símbolos, exibir a Hierarquia de Chamada de um método, localizar referências de símbolos e realizar outras tarefas. Se você escolher um elemento de código no **Gerenciador de Soluções**, o arquivo associado será aberto em uma guia **Visualização** e o cursor se moverá para o elemento no arquivo. Para obter mais informações, confira [Exibir a estrutura do código](../ide/viewing-the-structure-of-code.md).

## <a name="find-items-faster"></a>Localizar itens mais rapidamente

Você pode procurar no IDE comandos, arquivos e opções, bem como filtrar o conteúdo de janelas de ferramenta para mostrar somente as informações relevantes para sua tarefa atual.

- **Filtrar o conteúdo de janelas de ferramentas**. Você pode pesquisar no conteúdo de muitas janelas de ferramentas, como a **Caixa de Ferramentas**, a janela **Propriedades** e o **Gerenciador de Soluções**, mas só poderá exibir itens cujos nomes contenhamos caracteres que você especificar.

- **Exiba apenas os erros que você deseja resolver**. Se você escolher o botão **Filtrar** na barra de ferramentas **Lista de Erros**, poderá reduzir o número de erros que aparecem na janela **Lista de Erros**. Você só pode exibir os erros em arquivos que estão abertos no editor, somente os erros no arquivo atual ou somente os erros no projeto atual. Você também pode pesquisar na janela **Lista de Erros** para localizar erros específicos.

- **Localizar caixas de diálogo, comandos de menu e opções**. Na caixa [Início Rápido](../ide/reference/quick-launch-environment-options-dialog-box.md), digite palavras-chave ou frases para os itens que você está tentando localizar. Por exemplo, as seguintes opções aparecerão se você inserir `new project`:

    ![Resultados do Início Rápido para "novo projeto"](../ide/media/productivity_quicklaunch.png)

    O **Início Rápido** exibe links para a caixa de diálogo **Novo Projeto**, a caixa de diálogo **Adicionar Novo Item** e a página **Projetos e Soluções** na caixa de diálogo **Opções**, entre outros. Os resultados do Início Rápido também podem incluir arquivos de projeto e janelas de ferramenta.

## <a name="debug-code"></a>Depurar o código

A depuração pode consumir muito tempo, mas as dicas a seguir podem ajudar a acelerar o processo.

- **Teste a mesma página, aplicativo ou site em navegadores diferentes**. À medida que você depura seu código, poderá facilmente mudar entre os navegadores da Web instalados, incluindo o [Inspetor de Página (Visual Studio)](https://msdn.microsoft.com/Library/65880969-1ad2-47be-85b9-bb12c81bf209), sem ter que abrir a caixa de diálogo **Procurar Com**. Você pode usar a lista **Destino de Depuração**, que está na barra de ferramentas **Standard** ao lado do botão **Iniciar Depuração**, para verificar rapidamente qual navegador está utilizando enquanto depura ou exibe as páginas.

    ![Selecionar opções de depuração de navegador da Web](../ide/media/webbrowserdropdowntoolbar.png)

- **Definir pontos de interrupção temporários**. Você pode criar um ponto de interrupção temporário na linha de código atual e iniciar o depurador simultaneamente. Quando você atinge esta linha de código, o depurador entra em modo de interrupção. Para obter mais informações, confira [Navegar pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md).

    Para usar este recurso, escolha as teclas **Ctrl**+**F10** ou abra o menu de atalho para a próxima linha de código em que você deseja quebrar e, em seguida, escolha **Executar até o cursor**.

- **Mover o ponto de execução durante a depuração**. Você pode mover o ponto de execução atual para uma seção de código diferente e então reiniciar a depuração desse ponto. Essa técnica será útil se você quiser depurar uma seção de código sem precisar recriar todas as etapas necessárias para acessar a seção. Para obter mais informações, confira [Navegar pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md).

     Para mover o ponto de execução, arraste a ponta da seta amarela para um local em que deseja definir a declaração seguinte no mesmo arquivo de origem e, então, escolha a tecla **F5** para continuar a depuração.

- **Capturar informações de valor de variáveis**. Você pode adicionar um DataTip a uma variável no seu código e fixá-lo para poder acessar o último valor conhecido da variável após a conclusão da depuração. Para obter mais informações, consulte [Exibir valores de dados em Dicas de Dados](../debugger/view-data-values-in-data-tips-in-the-code-editor.md).

     Para adicionar um DataTip, o depurador deverá estar em modo de interrupção. Coloque o cursor na variável e então escolha o botão de fixação no DataTip em que ele aparece. Quando a depuração é interrompida, um ícone de pino azul aparece no arquivo de origem ao lado da linha de código que contém a variável. Se você apontar para o pino azul, será exibido o valor da variável de sessão de depuração mais recente.

- **Limpar a janela Imediata**. Você pode apagar rapidamente o conteúdo da [Janela imediata](../ide/reference/immediate-window.md) no tempo de design inserindo `>cls` ou `>Edit.ClearAll`

     Para obter mais informações sobre comandos adicionais, confira [Aliases de comando do Visual Studio](../ide/reference/visual-studio-command-aliases.md).

## <a name="access-visual-studio-tools"></a>Acessar ferramentas do Visual Studio

Você poderá acessar rapidamente o Prompt de Comando do Desenvolvedor ou outra ferramenta do Visual Studio se você fixá-la no menu Iniciar ou na barra de tarefas.

1. No Windows Explorer, navegue até `%ProgramData%\Microsoft\Windows\Start Menu\Programs\Visual Studio 2017\Visual Studio Tools`.

1. Clique com botão direito do mouse ou abra o menu de contexto para o **Prompt de Comando do Desenvolvedor** e, em seguida, selecione **Fixar na tela inicial** ou **Fixar na barra de tarefas**.

## <a name="manage-files-toolbars-and-windows"></a>Gerenciar arquivos, barras de ferramentas e janelas

A qualquer momento, você pode estar trabalhando em vários arquivos de código e se mover entre várias janelas de ferramenta enquanto desenvolve um aplicativo. Você pode se manter organizado usando as dicas a seguir.

- **Manter arquivos que você usa frequentemente visíveis no editor**. Você pode fixar arquivos no lado esquerdo da guia de forma que eles permaneçam visíveis, independentemente de quantos arquivos estiverem abertos no editor.

     Para fixar um arquivo, escolha a guia do arquivo e, então, selecione o botão **Ativar/desativar status de pin**.

- **Mover documentos e janelas para outros monitores**. Se você usar mais de um monitor quando desenvolver aplicativos, poderá trabalhar em partes do seu aplicativo mais facilmente movendo arquivos que estejam abertos no editor para outro monitor. Você também pode mover janelas de ferramentas, como as de depuração, para outro monitor e encaixar as janelas de documentos e de ferramentas para criar "rafts". Para obter mais informações, consulte [Personalização de layouts de janela no Visual Studio](../ide/customizing-window-layouts-in-visual-studio.md).

     Você também pode gerenciar arquivos mais facilmente criando outra instância do **Gerenciador de Soluções** e movendo-a para outro monitor. Para criar outra instância do **Gerenciador de Soluções**, abra um menu de atalho no **Gerenciador de Soluções** e então escolha **Novo Modo de Exibição do Gerenciador de Soluções**.

- **Personalizar as fontes que aparecem no Visual Studio**. Você pode alterar o tipo de fonte, a cor e o tamanho usados para o texto no IDE. Por exemplo, você pode personalizar a cor de elementos de código específicos no editor e a fonte em janelas de ferramenta ou por meio do IDE. Para obter mais informações, confira [Como alterar fontes e cores](../ide/how-to-change-fonts-and-colors-in-visual-studio.md) e [Como alterar fontes e cores no editor](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md).

## <a name="see-also"></a>Consulte também

- [Atalhos de teclado padrão para comandos usados com frequência](../ide/default-keyboard-shortcuts-for-frequently-used-commands-in-visual-studio.md)
- [Como personalizar menus e barras de ferramentas](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md)
- [Passo a passo: criar um aplicativo simples](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md)
- [Dicas e truques de acessibilidade](../ide/reference/accessibility-tips-and-tricks.md)