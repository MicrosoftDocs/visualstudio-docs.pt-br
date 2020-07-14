---
title: 'Instruções passo a passo: criando um processador de diretiva'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- text templates, custom directive processors
- walkthroughs [text templates], directive processor
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 4efe12b9871dc07bd7427e1567973701d3c6c527
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532230"
---
# <a name="walkthrough-create-a-custom-directive-processor"></a>Passo a passo: criar um processador de diretiva personalizado

Os *processadores de diretiva* funcionam adicionando código à *classe de transformação gerada*. Se você chamar uma *diretiva* de um *modelo de texto*, o restante do código que você escrever no seu modelo de texto poderá contar com a funcionalidade que a diretiva fornece.

Você pode escrever seus próprios processadores de diretriz personalizados. Isso permite que você personalize seus modelos de texto. Para criar um processador de diretriz personalizado, é preciso criar uma classe herdada de <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> ou de <xref:Microsoft.VisualStudio.TextTemplating.RequiresProvidesDirectiveProcessor>.

As tarefas ilustradas nesta explicação passo a passo incluem o seguinte:

- Criar um processador de diretiva personalizado

- Registrar o processador de diretivas

- Testar o processador de diretivas

## <a name="create-a-custom-directive-processor"></a>Criar um processador de diretriz personalizado

Neste passo a passo, você cria um processador de diretriz personalizado. Você adiciona uma diretiva personalizado que lê um arquivo XML, armazena-o em uma variável <xref:System.Xml.XmlDocument> e o expõe por meio de uma propriedade. Na seção “Testando o processador de diretriz”, você usa essa propriedade em um modelo de texto para acessar o arquivo XML.

A chamada para a diretiva personalizada é semelhante a esta:

`<#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<Your Path>DocFile.xml" #>`

O processador de diretriz personalizado adiciona a variável e a propriedade à classe de transformação gerada. A diretiva que você escreve usa as classes <xref:System.CodeDom> para criar o código que o mecanismo adiciona à classe de transformação gerada. As <xref:System.CodeDom> classes criam código no Visual C# ou Visual Basic, dependendo do idioma especificado no `language` parâmetro da `template` diretiva. A linguagem do processador de diretriz e a linguagem do modelo de texto que está acessando o processador de diretriz não precisam coincidir.

O código que a diretiva cria é semelhante a este:

```csharp
private System.Xml.XmlDocument document0Value;

public virtual System.Xml.XmlDocument Document0
{
  get
  {
    if ((this.document0Value == null))
    {
      this.document0Value = XmlReaderHelper.ReadXml(<FileNameParameterValue>);
    }
    return this.document0Value;
  }
}
```

```vb
Private document0Value As System.Xml.XmlDocument

Public Overridable ReadOnly Property Document0() As System.Xml.XmlDocument
    Get
        If (Me.document0Value Is Nothing) Then
            Me.document0Value = XmlReaderHelper.ReadXml(<FileNameParameterValue>)
        End If
        Return Me.document0Value
    End Get
End Property
```

### <a name="to-create-a-custom-directive-processor"></a>Para criar um processador de diretriz personalizado

1. No Visual Studio, crie um novo projeto de biblioteca de classes C# ou Visual Basic chamado CustomDP.

    > [!NOTE]
    > Se você quiser instalar o processador de diretiva em mais de um computador, é melhor usar um projeto de VSIX (extensão do Visual Studio) e incluir um arquivo. pkgdef na extensão. Para obter mais informações, consulte [implantando um processador de diretiva personalizada](../modeling/deploying-a-custom-directive-processor.md).

2. Adicione referências a esses assemblies:

    - **Microsoft. VisualStudio. TextTemplating. \* . 0**

    - **Microsoft. VisualStudio. TextTemplating. interfaces. \* . 0**

3. Substitua o código em **Class1** pelo código a seguir. Este código define uma classe CustomDirectiveProcessor que herda da classe <xref:Microsoft.VisualStudio.TextTemplating.DirectiveProcessor> e implementa os métodos necessários.

    ```csharp
    using System;
    using System.CodeDom;
    using System.CodeDom.Compiler;
    using System.Collections.Generic;
    using System.Globalization;
    using System.IO;
    using System.Text;
    using System.Xml;
    using System.Xml.Serialization;
    using Microsoft.VisualStudio.TextTemplating;

    namespace CustomDP
    {
        public class CustomDirectiveProcessor : DirectiveProcessor
        {
            // This buffer stores the code that is added to the
            // generated transformation class after all the processing is done.
            // ---------------------------------------------------------------------
            private StringBuilder codeBuffer;

            // Using a Code Dom Provider creates code for the
            // generated transformation class in either Visual Basic or C#.
            // If you want your directive processor to support only one language, you
            // can hard code the code you add to the generated transformation class.
            // In that case, you do not need this field.
            // --------------------------------------------------------------------------
            private CodeDomProvider codeDomProvider;

            // This stores the full contents of the text template that is being processed.
            // --------------------------------------------------------------------------
            private String templateContents;

            // These are the errors that occur during processing. The engine passes
            // the errors to the host, and the host can decide how to display them,
            // for example the host can display the errors in the UI
            // or write them to a file.
            // ---------------------------------------------------------------------
            private CompilerErrorCollection errorsValue;
            public new CompilerErrorCollection Errors
            {
                get { return errorsValue; }
            }

            // Each time this directive processor is called, it creates a new property.
            // We count how many times we are called, and append "n" to each new
            // property name. The property names are therefore unique.
            // -----------------------------------------------------------------------------
            private int directiveCount = 0;

            public override void Initialize(ITextTemplatingEngineHost host)
            {
                // We do not need to do any initialization work.
            }

            public override void StartProcessingRun(CodeDomProvider languageProvider, String templateContents, CompilerErrorCollection errors)
            {
                // The engine has passed us the language of the text template
                // we will use that language to generate code later.
                // ----------------------------------------------------------
                this.codeDomProvider = languageProvider;
                this.templateContents = templateContents;
                this.errorsValue = errors;

                this.codeBuffer = new StringBuilder();
            }

            // Before calling the ProcessDirective method for a directive, the
            // engine calls this function to see whether the directive is supported.
            // Notice that one directive processor might support many directives.
            // ---------------------------------------------------------------------
            public override bool IsDirectiveSupported(string directiveName)
            {
                if (string.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) == 0)
                {
                    return true;
                }
                if (string.Compare(directiveName, "SuperCoolDirective", StringComparison.OrdinalIgnoreCase) == 0)
                {
                    return true;
                }
                return false;
            }

            public override void ProcessDirective(string directiveName, IDictionary<string, string> arguments)
            {
                if (string.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) == 0)
                {
                    string fileName;

                    if (!arguments.TryGetValue("FileName", out fileName))
                    {
                        throw new DirectiveProcessorException("Required argument 'FileName' not specified.");
                    }

                    if (string.IsNullOrEmpty(fileName))
                    {
                        throw new DirectiveProcessorException("Argument 'FileName' is null or empty.");
                    }

                    // Now we add code to the generated transformation class.
                    // This directive supports either Visual Basic or C#, so we must use the
                    // System.CodeDom to create the code.
                    // If a directive supports only one language, you can hard code the code.
                    // --------------------------------------------------------------------------

                    CodeMemberField documentField = new CodeMemberField();

                    documentField.Name = "document" + directiveCount + "Value";
                    documentField.Type = new CodeTypeReference(typeof(XmlDocument));
                    documentField.Attributes = MemberAttributes.Private;

                    CodeMemberProperty documentProperty = new CodeMemberProperty();

                    documentProperty.Name = "Document" + directiveCount;
                    documentProperty.Type = new CodeTypeReference(typeof(XmlDocument));
                    documentProperty.Attributes = MemberAttributes.Public;
                    documentProperty.HasSet = false;
                    documentProperty.HasGet = true;

                    CodeExpression fieldName = new CodeFieldReferenceExpression(new CodeThisReferenceExpression(), documentField.Name);
                    CodeExpression booleanTest = new CodeBinaryOperatorExpression(fieldName, CodeBinaryOperatorType.IdentityEquality, new CodePrimitiveExpression(null));
                    CodeExpression rightSide = new CodeMethodInvokeExpression(new CodeTypeReferenceExpression("XmlReaderHelper"), "ReadXml", new CodePrimitiveExpression(fileName));
                    CodeStatement[] thenSteps = new CodeStatement[] { new CodeAssignStatement(fieldName, rightSide) };

                    CodeConditionStatement ifThen = new CodeConditionStatement(booleanTest, thenSteps);
                    documentProperty.GetStatements.Add(ifThen);

                    CodeStatement s = new CodeMethodReturnStatement(fieldName);
                    documentProperty.GetStatements.Add(s);

                    CodeGeneratorOptions options = new CodeGeneratorOptions();
                    options.BlankLinesBetweenMembers = true;
                    options.IndentString = "    ";
                    options.VerbatimOrder = true;
                    options.BracingStyle = "C";

                    using (StringWriter writer = new StringWriter(codeBuffer, CultureInfo.InvariantCulture))
                    {
                        codeDomProvider.GenerateCodeFromMember(documentField, writer, options);
                        codeDomProvider.GenerateCodeFromMember(documentProperty, writer, options);
                    }
                }

                // One directive processor can contain many directives.
                // If you want to support more directives, the code goes here...
                // -----------------------------------------------------------------
                if (string.Compare(directiveName, "supercooldirective", StringComparison.OrdinalIgnoreCase) == 0)
                {
                    // Code for SuperCoolDirective goes here...
                }

                // Track how many times the processor has been called.
                // -----------------------------------------------------------------
                directiveCount++;

            }

            public override void FinishProcessingRun()
            {
                this.codeDomProvider = null;

                // Important: do not do this:
                // The get methods below are called after this method
                // and the get methods can access this field.
                // -----------------------------------------------------------------
                // this.codeBuffer = null;
            }

            public override string GetPreInitializationCodeForProcessingRun()
            {
                // Use this method to add code to the start of the
                // Initialize() method of the generated transformation class.
                // We do not need any pre-initialization, so we will just return "".
                // -----------------------------------------------------------------
                // GetPreInitializationCodeForProcessingRun runs before the
                // Initialize() method of the base class.
                // -----------------------------------------------------------------
                return String.Empty;
            }

            public override string GetPostInitializationCodeForProcessingRun()
            {
                // Use this method to add code to the end of the
                // Initialize() method of the generated transformation class.
                // We do not need any post-initialization, so we will just return "".
                // ------------------------------------------------------------------
                // GetPostInitializationCodeForProcessingRun runs after the
                // Initialize() method of the base class.
                // -----------------------------------------------------------------
                return String.Empty;
            }

            public override string GetClassCodeForProcessingRun()
            {
                //Return the code to add to the generated transformation class.
                // -----------------------------------------------------------------
                return codeBuffer.ToString();
            }

            public override string[] GetReferencesForProcessingRun()
            {
                // This returns the references that we want to use when
                // compiling the generated transformation class.
                // -----------------------------------------------------------------
                // We need a reference to this assembly to be able to call
                // XmlReaderHelper.ReadXml from the generated transformation class.
                // -----------------------------------------------------------------
                return new string[]
                {
                    "System.Xml",
                    this.GetType().Assembly.Location
                };
            }

            public override string[] GetImportsForProcessingRun()
            {
                //This returns the imports or using statements that we want to
                //add to the generated transformation class.
                // -----------------------------------------------------------------
                //We need CustomDP to be able to call XmlReaderHelper.ReadXml
                //from the generated transformation class.
                // -----------------------------------------------------------------
                return new string[]
                {
                    "System.Xml",
                    "CustomDP"
                };
            }
        }

        // -------------------------------------------------------------------------
        // The code that we are adding to the generated transformation class
        // will call this method.
        // -------------------------------------------------------------------------
        public static class XmlReaderHelper
        {
            public static XmlDocument ReadXml(string fileName)
            {
                XmlDocument d = new XmlDocument();

                using (XmlReader reader = XmlReader.Create(fileName))
                {
                    try
                    {
                        d.Load(reader);
                    }
                    catch (System.Xml.XmlException e)
                    {
                        throw new DirectiveProcessorException("Unable to read the XML file.", e);
                    }
                }
                return d;
            }
        }
    }
    ```

    ```vb
    Imports System
    Imports System.CodeDom
    Imports System.CodeDom.Compiler
    Imports System.Collections.Generic
    Imports System.Globalization
    Imports System.IO
    Imports System.Text
    Imports System.Xml
    Imports System.Xml.Serialization
    Imports Microsoft.VisualStudio.TextTemplating

    Namespace CustomDP

        Public Class CustomDirectiveProcessor
        Inherits DirectiveProcessor

            ' This buffer stores the code that is added to the
            ' generated transformation class after all the processing is done.
            ' ---------------------------------------------------------------
            Private codeBuffer As StringBuilder

            ' Using a Code Dom Provider creates code for the
            ' generated transformation class in either Visual Basic or C#.
            ' If you want your directive processor to support only one language, you
            ' can hard code the code you add to the generated transformation class.
            ' In that case, you do not need this field.
            ' --------------------------------------------------------------------------
            Private codeDomProvider As CodeDomProvider

            ' This stores the full contents of the text template that is being processed.
            ' --------------------------------------------------------------------------
            Private templateContents As String

            ' These are the errors that occur during processing. The engine passes
            ' the errors to the host, and the host can decide how to display them,
            ' for example the host can display the errors in the UI
            ' or write them to a file.
            ' ---------------------------------------------------------------------
            Private errorsValue As CompilerErrorCollection
            Public Shadows ReadOnly Property Errors() As CompilerErrorCollection
                Get
                    Return errorsValue
                End Get
            End Property

            ' Each time this directive processor is called, it creates a new property.
            ' We count how many times we are called, and append "n" to each new
            ' property name. The property names are therefore unique.
            ' --------------------------------------------------------------------------
            Private directiveCount As Integer = 0

            Public Overrides Sub Initialize(ByVal host As ITextTemplatingEngineHost)

                ' We do not need to do any initialization work.
            End Sub

            Public Overrides Sub StartProcessingRun(ByVal languageProvider As CodeDomProvider, ByVal templateContents As String, ByVal errors As CompilerErrorCollection)

                ' The engine has passed us the language of the text template
                ' we will use that language to generate code later.
                ' ----------------------------------------------------------
                Me.codeDomProvider = languageProvider
                Me.templateContents = templateContents
                Me.errorsValue = errors

                Me.codeBuffer = New StringBuilder()
            End Sub

            ' Before calling the ProcessDirective method for a directive, the
            ' engine calls this function to see whether the directive is supported.
            ' Notice that one directive processor might support many directives.
            ' ---------------------------------------------------------------------
            Public Overrides Function IsDirectiveSupported(ByVal directiveName As String) As Boolean

                If String.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then
                    Return True
                End If

                If String.Compare(directiveName, "SuperCoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then
                    Return True
                End If

                Return False
            End Function

            Public Overrides Sub ProcessDirective(ByVal directiveName As String, ByVal arguments As IDictionary(Of String, String))

                If String.Compare(directiveName, "CoolDirective", StringComparison.OrdinalIgnoreCase) = 0 Then

                    Dim fileName As String

                    If Not (arguments.TryGetValue("FileName", fileName)) Then
                        Throw New DirectiveProcessorException("Required argument 'FileName' not specified.")
                    End If

                    If String.IsNullOrEmpty(fileName) Then
                        Throw New DirectiveProcessorException("Argument 'FileName' is null or empty.")
                    End If

                    ' Now we add code to the generated transformation class.
                    ' This directive supports either Visual Basic or C#, so we must use the
                    ' System.CodeDom to create the code.
                    ' If a directive supports only one language, you can hard code the code.
                    ' --------------------------------------------------------------------------

                    Dim documentField As CodeMemberField = New CodeMemberField()

                    documentField.Name = "document" & directiveCount & "Value"
                    documentField.Type = New CodeTypeReference(GetType(XmlDocument))
                    documentField.Attributes = MemberAttributes.Private

                    Dim documentProperty As CodeMemberProperty = New CodeMemberProperty()

                    documentProperty.Name = "Document" & directiveCount
                    documentProperty.Type = New CodeTypeReference(GetType(XmlDocument))
                    documentProperty.Attributes = MemberAttributes.Public
                    documentProperty.HasSet = False
                    documentProperty.HasGet = True

                    Dim fieldName As CodeExpression = New CodeFieldReferenceExpression(New CodeThisReferenceExpression(), documentField.Name)
                    Dim booleanTest As CodeExpression = New CodeBinaryOperatorExpression(fieldName, CodeBinaryOperatorType.IdentityEquality, New CodePrimitiveExpression(Nothing))
                    Dim rightSide As CodeExpression = New CodeMethodInvokeExpression(New CodeTypeReferenceExpression("XmlReaderHelper"), "ReadXml", New CodePrimitiveExpression(fileName))
                    Dim thenSteps As CodeStatement() = New CodeStatement() {New CodeAssignStatement(fieldName, rightSide)}

                    Dim ifThen As CodeConditionStatement = New CodeConditionStatement(booleanTest, thenSteps)
                    documentProperty.GetStatements.Add(ifThen)

                    Dim s As CodeStatement = New CodeMethodReturnStatement(fieldName)
                    documentProperty.GetStatements.Add(s)

                    Dim options As CodeGeneratorOptions = New CodeGeneratorOptions()
                    options.BlankLinesBetweenMembers = True
                    options.IndentString = "    "
                    options.VerbatimOrder = True
                    options.BracingStyle = "VB"

                    Using writer As StringWriter = New StringWriter(codeBuffer, CultureInfo.InvariantCulture)

                        codeDomProvider.GenerateCodeFromMember(documentField, writer, options)
                        codeDomProvider.GenerateCodeFromMember(documentProperty, writer, options)
                    End Using

                End If

                ' One directive processor can contain many directives.
                ' If you want to support more directives, the code goes here...
                ' -----------------------------------------------------------------
                If String.Compare(directiveName, "supercooldirective", StringComparison.OrdinalIgnoreCase) = 0 Then

                    ' Code for SuperCoolDirective goes here.
                End If

                ' Track how many times the processor has been called.
                ' -----------------------------------------------------------------
                directiveCount += 1
            End Sub

            Public Overrides Sub FinishProcessingRun()

                Me.codeDomProvider = Nothing

                ' Important: do not do this:
                ' The get methods below are called after this method
                ' and the get methods can access this field.
                ' -----------------------------------------------------------------
                ' Me.codeBuffer = Nothing
            End Sub

            Public Overrides Function GetPreInitializationCodeForProcessingRun() As String

                ' Use this method to add code to the start of the
                ' Initialize() method of the generated transformation class.
                ' We do not need any pre-initialization, so we will just return "".
                ' -----------------------------------------------------------------
                ' GetPreInitializationCodeForProcessingRun runs before the
                ' Initialize() method of the base class.
                ' -----------------------------------------------------------------
                Return String.Empty
            End Function

            Public Overrides Function GetPostInitializationCodeForProcessingRun() As String

                ' Use this method to add code to the end of the
                ' Initialize() method of the generated transformation class.
                ' We do not need any post-initialization, so we will just return "".
                ' ------------------------------------------------------------------
                ' GetPostInitializationCodeForProcessingRun runs after the
                ' Initialize() method of the base class.
                ' -----------------------------------------------------------------
                Return String.Empty
            End Function

            Public Overrides Function GetClassCodeForProcessingRun() As String

                ' Return the code to add to the generated transformation class.
                ' -----------------------------------------------------------------
                Return codeBuffer.ToString()
            End Function

            Public Overrides Function GetReferencesForProcessingRun() As String()

                ' This returns the references that we want to use when
                ' compiling the generated transformation class.
                ' -----------------------------------------------------------------
                ' We need a reference to this assembly to be able to call
                ' XmlReaderHelper.ReadXml from the generated transformation class.
                ' -----------------------------------------------------------------
                Return New String() {"System.Xml", Me.GetType().Assembly.Location}
            End Function

            Public Overrides Function GetImportsForProcessingRun() As String()

                ' This returns the imports or using statements that we want to
                ' add to the generated transformation class.
                ' -----------------------------------------------------------------
                ' We need CustomDP to be able to call XmlReaderHelper.ReadXml
                ' from the generated transformation class.
                ' -----------------------------------------------------------------
                Return New String() {"System.Xml", "CustomDP"}
            End Function
        End Class

        ' --------------------------------------------------------------------------
        ' The code that we are adding to the generated transformation class
        ' will call this method.
        ' --------------------------------------------------------------------------
        Public Class XmlReaderHelper

            Public Shared Function ReadXml(ByVal fileName As String) As XmlDocument

                Dim d As XmlDocument = New XmlDocument()

                Using reader As XmlReader = XmlReader.Create(fileName)

                    Try
                        d.Load(reader)

                    Catch e As System.Xml.XmlException

                        Throw New DirectiveProcessorException("Unable to read the XML file.", e)
                    End Try
                End Using

                Return d
            End Function
        End Class

    End Namespace
    ```

4. Somente para Visual Basic, abra o menu **projeto** e clique em **Propriedades de CustomDP**. Na guia **aplicativo** , em **namespace raiz**, exclua o valor padrão, `CustomDP` .

5. No menu **Arquivo** , clique em **Salvar Tudo**.

6. No menu **Compilar**, clique em **Compilar Solução**.

### <a name="build-the-project"></a>Compilar o projeto

Compile o projeto. No menu **Compilar**, clique em **Compilar Solução**.

## <a name="register-the-directive-processor"></a>Registrar o processador de diretivas

Antes de poder chamar uma diretiva de um modelo de texto no Visual Studio, você deve adicionar uma chave do registro para o processador de diretiva.

> [!NOTE]
> Se você quiser instalar o processador de diretiva em mais de um computador, é melhor definir uma extensão do Visual Studio (VSIX) que inclui um arquivo *. pkgdef* junto com o assembly. Para obter mais informações, consulte [implantando um processador de diretiva personalizada](../modeling/deploying-a-custom-directive-processor.md).

As chaves dos processadores de diretriz estão no Registro, no seguinte local:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\VisualStudio\*.0\TextTemplating\DirectiveProcessors
```

Para sistemas de 64 bits, o local do Registro é:

```
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\VisualStudio\*.0\TextTemplating\DirectiveProcessors
```

Nesta seção, você adiciona uma chave para o processador de diretriz personalizado ao Registro no mesmo local.

> [!CAUTION]
> A edição incorreta do Registro pode danificar seriamente o sistema. Antes de alterar o Registro, faça o backup de todos os dados importantes que estão no computador.

### <a name="to-add-a-registry-key-for-the-directive-processor"></a>Para adicionar uma chave do Registro para o processador de diretriz

1. Execute o `regedit` comando usando o menu iniciar ou a linha de comando.

2. Navegue até o local **HKEY_LOCAL_MACHINE \software\microsoft\visualstudio \\ \* 0 \ TextTemplating\DirectiveProcessors**e clique no nó.

   Em sistemas de 64 bits, use **HKEY_LOCAL_MACHINE \software\wow6432node\microsoft\visualstudio \\ \* . 0 \ TextTemplating\DirectiveProcessors**

3. Adicione uma nova chave chamada CustomDirectiveProcessor.

    > [!NOTE]
    > Este é o nome que você usará no campo Processador de suas diretivas personalizadas. Esse nome não precisa corresponder ao nome da diretiva, ao nome da classe do processador de diretriz ou ao namespace do processador de diretriz.

4. Adicione um novo valor da cadeia de caracteres chamada Class que tenha o valor CustomDP.CustomDirectiveProcessor como o nome da nova cadeia de caracteres.

5. Adicione um novo valor da cadeia de caracteres chamado CodeBase que tenha um valor igual ao caminho do arquivo CustomDP.dll criado anteriormente neste passo a passo.

     Por exemplo, o caminho pode ser semelhante a `C:\UserFiles\CustomDP\bin\Debug\CustomDP.dll` .

     A chave do Registro deverá ter os seguintes valores:

   | Nome | Type | Dados |
   |-|-|-|
   | (Padrão) | REG_SZ | (valor não definido) |
   | Classe | REG_SZ | CustomDP.CustomDirectiveProcessor |
   | CodeBase | REG_SZ | <strong>\<Path to Your Solution></strong>CustomDP\bin\Debug\CustomDP.dll |

     Se você colocou o assembly no GAC, os valores deverão se parecer com o seguinte:

   | Nome | Type | Dados |
   |-|-|-|
   | (Padrão) | REG_SZ | (valor não definido) |
   | Classe | REG_SZ | CustomDP.CustomDirectiveProcessor |
   | Assembly | REG_SZ | CustomDP.dll |

6. Reinicie o Visual Studio.

## <a name="test-the-directive-processor"></a>Testar o processador de diretivas

Para testar o processador de diretriz, você precisa escrever um modelo de texto que o chame.

Neste exemplo, o modelo de texto chama a diretiva e passa o nome de um arquivo XML que contém a documentação de um arquivo de classe. O modelo de texto usa a <xref:System.Xml.XmlDocument> propriedade que a diretiva cria para navegar no XML e imprimir os comentários da documentação.

### <a name="to-create-an-xml-file-for-use-in-testing-the-directive-processor"></a>Para criar um arquivo XML para uso no teste do processador de diretriz

1. Crie um arquivo chamado *DocFile.xml* usando qualquer editor de texto (por exemplo, bloco de notas).

    > [!NOTE]
    > Você pode criar esse arquivo em qualquer local (por exemplo, *C:\Test\DocFile.xml*).

2. Adicione o seguinte ao arquivo XML:

    ```xml
    <?xml version="1.0"?>
    <doc>
        <assembly>
            <name>xmlsample</name>
        </assembly>
        <members>
            <member name="T:SomeClass">
                <summary>Class level summary documentation goes here.</summary>
                <remarks>Longer comments can be associated with a type or member through the remarks tag</remarks>
            </member>
            <member name="F:SomeClass.m_Name">
                <summary>Store for the name property</summary>
            </member>
            <member name="M:SomeClass.#ctor">
                <summary>The class constructor.</summary>
            </member>
            <member name="M:SomeClass.SomeMethod(System.String)">
                <summary>Description for SomeMethod.</summary>
                <param name="s">Parameter description for s goes here</param>
                <seealso cref="T:System.String">You can use the cref attribute on any tag to reference a type or member and the compiler will check that the reference exists.</seealso>
            </member>
            <member name="M:SomeClass.SomeOtherMethod">
                <summary>Some other method.</summary>
                <returns>Return results are described through the returns tag.</returns>
                <seealso cref="M:SomeClass.SomeMethod(System.String)">Notice the use of the cref attribute to reference a specific method</seealso>
            </member>
            <member name="M:SomeClass.Main(System.String[])">
                <summary>The entry point for the application.</summary>
                <param name="args">A list of command line arguments</param>
            </member>
            <member name="P:SomeClass.Name">
                <summary>Name property</summary>
                <value>A value tag is used to describe the property value</value>
            </member>
        </members>
    </doc>
    ```

3. Salve e feche o arquivo.

### <a name="to-create-a-text-template-to-test-the-directive-processor"></a>Para criar um modelo de texto para testar o processador de diretriz

1. No Visual Studio, crie um novo projeto de biblioteca de classes C# ou Visual Basic chamado TemplateTest.

2. Adicione um novo arquivo de modelo de texto chamado TestDP.tt.

3. Verifique se a propriedade da **ferramenta personalizada** de TestDP.tt está definida como `TextTemplatingFileGenerator` .

4. Altere o conteúdo de TestDP.tt para o texto a seguir.

    > [!NOTE]
    > Substitua a cadeia de caracteres `<YOUR PATH>` pelo caminho para o arquivo de *DocFile.xml* .

    A linguagem do modelo de texto não precisa corresponder à linguagem do processador de diretriz.

    ```csharp
    <#@ assembly name="System.Xml" #>
    <#@ template debug="true" #>
    <#@ output extension=".txt" #>

    <#  // This will call the custom directive processor. #>
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>

    <#  // Uncomment this line if you want to see the generated transformation class. #>
    <#  // System.Diagnostics.Debugger.Break(); #>

    <#  // This will use the results of the directive processor. #>
    <#  // The directive processor has read the XML and stored it in Document0. #>
    <#
        XmlNode node = Document0.DocumentElement.SelectSingleNode("members");

        foreach (XmlNode member in node.ChildNodes)
        {
            XmlNode name = member.Attributes.GetNamedItem("name");
            WriteLine("{0,7}:  {1}", "Name", name.Value);

            foreach (XmlNode comment in member.ChildNodes)
            {
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText);
            }
            WriteLine("");
        }
    #>

    <# // You can call the directive processor again and pass it a different file. #>
    <# // @ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\<Your Second File>" #>

    <#  // To use the results of the second directive call, use Document1. #>
    <#
        // XmlNode node2 = Document1.DocumentElement.SelectSingleNode("members");

        // ...
    #>
    ```

    ```vb
    <#@ assembly name="System.Xml" #>
    <#@ template debug="true" language="vb" #>
    <#@ output extension=".txt" #>

    <#  ' This will call the custom directive processor. #>
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>

    <#  ' Uncomment this line if you want to see the generated transformation class. #>
    <#  ' System.Diagnostics.Debugger.Break() #>

    <#  ' This will use the results of the directive processor. #>
    <#  ' The directive processor has read the XML and stored it in Document0. #>
    <#
        Dim node as XmlNode = Document0.DocumentElement.SelectSingleNode("members")

        Dim member As XmlNode
        For Each member In node.ChildNodes

            Dim name As XmlNode = member.Attributes.GetNamedItem("name")
            WriteLine("{0,7}:  {1}", "Name", name.Value)

            Dim comment As XmlNode
            For Each comment In member.ChildNodes
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText)
            Next

            WriteLine("")
        Next
    #>

    <# ' You can call the directive processor again and pass it a different file. #>
    <# ' @ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFileTwo.xml" #>

    <#  ' To use the results of the second directive call, use Document1. #>
    <#
        ' node = Document1.DocumentElement.SelectSingleNode("members")

        ' ...
    #>
    ```

    > [!NOTE]
    > Nesse exemplo, o valor do parâmetro `Processor` é `CustomDirectiveProcessor`. O valor do parâmetro `Processor` deve corresponder ao nome da chave do Registro do processador.

5. No menu **arquivo** , escolha **salvar tudo**.

### <a name="to-test-the-directive-processor"></a>Para testar o processador de diretriz

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em TestDP.tt e clique em **executar ferramenta personalizada**.

   Para Visual Basic usuários, TestDP.txt podem não aparecer em **Gerenciador de soluções** por padrão. Para exibir todos os arquivos atribuídos ao projeto, abra o menu **projeto** e clique em **Mostrar todos os arquivos**.

2. Em **Gerenciador de soluções**, expanda o nó TestDP.txt e clique duas vezes em TestDP.txt para abri-lo no editor.

    A saída de texto gerada será exibida. A saída deve ser semelhante ao seguinte:

    ```text
       Name:  T:SomeClass
    summary:  Class level summary documentation goes here.
    remarks:  Longer comments can be associated with a type or member through the remarks tag

       Name:  F:SomeClass.m_Name
    summary:  Store for the name property

       Name:  M:SomeClass.#ctor
    summary:  The class constructor.

       Name:  M:SomeClass.SomeMethod(System.String)
    summary:  Description for SomeMethod.
      param:  Parameter description for s goes here
    seealso:  You can use the cref attribute on any tag to reference a type or member and the compiler will check that the reference exists.

       Name:  M:SomeClass.SomeOtherMethod
    summary:  Some other method.
    returns:  Return results are described through the returns tag.
    seealso:  Notice the use of the cref attribute to reference a specific method

       Name:  M:SomeClass.Main(System.String[])
    summary:  The entry point for the application.
      param:  A list of command line arguments

       Name:  P:SomeClass.Name
    summary:  Name property
      value:  A value tag is used to describe the property value
    ```

## <a name="add-html-to-generated-text"></a>Adicionar HTML ao texto gerado

Depois de testar seu processador de diretriz personalizado, você pode adicionar um HTML ao texto gerado.

### <a name="to-add-html-to-the-generated-text"></a>Para adicionar HTML ao texto gerado

1. Substitua o código em *TestDP.tt* pelo seguinte. O HTML é realçado. Certifique-se de substituir a cadeia de caracteres `YOUR PATH` pelo caminho para o arquivo de *DocFile.xml* .

    > [!NOTE]
    > Marcas abertas adicionais separam \<# and close #> o código da instrução das marcas HTML.

    ```csharp
    <#@ assembly name="System.Xml" #>
    <#@ template debug="true" #>
    <#@ output extension=".htm" #>

    <#  // This will call the custom directive processor #>
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>

    <#  // Uncomment this line if you want to see the generated transformation class #>
    <#  // System.Diagnostics.Debugger.Break(); #>

    <html><body>

    <#  // This will use the results of the directive processor #>.
    <#  // The directive processor has read the XML and stored it in Document0#>.
    <#
        XmlNode node = Document0.DocumentElement.SelectSingleNode("members");

        foreach (XmlNode member in node.ChildNodes)
        {
    #>
    <h3>
    <#
            XmlNode name = member.Attributes.GetNamedItem("name");
            WriteLine("{0,7}:  {1}", "Name", name.Value);
    #>
    </h3>
    <#
            foreach (XmlNode comment in member.ChildNodes)
            {
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText);
    #>
    <br/>
    <#
            }
        }
    #>
    </body></html>
    ```

    ```vb
    <#@ assembly name="System.Xml" #>
    <#@ template debug="true" language="vb" #>
    <#@ output extension=".htm" #>

    <#  ' This will call the custom directive processor #>
    <#@ CoolDirective Processor="CustomDirectiveProcessor" FileName="<YOUR PATH>\DocFile.xml" #>

    <#  ' Uncomment this line if you want to see the generated transformation class #>
    <#  ' System.Diagnostics.Debugger.Break() #>

    <html><body>

    <#  ' This will use the results of the directive processor #>.
    <#  ' The directive processor has read the XML and stored it in Document0#>.
    <#
        Dim node as XmlNode = Document0.DocumentElement.SelectSingleNode("members")

        Dim member As XmlNode
        For Each member In node.ChildNodes
    #>
    <h3>
    <#
            Dim name As XmlNode = member.Attributes.GetNamedItem("name")
            WriteLine("{0,7}:  {1}", "Name", name.Value)
    #>
    </h3>
    <#
            Dim comment As XmlNode
            For Each comment In member.ChildNodes
                WriteLine("{0,7}:  {1}", comment.Name, comment.InnerText)
    #>
    <br/>
    <#
            Next
        Next
    #>
    </body></html>
    ```

2. No menu **arquivo** , clique em **salvar TestDP.txt**.

3. Para exibir a saída em um navegador, em **Gerenciador de soluções**, clique com o botão direito do mouse em TestDP.htm e clique em **Exibir no navegador**.

   A saída deve ser igual ao texto original, exceto pelo formato HTML aplicado. Cada nome de item aparece em negrito.
