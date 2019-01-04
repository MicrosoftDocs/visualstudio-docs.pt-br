---
title: 'CA3077: Processamento não seguro no design de API, no documento XML e no leitor de texto XML'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: reference
ms.assetid: 7f33771b-f3c8-4c02-bef6-f581b623c303
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 33c6aaea4cdc7de1c81338eb4861d56d73cb5909
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53841272"
---
# <a name="ca3077-insecure-processing-in-api-design-xml-document-and-xml-text-reader"></a>CA3077: Processamento não seguro no design de API, no documento XML e no leitor de texto XML

|||
|-|-|
|NomeDoTipo|InsecureDTDProcessingInAPIDesign|
|CheckId|CA3077|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Quando a criação de uma API deriva do XMLDocument e XMLTextReader, lembre-se <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A>.  Usando instâncias de DTDProcessing inseguras ao referenciar ou resolvendo origens de entidade externa ou definir os valores inseguros em XML pode levar à divulgação de informações.

## <a name="rule-description"></a>Descrição da regra
 Um *definição de tipo de documento (DTD)* é uma das duas maneiras de um analisador XML pode determinar a validade de um documento, conforme definido pelo [World Wide Web Consortium (W3C) Extensible Markup Language (XML) 1.0](http://www.w3.org/TR/2008/REC-xml-20081126/). Essa regra procura as propriedades e instâncias onde os dados não confiáveis é aceito para alertar os desenvolvedores sobre o potencial [divulgação de informações](/dotnet/framework/wcf/feature-details/information-disclosure) ameaças, que podem levar à [negação de serviço (DoS)](/dotnet/framework/wcf/feature-details/denial-of-service) ataques. Essa regra dispara quando:

- <xref:System.Xml.XmlDocument> ou <xref:System.Xml.XmlTextReader> classes usam valores de resolvedor padrão para processamento de DTD.

- Nenhum construtor for definido para o XmlDocument ou as classes derivadas de XmlTextReader ou nenhum valor seguro é usado para <xref:System.Xml.XmlResolver>.

## <a name="how-to-fix-violations"></a>Como corrigir violações

- Capturar e processar todas as exceções de XmlTextReader corretamente para evitar a divulgação de informações de caminho.

- Use <xref:System.Xml.XmlSecureResolver>em vez de XmlResolver para restringir os recursos que o XmlTextReader pode acessar.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
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