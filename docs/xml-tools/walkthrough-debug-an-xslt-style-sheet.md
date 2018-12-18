---
title: 'Passo a passo: Depurar uma folha de estilos XSLT'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 3db9fa5a-f619-4cb6-86e7-64b364e58e5d
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ebc8e8f8700690a2ae74fcc91384fb77b238ea33
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34693390"
---
# <a name="walkthrough-debug-an-xslt-style-sheet"></a>Passo a passo: Depurar uma folha de estilos XSLT

As etapas nessa explicação passo a passo demonstra como usar o depurador XSLT. As etapas incluem variáveis de exibição, pontos de interrupção, e percorrendo o código. A folha de estilos localiza os livros que custam abaixo do preço médio de livro.

## <a name="to-prepare-for-this-walkthrough"></a>Para preparar-se para esse passo a passo

1.  Feche soluções abertas.

2.  Copie os dois arquivos de exemplo para seu computador local.

## <a name="start-debugging"></a>Iniciar a depuração

### <a name="to-start-debugging"></a>Para iniciar a depuração

1.  Do **arquivo** , aponte para **abrir**e clique em **arquivo**.

2.  Localize o *belowAvg.xsl* de arquivo e clique em **abrir**.

     A folha de estilos é aberta no editor XML.

3.  Clique no botão Procurar (**...** ) sobre o **entrada** campo da janela de propriedades do documento.

4.  Localize o *books.xml* de arquivo e clique em **abrir**.

     Isso define o arquivo de documento de origem que é usado para a transformação XSLT.

5.  Clique com botão direito do `xsl:if` marca de início, aponte para **ponto de interrupção**e clique em **Inserir ponto de interrupção**.

6.  Clique o **depurar XSL** na barra de ferramentas do Editor de XML.

Isso inicia o processo de depuração e abre várias o windows que são usadas pelo depurador.

Há duas janelas que exibem o documento de entrada e estilos sobrepor. O depurador usar essas janelas para mostrar o estado atual de execução. O depurador está posicionado no `xsl:if` elemento da folha de estilos e no primeiro nó de catálogo no *books.xml* arquivo.

O **locais** janela exibe todas as variáveis locais e seus valores atuais. Isso inclui variáveis definidos na folha de estilos e também variáveis que o depurador usa para controlar os nós que estão atualmente no contexto.

O **saída XSL** janela exibe a saída da transformação XSL. Esta janela é separada do **saída do Visual Studio** janela.

## <a name="watch-window"></a>Janela Inspecionar

### <a name="to-use-the-watch-window"></a>Para usar a janela de observação

1.  Do **depurar** , aponte para **Windows**, aponte para **inspecionar**e clique em **inspecionar 1**.

     Isso torna o **inspecionar 1** visível da janela.

2.  Tipo `$bookAverage` no **nome** campo e pressione **Enter**.

     O valor da variável de `$bookAverage` é exibido na janela.

3.  Tipo `self::node()` no **nome** campo e pressione **Enter**.

     `self::node()` é uma expressão XPath que avalia ao nó atual de contexto. O valor da expressão XPath de `self::node()` é o primeiro nó de livro. Isso é alterado como nós progredimos com a transformação.

4.  Expanda o nó de `self::node()` em seguida, expanda o nó de `price` .

     Isso permite que você possa ver o valor do custo do livro e você pode facilmente compará-lo ao valor de `$bookAverage` . Porque o custo de livro abaixo de média, a condição de `xsl:if` deve obterá êxito.

## <a name="step-through-the-code"></a>Percorrer o código
 O depurador permite que você execute a linha de código por vez.

### <a name="to-step-through-the-code"></a>Para depurar código

1.  Pressione **F5** para continuar.

     Porque o primeiro nó de catálogo satisfeita o `xsl:if` condição, o nó de catálogo é adicionado para o **saída XSL** janela. O depurador continuará a ser executado até que está localizado novamente no elemento de `xsl:if` na folha de estilos. O depurador agora é posicionado no segundo nó Catálogo de *books.xml* arquivo.

     No **inspecionar 1** janela o `self::node()` valor é alterado para o segundo nó de catálogo. Examinando o valor do elemento de preço, você pode determinar que o preço está acima da média, então a condição de `xsl:if` deve falhar.

2.  Pressione **F5** para continuar.

     Porque o segundo nó de catálogo não atende a `xsl:if` condição, o nó de catálogo não é adicionado ao **saída XSL** janela. O depurador continuará a ser executado até que está localizado novamente no elemento de `xsl:if` na folha de estilos. Agora, o depurador é posicionado na terceira `book` nó o *books.xml* arquivo.

     No **inspecionar 1** janela o `self::node()` valor é alterado para o terceiro nó de catálogo. Examinando o valor do elemento de `price` , você pode determinar que o preço abaixo de média, então a condição de `xsl:if` deve obterá êxito.

3.  Pressione **F5** para continuar.

     Porque o `xsl:if` condição foi atendida, o catálogo de terceiro é adicionado para o **saída XSL** janela. Todos os livros no documento XML foram processados e paradas do depurador.

## <a name="sample-files"></a>Arquivos de exemplo

Os seguintes dois arquivos são usados por passo a passo.

### <a name="belowavgxsl"></a>belowAvg.xsl

```xml
<?xml version='1.0'?>
<xsl:stylesheet version="1.0"
      xmlns:xsl="http://www.w3.org/1999/XSL/Transform">
  <xsl:output method="xml" encoding="utf-8"/>
  <xsl:template match="/">
    <xsl:variable name="bookCount" select="count(/bookstore/book)"/>
    <xsl:variable name="bookTotal" select="sum(/bookstore/book/price)"/>
    <xsl:variable name="bookAverage" select="$bookTotal div $bookCount"/>
    <books>
      <!--Books That Cost Below Average-->
      <xsl:for-each select="/bookstore/book">
        <xsl:if test="price < $bookAverage">
          <xsl:copy-of select="."/>
        </xsl:if>
      </xsl:for-each>
    </books>
  </xsl:template>
</xsl:stylesheet>
```

### <a name="booksxml"></a>books.xml

```xml
<?xml version='1.0'?>
<!-- This file represents a fragment of a book store inventory database -->
<bookstore>
  <book genre="autobiography" publicationdate="1981" ISBN="1-861003-11-0">
    <title>The Autobiography of Benjamin Franklin</title>
    <author>
      <first-name>Benjamin</first-name>
      <last-name>Franklin</last-name>
    </author>
    <price>8.99</price>
  </book>
  <book genre="novel" publicationdate="1967" ISBN="0-201-63361-2">
    <title>The Confidence Man</title>
    <author>
      <first-name>Herman</first-name>
      <last-name>Melville</last-name>
    </author>
    <price>11.99</price>
  </book>
  <book genre="philosophy" publicationdate="1991" ISBN="1-861001-57-6">
    <title>The Gorgias</title>
    <author>
      <name>Plato</name>
    </author>
    <price>9.99</price>
  </book>
</bookstore>
```

## <a name="see-also"></a>Consulte também

- [Depuração de XSLT](../xml-tools/debugging-xslt.md)