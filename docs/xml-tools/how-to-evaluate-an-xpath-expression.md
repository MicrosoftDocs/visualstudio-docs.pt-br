---
title: 'Como: Avalie uma expressão XPath'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 159ba4ef-75e4-4ac8-80dc-e064e0bec345
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 02492f2e1760df3ce5cd6751808303bae75577e2
ms.sourcegitcommit: 697162f54d3c4e30df702fd0289e447e211e3a85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34549045"
---
# <a name="how-to-evaluate-an-xpath-expression"></a>Como: Avalie uma expressão XPath

Você pode avaliar expressões XPath com o **QuickWatch** caixa de diálogo. A expressão XPath deve ser válido de acordo com a recomendação XPath 1,0 W3C. O contexto XSLT atual — ou seja, o `self::node()` nó o **locais** janela — fornece o contexto de avaliação da expressão XPath.

 A lista a seguir descreve quais funções são suportadas para avaliar uma expressão XPath:

-   As funções internas XPath são suportadas.

-   As funções internas XSLT não são suportadas.

-   As funções definidas pelo usuário não são suportadas.

> [!NOTE]
> O procedimento a seguir usa o *belowAvg.xsl* e *books.xml* arquivos do [passo a passo: depurar uma folha de estilos XSLT](../xml-tools/walkthrough-debug-an-xslt-style-sheet.md) tópico.

## <a name="to-evaluate-an-xpath-expression"></a>Para avaliar uma expressão XPath

1.  Inserir um ponto de interrupção na tag de início de `xsl:if` .

2.  Clique o **depurar XSL** na barra de ferramentas do Editor de XML.

     Inicia e as quebras do depurador na marca `xsl:if` .

3.  Clique com botão direito e selecione **QuickWatch**.

     O **QuickWatch** caixa de diálogo é exibida.

4.  Digite `./price/text()` no **expressão** campo o **QuickWatch** caixa de diálogo e clique em **reavaliar**.

     O preço do nó atual do catálogo aparece no **valor** caixa.

5.  Altere a expressão XPath para `./price/text() < $bookAverage` e clique em **reavaliar**.

     O **valor** caixa mostra que a expressão XPath é avaliada como `true`.

## <a name="see-also"></a>Consulte também

- [Depuração de XSLT](../xml-tools/debugging-xslt.md)