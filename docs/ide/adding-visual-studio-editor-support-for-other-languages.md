---
title: Adicionando suporte para outras linguagens ao editor do Visual Studio
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
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.workload:
- multiple
ms.openlocfilehash: 57991a7cac2d45cf618642ccd19ead1d94ce5978
ms.sourcegitcommit: 401be39a42ffe007593528b5bba62583ca9fcafd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/30/2018
ms.locfileid: "50244470"
---
# <a name="add-visual-studio-editor-support-for-other-languages"></a>Adicionar suporte para outras linguagens ao editor do Visual Studio

Saiba mais sobre como o editor do Visual Studio dá suporte à leitura e à navegação por meio de diferentes linguagens de computador e como é possível adicionar suporte ao editor do Visual Studio para outras linguagens.

## <a name="syntax-colorization-statement-completion-and-navigate-to-support"></a>Colorização de sintaxe, preenchimento de declaração e suporte Navegar até

Os recursos no editor do Visual Studio, como colorização de sintaxe, preenchimento de declaração (também conhecido como IntelliSense) e _Navegar Para_, podem ajudá-lo a escrever, ler e editar o código com mais facilidade. A captura de tela a seguir mostra um exemplo de edição de um script Perl no Visual Studio. A sintaxe é automaticamente colorizada. Por exemplo, os comentários no código são coloridos em verde, o código é em preto, os caminhos são em vermelho e as instruções são em azul. O editor do Visual Studio aplica automaticamente a colorização de sintaxe a qualquer linguagem que ele dá suporte. Além disso, quando você começar a inserir uma palavra-chave ou objeto de linguagem conhecido, o preenchimento de declaração exibe uma lista de possíveis declarações e objetos. O preenchimento de declaração pode ajudá-lo a escrever o código com mais rapidez e facilidade.

![Colorização de sintaxe no script Perl](../ide/media/vside_perledit.png)

No momento, o Visual Studio oferece suporte à colorização de sintaxe e preenchimento de declaração básico para as seguintes linguagens usando [gramáticas TextMate](https://manual.macromates.com/en/language_grammars). Se sua linguagem favorita não estiver na tabela, não se preocupe – é possível adicioná-la.

|||||||
|-|-|-|-|-|-|
|Bat|F#|Java|Markdown|Rust|Visual Basic|
|Clojure|Ir|JavaDoc|Objective-C|ShaderLab|C#|
|CMake|Groovy|JSON|Perl|ShellScript|Visual C++|
|CoffeeScript|HTML|LESS|Python|SQL|VBNet|
|CSS|INI|LUA|R|Swift|XML|
|Docker|Jade|Marca|Ruby|TypeScript|YAML|

Além da colorização de sintaxe e do preenchimento de declaração, o Visual Studio também tem um recurso chamado [Navegar até](https://blogs.msdn.microsoft.com/benwilli/2015/04/09/visual-studio-tip-3-use-navigate-to/). Esse recurso permite pesquisar rapidamente arquivos de código, caminhos de arquivo e símbolos de código. O Visual Studio oferece suporte Navegar até para as seguintes linguagens.

-   Ir

-   Java

-   JavaScript

-   PHP

-   TypeScript

-   Visual Basic

-   Visual C++

-   C#

Todos esses tipos de arquivo terão os recursos descritos anteriormente, mesmo se o suporte para uma linguagem determinada ainda não tiver sido instalado. Instalar suporte especializado para algumas linguagens pode oferecer suporte a outras linguagens, como IntelliSense ou outros recursos de linguagem avançados como lâmpadas.

## <a name="add-support-for-non-supported-languages"></a>Adicionar suporte para linguagens sem suporte

A Atualização 1 do Visual Studio 2015 e versões posteriores oferecem suporte a linguagens no editor usando [Gramáticas TextMate](https://manual.macromates.com/en/language_grammars). Se a sua linguagem de programação favorita não tiver suporte no editor do Visual Studio, em primeiro lugar, pesquise na Web – um pacote TextMate para a linguagem já pode existir. No entanto, se você não encontrar um, poderá adicionar suporte a ela sozinho na Atualização 1 do Visual Studio 2015 ou posterior, criando um modelo de pacote TextMate para snippets e gramáticas de linguagem.

Adicione novas Gramáticas TextMate para o Visual Studio na seguinte pasta:

*%userprofile%\\.vs\Extensions*

Nesse caminho base, adicione as pastas a seguir se forem aplicáveis à sua situação:

|Nome da Pasta|Descrição|
|-----------------|-----------------|
|\\*\<nome da linguagem>*|A pasta da linguagem. Substitua *\<nome da linguagem>* pelo nome da linguagem. Por exemplo, *\Matlab*.|
|*\Syntaxes*|A pasta da gramática. Contém os arquivos *.json* da gramática para a linguagem, como *Matlab.json*.|
|*\Snippets*|A pasta de snippets. Contém snippets da linguagem.|

No Windows, *%userprofile%* determina o caminho: *c:\Usuários\\\<nome do usuário >*. Se a pasta de extensões não existir em seu sistema, será necessário criá-la. Se a pasta já existir, ela será oculta.

Para obter detalhes sobre como criar Gramáticas TextMate, consulte [TextMate – Introduction to Language Grammars: How to add source code syntax highlighting embedded in HTML (TextMate – Introdução a gramáticas de linguagem: como adicionar realce de sintaxe do código-fonte inserido no HTML)](https://developmentality.wordpress.com/2011/02/08/textmate-introduction-to-language-grammars/) e [Notes on how to create a Language Grammar and Custom Theme for a Textmate Bundle (Observações sobre como criar uma gramática de linguagem e um tema personalizado para um pacote Textmate)](https://benparizek.com/notebook/notes-on-how-to-create-a-language-grammar-and-custom-theme-for-a-textmate-bundle).

## <a name="see-also"></a>Consulte também

- [Passo a passo: Criar um snippet de código](../ide/walkthrough-creating-a-code-snippet.md)
- [Passo a passo: exibir preenchimento de declaração](../extensibility/walkthrough-displaying-statement-completion.md)
