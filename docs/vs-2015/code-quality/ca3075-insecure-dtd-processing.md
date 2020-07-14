---
title: 'CA3075: processamento de DTD inseguro | Microsoft Docs'
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 65798d66-7a30-4359-b064-61a8660c1eed
caps.latest.revision: 19
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: d8cd78b529618504b5f14905a764c369da249fe2
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545165"
---
# <a name="ca3075-insecure-dtd-processing"></a>CA3075: Processamento de DTD não seguro
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|InsecureDTDProcessing|
|CheckId|CA3075|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Se você usar instâncias de <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A> inseguras ou referenciar origens de entidade externa, o analisador poderá aceitar a entrada não confiável e divulgar as informações confidenciais para invasores.

## <a name="rule-description"></a>Descrição da Regra
 Uma [DTD (definição de tipo de documento)](https://msdn.microsoft.com/library/aa468547.aspx) é uma das duas maneiras que um analisador XML pode determinar a validade de um documento, conforme definido pelo [World Wide Web Consortium (W3C) linguagem XML (XML) 1,0](https://www.w3.org/TR/2008/REC-xml-20081126/). Essa regra busca Propriedades e instâncias em que os dados não confiáveis são aceitos para avisar os desenvolvedores sobre possíveis ameaças de [divulgação de informações](https://msdn.microsoft.com/library/4064c89f-afa6-444a-aa7e-807ef072131c) , o que pode levar a ataques [de negação de serviço (dos)](https://msdn.microsoft.com/library/dfb150f3-d598-4697-a5e6-6779e4f9b600) . Esta regra é disparada quando:

- DtdProcessing está habilitado na <xref:System.Xml.XmlReader> instância, que resolve entidades XML externas usando <xref:System.Xml.XmlUrlResolver> .

- A <xref:System.Xml.XmlNode.InnerXml%2A> propriedade no XML está definida.

- <xref:System.Xml.XmlReaderSettings.DtdProcessing%2A>a propriedade está definida como Parse.

- A entrada não confiável é processada usando <xref:System.Xml.XmlResolver> em vez de <xref:System.Xml.XmlSecureResolver> .

- O XmlReader.<xref:System.Xml.XmlReader.Create%2A> o método é invocado com uma <xref:System.Xml.XmlReaderSettings> instância insegura ou nenhuma instância.

- <xref:System.Xml.XmlReader>é criado com valores ou configurações padrão inseguras.

  Em cada um desses casos, o resultado é o mesmo: o conteúdo do sistema de arquivos ou compartilhamentos de rede do computador em que o XML é processado será exposto ao invasor, que pode ser usado como um vetor de DoS.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações

- Pegue e processe todas as exceções de XmlTextReader corretamente para evitar a divulgação de informações de caminho.

- Use o  <xref:System.Xml.XmlSecureResolver> para restringir os recursos que o XmlTextReader pode acessar.

- Não permita que o  <xref:System.Xml.XmlReader> abra nenhum recurso externo definindo a <xref:System.Xml.XmlResolver> propriedade como **NULL**.

- Certifique-se de que a <xref:System.Data.DataViewManager.DataViewSettingCollectionString%2A> propriedade de <xref:System.Data.DataViewManager> seja atribuída de uma fonte confiável.

  .NET 3,5 e anterior

- Desabilite o processamento de DTD se você estiver lidando com fontes não confiáveis definindo a  <xref:System.Xml.XmlReaderSettings.ProhibitDtd%2A> propriedade como **true** .

- A classe XmlTextReader tem uma demanda de herança de confiança total. Consulte [demandas de herança](https://msdn.microsoft.com/28b9adbb-8f08-4f10-b856-dbf59eb932d9) para obter mais informações.

  .NET 4 e posterior

- Evite habilitar DtdProcessing se você estiver lidando com fontes não confiáveis definindo a propriedade DtdProcessing como [proibir ou ignorar](https://msdn.microsoft.com/library/system.xml.dtdprocessing.aspx)

- Verifique se o método Load () usa uma instância de XmlReader em todos os casos de InnerXml.

> [!NOTE]
> Essa regra pode relatar falsos positivos em algumas instâncias de XmlSecureResolver válidas. Estamos trabalhando para solucionar esse problema em meados de 2016.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
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
    XmlTextReader reader = new XmlTextReader(sreader) { DtdProcessing = DtdProcessing.Prohibit };
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
            XmlTextReader reader = new XmlTextReader(stream) { DtdProcessing = DtdProcessing.Prohibit } ;
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
            XmlTextReader reader = new XmlTextReader(path) { DtdProcessing = DtdProcessing.Prohibit };
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
