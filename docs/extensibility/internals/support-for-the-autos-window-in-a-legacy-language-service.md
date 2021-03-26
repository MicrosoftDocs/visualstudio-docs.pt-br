---
title: Dar suporte à janela Autos em um serviço de linguagem herdada
description: Saiba como implementar o suporte para a janela automáticos, que exibe as expressões que estão no escopo quando o programa que está sendo depurado é pausado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], Autos window
- Autos window, supporting in language services [managed package framework]
ms.assetid: 47d40aae-7a3c-41e1-a949-34989924aefb
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 70a8697027cde07ca2b30d01a73a80d771155c5c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080626"
---
# <a name="support-for-the-autos-window-in-a-legacy-language-service"></a>Suporte para a janela de automóveis em um serviço de linguagem herdado

A janela **automáticos** exibe expressões como variáveis e parâmetros que estão no escopo quando o programa que está sendo depurado é pausado (devido a um ponto de interrupção ou uma exceção). As expressões podem incluir variáveis, locais ou globais, e parâmetros que foram alterados no escopo local. A janela **autos** também pode incluir instanciações de uma classe, estrutura ou algum outro tipo. Tudo o que um avaliador de expressão pode avaliar pode ser mostrado na janela **autos** .

 A MPF (estrutura de pacote gerenciada) não fornece suporte direto para a janela de **automóveis** . No entanto, se você substituir o <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> método, poderá retornar uma lista de expressões a serem apresentadas na janela **autos** .

## <a name="implementing-support-for-the-autos-window"></a>Implementando o suporte para a janela de automóveis

 Tudo o que você precisa fazer para dar suporte à janela **autos** é implementar o <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe. Sua implementação deve decidir, dado um local no arquivo de origem, quais expressões devem aparecer na janela **autos** . O método retorna uma lista de cadeias de caracteres nas quais cada cadeia representa uma única expressão. Um valor de retorno <xref:Microsoft.VisualStudio.VSConstants.S_OK> indica que a lista contém expressões, enquanto <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> indica que não há expressões a serem mostradas.

 As expressões reais retornadas são os nomes das variáveis ou parâmetros que aparecem nesse local no código. Esses nomes são passados para o avaliador de expressão para obter valores e tipos que são exibidos na janela **automáticos** .

### <a name="example"></a>Exemplo
 O exemplo a seguir mostra uma implementação do <xref:Microsoft.VisualStudio.Package.LanguageService.GetProximityExpressions%2A> método que obtém uma lista de expressões do <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método usando o motivo da análise <xref:Microsoft.VisualStudio.Package.ParseReason> . Cada uma das expressões é encapsulada como um `TestVsEnumBSTR` que implementa a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsEnumBSTR> interface.

 Observe que os `GetAutoExpressionsCount` `GetAutoExpression` métodos e são métodos personalizados no `TestAuthoringSink` objeto e foram adicionados para dar suporte a esse exemplo. Elas representam uma maneira na qual as expressões adicionadas ao `TestAuthoringSink` objeto pelo analisador (chamando o <xref:Microsoft.VisualStudio.Package.AuthoringSink.AutoExpression%2A> método) podem ser acessadas fora do analisador.

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
