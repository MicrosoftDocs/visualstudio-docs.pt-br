---
title: Informações de parâmetro em uma função de linguagem herdado2 | Microsoft Docs
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
- IntelliSense, Parameter Info tool tip
- language services [managed package framework], IntelliSense Parameter Info
- Parameter Info (IntelliSense), supporting in language services [managed package framework]
ms.assetid: a117365d-320d-4bb5-b61d-3e6457b8f6bc
caps.latest.revision: 24
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: a540a2e5b282e1242109edd67a5dfbc95067e183
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781316"
---
# <a name="parameter-info-in-a-legacy-language-service"></a>Informações de parâmetro em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Informações de parâmetro do IntelliSense é uma dica de ferramenta que exibe a assinatura de um método quando o usuário digita a lista de parâmetros iniciar caractere (normalmente um parêntese de abertura) para a lista de parâmetros de método. Como cada parâmetro for inserido e o separador de parâmetro (geralmente uma vírgula) é digitado, a dica de ferramenta é atualizada para mostrar o próximo parâmetro em negrito.  
  
 As classes do framework (MPF) de pacote gerenciado dão suporte para gerenciar a dica de ferramenta de informações do parâmetro. O analisador deve detectar parâmetro inicia parâmetro em seguida, e os caracteres de final do parâmetro e ele devem fornecer uma lista de assinaturas de método e seus parâmetros associados.  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações, consulte [estender o Editor e os serviços de linguagem](../../extensibility/extending-the-editor-and-language-services.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
## <a name="implementation"></a>Implementação  
 O analisador deve definir o valor de gatilho <xref:Microsoft.VisualStudio.Package.TokenTriggers> é definido quando ele encontra um caractere de início de lista de parâmetro (geralmente um parêntese de abertura). Ele deve ser definido um <xref:Microsoft.VisualStudio.Package.TokenTriggers> disparar quando ele encontra um separador de parâmetro (geralmente uma vírgula). Isso faz com que uma dica de ferramenta de informações do parâmetro a ser atualizado e mostrar o próximo parâmetro em negrito. O analisador deve definir o valor de gatilho <xref:Microsoft.VisualStudio.Package.TokenTriggers> quando se encontra o caractere de final de lista de parâmetro (geralmente um parêntese de fechamento).  
  
 O <xref:Microsoft.VisualStudio.Package.TokenTriggers> valor de gatilho inicia uma chamada para o <xref:Microsoft.VisualStudio.Package.Source.MethodTip%2A> método, que por sua vez chama o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> analisador de método com um motivo de análise de <xref:Microsoft.VisualStudio.Package.ParseReason>. Se o analisador determina se o identificador antes de começar a lista de parâmetros de caractere é um nome de método reconhecido, ele retorna uma lista de assinaturas de método em correspondentes a <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto. Se forem encontradas quaisquer assinaturas de método, a dica de ferramenta de informações do parâmetro é exibida com a primeira assinatura na lista. Esta dica de ferramenta, em seguida, é atualizada conforme mais da assinatura é digitado. Quando o caractere de final de lista de parâmetro é digitado, a dica de ferramenta de informações do parâmetro é removida do modo de exibição.  
  
> [!NOTE]
>  Para garantir que a dica de ferramenta de informações do parâmetro está formatada corretamente, você deve substituir as propriedades no <xref:Microsoft.VisualStudio.Package.Methods> classe para fornecer os caracteres apropriados. A base <xref:Microsoft.VisualStudio.Package.Methods> pressupõe que a classe c# – assinatura do método de estilo. Consulte o <xref:Microsoft.VisualStudio.Package.Methods> classe para obter detalhes sobre como isso pode ser feito.  
  
## <a name="enabling-support-for-the-parameter-info"></a>Habilitando o suporte para as informações de parâmetro  
 Para dar suporte a dicas de ferramenta de informações do parâmetro, você deve definir a `ShowCompletion` chamado parâmetro do <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> para `true`. O serviço de linguagem lê o valor desta entrada de registro do <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> propriedade.  
  
 Além disso, o <xref:Microsoft.VisualStudio.Package.LanguagePreferences.ParameterInformation%2A> propriedade deve ser definida como `true` para a dica de ferramenta de informações do parâmetro a ser mostrado.  
  
### <a name="example"></a>Exemplo  
 Aqui está um exemplo simplificado de detectar os caracteres da lista de parâmetro e definir os gatilhos apropriados. Este exemplo é apenas para fins ilustrativos. Ele pressupõe que o scanner contém um método `GetNextToken` que identifica e retorna os tokens de uma linha de texto. O exemplo de código simplesmente define os disparadores sempre que ele vê o tipo certo de caractere.  
  
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
  
## <a name="supporting-the-parameter-info-tooltip-in-the-parser"></a>A dica de ferramenta de informações do parâmetro de suporte no analisador  
 O <xref:Microsoft.VisualStudio.Package.Source> classe faz algumas suposições sobre o conteúdo do <xref:Microsoft.VisualStudio.Package.AuthoringScope> e <xref:Microsoft.VisualStudio.Package.AuthoringSink> classes quando a dica de ferramenta de informações do parâmetro é exibida e atualizada.  
  
- O analisador é dada <xref:Microsoft.VisualStudio.Package.ParseReason> quando o caractere de início da lista de parâmetro é digitado.  
  
- O local fornecido <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto é imediatamente após o caractere inicial de lista de parâmetros. O analisador deve coletar as assinaturas de todas as declarações de método disponíveis em posicionar e armazená-los em uma lista em sua versão do <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto. Essa lista inclui o nome do método, método tipo (ou no tipo de retorno) e uma lista de parâmetros possíveis. Essa lista é pesquisada posteriormente para a assinatura do método ou assinaturas para exibir na dica de ferramenta informações do parâmetro.  
  
  O analisador, em seguida, deve analisar a linha especificada pelo <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto para coletar o nome do método que está sendo inserido, bem como a distância ao longo do usuário é digitar os parâmetros. Isso é feito ao passar o nome do método a ser o <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A> método na <xref:Microsoft.VisualStudio.Package.AuthoringSink> objeto e, em seguida, chamar o <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A> método quando o caractere inicial de lista de parâmetros é analisado, chamar o <xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A> método quando a lista de parâmetros próximo caractere é analisado e, finalmente, a chamada a <xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A> método quando o caractere de final de lista de parâmetro é analisado. Os resultados dessas chamadas de método são usados pelo <xref:Microsoft.VisualStudio.Package.Source> classe para atualizar a dica de ferramenta de informações do parâmetro adequadamente.  
  
### <a name="example"></a>Exemplo  
 Aqui está uma linha de texto que o usuário pode inserir. Os números abaixo da linha indicam qual etapa é obtida pelo analisador nessa posição na linha (supondo que a análise se move da esquerda para a direita). A suposição aqui é que tudo antes da linha já foi analisado para assinaturas de método, incluindo a assinatura do método "testfunc".  
  
```  
testfunc("a string",3);  
     ^^          ^ ^  
     12          3 4  
```  
  
 As etapas que usa o analisador são descritas abaixo:  
  
1.  As chamadas de analisador <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartName%2A> com o texto "testfunc".  
  
2.  As chamadas de analisador <xref:Microsoft.VisualStudio.Package.AuthoringSink.StartParameters%2A>.  
  
3.  As chamadas de analisador <xref:Microsoft.VisualStudio.Package.AuthoringSink.NextParameter%2A>.  
  
4.  As chamadas de analisador <xref:Microsoft.VisualStudio.Package.AuthoringSink.EndParameters%2A>.

