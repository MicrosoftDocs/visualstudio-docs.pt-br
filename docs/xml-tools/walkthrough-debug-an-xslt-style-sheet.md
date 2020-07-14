---
title: Depurar folhas de estilo XSLT
ms.date: 03/05/2019
ms.topic: how-to
ms.assetid: 3db9fa5a-f619-4cb6-86e7-64b364e58e5d
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8c75d3cae07101363f6c986a1defb375f602f466
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815117"
---
# <a name="walkthrough-debug-an-xslt-style-sheet"></a>Walkthrough: Depurar uma folha de estilos XSLT

As etapas nessa explicação passo a passo demonstra como usar o depurador XSLT. As etapas incluem variáveis de exibição, pontos de interrupção, e percorrendo o código. O depurador permite que você execute o código uma linha por vez.

Para se preparar para este passo a passos, primeiro copie os dois [arquivos de exemplo](#sample-files) para o computador local. Um é a folha de estilo e um é o arquivo XML que usaremos como entrada para a folha de estilos. Neste tutorial, a folha de estilos que usamos localiza todos os livros cujo custo está abaixo do preço médio do livro.

> [!NOTE]
> O depurador XSLT só está disponível na edição Enterprise do Visual Studio.

## <a name="start-debugging"></a>Iniciar a depuração

1. No menu **arquivo** , escolha **abrir**  >  **arquivo**.

2. Localize o arquivo *below-Average. xsl* e escolha **abrir**.

   A folha de estilos é aberta no editor de XML.

3. Clique no botão procurar (**...**) no campo de **entrada** da janela Propriedades do documento. (Se a janela **Propriedades** não estiver visível, clique com o botão direito do mouse em qualquer lugar do arquivo aberto no editor e escolha **Propriedades**.)

4. Localize o arquivo *books.xml* e, em seguida, escolha **abrir**.

   Isso define o arquivo de documento de origem que é usado para a transformação XSLT.

5. Defina um [ponto de interrupção](../debugger/using-breakpoints.md) na linha 12 de *below-Average. xsl*. Você pode fazer isso de várias maneiras:

   - Clique na margem do editor na linha 12.

   - Clique em qualquer lugar na linha 12 e pressione **F9**.

   - Clique com o botão direito do mouse na `xsl:if` marca de início e escolha ponto de interrupção de inserção de **pontos**de interrupção  >  **Insert Breakpoint**.

      ![Inserir ponto de interrupção no arquivo XSL no Visual Studio](media/insert-breakpoint.PNG)

6. Na barra de menus, escolha **XML**  >  **Iniciar Depuração XSLT** (ou pressione **ALT** + **F5**).

   O processo de depuração é iniciado.

   No editor, o depurador é posicionado no `xsl:if` elemento da folha de estilos. Outro arquivo chamado *below-average.xml* é aberto no editor; Esse é o arquivo de saída que será populado como cada nó no arquivo de entrada *books.xml* é processado.

   As janelas **automáticos**, **locais**e **inspecionar 1** aparecem na parte inferior da janela do Visual Studio. A janela **locais** exibe todas as variáveis locais e seus valores atuais. Isso inclui variáveis definidos na folha de estilos e também variáveis que o depurador usa para controlar os nós que estão atualmente no contexto.

## <a name="watch-window"></a>Janela Inspecionar

Adicionaremos duas variáveis à janela **Watch 1** para que possamos examinar seus valores à medida que o arquivo de entrada for processado. (Você também pode usar a janela **locais** para examinar valores se as variáveis que você deseja observar já estiverem lá.)

1. No menu **depurar** , escolha **Windows**  >  **Watch**  >  **Watch 1**.

   A janela **Watch 1** torna-se visível.

2. Digite `$bookAverage` o campo **nome** e pressione **Enter**.

   O valor da `$bookAverage` variável é exibido no campo **valor** .

3. Na próxima linha, digite `self::node()` o campo **nome** e pressione **Enter**.

   `self::node()`é uma expressão XPath que é avaliada como o nó de contexto atual. O valor da expressão XPath de `self::node()` é o primeiro nó de livro. Isso é alterado como nós progredimos com a transformação.

4. Expanda o `self::node()` nó e, em seguida, expanda o nó que é o valor `price` .

   ![janela Inspeção durante a depuração XSLT no Visual Studio](media/xslt-debugging-watch-window.png)

   Você pode ver o valor do preço do livro para o nó do livro atual e compará-lo com o `$bookAverage` valor. Como o preço do livro está abaixo da média, a `xsl:if` condição deve ter sucesso quando você continua o processo de depuração.

## <a name="step-through-the-code"></a>Percorrer o código

1. Pressione **F5** para continuar.

   Como o primeiro nó de livro satisfez a `xsl:if` condição, o nó de livro é adicionado ao arquivo de saída *below-average.xml* . O depurador continuará a ser executado até que está localizado novamente no elemento de `xsl:if` na folha de estilos. O depurador agora está posicionado no segundo nó de livro no arquivo de *books.xml* .

   Na janela **Watch 1** , o `self::node()` valor muda para o segundo nó de livro. Examinando o valor do elemento de preço, você pode determinar que o preço está acima da média, então a condição de `xsl:if` deve falhar.

2. Pressione **F5** para continuar.

   Como o segundo nó de livro não atende à `xsl:if` condição, o nó de livro não é adicionado ao arquivo de saída *below-average.xml* . O depurador continuará a ser executado até ser posicionado novamente no `xsl:if` elemento na folha de estilos. O depurador agora está posicionado no terceiro `book` nó do arquivo de *books.xml* .

   Na janela **Watch 1** , o `self::node()` valor muda para o terceiro nó de livro. Examinando o valor do `price` elemento, você pode determinar se o preço está abaixo da média. A `xsl:if` condição deve ter sucesso.

3. Pressione **F5** para continuar.

   Como a `xsl:if` condição foi satisfeita, o terceiro livro é adicionado ao arquivo de saída *below-average.xml* . Todos os livros no documento XML foram processados e paradas do depurador.

## <a name="sample-files"></a>Arquivos de exemplo

Os seguintes dois arquivos são usados por passo a passo.

### <a name="below-averagexsl"></a>below-Average. xsl

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
        <xsl:if test="price &lt; $bookAverage">
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

## <a name="see-also"></a>Veja também

- [Depuração de XSLT](../xml-tools/debugging-xslt.md)
