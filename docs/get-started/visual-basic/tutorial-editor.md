---
title: Introdução à edição para desenvolvedores do Visual Basic
description: Esta introdução de 10 minutos ao editor de códigos do Visual Studio mostra algumas das formas pelas quais o Visual Studio facilita a escrita, a navegação e o entendimento do código Visual Basic.
ms.custom: seodec18, get-started
ms.date: 11/20/2018
ms.technology: vs-ide-general
ms.topic: tutorial
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- VB
ms.workload:
- dotnet
ms.openlocfilehash: 3af730ae4d5b358eab223e2a5a8288daaf632071
ms.sourcegitcommit: d3a485d47c6ba01b0fc9878cbbb7fe88755b29af
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/19/2019
ms.locfileid: "58069626"
---
# <a name="learn-to-use-the-code-editor"></a>Saiba como usar o editor de códigos

Nesta introdução de 10 minutos ao editor de código do Visual Studio, adicionaremos o código a um arquivo para ver algumas das formas pelas quais o Visual Studio facilita a escrita, a navegação e o entendimento do código.

> [!TIP]
> Se você ainda não tiver instalado o Visual Studio, acesse a página [Downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2017) para instalá-lo gratuitamente.

Este artigo pressupõe que você já esteja familiarizado com o Visual Basic. Caso contrário, sugerimos que você primeiro examine um tutorial, como [Introdução ao Visual Basic no Visual Studio](../../get-started/visual-basic/tutorial-console.md).

> [!TIP]
> Para acompanhar este artigo, verifique se você tem as configurações do Visual Basic selecionadas para o Visual Studio. Para obter informações sobre como selecionar configurações para o IDE (ambiente de desenvolvimento integrado), confira [Selecionar configurações de ambiente](visual-studio-ide.md#select-environment-settings).

## <a name="create-a-new-code-file"></a>Criar um novo arquivo de código

Comece criando um novo arquivo e adicionando códigos nele.

::: moniker range="vs-2017"

1. Abra o Visual Studio.

::: moniker-end

::: moniker range=">=vs-2019"

1. Abra o Visual Studio. Pressione **Esc** ou clique em **Continuar sem código** na janela de início para abrir o ambiente de desenvolvimento.

::: moniker-end

2. No menu **Arquivo** na barra de menus, escolha **Novo Arquivo**.

3. Na caixa de diálogo **Novo Arquivo**, na categoria **Geral**, escolha **Classe do Visual Basic** e, em seguida, escolha **Abrir**.

   Um novo arquivo é aberto no editor com o esqueleto de uma classe do Visual Basic. (Você já pode observar que não precisa criar um projeto completo do Visual Studio para obter alguns dos benefícios oferecidos pelo editor de códigos, como o realce de sintaxe. Basta ter um arquivo de código!)

   ![Arquivo de código Visual Basic no Visual Studio](media/tutorial-editor.png)

## <a name="use-code-snippets"></a>Usar snippets de código

O Visual Studio fornece *snippets de código* úteis que você pode usar para gerar os blocos de código usados com frequência de forma rápida e fácil. Os [snippets de código](../../ide/code-snippets.md) estão disponíveis para diferentes linguagens de programação, incluindo Visual Basic, C# e C++. Vamos adicionar o snippet **Sub** do Visual Basic ao nosso arquivo.

1. Coloque o cursor acima da linha que indica `End Class` e digite **sub**.

   Uma caixa de diálogo pop-up será exibida com informações sobre a palavra-chave `Sub` e como inserir o snippet de código **Sub**.

   ![IntelliSense para o snippet de código no Visual Studio](media/tutorial-intellisense-snippet.png)

1. Pressione a **Guia** duas vezes para inserir o snippet de código.

   A estrutura do código do procedimento Sub `MySub()` é adicionada ao arquivo.

Os snippets de código disponíveis variam em linguagens de programação diferentes. Examine os snippets de código disponíveis para o Visual Basic selecionando **Editar** > **IntelliSense** > **Inserir Snippet** (ou pressione **Ctrl**+**K**, **Ctrl**+**X**). Para o Visual Basic, os snippets de código estão disponíveis para as seguintes categorias:

![Lista de snippets de código do Visual Basic](media/tutorial-code-snippet-list.png)

Há snippets para determinar se existe um arquivo no computador, fazer uma gravação em um arquivo de texto, ler um valor de registro, executar uma consulta SQL, criar uma [instrução For Each...Next](/dotnet/visual-basic/language-reference/statements/for-each-next-statement), entre outros.

## <a name="comment-out-code"></a>Comentar o código

A barra de ferramentas, que é a linha de botões sob a barra de menus no Visual Studio, pode ajudar a aumentar sua produtividade durante a codificação. Por exemplo, você pode ativar/desativar o modo de preenchimento do IntelliSense, aumentar ou diminuir um recuo de linha ou comentar um código que não deseja compilar. (O [IntelliSense](../../ide/using-intellisense.md) é um recurso de codificação que exibe uma lista de métodos correspondentes, entre outras coisas.) Nesta seção, comentaremos alguns códigos.

![Botões de barra de ferramentas do editor](media/tutorial-editor-toolbar.png)

1. Cole o código a seguir no corpo do procedimento `MySub()`.

   ```vb
   ' _words is a string array that we'll sort alphabetically
   Dim _words = New String() {
   "the",
   "quick",
   "brown",
   "fox",
   "jumps"
   }

   Dim morewords = New String() {
   "over",
   "the",
   "lazy",
   "dog"
   }

   Dim query = From word In _words
               Order By word.Length
               Select word
   ```

1. Não estamos usando a matriz `morewords`, mas podemos usá-la mais tarde. Portanto, não queremos excluí-la por completo. Em vez disso, vamos comentar as linhas. Selecione a definição inteira de `morewords` até a chave de fechamento e, em seguida, escolha o botão **Comentar as linhas selecionadas** na barra de ferramentas. Caso prefira usar o teclado, pressione **Ctrl**+**K**, **Ctrl**+**C**.

   ![Botão de comentários](media/tutorial-comment-out.png)

   O caractere de comentário `'` do Visual Basic é adicionado ao início de cada linha selecionada para comentar o código.

## <a name="collapse-code-blocks"></a>Recolher blocos de código

Recolha seções de código para se concentrar apenas nas partes de seu interesse. Para praticar, vamos recolher a matriz `_words` para uma linha de código. Escolha a caixa cinza pequena com o sinal de subtração na margem da linha que indica `Dim _words = New String() {`. Ou, se você é um usuário de teclado, posicione o cursor em qualquer lugar da definição de matriz e pressione **Ctrl**+**M**, **Ctrl**+**M**.

![Botão Recolher estrutura de tópicos](media/tutorial-collapse.png)

O bloco de código é recolhido apenas na primeira linha, seguido por um sinal de reticências (`...`). Para expandir o bloco de código novamente, clique na mesma caixa cinza que agora tem um sinal de adição ou pressione **Ctrl**+**M**, **Ctrl**+**M** novamente. Esse recurso é chamado de [Estrutura de tópicos](../../ide/outlining.md) e é útil principalmente ao recolher métodos longos ou classes inteiras.

## <a name="view-symbol-definitions"></a>Exibir definições de símbolo

O editor do Visual Studio facilita a inspeção da definição de um tipo, de um método, etc. Uma maneira é navegar até o arquivo que contém a definição, por exemplo, ao selecionar **Ir para Definição** em qualquer lugar em que o símbolo esteja referenciado. Uma maneira ainda mais rápida que não move o foco para fora do arquivo em que você está trabalhando é usar a opção [Inspecionar Definição](../../ide/go-to-and-peek-definition.md#peek-definition). Vamos espiar a definição do tipo `String`.

1. Clique com o botão direito do mouse na palavra `String` e escolha **Inspecionar Definição** no menu de conteúdo. Se preferir, pressione **Alt**+**F12**.

   Uma janela pop-up será exibida com a definição da classe `String`. Você pode rolar na janela pop-up ou até mesmo inspecionar a definição de outro tipo do código inspecionado.

   ![Inspecionar janela de definição](media/tutorial-peek-definition.png)

1. Feche a janela de definição inspecionada ao selecionar a caixa pequena com um “x” no canto superior direito da janela pop-up.

## <a name="use-intellisense-to-complete-words"></a>Usar o IntelliSense para completar palavras

O [IntelliSense](../../ide/using-intellisense.md) é um recurso valioso quando você está gravando o código. Ele pode mostrar informações sobre membros disponíveis de um tipo ou detalhes de parâmetros para sobrecargas diferentes de um método. Você também pode usar o IntelliSense para completar uma palavra depois que você digitar caracteres suficientes para desambiguá-la. Vamos adicionar uma linha de código para imprimir as cadeias de caracteres ordenadas na janela de console, que é o local padrão para envio da saída do programa.

1. Abaixo da variável `query`, comece a digitar o código a seguir:

   ```vb
   For Each str In qu
   ```

   Você verá o IntelliSense mostrar as **Informações Rápidas** sobre o símbolo `query`.

   ![Preenchimento de palavras do IntelliSense no Visual Studio](media/tutorial-intellisense-completion-list.png)

1. Para inserir o restante da palavra `query` usando a funcionalidade de preenchimento de palavras do IntelliSense, pressione **Tab**.

1. Finalize o bloco de código para que ele se pareça com o seguinte código.

   ```vb
   For Each str In query
       Console.WriteLine(str)
   Next
   ```

## <a name="refactor-a-name"></a>Refatorar um nome

Ninguém obtém o código correto na primeira vez e uma das coisas que talvez você precise alterar é o nome de uma variável ou de um método. Vamos experimentar a funcionalidade de [refatorar](../../ide/refactoring-in-visual-studio.md) do Visual Studio para renomear a variável `_words` como `words`.

1. Coloque o cursor sobre a definição da variável `_words` e escolha **Renomear** no menu de atalho ou de contexto.

   Uma caixa de diálogo pop-up chamada **Renomear** aparecerá no canto superior direito do editor.

1. Com a variável `_words` ainda selecionada, digite o nome desejado de **words**. Observe que a referência ao `words` na consulta também será renomeada automaticamente. Antes de pressionar **Enter** ou clicar em **Aplicar**, marque a caixa de seleção **Incluir comentários** na caixa pop-up **Renomear**.

   ![Caixa de diálogo Renomear](media/tutorial-rename.png)

1. Pressione **Enter** ou clique em **Aplicar**.

   As duas ocorrências de `words` serão renomeadas, bem como a referência a `words` no comentário do código.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Saiba mais sobre projetos e soluções](tutorial-projects-solutions.md)

## <a name="see-also"></a>Consulte também

- [Snippets de código](../../ide/code-snippets.md)
- [Navegar pelo código](../../ide/navigating-code.md)
- [Estrutura de tópicos](../../ide/outlining.md)
- [Ir para Definição e Definição de Pico](../../ide/go-to-and-peek-definition.md)
- [Refatoração](../../ide/refactoring-in-visual-studio.md)
- [Usar o IntelliSense](../../ide/using-intellisense.md)