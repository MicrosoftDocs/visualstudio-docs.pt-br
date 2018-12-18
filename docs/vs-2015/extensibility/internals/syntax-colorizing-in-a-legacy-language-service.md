---
title: Coloração de sintaxe em um serviço de linguagem herdado | Microsoft Docs
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
- language services [managed package framework], syntax highlighting
- colorization, supporting in language services [managed package framework]
- syntax highlighting, supporting in language services [managed package framework]
- language services [managed package framework], colorization
ms.assetid: 1ca1736a-f554-42e4-a9c7-fe8c3c1717df
caps.latest.revision: 29
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 20655534439fa187488087e1ae819a7ffca4c27a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730279"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>Coloração de sintaxe em um serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Colorização de sintaxe é um recurso que faz com que os diferentes elementos de uma linguagem de programação a ser exibido em um arquivo de origem em diferentes cores e estilos. Para dar suporte a esse recurso, você precisa fornecer um analisador ou um scanner que pode identificar os tipos de elementos léxicos ou tokens no arquivo. Muitas linguagens de distinguir as palavras-chave, delimitadores (por exemplo, parênteses ou chaves) e comentários por colori-los de maneiras diferentes.  
  
 Serviços de linguagem herdado são implementados como parte de um VSPackage, mas a maneira mais recente para implementar recursos de serviço de linguagem é usar extensões MEF. Para obter mais informações, consulte [estender o Editor e os serviços de linguagem](../../extensibility/extending-the-editor-and-language-services.md).  
  
> [!NOTE]
>  É recomendável que você comece a usar o novo editor de API mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitem que você tirar proveito dos novos recursos do editor.  
  
## <a name="implementation"></a>Implementação  
 Para dar suporte a colorização, a estrutura de pacote gerenciado (MPF) inclui o <xref:Microsoft.VisualStudio.Package.Colorizer> de classe que implementa o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> interface. Essa classe interage com um <xref:Microsoft.VisualStudio.Package.IScanner> para determinar o token e cores. Para obter mais informações sobre scanners, consulte [analisador de serviço de linguagem herdado e o Scanner](../../extensibility/internals/legacy-language-service-parser-and-scanner.md). O <xref:Microsoft.VisualStudio.Package.Colorizer> classe, em seguida, cada caractere do token com as informações de cores de marca e retorna essas informações para o editor exibindo o arquivo de origem.  
  
 As informações de cores retornadas para o editor são um índice em uma lista de itens de coloração. Cada item que pode ser colorido Especifica um valor de cor e um conjunto de atributos de fonte, como negrito ou tachado. O editor fornece um conjunto de itens de coloração padrão que pode usar o seu serviço de linguagem. Tudo o que você precisa fazer é especificar o índice de cor apropriado para cada tipo de token. No entanto, você pode fornecer um conjunto de itens de coloração personalizados e os índices que você fornecer para tokens e sua própria lista de itens de coloração, em vez de lista padrão de referência. Você também deve definir a `RequestStockColors` entrada de registro como 0 (ou não especifique o `RequestStockColors` entrada em todos os) para dar suporte a cores personalizadas. Você pode definir essa entrada de registro com um parâmetro nomeado para o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> atributo definido pelo usuário. Para obter mais informações sobre como registrar um serviço de linguagem e definir suas opções, consulte [registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md).  
  
## <a name="custom-colorable-items"></a>Itens personalizados que podem ser coloridos  
 Para fornecer seus próprios itens de coloração personalizados, você deve substituir a <xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A> e <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A> método o <xref:Microsoft.VisualStudio.Package.LanguageService> classe. O primeiro método retorna o número de itens de coloração personalizados que dá suporte a seu serviço de linguagem e a segunda obtém o item de coloração personalizado por índice. Você criar a lista padrão de itens de coloração personalizados. No construtor do seu serviço de linguagem, tudo o que você precisa fazer é fornecer a cada item que pode ser colorido com um nome. Visual Studio identifica automaticamente o caso em que o usuário seleciona um conjunto de itens de coloração diferente. Esse nome é o que aparece na **fontes e cores** página de propriedades na **opções** caixa de diálogo (disponível no Visual Studio **ferramentas** menu) e determina a quais esse nome cor de que um usuário tiver substituído. As opções do usuário são armazenadas em cache no registro e acessadas pelo nome de cor. O **fontes e cores** página de propriedades lista todos os nomes de cor em ordem alfabética, portanto, você pode agrupar suas cores personalizadas, precedendo cada nome de cor com seu nome de idioma; por exemplo, "**TestLanguage - comentário**"e"**TestLanguage - palavra-chave**". Ou você pode agrupar seu itens de coloração por tipo, "**comentário (TestLanguage)**"e"**palavra-chave (TestLanguage)**". O agrupamento por nome de idioma é preferencial.  
  
> [!CAUTION]
>  É altamente recomendável que você inclua o nome do idioma no nome do item que pode ser colorido para evitar colisões com nomes existentes de item que pode ser colorido.  
  
> [!NOTE]
>  Se você alterar o nome de uma das suas cores durante o desenvolvimento, você deve redefinir o cache que o Visual Studio criado na primeira vez em que suas cores foram acessadas. Você pode fazer isso executando o **redefinir o Hive Experimental** comando no menu de programa do SDK do Visual Studio.  
  
 Observe que o primeiro item na sua lista de itens de coloração nunca é referenciado. O Visual Studio sempre fornece a cores de texto padrão e os atributos para aquele item. A maneira mais fácil de lidar com isso é fornecer um item que pode ser colorido de espaço reservado como o primeiro item.  
  
### <a name="high-color-colorable-items"></a>Itens de coloração High Color  
 Itens de coloração também pode dar suporte a valores de cor de 24 bits ou alta por meio de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interface. MPF <xref:Microsoft.VisualStudio.Package.ColorableItem> classe oferece suporte a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interface e as cores de 24 bits são especificadas no construtor junto com as cores normais. Consulte o <xref:Microsoft.VisualStudio.Package.ColorableItem> classe para obter mais detalhes. O exemplo a seguir mostra como definir as cores de 24 bits para palavras-chave e comentários. As cores de 24 bits são usadas quando a cor de 24 bits é suportada na área de trabalho do usuário; Caso contrário, as cores do texto normais são usadas.  
  
 Lembre-se de que essas são as cores padrão para sua linguagem; o usuário pode alterar essas cores como desejarem.  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra uma maneira de declarar e preencher uma matriz de itens de coloração personalizados usando o <xref:Microsoft.VisualStudio.Package.ColorableItem> classe. Este exemplo define as cores de palavra-chave e o comentário usando cores de 24 bits.  
  
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
                new ColorableItem("TestLanguage – Text",  
                                  "Text",  
                                  COLORINDEX.CI_SYSPLAINTEXT_FG,  
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,  
                                  System.Drawing.Color.Empty,  
                                  System.Drawing.Color.Empty,  
                                  FONTFLAGS.FF_DEFAULT),  
                new ColorableItem("TestLanguage – Keyword",  
                                  "Keyword",  
                                  COLORINDEX.CI_MAROON,  
                                  COLORINDEX.CI_SYSPLAINTEXT_BK,  
                                  System.Drawing.Color.FromArgb(192,32,32),  
                                  System.Drawing.Color.Empty,  
                                  FONTFLAGS.FF_BOLD),  
                new ColorableItem("TestLanguage – Comment",  
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
  
## <a name="the-colorizer-class-and-the-scanner"></a>A classe colorizador e varredura  
 A base <xref:Microsoft.VisualStudio.Package.LanguageService> classe tem um <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A> método que instantiantes o <xref:Microsoft.VisualStudio.Package.Colorizer> classe. O scanner que é retornado a <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método é passado para o <xref:Microsoft.VisualStudio.Package.Colorizer> construtor de classe.  
  
 Você deve implementar o <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método em sua própria versão do <xref:Microsoft.VisualStudio.Package.LanguageService> classe. O <xref:Microsoft.VisualStudio.Package.Colorizer> classe usa o scanner para obter todas as informações de cores de token.  
  
 O scanner precisa popular um <xref:Microsoft.VisualStudio.Package.TokenInfo> de estrutura para todos os tokens ele localiza. Essa estrutura contém informações como o alcance o token ocupa, o índice de cores a ser usado, qual é o tipo os gatilhos de token e o token (consulte <xref:Microsoft.VisualStudio.Package.TokenTriggers>). Somente o índice de intervalo e a cor são necessários para colorização pelo <xref:Microsoft.VisualStudio.Package.Colorizer> classe.  
  
 O índice de cor armazenado na <xref:Microsoft.VisualStudio.Package.TokenInfo> estrutura normalmente é um valor da <xref:Microsoft.VisualStudio.Package.TokenColor> enumeração, que fornece um número de índices nomeados correspondentes a vários elementos de linguagem, como operadores e palavras-chave. Se seus itens de coloração personalizados correspondências de listar os itens apresentados no <xref:Microsoft.VisualStudio.Package.TokenColor> enumeração, em seguida, você pode simplesmente usar a enumeração como a cor para cada token. No entanto, se você tiver itens de coloração adicionais ou você não deseja usar os valores existentes nessa ordem, você pode organizar sua lista de itens de coloração personalizados para atender às suas necessidades e retornar o índice apropriado para essa lista. Apenas certifique-se de converter o índice para uma <xref:Microsoft.VisualStudio.Package.TokenColor> quando armazená-los no <xref:Microsoft.VisualStudio.Package.TokenInfo> estrutura; [!INCLUDE[vs_current_short](../../includes/vs-current-short-md.md)] vê apenas o índice.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como o scanner pode identificar os três tipos de token: números, pontuação e identificadores (tudo o que não é um número ou a pontuação). Este exemplo é apenas para fins ilustrativos e não representa uma implementação de analisador e scanner abrangente. Ele supõe que haja uma `Lexer` classe com um `GetNextToken()` método que retorna uma cadeia de caracteres.  
  
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
 [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)   
 [Scanner e analisador de serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)   
 [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)

