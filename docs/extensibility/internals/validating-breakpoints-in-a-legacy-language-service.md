---
title: Validando pontos de interrupção em um serviço de linguagem herdada | Microsoft Docs
description: Saiba como você pode substituir o método ValidateBreakpointLocation em um serviço de linguagem herdado para validar os pontos de interrupção antes que o depurador seja iniciado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoint validation
- language services [managed package framework], breakpoint validation
ms.assetid: a7e873cd-dfe1-474f-bda5-fd7532774b15
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 86029300c34e111344157bf39a15dceab8c1b77a
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085787"
---
# <a name="validating-breakpoints-in-a-legacy-language-service"></a>Validando pontos de interrupção em um serviço de linguagem herdado
Um ponto de interrupção indica que a execução do programa deve parar em um momento específico enquanto está sendo executada em um depurador. Um usuário pode inserir um ponto de interrupção em qualquer linha no arquivo de origem, já que o editor não tem conhecimento do que constitui um local válido para um ponto de interrupção. Quando o depurador é iniciado, todos os pontos de interrupção marcados (chamados de pontos de interrupção pendentes) são associados ao local apropriado no programa em execução. Ao mesmo tempo, os pontos de interrupção são validados para garantir que eles marquem locais de código válidos. Por exemplo, um ponto de interrupção em um comentário não é válido, pois não há nenhum código nesse local no código-fonte. O depurador desabilita pontos de interrupção inválidos.

 Como o serviço de linguagem sabe sobre o código-fonte que está sendo exibido, ele pode validar os pontos de interrupção antes que o depurador seja iniciado. Você pode substituir o <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> método para retornar um intervalo especificando um local válido para um ponto de interrupção. O local do ponto de interrupção ainda é validado quando o depurador é iniciado, mas o usuário é notificado sobre pontos de interrupção inválidos sem esperar que o depurador seja carregado.

## <a name="implementing-support-for-validating-breakpoints"></a>Implementando suporte para validação de pontos de interrupção

- O <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> método recebe a posição do ponto de interrupção. Sua implementação deve decidir se o local é válido e indicar isso retornando um intervalo de texto que identifica o código associado à posição da linha do ponto de interrupção.

- Retornar <xref:Microsoft.VisualStudio.VSConstants.S_OK> se o local for válido ou <xref:Microsoft.VisualStudio.VSConstants.S_FALSE> se não for válido.

- Se o ponto de interrupção for válido, o intervalo de texto será realçado junto com o ponto de interrupção.

- Se o ponto de interrupção for inválido, uma mensagem de erro aparecerá na barra de status.

### <a name="example"></a>Exemplo
 Este exemplo mostra uma implementação do <xref:Microsoft.VisualStudio.Package.LanguageService.ValidateBreakpointLocation%2A> método que chama o analisador para obter o intervalo de código (se houver) no local especificado.

 Este exemplo pressupõe que você adicionou um `GetCodeSpan` método à <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe que valida o intervalo de texto e retorna `true` se ele é um local de ponto de interrupção válido.

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

## <a name="see-also"></a>Confira também
- [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)
