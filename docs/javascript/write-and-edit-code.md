---
title: Introdução à edição para desenvolvedores do JavaScript
description: Esta introdução ao editor de códigos do Visual Studio mostra algumas das formas pelas quais o Visual Studio facilita a escrita, a navegação e o entendimento do código JavaScript.
ms.date: 12/13/2018
ms.topic: how-to
author: mikejo5000
ms.author: mikejo
manager: jillfra
dev_langs:
- JavaScript
ms.workload:
- nodejs
ms.openlocfilehash: 0f4fff1b13f8e3827d685ee16ccea55e78f733a6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85289086"
---
# <a name="learn-to-use-the-code-editor"></a>Saiba como usar o editor de códigos

Nesta breve introdução ao editor de códigos do Visual Studio, examinaremos algumas das formas pelas quais o Visual Studio facilita a escrita, a navegação e o entendimento do código.

> [!TIP]
> Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/) para instalá-lo gratuitamente. Dependendo do tipo de desenvolvimento de aplicativo que você estiver fazendo, talvez você precise instalar a **carga de trabalho de desenvolvimento em Node.js** com o Visual Studio.

Este artigo pressupõe que você já esteja familiarizado com o desenvolvimento em JavaScript. Caso contrário, sugerimos que você primeiro examine um tutorial, como [Criar um aplicativo Node.js e Express](../javascript/tutorial-nodejs.md).

## <a name="add-a-new-project-file"></a>Adicionar um novo arquivo de projeto

Você pode usar o IDE para adicionar novos arquivos ao projeto.

1. Com o projeto aberto no Visual Studio, clique com o botão direito do mouse em uma pasta ou no nó do projeto no Gerenciador de soluções (painel direito) e escolha **Adicionar**  >  **novo item**.

1. Na caixa de diálogo **Novo Arquivo**, na categoria **Geral**, escolha o tipo de arquivo que deseja adicionar, como **Arquivo JavaScript** e, em seguida, escolha **Abrir**.

    O novo arquivo será adicionado ao projeto e aberto no editor.

## <a name="use-intellisense-to-complete-words"></a>Usar o IntelliSense para completar palavras

O IntelliSense é um recurso muito útil durante a codificação. Ele pode mostrar informações sobre membros disponíveis de um tipo ou detalhes de parâmetros para sobrecargas diferentes de um método. No código a seguir, ao digitar `Router()`, você verá os tipos de argumento que podem ser passados. Isso é chamado de ajuda da assinatura.

![Usar o IntelliSense](../javascript/media/write-code-signature-checking.png)

Você também pode usar o IntelliSense para completar uma palavra depois que você digitar caracteres suficientes para desambiguá-la. Se você colocar o cursor após a cadeia de caracteres `data` no código a seguir e digitar `get`, o IntelliSense mostrará as funções definidas anteriormente no código ou definidas em uma biblioteca de terceiros adicionada ao projeto.

![Usar o IntelliSense](../javascript/media/write-code-intellisense.png)

O IntelliSense também pode mostrar informações sobre tipos quando você focaliza elementos de programação.

Para fornecer informações do IntelliSense, o serviço de linguagem pode usar arquivos *d.ts* TypeScript e comentários JSDoc. Para as bibliotecas JavaScript mais comuns, os arquivos *d.ts* são adquiridos automaticamente. Para obter mais detalhes sobre como as informações do IntelliSense são adquiridas, confira [JavaScript IntelliSense](../ide/javascript-intellisense.md?toc=/visualstudio/javascript/toc.json)

## <a name="check-syntax"></a>Verificar sintaxe

O serviço de linguagem usa o ESLint para fornecer verificação de sintaxe e linting. Se você precisar definir opções para a verificação de sintaxe no editor, selecione **ferramentas**  >  **Opções**de  >  **JavaScript/TypeScript**  >  **refiapoção**de JavaScript/TypeScript. As opções de linting apontarão para o arquivo de configuração global do ESLint.

No código a seguir, você verá um realce de sintaxe verde (rabiscos verdes) na expressão. Passe o mouse sobre o realce de sintaxe.

![Exibir erro de sintaxe](../javascript/media/write-code-syntax-checking.png)

A última linha dessa mensagem informa que o serviço de linguagem esperava uma vírgula (`,`). O rabisco verde indica um aviso. Rabiscos vermelhos indicam um erro.

No painel inferior, clique na guia **Lista de Erros** para ver o aviso e a descrição, juntamente com o nome de arquivo e o número de linha.

![Exibir lista de erros](../javascript/media/write-code-error-list.png)

Corrija esse código adicionando a vírgula (`,`) antes de `"data"`.

## <a name="comment-out-code"></a>Comentar o código

A barra de ferramentas, que é a linha de botões sob a barra de menus no Visual Studio, pode ajudar a aumentar sua produtividade durante a codificação. Por exemplo, você pode alternar o modo de preenchimento do IntelliSense (o [IntelliSense](../ide/using-intellisense.md) é um recurso de codificação que exibe uma lista de correspondência de métodos, entre outras coisas), aumentar ou diminuir um recuo de linha ou comentar um código que você não deseja compilar. Nesta seção, comentaremos alguns códigos.

Selecione uma ou mais linhas de código no editor e, em seguida, escolha o botão **Comentar as linhas selecionadas**![botão Comentar](../javascript/media/write-code-comment-out.png) na barra de ferramentas. Se preferir usar o teclado, pressione **Ctrl** + **K**, **Ctrl** + **C**.

Os caracteres de comentário `//` do JavaScript são adicionados ao início de cada linha selecionada para comentar o código.

## <a name="collapse-code-blocks"></a>Recolher blocos de código

Caso precise organizar a exibição de algumas regiões de código, você poderá recolhê-lo. Escolha a caixa cinza pequena com o sinal de subtração na margem da primeira linha de uma função. Ou, se você for um usuário de teclado, coloque o cursor em qualquer lugar no código do construtor e pressione **Ctrl** + **m**, **Ctrl** + **m**.

![Botão Recolher estrutura de tópicos](../javascript/media/write-code-collapse-code.png)

O bloco de código é recolhido apenas na primeira linha, seguido por um sinal de reticências (`...`). Para expandir o bloco de código novamente, clique na mesma caixa cinza que agora tem um sinal de adição ou pressione **Ctrl** + **m**, **Ctrl** + **m** novamente. Essa funcionalidade é chamada [Estrutura de tópicos](../ide/outlining.md) e é especialmente útil ao recolher funções longas ou classes inteiras.

## <a name="view-definitions"></a>Exibir definições

O editor do Visual Studio torna mais fácil inspecionar a definição de um tipo, função, etc. Uma maneira é navegar até o arquivo que contém a definição, por exemplo, escolhendo **ir para definição** em qualquer lugar em que o elemento de programação é referenciado. Uma maneira ainda mais rápida que não move o foco para fora do arquivo em que você está trabalhando é usar a opção [Inspecionar Definição](../ide/go-to-and-peek-definition.md#peek-definition). Vamos inspecionar a definição do método `render` no exemplo abaixo.

Clique com o botão direito do mouse em `render` e escolha **Inspecionar Definição** no menu de conteúdo. Ou pressione **ALT** + **F12**.

   Uma janela pop-up é exibida com a definição do método `render`. Você pode rolar na janela pop-up ou até mesmo inspecionar a definição de outro tipo do código inspecionado.

   ![Inspecionar janela de definição](../javascript/media/write-code-peek-definition.png)

Feche a janela de definição inspecionada ao selecionar a caixa pequena com um “x” no canto superior direito da janela pop-up.

## <a name="use-code-snippets"></a>Usar snippets de código

O Visual Studio fornece *snippets de código* úteis que você pode usar para gerar os blocos de código usados com frequência de forma rápida e fácil. Os [snippets de código](../ide/code-snippets.md) estão disponíveis para diferentes linguagens de programação, incluindo JavaScript. Vamos adicionar um loop `for` ao arquivo de código.

Coloque o cursor onde você deseja inserir o trecho de código, clique com o botão direito do mouse **e escolha trecho de código de**  >  **inserção**.

![Snippet de código no Visual Studio](../javascript/media/write-code-insert-snippet.png)

Uma caixa **Inserir Snippet** é exibida no editor. Escolha **Geral** e, em seguida, clique duas vezes no item **for** da lista.

![Snippet de código para um loop for no Visual Studio](../javascript/media/write-code-insert-snippet-for-loop.png)

Isso adiciona o snippet de loop `for` ao código:

```javascript
for (var i = 0; i < length; i++) {

}
```

Você pode examinar os trechos de código disponíveis para a sua linguagem escolhendo **Editar**  >  **IntelliSense**  >  **trecho**do IntelliSense INSERT e, em seguida, escolhendo a pasta do seu idioma.

## <a name="see-also"></a>Veja também

- [Trechos de código](../ide/code-snippets.md)
- [Navegue pelos códigos](../ide/navigating-code.md)
- [Estrutura de tópicos](../ide/outlining.md)
- [Ir para Definição e Definição de Pico](../ide/go-to-and-peek-definition.md)
- [Refatoração](../ide/refactoring-in-visual-studio.md)
- [Usar o IntelliSense](../ide/using-intellisense.md)
