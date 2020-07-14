---
title: Adicionar atributo DebuggerDisplay
ms.date: 05/12/2020
ms.topic: reference
author: mikadumont
ms.author: midumont
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: 611df048d4ce569c10ae933be9053acf1174c06f
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85290023"
---
# <a name="add-debuggerdisplay-attribute"></a>Adicionar atributo DebuggerDisplay

Esta geração de código aplica-se a:

- C#

**O que:** O [atributo DebuggerDisplay](https://docs.microsoft.com/visualstudio/debugger/using-the-debuggerdisplay-attribute) controla como um objeto, uma propriedade ou um campo é exibido nas janelas da variável do depurador.

**Quando:** Você deseja [fixar as propriedades](https://docs.microsoft.com/visualstudio/debugger/view-data-values-in-data-tips-in-the-code-editor#pin-properties-in-datatips) no depurador programaticamente no seu código.

**Por que:** As propriedades de fixação permitem que você inspecione rapidamente os objetos por suas propriedades, lendo a propriedade na parte superior da lista de propriedades do objeto dentro do depurador. 

## <a name="how-to"></a>Como fazer

1. Coloque o cursor em um tipo, representante, propriedade ou campo. 

2. Pressione **Ctrl** + **.** para disparar o menu **ações rápidas e refatorar** e selecione **Adicionar atributo DebuggerDisplay**.

    ![Gerar Operadores de Comparação](media/add-debugger-display-attribute.png)

3. O atributo DebuggerDisplay será adicionado junto com um método auto que retorna o ToString padrão (). 

## <a name="see-also"></a>Veja também

- [Geração de código](../code-generation-in-visual-studio.md)
- [Visualizar Alterações](../../ide/preview-changes.md)
