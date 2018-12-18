---
title: 'CA3075: Processamento de DTD inseguro | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 65798d66-7a30-4359-b064-61a8660c1eed
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 8284f065a829ac7ecc29330fb8a9dad74e92690e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49850160"
---
# <a name="ca3075-insecure-dtd-processing"></a>CA3075: processamento de DTD não seguro
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|InsecureDTDProcessing|
|CheckId|CA3075|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Se você usar instâncias de <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A> inseguras ou referenciar origens de entidade externa, o analisador poderá aceitar a entrada não confiável e divulgar as informações confidenciais para invasores.

## <a name="rule-description"></a>Descrição da Regra
 Um [definição de tipo de documento (DTD)](https://msdn.microsoft.com/library/aa468547.aspx) é uma das duas maneiras de um analisador XML pode determinar a validade de um documento, conforme definido pelo [World Wide Web Consortium (W3C) Extensible Markup Language (XML) 1.0](http://www.w3.org/TR/2008/REC-xml-20081126/). Essa regra procura as propriedades e instâncias onde os dados não confiáveis é aceito para alertar os desenvolvedores sobre o potencial [divulgação de informações](http://msdn.microsoft.com/library/4064c89f-afa6-444a-aa7e-807ef072131c) ameaças, que podem levar à [negação de serviço (DoS)](http://msdn.microsoft.com/library/dfb150f3-d598-4697-a5e6-6779e4f9b600) ataques. Essa regra dispara quando:

- DtdProcessing está habilitada no <xref:System.Xml.XmlReader> instância, que resolve entidades externas de XML usando <xref:System.Xml.XmlUrlResolver>.

- O <xref:System.Xml.XmlNode.InnerXml%2A> está definida no XML.

- <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A> propriedade é definida como a análise.

- Não-confiáveis de entrada será processada usando <xref:System.Xml.XmlResolver> em vez de <xref:System.Xml.XmlSecureResolver> .

- O XmlReader.<xref:System.Xml.XmlReader.Create%2A> método é invocado com um carimbo <xref:System.Xml.XmlReaderSettings> nenhuma instância ou em todos.

- <xref:System.Xml.XmlReader> é criado com as configurações padrão inseguro ou valores.

  Cada um desses casos, o resultado é o mesmo: o conteúdo de qualquer um dos compartilhamentos de arquivos sistema ou de rede do computador em que o XML é processado será exposto para o invasor, que pode ser usado como um vetor DoS.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações

- Capturar e processar todas as exceções de XmlTextReader corretamente para evitar a divulgação de informações de caminho.

- Use o <xref:System.Xml.XmlSecureResolver> para restringir os recursos que o XmlTextReader pode acessar.

- Não permita que o <xref:System.Xml.XmlReader> para abrir todos os recursos externos definindo o <xref:System.Xml.XmlResolver> propriedade **nulo**.

- Certifique-se de que o <xref:System.Data.DataViewManager.DataViewSettingCollectionString%2A> propriedade de <xref:System.Data.DataViewManager> é atribuído a partir de uma fonte confiável.

  .NET 3.5 e anterior

- Desabilitar o processamento de DTD se você está lidando com fontes não confiáveis, definindo o <xref:System.Xml.XmlReaderSettings.ProhibitDtd%2A> propriedade para **verdadeiro** .

- Classe de XmlTextReader tem uma exigência de herança de confiança total. Ver [demandas de herança](http://msdn.microsoft.com/en-us/28b9adbb-8f08-4f10-b856-dbf59eb932d9) para obter mais informações.

  .NET 4 e posterior

- Evite habilitar DtdProcessing se você estiver lidando com fontes não confiáveis, definindo a propriedade DtdProcessing como [proibir ou ignorar](https://msdn.microsoft.com/library/system.xml.dtdprocessing.aspx)

- Certifique-se de que o método Load () usa uma instância de XmlReader em todos os casos de InnerXml.

> [!NOTE]
>  Essa regra pode relatar falsos positivos em algumas instâncias de XmlSecureResolver válidas. Estamos trabalhando para resolver esse problema em meados de 2016.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 A menos que você tiver certeza de que a entrada é conhecida por ser de uma fonte confiável, não suprima uma regra deste aviso.

## <a name="pseudo-code-examples"></a>Exemplos de código pseudo

### <a name="violation"></a>Violação

```csharp
using System.IO;
using System.Xml.Schema;

class TestClass
{
    public XmlSchema Test
    {
        get
        {
            var src = "";
            TextReader tr = new StreamReader(src);
            XmlSchema schema = XmlSchema.Read(tr, null); // warn
            return schema;
        }
    }
}
```

### <a name="solution"></a>Solução

```csharp
using System.IO;
using System.Xml;
using System.Xml.Schema;

class TestClass
{
    public XmlSchema Test
    {
        get
        {
            var src = "";
            TextReader tr = new StreamReader(src);
            XmlTextReader reader = new XmlTextReader(tr) { DtdProcessing = DtdProcessing.Prohibit };
            XmlSchema schema = XmlSchema.Read(reader , null);
            return schema;
        }
    }
}
```

### <a name="violation"></a>Violação

```csharp
using System.Xml;

namespace TestNamespace
{
    public class TestClass
    {
        public XmlReaderSettings settings = new XmlReaderSettings();
        public void TestMethod(string path)
        {
            var reader = XmlReader.Create(path, settings);  // warn
        }
    }
}
```

### <a name="solution"></a>Solução

```csharp
using System.Xml;

namespace TestNamespace
{
    public class TestClass
    {
        public XmlReaderSettings settings = new XmlReaderSettings()
        {
            DtdProcessing = DtdProcessing.Prohibit
        };

        public void TestMethod(string path)
        {
            var reader = XmlReader.Create(path, settings);
        }
    }
}
```

### <a name="violations"></a>Violações

```csharp
using System.Xml;

namespace TestNamespace
{
    public class DoNotUseSetInnerXml
    {
        public void TestMethod(string xml)
        {
            XmlDocument doc = new XmlDocument() { XmlResolver = null };
            doc.InnerXml = xml; // warn
        }
    }
}
```

```csharp
using System.Xml;

namespace TestNamespace
{
    public class DoNotUseLoadXml
    {
        public void TestMethod(string xml)
        {
            XmlDocument doc = new XmlDocument(){ XmlResolver = null };
            doc.LoadXml(xml); // warn
        }
    }
}
```

### <a name="solution"></a>Solução

```csharp
using System.Xml;

public static void TestMethod(string xml)
{
    XmlDocument doc = new XmlDocument() { XmlResolver = null };
    System.IO.StringReader sreader = new System.IO.StringReader(xml);
    XmlTextReader reader = new XmlTextReader(sreader) { DtdProcessing = DtdProcessing.Prohibit };
    doc.Load(reader);
}
```

### <a name="violation"></a>Violação

```csharp
using System.IO;
using System.Xml;
using System.Xml.Serialization;

namespace TestNamespace
{
    public class UseXmlReaderForDeserialize
    {
        public void TestMethod(Stream stream)
        {
            XmlSerializer serializer = new XmlSerializer(typeof(UseXmlReaderForDeserialize));
            serializer.Deserialize(stream); // warn
        }
    }
}
```

### <a name="solution"></a>Solução

```csharp
using System.IO;
using System.Xml;
using System.Xml.Serialization;

namespace TestNamespace
{
    public class UseXmlReaderForDeserialize
    {
        public void TestMethod(Stream stream)
        {
            XmlSerializer serializer = new XmlSerializer(typeof(UseXmlReaderForDeserialize));
            XmlTextReader reader = new XmlTextReader(stream) { DtdProcessing = DtdProcessing.Prohibit } ;
            serializer.Deserialize(reader );
        }
    }
}
```

### <a name="violation"></a>Violação

```csharp
using System.Xml;
using System.Xml.XPath;

namespace TestNamespace
{
    public class UseXmlReaderForXPathDocument
    {
        public void TestMethod(string path)
        {
            XPathDocument doc = new XPathDocument(path); // warn
        }
    }
}
```

### <a name="solution"></a>Solução

```csharp
using System.Xml;
using System.Xml.XPath;

namespace TestNamespace
{
    public class UseXmlReaderForXPathDocument
    {
        public void TestMethod(string path)
        {
            XmlTextReader reader = new XmlTextReader(path) { DtdProcessing = DtdProcessing.Prohibit };
            XPathDocument doc = new XPathDocument(reader);
        }
    }
}
```

### <a name="violation"></a>Violação

```csharp
using System.Xml;

namespace TestNamespace
{
    class TestClass
    {
        public XmlDocument doc = new XmlDocument() { XmlResolver = new XmlUrlResolver() };
    }
}
```

### <a name="solution"></a>Solução

```csharp
using System.Xml;

namespace TestNamespace
{
    class TestClass
    {
        public XmlDocument doc = new XmlDocument() { XmlResolver = null }; // or set to a XmlSecureResolver instance
    }
}
```

### <a name="violations"></a>Violações

```csharp
using System.Xml;

namespace TestNamespace
{
    public class TestClass
    {
        public void TestMethod(string path)
        {
            XmlReaderSettings settings = new XmlReaderSettings(){ DtdProcessing = DtdProcessing.Parse };
            XmlReader reader = XmlReader.Create(path, settings); // warn
        }
    }
}
```

```csharp
using System.Xml;

namespace TestNamespace
{
    class TestClass
    {
        private static void TestMethod()
        {
            var reader = XmlTextReader.Create(""doc.xml""); //warn
        }
    }
}
```

```csharp
using System.Xml;

namespace TestNamespace
{
    public class TestClass
    {
        public void TestMethod(string path)
        {
            try {
                XmlTextReader reader = new XmlTextReader(path); // warn
            }
            catch { throw ; }
            finally {}
        }
    }
}
```

### <a name="solution"></a>Solução

```csharp
using System.Xml;

namespace TestNamespace
{
    public class TestClass
    {
        public void TestMethod(string path)
        {
            XmlReaderSettings settings = new XmlReaderSettings(){ DtdProcessing = DtdProcessing.Prohibit };
            XmlReader reader = XmlReader.Create(path, settings);
        }
    }
}
```



