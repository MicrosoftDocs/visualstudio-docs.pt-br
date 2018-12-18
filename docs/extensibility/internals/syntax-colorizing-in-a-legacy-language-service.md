---
title: Coloração de sintaxe em um serviço de linguagem herdado | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], syntax highlighting
- colorization, supporting in language services [managed package framework]
- syntax highlighting, supporting in language services [managed package framework]
- language services [managed package framework], colorization
ms.assetid: 1ca1736a-f554-42e4-a9c7-fe8c3c1717df
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 1d82a85958fd979a3d9d44375656b08356ef09d9
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31135942"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>Coloração de sintaxe em um serviço de linguagem herdado
Coloração de sintaxe é um recurso que faz com que os elementos de uma linguagem de programação a ser exibido em um arquivo de origem em diferentes cores e estilos. Para dar suporte a esse recurso, você precisa fornecer um analisador ou scanner que pode identificar os tipos de elementos lexicais ou tokens no arquivo. Muitas linguagens de distinguem as palavras-chave, delimitadores (como parênteses ou chaves) e comentários por colori-los de maneiras diferentes.  
  
 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações, consulte [estendendo o Editor e o idioma serviços](../../extensibility/extending-the-editor-and-language-services.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API assim que possível. Isso melhorar o desempenho do seu serviço de linguagem e permitem que você aproveite os novos recursos do editor.  
  
## <a name="implementation"></a>Implementação  
 Para dar suporte a colorização, a estrutura de pacote gerenciado (MPF) inclui o <xref:Microsoft.VisualStudio.Package.Colorizer> de classe que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> interface. Essa classe interage com um <xref:Microsoft.VisualStudio.Package.IScanner> para determinar o token e cores. Para obter mais informações sobre scanners, consulte [analisador de serviço de linguagem herdado e o Scanner](../../extensibility/internals/legacy-language-service-parser-and-scanner.md). O <xref:Microsoft.VisualStudio.Package.Colorizer> classe depois marca cada caractere do token com as informações de cor e retorna essas informações para o editor exibindo o arquivo de origem.  
  
 As informações de cor retornadas para o editor são um índice em uma lista de itens pode ser coloridos. Cada item pode ser colorido Especifica um valor de cor e um conjunto de atributos de fonte, como negrito ou tachado. O editor fornece um conjunto de itens padrão pode ser colorido pode usar o serviço de linguagem. Tudo o que você precisa fazer é especificar o índice de cor apropriado para cada tipo de token. No entanto, você pode fornecer um conjunto de itens pode ser coloridos personalizados e os índices que você fornecer tokens de e fazer referência a sua própria lista de itens pode ser coloridos, em vez de lista padrão. Você também deve definir o `RequestStockColors` entrada do registro para 0 (ou não especifique o `RequestStockColors` entrada em todos os) para dar suporte a cores personalizadas. Você pode definir essa entrada de registro com um parâmetro nomeado para o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> atributo definido pelo usuário. Para obter mais informações sobre como registrar um serviço de linguagem e definir suas opções, consulte [registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md).  
  
## <a name="custom-colorable-items"></a>Itens pode ser coloridos personalizados  
 Para fornecer seus próprios itens pode ser coloridos personalizados, você deve substituir o <xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A> e <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A> método sobre o <xref:Microsoft.VisualStudio.Package.LanguageService> classe. O primeiro método retorna o número de itens pode ser coloridos personalizados que oferece suporte ao seu serviço de linguagem e o segundo obtém o item pode ser colorido personalizado por índice. Criar a lista padrão de itens pode ser coloridos personalizados. No construtor do seu serviço de idioma, tudo o que você precisa fazer é fornecer a cada item pode ser colorido com um nome. O Visual Studio automaticamente trata o caso em que o usuário seleciona um conjunto diferente de itens pode ser coloridos. Esse nome é o que aparece no **fontes e cores** página de propriedade no **opções** caixa de diálogo (disponível no Visual Studio **ferramentas** menu) e esse nome determina quais cor de que um usuário tiver substituído. As opções do usuário são armazenadas em cache no registro e acessadas pelo nome da cor. O **fontes e cores** página de propriedade lista todos os nomes de cor em ordem alfabética, para que você pode agrupar as cores personalizadas, precedendo cada nome de cor com o nome do idioma; por exemplo, "**TestLanguage - comentário**"e"**TestLanguage - palavra-chave**". Ou você pode agrupar os itens pode ser coloridos por tipo, "**comentário (TestLanguage)**"e"**palavra-chave (TestLanguage)**". Agrupar por nome de idioma é preferencial.  
  
> [!CAUTION]
>  É altamente recomendável que você incluir o nome do idioma no nome do item pode ser colorido para evitar colisões com nomes de item pode ser colorido existentes.  
  
> [!NOTE]
>  Se você alterar o nome de uma das suas cores durante o desenvolvimento, você deve redefinir o cache que o Visual Studio criado na primeira vez em que as cores foram acessadas. Você pode fazer isso executando o **redefinir o Hive Experimental** comando no menu de programa do SDK do Visual Studio.  
  
 Observe que o primeiro item na lista de itens pode ser coloridos nunca é referenciado. O Visual Studio fornece sempre as cores padrão de texto e atributos para aquele item. É a maneira mais fácil de lidar com isso fornecer um item pode ser colorido de espaço reservado como o primeiro item.  
  
### <a name="high-color-colorable-items"></a>Itens pode ser colorido High Color  
 Pode ser coloridos itens também podem dar suporte a valores de cor de 24 bits ou alto por meio de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interface. MPF <xref:Microsoft.VisualStudio.Package.ColorableItem> classe oferece suporte a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interface e as cores de 24 bits são especificadas no construtor junto com as cores normais. Consulte o <xref:Microsoft.VisualStudio.Package.ColorableItem> classe para obter mais detalhes. O exemplo a seguir mostra como definir as cores de 24 bits para palavras-chave e comentários. As cores de 24 bits são usadas quando a cor de 24 bits é suportada na área de trabalho do usuário. Caso contrário, são usadas as cores de texto normal.  
  
 Lembre-se de que essas são as cores padrão para sua linguagem. o usuário pode alterar essas cores para que desejarem.  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra uma maneira de declarar e preencher uma matriz de itens pode ser coloridos personalizados usando o <xref:Microsoft.VisualStudio.Package.ColorableItem> classe. Este exemplo define as cores de palavra-chave e comentários usando cores de 24 bits.  
  
```csharp  
using Microsoft.VisualStudio.Package;  
using Microsoft.VisualStudio.TextManager.Interop;  
  
namespace TestLanguagePackage  
{  
    public class TestLanguageService : LanguageService  
    {  
        private ColorableItem[] m_colorableItems;  
  
        TestLanguageService() : base()  
        {  
            m_colorableItems = new ColorableItem[] {  
                new ColorableItem("TestLanguage - Text",  
                                  "Text",  
                                  COLORINDEX.CI_SYSPLAINTEXT_FG,  
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,  
                                  System.Drawing.Color.Empty,  
                                  System.Drawing.Color.Empty,  
                                  FONTFLAGS.FF_DEFAULT),  
                new ColorableItem("TestLanguage - Keyword",  
                                  "Keyword",  
                                  COLORINDEX.CI_MAROON,  
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,  
                                  System.Drawing.Color.FromArgb(192,32,32),  
                                  System.Drawing.Color.Empty,  
                                  FONTFLAGS.FF_BOLD),  
                new ColorableItem("TestLanguage - Comment",  
                                  "Comment",  
                                  COLORINDEX.CI_DARKGREEN,  
                                  COLORINDEX.CI_LIGHTGRAY,  
                                  System.Drawing.Color.FromArgb(32,128,32),  
                                  System.Drawing.Color.Empty,  
                                  FONTFLAGS.FF_DEFAULT)  
                // ...  
                // Add as many colorable items as you want to support.  
            };  
        }  
    }  
}  
```  
  
## <a name="the-colorizer-class-and-the-scanner"></a>A classe colorizador e o mecanismo de varredura  
 A base de <xref:Microsoft.VisualStudio.Package.LanguageService> classe tiver um <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A> método que instantiantes o <xref:Microsoft.VisualStudio.Package.Colorizer> classe. O scanner que é retornado o <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método é passado para o <xref:Microsoft.VisualStudio.Package.Colorizer> construtor de classe.  
  
 Você deve implementar o <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método na sua versão de <xref:Microsoft.VisualStudio.Package.LanguageService> classe. O <xref:Microsoft.VisualStudio.Package.Colorizer> classe usa o scanner para obter todas as informações de token de cor.  
  
 O scanner precisa preencher um <xref:Microsoft.VisualStudio.Package.TokenInfo> estrutura para cada token ele localiza. Essa estrutura contém informações como o alcance o token ocupa, o índice de cor a ser usado, qual é o tipo os gatilhos de tokens e tokens (consulte <xref:Microsoft.VisualStudio.Package.TokenTriggers>). Somente o índice de intervalo e cor são necessários para colorização pela <xref:Microsoft.VisualStudio.Package.Colorizer> classe.  
  
 O índice de cor armazenado na <xref:Microsoft.VisualStudio.Package.TokenInfo> estrutura normalmente é um valor da <xref:Microsoft.VisualStudio.Package.TokenColor> enumeração, que fornece um número de índices nomeados correspondente a vários elementos de linguagem, como palavras-chave e operadores. Se os itens personalizados de pode ser coloridos listam correspondências os itens apresentados a <xref:Microsoft.VisualStudio.Package.TokenColor> enumeração, em seguida, você pode usar apenas a enumeração como a cor para cada token. No entanto, se você tiver itens pode ser coloridos adicionais ou você não deseja usar os valores existentes em ordem, você pode organizar sua lista de itens pode ser colorido personalizados para atender às suas necessidades e retornar o índice apropriado na lista. Apenas certifique-se de converter o índice de um <xref:Microsoft.VisualStudio.Package.TokenColor> quando armazená-los no <xref:Microsoft.VisualStudio.Package.TokenInfo> estrutura; [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] vê somente o índice.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como o scanner pode identificar os três tipos de token: números, pontos e identificadores (tudo o que não é um número ou a pontuação). Este exemplo é apenas para fins ilustrativos e não representa uma implementação de analisador e o scanner abrangente. Ele supõe que haja uma `Lexer` classe com um `GetNextToken()` método que retorna uma cadeia de caracteres.  
  
```csharp  
using Microsoft.VisualStudio.Package;  
using Microsoft.VisualStudio.TextManager.Interop;  
  
namespace TestLanguagePackage  
{  
    private Lexer lex;  
  
    public class TestScanner : IScanner  
    {  
        public bool ScanTokenAndProvideInfoAboutIt(TokenInfo tokenInfo,  
                                                   ref int state)  
        {  
            bool foundToken = false;  
            string token = lex.GetNextToken();  
            if (token != null)  
            {  
                char firstChar = token[0];  
                if (Char.IsPunctuation(firstChar))  
                {  
                    tokenInfo.Type = TokenType.Operator;  
                    tokenInfo.Color = TokenColor.Keyword;  
                }  
                else if (Char.IsNumber(firstChar))  
                {  
                    tokenInfo.Type = TokenType.Literal;  
                    tokenInfo.Color = TokenColor.Number;  
                }  
                else  
                {  
                    tokenInfo.Type = TokenType.Identifier;  
                    tokenInfo.Color = TokenColor.Identifier;  
                }  
            }  
            return foundToken;  
        }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Recursos de serviço de linguagem herdada](../../extensibility/internals/legacy-language-service-features1.md)   
 [O scanner e o analisador de serviço de linguagem herdados](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)   
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)