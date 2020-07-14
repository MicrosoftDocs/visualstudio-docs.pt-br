---
title: 'CA3076: execução de script XSLT insegura | Microsoft Docs'
ms.date: 11/15/2016
ms.technology: vs-ide-code-analysis
ms.topic: reference
ms.assetid: 53cb7a46-c564-488f-bc51-0e210a7853c9
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: wpickett
ms.openlocfilehash: 2b3e06bb7a150c4bb07eefc0571818f1127fe460
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545113"
---
# <a name="ca3076-insecure-xslt-script-execution"></a>CA3076: Execução de script XSLT não seguro
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

|Item|Valor|
|-|-|
|TypeName|InsecureXSLTScriptExecution|
|CheckId|CA3076|
|Categoria|Microsoft.Security|
|Alteração Significativa|Sem interrupção|

## <a name="cause"></a>Causa
 Se você executar as [transformações de linguagem de folhas de estilos extensível (XSLT)](https://support.microsoft.com/kb/313997) em aplicativos .net de forma insegura, o processador poderá [resolver referências de URI não confiáveis](https://msdn.microsoft.com/ba3e4d4f-1ee7-4226-a51a-78a1f1b5bd8a) que poderiam divulgar informações confidenciais a invasores, levando à negação de serviço e a ataques entre sites.

## <a name="rule-description"></a>Descrição da Regra
 O [XSLT](https://msdn.microsoft.com/6377ce5f-3c45-42a6-b7a9-ec8da588b60c) é um padrão World Wide Web CONSORTIUM (W3C) para transformar dados XML. Normalmente, o XSLT é usado para gravar folhas de estilo para transformar dados XML em outros formatos, como HTML, texto de comprimento fixo, texto separado por vírgula ou um formato XML diferente. Embora seja proibido por padrão, você pode optar por habilitá-lo para seu projeto.

 Para garantir que você não esteja expondo uma superfície de ataque, essa regra é disparada sempre que XslCompiledTransform.<xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> recebe instâncias de combinação não seguras do <xref:System.Xml.Xsl.XsltSettings> e <xref:System.Xml.XmlResolver> , o que permite o processamento de script mal-intencionado.

## <a name="how-to-fix-violations"></a>Como Corrigir Violações

- Substitua o argumento XsltSettings inseguro por XsltSettings.<xref:System.Xml.Xsl.XsltSettings.Default%2A> ou com uma instância que tenha desabilitado a função de documento e a execução de script.

- Substitua o <xref:System.Xml.XmlResolver> argumento por um nulo ou uma <xref:System.Xml.XmlSecureResolver> instância.

## <a name="when-to-suppress-warnings"></a>Quando Suprimir Avisos
 A menos que você tenha certeza de que a entrada é conhecida por ser de uma fonte confiável, não omita uma regra desse aviso.

## <a name="pseudo-code-examples"></a>Exemplos de pseudocódigo

### <a name="violation"></a>Infra

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

### <a name="violation"></a>Infra

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
