---
title: Adicionar suporte do editor para outros idiomas
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- syntax colorization
- IntelliSense
- IDE, navigation
- documents [Visual Studio], navigation
- TextMate bundle
- TextMate language grammar
- language support
ms.assetid: d78c43ee-4ef2-42e5-984e-d137de4e7e92
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 247567030d47a55b29a3fca901e12948ddd85916
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85533751"
---
# <a name="add-visual-studio-editor-support-for-other-languages"></a>Adicionar suporte para outras linguagens ao editor do Visual Studio

Saiba mais sobre como o editor do Visual Studio dá suporte à leitura e à navegação por meio de diferentes linguagens de computador e como é possível adicionar suporte ao editor do Visual Studio para outras linguagens.

## <a name="syntax-colorization-statement-completion-and-navigate-to-support"></a>Colorização de sintaxe, preenchimento de declaração e suporte Navegar até

Os recursos no editor do Visual Studio, como colorização de sintaxe, preenchimento de declaração (também conhecido como IntelliSense) e _Navegar Para_, podem ajudá-lo a escrever, ler e editar o código com mais facilidade. A captura de tela a seguir mostra um exemplo de edição de um script Perl no Visual Studio. A sintaxe é automaticamente colorizada. Por exemplo, os comentários no código são coloridos em verde, o código é em preto, os caminhos são em vermelho e as instruções são em azul. O editor do Visual Studio aplica automaticamente a colorização de sintaxe a qualquer linguagem que ele dá suporte. Além disso, quando você começar a inserir uma palavra-chave ou objeto de linguagem conhecido, o preenchimento de declaração exibe uma lista de possíveis declarações e objetos. O preenchimento de declaração pode ajudá-lo a escrever o código com mais rapidez e facilidade.

![Colorização de sintaxe no script Perl](../ide/media/vside_perledit.png)

No momento, o Visual Studio oferece suporte à colorização de sintaxe e preenchimento de declaração básico para as seguintes linguagens usando [gramáticas TextMate](https://manual.macromates.com/en/language_grammars). Se sua linguagem de programação favorita não estiver na tabela, não se preocupe&mdash;será possível adicioná-la.


- Bat
- F#
- Java
- Markdown
- Rust
- Visual Basic
- Clojure
- Go
- JavaDoc
- Objective-C
- ShaderLab
- C#
- CMake
- Groovy
- JSON
- Perl
- ShellScript
- Visual C++
- CoffeeScript
- HTML
- LESS
- Python
- SQL
- VBNet
- CSS
- INI
- LUA
- R
- Swift
- XML
- Docker
- Jade
- Faça
- Ruby
- TypeScript
- YAML

Além da colorização de sintaxe e do preenchimento de declaração, o Visual Studio também tem um recurso chamado [Navegar até](https://blogs.msdn.microsoft.com/benwilli/2015/04/09/visual-studio-tip-3-use-navigate-to/). Esse recurso permite pesquisar rapidamente arquivos de código, caminhos de arquivo e símbolos de código. O Visual Studio oferece suporte Navegar até para as seguintes linguagens.

- C#

- C++

- TypeScript

- JavaScript

- Visual Basic

- Go

- Java

- PHP

Todos esses tipos de arquivo terão os recursos descritos anteriormente, mesmo se o suporte para uma linguagem determinada ainda não tiver sido instalado. Instalar suporte especializado para algumas linguagens pode oferecer suporte a outras linguagens, como IntelliSense ou outros recursos de linguagem avançados como lâmpadas.

## <a name="add-support-for-non-supported-languages"></a>Adicionar suporte para linguagens sem suporte

O Visual Studio 2015 oferece suporte a linguagens no editor usando [Gramáticas TextMate](https://manual.macromates.com/en/language_grammars). Se a sua linguagem de programação favorita não tiver suporte no editor do Visual Studio, em primeiro lugar, pesquise na Web &mdash; um pacote TextMate para a linguagem já pode existir. No entanto, se você não encontrar um, poderá adicionar suporte a ela sozinho criando um modelo de pacote TextMate para snippets e gramáticas de linguagem.

Adicione novas Gramáticas TextMate para o Visual Studio na seguinte pasta:

*%userprofile%\\.vs\Extensions*

Nesse caminho base, adicione as pastas a seguir se forem aplicáveis à sua situação:

|Nome da Pasta|Descrição|
|-----------------|-----------------|
|\\*\<language name>*|A pasta da linguagem. Substituir *\<language name>* pelo nome do idioma. Por exemplo, *\Matlab*.|
|*\Syntaxes*|A pasta da gramática. Contém os arquivos *.json* da gramática para a linguagem, como *Matlab.json*.|
|*\Snippets*|A pasta de snippets. Contém snippets da linguagem.|

No Windows, *% USERPROFILE%* é resolvido para o caminho: *c:\Users \\ \<user name> *. Se a pasta *Extensões* não existir em seu sistema, será necessário criá-la. Se a pasta já existir, ela será oculta.

> [!TIP]
> Se você tiver arquivos abertos no editor, precisará fechá-los e reabri-los para ver o realce de sintaxe depois de adicionar as Gramáticas TextMate.

Para obter detalhes sobre como criar Gramáticas TextMate, confira [TextMate: introdução a gramáticas de linguagem](https://developmentality.wordpress.com/2011/02/08/textmate-introduction-to-language-grammars/) e [Observações sobre como criar uma gramática de linguagem e um tema personalizado para um pacote Textmate](https://benparizek.com/notebook/notes-on-how-to-create-a-language-grammar-and-custom-theme-for-a-textmate-bundle).

## <a name="see-also"></a>Confira também

- [Adicionar uma extensão do Language Server Protocol](../extensibility/adding-an-lsp-extension.md)
- [Passo a passo: Para criar um snippet de código](../ide/walkthrough-creating-a-code-snippet.md)
- [Passo a passo: exibir preenchimento de declaração](../extensibility/walkthrough-displaying-statement-completion.md)
- [Código de exemplo: Grammar](https://github.com/microsoft/VSSDK-Extensibility-Samples/tree/master/TextmateGrammar)
- [Código de exemplo: suporte a idioma personalizado](https://github.com/microsoft/VSSDK-Extensibility-Samples/tree/master/Ook_Language_Integration)