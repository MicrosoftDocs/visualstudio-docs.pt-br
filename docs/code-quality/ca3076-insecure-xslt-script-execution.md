---
title: 'CA3076: execução de script XSLT não seguro'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-code-analysis
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 74fe556d775e60dec5dde4528a1924e55ab4c2ed
ms.sourcegitcommit: 568bb0b944d16cfe1af624879fa3d3594d020187
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/13/2018
ms.locfileid: "45546386"
---
# <a name="ca3076-insecure-xslt-script-execution"></a>CA3076: execução de script XSLT não seguro

|||
|-|-|
|NomeDoTipo|InsecureXSLTScriptExecution|
|CheckId|CA3076|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa

Se você executar maneira insegura extensível folhas de estilos XSLT (linguagem) em aplicativos .NET, o processador pode resolver referências URI não confiáveis que poderiam revelar informações confidenciais para invasores, levando a negação de serviço e entre sites os ataques. Para obter mais informações, consulte [XSLT segurança Considerations(.NET Guide)](/dotnet/standard/data/xml/xslt-security-considerations).

## <a name="rule-description"></a>Descrição da regra

**XSLT** é um padrão de World Wide Web Consortium (W3C) para transformar os dados XML. XSLT normalmente é usado para gravar as folhas de estilo para transformar dados XML em outros formatos, como HTML, texto de comprimento fixo, texto separado por vírgula ou outro formato XML. Embora proibidas por padrão, você pode optar por habilitá-la para seu projeto.

Para garantir que você não estiver expondo uma superfície de ataque, essa regra dispara sempre que o XslCompiledTransform.<xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> recebe a instâncias de combinação inseguro de <xref:System.Xml.Xsl.XsltSettings> e <xref:System.Xml.XmlResolver>, que permite o processamento de script mal-intencionado.

## <a name="how-to-fix-violations"></a>Como corrigir violações

- Substitua o argumento XsltSettings inseguro XsltSettings.<xref:System.Xml.Xsl.XsltSettings.Default%2A> ou, com uma instância que desabilitou a execução de script e a função do documento.

- Substitua os <xref:System.Xml.XmlResolver> argumento com null ou um <xref:System.Xml.XmlSecureResolver> instância.

## <a name="when-to-suppress-warnings"></a>Quando suprimir avisos

A menos que você tiver certeza de que a entrada é conhecida por ser de uma fonte confiável, não suprima uma regra deste aviso.

## <a name="pseudo-code-examples"></a>Exemplos de código pseudo

### <a name="violation-that-uses-xsltsettingstrustedxslt"></a>Violação que usa XsltSettings.TrustedXslt

```csharp
using System.Xml;
using System.Xml.Xsl;

namespace TestNamespace
{
    class TestClass
    {
         void TestMethod()
        {
             XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();
             var settings = XsltSettings.TrustedXslt;
             var resolver = new XmlUrlResolver();
             xslCompiledTransform.Load("testStylesheet", settings, resolver); // warn
        }
    }
}
```

### <a name="solution-that-uses-xsltsettingsdefault"></a>Solução que usa XsltSettings.Default

```csharp
using System.Xml;
using System.Xml.Xsl;

namespace TestNamespace
{
    class TestClass
    {
        void TestMethod()
        {
            XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();
            var settings = XsltSettings.Default;
            var resolver = new XmlUrlResolver();
            xslCompiledTransform.Load("testStylesheet", settings, resolver);
        }
    }
}
```

### <a name="violationmdashdocument-function-and-script-execution-not-disabled"></a>Violação de&mdash;documentar a execução de função e o script não está desabilitada

```csharp
using System.Xml;
using System.Xml.Xsl;

namespace TestNamespace
{
    class TestClass
    {
        private static void TestMethod(XsltSettings settings)
        {
            try
            {
                XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();
                var resolver = new XmlUrlResolver();
                xslCompiledTransform.Load("testStylesheet", settings, resolver); // warn
            }
            catch { throw; }
            finally { }
        }
    }
}
```

### <a name="solutionmdashdisable-document-function-and-script-execution"></a>Solução&mdash;desabilitar a execução de função e script de documento

```csharp
using System.Xml;
using System.Xml.Xsl;

namespace TestNamespace
{
    class TestClass
    {
        private static void TestMethod(XsltSettings settings)
        {
            try
            {
                XslCompiledTransform xslCompiledTransform = new XslCompiledTransform();
                settings.EnableDocumentFunction = false;
                settings.EnableScript = false;
                var resolver = new XmlUrlResolver();
                xslCompiledTransform.Load("testStylesheet", settings, resolver);
            }
            catch { throw; }
            finally { }
        }
    }
}
```

## <a name="see-also"></a>Consulte também

- [Considerações de segurança XSLT (guia do .NET)](/dotnet/standard/data/xml/xslt-security-considerations)