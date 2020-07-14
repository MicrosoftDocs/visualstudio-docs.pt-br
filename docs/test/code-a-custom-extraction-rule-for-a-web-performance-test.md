---
title: Codificando uma regra de extração personalizada para um teste de desempenho Web
ms.date: 10/19/2016
ms.topic: how-to
helpviewer_keywords:
- extraction rules
- Web performance tests, creating custom extraction rules
- extraction rules, creating custom
ms.assetid: 6bcc5712-6cc6-4f59-8933-6e8078318c45
dev_langs:
- CSharp
- VB
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 00001662667ed7020909d23cf3cfbd4b8437eabf
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85288878"
---
# <a name="code-a-custom-extraction-rule-for-a-web-performance-test"></a>Codificar uma regra de extração personalizada para um teste de desempenho Web

Você pode criar suas próprias regras de extração. Para fazer isso, você deve derivar suas próprias regras de uma classe de regra de extração. As regras de extração derivam da classe base <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule>.

> [!NOTE]
> Também é possível criar regras de validação personalizadas. Para obter mais informações, consulte [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-create-a-custom-extraction-rule"></a>Para criar uma regra de extração personalizada

1. Abra um projeto de teste que contém um teste de desempenho Web.

2. (Opcional) Crie um projeto de biblioteca de classes separado no qual armazenar a regra de extração.

    > [!IMPORTANT]
    > Você pode criar a classe no mesmo projeto em que estão seus testes. No entanto, se desejar reutilizar a regra, é melhor criar um projeto de biblioteca de classes separado no qual armazenar a regra. Se você criar um projeto separado, será preciso concluir as etapas opcionais neste procedimento.

3. (Opcional) No projeto de biblioteca de classes, adicione uma referência à dll Microsoft.VisualStudio.QualityTools.WebTestFramework.

4. Crie uma classe que derive da classe <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule>. Implemente os membros <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract*> e <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.RuleName*>.

5. (Opcional) Crie o novo projeto de biblioteca de classes.

6. (Opcional) No projeto de teste, adicione uma referência ao projeto de biblioteca de classes que contém a regra de extração personalizada.

7. No projeto de teste, abra um teste de desempenho Web no **Editor de Testes de Desempenho Web**.

8. Para adicionar a regra de extração Personalizada, clique com o botão direito do mouse em uma solicitação de teste de desempenho Web e selecione **Adicionar regra de extração**.

     A caixa de diálogo **Adicionar Regra de Extração** é exibida. Você verá a regra de validação personalizada na lista **Selecionar Uma Regra**, juntamente com as regras de validação predefinidas. Selecione a regra de extração personalizada e escolha **OK**.

9. Execute o teste de desempenho na Web.

## <a name="example"></a>Exemplo

O código a seguir mostra uma implementação de uma regra de extração personalizada. Essa regra extrai o valor de um campo de entrada especificado. Use este exemplo como ponto de partida para suas próprias regras de extração personalizadas.

```csharp
using System;
using System.Collections.Generic;
using Microsoft.VisualStudio.TestTools.WebTesting;
using System.Globalization;

namespace ClassLibrary2
{
    //-------------------------------------------------------------------------
    // This class creates a custom extraction rule named "Custom Extract Input"
    // The user of the rule specifies the name of an input field, and the
    // rule attempts to extract the value of that input field.
    //-------------------------------------------------------------------------
    public class CustomExtractInput : ExtractionRule
    {
        /// Specify a name for use in the user interface.
        /// The user sees this name in the Add Extraction dialog box.
        //---------------------------------------------------------------------
        public override string RuleName
        {
            get { return "Custom Extract Input"; }
        }

        /// Specify a description for use in the user interface.
        /// The user sees this description in the Add Extraction dialog box.
        //---------------------------------------------------------------------
        public override string RuleDescription
        {
            get { return "Extracts the value from a specified input field"; }
        }

        // The name of the desired input field
        private string NameValue;
        public string Name
        {
            get { return NameValue; }
            set { NameValue = value; }
        }

        // The Extract method.  The parameter e contains the web performance test context.
        //---------------------------------------------------------------------
        public override void Extract(object sender, ExtractionEventArgs e)
        {
            if (e.Response.HtmlDocument != null)
            {
                foreach (HtmlTag tag in e.Response.HtmlDocument.GetFilteredHtmlTags(new string[] { "input" }))
                {
                    if (String.Equals(tag.GetAttributeValueAsString("name"), Name, StringComparison.InvariantCultureIgnoreCase))
                    {
                        string formFieldValue = tag.GetAttributeValueAsString("value");
                        if (formFieldValue == null)
                        {
                            formFieldValue = String.Empty;
                        }

                        // add the extracted value to the web performance test context
                        e.WebTest.Context.Add(this.ContextParameterName, formFieldValue);
                        e.Success = true;
                        return;
                    }
                }
            }
            // If the extraction fails, set the error text that the user sees
            e.Success = false;
            e.Message = String.Format(CultureInfo.CurrentCulture, "Not Found: {0}", Name);
        }
    }
}
```

```vb
Imports System
Imports System.Collections.Generic
Imports Microsoft.VisualStudio.TestTools.WebTesting
Imports System.Globalization

Namespace ClassLibrary2

    '-------------------------------------------------------------------------
    ' This class creates a custom extraction rule named "Custom Extract Input"
    ' The user of the rule specifies the name of an input field, and the
    ' rule attempts to extract the value of that input field.
    '-------------------------------------------------------------------------
    Public Class CustomExtractInput
        Inherits ExtractionRule

        ' Specify a name for use in the user interface.
        ' The user sees this name in the Add Extraction dialog box.
        '---------------------------------------------------------------------
        Public Overrides ReadOnly Property RuleName() As String
            Get
                Return "Custom Extract Input"
            End Get
        End Property

        ' Specify a description for use in the user interface.
        ' The user sees this description in the Add Extraction dialog box.
        '---------------------------------------------------------------------
        Public Overrides ReadOnly Property RuleDescription() As String
            Get
                Return "Extracts the value from a specified input field"
            End Get
        End Property

        ' The name of the desired input field
        Private NameValue As String
        Public Property Name() As String
            Get
                Return NameValue
            End Get
            Set(ByVal value As String)
                NameValue = value
            End Set
        End Property

        ' The Extract method.  The parameter e contains the web performance test context.
        '---------------------------------------------------------------------
        Public Overrides Sub Extract(ByVal sender As Object, ByVal e As ExtractionEventArgs)

            If Not e.Response.HtmlDocument Is Nothing Then

                For Each tag As HtmlTag In e.Response.HtmlDocument.GetFilteredHtmlTags(New String() {"input"})

                    If String.Equals(tag.GetAttributeValueAsString("name"), Name, StringComparison.InvariantCultureIgnoreCase) Then

                        Dim formFieldValue As String = tag.GetAttributeValueAsString("value")
                        If formFieldValue Is Nothing Then

                            formFieldValue = String.Empty
                        End If

                        ' add the extracted value to the web performance test context
                        e.WebTest.Context.Add(Me.ContextParameterName, formFieldValue)
                        e.Success = True
                        Return
                    End If
                Next
            End If
            ' If the extraction fails, set the error text that the user sees
            e.Success = False
            e.Message = String.Format(CultureInfo.CurrentCulture, "Not Found: {0}", Name)
        End Sub
    End Class
End Namespace
```

O método <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract*> contém a funcionalidade principal de uma regra de extração. O método <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule.Extract*> no exemplo anterior usa um <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionEventArgs> que fornece a resposta gerada pela solicitação que essa regra de extração cobre. A resposta contém um <xref:Microsoft.VisualStudio.TestTools.WebTesting.HtmlDocument> que contém todos os marcadores na resposta. Os marcadores de entrada são filtrados no <xref:Microsoft.VisualStudio.TestTools.WebTesting.HtmlDocument>. Cada marcação de entrada é examinada quanto a um atributo chamado `name`, cujo valor é igual àquele fornecido pelo usuário para a propriedade `Name`. Se uma marcação com esse atributo correspondente for encontrada, será feita uma tentativa de extrair um valor contido no atributo `value`, se um atributo de valor existir. Se existir, o nome e o valor do marcador serão extraídos e adicionados ao contexto de teste de desempenho na Web. A regra de extração é aprovada.

## <a name="see-also"></a>Veja também

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.ExtractionRule>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractAttributeValue>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractFormField>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractHttpHeader>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractRegularExpression>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractText>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ExtractHiddenFields>
- [Codificando uma regra de validação personalizada para um teste de desempenho para Web](../test/code-a-custom-validation-rule-for-a-web-performance-test.md)
