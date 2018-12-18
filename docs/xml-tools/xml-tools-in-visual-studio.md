---
title: Ferramentas XML
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
f1_keywords:
- vb.xmldesigner
helpviewer_keywords:
- XML [Visual Studio], resources
- Enterprise Templates, XML and
- discovery files, XML
- server controls, XML and
- Web server controls, XML
- XSL
- XML [Visual Studio], data sources
- XML schemas
- XML [Visual Studio], SGML relationship to
- CSS, style sheets for XML
- XML [Visual Studio], .NET Framework classes
- data [Visual Studio], XML
- classes [Visual Studio], XML
- style sheets, for XML
- Web services
- SGML, XML
- XML [Visual Studio]
- datasets [Visual Basic], XML Schemas
- XSD schemas
- XSL, style sheets
- XMLDataDocument class
ms.assetid: 1fd5de47-2d61-4180-9539-c2c4bf9ab768
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: f87c06e2bfc3885c0f52230e927933ff3cb0d87c
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53054992"
---
# <a name="xml-tools-in-visual-studio"></a>Ferramentas XML no Visual Studio

*Extensible Markup Language (XML)* é uma linguagem de marcação que fornece um formato para descrever dados. Isso facilita declarações mais precisas de conteúdo e mais resultados de pesquisa significativos nas diversas plataformas. Além disso, o XML permite a separação da apresentação dos dados. Por exemplo, em HTML, usam-se marcas para dizer ao navegador para exibir dados como negrito ou itálico; em XML, usam-se marcas somente para descrever dados, como nome da cidade, temperatura e pressão barométrica. Em XML, você usar folhas de estilo, como Extensible Stylesheet Language (XSL) e folhas de estilo em cascata (CSS) para apresentar os dados em um navegador. O XML separa os dados da apresentação e do processo. Isso permite exibir e processar os dados como desejar, aplicando diferentes folhas de estilo e aplicações.

O XML é um subconjunto do SGML que é otimizado para entrega na Web. Ele é definido pelo World Wide Web Consortium (W3C). Essa padronização garante que dados estruturados serão uniformes e independentes de aplicativos ou fornecedores.

O XML é a essência dos muitos recursos do Visual Studio e o .NET Framework. A lista a seguir artigo nomeia as ferramentas e recursos relacionados ao XML que são oferecidos no Visual Studio e o .NET Framework.

Para obter mais informações, consulte o <xref:System.Xml?displayProperty=fullName> documentação.

## <a name="reference"></a>Referência

[Microsoft.VisualStudio.XmlEditor](http://go.microsoft.com/fwlink/?LinkID=165699) expõe o [Editor de XML](http://go.microsoft.com/fwlink/?LinkId=228249) árvore por meio de análise [LINQ](http://go.microsoft.com/fwlink/?LinkId=228250) para todos os documentos XML.

[Referência a padrões XML](https://msdn.microsoft.com/79c78508-c9d0-423a-a00f-672e855de401) fornece informações sobre tecnologias XML, incluindo XML, definição de tipo de documento (DTD), linguagem de definição de esquema XML (XSD) e XSLT.

<xref:System.Xml?displayProperty=fullName> Descreve as classes e outros elementos que compõem o <xref:System.Xml> namespace e fornece links para informações mais detalhadas sobre cada item.

<xref:System.Xml.Serialization?displayProperty=fullName> Descreve as classes e outros elementos que compõem o <xref:System.Xml.Serialization> namespace e fornece links para informações mais detalhadas sobre cada item.

## <a name="related-sections"></a>Seções relacionadas

[Modelo de objeto de documento (DOM) XML](/dotnet/standard/data/xml/xml-document-object-model-dom) descreve como o <xref:System.Xml.XmlDocument> e suas classes associadas estão em conformidade com as especificações de suporte de namespace de nível 2 e W3C Document Object Model (núcleos) de nível 1.

[Processar dados XML com XmlReader e XmlWriter](/previous-versions/windows/silverlight/dotnet-windows-silverlight/cc189001\(v\=vs.95\))

[Transformações XSLT](/dotnet/standard/data/xml/xslt-transformations) descreve como o <xref:System.Xml.Xsl.XslCompiledTransform> classe implementa a recomendação XSLT 1.0.

[Processar dados XML usando o modelo de dados XPath](/dotnet/standard/data/xml/process-xml-data-using-the-xpath-data-model) descreve como o <xref:System.Xml.XPath.XPathNavigator> classe pode processar dados XML armazenados em um <xref:System.Xml.XPath.XPathDocument> ou um <xref:System.Xml.XmlDocument> objeto. A classe <xref:System.Xml.XPath.XPathNavigator> é baseada no Modelo de Dados XQuery 1.0 e XPath 2.0 ou pode ser usada para navegar e editar dados XML.

[Modelo de objeto de esquema XML (SOM)](/dotnet/standard/data/xml/xml-schema-object-model-som) descreve as classes usadas para criar e manipular esquemas XML, fornecendo um <xref:System.Xml.Schema.XmlSchema> classe para carregar e editar um esquema.