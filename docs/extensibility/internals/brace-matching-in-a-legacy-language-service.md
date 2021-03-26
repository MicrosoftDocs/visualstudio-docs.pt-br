---
title: Correspondência de chaves em um serviço de idioma herdado | Microsoft Docs
description: Saiba mais sobre correspondência de chaves em um serviço de linguagem herdado, que ajuda a acompanhar elementos de linguagem que devem ocorrer juntos, como parênteses e chaves.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- brace matching
- language services [managed package framework], brace matching
ms.assetid: 4e3d0a70-f22f-49dd-92d8-edf48ab62b52
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a92a3ca34e6314463bbfecbd8c4236789f213635
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086099"
---
# <a name="brace-matching-in-a-legacy-language-service"></a>Correspondência de chaves em um serviço de idioma herdado
Correspondência de chaves ajuda o desenvolvedor a acompanhar elementos de linguagem que precisam ocorrer juntos, como parênteses e chaves. Quando um desenvolvedor entra em uma chave de fechamento, a chave de abertura é realçada.

 Você pode corresponder a dois ou três elementos coincidentes, chamados pares e corridas. As corridas são conjuntos de três elementos coexistentes. Por exemplo, em C#, a `foreach` instrução forma um triplo: `foreach()` , `{` e `}` . Todos os três elementos são realçados quando a chave de fechamento é digitada.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para saber mais sobre a nova maneira de implementar a correspondência de chaves, consulte [passo a passos: Exibir chaves correspondentes](../../extensibility/walkthrough-displaying-matching-braces.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

 A <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe dá suporte a pares e corridas com os <xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchPair%2A> <xref:Microsoft.VisualStudio.Package.AuthoringSink.MatchTriple%2A> métodos e.

## <a name="implementation"></a>Implementação
 O serviço de linguagem precisa identificar todos os elementos correspondentes no idioma e, em seguida, localizar todos os pares correspondentes. Isso normalmente é feito pela implementação do <xref:Microsoft.VisualStudio.Package.IScanner> para detectar um idioma correspondente e, em seguida, usar o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método para corresponder os elementos.

 O <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> método chama o scanner para indexar a linha e retornar o token logo antes do cursor. O verificador indica que um par de elementos de linguagem foi encontrado definindo um valor de gatilho de token de <xref:Microsoft.VisualStudio.Package.TokenTriggers> no token atual. O <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> método chama o <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> método que, por sua vez, chama o <xref:Microsoft.VisualStudio.Package.LanguageService.BeginParse%2A> método com o valor da razão de análise de <xref:Microsoft.VisualStudio.Package.ParseReason> para localizar o elemento de linguagem correspondente. Quando o elemento de idioma correspondente é encontrado, ambos os elementos são realçados.

 Para obter uma descrição completa de como digitar uma chave dispara o realce de chaves, consulte a seção de *exemplo de operação de análise* no artigo [analisador de serviço de idioma herdado e scanner](../../extensibility/internals/legacy-language-service-parser-and-scanner.md).

## <a name="enable-support-for-brace-matching"></a>Habilitar suporte para correspondência de chaves
 O <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> atributo pode definir as entradas do registro **MatchBraces**, **MatchBracesAtCaret** e **ShowMatchingBrace** que definem as propriedades correspondentes da <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe. As propriedades de preferência de idioma também podem ser definidas pelo usuário.

|Entrada de registro|Propriedade|Descrição|
|--------------------|--------------|-----------------|
|MatchBraces|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBraces%2A>|Habilita a correspondência de chaves.|
|MatchBracesAtCaret|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableMatchBracesAtCaret%2A>|Habilita a correspondência de chaves conforme o cursor se move.|
|ShowMatchingBrace|<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>|Realça a chave correspondente.|

## <a name="match-conditional-statements"></a>Corresponder instruções condicionais
 Você pode fazer a correspondência de instruções condicionais, como,, `if` `else if` e `else` , ou `#if` , `#elif` ,, `#else` `#endif` da mesma forma que os delimitadores correspondentes. Você pode subclassear a <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe e fornecer um método que possa adicionar intervalos de texto, bem como delimitadores, à matriz interna de elementos correspondentes.

## <a name="set-the-trigger"></a>Definir o gatilho
 O exemplo a seguir mostra como detectar parênteses correspondentes, chaves e chaves quadradas e definir o gatilho para ele no scanner. O <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> método na <xref:Microsoft.VisualStudio.Package.Source> classe detecta o gatilho e chama o analisador para localizar o par correspondente (consulte a seção *localizando a correspondência* neste artigo). Este exemplo é apenas para fins ilustrativos. Ele pressupõe que o scanner contém um método `GetNextToken` que identifica e retorna tokens de uma linha de texto.

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private const string braces = "()[]{}";
        private Lexer lex;

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false;
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char firstChar = token[0];
                if (Char.IsPunctuation(firstChar) && token.Length > 0)
                {
                    if (braces.IndexOf(firstChar) != -1)
                    {
                        tokenInfo.Trigger = TokenTriggers.MatchBraces;
                    }
                }
            }
            return foundToken;
        }
```

## <a name="match-the-braces"></a>Corresponder às chaves
 Este é um exemplo simplificado para corresponder os elementos de linguagem `{ }` , `( )` e e `[ ]` adicionar seus intervalos ao <xref:Microsoft.VisualStudio.Package.AuthoringSink> objeto. Essa abordagem não é uma abordagem recomendada para a análise do código-fonte; Ele é apenas para fins ilustrativos.

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class Parser
    {
         private IList<TextSpan[]> m_braces;
         public IList<TextSpan[]> Braces
         {
             get { return m_braces; }
         }
         private void AddMatchingBraces(TextSpan braceSpan1, TextSpan braceSpan2)
         {
             if IsMatch(braceSpan1, braceSpan2)
                 m_braces.Add(new TextSpan[] { braceSpan1, braceSpan2 });
         }

         private bool IsMatch(TextSpan braceSpan1, TextSpan braceSpan2)
         {
             //definition for matching here
          }
    }

    public class TestLanguageService : LanguageService
    {
         Parser parser = new Parser();
         Source source = (Source) this.GetSource(req.FileName);

         private AuthoringScope ParseSource(ParseRequest req)
         {
             if (req.Sink.BraceMatching)
             {
                 if (req.Reason==ParseReason.MatchBraces)
                 {
                     foreach (TextSpan[] brace in parser.Braces)
                     {
                         req.Sink.MatchPair(brace[0], brace[1], 1);
                     }
                 }
             }
             return new TestAuthoringScope();
         }
    }
}
```

## <a name="see-also"></a>Confira também
- [Recursos do serviço de linguagem herdada](../../extensibility/internals/legacy-language-service-features1.md)
- [Analisador e scanner do serviço de idioma herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
