---
title: 'CA3075: Processamento de DTD não seguro'
ms.date: 03/18/2019
ms.topic: reference
ms.assetid: 65798d66-7a30-4359-b064-61a8660c1eed
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 42efb51dfe9c447538fe8f01bdd37c73bf993d8f
ms.sourcegitcommit: 0c2523d975d48926dd2b35bcd2d32a8ae14c06d8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2019
ms.locfileid: "71237111"
---
# <a name="ca3075-insecure-dtd-processing"></a>CA3075: Processamento de DTD não seguro

|||
|-|-|
|NomeDoTipo|InsecureDTDProcessing|
|CheckId|CA3075|
|Categoria|Microsoft.Security|
|Alteração significativa|Sem interrupção|

## <a name="cause"></a>Causa

Se você usar instâncias de <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A> inseguras ou referenciar origens de entidade externa, o analisador poderá aceitar a entrada não confiável e divulgar as informações confidenciais para invasores.

## <a name="rule-description"></a>Descrição da regra

Uma *DTD (definição de tipo de documento)* é uma das duas maneiras que um analisador XML pode determinar a validade de um documento, conforme definido pelo [World Wide Web Consortium (W3C) linguagem XML (XML) 1,0](http://www.w3.org/TR/2008/REC-xml-20081126/). Essa regra busca Propriedades e instâncias em que os dados não confiáveis são aceitos para avisar os desenvolvedores sobre possíveis ameaças de [divulgação de informações](/dotnet/framework/wcf/feature-details/information-disclosure) ou ataques [de negação de serviço (dos)](/dotnet/framework/wcf/feature-details/denial-of-service) . Esta regra é disparada quando:

- DtdProcessing está habilitado na <xref:System.Xml.XmlReader> instância, que resolve entidades XML externas usando. <xref:System.Xml.XmlUrlResolver>

- A <xref:System.Xml.XmlNode.InnerXml%2A> Propriedade no XML está definida.

- <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A>a propriedade está definida como Parse.

- A entrada não confiável é processada <xref:System.Xml.XmlResolver> usando em <xref:System.Xml.XmlSecureResolver>vez de.

- O <xref:System.Xml.XmlReader.Create%2A?displayProperty=nameWithType> método é invocado com uma instância <xref:System.Xml.XmlReaderSettings> insegura ou nenhuma instância.

- <xref:System.Xml.XmlReader>é criado com valores ou configurações padrão inseguras.

Em cada um desses casos, o resultado é o mesmo: o conteúdo do sistema de arquivos ou compartilhamentos de rede do computador onde o XML é processado será exposto ao invasor, ou o processamento de DTD pode ser usado como um vetor de DoS.

## <a name="how-to-fix-violations"></a>Como corrigir violações

- Pegue e processe todas as exceções de XmlTextReader corretamente para evitar a divulgação de informações de caminho.

- Use o <xref:System.Xml.XmlSecureResolver> para restringir os recursos que o XmlTextReader pode acessar.

- Não permita que o <xref:System.Xml.XmlReader> abra nenhum recurso externo definindo a <xref:System.Xml.XmlResolver> Propriedade como **NULL**.

- Certifique-se <xref:System.Data.DataViewManager.DataViewSettingCollectionString%2A?displayProperty=nameWithType> de que a propriedade seja atribuída de uma fonte confiável.

**.NET 3,5 e anterior**

- Desabilite o processamento de DTD se você estiver lidando com fontes não confiáveis definindo <xref:System.Xml.XmlReaderSettings.ProhibitDtd%2A> a propriedade como **true**.

- A classe XmlTextReader tem uma demanda de herança de confiança total.

**.NET 4 e posterior**

- Evite habilitar DtdProcessing se você estiver lidando com fontes não confiáveis definindo a <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A?displayProperty=nameWithType> Propriedade como **proibir** ou **ignorar**.

- Verifique se o método Load () usa uma instância de XmlReader em todos os casos de InnerXml.

> [!NOTE]
> Essa regra pode relatar falsos positivos em algumas instâncias de XmlSecureResolver válidas.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

A menos que você tenha certeza de que a entrada é conhecida por ser de uma fonte confiável, não omita uma regra desse aviso.

## <a name="pseudo-code-examples"></a>Exemplos de pseudocódigo

### <a name="violation"></a>Infra

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

### <a name="violation"></a>Infra

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
    XmlReader reader = XmlReader.Create(sreader, new XmlReaderSettings() { XmlResolver = null });
    doc.Load(reader);
}
```

### <a name="violation"></a>Infra

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
            XmlReader reader = XmlReader.Create(stream, new XmlReaderSettings() { XmlResolver = null });
            serializer.Deserialize(reader );
        }
    }
}
```

### <a name="violation"></a>Infra

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
            XmlReader reader = XmlReader.Create(path, new XmlReaderSettings() { XmlResolver = null });
            XPathDocument doc = new XPathDocument(reader);
        }
    }
}
```

### <a name="violation"></a>Infra

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
            XmlReaderSettings settings = new XmlReaderSettings() { XmlResolver = null };
            XmlReader reader = XmlReader.Create(path, settings);
        }
    }
}
```
