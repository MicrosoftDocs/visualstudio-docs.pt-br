---
title: Codificando uma regra de validação personalizada para um teste de desempenho Web
ms.date: 10/19/2016
ms.topic: conceptual
helpviewer_keywords:
- custom validation rules
- validation rules, creating
- web performance tests, creating custom validation rules
- rules, validation
- validation rules
ms.assetid: 989124bc-1a86-41f7-b37d-8f9e54dd4f0b
dev_langs:
- CSharp
- VB
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.openlocfilehash: 407c6e5b8beec118ce8f25edb35e66722990e8ca
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53047668"
---
# <a name="code-a-custom-validation-rule-for-a-web-performance-test"></a>Codificar uma regra de validação personalizada para um teste de desempenho Web

Você pode criar suas próprias regras de validação. Para fazer isso, você deve derivar sua própria classe de regra de uma classe de regra de validação. As regras de validação derivam-se da classe base <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule>.

> [!NOTE]
> Também é possível criar regras de extração personalizadas. Para obter mais informações, consulte [Criar código personalizado e plug-ins para testes de carga](../test/create-custom-code-and-plug-ins-for-load-tests.md).

[!INCLUDE [web-load-test-deprecated](includes/web-load-test-deprecated.md)]

## <a name="to-create-custom-validation-rules"></a>Para criar regras de validação personalizadas

1.  Abra um projeto de teste que contenha um teste de desempenho na Web.

2.  (Opcional) Crie um projeto de biblioteca de classes separado na qual armazenar a regra de validação.

    > [!IMPORTANT]
    > Você pode criar a classe no mesmo projeto em que estão seus testes. No entanto, se desejar reutilizar a regra, é melhor criar um projeto de biblioteca de classes separado no qual armazenar a regra. Se você criar um projeto separado, será preciso concluir as etapas opcionais neste procedimento.

3.  (Opcional) No projeto de biblioteca de classes, adicione uma referência à DLL Microsoft.VisualStudio.QualityTools.WebTestFramework.

4.  Crie uma classe que derive da classe <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule>. Implemente os membros <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule.Validate*> e <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule.RuleName*>.

5.  (Opcional) Crie o novo projeto de biblioteca de classes.

6.  (Opcional) No projeto de teste, adicione uma referência ao projeto de biblioteca de classes que contenha a regra de validação personalizada.

7.  No projeto de teste, abra um teste de desempenho Web no **Editor de Testes de Desempenho Web**.

8.  Para adicionar a regra de validação personalizada a uma solicitação de teste de desempenho Web, clique com o botão direito do mouse em uma solicitação e selecione **Adicionar regra de validação**.

     A caixa de diálogo **Adicionar regra de validação** será exibida. Você verá a regra de validação personalizada na lista **Selecionar Uma Regra**, juntamente com as regras de validação predefinidas. Selecione sua regra de validação personalizada e escolha **OK**.

9. Execute o teste de desempenho na Web.

## <a name="example"></a>Exemplo

O código a seguir mostra uma implementação de uma regra de validação personalizada. Essa regra de validação imita o comportamento da regra de validação de marca obrigatória predefinida. Use este exemplo como ponto de partida para suas próprias regras de validação personalizadas.

> [!WARNING]
> As propriedades públicas no código de um validador personalizado não podem conter valores nulos.

```csharp
using System;
using System.Diagnostics;
using System.Globalization;
using Microsoft.VisualStudio.TestTools.WebTesting;

namespace SampleWebTestRules
{
    //-------------------------------------------------------------------------
    // This class creates a custom validation rule named "Custom Validate Tag"
    // The custom validation rule is used to check that an HTML tag with a
    // particular name is found one or more times in the HTML response.
    // The user of the rule can specify the HTML tag to look for, and the
    // number of times that it must appear in the response.
    //-------------------------------------------------------------------------
    public class CustomValidateTag : ValidationRule
    {
        /// Specify a name for use in the user interface.
        /// The user sees this name in the Add Validation dialog box.
        //---------------------------------------------------------------------
        public override string RuleName
        {
            get { return "Custom Validate Tag"; }
        }

        /// Specify a description for use in the user interface.
        /// The user sees this description in the Add Validation dialog box.
        //---------------------------------------------------------------------
        public override string RuleDescription
        {
            get { return "Validates that the specified tag exists on the page."; }
        }

        // The name of the required tag
        private string RequiredTagNameValue;
        public string RequiredTagName
        {
            get { return RequiredTagNameValue; }
            set { RequiredTagNameValue = value; }
        }

        // The minimum number of times the tag must appear in the response
        private int MinOccurrencesValue;
        public int MinOccurrences
        {
            get { return MinOccurrencesValue; }
            set { MinOccurrencesValue = value; }
        }

        // Validate is called with the test case Context and the request context.
        // These allow the rule to examine both the request and the response.
        //---------------------------------------------------------------------
        public override void Validate(object sender, ValidationEventArgs e)
        {
            bool validated = false;
            int numTagsFound = 0;

            foreach (HtmlTag tag in e.Response.HtmlDocument.GetFilteredHtmlTags(RequiredTagName))
            {
                Debug.Assert(string.Equals(tag.Name, RequiredTagName, StringComparison.InvariantCultureIgnoreCase));

                if (++numTagsFound >= MinOccurrences)
                {
                    validated = true;
                    break;
                }
            }

            e.IsValid = validated;

            // If the validation fails, set the error text that the user sees
            if (!validated)
            {
                if (numTagsFound > 0)
                {
                    e.Message = String.Format("Only found {0} occurrences of the tag", numTagsFound);
                }
                else
                {
                    e.Message = String.Format("Did not find any occurrences of tag '{0}'", RequiredTagName);
                }
            }
        }
    }
}
```

```vb
Imports System
Imports System.Diagnostics
Imports System.Globalization
Imports Microsoft.VisualStudio.TestTools.WebTesting

Namespace SampleWebTestRules

    '-------------------------------------------------------------------------
    ' This class creates a custom validation rule named "Custom Validate Tag"
    ' The custom validation rule is used to check that an HTML tag with a
    ' particular name is found one or more times in the HTML response.
    ' The user of the rule can specify the HTML tag to look for, and the
    ' number of times that it must appear in the response.
    '-------------------------------------------------------------------------
    Public Class CustomValidateTag
        Inherits Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule

        ' Specify a name for use in the user interface.
        ' The user sees this name in the Add Validation dialog box.
        '---------------------------------------------------------------------
        Public Overrides ReadOnly Property RuleName() As String
            Get
                Return "Custom Validate Tag"
            End Get
        End Property

        ' Specify a description for use in the user interface.
        ' The user sees this description in the Add Validation dialog box.
        '---------------------------------------------------------------------
        Public Overrides ReadOnly Property RuleDescription() As String
            Get
                Return "Validates that the specified tag exists on the page."
            End Get
        End Property

        ' The name of the required tag
        Private RequiredTagNameValue As String
        Public Property RequiredTagName() As String
            Get
                Return RequiredTagNameValue
            End Get
            Set(ByVal value As String)
                RequiredTagNameValue = value
            End Set
        End Property

        ' The minimum number of times the tag must appear in the response
        Private MinOccurrencesValue As Integer
        Public Property MinOccurrences() As Integer
            Get
                Return MinOccurrencesValue
            End Get
            Set(ByVal value As Integer)
                MinOccurrencesValue = value
            End Set
        End Property

        ' Validate is called with the test case Context and the request context.
        ' These allow the rule to examine both the request and the response.
        '---------------------------------------------------------------------
        Public Overrides Sub Validate(ByVal sender As Object, ByVal e As ValidationEventArgs)

            Dim validated As Boolean = False
            Dim numTagsFound As Integer = 0

            For Each tag As HtmlTag In e.Response.HtmlDocument.GetFilteredHtmlTags(RequiredTagName)

                Debug.Assert(String.Equals(tag.Name, RequiredTagName, StringComparison.InvariantCultureIgnoreCase))

                numTagsFound += 1
                If numTagsFound >= MinOccurrences Then

                    validated = True
                    Exit For
                End If
            Next

            e.IsValid = validated

            ' If the validation fails, set the error text that the user sees
            If Not (validated) Then
                If numTagsFound > 0 Then
                    e.Message = String.Format("Only found {0} occurrences of the tag", numTagsFound)
                Else
                    e.Message = String.Format("Did not find any occurrences of tag '{0}'", RequiredTagName)
                End If
            End If
        End Sub
    End Class
End Namespace
```

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualStudio.TestTools.WebTesting.ValidationRule>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidateFormField>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleRequestTime>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleRequiredAttributeValue>
- <xref:Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleRequiredTag>
- [Codificando uma regra de extração personalizada para um teste de desempenho Web](../test/code-a-custom-extraction-rule-for-a-web-performance-test.md)