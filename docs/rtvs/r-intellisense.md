---
title: IntelliSense para código em R
description: O Visual Studio IntelliSense exibe informações sobre funções, membros do objeto, snippets de código e conclusões conforme você digita o código R.
ms.date: 01/24/2018
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: a9efdae5623c00abe4626d1bbb21af4a790fa487
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35666859"
---
# <a name="intellisense"></a>IntelliSense

O Visual Studio IntelliSense exibe informações sobre funções que você pode chamar, membros dos objetos, argumentos de função e [snippets de código](code-snippets-for-r.md) diretamente em sua exibição ao escrever código. Ele também exibe preenchimentos possíveis enquanto você digita e termina quando você pressiona as teclas **Tab** ou **Enter** (consulte [Opções do editor](editing-r-code-in-visual-studio.md#editor-options) da guia **Avançado**). O IntelliSense está disponível no editor e na [janela interativa](interactive-repl-for-r-in-visual-studio.md).

![IntelliSense mostrando uma assinatura de função](media/intellisense-function-signature.png)

Ao digitar uma função ou outra instrução, o IntelliSense fornece um menu de preenchimento automático filtrado (diferenciando maiúsculas de minúsculas ), de acordo com o que você já inseriu:

![Menu de preenchimento automático do IntelliSense](media/intellisense-auto-complete-menu.png)

Pressionar **Tab** (ou **Enter** ou **Espaço**, dependendo de como as opções são definidas) insere o item selecionado na lista suspensa. Você pode alterar a seleção com as teclas de direção.

O IntelliSense também oferece sugestões para membros dos objetos R:

![Sugestões do IntelliSense para membros do objeto](media/intellisense-auto-complete-r-objects.png)

Pressionar **ESC** ignora o menu completamente. Você pode ativá-lo novamente com **Ctrl**+**Espaço**.

Digitar o `(` de abertura para uma chamada de função insere o `)` de fechamento e abre a Ajuda de assinatura conforme mostrado anteriormente:

![Ajuda de assinatura do IntelliSense para uma função](media/intellisense-function-signature.png)

Novamente, **ESC** descarta o pop-up. Para assinaturas de função, você pode ativá-lo novamente com **Ctrl**+**Shift**+**Espaço**.

> [!Tip]
> Se a ajuda do parâmetro obscurecer o texto abaixo dela, pressione e mantenha pressionada a tecla **Ctrl** para tornar o texto da ajuda do parâmetro translúcido.

## <a name="intellisense-for-user-defined-functions-and-variables"></a>IntelliSense para funções e variáveis definidas pelo usuário

O IntelliSense aplica-se a funções definidas pelo usuário no mesmo arquivo, incluindo o preenchimento de parâmetro de nome:

![IntelliSense para funções definidas pelo usuário](media/intellisense-same-file-functions.png)

![Preenchimento de parâmetro do IntelliSense para funções definidas pelo usuário](media/intellisense-parameter-completion.png)

O IntelliSense também se aplica a variáveis no mesmo arquivo e na sessão atual:

![Preenchimento de variável do IntelliSense](media/intellisense-variable-completion.png)

> [!Note]
> Na janela interativa, o IntelliSense considera apenas nomes na sessão do R atual e ignora os arquivos em seu projeto.

## <a name="code-suggestions"></a>Sugestões de código

Quando uma lâmpada (chamada de smart tag) aparece na margem, o Visual Studio está sugerindo que um atalho está disponível para uma ação bastante usada. Por exemplo, passe o mouse sobre uma linha que contém uma instrução `library` no editor para ver uma lâmpada. Selecionar a lâmpada exibe as opções disponíveis:

![Smart tags para R no editor](media/intellisense-smart-tags.png)
