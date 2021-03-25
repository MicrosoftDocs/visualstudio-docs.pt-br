---
title: Estrutura de tópicos em um serviço de linguagem herdada | Microsoft Docs
description: Saiba como dar suporte à estrutura de tópicos por meio da implementação de regiões ocultas em um serviço de linguagem herdado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- outlining
- language services [managed package framework], outlining
- outlining, supporting in language services [managed package framework]
ms.assetid: 7b5578b4-a20a-4b94-ad4c-98687ac133b9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a56d755341aa611f0e2762f6bae8940778fe0864
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062948"
---
# <a name="outlining-in-a-legacy-language-service"></a>Estrutura de tópicos em um serviço de linguagem herdado
A estrutura de tópicos torna possível recolher um programa complexo em uma visão geral ou uma estrutura de tópicos. Por exemplo, em C#, todos os métodos podem ser recolhidos para uma única linha, mostrando apenas a assinatura do método. Além disso, estruturas e classes podem ser recolhidas para mostrar apenas os nomes das estruturas e classes. Dentro de um único método, a lógica complexa pode ser recolhida para mostrar o fluxo geral, mostrando apenas a primeira linha de instruções, como `foreach` , `if` e `while` .

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para obter mais informações, consulte [Walkthrough: contorno](../../extensibility/walkthrough-outlining.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="enabling-support-for-outlining"></a>Habilitando o suporte para estrutura de tópicos
 A `AutoOutlining` entrada do registro é definida como 1 para habilitar a estrutura de tópicos automática. A estrutura de tópicos automática define uma análise da origem inteira quando um arquivo é carregado ou alterado para identificar regiões ocultas e mostrar os glifos de estrutura de tópicos. A estrutura de tópicos também pode ser controlada manualmente pelo usuário.

 O valor da `AutoOutlining` entrada do registro pode ser obtido por meio da <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> Propriedade na <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe. A `AutoOutlining` entrada do registro pode ser inicializada com um parâmetro nomeado para o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> atributo (consulte [registrando um serviço de idioma herdado](../../extensibility/internals/registering-a-legacy-language-service1.md) para obter detalhes).

## <a name="the-hidden-region"></a>A região oculta
 Para fornecer a estrutura de tópicos, o serviço de idioma deve dar suporte a regiões ocultas. Esses são trechos de texto que podem ser expandidos ou recolhidos. Regiões ocultas podem ser delimitadas por símbolos de idioma padrão, como chaves, ou por símbolos personalizados. Por exemplo, C# tem um `#region` / `#endregion` par que delimita uma região oculta.

 As regiões ocultas são gerenciadas por um Gerenciador de região oculta, que é exposto como a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> interface.

 A estrutura de tópicos usa regiões ocultas a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegion> interface e contém o intervalo da região oculta, o estado atual visível e a faixa a ser mostrada quando a extensão é recolhida.

 O analisador de serviço de linguagem usa o <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> método para adicionar uma nova região oculta com o comportamento padrão para regiões ocultas, enquanto o <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> método permite que você personalize a aparência e o comportamento do contorno. Depois que as regiões ocultas são dadas à sessão de região oculta, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] o gerencia as regiões ocultas para o serviço de idioma.

 Se você precisar determinar quando a sessão de região oculta é destruída, uma região oculta é alterada ou você precisa garantir que uma região oculta específica esteja visível; Você deve derivar uma classe da <xref:Microsoft.VisualStudio.Package.Source> classe e substituir os métodos apropriados, <xref:Microsoft.VisualStudio.Package.Source.OnBeforeSessionEnd%2A> , <xref:Microsoft.VisualStudio.Package.Source.OnHiddenRegionChange%2A> e <xref:Microsoft.VisualStudio.Package.Source.MakeBaseSpanVisible%2A> , respectivamente.

### <a name="example"></a>Exemplo
 Aqui está um exemplo simplificado de criação de regiões ocultas para todos os pares de chaves. Supõe-se que a linguagem forneça correspondência de chaves e que as chaves a serem correspondidas incluam pelo menos as chaves ({e}). Essa abordagem é apenas para fins ilustrativos. Uma implementação completa teria uma manipulação completa de casos no <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> . Este exemplo também mostra como definir a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> preferência como `true` temporariamente. Uma alternativa é especificar o `AutoOutlining` parâmetro nomeado no `ProvideLanguageServiceAttribute` atributo em seu pacote de idioma.

 Este exemplo pressupõe regras C# para comentários, cadeias de caracteres e literais.

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace MyLanguagePackage
{

    public class MyLanguageService : LanguageService
    {
        private LanguagePreferences m_preferences;

        public override LanguagePreferences  GetLanguagePreferences()
        {
            if (m_preferences == null)
            {
                m_preferences = new LanguagePreferences(this.Site,
                                                        typeof(MyLanguageService).GUID,
                                                        Name);
                m_preferences.Init();
                // Temporarily enabled auto-outlining
                m_preferences.AutoOutlining = true;
            }
            return m_preferences;
        }

        public override AuthoringScope  ParseSource(ParseRequest req)
        {
            Source source = (Source) this.GetSource(req.FileName);
            switch (req.Reason)
            {
               case ParseReason.HighlightBraces:
               case ParseReason.MatchBraces:
               case ParseReason.MemberSelectAndHighlightBraces:
                  if (source.Braces != null)
                  {
                      foreach (TextSpan[] brace in source.Braces)
                      {
                         if (brace.Length == 2)
                         {
                             if (req.Sink.HiddenRegions == true
                                   && source.GetText(brace[0]).Equals("{")
                                   && source.GetText(brace[1]).Equals("}"))
                             {
                                //construct a TextSpan of everything between the braces
                                TextSpan hideSpan = new TextSpan();
                                hideSpan.iStartIndex = brace[0].iStartIndex;
                                hideSpan.iStartLine = brace[0].iStartLine;
                                hideSpan.iEndIndex = brace[1].iEndIndex;
                                hideSpan.iEndLine = brace[1].iEndLine;
                                req.Sink.ProcessHiddenRegions = true;
                                req.Sink.AddHiddenRegion(hideSpan);
                             }
                             req.Sink.MatchPair(brace[0], brace[1], 1);
                         }
                         else if (brace.Length >= 3)
                             req.Sink.MatchTriple(brace[0], brace[1], brace[2], 1);
                  }
        }
                   break;
               default:
                   break;
      }
            // Must always return a valid AuthoringScope object.
            return new MyAuthoringScope();
        }
    }
}
```

## <a name="see-also"></a>Confira também
- [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)
- [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)
