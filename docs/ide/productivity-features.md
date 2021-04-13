---
title: Guia de produtividade
description: Saiba mais sobre os atalhos de teclado e os recursos de produtividade no Visual Studio que podem ajudá-lo a escrever código, depurar código e manipular erros com eficiência.
ms.custom: SEO-VS-2020
ms.date: 4/29/2020
ms.topic: conceptual
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 181ce2071d780c9ef481d281f543c49d65262078
ms.sourcegitcommit: 6d88913a8b5a9e5eda01d3f95205b4d138f440f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/13/2021
ms.locfileid: "107296775"
---
# <a name="productivity-guide-for-visual-studio"></a>Guia de produtividade do Visual Studio

Se você quiser economizar tempo enquanto está escrevendo código, você está no lugar certo. Este guia de produtividade inclui dicas que podem ajudá-lo a começar a usar o Visual Studio, escrever código, depurar código, lidar com erros e utilizar atalhos &mdash; de teclado em uma única página.

Para saber mais sobre atalhos de teclado úteis, confira [Atalhos de produtividade](../ide/productivity-shortcuts.md). Para obter uma lista completa de atalhos de comando, confira [Atalhos de teclado padrão](../ide/default-keyboard-shortcuts-in-visual-studio.md).

## <a name="get-started"></a>Introdução

Economize tempo com os menus pesquisando rapidamente tudo o que você precisa, incluindo comandos, configurações, documentação e opções de instalação. Consulte os atalhos de teclado para comandos nos resultados da pesquisa no Visual Studio para que você possa memorizar mais facilmente. 

- **Código fictício usando a lista de tarefas**. Se você não tiver requisitos suficientes para concluir uma parte do código, use Lista de Tarefas para rastrear comentários de código que usam tokens como `TODO` e `HACK` , ou tokens personalizados, e para gerenciar atalhos que levam você diretamente a um local predefinido no código. Para obter mais informações, consulte [usar o lista de tarefas](../ide/using-the-task-list.md).

- **Use atalhos de Gerenciador de soluções**. Se você for novo no Visual Studio, esses atalhos serão úteis e pouparão tempo enquanto você estiver chegando a uma nova base de código. Para obter a lista completa de atalhos, consulte [atalhos de teclado padrão no Visual Studio](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_solutionexplorerGLOBAL).

- **[Identificar e personalizar atalhos de teclado no Visual Studio](../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)**. Você pode identificar atalhos de teclado para comandos do Visual Studio, personalizar esses atalhos e exportá-los para que outras pessoas os usem. Você sempre pode localizar e alterar um atalho de teclado na caixa de diálogo opções.

- **Torne o Visual Studio mais acessível**. O Visual Studio tem recursos internos de acessibilidade que são compatíveis com leitores de tela e outras tecnologias assistenciais. Consulte [dicas e truques de acessibilidade para o Visual Studio](../ide/reference/accessibility-tips-and-tricks.md) para obter a lista completa de recursos disponíveis. 

- **Confira o ciclo de vida do produto e a manutenção do Visual Studio**. Para obter informações sobre como obter atualizações para o Visual Studio, opções de suporte para clientes corporativos e profissionais, suporte para versões mais antigas do Visual Studio e componentes não cobertos pelo serviço do Visual Studio, consulte [ciclo de vida do produto e manutenção do Visual Studio](/visualstudio/releases/2019/servicing). 

- **Instalar e gerenciar pacotes NuGet no Visual Studio**. A interface do usuário do Gerenciador de Pacotes do NuGet no Visual Studio no Windows possibilita instalar, desinstalar e atualizar pacotes do NuGet com facilidade em projetos e soluções. Para obter mais informações, consulte [instalar e gerenciar pacotes no Visual Studio usando o Gerenciador de pacotes NuGet](/nuget/consume-packages/install-use-packages-visual-studio).

## <a name="write-code"></a>Escrever código

Escreva código mais rapidamente usando os seguintes recursos.

- **Usar comandos de conveniência**. O Visual Studio contém vários comandos para ajudar você a realizar tarefas comuns de edição mais rapidamente. Por exemplo, você pode escolher um comando para duplicar com facilidade uma linha de código sem precisar copiá-la, reposicionar o cursor e, em seguida, colá-la. Escolha **Editar**  >  **duplicar** ou pressione **Ctrl** + **E**,**V**. Você também pode expandir ou contratar rapidamente uma seleção de texto escolhendo **Editar**  >    >  **seleção de expansão** avançada ou **Editar**  >    >  **seleção de contrato** avançada ou pressionando **Shift** + **ALT** + **=** ou **Shift** + **ALT** + **-** .

- **Use o IntelliSense**. À medida que você inserir código no editor, informações do IntelliSense, como Membros da Lista, Informações do Parâmetro, Informações Rápidas, Ajuda de Assinatura e Completar Palavras, serão exibidas. Esses recursos dão suporte à correspondência difusa de texto; por exemplo, as listas de resultados para membros da lista incluem não apenas entradas que começam com os caracteres que você inseriu, mas também entradas que contêm a combinação de caracteres em qualquer lugar em seus nomes. Para obter mais informações, confira [Usar o IntelliSense](../ide/using-intellisense.md).

- **Altere a inserção automática de opções do IntelliSense à medida que você insere o código**. Ao alternar o IntelliSense para o modo de sugestão, você pode especificar que opções do IntelliSense será inseridas somente se você as escolher explicitamente.

     Para habilitar o modo de sugestão, escolha as teclas de barra de espaços **Ctrl** + **ALT** +  ou, na barra de menus, escolha **Editar**  >    >  **modo de conclusão de alternância** do IntelliSense.

- **Use trechos de código**. Você pode usar snippets internos ou criar seus próprios snippets.

     Para inserir um trecho de código, na barra de menus, escolha **Editar**  >    >  **trecho de código de inserção** do IntelliSense ou **surround com** ou abra o menu de atalho em um arquivo e escolha **trecho de** código de  >  **inserção** ou **surround com**. Para obter mais informações, consulte [Snippets de Código](../ide/code-snippets.md).

- **Corrija erros de código embutidos**. As Ações Rápidas permitem refatorar, gerar ou, de outro modo, modificar o código de maneira fácil com uma única ação. Essas ações podem ser aplicadas usando o ícone de ![ chave de fenda ](media/screwdriver-icon.png) ou ícones de ícone de lâmpada de lâmpada ou ![ ](media/light-bulb-icon.png) pressionando **ALT** + **Enter** ou **Ctrl** + **.** quando o cursor estiver sobre a linha de código apropriada. Consulte [Ações Rápidas](quick-actions.md) para obter mais informações.

- **Exibir e editar a definição de um elemento de código**. Você pode exibir e editar rapidamente o módulo no qual um elemento de código, como um membro, uma variável ou um local, é definido.

    Para abrir uma definição em uma janela pop-up, realce o elemento e, em seguida, escolha as teclas **ALT** + **F12** ou abra o menu de atalho para o elemento e escolha **inspecionar definição**. Para abrir uma definição em uma janela de código separada, abra o menu de atalho para o elemento de código e então escolha **Ir Para Definição**.

- **Use aplicativos de exemplo**. É possível acelerar o desenvolvimento de aplicativos baixando e instalando aplicativos de exemplo do [Microsoft Developer Network](https://code.msdn.microsoft.com/). Você também pode aprender uma tecnologia em particular ou um conceito baixando e explorando um Sample Pack para essa área.

- **Alterar a formatação de chaves com formatação/novas linhas**. Use a página opções de **formatação**  para definir opções de formatação de código no editor de código, incluindo novas linhas. Para obter mais informações sobre como usar essa configuração em C#, consulte [caixa de diálogo opções: editor de texto > C# > estilo de código > formatação](../ide/reference/options-text-editor-csharp-formatting.md). Para C++, consulte [definir suas preferências de codificação em c++ no Visual Studio](/cpp/ide/how-to-set-preferences). Para Python, consulte [Formatar código Python](../python/formatting-python-code.md).

- **Altere o recuo com tabulações**. Use configurações personalizadas do editor, adaptadas a cada base de código, para impor estilos de codificação consistentes para vários desenvolvedores trabalhando no mesmo projeto em diferentes editores e IDEs. Verifique se toda a sua equipe segue as mesmas convenções de linguagem, convenções de nomenclatura e regras de formatação. Como essas configurações personalizadas são portáteis e viajam com seu código, você pode impor estilos de codificação mesmo fora do Visual Studio. Para obter mais informações, consulte [Opções, editor de texto, todas as linguagens, guias](../ide/reference/options-text-editor-all-languages-tabs.md#tabs).

## <a name="navigate-within-your-code-and-the-ide"></a>Navegar dentro de seu código e do IDE

Você pode usar várias técnicas para localizar e mover para locais específicos em seu código com mais rapidez. Você também pode alterar o layout de suas janelas do Visual Studio com base em suas preferências. 

- **Usar indicadores em linhas de código**. Você pode usar indicadores para navegar rapidamente para linhas específicas do código em um arquivo.

    Para definir um indicador, na barra de menus, escolha **Editar**  >  **indicadores**  >  **alternar indicador**. Você pode exibir todos os indicadores para uma solução na janela **Indicadores**. Para obter mais informações, confira [Definir indicadores no código](../ide/setting-bookmarks-in-code.md).

- **Pesquisar definições de símbolo em um arquivo**. Você pode pesquisar em uma solução para localizar definições de símbolos e nomes de arquivos, mas os resultados da pesquisa não incluirão os namespaces ou as variáveis locais.

   Para acessar esse recurso, na barra de menus, escolha **Editar**  >  **navegar para**.

- **Procure a estrutura geral do seu código**. No **Gerenciador de Soluções**, você pode pesquisar e procurar classes e seus tipos e membros em seus projetos. Você também pode pesquisar símbolos, exibir a Hierarquia de Chamada de um método, localizar referências de símbolos e realizar outras tarefas. Se você escolher um elemento de código no **Gerenciador de Soluções**, o arquivo associado será aberto em uma guia **Visualização** e o cursor se moverá para o elemento no arquivo. Para obter mais informações, confira [Exibir a estrutura do código](../ide/viewing-the-structure-of-code.md).

- **Vá para um local em um arquivo com o modo de mapa**. O modo de mapa exibe linhas de código, em miniatura, na barra de rolagem. Para obter mais informações sobre esse modo de exibição, consulte [como: personalizar a barra de rolagem](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md#map-mode).

- **Entenda sua estrutura de código com o mapa de código**. Os mapas de código podem ajudá-lo a Visualizar dependências em seu código e ver como ele se encaixa sem ler arquivos e linhas de código. Para saber mais, confira [Mapear as dependências com mapas de código](../modeling/map-dependencies-across-your-solutions.md).

- **Consulte arquivos usados com frequência com editar/ir para o arquivo recente**. Use os comandos go to no Visual Studio para executar uma pesquisa focada de seu código para ajudá-lo a localizar rapidamente os itens especificados. Para obter instruções detalhadas, consulte [Localizar código usando ir para comandos](../ide/go-to.md).

- **Mova o [janela Propriedades](../ide/reference/properties-window.md) para o lado direito**. Se você estiver procurando um layout de janela mais familiar, poderá mover o janela Propriedades no Visual Studio pressionando **F4**.

## <a name="find-items-faster"></a>Localizar itens mais rapidamente

Você pode procurar no IDE comandos, arquivos e opções, bem como filtrar o conteúdo de janelas de ferramenta para mostrar somente as informações relevantes para sua tarefa atual.

- **Filtrar o conteúdo de janelas de ferramentas**. Você pode pesquisar no conteúdo de muitas janelas de ferramentas, como a **Caixa de Ferramentas**, a janela **Propriedades** e o **Gerenciador de Soluções**, mas só poderá exibir itens cujos nomes contenhamos caracteres que você especificar.

- **Exiba apenas os erros que você deseja resolver**. Se você escolher o botão **Filtrar** na barra de ferramentas **Lista de Erros**, poderá reduzir o número de erros que aparecem na janela **Lista de Erros**. Você só pode exibir os erros em arquivos que estão abertos no editor, somente os erros no arquivo atual ou somente os erros no projeto atual. Você também pode pesquisar dentro da janela de **lista de erros** para localizar erros específicos.

- **Localizar caixas de diálogo, comandos de menu, opções e mais**. Na caixa de pesquisa, digite as palavras-chave ou frases dos itens que você está tentando localizar. Por exemplo, as seguintes opções aparecerão se você inserir **novo projeto**:

   ::: moniker range="vs-2017"

   ![Resultados do Início Rápido para "novo projeto"](../ide/media/productivity_quicklaunch.png)

   O **Início Rápido** exibe links para criar um projeto, para adicionar um novo item a um projeto e para a página **Projetos e Soluções** na caixa de diálogo **Opções**, entre outros. Os resultados da pesquisa também podem incluir arquivos de projeto e janelas de ferramentas.

   ::: moniker-end

   ::: moniker range=">=vs-2019"

   ![Resultados para o 'novo projeto'](../ide/media/vs-2019/productivity-quick-launch-new-project.png)

   ::: moniker-end

   Pressione **Ctrl** + **Q** para ir direto para a caixa de pesquisa.

## <a name="debug-code"></a>Depurar o código

A depuração pode consumir muito tempo, mas as dicas a seguir podem ajudar a acelerar o processo.

- **Use as ferramentas do depurador do Visual Studio**. No contexto do Visual Studio, quando você *depura seu aplicativo*, normalmente significa que você está executando o aplicativo no modo de depurador. O depurador fornece várias maneiras de ver o que seu código está fazendo durante a execução. Consulte [primeiro o depurador do Visual Studio](../debugger/debugger-feature-tour.md) para obter um guia para começar. 

- **Teste a mesma página, aplicativo ou site em navegadores diferentes**. À medida que você depura seu código, poderá facilmente mudar entre os navegadores da Web instalados, incluindo o [Inspetor de Página (Visual Studio)](/previous-versions/hh974728(v=vs.140)), sem ter que abrir a caixa de diálogo **Procurar Com**. Você pode usar a lista de **destino de depuração** , que está na barra de ferramentas **padrão** ao lado do botão **Iniciar Depuração** , para verificar rapidamente qual navegador você está usando ao depurar ou exibir páginas.

    ![Selecionar opções de depuração de navegador da Web](../ide/media/webbrowserdropdowntoolbar.png)

- **Definir pontos de interrupção temporários**. Você pode criar um ponto de interrupção temporário na linha de código atual e iniciar o depurador simultaneamente. Quando você atinge esta linha de código, o depurador entra em modo de interrupção. Para obter mais informações, confira [Navegar pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md).

    Para usar esse recurso, escolha as teclas **Ctrl** + **F10** ou abra o menu de atalho para a linha de código na qual você deseja interromper e, em seguida, escolha **executar até o cursor**.

- **Mover o ponto de execução durante a depuração**. Você pode mover o ponto de execução atual para uma seção de código diferente e então reiniciar a depuração desse ponto. Essa técnica será útil se você quiser depurar uma seção de código sem precisar recriar todas as etapas necessárias para acessar a seção. Para obter mais informações, confira [Navegar pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md).

     Para mover o ponto de execução, arraste a ponta de seta amarela para um local onde você deseja definir a próxima instrução no mesmo arquivo de origem e escolha a tecla **F5** para continuar a depuração.

- **Capturar informações de valor de variáveis**. Você pode adicionar um DataTip a uma variável no seu código e fixá-lo para poder acessar o último valor conhecido da variável após a conclusão da depuração. Para obter mais informações, consulte [Exibir valores de dados em Dicas de Dados](../debugger/view-data-values-in-data-tips-in-the-code-editor.md).

     Para adicionar um DataTip, o depurador deverá estar em modo de interrupção. Coloque o cursor na variável e então escolha o botão de fixação no DataTip em que ele aparece. Quando a depuração é interrompida, um ícone de pino azul aparece no arquivo de origem ao lado da linha de código que contém a variável. Se você apontar para o pino azul, será exibido o valor da variável de sessão de depuração mais recente.

- **Limpar a janela Imediata**. Você pode apagar o conteúdo da [janela imediata](../ide/reference/immediate-window.md) em tempo de design digitando `>cls` ou `>Edit.ClearAll`

     Para obter mais informações sobre comandos adicionais, consulte [aliases de comando do Visual Studio](../ide/reference/visual-studio-command-aliases.md).

- **[Encontre alterações de código e outros históricos com CodeLens](../ide/find-code-changes-and-other-history-with-codelens.md)**. O CodeLens permite que você mantenha o foco no trabalho enquanto descobre o que aconteceu com seu código – sem sair do editor. Encontre referências e alterações no código, bugs vinculados, itens de trabalho, revisões de código e testes de unidade.

- **Use Live share para depurar em tempo real com outras pessoas**. O Live Share permite que você edite e depure em colaboração com outras pessoas em tempo real, sejam quais forem as linguagens de programação usadas ou os tipos de aplicativo criados. Para obter mais informações, consulte [o que é Visual Studio Live share?](/visualstudio/liveshare/)

- **Use a janela interativa para escrever e testar código pequeno**. O Visual Studio fornece uma janela interativa de REPL (Read-Evaluate-Print-loop) que permite inserir código arbitrário e ver resultados imediatos. Essa forma de codificação ajuda você a aprender e experimentar APIs e bibliotecas e desenvolver de forma interativa o código de trabalho para incluir em seus projetos. Para o Python, consulte [trabalhar com a janela interativa do Python](../python/python-interactive-repl-in-visual-studio.md). O recurso de janela interativa também está disponível para C#. 

## <a name="access-visual-studio-tools"></a>Acessar ferramentas do Visual Studio

Você poderá acessar rapidamente o Prompt de Comando do Desenvolvedor ou outra ferramenta do Visual Studio se você fixá-la no menu Iniciar ou na barra de tarefas.

::: moniker range="vs-2017"

1. No Windows Explorer, procure *%ProgramData%\Microsoft\Windows\Start Menu\Programs\Visual Studio 2017\Visual Studio Tools*.

::: moniker-end

::: moniker range=">=vs-2019"

1. No Windows Explorer, procure *%ProgramData%\Microsoft\Windows\Start Menu\Programs\Visual Studio 2019\Visual Studio Tools*.

::: moniker-end

2. Clique com botão direito do mouse ou abra o menu de contexto para o **Prompt de Comando do Desenvolvedor** e, em seguida, selecione **Fixar na tela inicial** ou **Fixar na barra de tarefas**.

## <a name="manage-files-toolbars-and-windows"></a>Gerenciar arquivos, barras de ferramentas e janelas

A qualquer momento, você pode estar trabalhando em vários arquivos de código e se mover entre várias janelas de ferramenta enquanto desenvolve um aplicativo. Você pode se manter organizado usando as seguintes dicas:

- **Manter arquivos que você usa frequentemente visíveis no editor**. Você pode fixar arquivos no lado esquerdo da guia para que eles permaneçam visíveis, independentemente de quantos arquivos estejam abertos no editor.

   Para fixar um arquivo, escolha a guia do arquivo e, em seguida, escolha o botão **Ativar status do PIN** .

- **Mover documentos e janelas para outros monitores**. Se você usar mais de um monitor quando desenvolver aplicativos, poderá trabalhar em partes do seu aplicativo mais facilmente movendo arquivos que estejam abertos no editor para outro monitor. Você também pode mover janelas de ferramentas, como as de depuração, para outro monitor e encaixar as janelas de documentos e de ferramentas para criar "rafts". Para obter mais informações, consulte [Personalização de layouts de janela no Visual Studio](../ide/customizing-window-layouts-in-visual-studio.md).

   Você também pode gerenciar arquivos mais facilmente criando outra instância do **Gerenciador de Soluções** e movendo-a para outro monitor. Para criar outra instância do **Gerenciador de Soluções**, abra um menu de atalho no **Gerenciador de Soluções** e então escolha **Novo Modo de Exibição do Gerenciador de Soluções**.

- **Personalizar as fontes que aparecem no Visual Studio**. Você pode alterar o tipo de fonte, a cor e o tamanho usados para o texto no IDE. Por exemplo, você pode personalizar a cor de elementos de código específicos no editor e a fonte em janelas de ferramenta ou por meio do IDE. Para obter mais informações, consulte [como alterar fontes e cores](../ide/how-to-change-fonts-and-colors-in-visual-studio.md) e [como alterar fontes e cores no editor](../ide/reference/how-to-change-fonts-and-colors-in-the-editor.md).

## <a name="see-also"></a>Confira também

- [Postagem no blog de dicas e truques sobre o Visual Studio](https://devblogs.microsoft.com/visualstudio/visual-studio-tips-and-tricks/)
- [Atalhos de teclado padrão para comandos usados com frequência](../ide/default-keyboard-shortcuts-for-frequently-used-commands-in-visual-studio.md)
- [Como: personalizar menus e barras de ferramentas](../ide/how-to-customize-menus-and-toolbars-in-visual-studio.md)
- [Walkthrough: criar um aplicativo simples](../get-started/csharp/tutorial-wpf.md)
- [Dicas e truques de acessibilidade](../ide/reference/accessibility-tips-and-tricks.md)