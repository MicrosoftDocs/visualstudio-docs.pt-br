---
title: Informações de parâmetro em um idioma herdado Service2 | Microsoft Docs
description: Saiba como dar suporte à operação de informações de parâmetro do IntelliSense para exibir uma assinatura de método, pois o método é digitado em um serviço de linguagem herdado.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Parameter Info tool tip
- language services [managed package framework], IntelliSense Parameter Info
- Parameter Info (IntelliSense), supporting in language services [managed package framework]
ms.assetid: a117365d-320d-4bb5-b61d-3e6457b8f6bc
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0488c9d6570d9ed127c5b021ddfcf7d74f0dd856
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062922"
---
# <a name="parameter-info-in-a-legacy-language-service-2"></a>Informações de parâmetro em um serviço de linguagem herdado 2
As informações de parâmetro do IntelliSense são uma dica de ferramenta que exibe a assinatura de um método quando o usuário digita o caractere inicial da lista de parâmetros (normalmente um parêntese de abertura) para a lista de parâmetros do método. À medida que cada parâmetro é inserido e o separador de parâmetro (normalmente uma vírgula) é digitado, a dica de ferramenta é atualizada para mostrar o próximo parâmetro em negrito.

 As classes do MPF (estrutura de pacote gerenciada) fornecem suporte para gerenciar a dica de ferramenta de informações de parâmetro. O analisador deve detectar os caracteres de início do parâmetro, do próximo parâmetro e de término do parâmetro, e deve fornecer uma lista das assinaturas do método e seus parâmetros associados.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para obter mais informações, consulte [estendendo o editor e os serviços de linguagem](../../extensibility/extending-the-editor-and-language-services.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="implementation"></a>Implementação
 O analisador deve definir que o valor do gatilho <xref:Microsoft.VisualStudio.Package.TokenTriggers> seja definido quando encontrar um caractere de início da lista de parâmetros (geralmente um parêntese de abertura). Ele deve definir um <xref:Microsoft.VisualStudio.Package.TokenTriggers> gatilho quando encontrar um separador de parâmetro (geralmente uma vírgula). Isso faz com que uma dica de ferramenta de informações de parâmetro seja atualizada e mostre o próximo parâmetro em negrito. O analisador deve definir o valor do gatilho <xref:Microsoft.VisualStudio.Package.TokenTriggers> quando se encontrar o caractere final da lista de parâmetros (geralmente um parêntese de fechamento).

 O <xref:Microsoft.VisualStudio.Package.TokenTriggers> valor do gatilho inicia uma chamada para o <xref:Microsoft.VisualStudio.Package.Source.MethodTip%2A> método que, por sua vez, chama o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> analisador de método com um motivo de análise de <xref:Microsoft.VisualStudio.Package.ParseReason> . Se o analisador determinar que o identificador antes do caractere de início da lista de parâmetros é um nome de método reconhecido, ele retornará uma lista de assinaturas de método correspondentes no <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto. Se alguma assinatura de método for encontrada, a dica de ferramenta informações de parâmetro será exibida com a primeira Signature na lista. Essa dica de ferramenta é então atualizada à medida que mais da assinatura é digitada. Quando o caractere final da lista de parâmetros é digitado, a dica de ferramenta informações do parâmetro é removida da exibição.

> [!NOTE]
> Para garantir que a dica de ferramenta informações do parâmetro esteja formatada corretamente, você deve substituir as propriedades na <xref:Microsoft.VisualStudio.Package.Methods> classe para fornecer os caracteres apropriados. A <xref:Microsoft.VisualStudio.Package.Methods> classe base pressupõe uma assinatura de método de estilo C#. Consulte a <xref:Microsoft.VisualStudio.Package.Methods> classe para obter detalhes sobre como isso pode ser feito.

## <a name="enabling-support-for-the-parameter-info"></a>Habilitando o suporte para as informações de parâmetro
 Para dar suporte a dicas de ferramentas de informações de parâmetros, você deve definir o `ShowCompletion` parâmetro nomeado do <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> para `true` . O serviço de idioma lê o valor dessa entrada de registro da <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> propriedade.

 Além disso, a <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ParameterInformation%2A> propriedade deve ser definida como `true` para a dica de ferramenta informações de parâmetro a ser mostrada.

### <a name="example"></a>Exemplo
 Aqui está um exemplo simplificado para detectar os caracteres da lista de parâmetros e definir os gatilhos apropriados. Este exemplo é apenas para fins ilustrativos. Ele pressupõe que o scanner contém um método `GetNextToken` que identifica e retorna tokens de uma linha de texto. O código de exemplo simplesmente define os gatilhos sempre que ele vê o tipo certo de caractere.

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private Lexer lex;
        private const char parameterListStartChar = '(';
        private const char parameterListEndChar   = ')';
        private const char parameterNextChar      = ',';

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char c = token[0];
                if (Char.IsPunctuation(c))
                {
                    tokenInfo.Type = TokenType.Operator;
                    tokenInfo.Color = TokenColor.Keyword;
                    tokenInfo.EndIndex = index;

                    if (c == parameterListStartChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterStart;
                    }
                    else if (c == parameterListNextChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterNext;
                    else if (c == parameterListEndChar)
                    {
                        tokenInfo.Trigger |= TokenTriggers.ParameterEnd;
                    }
                }
            return foundToken;
        }
    }
}
```

## <a name="supporting-the-parameter-info-tooltip-in-the-parser"></a>Dando suporte à dica de ferramenta informações do parâmetro no analisador
 A <xref:Microsoft.VisualStudio.Package.Source> classe faz algumas suposições sobre o conteúdo das <xref:Microsoft.VisualStudio.Package.AuthoringScope> classes e <xref:Microsoft.VisualStudio.Package.AuthoringSink> quando a dica de ferramenta de informações do parâmetro é exibida e atualizada.

- O analisador é fornecido <xref:Microsoft.VisualStudio.Package.ParseReason> quando o caractere inicial da lista de parâmetros é digitado.

- O local fornecido no <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto é imediatamente após o caractere de início da lista de parâmetros. O analisador deve coletar as assinaturas de todas as declarações de método disponíveis nessa posição e armazená-las em uma lista em sua versão do <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto. Essa lista inclui o nome do método, tipo de método (ou tipo de retorno) e uma lista de parâmetros possíveis. Posteriormente, essa lista é pesquisada para a assinatura do método ou assinaturas a serem exibidas na dica de ferramenta informações do parâmetro.

  O analisador deve analisar a linha especificada pelo <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto para reunir o nome do método que está sendo inserido, bem como o quanto ao longo do usuário está digitando parâmetros. Isso é feito passando o nome do método para o <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A> método no <xref:Microsoft.VisualStudio.Package.AuthoringSink> objeto e, em seguida, chamando o <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A> método quando o caractere de início da lista de parâmetros é analisado, chamando o <xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A> método quando o próximo caractere da lista de parâmetros é analisado e, finalmente, chamando o <xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A> método quando o caractere final da lista de parâmetros é analisado. Os resultados dessas chamadas de método são usados pela <xref:Microsoft.VisualStudio.Package.Source> classe para atualizar a dica de ferramenta de informações de parâmetro adequadamente.

### <a name="example"></a>Exemplo
 Aqui está uma linha de texto que o usuário pode inserir. Os números abaixo da linha indicam qual etapa é tomada pelo analisador nessa posição na linha (supondo que a análise se mova da esquerda para a direita). A suposição aqui é que tudo antes da linha já tenha sido analisado para assinaturas de método, incluindo a assinatura do método "testfunc".

```
testfunc("a string",3);
     ^^          ^ ^
     12          3 4
```

 As etapas que o analisador usa são descritas abaixo:

1. O analisador chama <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A> o texto "testfunc".

2. O analisador chama <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A> .

3. O analisador chama <xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A> .

4. O analisador chama <xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A> .
