---
title: 'CA3076: Execução de Script XSLT não | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 53cb7a46-c564-488f-bc51-0e210a7853c9
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: wpickett
ms.openlocfilehash: 39aebc0e7681b139e021c48c12a87d4b060cc7af
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49911467"
---
# <a name="ca3076-insecure-xslt-script-execution"></a>CA3076: execução de script XSLT não seguro
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|||
|-|-|
|NomeDoTipo|InsecureXSLTScriptExecution|
|CheckId|CA3076|
|Categoria|Microsoft.Security|
|Alteração Significativa|Não separável|

## <a name="cause"></a>Causa
 Se você executar [extensível folhas de estilos XSLT (linguagem)](https://support.microsoft.com/en-us/kb/313997) em aplicativos .NET de maneira insegura, o processador pode [resolver referências de URI não confiáveis](http://msdn.microsoft.com/en-us/ba3e4d4f-1ee7-4226-a51a-78a1f1b5bd8a) que poderia revelar confidenciais informações para invasores, levando a ataques de negação de serviço e Cross-Site.

## <a name="rule-description"></a>Descrição da Regra
 [XSLT](http://msdn.microsoft.com/en-us/6377ce5f-3c45-42a6-b7a9-ec8da588b60c) é um padrão de World Wide Web Consortium (W3C) para transformar os dados XML. XSLT normalmente é usado para gravar as folhas de estilo para transformar dados XML em outros formatos, como HTML, fixa comprimento texto, texto separado por vírgula ou outro formato XML. Embora proibidas por padrão, você pode optar por habilitá-la para seu projeto.

 Para garantir que você não estiver expondo uma superfície de ataque, essa regra dispara sempre que o XslCompiledTransform.<xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> recebe a instâncias de combinação inseguro de <xref:System.Xml.Xsl.XsltSettings> e <xref:System.Xml.XmlResolver>, que permite o processamento de script mal-intencionado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações

-   Substitua o argumento XsltSettings inseguro XsltSettings.<xref:System.Xml.Xsl.XsltSettings.Default%2A> ou, com uma instância que desabilitou a execução de script e a função do documento.

-   Substitua os <xref:System.Xml.XmlResolver> argumento com null ou um <xref:System.Xml.XmlSecureResolver> instância.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 A menos que você tiver certeza de que a entrada é conhecida por ser de uma fonte confiável, não suprima uma regra deste aviso.

## <a name="pseudo-code-examples"></a>Exemplos de código pseudo

### <a name="violation"></a>Violação

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

### <a name="solution"></a>Solução

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

### <a name="violation"></a>Violação

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

### <a name="solution"></a>Solução

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



