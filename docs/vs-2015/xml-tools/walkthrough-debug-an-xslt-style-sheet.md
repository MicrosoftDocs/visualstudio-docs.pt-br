---
title: 'Passo a passo: Depurar uma folha de estilos XSLT | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3db9fa5a-f619-4cb6-86e7-64b364e58e5d
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 10dad7382a30800675c257a4e2c8219d20e5b18b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49887679"
---
# <a name="walkthrough-debug-an-xslt-style-sheet"></a>Passo a passo: Depurar uma folha de estilos XSLT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

As etapas nessa explicação passo a passo demonstra como usar o depurador XSLT. As etapas incluem variáveis de exibição, pontos de interrupção, e percorrendo o código. A folha de estilos localiza os livros que custam abaixo do preço médio de livro.  
  
### <a name="to-prepare-for-this-walkthrough"></a>Para preparar-se para esse passo a passo  
  
1.  Feche soluções abertas.  
  
2.  Copie os dois arquivos de exemplo para seu computador local.  
  
## <a name="start-debugging"></a>Iniciar a depuração  
  
#### <a name="to-start-debugging"></a>Para iniciar a depuração  
  
1. Dos **arquivo** , aponte para **abra**e clique em **arquivo**.  
  
2. Localize o arquivo de Belowavg e clique em **aberto**.  
  
    A folha de estilos é aberta no editor XML.  
  
3. Clique no botão Procurar (**...** ) sobre o **entrada** campo da janela de propriedades do documento.  
  
4. Localize o arquivo de Books. XML e clique em **aberto**.  
  
    Isso define o arquivo de documento de origem que é usado para a transformação XSLT.  
  
5. Clique com botão direito do `xsl:if` marca de início, aponte para **ponto de interrupção**e clique em **Inserir ponto de interrupção**.  
  
6. Clique o **depurar XSL** na barra de ferramentas do Editor de XML.  
  
   Isso inicia o processo de depuração e abre várias o windows que são usadas pelo depurador.  
  
   Há duas janelas que exibem o documento de entrada e estilos sobrepor. O depurador usar essas janelas para mostrar o estado atual de execução. O depurador é posicionado no elemento de `xsl:if` de folha de estilos e no primeiro nó de livro no arquivo de books.xml.  
  
   A janela locais exibe todas as variáveis locais e seus valores atuais. Isso inclui variáveis definidos na folha de estilos e também variáveis que o depurador usa para controlar os nós que estão atualmente no contexto.  
  
   O **saída XSL** janela exibe a saída da transformação XSL. Essa janela é separada dos **saída do Visual Studio** janela.  
  
## <a name="watch-window"></a>Observação de janela  
  
#### <a name="to-use-the-watch-window"></a>Para usar a janela de observação  
  
1.  Do **Debug** , aponte para **Windows**, aponte para **Assista**e clique em **inspeção 1**.  
  
     Isso torna a observação 1 janela visível.  
  
2.  Tipo de `$bookAverage` no **nome** do campo e pressione ENTER.  
  
     O valor da variável de `$bookAverage` é exibido na janela.  
  
3.  Tipo de `self::node()` no **nome** do campo e pressione ENTER.  
  
     `self::node()` é uma expressão XPath que avalia ao nó atual de contexto. O valor da expressão XPath de `self::node()` é o primeiro nó de livro. Isso é alterado como nós progredimos com a transformação.  
  
4.  Expanda o nó de `self::node()` em seguida, expanda o nó de `price` .  
  
     Isso permite que você possa ver o valor do custo do livro e você pode facilmente compará-lo ao valor de `$bookAverage` . Porque o custo de livro abaixo de média, a condição de `xsl:if` deve obterá êxito.  
  
## <a name="step-through-the-code"></a>Avançar no código  
 O depurador permite que você execute a linha de código por vez.  
  
#### <a name="to-step-through-the-code"></a>Para depurar código  
  
1.  Pressione **F5** para continuar.  
  
     Porque o primeiro nó de livro tiver satisfeito a condição de `xsl:if` , o nó de livro é adicionada à janela de saída XSL. O depurador continuará a ser executado até que está localizado novamente no elemento de `xsl:if` na folha de estilos. O depurador é posicionado agora no segundo nó de livro no arquivo de books.xml.  
  
     Na janela Watch1 o valor de `self::node()` alterações no segundo nó de livro. Examinando o valor do elemento de preço, você pode determinar que o preço está acima da média, então a condição de `xsl:if` deve falhar.  
  
2.  Pressione **F5** para continuar.  
  
     Porque o segundo nó de livro não está de acordo com a condição de `xsl:if` , o nó de livro não é adicionada à janela de saída XSL. O depurador continuará a ser executado até que está localizado novamente no elemento de `xsl:if` na folha de estilos. O depurador é posicionado agora no terceiro nó de `book` no arquivo de books.xml.  
  
     Na janela Watch1 o valor de `self::node()` alterações para o terceiro nó de livro. Examinando o valor do elemento de `price` , você pode determinar que o preço abaixo de média, então a condição de `xsl:if` deve obterá êxito.  
  
3.  Pressione **F5** para continuar.  
  
     Porque a condição de `xsl:if` foi encontrada, o terceiro livro é adicionada à janela de saída XSL. Todos os livros no documento XML foram processados e paradas do depurador.  
  
## <a name="sample-files"></a>Arquivos de exemplo  
 Os seguintes dois arquivos são usados por passo a passo.  
  
### <a name="belowavgxsl"></a>belowAvg.xsl  
  
```  
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
  
```  
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
 [Depuração de XSLT](../xml-tools/debugging-xslt.md)

