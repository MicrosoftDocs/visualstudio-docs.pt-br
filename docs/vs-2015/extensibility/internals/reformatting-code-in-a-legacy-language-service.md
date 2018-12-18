---
title: Reformatar o código em um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- reformatting code, supporting in language services [managed package framework]
- language services [managed package framework], reformatting code
ms.assetid: 08bb3375-8fef-4f4e-9efa-0d7333bab0eb
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 95b878448904c194bd758d266e67599369502fe6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51779262"
---
# <a name="reformatting-code-in-a-legacy-language-service"></a>Reformatando o código em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

No [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] código-fonte pode ser reformatado ao normalizar o uso de espaços em branco e recuos. Isso pode incluir inserindo ou remoção de espaços ou tabulações no início de cada linha, adicionar novas linhas entre as linhas ou substituindo espaços por tabulações ou guias com espaços.  
  
> [!NOTE]
>  **Observação** inserindo ou excluindo os caracteres de nova linha pode afetar marcadores, como pontos de interrupção e indicadores, mas adicionando ou removendo espaços ou tabulações não afeta marcadores.  
  
 Os usuários podem iniciar uma operação de reformatação, selecionando **seleção de formato** ou **Formatar documento** do **avançado** menu o **editar**menu. Uma operação de reformatação também pode ser disparada quando um trecho de código ou um determinado caractere é inserido. Por exemplo, quando você digita uma chave de fechamento em c#, tudo entre a chave de abertura correspondente e o colchete de fechamento é recuado automaticamente para o nível adequado.  
  
 Quando [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] envia o **Formatar seleção** ou **Formatar documento** comando para o serviço de linguagem, o <xref:Microsoft.VisualStudio.Package.ViewFilter> chamado pela classe o <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> método no <xref:Microsoft.VisualStudio.Package.Source> classe. Para dar suporte a formatação que você deve substituir o <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> método e fornecer sua própria formatação de código.  
  
## <a name="enabling-support-for-reformatting"></a>Habilitando o suporte para reformatação  
 Para dar suporte à formatação, o `EnableFormatSelection` parâmetro do <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> deve ser definida como `true` ao registrar o VSPackage. Isso define a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableFormatSelection%2A> propriedade para `true`. O <xref:Microsoft.VisualStudio.Package.ViewFilter.CanReformat%2A> método retorna o valor dessa propriedade. Se ela retorna true, o <xref:Microsoft.VisualStudio.Package.ViewFilter> classe chama o <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A>.  
  
## <a name="implementing-reformatting"></a>Implementando a reformatação  
 Para implementar a reformatação, você deve derivar uma classe a partir de <xref:Microsoft.VisualStudio.Package.Source> de classe e substituir o <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> método. O <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> objeto descreve o alcance para formatar e o <xref:Microsoft.VisualStudio.Package.EditArray> objeto mantém as edições feitas no alcance. Observe que esse intervalo pode ser o documento inteiro. No entanto, como não há probabilidade de serem várias alterações feitas para o período, todas as alterações devem ser reversíveis em uma única ação. Para fazer isso, encapsule a todas as alterações em um <xref:Microsoft.VisualStudio.Package.CompoundAction> objeto (consulte a seção "Usando a classe CompoundAction" neste tópico).  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir garante que há um único espaço depois de cada vírgula na seleção, a menos que a vírgula é seguida por uma tabulação ou no final da linha. Espaços à direita depois da última vírgula em uma linha são excluídos. Consulte a seção "Usando a classe CompoundAction" neste tópico para ver como esse método é chamado do <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> método.  
  
```csharp  
using Microsoft.VisualStudio.Package;  
using Microsoft VisualStudio.TextManager.Interop;  
  
namespace MyLanguagePackage  
{  
    class MySource : Source  
    {  
        private void DoFormatting(EditArray mgr, TextSpan span)  
        {  
            // Make sure there is one space after every comma unless followed  
            // by a tab or comma is at end of line.  
            IVsTextLines pBuffer = GetTextLines();  
            if (pBuffer != null)  
            {  
                int    startIndex = span.iStartIndex;  
                int    endIndex   = 0;  
                string line       = "";  
                // Loop over all lines in span  
                for (int i = span.iStartLine; i <= span.iEndLine; i++)  
                {  
                    if (i < span.iEndLine)  
                    {  
                        pBuffer.GetLengthOfLine(i, out endIndex);  
                    }  
                    else  
                    {  
                        endIndex = span.iEndIndex;  
                    }  
                    pBuffer.GetLineText(i, startIndex, i, endIndex, out line);  
  
                    if (line.Length > 0)  
                    {  
                        int index = 0;  
                        // Loop over all commas in line  
                        while ((index = line.IndexOf(',', index)) != -1)  
                        {  
                            int spaceIndex = index + 1;  
                            // Determine how many spaces after comma  
                            while (spaceIndex < line.Length && line[spaceIndex] == ' ')  
                            {  
                                ++spaceIndex;  
                            }  
  
                            int      spaceCount      = spaceIndex - (index + 1);  
                            string   replacementText = " ";  
                            bool     fDoEdit         = true;  
                            TextSpan editTextSpan    = new TextSpan();  
  
                            editTextSpan.iStartLine  = i;  
                            editTextSpan.iEndLine    = i;  
                            editTextSpan.iStartIndex = index + 1;  
  
                            if (spaceIndex == line.Length)  
                            {  
                                if (spaceCount > 0)  
                                {  
                                    // Delete spaces after a comma at end of line  
                                    editTextSpan.iEndIndex = spaceIndex;  
                                    replacementText = "";  
                                }  
                                else  
                                {  
                                    // Otherwise, do not add spaces if comma is  
                                    // at end of line.  
                                    fDoEdit = false;  
                                }  
                            }  
                            else if (spaceCount == 0)  
                            {  
                                if (spaceIndex < line.Length && line[spaceIndex] == '\t')  
                                {  
                                    // Do not insert space if a tab follows  
                                    // a comma.  
                                    fDoEdit = false;  
                                }  
                                else  
                                {  
                                    // No space after comma so add a space.  
                                    editTextSpan.iEndIndex = index + 1;  
                                }  
                            }  
                            else if (spaceCount > 1)  
                            {  
                                // More than one space after comma, replace  
                                // with a single space.  
                                editTextSpan.iEndIndex = spaceIndex;  
                            }  
                            else  
                            {  
                                // Single space after a comma and not at end  
                                // of the line, leave it alone.  
                                fDoEdit = false;  
                            }  
                            if (fDoEdit)  
                            {  
                                // Add edit operation  
                                mgr.Add(new EditSpan(editTextSpan, replacementText));  
                            }  
                            index = spaceIndex;  
                        }  
                    }  
                    startIndex = 0; // All subsequent lines start at 0  
                }  
                // Apply all edits  
                mgr.ApplyEdits();  
            }  
        }  
    }  
}  
```  
  
## <a name="using-the-compoundaction-class"></a>Usando a classe CompoundAction  
 Todos os a reformatação feito em uma seção de código deve ser reversível em uma única ação. Isso pode ser feito usando um <xref:Microsoft.VisualStudio.Package.CompoundAction> classe. Essa classe encapsula um conjunto de operações de edição no buffer de texto em uma operação de edição único.  
  
### <a name="example"></a>Exemplo  
 Aqui está um exemplo de como usar o <xref:Microsoft.VisualStudio.Package.CompoundAction> classe. Veja o exemplo na seção "Implementar o suporte para formatação" neste tópico para obter um exemplo de como o `DoFormatting` método.  
  
```csharp  
using Microsoft.VisualStudio.Package;  
using Microsoft VisualStudio.TextManager.Interop;  
  
namespace MyLanguagePackage  
{  
    class MySource : Source  
    {  
        public override void ReformatSpan(EditArray mgr, TextSpan span)  
        {  
            string description = "Reformat code";  
            CompoundAction ca = new CompoundAction(this, description);  
            using (ca)  
            {  
                ca.FlushEditActions();      // Flush any pending edits  
                DoFormatting(mgr, span);    // Format the span  
            }  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)

