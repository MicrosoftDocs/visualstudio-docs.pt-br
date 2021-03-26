---
title: Reformatando código em um serviço de linguagem herdada | Microsoft Docs
description: Saiba como habilitar o suporte para reformatação de código-fonte para um serviço de linguagem herdada do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- reformatting code, supporting in language services [managed package framework]
- language services [managed package framework], reformatting code
ms.assetid: 08bb3375-8fef-4f4e-9efa-0d7333bab0eb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e8dc10e4def3e4725bb4f64041cdb17146b9d84d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060855"
---
# <a name="reformatting-code-in-a-legacy-language-service"></a>Reformatando o código em um serviço de linguagem herdado

No [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] código-fonte pode ser reformatado normalizando o uso de recuos e espaço em branco. Isso pode incluir inserção ou remoção de espaços ou tabulações no início de cada linha, adição de novas linhas entre linhas ou substituição de espaços por tabulações ou tabulações por espaços.

> [!NOTE]
> Inserir ou excluir caracteres de nova linha pode afetar marcadores como pontos de interrupção e indicadores, mas adicionar ou remover espaços ou tabulações não afeta os marcadores.

Os usuários podem iniciar uma operação de reformatação selecionando **Formatar seleção** ou **Formatar documento** no menu **avançado** no menu **Editar** . Uma operação de reformatação também pode ser disparada quando um trecho de código ou um caractere específico é inserido. Por exemplo, quando você digita uma chave de fechamento em C#, tudo entre a chave de abertura correspondente e a chave de fechamento é automaticamente recuado para o nível apropriado.

Quando o [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] envia o comando **Format Selection** ou **Format Document** para o serviço Language, a <xref:Microsoft.VisualStudio.Package.ViewFilter> classe chama o <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> método na <xref:Microsoft.VisualStudio.Package.Source> classe. Para dar suporte à formatação, você deve substituir o <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> método e fornecer seu próprio código de formatação.

## <a name="enabling-support-for-reformatting"></a>Habilitando o suporte para reformatação

Para dar suporte à formatação, o `EnableFormatSelection` parâmetro de <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> deve ser definido como `true` quando você registra seu VSPackage. Isso define a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableFormatSelection%2A> propriedade como `true` . O <xref:Microsoft.VisualStudio.Package.ViewFilter.CanReformat%2A> método retorna o valor dessa propriedade. Se retornar true, a <xref:Microsoft.VisualStudio.Package.ViewFilter> classe chamará o <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> .

## <a name="implementing-reformatting"></a>Implementando a reformatação

Para implementar a reformatação, você deve derivar uma classe da <xref:Microsoft.VisualStudio.Package.Source> classe e substituir o <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> método. O <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> objeto descreve o intervalo a ser formatado e o <xref:Microsoft.VisualStudio.Package.EditArray> objeto mantém as edições feitas no span. Observe que essa extensão pode ser o documento inteiro. No entanto, como é provável que haja várias alterações feitas no span, todas as alterações devem ser reversível em uma única ação. Para fazer isso, empacote todas as alterações em um <xref:Microsoft.VisualStudio.Package.CompoundAction> objeto (consulte a seção "usando a classe comlibraaction" neste tópico).

### <a name="example"></a>Exemplo

O exemplo a seguir garante que haja um único espaço após cada vírgula na seleção, a menos que a vírgula seja seguida por uma Tabulação ou esteja no final da linha. Os espaços à direita após a última vírgula em uma linha são excluídos. Consulte a seção "usando a classe comlibraaction" neste tópico para ver como esse método é chamado a partir do <xref:Microsoft.VisualStudio.Package.Source.ReformatSpan%2A> método.

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

## <a name="using-the-compoundaction-class"></a>Usando a classe comlibraaction

Toda a reformatação feita em uma seção de código deve ser reversível em uma única ação. Isso pode ser feito usando uma <xref:Microsoft.VisualStudio.Package.CompoundAction> classe. Essa classe encapsula um conjunto de operações de edição no buffer de texto em uma única operação de edição.

### <a name="example"></a>Exemplo

Aqui está um exemplo de como usar a <xref:Microsoft.VisualStudio.Package.CompoundAction> classe. Consulte o exemplo na seção "Implementando o suporte para formatação" neste tópico para obter um exemplo do `DoFormatting` método.

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

## <a name="see-also"></a>Confira também

- [Recursos do serviço de linguagem herdado](legacy-language-service-features1.md)
