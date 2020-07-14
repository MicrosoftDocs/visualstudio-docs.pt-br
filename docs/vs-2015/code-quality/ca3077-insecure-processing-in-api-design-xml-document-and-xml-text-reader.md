---
title: 'CA3077: processamento inseguro no design de API, documento XML e leitor de texto XML | Microsoft Docs'
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 7f33771b-f3c8-4c02-bef6-f581b623c303
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: c0d6a6f6ab42d69d4503741f6625627c46d4ef77
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545100"
---
# <a name="ca3077-insecure-processing-in-api-design-xml-document-and-xml-text-reader"></a>CA3077: Processamento não seguro no design de API, no documento XML e no leitor de texto XML
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|InsecureDTDProcessingInAPIDesign|
|CheckId|CA3077|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Ao criar uma API derivada de XMLDocument e XMLTextReader, lembre-se de <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A> .  Usar instâncias DTDProcessing inseguras ao referenciar ou resolver fontes de entidade externas ou definir valores inseguros no XML pode levar à divulgação de informações.

## <a name="rule-description"></a>Descrição da Regra
 Uma [DTD (definição de tipo de documento)](https://msdn.microsoft.com/library/aa468547.aspx) é uma das duas maneiras que um analisador XML pode determinar a validade de um documento, conforme definido pelo [World Wide Web Consortium (W3C) linguagem XML (XML) 1,0](https://www.w3.org/TR/2008/REC-xml-20081126/). Essa regra busca Propriedades e instâncias em que os dados não confiáveis são aceitos para avisar os desenvolvedores sobre possíveis ameaças de [divulgação de informações](https://msdn.microsoft.com/library/4064c89f-afa6-444a-aa7e-807ef072131c) , o que pode levar a ataques [de negação de serviço (dos)](https://msdn.microsoft.com/library/dfb150f3-d598-4697-a5e6-6779e4f9b600) . Esta regra é disparada quando:

- <xref:System.Xml.XmlDocument>ou <xref:System.Xml.XmlTextReader> classes usam valores de resolvedor padrão para processamento de DTD.

- Nenhum construtor é definido para as classes derivadas XmlDocument ou XmlTextReader ou nenhum valor seguro é usado para <xref:System.Xml.XmlResolver> .

## <a name="how-to-fix-violations"></a>Como Corrigir Violações

- Pegue e processe todas as exceções de XmlTextReader corretamente para evitar a divulgação de informações de caminho.

- Use  <xref:System.Xml.XmlSecureResolver> em vez de XmlResolver para restringir os recursos que o XmlTextReader pode acessar.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
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
