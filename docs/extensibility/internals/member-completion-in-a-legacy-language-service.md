---
title: Conclusão de membro em um serviço de linguagem herdada | Microsoft Docs
description: Saiba como a dica da ferramenta de conclusão de membros do IntelliSense funciona em um serviço de linguagem herdado e como ele é compatível com o MPF (estrutura de pacote gerenciado).
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- IntelliSense, Member Completion tool tip
- Member Completion, supporting in language services [managed package framework]
- language services [managed package framework], IntelliSense Member Completion
ms.assetid: 500f718d-9028-49a4-8615-ba95cf47fc52
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5279b3a96cb9658b968a5d51bbd8b1c2a41862b6
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105095128"
---
# <a name="member-completion-in-a-legacy-language-service"></a>Preenchimento de membro em um serviço de linguagem herdado

A conclusão do membro do IntelliSense é uma dica de ferramenta que exibe uma lista de possíveis membros de um escopo específico, como uma classe, estrutura, enumeração ou namespace. Por exemplo, em C#, se o usuário digitar "This" seguido por um ponto, uma lista de todos os membros da classe ou da estrutura no escopo atual será apresentada em uma lista da qual o usuário pode selecionar.

A MPF (estrutura de pacote gerenciada) fornece suporte para a dica de ferramenta e gerenciamento da lista na dica de ferramenta; Tudo o que é necessário é a cooperação do analisador para fornecer os dados que aparecem na lista.

Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para obter mais informações, consulte [estendendo o editor e os serviços de linguagem](../../extensibility/extending-the-editor-and-language-services.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="how-it-works"></a>Como funciona

A seguir estão as duas maneiras nas quais uma lista de membros é mostrada usando as classes do MPF:

- Posicionando o cursor em um identificador ou depois de um caractere de conclusão de membro e selecionando **listar Membros** no menu do **IntelliSense** .

- O <xref:Microsoft.VisualStudio.Package.IScanner> Verificador detecta um caractere de conclusão de membro e define um gatilho de token de [TokenTriggers. MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) para esse caractere.

Um caractere de conclusão de membro indica que um membro de uma classe, estrutura ou enumeração deve ser seguido. Por exemplo, em C# ou Visual Basic o caractere de conclusão de membro é um `.` , enquanto em C++, o caractere é um `.` ou um `->` . O valor do gatilho é definido quando o caractere de seleção de membro é verificado.

### <a name="the-intellisense-member-list-command"></a>O comando de lista de membros do IntelliSense

O <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> comando inicia uma chamada para o <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> método na <xref:Microsoft.VisualStudio.Package.Source> classe e o <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> método, por sua vez, chama o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> analisador de método com o motivo da análise de [ParseReason. DisplayMemberList](<xref:Microsoft.VisualStudio.Package.ParseReason.DisplayMemberList>).

O analisador determina o contexto da posição atual, bem como o token sob ou imediatamente antes da posição atual. Com base nesse token, uma lista de declarações é apresentada. Por exemplo, em C#, se você posicionar o cursor em um membro de classe e selecionar **membros da lista**, obterá uma lista de todos os membros da classe. Se você posicionar o cursor após um período que segue uma variável de objeto, obterá uma lista de todos os membros da classe que o objeto representa. Observe que, se o cursor estiver posicionado em um membro quando a lista de membros for mostrada, a seleção de um membro da lista substituirá o membro em que o cursor está ligado com aquele na lista.

### <a name="the-token-trigger"></a>O gatilho de token

O gatilho [TokenTriggers. MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) inicia uma chamada para o <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> método na <xref:Microsoft.VisualStudio.Package.Source> classe e o <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> método, por sua vez, chama o analisador com o motivo da análise de [ParseReason. MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>). Se o gatilho de token também incluir o sinalizador [TokenTriggers. MatchBraces](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MatchBraces>) , o motivo da análise será [ParseReason. MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>), que combina a seleção de membros e o realce de chaves.

O analisador determina o contexto da posição atual, bem como o que foi digitado antes do caractere de seleção de membro. A partir dessas informações, o analisador cria uma lista de todos os membros do escopo solicitado. Essa lista de declarações é armazenada no <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto retornado do <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método. Se qualquer declaração for retornada, a dica de ferramenta de conclusão do membro será exibida. A dica de ferramenta é gerenciada por uma instância da <xref:Microsoft.VisualStudio.Package.CompletionSet> classe.

## <a name="enable-support-for-member-completion"></a>Habilitar suporte para conclusão de membro

Você deve ter a `CodeSense` entrada do registro definida como 1 para dar suporte a qualquer operação do IntelliSense. Essa entrada de registro pode ser definida com um parâmetro nomeado passado para o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> atributo de usuário associado ao pacote de idioma. As classes de serviço de linguagem lêem o valor dessa entrada de registro da <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> Propriedade na <xref:Microsoft.VisualStudio.Package.LanguagePreferences> classe.

Se o scanner retornar o gatilho de token de [TokenTriggers. MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>)e o analisador retornar uma lista de declarações, a lista de conclusão de membros será exibida.

## <a name="support-member-completion-in-the-scanner"></a>Suporte para conclusão de membro no scanner

O scanner deve ser capaz de detectar um caractere de conclusão de membro e definir o gatilho de token de [TokenTriggers. MemberSelect](<xref:Microsoft.VisualStudio.Package.TokenTriggers.MemberSelect>) quando esse caractere é analisado.

### <a name="scanner-example"></a>Exemplo de scanner

Veja um exemplo simplificado de como detectar o caractere de conclusão do membro e definir o <xref:Microsoft.VisualStudio.Package.TokenTriggers> sinalizador apropriado. Este exemplo é apenas para fins ilustrativos. Ele pressupõe que o scanner contém um método `GetNextToken` que identifica e retorna tokens de uma linha de texto. O código de exemplo simplesmente define o gatilho sempre que vê o tipo certo de caractere.

```csharp
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    public class TestScanner : IScanner
    {
        private Lexer lex;
        private const char memberSelectChar = '.';

        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,
                                                   ref int state)
        {
            bool foundToken = false
            string token = lex.GetNextToken();
            if (token != null)
            {
                foundToken = true;
                char c = token[0];
                if (c == memberSelectChar)
                {
                        tokenInfo.Trigger |= TokenTriggers.MemberSelect;
                }
            }
            return foundToken;
        }
    }
}
```

## <a name="support-member-completion-in-the-parser"></a>Suporte para conclusão de membro no analisador

Para a conclusão do membro, a <xref:Microsoft.VisualStudio.Package.Source> classe chama o <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> método. Você deve implementar a lista em uma classe derivada da <xref:Microsoft.VisualStudio.Package.Declarations> classe. Consulte a <xref:Microsoft.VisualStudio.Package.Declarations> classe para obter detalhes sobre os métodos que você deve implementar.

O analisador é chamado com [ParseReason. MemberSelect](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelect>) ou [ParseReason. MemberSelectAndHighlightBraces](<xref:Microsoft.VisualStudio.Package.ParseReason.MemberSelectAndHighlightBraces>) quando um caractere de seleção de membro é digitado. O local fornecido no <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto é imediatamente após o caractere de seleção de membro. O analisador deve coletar os nomes de todos os membros que podem aparecer em uma lista de membros naquele ponto específico no código-fonte. Em seguida, o analisador deve analisar a linha atual para determinar o escopo que o usuário deseja associar ao caractere de seleção de membro.

Esse escopo se baseia no tipo do identificador antes do caractere de seleção de membro. Por exemplo, em C#, dada a variável `languageService` de membro que tem um tipo de `LanguageService` , digitando **languageService.** produz uma lista de todos os membros da `LanguageService` classe. Também em C#, digitando **isso.** produz uma lista de todos os membros da classe no escopo atual.

### <a name="parser-example"></a>Exemplo do analisador

O exemplo a seguir mostra uma maneira de preencher uma <xref:Microsoft.VisualStudio.Package.Declarations> lista. Esse código pressupõe que o analisador construa uma declaração e a adiciona à lista chamando um `AddDeclaration` método na `TestAuthoringScope` classe.

```csharp
using System.Collections;
using Microsoft.VisualStudio.Package;
using Microsoft.VisualStudio.TextManager.Interop;

namespace TestLanguagePackage
{
    internal class TestDeclaration
    {
        public string Name;            // Name of declaration
        public int     TypeImageIndex; // Glyph index
        public string Description;     // Description of declaration

        public TestDeclaration(string name, int typeImageIndex, string description)
        {
            this.Name = name;
            this.TypeImageIndex = typeImageIndex;
            this.Description = description;
        }
    }

    //===================================================
    internal class TestDeclarations : Declarations
    {
        private ArrayList declarations;

        public TestDeclarations()
            : base()
        {
            declarations = new ArrayList();
        }

        public void AddDeclaration(TestDeclaration declaration)
        {
            declarations.Add(declaration);
        }

        //////////////////////////////////////////////////////////////////////
        // Declarations of class methods that must be implemented.
        public override int GetCount()
        {
            // Return the number of declarations to show.
            return declarations.Count;
        }

        public override string GetDescription(int index)
        {
            // Return the description of the specified item.
            string description = "";
            if (index >= 0 && index < declarations.Count)
            {
                description = ((TestDeclaration)declarations[index]).Description;
            }
            return description;
        }

        public override string GetDisplayText(int index)
        {
            // Determine what is displayed in the tool tip list.
            string text = null;
            if (index >= 0 && index < declarations.Count)
            {
                text = ((TestDeclaration)declarations[index]).Name;
            }
            return text;
        }

        public override int GetGlyph(int index)
        {
            // Return index of image to display next to the display text.
            int imageIndex = -1;
            if (index >= 0 && index < declarations.Count)
            {
                imageIndex = ((TestDeclaration)declarations[index]).TypeImageIndex;
            }
            return imageIndex;
        }

        public override string GetName(int index)
        {
            string name = null;
            if (index >= 0 && index < declarations.Count)
            {
                name = ((TestDeclaration)declarations[index]).Name;
            }
            return name;
        }
    }

    //===================================================
    public class TestAuthoringScope : AuthoringScope
    {
        private TestDeclarations declarationsList;

        public void AddDeclaration(TestDeclaration declaration)
        {
            if (declaration != null)
            {
                if (declarationsList == null)
                {
                    declarationsList = new TestDeclarations();
                }
                declarationsList.AddDeclaration(declaration);
            }
        }

        public override Declarations GetDeclarations(IVsTextView view,
                                                     int line,
                                                     int col,
                                                     TokenInfo info,
                                                     ParseReason reason)
        {
            return declarationsList;
        }

        /////////////////////////////////////////////////
        // Remainder of AuthoringScope methods not shown.
        /////////////////////////////////////////////////
    }

    //===================================================
    class TestLanguageService : LanguageService
    {
        public override AuthoringScope ParseSource(ParseRequest req)
        {
            TestAuthoringScope scope = new TestAuthoringScope();
            if (req.Reason == ParseReason.MemberSelect ||
                req.Reason == ParseReason.MemberSelectAndHighlightBraces)
            {
                // Gather list of declarations based on what the user
                // has typed so far. In this example, this list is an array of
                // MemberDeclaration objects (a helper class you might implement
                // to hold member declarations).
                // How this list is gathered is dependent on the parser
                // and is not shown here.
                MemberDeclarations memberDeclarations;
                memberDeclarations = GetDeclarationsForScope();

                // Now populate the Declarations list in the authoring scope.
                // GetImageIndexBasedOnType() is a helper method you
                // might implement to convert a member type to an index into
                // the image list returned from the language service.
                foreach (MemberDeclaration dec in memberDeclarations)
                {
                    scope.AddDeclaration(new TestDeclaration(
                                             dec.Name,
                                             GetImageIndexBasedOnType(dec.Type),
                                             dec.Description));
                }
            }
            return scope;
        }
    }
}
```
