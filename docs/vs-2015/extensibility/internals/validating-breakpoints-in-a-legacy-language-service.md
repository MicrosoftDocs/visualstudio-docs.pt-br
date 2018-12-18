---
title: Validar pontos de interrupção em um serviço de linguagem herdado | Microsoft Docs
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
- breakpoint validation
- language services [managed package framework], breakpoint validation
ms.assetid: a7e873cd-dfe1-474f-bda5-fd7532774b15
caps.latest.revision: 15
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 0868e516720fd32a445f60f05f345936d24d6d7a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51734977"
---
# <a name="validating-breakpoints-in-a-legacy-language-service"></a>Validando pontos de interrupção em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um ponto de interrupção indica que a execução do programa deve parar em um ponto específico, enquanto ele está sendo executado em um depurador. Um usuário pode colocar um ponto de interrupção em qualquer linha no arquivo de origem, uma vez que o editor não tem conhecimento sobre o que constitui um local válido para um ponto de interrupção. Quando o depurador é iniciado, todos os pontos de interrupção marcados (chamados de pontos de interrupção pendentes) são vinculados para o local apropriado no programa em execução. Ao mesmo tempo que os pontos de interrupção são validados para garantir que eles marcam os locais de código válido. Por exemplo, um ponto de interrupção em um comentário não é válido, porque não há nenhum código nesse local no código-fonte. O depurador desabilita os pontos de interrupção inválidos.  
  
 Uma vez que o serviço de linguagem sabe sobre o código-fonte que está sendo exibido, pode validar os pontos de interrupção antes que o depurador é iniciado. Você pode substituir o <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> método retorne um span especificando um local válido para um ponto de interrupção. O local do ponto de interrupção ainda é validado quando o depurador é iniciado, mas o usuário é notificado de pontos de interrupção inválida sem esperar que o depurador carregar.  
  
## <a name="implementing-support-for-validating-breakpoints"></a>Implementação do suporte para validar os pontos de interrupção  
  
-   O <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> método é dada a posição do ponto de interrupção. Sua implementação deve decidir se o local é válido e indicar isso retornando um intervalo de texto que identifica o código associado com a posição da linha que o ponto de interrupção.  
  
-   Retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK> se o local for válido, ou <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> se ele não é válido.  
  
-   Se o ponto de interrupção é válido, o intervalo de texto é realçado, juntamente com o ponto de interrupção.  
  
-   Se o ponto de interrupção for inválido, uma mensagem de erro será exibida na barra de status.  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra uma implementação do <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> método que chama o analisador para obter o trecho de código (se houver) no local especificado.  
  
 Este exemplo pressupõe que você tenha adicionado uma `GetCodeSpan` método para o <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe que valida o intervalo de texto e retorna `true` se ele for um local de ponto de interrupção válido.  
  
```csharp  
using Microsoft VisualStudio;  
using Microsoft.VisualStudio.Package;  
using Microsoft.VisualStudio.TextManager.Interop;  
  
namespace TestLanguagePackage  
{  
    class TestLanguageService : LanguageService  
    {  
        public override int ValidateBreakpointLocation(IVsTextBuffer buffer,  
                                                       int line,  
                                                       int col,  
                                                       TextSpan[] pCodeSpan)  
        {  
            int retval = VSConstants.S_FALSE;  
            if (pCodeSpan != null)  
            {  
                // Initialize span to current line by default.  
                pCodeSpan[0].iStartLine = line;  
                pCodeSpan[0].iStartIndex = col;  
                pCodeSpan[0].iEndLine = line;  
                pCodeSpan[0].iEndIndex = col;  
            }  
  
            if (buffer != null)  
            {  
                IVsTextLines textLines = buffer as IVsTextLines;  
                if (textLines != null)  
                {  
                    Source src = this.GetSource(textLines);  
                    if (src != null)  
                    {  
                        TokenInfo tokenInfo = new TokenInfo();  
                        string text = src.GetText();  
                        ParseRequest req = CreateParseRequest(src,  
                                                              line,  
                                                              col,  
                                                              tokenInfo,  
                                                              text,  
                                                              src.GetFilePath(),  
                                                              ParseReason.CodeSpan,  
                                                              null);  
                        req.Scope = this.ParseSource(req);  
                        TestAuthoringSink sink = req.Sink as TestAuthoringSink;  
  
                        TextSpan span = new TextSpan();  
                        if (sink.GetCodeSpan(out span))  
                        {  
                            pCodeSpan[0] = span;  
                            retval = VSConstants.S_OK;  
                        }  
                    }  
                }  
            }  
            return retval;  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)

