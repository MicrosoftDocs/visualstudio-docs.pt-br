---
title: 'CA3077: Processamento inseguro no Design de API, documento XML e leitor de texto XML | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7f33771b-f3c8-4c02-bef6-f581b623c303
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 0e75f86b958d0f2602a3f32830e8c6f18c185584
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49925065"
---
# <a name="ca3077-insecure-processing-in-api-design-xml-document-and-xml-text-reader"></a>CA3077: processamento não seguro no design de API, no documento XML e no leitor de texto XML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|InsecureDTDProcessingInAPIDesign|
|CheckId|CA3077|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Quando a criação de uma API deriva do XMLDocument e XMLTextReader, lembre-se <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A>.  Usando instâncias de DTDProcessing inseguras ao referenciar ou resolvendo origens de entidade externa ou definir os valores inseguros em XML pode levar à divulgação de informações.

## <a name="rule-description"></a>Descrição da Regra
 Um [definição de tipo de documento (DTD)](https://msdn.microsoft.com/library/aa468547.aspx) é uma das duas maneiras de um analisador XML pode determinar a validade de um documento, conforme definido pelo [World Wide Web Consortium (W3C) Extensible Markup Language (XML) 1.0](http://www.w3.org/TR/2008/REC-xml-20081126/). Essa regra procura as propriedades e instâncias onde os dados não confiáveis é aceito para alertar os desenvolvedores sobre o potencial [divulgação de informações](http://msdn.microsoft.com/library/4064c89f-afa6-444a-aa7e-807ef072131c) ameaças, que podem levar à [negação de serviço (DoS)](http://msdn.microsoft.com/library/dfb150f3-d598-4697-a5e6-6779e4f9b600) ataques. Essa regra dispara quando:

-   <xref:System.Xml.XmlDocument> ou <xref:System.Xml.XmlTextReader> classes usam valores de resolvedor padrão para processamento de DTD.

-   Nenhum construtor for definido para o XmlDocument ou as classes derivadas de XmlTextReader ou nenhum valor seguro é usado para <xref:System.Xml.XmlResolver>.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações

-   Capturar e processar todas as exceções de XmlTextReader corretamente para evitar a divulgação de informações de caminho.

-   Use <xref:System.Xml.XmlSecureResolver>em vez de XmlResolver para restringir os recursos que o XmlTextReader pode acessar.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 A menos que você tiver certeza de que a entrada é conhecida por ser de uma fonte confiável, não suprima uma regra deste aviso.

## <a name="pseudo-code-examples"></a>Exemplos de código pseudo

### <a name="violation"></a>Violação

```csharp
using System;
using System.Xml;

namespace TestNamespace
{
    class TestClass : XmlDocument
    {
        public TestClass () {} // warn
    }

    class TestClass2 : XmlTextReader
    {
        public TestClass2() // warn
        {
        }
    }
}
```

### <a name="solution"></a>Solução

```csharp
using System;
using System.Xml;

namespace TestNamespace
{
    class TestClass : XmlDocument
    {
        public TestClass ()
        {
            XmlResolver = null;
        }
    }

    class TestClass2 : XmlTextReader
    {
        public TestClass2()
        {
               XmlResolver = null;
        }
    }
}
```



