---
title: Suporte para a janela Autos em um serviço de linguagem herdado | Microsoft Docs
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
- language services [managed package framework], Autos window
- Autos window, supporting in language services [managed package framework]
ms.assetid: 47d40aae-7a3c-41e1-a949-34989924aefb
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8e1f787b3a0f2ab1c153dfd3742c8939975e3ad1
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764468"
---
# <a name="support-for-the-autos-window-in-a-legacy-language-service"></a>Suporte para a janela de automáticos em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O **automóveis** janela exibe expressões como variáveis e parâmetros que estão no escopo quando o programa que está sendo depurado está em pausa (seja devido a um ponto de interrupção ou uma exceção). As expressões podem incluir variáveis, locais ou globais e os parâmetros que foram alterados no escopo local. O **automóveis** janela também pode incluir instanciações de uma classe, estrutura ou algum outro tipo. Tudo o que um avaliador de expressão pode avaliar potencialmente pode ser mostrado na **automóveis** janela.  
  
 A estrutura de pacote gerenciado (MPF) não oferece suporte direto para o **automóveis** janela. No entanto, se você substituir a <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> método, você pode retornar uma lista de expressões a ser apresentado na **Autos** janela.  
  
## <a name="implementing-support-for-the-autos-window"></a>Implementação de suporte para a janela Autos  
 Tudo que você precisa fazer para dar suporte a **Autos** janela é implementar a <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> método no <xref:Microsoft.VisualStudio.Package.LanguageService> classe. Sua implementação deve decidir, dado um local no arquivo de origem, expressões devem aparecer na **automóveis** janela. O método retorna uma lista de cadeias de caracteres na qual cada cadeia de caracteres representa uma única expressão. Um valor de retorno <xref:Microsoft.VisualStudio.VSConstants.S_OK> indica que a lista contém expressões, enquanto <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> indica que não há nenhuma expressão para mostrar.  
  
 As expressões reais retornadas são os nomes dos parâmetros que aparecem nesse local no código ou variáveis. Esses nomes são passados para o avaliador de expressão para obter valores e tipos que são exibidos na **automóveis** janela.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma implementação do <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> método que obtém uma lista de expressões do <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método usando o motivo pelo qual análise <xref:Microsoft.VisualStudio.Package.ParseReason>. Cada uma das expressões é empacotada como um `TestVsEnumBSTR` que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsEnumBSTR> interface.  
  
 Observe que o `GetAutoExpressionsCount` e `GetAutoExpression` métodos são métodos personalizados no `TestAuthoringSink` do objeto e foram adicionados para dar suporte a este exemplo. Eles representam uma maneira de em quais expressões adicionadas para o `TestAuthoringSink` objeto pelo analisador (chamando o <xref:Microsoft.VisualStudio.Package.AuthoringSink.AutoExpression%2A> método) podem ser acessados fora do analisador.  
  
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

