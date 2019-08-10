---
title: 'CA3077: Processamento não seguro no design de API, no documento XML e no leitor de texto XML'
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 7f33771b-f3c8-4c02-bef6-f581b623c303
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ca39cef1fb4f1bf1114673dd96a91a1ac8e105cc
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68919871"
---
# <a name="ca3077-insecure-processing-in-api-design-xml-document-and-xml-text-reader"></a>CA3077: Processamento não seguro no design de API, no documento XML e no leitor de texto XML

|||
|-|-|
|NomeDoTipo|InsecureDTDProcessingInAPIDesign|
|CheckId|CA3077|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
Ao criar uma API derivada de XMLDocument e XMLTextReader, lembre-se <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A>de.  Usar instâncias DTDProcessing inseguras ao referenciar ou resolver fontes de entidade externas ou definir valores inseguros no XML pode levar à divulgação de informações.

## <a name="rule-description"></a>Descrição da regra
Uma *DTD (definição de tipo de documento)* é uma das duas maneiras que um analisador XML pode determinar a validade de um documento, conforme definido pelo [World Wide Web Consortium (W3C) linguagem XML (XML) 1,0](http://www.w3.org/TR/2008/REC-xml-20081126/). Essa regra busca Propriedades e instâncias em que os dados não confiáveis são aceitos para avisar os desenvolvedores sobre possíveis ameaças de [divulgação de informações](/dotnet/framework/wcf/feature-details/information-disclosure) , o que pode levar a ataques [de negação de serviço (dos)](/dotnet/framework/wcf/feature-details/denial-of-service) . Esta regra é disparada quando:

- <xref:System.Xml.XmlDocument>ou <xref:System.Xml.XmlTextReader> classes usam valores de resolvedor padrão para processamento de DTD.

- Nenhum construtor é definido para as classes derivadas XmlDocument ou XmlTextReader ou nenhum valor seguro é usado para <xref:System.Xml.XmlResolver>.

## <a name="how-to-fix-violations"></a>Como corrigir violações

- Pegue e processe todas as exceções de XmlTextReader corretamente para evitar a divulgação de informações de caminho.

- Use <xref:System.Xml.XmlSecureResolver>em vez de XmlResolver para restringir os recursos que o XmlTextReader pode acessar.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos
A menos que você tenha certeza de que a entrada é conhecida por ser de uma fonte confiável, não omita uma regra desse aviso.

## <a name="pseudo-code-examples"></a>Exemplos de pseudocódigo

### <a name="violation"></a>Infra

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