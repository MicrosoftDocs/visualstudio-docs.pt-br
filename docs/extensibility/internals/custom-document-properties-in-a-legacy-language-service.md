---
title: Propriedades de documento personalizadas em serviços de idioma herdados
description: Saiba como criar propriedades de documento personalizadas que são exibidas no janela Propriedades do Visual Studio, como parte de um serviço de idioma herdado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom document properties, language services [managed package framework]
- document properties, custom
- language services [managed package framework], custom document properties
ms.assetid: cc714a67-b33e-4440-9203-3c90f648bd9c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1e154ba5e6ce4c85f597957b1d6704ca341b3c4d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091130"
---
# <a name="custom-document-properties-in-a-legacy-language-service"></a>Propriedades de documento personalizadas em um serviço de idioma herdado
As propriedades do documento podem ser exibidas na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] janela **Propriedades** . Linguagens de programação geralmente não têm propriedades associadas a arquivos de origem individuais. No entanto, o XML dá suporte a propriedades de documento que afetam a codificação, o esquema e a folha de estilos.

## <a name="discussion"></a>Discussão
 Se seu idioma precisar de propriedades de documento personalizadas, você deverá derivar uma classe da <xref:Microsoft.VisualStudio.Package.DocumentProperties> classe e implementar as propriedades necessárias em sua classe derivada.

 Além disso, as propriedades do documento normalmente são armazenadas no próprio arquivo de origem. Isso requer que o serviço de linguagem analise as informações de Propriedade do arquivo de origem para exibição na janela **Propriedades** e atualize o arquivo de origem quando uma alteração é feita nas propriedades do documento na janela **Propriedades** .

## <a name="customize-the-documentproperties-class"></a>Personalizar a classe DocumentProperties
 Para dar suporte a propriedades de documento personalizadas, você deve derivar uma classe da <xref:Microsoft.VisualStudio.Package.DocumentProperties> classe e adicionar quantas propriedades forem necessárias. Você também deve fornecer atributos de usuário para organizá-los na janela **Propriedades** exibir. Se uma propriedade tiver apenas um `get` acessador, ela será mostrada como somente leitura na janela **Propriedades** . Se uma propriedade tiver ambos `get` e `set` acessadores, a propriedade também poderá ser atualizada na janela **Propriedades** .

### <a name="example"></a>Exemplo
 Aqui está uma classe de exemplo derivada de <xref:Microsoft.VisualStudio.Package.DocumentProperties> , mostrando duas propriedades `Filename` e `Description` . Quando uma propriedade é atualizada, um método personalizado na <xref:Microsoft.VisualStudio.Package.LanguageService> classe é chamado para gravar a propriedade no arquivo de origem.

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    class TestDocumentProperties : DocumentProperties
    {
        private string m_filename;
        private string m_description;

        public TestDocumentProperties(CodeWindowManager mgr)
            : base(mgr)
        {
        }

        // Helper function to initialize this property without
        // going through the FileName property (which does a lot
        // more than we need when the filename is set).
        public void SetFileName(string filename)
        {
            m_filename = filename;
        }

        // Helper function to initialize this property without
        // going through the Description property (which does a lot
        // more than we need when the description is set).
        public void SetDescription(string description)
        {
            m_description = description;
        }

        ////////////////////////////////////////////////////////////
        // The document properties

        [CategoryAttribute("General")]
        [DescriptionAttribute("Name of the file")]
        [DisplayNameAttribute("Filename")]
        public string FileName
        {
            get { return m_filename; }
            set
            {
               if (value != m_filename)
               {
                    m_filename = value;
                    SetPropertyValue("Filename", m_filename);
               }
            }
        }

        [CategoryAttribute("General")]
        [DescriptionAttribute("Description of the file")]
        [DisplayNameAttribute("Description")]
        public string Description
        {
            get { return m_description; }
            set
            {
                if (value != m_description)
                {
                    m_description = value;
                    SetPropertyValue("Description", m_description);
                }
            }
        }

        ///////////////////////////////////////////////////////////
        // Private methods.

        private void SetPropertyValue(string propertyName, string propertyValue)
        {
            Source src = this.GetSource();
            if (src != null)
            {
                TestLanguageService service = src.LanguageService as TestLanguageService;
                if (service != null)
                {
                    // Set the property in to the source file.
                    service.SetPropertyValue(src, propertyName, propertyValue);
                }
            }
        }
    }
}
```

## <a name="instantiate-the-custom-documentproperties-class"></a>Instanciar a classe Custom DocumentProperties
 Para instanciar sua classe de propriedades de documento personalizada, você deve substituir o <xref:Microsoft.VisualStudio.Package.LanguageService.CreateDocumentProperties%2A> método em sua versão da <xref:Microsoft.VisualStudio.Package.LanguageService> classe para retornar uma única instância da sua <xref:Microsoft.VisualStudio.Package.DocumentProperties> classe.

### <a name="example"></a>Exemplo

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    class TestLanguageService : LanguageService
    {
        private TestDocumentProperties m_documentProperties;

        public override DocumentProperties CreateDocumentProperties(CodeWindowManager mgr)
        {
            if (m_documentProperties == null)
            {
                m_documentProperties = new TestDocumentProperties(mgr);
            }
            return m_documentProperties;
        }
    }
}
```

## <a name="properties-in-the-source-file"></a>Propriedades no arquivo de origem
 Como as propriedades do documento são geralmente específicas do arquivo de origem, os valores são armazenados no próprio arquivo de origem. Isso requer suporte do analisador de idioma ou do scanner para definir essas propriedades. Por exemplo, as propriedades de um documento XML são armazenadas no nó raiz. Os valores no nó raiz são modificados quando os valores da janela **Propriedades** são alterados e o nó raiz é atualizado no editor.

### <a name="example"></a>Exemplo
 Este exemplo armazena as propriedades `Filename` e `Description` nas duas primeiras linhas do arquivo de origem, inseridas em um cabeçalho de comentário especial, como:

```
//!Filename = file.testext
//!Description = A sample file
```

 Este exemplo mostra os dois métodos necessários para obter e definir as propriedades do documento das duas primeiras linhas do arquivo de origem, bem como as propriedades serão atualizadas se o usuário modificar o arquivo de origem diretamente. O `SetPropertyValue` método no exemplo mostrado aqui é o mesmo chamado da `TestDocumentProperties` classe, conforme mostrado na seção *Personalizando a classe DocumentProperties* .

 Este exemplo usa o verificador para determinar o tipo de tokens nas duas primeiras linhas. Este exemplo é apenas para fins ilustrativos. Uma abordagem mais comum a essa situação é analisar o arquivo de origem no que é chamado de árvore de análise, em que cada nó da árvore contém informações sobre um token específico. O nó raiz conterá as propriedades do documento.

```csharp
using System.ComponentModel;
using Microsoft.VisualStudio.Package;

namespace TestLanguagePackage
{
    // TokenType.Comment is the last item in that enumeration.
    public enum TestTokenTypes
    {
        DocPropertyLine = TokenType.Comment + 1,
        DocPropertyName,
        DocPropertyAssign,
        DocPropertyValue
    }

    class TestLanguageService : LanguageService
    {
        // Search this many lines from the beginning for properties.
        private static int maxLinesToSearch = 2;

        private TestDocumentProperties m_documentProperties;

        // Called whenever a full parsing operation has completed.
        public override void OnParseComplete(ParseRequest req)
        {
            if (m_documentProperties != null)
            {
                Source src = GetSource(req.View);
                if (src != null)
                {
                    string value = GetPropertyValue(src, "Filename");
                    m_documentProperties.SetFileName(value);

                    value = GetPropertyValue(src, "Description");
                    m_documentProperties.SetDescription(value);

                    // Update the Properties Window.
                    m_documentProperties.Refresh();
                }
            }
        }

        // Retrieves the specified property value from the given source.
        public string GetPropertyValue(Source src, string propertyName)
        {
            string propertyValue = "";

            if (src != null)
            {
                IVsTextColorState colorState = src.ColorState;
                if (colorState != null)
                {
                    string      line;
                    TokenInfo[] lineInfo = null;
                    int         i;

                    for (i = 0; i < maxLinesToSearch; i++)
                    {
                        line     = src.GetLine(i);
                        lineInfo = src.GetColorizer().GetLineInfo(
                                                        src.GetTextLines(),
                                                        i,
                                                        colorState);
                        if (lineInfo == null)
                        {
                            continue;
                        }
                        if (lineInfo[0].Type != (TokenType)TestTokenTypes.DocPropertyLine)
                        {
                            // Not a property line.
                            continue;
                        }
                        TokenInfo valueInfo = new TokenInfo();
                        int tokenIndex = -1;
                        for (tokenIndex = 0;
                             tokenIndex < lineInfo.Length;
                             tokenIndex++)
                        {
                            if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyName)
                            {
                                break;
                            }
                        }
                        if (tokenIndex >= lineInfo.Length)
                        {
                            // No property name on the line.
                            continue;
                        }
                        string name = src.GetText(i,
                                                  lineInfo[tokenIndex].StartIndex,
                                                  i,
                                                  lineInfo[tokenIndex].EndIndex + 1);
                        if (name != null)
                        {
                            if (String.Compare(name, propertyName, true) == 0)
                            {
                                for ( ;
                                     tokenIndex < lineInfo.Length;
                                     tokenIndex++)
                                {
                                    if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyValue)
                                    {
                                        break;
                                    }
                                }
                                if (tokenIndex < lineInfo.Length)
                                {
                                    propertyValue = src.GetText(i,
                                                          lineInfo[tokenIndex].StartIndex,
                                                          i,
                                                          lineInfo[tokenIndex].EndIndex + 1);
                                }
                                break;
                            }
                        }
                    }
                }
            }
            return propertyValue;
        }

        // Sets the specified property into the given source file.
        // Called from the TestDocumentProperties class.
        public void SetPropertyValue(Source src, string propertyName, string propertyValue)
        {
            string newLine;

            if (propertyName == null || propertyName == "")
            {
                // No property name, so nothing to do
                return;
            }
            if (propertyValue == null)
            {
                propertyValue = "";
            }
            // This is the line to be inserted.
            newLine = String.Format("//!{0} = {1}", propertyName, propertyValue);

            // First, find the line on which the property belongs.
            // If line is found, replace it.
            // Otherwise, insert the line at the beginning of the file.
            if (src != null)
            {
                IVsTextColorState colorState = src.ColorState;
                if (colorState != null)
                {
                    int         lineNumber = -1;
                    string      line;
                    TokenInfo[] lineInfo   = null;
                    int         i;

                    for (i = 0; i < maxLinesToSearch; i++)
                    {
                        line     = src.GetLine(i);
                        lineInfo = src.GetColorizer().GetLineInfo(
                                                        src.GetTextLines(),
                                                        i,
                                                        colorState);
                        if (lineInfo == null)
                        {
                            continue;
                        }
                        if (lineInfo[0].Type != (TokenType)TestTokenTypes.DocPropertyLine)
                        {
                            // Not a property line
                            continue;
                        }
                        TokenInfo valueInfo = new TokenInfo();
                        int tokenIndex = -1;
                        for (tokenIndex = 0;
                             tokenIndex < lineInfo.Length;
                             tokenIndex++)
                        {
                            if (lineInfo[tokenIndex].Type == (TokenType)TestTokenTypes.DocPropertyName)
                            {
                                break;
                            }
                        }
                        if (tokenIndex >= lineInfo.Length)
                        {
                            // No property name on the line.
                            continue;
                        }
                        string name = src.GetText(i,
                                                  lineInfo[tokenIndex].StartIndex,
                                                  i,
                                                  lineInfo[tokenIndex].EndIndex + 1);
                        if (name != null)
                        {
                            if (String.Compare(name, propertyName, true) == 0)
                            {
                                lineNumber = i;
                                break;
                            }
                        }
                    }

                    // Set up an undo context that also handles the insert/replace.
                    EditArray editArray = new EditArray(src,
                                                        true,
                                                        "Update Property");
                    if (editArray != null)
                    {
                        TextSpan span = new TextSpan();
                        if (lineNumber != -1)
                        {
                            // Replace line.
                            int lineLength = 0;
                            src.GetTextLines().GetLengthOfLine(lineNumber,
                                                               out lineLength);
                            span.iStartLine  = lineNumber;
                            span.iStartIndex = 0;
                            span.iEndLine    = lineNumber;
                            span.iEndIndex   = lineLength;
                        }
                        else
                        {
                            // Insert new line.
                            span.iStartLine  = 0;
                            span.iStartIndex = 0;
                            span.iEndLine    = 0;
                            span.iEndIndex   = 0;
                            newLine += "\n";
                        }
                        editArray.Add(new EditSpan(span, newLine));
                        editArray.ApplyEdits();
                    }
                }
            }
        }
    }
}
```

## <a name="see-also"></a>Confira também
- [Recursos do serviço de linguagem herdada](../../extensibility/internals/legacy-language-service-features1.md)
