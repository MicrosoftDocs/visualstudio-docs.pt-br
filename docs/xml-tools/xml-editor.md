---
title: Editor de XML
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 8e120d65c9336acaa509e74c79d9e538673cd256
ms.sourcegitcommit: bc43970c000f07c9cc2051f1264a9742943a9755
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51349316"
---
# <a name="xml-editor"></a>Editor de XML

O editor XML se baseia no editor de texto do Visual Studio e inclui suporte adicional para linguagens XML. O editor XML inclui os seguintes recursos:

- Verificação de sintaxe XML 1.0.

- Validação de esquema quando você digita.

- Suporte de snippets de XML, incluindo snippets gerados por esquema.

- Suporte para definição de tipo de documento (DTD).

- Suporte para o esquema da linguagem XSD.

- Criando um esquema XML de um documento de instância XML.

- Convertendo um DTD ou um esquema XDR em um esquema XML.

- Verificação de sintaxe XSLT 1.0.

- Estrutura de tópicos de documento de modo que os elementos possam ser expandidos e recolhidos.

- Integração com o [XML Schema Explorer](../xml-tools/xml-schema-explorer.md). Isso fornece uma exibição hierárquica dos esquemas XML.

O editor de XML é invocado para extensões de arquivo conhecidas, como *. XML*, *. xsd*, *. xsl*, e *. config*. Também é chamado em qualquer extensão de arquivo desconhecida se o arquivo parecer conter XML. Você também pode abrir qualquer arquivo com o editor de XML usando o **abrir com** opção e selecionando o editor de XML da lista.

## <a name="xslt-intellisense"></a>XSLT IntelliSense

[IntelliSense do XSLT](../xml-tools/xml-editor-intellisense-features.md) permite nomes de conjunto de atributos de preenchimento automático, modos de modelo e os nomes e nomes de parâmetro para um modo especificado ou um especificado chamado modelo.

## <a name="xslt-profiler"></a>Criador de perfil XSLT

O [profiler XSLT](../xml-tools/walkthrough-xslt-profiler.md) cria de desempenho detalhados XSLT relatórios que ajudam você a medem, avaliar e direcionar problemas relacionados ao desempenho no código XSLT. O profiler XSLT também inclui dicas úteis para XSL e otimizações de folha de estilos XSLT.

## <a name="xslt-hierarchy"></a>Hierarquia XSLT

O [ferramenta da hierarquia XSLT](../xml-tools/walkthrough-using-xslt-hierarchy.md) permite que você adicione pontos de interrupção em folhas de estilo embutidas e/ou regras de modelo interno.

## <a name="see-also"></a>Consulte também

- [Recursos do editor de código](../ide/writing-code-in-the-code-and-text-editor.md) fornece informações sobre o editor de texto.
- [Referência a padrões XML](https://msdn.microsoft.com/79c78508-c9d0-423a-a00f-672e855de401) fornece informações sobre tecnologias XML, incluindo XML, definição de tipo de documento (DTD), linguagem de definição de esquema XML (XSD) e XSLT.
- [Ferramentas XML no Visual Studio](../xml-tools/xml-tools-in-visual-studio.md)