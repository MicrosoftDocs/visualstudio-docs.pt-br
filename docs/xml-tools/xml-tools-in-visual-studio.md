---
title: Editor de XML e designer de esquema
ms.date: 11/04/2016
ms.topic: overview
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
- XML [Visual Studio], .NET classes
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
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e763fa3475f26b9742ea5fb7061978e711eb22ea
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816417"
---
# <a name="overview-of-xml-tools-in-visual-studio"></a>Visão geral das ferramentas XML no Visual Studio

*Linguagem XML (XML)* é uma linguagem de marcação que fornece um formato para descrever os dados. O XML separa os dados e sua apresentação usando folhas de estilo associadas, como XSL (Extensible Stylesheet Language) e CSS (Cascading Style Sheets). O Visual Studio inclui ferramentas e recursos que facilitam trabalhar com os esquemas XML, XSLT e XML.

## <a name="xml-editor"></a>Editor de XML

O [Editor de XML](xml-editor.md) é usado para editar documentos XML. Ele fornece verificação de sintaxe XML completa, validação de esquema enquanto você digita, codificação de cor e IntelliSense. Se um esquema ou um definição de tipo de documento forem fornecidos, ele é usado pelo IntelliSense para listar os elementos e atributos permitidos.

Recursos adicionais incluem:

- Suporte a trecho XML, incluindo trechos de código gerados pelo esquema

- Documento de estrutura de tópicos para que os elementos possam ser expandidos e recolhidos

- A capacidade de executar transformações XSLT e exibir os resultados como texto, XML ou HTML

- A capacidade de gerar esquemas XSD (linguagem de definição de esquema XML) a partir do documento da instância XML

- Suporte para edição de folhas de estilo XSLT, incluindo suporte a IntelliSense

- XML Schema Explorer

## <a name="xml-schema-designer"></a>Designer de Esquema XML

O [Designer de esquema XML](xml-schema-designer.md) é integrado ao Visual Studio e ao editor de XML para permitir que você trabalhe com esquemas XSD (linguagem de definição de esquema XML).

## <a name="xslt-debugging"></a>Depuração de XSLT

O Visual Studio dá suporte à [depuração de folhas de estilo XSLT](../xml-tools/debugging-xslt.md). Usando o depurador, você pode definir pontos de quebra em uma folha de estilos XSLT, entrar em uma folha de estilos XSLT a partir do código, e assim por diante.

> [!NOTE]
> O depurador XSLT só está disponível na edição Enterprise do Visual Studio.

## <a name="see-also"></a>Veja também

- <xref:System.Xml?displayProperty=fullName>
- [Transformações XSLT](/dotnet/standard/data/xml/xslt-transformations)
- [Processar dados XML usando o modelo de dados XPath](/dotnet/standard/data/xml/process-xml-data-using-the-xpath-data-model)
- [XML Document Object Model (DOM)](/dotnet/standard/data/xml/xml-document-object-model-dom)
- [SOM (Schema Object Model) XML](/dotnet/standard/data/xml/xml-schema-object-model-som)
