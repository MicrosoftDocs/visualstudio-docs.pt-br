---
title: 'Passo a passo: Usando a hierarquia XSLT | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5e60c8ec-cd05-4597-b856-55038218acf4
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 5b94a958a915ad7858575e093cae525df17cc23e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49280950"
---
# <a name="walkthrough-using-xslt-hierarchy"></a>Passo a passo: Usando a hierarquia XSLT
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
A ferramenta da hierarquia XSLT simplifica muitas tarefas de desenvolvimento XML. Uma folha de estilos XSLT frequentemente usa `includes` e instruções de `imports` . A compilação parte da folha de estilos principal, mas quando você verá um erro no resultado de criar uma folha de estilos XSLT, o erro pode vir de uma fonte diferente da folha de estilos principal. Corrigir o erro ou editar a folha de estilos podem exigir acesso incluiu ou importaram folhas de estilos. Percorrer de folha de estilo no depurador pode abrir folhas de estilo embutidas e importados, e você pode querer adicionar um ponto de interrupção em algum ponto de uma ou mais das folhas de estilo embutidas.  
  
 Outro cenário onde a ferramenta da hierarquia XSLT pode ser útil é colocando pontos de interrupção nas regras de modelo interno. As regras de modelo são modelos especiais gerados para cada modo de folha de estilos e chamados por `xsl:apply-templates` quando nenhum outro modelo corresponde ao nó. Para implementar a depuração em regras de modelos internos, o depurador XSLT gerencia o arquivo com as regras na pasta temporária e compilar-las juntamente com a folha de estilos principal. Sem entrar no código de qualquer `xsl:apply-template`, pode ser difícil localizar as folhas de estilos que foram incluídas na folha de estilos principal ou localizar e abrir a folha de estilos com as regras de modelo interno.  
  
 O exemplo neste tópico demonstra a depuração em uma folha de estilos referenciada.  
  
### <a name="procedure-title"></a>Título do procedimento  
  
1.  Abrir um documento XML no Visual Studio. Este exemplo usa o seguinte documento de `collection.xml` .  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <?xml-stylesheet type="text/xsl" href="xslinclude.xsl"?>  
    <COLLECTION>  
      <BOOK>  
        <TITLE>Lover Birds</TITLE>  
        <AUTHOR>Cynthia Randall</AUTHOR>  
        <PUBLISHER>Lucerne Publishing</PUBLISHER>  
      </BOOK>  
      <BOOK>  
        <TITLE>The Sundered Grail</TITLE>  
        <AUTHOR>Eva Corets</AUTHOR>  
        <PUBLISHER>Lucerne Publishing</PUBLISHER>  
      </BOOK>  
      <BOOK>  
        <TITLE>Splish Splash</TITLE>  
        <AUTHOR>Paula Thurman</AUTHOR>  
        <PUBLISHER>Scootney</PUBLISHER>  
      </BOOK>  
    </COLLECTION>  
    ```  
  
2.  Adicione o seguinte `xslincludefile.xsl`:  
  
    ```  
    <?xml version='1.0'?>  
    <xsl:stylesheet version="1.0"  
          xmlns:xsl="http://www.w3.org/1999/XSL/Transform"  
          xml:space="preserve">  
  
    <xsl:template match="TITLE">  
       Title - <xsl:value-of select="."/><BR/>  
    </xsl:template>  
  
    <xsl:template match="AUTHOR">  
       Author - <xsl:value-of select="."/><BR/>  
    </xsl:template>  
  
    <xsl:template match="PUBLISHER">  
       Publisher - <xsl:value-of select="."/><BR/><!-- removed second <BR/> -->  
    </xsl:template>  
  
    </xsl:stylesheet>  
    ```  
  
3.  Adicione o seguinte arquivo de `xslinclude.xsl` :  
  
    ```  
    <?xml version='1.0'?>  
    <xsl:stylesheet version="1.0"  
          xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
  
      <xsl:output method="xml" omit-xml-declaration="yes"/>  
  
      <xsl:template match="/">  
        <xsl:for-each select="COLLECTION/BOOK">  
          <xsl:apply-templates select="TITLE"/>  
          <xsl:apply-templates select="AUTHOR"/>  
          <xsl:apply-templates select="PUBLISHER"/>  
          <BR/>  
          <!-- add this -->  
        </xsl:for-each>  
      </xsl:template>  
  
      <!-- The following template rule will not be called,  
      because the related template in the including stylesheet  
      is called. If we move this template so that  
      it follows the xsl:include instruction, this one  
      will be called instead.-->  
      <xsl:template match="TITLE">  
        <DIV STYLE="color:blue">  
          Title: <xsl:value-of select="."/>  
        </DIV>  
      </xsl:template>  
  
      <xsl:include href="xslincludefile.xsl" />  
    </xsl:stylesheet>  
    ```  
  
4.  Adicione um ponto de interrupção na instrução: `<xsl:include href="xslincludefile.xsl" />`  
  
5.  Inicie a depuração.  
  
6.  Quando o depurador para a instrução `<xsl:include href="xslincludefile.xsl" />`, pressione a etapa no botão. Observe que a depuração pode ser continuada na folha de estilos referenciada. A hierarquia é visível e o designer o caminho correto.  
  
## <a name="see-also"></a>Consulte também  
 [Passo a passo: Criador de Perfil XSLT](../xml-tools/walkthrough-xslt-profiler.md)



