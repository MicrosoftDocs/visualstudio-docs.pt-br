---
title: Ações rápidas, lâmpadas e chaves de fenda
ms.date: 03/28/2018
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
dev_langs:
- CSharp
- VB
ms.workload:
- multiple
ms.openlocfilehash: 7089a9a654d1c346fefcca119f74a87d89f323b8
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349368"
---
# <a name="quick-actions"></a>Ações Rápidas

As Ações Rápidas permitem refatorar, gerar ou, de outro modo, modificar o código de maneira fácil com uma única ação. As Ações Rápidas estão disponíveis para C#, [C++](/cpp/ide/writing-and-refactoring-code-cpp) e os arquivos de código do Visual Basic. Algumas ações são específicas para uma linguagem e outras se aplicam a todas as linguagens.

É possível usar as Ações rápidas para:

- Aplicar uma correção de código para uma violação de regra do [analisador de código](../code-quality/roslyn-analyzers-overview.md)
- [Suprimir](../code-quality/use-roslyn-analyzers.md) uma violação de regra do analisador de código
- Aplicar uma refatoração (por exemplo, [embutir uma variável temporária](../ide/reference/inline-temporary-variable.md))
- Gerar um código (por exemplo, [introduzir uma variável local](../ide/reference/introduce-local-variable.md))

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Refatoração (Visual Studio para Mac)](/visualstudio/mac/refactoring).

As Ações Rápidas podem ser aplicadas usando os ícones de lâmpada ![Ícone de lâmpada](media/light-bulb-icon.png) ou de chave de fenda ![ícone de chave de fenda](media/screwdriver-icon.png) ou pressionando **Ctrl**+**.** quando o cursor estiver em uma linha de código para a qual uma ação está disponível. Você verá uma lâmpada erro ![ícone de lâmpada de erro](media/error-light-bulb-icon.png) se houver um rabisco vermelho, indicando um erro e o Visual Studio terá uma solução disponível para esse erro.

Para qualquer idioma, terceiros podem oferecer diagnósticos e sugestões personalizados, por exemplo, como parte de um SDK, e as lâmpadas do Visual Studio são acesas de acordo com essas regras.

## <a name="icons"></a>Ícones

O ícone exibido quando uma Ação Rápida fica disponível oferece uma indicação do tipo de correção ou que a refatoração está disponível. O ícone de *chave de fenda* ![ícone de chave de fenda](media/screwdriver-icon.png) indica apenas que há ações disponíveis para alterar o código, mas você não deve necessariamente usá-las. O ícone de *lâmpada amarela* ![ícone de lâmpada](media/light-bulb-icon.png) indica que há ações disponíveis que você *deve* executar para melhorar o seu código. O ícone de *lâmpada de erro* ![ícone de lâmpada de erro](media/error-light-bulb-icon.png) indica que há uma ação disponível que corrige um erro no seu código.

## <a name="to-see-a-light-bulb-or-screwdriver"></a>Para ver uma lâmpada ou chave de fenda

- Se uma correção estiver disponível, lâmpadas serão exibidas espontaneamente quando você passar o mouse no local de um erro.

   ![Lâmpada com o mouse focalizando](../ide/media/vs2015_lightbulb_hover.png)

- Lâmpadas e chaves de fenda são exibidas na margem esquerda do editor quando você move o cursor para uma linha de código para o qual uma Ação Rápida está disponível.

- Pressione **Ctrl**+**.** em qualquer lugar em uma linha para ver uma lista de Ações Rápidas e refatorações disponíveis.

## <a name="to-see-potential-fixes"></a>Para ver as possíveis correções

Selecione a seta para baixo ao lado da lâmpada ou do link **Mostrar possíveis correções** para exibir uma lista de Ações Rápidas disponíveis.

![Lâmpada expandida](../ide/media/vs2015_lightbulb_hover_expanded.png)

## <a name="see-also"></a>Consulte também

- [Geração de código no Visual Studio](../ide/code-generation-in-visual-studio.md)
- [Ações Rápidas Comuns](../ide/common-quick-actions.md)
- [Estilos de código e ações rápidas](../ide/code-styles-and-quick-actions.md)
- [Escrever e refatorar o código (C++)](/cpp/ide/writing-and-refactoring-code-cpp)
- [Refatoração (Visual Studio para Mac)](/visualstudio/mac/refactoring)