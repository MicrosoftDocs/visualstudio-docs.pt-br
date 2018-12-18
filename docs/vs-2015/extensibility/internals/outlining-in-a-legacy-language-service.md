---
title: Estrutura de tópicos em um serviço de linguagem herdado | Microsoft Docs
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
- outlining
- language services [managed package framework], outlining
- outlining, supporting in language services [managed package framework]
ms.assetid: 7b5578b4-a20a-4b94-ad4c-98687ac133b9
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 356b3d49fa8eb74ef2352e6ba36597d1c39fecf4
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51751537"
---
# <a name="outlining-in-a-legacy-language-service"></a>Estrutura de tópicos em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Estrutura de tópicos torna possível recolher um programa complexo em uma visão geral ou a estrutura de tópicos. Por exemplo, no c# todos os métodos podem ser recolhidos para uma única linha, mostrando apenas a assinatura do método. Além disso, as estruturas e classes podem ser recolhidas para mostrar somente os nomes das estruturas e classes. Dentro de um único método, uma lógica complexa pode ser recolhida para mostrar o fluxo geral mostrando apenas a primeira linha de instruções, como `foreach`, `if`, e `while`.  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações, consulte [instruções passo a passo: estrutura de tópicos](../../extensibility/walkthrough-outlining.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
## <a name="enabling-support-for-outlining"></a>Habilitando o suporte para a estrutura de tópicos  
 O `AutoOutlining` entrada do registro é definida como 1 para habilitar a estrutura de tópicos automática. Estrutura de tópicos automática configura uma análise da fonte inteira quando um arquivo for carregado ou alterado para identificar regiões ocultas e mostrar os glifos de estrutura de tópicos. Estrutura de tópicos também pode ser controlada manualmente pelo usuário.  
  
 O valor da `AutoOutlining` entrada de registro pode ser obtida por meio do <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> propriedade no <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe. O `AutoOutlining` entrada de registro pode ser inicializada com um parâmetro nomeado para o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> atributo (consulte [Registrando um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md) para obter detalhes).  
  
## <a name="the-hidden-region"></a>A região oculta  
 Para fornecer a estrutura de tópicos, o serviço de linguagem deve dar suporte a regiões ocultas. Esses são os intervalos de texto que podem ser expandidos ou recolhidos. Regiões ocultas podem ser delimitados por símbolos de idioma padrão, como chaves, ou por símbolos personalizados. Por exemplo, o c# tem um `#region` / `#endregion` par que delimita uma região oculta.  
  
 Regiões ocultas são gerenciados por um Gerenciador de região oculta, que é exposto como o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenTextSession> interface.  
  
 Estrutura de tópicos usa regiões ocultas o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiddenRegion> de interface e conter o alcance da região oculta, o estado de visibilidade atual e a faixa a ser mostrado quando o período é recolhido.  
  
 O analisador de serviço de linguagem usa o <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> método para adicionar uma nova região ocultada com o comportamento padrão para as regiões ocultas, embora o <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddHiddenRegion%2A> método permite que você personalize a aparência e comportamento da estrutura de tópicos. Depois que as regiões ocultas são fornecidos para a sessão de região oculta, [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] gerencia as regiões ocultas para o serviço de linguagem.  
  
 Se você precisar determinar quando a sessão de região oculta é destruída, uma região oculta é alterada, ou você precisa certificar-se de que uma determinada região oculta estiver visível; Você deve derivar uma classe a partir de <xref:Microsoft.VisualStudio.Package.Source> de classe e substituir os métodos apropriados, <xref:Microsoft.VisualStudio.Package.Source.OnBeforeSessionEnd%2A>, <xref:Microsoft.VisualStudio.Package.Source.OnHiddenRegionChange%2A>, e <xref:Microsoft.VisualStudio.Package.Source.MakeBaseSpanVisible%2A>, respectivamente.  
  
### <a name="example"></a>Exemplo  
 Aqui está um exemplo simplificado de criação de regiões ocultas para todos os pares de chaves. Supõe-se que a linguagem fornece a correspondência de chaves e as chaves a serem correspondidos incluem pelo menos as chaves ({e}). Essa abordagem é apenas para fins ilustrativos. Uma implementação completa teria um tratamento completo de casos no <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>. Este exemplo também mostra como definir a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.AutoOutlining%2A> preferência para `true` temporariamente. Uma alternativa é especificar o `AutoOutlining` parâmetro no nomeado o `ProvideLanguageServiceAttribute` atributo em seu pacote de idiomas.  
  
 Este exemplo presume c# regras para comentários, cadeias de caracteres e literais.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)   
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)

