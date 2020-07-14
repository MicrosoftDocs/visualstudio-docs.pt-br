---
title: 'Passo a passo: usando XSLT IntelliSense'
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 079d95ac-2eaf-4ae1-9cd3-2c81a961a942
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a085627d598bfcc969c2e76d717a2f49a31922b2
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85817275"
---
# <a name="walkthrough-using-xslt-intellisense"></a>Passo a passo: usando XSLT IntelliSense

Essa explicação passo a passo demonstra como usar IntelliSense do XSLT para completar automaticamente o valor de alguns atributos.

## <a name="to-use-intellisense-in-the-name-attribute-of-xslwith-param-and-xslcall-template-elements"></a>Para usar o IntelliSense no atributo de nome de elementos xsl:with-param e xsl:call-template

1. Crie um novo arquivo XSLT e copie no seguinte código:

    ```xml
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
    <!-- These 2 elements effectively assign
         $messages = resources/en.xml/<messages>,
         then $messages is used in the "localized-message" template.  -->
    <xsl:param name="lang">en</xsl:param>
    <xsl:variable name="messages"
          select="document(concat('resources/', $lang, '.xml'))/messages"/>

    <xsl:template name="msg23" match="msg23">
    </xsl:template>

    <xsl:template name="localized-message">
      <xsl:param name="msgcode"/>
      <!-- Show message string. -->
      <xsl:message terminate="yes">
        <xsl:value-of select="$messages/message[@name=$msgcode]"/>
      </xsl:message>
    </xsl:template>
    </xsl:stylesheet>
    ```

2. Insira o cursor depois `<xsl:template name="msg23" match="msg23">` e pressione **Enter**. Inicie digitando o elemento `xsl:call-template` a seguir:

    ```xml
    <xsl:call-template name="localized-message">
    </xsl:call-template>
    ```

     A lista de nomes de modelo aparece no atributo `name=""` do elemento `xsl:call-template` à medida que você digita.

3. Insira o cursor depois `<xsl:call-template name="localized-message">` e pressione **Enter**. Inicie digitando o elemento `xsl:with-param` a seguir:

    ```xml
    <xsl:with-param name="msgcode">msg23</xsl:with-param>
    ```

     A lista de nomes de parâmetro aparece no atributo `name=""` do elemento `xsl:with-param`.

## <a name="to-use-intellisense-in-the-mode-attribute-of-an-xslapply-templates-element"></a>Para usar o IntelliSense no atributo do modo de um elemento xsl:apply-templates

1. Crie um novo arquivo XSLT e copie no seguinte código:

    ```xml
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" version="1.0">
      <xsl:template match="/">
        <HTML>
          <BODY>
            <TABLE>
              <xsl:apply-templates select="customers/customer">
                <xsl:sort select="state"/>
                <xsl:sort select="name"/>
              </xsl:apply-templates>
            </TABLE>
          </BODY>
        </HTML>
      </xsl:template>
      <xsl:template match="customer">
        <TR>
          <xsl:apply-templates select="name" />
          <xsl:apply-templates select="address" />
          <xsl:apply-templates select="phone" />
        </TR>
      </xsl:template>
      <xsl:template match="name">
        <TD STYLE="font-size:14pt font-family:serif">
          <xsl:apply-templates />
        </TD>
      </xsl:template>
      <xsl:template match="address">
        <TD>
          <xsl:apply-templates />
        </TD>
      </xsl:template>
      <xsl:template match="phone">
        <TD>
          <xsl:apply-templates />
        </TD>
      </xsl:template>
      <xsl:template match="phone" mode="accountNumber">
        <xsl:param name="Area_Code"/>
        <TD STYLE="font-style:italic">
          1-<xsl:value-of select="."/>-001
        </TD>
      </xsl:template>
    </xsl:stylesheet>
    ```

2. Insira o cursor depois `<xsl:apply-templates select="phone" />` e pressione **Enter**. Inicie digitando o elemento `xsl: apply-templates` a seguir:

    ```xml
    <xsl:apply-templates select="phone"  mode="accountNumber">
    ```

     A lista de modos de modelo aparece no atributo `mode=""` do elemento `xsl:apply-templates`.

## <a name="to-use-intellisense-in-the-stylesheet-prefix-and-result-prefix-attributes-of-an-xslnamespace-alias-element"></a>Para usar o IntelliSense nos atributos stylesheet-prefix e result-prefix de um elemento xsl:namespace-alias

1. Crie um novo arquivo XSLT e copie no seguinte código:

    ```xml
    <xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:alt="http://www.w3.org/1999/XSL/Transform-alternate"
    version="1.0">
      <xsl:param name="browser" select="'InternetExplorer'"/>
      <xsl:template match="/">
        <alt:stylesheet>
          <xsl:choose>
            <xsl:when test="$browser='InternetExplorer'">
              <alt:import href="IERoutines.xsl"/>
              <alt:template match="/">
                <div>
                  <alt:call-template name="showTable"/>
                </div>
              </alt:template>
            </xsl:when>
            <xsl:otherwise>
              <alt:import href="OtherBrowserRoutines.xsl"/>
              <alt:template match="/">
                <div>
                  <alt:call-template name="showTable"/>
                </div>
              </alt:template>
            </xsl:otherwise>
          </xsl:choose>
        </alt:stylesheet>
      </xsl:template>
    </xsl:stylesheet>
    ```

2. Insira o cursor depois `<xsl:stylesheet xmlns:xsl="http://www.w3.org/1999/XSL/Transform" xmlns:alt="http://www.w3.org/1999/XSL/Transform-alternate" version="1.0">` e pressione **Enter**. Inicie digitando o elemento `xsl:namespace-alias` a seguir:

    ```xml
    <xsl:namespace-alias stylesheet-prefix="alt" result-prefix="xsl"/>
    ```

     Observe como a lista de prefixos apareceu nos atributos `stylesheet-prefix` e `result-prefix` do elemento de `xsl:namespace-alias`.

## <a name="see-also"></a>Veja também

- [Recursos do IntelliSense do editor de XML](../xml-tools/xml-editor-intellisense-features.md)
