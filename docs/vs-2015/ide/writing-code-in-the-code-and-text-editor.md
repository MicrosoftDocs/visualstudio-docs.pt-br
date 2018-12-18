---
title: Escrevendo código no Code e no Editor de Texto | Microsoft Docs
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
- vs.texteditor
dev_langs:
- JScript
- VB
- CSharp
helpviewer_keywords:
- code editor, word wrap
- outlining
- code, editing
- squiggles
- code editor, outlining
- code editor, error and warning markers
- word wrap
- code editor, syntax coloring
- code editor, go to definition
- diff
- code editor [Visual Studio]
- code editor, diff
- error and warning markers
- code editor, navigation bar
- code editor, customizing
- comment selection
- code editor, tabify
- brace matching
- code editor, line numbers
- printing
- code editor, brace matching
- code editor, squiggles
- code editor, features
- line numbers
- go to definition
- syntax coloring
- code editor, navigate to
- code editor, comparing files
- code editor, zoom
- code editor
- code files
- go to line
- tabify
- zoom
- navigate to
- line break characters
- code editor, virtual space
- code editor, change tracking
- code editor, comment selection
- code editor, printing
- virtual space
- code editor, line break characters
- code editor, go to line
- code
ms.assetid: cb53ab9a-5b76-4759-b9e8-7bf32298ecbe
caps.latest.revision: 46
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: bd12cfee50db7dd085fee6c0591dfff3f579e640
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49838680"
---
# <a name="writing-code-in-the-code-and-text-editor"></a>Escrevendo código no editor de códigos e de texto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]
O editor do Visual Studio fornece muitos recursos que tornam mais fácil para você escrever e gerenciar seu código. Você pode expandir e recolher blocos de código diferentes usando a estrutura de tópicos. Você pode aprender mais sobre o código que você está usando através do IntelliSense, do **Pesquisador de Objetos** e da Hierarquia de Chamada. Você pode navegar dentro de seu código usando recursos como **Navegar Para**, **Ir para Definição** e **Localizar Todas as Referências**. Você pode inserir blocos de código com snippets de código e pode gerar código usando recursos como o **Gerar do uso**. Se você nunca usou o editor do Visual Studio 2015, consulte [Editando seu código](https://www.visualstudio.com/features/ide-vs) para uma visão geral rápida.  

 Você pode exibir seu código de várias maneiras diferentes. Para ver um modo de exibição de classe de sua solução, você pode abrir a janela **Modo de Exibição de Classe** ou expandir os nós no **Gerenciador de Soluções** em seus arquivos de classe.  

 Você pode pesquisar e substituir texto para um ou vários arquivos. Para obter mais informações, consulte [Localizando e substituindo texto](../ide/finding-and-replacing-text.md). Se você usar expressões regulares, observe que localizar e substituir agora usa expressões regulares do .NET. Para obter mais informações, consulte [Usando expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).  

 As diferentes linguagens do Visual Studio oferecem conjuntos de recursos diferentes e, em alguns casos, os recursos se comportam de forma diferente nas diferentes linguagens. Muitas dessas diferenças são especificadas nas descrições dos recursos, mas para obter mais informações, consulte as seções sobre as linguagens específicas do Visual Studio.  

> [!IMPORTANT]
>  A edição do Visual Studio e as configurações que você está usando podem afetar os recursos no IDE. Eles podem ser diferentes dos descritos neste tópico.  

## <a name="editor-features"></a>Recursos do Editor  

|||  
|-|-|  
|Coloração de sintaxe|Alguns elementos de sintaxe dos arquivos de código e de marcação são coloridos de maneiras diferentes para diferenciá-los. Por exemplo, palavras-chave (como `using` no C# e `Imports` no Visual Basic) são de uma cor, mas tipos (como `Console` e `Uri`) são de outra cor. Outros elementos de sintaxe também são coloridos, como comentários e literais de cadeia de caracteres. O C++ usa cores para fazer diferenciação entre tipos, enumerações e macros, entre outros tokens.<br /><br /> Você pode ver a cor padrão de cada tipo e pode alterar a cor de qualquer elemento de sintaxe específico na [caixa de diálogo Fontes e Cores, Ambiente, Opções](../ide/reference/fonts-and-colors-environment-options-dialog-box.md), que pode ser aberta no menu **Ferramentas**.|  
|Marcas de Erro e Aviso|Enquanto adiciona código e compila sua solução, você pode ver: (a)sublinhados ondulados de cores diferentes (conhecidos como rabiscos) ou (b) lâmpadas que aparecem em seu código. Rabiscos vermelhos indicam erros de sintaxe, azul indica erros de compilador, verde indica avisos e roxo indica outros tipos de erros. [As lâmpadas](../ide/perform-quick-actions-with-light-bulbs.md) sugerem correções para problemas e facilitam a aplicação da correção.<br /><br /> Você pode ver a cor padrão de cada rabisco de erro e de aviso na caixa de diálogo **Ferramentas/Opções/Ambiente/Fontes e Cores**. Procure por **Erro de Sintaxe**, **Erro do Compilador**, **Aviso** e **Outro Erro**.|  
|Correspondência de chave|Quando o ponto de inserção é colocado em uma chave de abertura em um arquivo de código, essa chave de abertura e a chave de fechamento são realçadas. Esse recurso fornece comentários imediatos sobre chaves no local incorreto ou ausentes. Você pode ativar ou desativar a correspondência de chaves com a configuração **Realce automático de delimitadores** (**Ferramentas/Opções/Editor de Texto**). Você pode alterar a cor do realce na configuração **Fontes e Cores** (**Ferramentas/Opções/Ambiente**). Procure **Correspondência de Chaves (Realce)** ou **Correspondência de Chaves (Retângulo)**.|  
|Números de Linha|Os números de linha podem ser exibidos na margem esquerda da janela de código. Eles não são exibidos por padrão. Você poderá ativar essa opção nas configurações **Todas as Linguagens do Editor de Texto** (**Ferramentas/Opções/Editor de Texto/Todas as Linguagens**). Você pode exibir números de linha para linguagens de programação individuais, alterando as configurações para essas linguagens (**Ferramentas/Opções/Editor de Texto/\<linguagem>**). Para imprimir os números de linha é necessário selecionar Incluir números de linha na caixa de diálogo **Imprimir**.|  
|Controle de Alterações|A cor da margem esquerda permite que você mantenha o controle das alterações feitas em um arquivo. As alterações que foram feitas desde que o arquivo foi aberto mas não foram salvas são indicadas por uma barra amarela na margem esquerda (conhecida como a margem de seleção). Depois de salvar as alterações (mas antes de fechar o arquivo), a barra ficará verde. Se você desfizer uma alteração depois de salvar o arquivo, a barra ficará laranja. Para desativar e ativar esse recurso, altere a opção **Controlar Alterações** nas configurações **Editor de Texto** (**Ferramentas/Opções/Editor de Texto**).|  
|Seleção de código e texto|É possível selecionar texto no modo padrão de fluxo contínuo ou no modo de caixa, no qual você seleciona uma parte retangular do texto em vez de um conjunto de linhas. Para fazer uma seleção no modo de caixa, pressione a tecla ALT enquanto arrasta o mouse sobre a seleção (ou pressione ALT + SHIFT + \<tecla de direção>). A seleção inclui todos os caracteres dentro do retângulo definido pelo primeiro caractere e o último caractere na seleção. Tudo que é digitado ou colado na área selecionada é inserido no mesmo ponto em cada linha.|  
|Aplicar Zoom|Você pode ampliar ou reduzir em qualquer janela de código pressionando a tecla CTRL e, mantendo-a pressionada, mover a roda de rolagem do mouse (ou CTRL + SHIFT +. para aumentar e CTRL + SHIFT +, para diminuir). Você também pode usar a caixa de Zoom no canto inferior esquerdo da janela de código para definir um percentual específico de aplicação de zoom. O recurso de aplicar zoom não funciona em janelas de ferramentas.|  
|Espaço virtual|Por padrão, as linhas nos editores do Visual Studio terminam após o último caractere de forma que a tecla SETA PARA A DIREITA, ao final de uma linha, move o cursor para o início da próxima linha. Em alguns editores uma linha não termina depois do último caractere e é possível colocar o cursor em qualquer lugar na linha. Você pode habilitar o espaço virtual no editor nas configurações **Ferramentas/Opções/Editor de Texto/Todas as Linguagens**. Observe que você pode habilitar **Espaço virtual** ou **Quebra automática de linha**, mas não ambos.|  
|Imprimindo|Você pode usar as opções da caixa de diálogo **Imprimir** para incluir números de linha ou ocultar regiões de código recolhidas ao imprimir um arquivo. Na caixa de diálogo **Configuração de Página** também é possível imprimir o caminho completo e o nome do arquivo, escolhendo **Cabeçalho de Página**.<br /><br /> Você pode definir opções de impressão a cores na caixa de diálogo **Ferramentas/Opções/Ambiente/Fontes e Cores**. Escolha **Impressora** na lista **Mostrar configurações de** para personalizar a impressão a cores. Você pode especificar cores para imprimir um arquivo diferentes das cores para edição de um arquivo.|  
|Desfazer global e Refazer|O comandos **Desfazer Última Ação Global** e **Refazer Última Ação Global** no menu **Editar** desfazem ou refazem ações globais que afetam vários arquivos. As ações globais incluem renomeação de uma classe ou namespace, executar uma operação de localização e substituição em uma solução, refatoração de um banco de dados ou qualquer outra ação que altera vários arquivos. Você pode aplicar os comandos desfazer e refazer global para ações na sessão atual do Visual Studio, mesmo depois de fechar a solução na qual a ação foi aplicada.|  

## <a name="advanced-editing-features"></a>Recursos de edição avançada  
 Você pode encontrar uma série de recursos avançados no submenu **Editar/Avançado**. Nem todos esses recursos estão disponíveis para todos os tipos de arquivos de código.  

|||  
|-|-|  
|Formatar Documento|Define o recuo adequado das linhas de código e move as chaves para separar linhas no documento.|  
|Formatar Seleção|Define o recuo adequado das linhas de código e move as chaves para separar linhas na seleção.|  
|Tabular linhas selecionadas|Troca espaços à esquerda por tabulações quando for apropriado.|  
|Cancelar tabulação das linhas selecionadas|Troca tabulações à esquerda por espaços. Se você desejar converter todos os espaços em seu arquivo para tabulações (ou todas as tabulações para espaços), você poderá usar os comandos `Edit.ConvertSpacesToTabs` e `Edit.ConvertTabsToSpaces`. Esses comandos não aparecem nos menus do Visual Studio, mas você pode chamá-los da janela de Acesso Rápido ou na janela Comando.|  
|Colocar em Maiúsculas|Alterar todos os caracteres na seleção para maiúsculos ou se não houver nenhuma seleção, altera o caractere no ponto de inserção para maiúsculo.|  
|Colocar em Minúsculas|Alterar todos os caracteres na seleção para minúsculos ou se não houver nenhuma seleção, altera o caractere no ponto de inserção para minúsculo.|  
|Validar Documento|Valida os arquivos de código JScript.|  
|Excluir Espaço em Branco Horizontal|Exclui tabulações ou espaços ao final da linha atual.|  
|Exibir Espaço em Branco|Exibe espaços como pontos elevados e tabulações como setas. O final de um arquivo é exibido como um glifo retangular. Se **Ferramentas/Opções/Editor de Texto/Todas as Linguagens/Quebra automática de linha/Mostrar glifos visíveis para quebra automática de linha** estiver selecionado, esse glifo também será exibido.|  
|Quebra automática de linha|Faz com que todas as linhas em um documento sejam visíveis na janela de código. Você pode ativar e desativar a quebra automática de linha na configuração Todas as Linguagens do Editor de Texto (**Ferramentas/Opções/Editor de Texto/Todas as Linguagens**).|  
|Remover Comentários da Seleção|Adiciona caracteres de comentários na seleção ou na linha atual.|  
|Comentar Seleção|Remove caracteres de comentários da seleção ou da linha atual.|  
|Aumentar recuo de linha|Adiciona uma tabulação (ou os espaços equivalentes) nas linhas selecionadas ou na linha atual.|  
|Diminuir recuo de linha|Remove uma tabulação (ou os espaços equivalentes) das linhas selecionadas ou da linha atual.|  
|Selecionar Marca|Em um documento que contém marcas (por exemplo, XML ou HTML), seleciona a marca.|  
|Selecionar Conteúdo da Marca|Em um documento que contém marcas (por exemplo, XML ou HTML), seleciona o conteúdo.|  

## <a name="navigate-in-the-code-window"></a>Navegar na janela de código  
 Você pode se mover em um documento de várias maneiras diferentes. Além das operações padrão, você pode usar os botões **Navegar para Trás** (ou CTRL + SINAL DE SUBTRAÇÃO) e **Navegar para Frente** (CTRL + SHIFT + SINAL DE SUBTRAÇÃO) na barra de ferramentas para mover o ponto de inserção para locais anteriores ou retornar para locais mais recentes no documento ativo. Esses botões retém os últimos 20 locais do ponto de inserção.  

 ![Botões de navegação para frente e para trás](../ide/media/vs2015-nav-buttons.png "VS2015_Nav_buttons")  

 Você também pode usar a barra de rolagem avançada em uma janela de código para obter uma visão geral do seu código. No modo de mapa, você pode obter visualizações do código ao mover o cursor para cima e para baixo da barra de rolagem, para obter mais informações, consulte [Como controlar seu código personalizando a barra de rolagem](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md).  

 Os comandos a seguir são métodos de navegação específicos do código:  

|||  
|-|-|  
|Ir para \<número de linha>|(**Editar/Ir para** ou CTRL + G): mover-se até um número de linha específico no documento ativo.|  
|Navegar para|(**Editar/Navegar Para** ou CTRL + ,): localiza um símbolo ou um arquivo na solução ativa. Ele ajuda você a escolher um bom conjunto de resultados correspondentes de uma consulta. Você pode pesquisar por palavras-chave que estão contidas em um símbolo usando caracteres de minúsculas concatenadas e caracteres de sublinhado para dividir o símbolo em palavras-chave.|  
|Localizar Todas as Referências|(menu de contexto): localiza todas as referências ao elemento selecionado na solução.|  
|Ir para definição|(menu de contexto ou F12): localiza a definição do elemento selecionado.|  
|Inspecionar Definição|(menu de contexto ou Alt + F12): localiza a definição do elemento selecionado e a exibe em uma janela pop-up. Para obter mais informações, consulte [How to: View and Edit Code by Using Peek Definition (Alt+F12)](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md) (Como exibir e editar códigos usando Inspecionar Definição (Alt + F12)).|  
|Próximo método, Método anterior|(**Editar/Próximo método, Método anterior**) nos arquivos de código do Visual Basic, use estes comandos para mover o ponto de inserção para métodos diferentes.|  
|Realce de referência|Quando você clica em um símbolo no código-fonte, todas as instâncias desse símbolo são realçadas no documento. Os símbolos realçados podem incluir declarações e referências e muitos outros símbolos que **Localizar Todas as Referências** retornaria. Isso inclui os nomes de classes, objetos, variáveis, métodos e propriedades. No código do Visual Basic, as palavras-chave de muitas estruturas de controle também são realçadas. Para mover-se para o próximo símbolo realçado ou para o anterior, pressione CTRL + SHIFT + SETA PARA BAIXO ou CTRL + SHIFT + SETA PARA CIMA. Você pode alterar a cor do realce em **Ferramentas/Opções/Ambiente/Fontes e Cores/Referência Realçada.**|  
|Localizar informações relacionadas ao código|Você pode localizar informações sobre o código específico, como alterações e quem fez essas alterações, referências, bugs, itens de trabalho, revisões de código e status de teste de unidade ao usar o CodeLens no editor de código. O CodeLens funciona como uma exibição de alerta quando você usa o Visual Studio Enterprise com o Team Foundation Server. Consulte [Localizar alterações de código e outros históricos](../ide/find-code-changes-and-other-history-with-codelens.md).|  

 Você também pode usar o **barra de navegação**, ou seja, as duas caixas suspensas exibidas na parte superior da janela de código, para navegar em um arquivo de código. Essa barra permite que você navegue diretamente até um tipo específico ou até um dos membros dentro de um tipo. A barra de navegação aparece com arquivos de código do Visual Basic, do C# e do C++.  

 Para ocultar a barra de navegação, altere a opção **Barra de Navegação** na configuração Todas as Linguagens do Editor de Texto (**Ferramentas/Opções/Editor de Texto/Todas as Linguagens** ou você pode alterar as configurações de linguagens individuais). Você pode navegar nas caixas suspensas da seguinte maneira:  

- Para mudar o foco da janela de código para a barra de navegação, pressione a combinação de tecla de atalho CTRL + F2.  

- Para retornar o foco da barra de navegação para a janela de código, pressione a tecla ESC.  

- Para mudar o foco de um item ao outro item na barra de navegação, pressione a tecla TAB.  

- Para selecionar o item de Barra de navegação que tem o foco e retornar ao IDE, pressione a tecla ENTER  

- Para navegar até uma classe ou um tipo, clique em seu nome na lista suspensa à esquerda.  

- Para navegar diretamente até um procedimento em uma classe, clique em um procedimento na lista suspensa à direita.  

  Em uma classe parcial, os membros definidos fora do arquivo de código atual podem estar esmaecidos.  

## <a name="find-code-using-navigate-to"></a>Localizar código usando Navegar Para
Comando a "Navegar até" do Visual Studio faz uma pesquisa restrita do seu código para ajudá-lo a localizar rapidamente elementos especificados em arquivos de código, caminhos de arquivo e símbolos de código. Ao contrário de outras pesquisas de texto como Localizar ou Localizar nos Arquivos, o Navegar Para limita sua pesquisa às áreas em que o código real reside, como arquivos, formulários e módulos de código. Por exemplo, se você pesquisar uma cadeia de caracteres em um aplicativo Web ASP .NET usando Localizar ou Localizar nos Arquivos em toda a solução, você poderá obter várias ocorrências, incluindo instâncias da cadeia de caracteres nos comentários de código. Usando navegar para, no entanto, você pode apenas obter uma única função, ignorando todas as instâncias da cadeia de caracteres nos comentários de código.

### <a name="navigate-code-using-navigate-to"></a>Navegar no código usando Navegar Para

1. No Visual Studio, abra uma solução ou uma pasta.
1. No menu principal, escolha **Editar**, **Navegar Para** ou pressione **CTRL + ,**.

    Uma pequena caixa de texto é exibida no canto superior do editor de código.
1. Na caixa de texto, digite o nome do elemento de código que você deseja localizar.

    ![Janela Navegar Para](../ide/media/vside-navigatetowindow.png "Janela Navegar Para")

    Conforme você digita, os resultados são exibidos em uma lista suspensa abaixo da caixa de texto.
1. Para ir até um elemento, escolha-o na lista.


### <a name="filter-your-search"></a>Filtrar sua pesquisa

Para limitar a pesquisa a somente símbolos de código, preceda a consulta Navegar Para com um caractere “@”. Por exemplo, se você pesquisar `@application`, O Navegar Para exibe, por exemplo, somente as classes que têm a palavra "aplicativo" nelas.

Se você usar minúsculas concatenadas em seu código, você poderá encontrar elementos de código de forma mais rápida inserindo somente as letras maiúsculas do nome do elemento de código. Por exemplo, se o código tem um componente chamado `ViewSwitcher`, você poderá encontrá-lo inserindo apenas as letras maiúsculas do nome (`"VS"`) na janela do Navegar Para.

![Janela Navegar Para – pesquisando com maiúsculas](../ide/media/vside-capitalsearch.png "Janela Navegar Para – pesquisando com maiúsculas")

Esse recurso é particularmente útil se seu código tem nomes longos.

## <a name="customize-the-editor"></a>Personalizar o Editor  
 **Importar e exportar configurações**: você pode compartilhar configurações com outro desenvolvedor, fazer com que suas configurações estejam em conformidade com um padrão ou retornar às configurações padrão do Visual Studio usando o **Assistente de Importação e Exportação de Configurações** no menu **Ferramentas**. Você pode alterar as configurações gerais ou linguagens e configurações específicas do projeto.  

 **Mapeamento de teclado**: você pode definir novas teclas de atalho ou redefinir as existentes nas configurações Ferramentas/Opções/Ambiente/Teclado. Para obter mais informações sobre teclas de atalho, consulte [Atalhos de teclado padrão](../ide/default-keyboard-shortcuts-in-visual-studio.md).  

 Para obter informações sobre as opções do editor específicas a um idioma, consulte o seguinte:  

-   [Configurações do Visual Basic](http://msdn.microsoft.com/library/2712b3b1-18f2-430c-ae91-28468bbf5f32)  

-   [Usando o Ambiente de Desenvolvimento do Visual Studio para C#](../csharp-ide/using-the-visual-studio-development-environment-for-csharp.md)  

-   [Opções, Editor de Texto, JavaScript, Formatação](../ide/reference/options-text-editor-javascript-formatting.md)  

## <a name="in-this-section"></a>Nesta seção  

-   [Localizando e substituindo texto](../ide/finding-and-replacing-text.md)  

-   [Codificações e quebras de linha](../ide/encodings-and-line-breaks.md)  

-   [Estrutura de tópicos](../ide/outlining.md)  

-   [Refatoração](../ide/refactoring-in-visual-studio.md)  

-   [Dicas de produtividade](../ide/productivity-tips-for-visual-studio.md)  

-   [Usando o IntelliSense](../ide/using-intellisense.md)  

-   [Personalizando o editor](../ide/customizing-the-editor.md)  

-   [Como acompanhar o código personalizando a barra de rolagem](../ide/how-to-track-your-code-by-customizing-the-scrollbar.md)  

-   [Como exibir e editar o código usando Inspecionar Definição (Alt + F12)](../ide/how-to-view-and-edit-code-by-using-peek-definition-alt-plus-f12.md)  

-   [Realizar ações rápidas com lâmpadas](../ide/perform-quick-actions-with-light-bulbs.md)  

-   [Snippets de código](../ide/code-snippets.md)  

-   [Usando a caixa de ferramentas](../ide/using-the-toolbox.md)  

-   [Exibindo a estrutura do código](../ide/viewing-the-structure-of-code.md)  

-   [Configurando identificadores no código](../ide/setting-bookmarks-in-code.md)  

-   [Usando a Lista de Tarefas](../ide/using-the-task-list.md)  

-   [Localizar alterações de código e outros históricos](../ide/find-code-changes-and-other-history-with-codelens.md)  

## <a name="see-also"></a>Consulte também  
 [Visual Studio IDE](../ide/visual-studio-ide.md)


