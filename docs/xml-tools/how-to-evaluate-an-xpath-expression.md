---
title: Avaliar uma expressão XPath durante a depuração
ms.date: 03/05/2019
ms.topic: how-to
ms.assetid: 159ba4ef-75e4-4ac8-80dc-e064e0bec345
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 64113461cd081eb97e2eb927119f1cd67f8a8d6e
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816248"
---
# <a name="evaluate-xpath-expressions"></a>Avaliar expressões XPath

Você pode avaliar as expressões XPath usando a janela **QuickWatch** durante a depuração. A expressão XPath deve ser válido de acordo com a recomendação XPath 1,0 W3C. O contexto XSLT atual (ou seja, o `self::node()` nó na janela **locais** ) fornece o contexto de avaliação para a expressão XPath.

Ao avaliar uma expressão XPath:

- As funções internas XPath são suportadas.

- Não há suporte para funções XSLT internas e funções definidas pelo usuário.

> [!NOTE]
> A depuração XSLT só está disponível na edição Enterprise do Visual Studio.

## <a name="evaluate-an-xpath-expression"></a>Avaliar uma expressão XPath

O procedimento a seguir usa o *below-Average. xsl* e os arquivos de *books.xml* da [instrução: Depurar uma página de folha de estilos XSLT](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md#sample-files) .

1. Inserir um ponto de interrupção na tag de início de `xsl:if` .

2. Para iniciar a depuração, escolha **XML**  >  **Iniciar Depuração XSLT** na barra de menus (ou pressione **ALT** + **F5**).

   Inicia e as quebras do depurador na marca `xsl:if` .

3. Clique com o botão direito do mouse e selecione **QuickWatch**.

   A janela **QuickWatch** é aberta.

4. Insira `./price/text()` no campo **expressão** da caixa de diálogo **QuickWatch** e escolha **reavaliar**.

   O preço do nó do livro atual aparece na caixa **valor** .

   ![Avaliar uma expressão XPath na janela QuickWatch](media/quickwatch-price.png)

5. Altere a expressão XPath para `./price/text() < $bookAverage` e clique em **reavaliar**.

   A caixa **valor** mostra que a expressão XPath é avaliada como `true` .

## <a name="see-also"></a>Veja também

- [Depuração de XSLT](../xml-tools/debugging-xslt.md)
