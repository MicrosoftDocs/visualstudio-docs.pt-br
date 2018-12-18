---
title: Snippets de código C#
ms.date: 06/05/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- snippets [C#]
- code snippets [C#]
- Code Snippet Inserter [C#]
- C#, code snippets
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
ms.openlocfilehash: feec485f752ac13b43310e4afd97bdfaac93ee51
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49849158"
---
# <a name="c-code-snippets"></a>Snippets de código C#

Os snippets de código são snippets de código prontos que você pode inserir rapidamente em seu código. Por exemplo, o snippet de código `for` cria um loop `for` vazio. Alguns snippets de código são snippets de código envolvidos, que permite que você selecione linhas de código e, em seguida, escolha um snippet de código que incorpora as linhas de código selecionadas. Por exemplo, quando você seleciona linhas de código e, em seguida, ativa o snippet de código `for`, ele cria um loop `for` com as linhas de código selecionadas dentro do bloco de loop. Os snippets de código podem fazer com que escrever código de programa seja mais rápido, mais fácil e mais confiável.

 Você pode inserir um snippet de código no local do cursor ou inserir um snippet de código envolvido com o código atualmente selecionado. A Unidade de Inserção de Snippet de Código é invocada por meio dos comandos **Inserir Snippet de Código** ou **Envolver Com** no menu do **IntelliSense** ou usando os atalhos de teclado **Ctrl**+**K**,**X** ou **Ctrl**+**K**,**S**, respectivamente.

 A **Unidade de Inserção de Snippet de Código** exibe o nome do snippet de código de todos os snippets de código disponíveis. A Unidade de Inserção de Snippet de Código também inclui uma caixa de diálogo de entrada em que você pode digitar o nome ou parte do nome do snippet de código. A Unidade de Inserção de Snippet de Código realça a correspondência mais próxima de um nome de snippet de código. Ao pressionar **Tab** a qualquer momento, a Unidade de Inserção de Snippet de Código será fechada e o snippet de código selecionado será inserido. Ao pressionar **Esc** ou clicar com o mouse no editor de códigos, a Unidade de Inserção de Snippet de Código será ignorada sem inserir um snippet de código.

## <a name="default-code-snippets"></a>Snippets de código padrão

Por padrão, os snippets de código a seguir são incluídos no Visual Studio para C#.

|Nome (ou atalho)|Descrição|Locais válidos para inserir o snippet|
| - |-----------------| - |
|#if|Cria uma diretiva [#if](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if) e uma diretiva [#endif](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-endif).|Em qualquer lugar.|
|#region|Cria uma diretiva [#region](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-region) e uma diretiva [#endregion](/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-endregion).|Em qualquer lugar.|
|~|Cria um [finalizador](/dotnet/csharp/programming-guide/classes-and-structs/destructors) (destruidor) para a classe que o contém.|Dentro de uma classe.|
|Atributo|Cria uma declaração para uma classe que deriva de <xref:System.Attribute>.|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|
|checked|Cria um bloco [checked](/dotnet/csharp/language-reference/keywords/checked).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|classe|Cria uma declaração de classe.|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|
|ctor|Cria um construtor para a classe que o contém.|Dentro de uma classe.|
|cw|Cria uma chamada para <xref:System.Console.WriteLine%2A>.|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|do|Cria um loop [do](/dotnet/csharp/language-reference/keywords/do) `while`.|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|else|Cria um bloco [else](/dotnet/csharp/language-reference/keywords/if-else).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|enum|Cria uma declaração [enum](/dotnet/csharp/language-reference/keywords/enum).|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|
|é igual a|Cria uma declaração de método que substitui o método <xref:System.Object.Equals%2A> definido na classe <xref:System.Object>.|Dentro de uma classe ou um struct.|
|exception|Cria uma declaração para uma classe que deriva de uma exceção (<xref:System.Exception> por padrão).|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|
|for|Cria um loop [for](/dotnet/csharp/language-reference/keywords/for).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|foreach|Cria um loop [foreach](/dotnet/csharp/language-reference/keywords/foreach-in).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|forr|Cria um loop [for](/dotnet/csharp/language-reference/keywords/for) que decrementa a variável de loop depois de cada iteração.|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|if|Cria um bloco [if](/dotnet/csharp/language-reference/keywords/if-else).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|indexador|Cria uma declaração do indexador.|Dentro de uma classe ou um struct.|
|interface|Cria uma declaração [interface](/dotnet/csharp/language-reference/keywords/interface).|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|
|invoke|Cria um bloco que invoca um evento com segurança.|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|iterator|Cria um iterador.|Dentro de uma classe ou um struct.|
|iterindex|Cria um par de iterador e indexador "nomeado" usando uma classe aninhada.|Dentro de uma classe ou um struct.|
|bloqueio|Cria um bloco [lock](/dotnet/csharp/language-reference/keywords/lock-statement).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|mbox|Cria uma chamada para <xref:System.Windows.Forms.MessageBox.Show%2A?displayProperty=fullName>. Talvez seja necessário adicionar uma referência a *System.Windows.Forms.dll*.|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|namespace|Cria uma declaração de [namespace](/dotnet/csharp/language-reference/keywords/namespace).|Dentro de um namespace (incluindo o namespace global).|
|prop|Cria uma declaração de [propriedade autoimplementada](/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties).|Dentro de uma classe ou um struct.|
|propfull|Cria uma declaração de propriedade com os acessadores `get` e `set`.|Dentro de uma classe ou um struct.|
|propg|Cria uma [propriedade implementada automaticamente](/dotnet/csharp/programming-guide/classes-and-structs/auto-implemented-properties) do tipo somente leitura, com um acessador `set` particular.|Dentro de uma classe ou um struct.|
|sim|Cria uma declaração de método principal [static](/dotnet/csharp/language-reference/keywords/static) [int](/dotnet/csharp/language-reference/keywords/int).|Dentro de uma classe ou um struct.|
|struct|Cria uma declaração [struct](/dotnet/csharp/language-reference/keywords/struct).|Dentro de um namespace (incluindo o namespace global), uma classe ou uma estrutura.|
|svm|Cria uma declaração de método principal [static](/dotnet/csharp/language-reference/keywords/static) [void](/dotnet/csharp/language-reference/keywords/void).|Dentro de uma classe ou um struct.|
|switch|Cria um bloco [switch](/dotnet/csharp/language-reference/keywords/switch).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|try|Cria um bloco [try-catch](/dotnet/csharp/language-reference/keywords/try-catch).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|tryf|Cria um bloco [try-finally](/dotnet/csharp/language-reference/keywords/try-finally).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|unchecked|Cria um bloco [unchecked](/dotnet/csharp/language-reference/keywords/unchecked).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|unsafe|Cria um bloco [unsafe](/dotnet/csharp/language-reference/keywords/unsafe).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|
|using|Cria uma diretiva [using](/dotnet/csharp/language-reference/keywords/using-directive).|Dentro de um namespace (incluindo o namespace global).|
|while|Cria um loop [while](/dotnet/csharp/language-reference/keywords/while).|Dentro de um método, um indexador, um acessador de propriedade ou um acessador de evento.|

## <a name="see-also"></a>Consulte também

- [Funções de snippet de código](../ide/code-snippet-functions.md)
- [Snippets de código](../ide/code-snippets.md)
- [Parâmetros de modelo](../ide/template-parameters.md)
- [Como usar snippets de código surround-with](../ide/how-to-use-surround-with-code-snippets.md)