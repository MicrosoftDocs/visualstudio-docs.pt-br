---
title: Recursos do editor de códigos no Visual Studio
ms.date: 02/23/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- code, editing [Visual Studio]
- code editor [Visual Studio]
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8be5d3692459c2c65d4243c831ef4de002828bb0
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349069"
---
# <a name="features-of-the-code-editor"></a>Recursos do editor de código

O editor do Visual Studio fornece muitos recursos que facilitam escrever e gerenciar seu código e texto. Você pode expandir e recolher blocos de código diferentes usando a estrutura de tópicos. Você pode aprender mais sobre o código através do IntelliSense, do **Pesquisador de Objetos** e da Hierarquia de Chamada. Você pode localizar o código usando recursos como **Navegar Para**, **Ir para Definição** e **Localizar Todas as Referências**. Você pode inserir blocos de código com snippets de código e pode gerar código usando recursos como o **Gerar do uso**. Se você nunca usou o editor do Visual Studio, consulte [Editar o código](https://visualstudio.microsoft.com/vs/features/ide/) para obter uma visão geral rápida.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Editor de código-fonte (Visual Studio para Mac)](/visualstudio/mac/source-editor).

Você pode exibir seu código de várias maneiras diferentes. Por padrão, o **Gerenciador de Soluções** mostra seu código organizado por arquivos. Você pode clicar na guia **Modo de Exibição de Classe** na parte inferior da janela para exibir o código organizado por classes.

Você pode pesquisar e substituir texto em um ou vários arquivos. Para obter mais informações, consulte [Localizar e substituir texto](../ide/finding-and-replacing-text.md). É possível usar expressões regulares para localizar e substituir texto. Para obter mais informações, confira [Usar expressões regulares no Visual Studio](../ide/using-regular-expressions-in-visual-studio.md).

As diferentes linguagens do Visual Studio oferecem conjuntos de recursos diferentes e, em alguns casos, os recursos se comportam de forma diferente nas diferentes linguagens. Muitas dessas diferenças são especificadas nas descrições dos recursos, mas para obter mais informações, consulte as seções sobre as linguagens específicas do Visual Studio.

## <a name="editor-features"></a>Recursos do editor

|||
|-|-|
|Coloração de sintaxe|Alguns elementos de sintaxe dos arquivos de código e de marcação são coloridos de maneiras diferentes para diferenciá-los. Por exemplo, palavras-chave (como `using` no C# e `Imports` no Visual Basic) são de uma cor, mas tipos (como `Console` e `Uri`) são de outra cor. Outros elementos de sintaxe também são coloridos, como comentários e literais de cadeia de caracteres. O C++ usa cores para fazer diferenciação entre tipos, enumerações e macros, entre outros tokens.<br /><br /> Você pode ver a cor padrão de cada tipo e pode alterar a cor de qualquer elemento de sintaxe específico na [caixa de diálogo Fontes e Cores, Ambiente, Opções](../ide/reference/fonts-and-colors-environment-options-dialog-box.md), que pode ser aberta no menu **Ferramentas**.|
|Marcas de Erro e Aviso|Enquanto adiciona código e compila sua solução, você pode ver: (a)sublinhados ondulados de cores diferentes (conhecidos como rabiscos) ou (b) lâmpadas que aparecem em seu código. Rabiscos vermelhos indicam erros de sintaxe, azul indica erros de compilador, verde indica avisos e roxo indica outros tipos de erros. As [Ações Rápidas](../ide/quick-actions.md) sugerem correções para problemas e facilitam a aplicação da correção.<br /><br /> Você pode ver a cor padrão de cada rabisco de erro e de aviso na caixa de diálogo **Ferramentas** > **Opções** > **Ambiente** > **Fontes e Cores**. Procure por **Erro de Sintaxe**, **Erro do Compilador**, **Aviso** e **Outro Erro**.|
|Correspondência de chave|Quando o ponto de inserção é colocado em uma chave de abertura em um arquivo de código, essa chave de abertura e a chave de fechamento são realçadas. Esse recurso fornece comentários imediatos sobre chaves no local incorreto ou ausentes. Você pode ativar ou desativar a correspondência de chaves com a configuração **Realce Automático de Delimitadores** (**Ferramentas** > **Opções** > **Editor de Texto**). Você pode alterar a cor do realce na configuração **Fontes e Cores** (**Ferramentas** > **Opções** > **Ambiente**). Procure **Correspondência de Chaves (Realce)** ou **Correspondência de Chaves (Retângulo)**.|
|Visualizador de Estrutura|Linhas pontilhadas conectam chaves correspondentes nos arquivos de código, o que facilita ver a abertura e o fechamento de pares de chave. Isso pode ajudar a localizar o código em sua base de código mais rapidamente. Você pode ativar ou desativar essas linhas em **Mostrar diretrizes de estrutura** na seção **Exibição** da página **Ferramentas** > **Opções** > **Editor de Texto** > **Geral**.|
|Números de Linha|Os números de linha podem ser exibidos na margem esquerda da janela de código. Eles não são exibidos por padrão. Você poderá ativar essa opção nas configurações **Todas as Linguagens do Editor de Texto** (**Ferramentas** > **Opções** > **Editor de Texto** > **Todas as Linguagens**). Você pode exibir números de linha para linguagens de programação individuais, alterando as configurações para essas linguagens (**Ferramentas** > **Opções** > **Editor de Texto** > **\<linguagem>**). Para imprimir os números de linha é necessário selecionar **Incluir números de linha** na caixa de diálogo **Imprimir**.|
|Controle de Alterações|A cor da margem esquerda permite que você mantenha o controle das alterações feitas em um arquivo. As alterações que foram feitas desde que o arquivo foi aberto mas não foram salvas são indicadas por uma barra amarela na margem esquerda (conhecida como a margem de seleção). Depois de salvar as alterações (mas antes de fechar o arquivo), a barra ficará verde. Se você desfizer uma alteração depois de salvar o arquivo, a barra ficará laranja. Para desativar e ativar esse recurso, altere a opção **Controlar Alterações** nas configurações **Editor de Texto** (**Ferramentas** > **Opções** > **Editor de Texto**).|
|Seleção de código e texto|É possível selecionar texto no modo padrão de fluxo contínuo ou no modo de caixa, no qual você seleciona uma parte retangular do texto em vez de um conjunto de linhas. Para fazer uma seleção no modo de caixa, pressione a tecla **Alt** enquanto arrasta o mouse sobre a seleção (ou pressione **Alt**+**Shift**+**\<tecla de direção>**). A seleção inclui todos os caracteres dentro do retângulo definido pelo primeiro caractere e o último caractere na seleção. Tudo que é digitado ou colado na área selecionada é inserido no mesmo ponto em cada linha.|
|Aplicar Zoom|Você pode ampliar ou reduzir em qualquer janela de código pressionando a tecla **Ctrl** e, mantendo-a pressionada, mover a roda de rolagem do mouse (ou **Ctrl**+**Shift**+**).** para aumentar e **Ctrl**+**Shift**+**,** para diminuir). Você também pode usar a caixa **Zoom** no canto inferior esquerdo da janela de código para definir um percentual específico de zoom. O recurso de aplicar zoom não funciona em janelas de ferramentas.|
|Espaço virtual|Por padrão, as linhas nos editores do Visual Studio terminam após o último caractere, de forma que a tecla **Seta para a Direita**, ao final de uma linha, move o cursor para o início da próxima linha. Em alguns editores uma linha não termina depois do último caractere e é possível colocar o cursor em qualquer lugar na linha. Você pode habilitar o espaço virtual no editor nas configurações **Ferramentas** > **Opções** > **Editor de Texto** > **Todas as Linguagens**. Observe que você pode habilitar **Espaço virtual** ou **Quebra automática de linha**, mas não ambos.|
|Imprimindo|Você pode usar as opções da caixa de diálogo **Imprimir** para incluir números de linha ou ocultar regiões de código recolhidas ao imprimir um arquivo. Na caixa de diálogo **Configuração de Página** também é possível imprimir o caminho completo e o nome do arquivo, escolhendo **Cabeçalho de Página**.<br /><br /> Você pode definir opções de impressão a cores na caixa de diálogo **Ferramentas** > **Opções** > **Ambiente** > **Fontes e Cores**. Escolha **Impressora** na lista **Mostrar configurações de** para personalizar a impressão a cores. Você pode especificar cores para imprimir um arquivo diferentes das cores para edição de um arquivo.|
|Desfazer global e Refazer|O comandos **Desfazer Última Ação Global** e **Refazer Última Ação Global** no menu **Editar** desfazem ou refazem ações globais que afetam vários arquivos. As ações globais incluem renomeação de uma classe ou namespace, executar uma operação de localização e substituição em uma solução, refatoração de um banco de dados ou qualquer outra ação que altera vários arquivos. Você pode aplicar os comandos desfazer e refazer global para ações na sessão atual do Visual Studio, mesmo depois de fechar a solução na qual a ação foi aplicada.|

## <a name="advanced-editing-features"></a>Recursos de edição avançada

Você pode encontrar uma série de recursos avançados no menu **Editar** > **Avançado** na barra de ferramentas. Nem todos esses recursos estão disponíveis para todos os tipos de arquivos de código.

|||
|-|-|
|[Formatar Documento](code-styles-and-quick-actions.md#format-document-command)|Define o recuo adequado das linhas de código e move as chaves para separar linhas no documento.|
|Formatar Seleção|Define o recuo adequado das linhas de código e move as chaves para separar linhas na seleção.|
|Tabular linhas selecionadas|Troca espaços à esquerda por tabulações quando for apropriado.|
|Cancelar tabulação das linhas selecionadas|Troca tabulações à esquerda por espaços. Se você desejar converter todos os espaços em seu arquivo para tabulações (ou todas as tabulações para espaços), você poderá usar os comandos `Edit.ConvertSpacesToTabs` e `Edit.ConvertTabsToSpaces`. Esses comandos não são exibidos nos menus do Visual Studio, mas você pode chamá-los por meio da janela **Acesso Rápido** ou da janela Comando.|
|Colocar em Maiúsculas|Alterar todos os caracteres na seleção para maiúsculos ou se não houver nenhuma seleção, altera o caractere no ponto de inserção para maiúsculo.|
|Colocar em Minúsculas|Alterar todos os caracteres na seleção para minúsculos ou se não houver nenhuma seleção, altera o caractere no ponto de inserção para minúsculo.|
|Mover linhas selecionadas para cima|Move a linha selecionada uma linha para cima. Atalho: **Alt**+**Seta para Cima**.|
|Mover Linhas Selecionadas para Baixo|Move a linha selecionada uma linha para baixo. Atalho: **Alt**+**Seta para Baixo**.|
|Excluir Espaço em Branco Horizontal|Exclui tabulações ou espaços ao final da linha atual.|
|Exibir Espaço em Branco|Exibe espaços como pontos elevados e tabulações como setas. O final de um arquivo é exibido como um glifo retangular. Se **Ferramentas** > **Opções** > **Editor de Texto** > **Todas as Linguagens** > **Quebra automática de linha** > **Mostrar glifos visíveis para quebra automática de linha** estiver selecionado, esse glifo também será exibido.|
|Quebra automática de linha|Faz com que todas as linhas em um documento sejam visíveis na janela de código. Você pode ativar e desativar a quebra automática de linha nas configurações **Todas as Linguagens do Editor de Texto** (**Ferramentas** > **Opções** > **Editor de Texto** > **Todas as Linguagens**).|
|Comentar Seleção|Adiciona caracteres de comentários na seleção ou na linha atual.|
|Remover Comentários da Seleção|Remove caracteres de comentários da seleção ou da linha atual.|
|Aumentar recuo de linha|Adiciona uma tabulação (ou os espaços equivalentes) nas linhas selecionadas ou na linha atual.|
|Diminuir recuo de linha|Remove uma tabulação (ou os espaços equivalentes) das linhas selecionadas ou da linha atual.|
|Selecionar Marca|Em um documento que contém marcas (por exemplo, XML ou HTML), seleciona a marca.|
|Selecionar Conteúdo da Marca|Em um documento que contém marcas (por exemplo, XML ou HTML), seleciona o conteúdo.|

## <a name="navigate-and-find-code"></a>Navegar e localizar código

Você pode se mover pelo editor de códigos de várias maneiras diferentes, incluindo navegar para trás e para frente até pontos de inserção anteriores, exibir a definição de um tipo ou membro e saltar até um método específico, usando a barra de navegação. Para obter mais informações, consulte [Navegar pelo código](navigating-code.md).

## <a name="find-references-in-your-code-base"></a>Localizar referências na base de código

Para localizar onde os elementos de código específicos são referenciados em toda a sua base de código, é possível usar o comando **Localizar Todas as Referências**. Além disso, quando você clica em um tipo ou membro, o recurso **realce de referência** destaca automaticamente todas as referências a esse tipo ou membro. Para obter mais informações, confira [Localizar referências no código](finding-references.md).

## <a name="customize-the-editor"></a>Personalizar o editor

É possível compartilhar configurações do Visual Studio com outro desenvolvedor, fazer com que suas configurações estejam em conformidade com um padrão ou retornar às configurações padrão do Visual Studio usando o comando **Assistente de Importação e Exportação de Configurações** no menu **Ferramentas**. No **Assistente de Importação e Exportação de Configurações**, é possível alterar configurações gerais selecionadas ou idioma e configurações específicas do projeto.

Para definir novas teclas de atalho ou redefinir as teclas de atalho existentes, vá até **Ferramentas** > **Opções** > **Ambiente** > **Teclado**. Para saber mais sobre teclas de atalho, veja [Atalhos de teclado padrão](../ide/default-keyboard-shortcuts-in-visual-studio.md).

Para obter mais informações sobre como personalizar o editor, consulte [Personalizar o editor](../ide/customizing-the-editor.md). Para conferir opções do editor específicas ao JavaScript, confira [Opções do editor de JavaScript](../ide/reference/options-text-editor-javascript-formatting.md).

## <a name="see-also"></a>Consulte também

- [Editor de código-fonte (Visual Studio para Mac)](/visualstudio/mac/source-editor)
- [Visual Studio IDE](../ide/visual-studio-ide.md)
- [Introdução ao C++ no Visual Studio](../ide/getting-started-with-cpp-in-visual-studio.md)
- [Introdução ao C# e ao ASP.NET no Visual Studio](../ide/tutorial-csharp-aspnet-core.md)
- [Introdução ao Python no Visual Studio](../ide/quickstart-python.md)