---
title: Suporte para a janela Autos em um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], Autos window
- Autos window, supporting in language services [managed package framework]
ms.assetid: 47d40aae-7a3c-41e1-a949-34989924aefb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: a1a2627bd36e6047db00afaada231dc49cde2cc3
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31135816"
---
# <a name="support-for-the-autos-window-in-a-legacy-language-service"></a>Suporte para a janela Autos em um serviço de linguagem herdado
O **Autos** janela exibe expressões como variáveis e parâmetros que estão no escopo quando o programa que está sendo depurado está em pausa (seja devido a um ponto de interrupção ou exceção). As expressões podem incluir variáveis, locais ou globais e os parâmetros que foram alterados no escopo local. O **Autos** janela também pode incluir instâncias de uma classe, estrutura ou algum outro tipo. Tudo o que pode avaliar um avaliador de expressão potencialmente pode ser mostrado no **Autos** janela.  
  
 A estrutura de pacote gerenciado (MPF) não oferece suporte direto para o **Autos** janela. No entanto, se você substituir o <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> método, você pode retornar uma lista de expressões a serem apresentados no **Autos** janela.  
  
## <a name="implementing-support-for-the-autos-window"></a>Implementando o suporte para a janela Autos  
 Você só precisa fazer para dar suporte a **Autos** janela é implementar o <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> método no <xref:Microsoft.VisualStudio.Package.LanguageService> classe. Sua implementação deve decidir, dado um local no arquivo de origem, expressões devem aparecer no **Autos** janela. O método retorna uma lista de cadeias de caracteres na qual cada cadeia de caracteres representa uma única expressão. Um valor de retorno <xref:Microsoft.VisualStudio.VSConstants.S_OK> indica que a lista contém expressões, enquanto <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> indica que não há nenhuma expressão para mostrar.  
  
 As expressões reais retornadas são os nomes dos parâmetros que aparecem nesse local no código ou variáveis. Esses nomes são passados para o avaliador de expressão para obter valores e tipos que são exibidos no **Autos** janela.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma implementação do <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> método que obtém uma lista de expressões do <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> usando o motivo de análise do método <xref:Microsoft.VisualStudio.Package.ParseReason>. Cada uma das expressões é empacotada como um `TestVsEnumBSTR` que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsEnumBSTR> interface.  
  
 Observe que o `GetAutoExpressionsCount` e `GetAutoExpression` métodos são métodos personalizados no `TestAuthoringSink` de objeto e foram adicionadas para oferecer suporte a este exemplo. Eles representam uma maneira na qual expressões adicionado ao `TestAuthoringSink` objeto pelo analisador (chamando o <xref:Microsoft.VisualStudio.Package.AuthoringSink.AutoExpression%2A> método) pode ser acessado fora do analisador.  
  
```csharp  
using Microsoft.VisualStudio;  
using Microsoft.VisualStudio.Package;  
using Microsoft.VisualStudio.TextManager.Interop;  
  
namespace TestLanguagePackage  
{  
    public class TestLanguageService : LanguageService  
    {  
        public override int GetProximityExpressions(IVsTextBuffer buffer,  
                                                    int line,  
                                                    int col,  
                                                    int cLines,  
                                                    out IVsEnumBSTR ppEnum)  
        {  
            int retval = VSConstants.E_NOTIMPL;  
            ppEnum = null;  
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
                                                              ParseReason.Autos,  
                                                              null);  
                        req.Scope = this.ParseSource(req);  
                        TestAuthoringSink sink = req.Sink as TestAuthoringSink;  
  
                        retval = VSConstants.S_FALSE;  
                        int spanCount = sink.GetAutoExpressionsCount();  
                        if (spanCount > 0) {  
                            TestVsEnumBSTR bstrList = new TestVsEnumBSTR();  
                            for (int i = 0; i < spanCount; i++)  
                            {  
                                TextSpan span;  
                                sink.GetAutoExpression(i, out span);  
                                string expression = src.GetText(span.iStartLine,  
                                                                span.iStartIndex,  
                                                                span.iEndLine,  
                                                                span.iEndIndex);  
                                bstrList.AddString(expression);  
                            }  
                            ppEnum = bstrList;  
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