---
title: Coloração de sintaxe em um serviço de linguagem herdada | Microsoft Docs
description: Saiba como dar suporte à colorização de sintaxe em um serviço de linguagem herdado fornecendo um analisador ou um scanner que possa identificar os tipos de elementos léxicos ou tokens.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], syntax highlighting
- colorization, supporting in language services [managed package framework]
- syntax highlighting, supporting in language services [managed package framework]
- language services [managed package framework], colorization
ms.assetid: 1ca1736a-f554-42e4-a9c7-fe8c3c1717df
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 627c0b5184588f77188928b6355a9034a3a3465e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105080538"
---
# <a name="syntax-colorizing-in-a-legacy-language-service"></a>Coloração de sintaxe em um serviço de linguagem herdado
A colorização de sintaxe é um recurso que faz com que diferentes elementos de uma linguagem de programação sejam exibidos em um arquivo de origem em diferentes cores e estilos. Para dar suporte a esse recurso, você precisa fornecer um analisador ou scanner que possa identificar os tipos de elementos léxicos ou tokens no arquivo. Muitas linguagens distinguem palavras-chave, delimitadores (como parênteses ou chaves) e comentários, colorando-as de maneiras diferentes.

 Os serviços de idioma herdados são implementados como parte de um VSPackage, mas a maneira mais recente de implementar recursos de serviço de linguagem é usar extensões de MEF. Para obter mais informações, consulte [estendendo o editor e os serviços de linguagem](../../extensibility/extending-the-editor-and-language-services.md).

> [!NOTE]
> Recomendamos que você comece a usar a nova API do editor o mais rápido possível. Isso melhorará o desempenho do seu serviço de linguagem e permitirá que você aproveite os novos recursos do editor.

## <a name="implementation"></a>Implementação
 Para dar suporte à colorização, a MPF (estrutura de pacote gerenciada) inclui a <xref:Microsoft.VisualStudio.Package.Colorizer> classe, que implementa a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsColorizer> interface. Essa classe interage com um <xref:Microsoft.VisualStudio.Package.IScanner> para determinar o token e as cores. Para obter mais informações sobre scanners, consulte [analisador e verificador de serviço de idioma herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md). <xref:Microsoft.VisualStudio.Package.Colorizer>Em seguida, a classe marca cada caractere do token com as informações de cor e retorna essas informações para o editor que exibe o arquivo de origem.

 As informações de cor retornadas ao editor são um índice em uma lista de itens coloráveis. Cada item com cores especifica um valor de cor e um conjunto de atributos de fonte, como negrito ou tachado. O Editor fornece um conjunto de itens coloráveis padrão que seu serviço de idioma pode usar. Tudo o que você precisa fazer é especificar o índice de cor apropriado para cada tipo de token. No entanto, você pode fornecer um conjunto de itens personalizáveis personalizados e os índices fornecidos para tokens e referenciar sua própria lista de itens coloráveis em vez da lista padrão. Você também deve definir a `RequestStockColors` entrada do registro como 0 (ou não especificar a `RequestStockColors` entrada) para dar suporte a cores personalizadas. Você pode definir essa entrada de registro com um parâmetro nomeado para o <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> atributo definido pelo usuário. Para obter mais informações sobre como registrar um serviço de linguagem e definir suas opções, consulte [registrando um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md).

## <a name="custom-colorable-items"></a>Itens personalizados que podem ser coloridos
 Para fornecer seus próprios itens coloridos personalizados, você deve substituir o <xref:Microsoft.VisualStudio.Package.LanguageService.GetItemCount%2A> método e <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorableItem%2A> na <xref:Microsoft.VisualStudio.Package.LanguageService> classe. O primeiro método retorna o número de itens colorable personalizados que o serviço de linguagem suporta e o segundo Obtém o item Colorable personalizado por índice. Você cria a lista padrão de itens colorable personalizados. No construtor do seu serviço de idioma, tudo o que você precisa fazer é fornecer a cada item colorável um nome. O Visual Studio manipula automaticamente o caso em que o usuário seleciona um conjunto diferente de itens coloráveis. Esse nome é o que aparece na página de propriedades **fontes e cores** da caixa de diálogo **Opções** (disponível no menu **ferramentas** do Visual Studio) e esse nome determina qual cor um usuário substituiu. As opções do usuário são armazenadas em um cache no registro e acessadas pelo nome da cor. A página de propriedades **fontes e cores** lista todos os nomes de cor em ordem alfabética, para que você possa agrupar suas cores personalizadas precedendo cada nome de cor com o nome do idioma; por exemplo, "**TestLanguage-comment**" e "**TestLanguage-keyword**". Ou você pode agrupar seus itens coloráveis por tipo, "**Comment (TestLanguage)**" e "**Keyword (TestLanguage)**". O agrupamento por nome de idioma é preferencial.

> [!CAUTION]
> É altamente recomendável que você inclua o nome do idioma no nome do item Colorable para evitar colisões com nomes de item Colorable existentes.

> [!NOTE]
> Se você alterar o nome de uma de suas cores durante o desenvolvimento, deverá redefinir o cache que o Visual Studio criou na primeira vez em que suas cores foram acessadas. Você pode fazer isso executando o comando **redefinir o hive experimental** no menu do programa SDK do Visual Studio.

 Observe que o primeiro item na lista de itens coloráveis nunca é referenciado. O Visual Studio sempre fornece os atributos e as cores de texto padrão para esse item. A maneira mais fácil de lidar com isso é fornecer um item de espaço reservado em cores como o primeiro item.

### <a name="high-color-colorable-items"></a>Itens colorable de alta cor
 Itens coloráveis também podem oferecer suporte a valores de 24 bits ou de cor alta por meio da <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interface. A <xref:Microsoft.VisualStudio.Package.ColorableItem> classe MPF dá suporte à <xref:Microsoft.VisualStudio.TextManager.Interop.IVsHiColorItem> interface e as cores de 24 bits são especificadas no Construtor junto com as cores normais. Consulte a <xref:Microsoft.VisualStudio.Package.ColorableItem> classe para obter mais detalhes. O exemplo a seguir mostra como definir as cores de 24 bits para palavras-chave e comentários. As cores de 24 bits são usadas quando há suporte para cores de 24 bits na área de trabalho do usuário; caso contrário, as cores de texto normais serão usadas.

 Lembre-se de que essas são as cores padrão para seu idioma; o usuário pode alterar essas cores para tudo o que quiser.

### <a name="example"></a>Exemplo
 Este exemplo mostra uma maneira de declarar e popular uma matriz de itens colorable personalizados usando a <xref:Microsoft.VisualStudio.Package.ColorableItem> classe. Este exemplo define a palavra-chave e as cores de comentário usando cores de 24 bits.

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

## <a name="the-colorizer-class-and-the-scanner"></a>A classe Colorizer e o scanner
 A <xref:Microsoft.VisualStudio.Package.LanguageService> classe base tem um <xref:Microsoft.VisualStudio.Package.LanguageService.GetColorizer%2A> método que instantiantes a <xref:Microsoft.VisualStudio.Package.Colorizer> classe. O verificador retornado do <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método é passado para o construtor da <xref:Microsoft.VisualStudio.Package.Colorizer> classe.

 Você deve implementar o <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método em sua própria versão da <xref:Microsoft.VisualStudio.Package.LanguageService> classe. A <xref:Microsoft.VisualStudio.Package.Colorizer> classe usa o verificador para obter todas as informações de cores de token.

 O verificador precisa preencher uma <xref:Microsoft.VisualStudio.Package.TokenInfo> estrutura para cada token encontrado. Essa estrutura contém informações como o span que o token ocupa, o índice de cores a ser usado, qual tipo é o token e gatilhos de token (consulte <xref:Microsoft.VisualStudio.Package.TokenTriggers> ). Somente o índice de intervalo e de cores é necessário para a colorização pela <xref:Microsoft.VisualStudio.Package.Colorizer> classe.

 O índice de cores armazenado na <xref:Microsoft.VisualStudio.Package.TokenInfo> estrutura normalmente é um valor da <xref:Microsoft.VisualStudio.Package.TokenColor> enumeração, que fornece vários índices nomeados correspondentes a vários elementos de linguagem, como palavras-chave e operadores. Se sua lista de itens colorable personalizados corresponder aos itens apresentados na <xref:Microsoft.VisualStudio.Package.TokenColor> enumeração, você poderá simplesmente usar a enumeração como a cor de cada token. No entanto, se você tiver itens coloráveis adicionais ou não quiser usar os valores existentes nessa ordem, poderá organizar sua lista de itens colorable personalizados para atender às suas necessidades e retornar o índice apropriado para essa lista. Apenas certifique-se de converter o índice em um <xref:Microsoft.VisualStudio.Package.TokenColor> ao armazená-lo na <xref:Microsoft.VisualStudio.Package.TokenInfo> estrutura; [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] vê apenas o índice.

### <a name="example"></a>Exemplo
 O exemplo a seguir mostra como o verificador pode identificar três tipos de token: números, pontuação e identificadores (qualquer coisa que não seja um número ou pontuação). Este exemplo é apenas para fins ilustrativos e não representa uma implementação abrangente do analisador e do scanner. Ele pressupõe que há uma `Lexer` classe com um `GetNextToken()` método que retorna uma cadeia de caracteres.

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

## <a name="see-also"></a>Confira também
- [Recursos do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-features1.md)
- [Analisador e scanner do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)
- [Registrar um serviço de linguagem herdado](../../extensibility/internals/registering-a-legacy-language-service1.md)
