---
title: Analisador e scanner do serviço de idioma herdado | Microsoft Docs
description: Saiba mais sobre o analisador e o verificador do serviço de idioma herdado que selecionam informações sobre o código que está sendo exibido.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- parsers, language services [managed package framework]
- language services [managed package framework], Parsers
ms.assetid: 1ac3de27-a23b-438d-9593-389e45839cfa
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9c57bd9f8b71f861fd5be4176211af6907b27e74
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090831"
---
# <a name="legacy-language-service-parser-and-scanner"></a>Analisador e scanner do serviço de linguagem herdado
O analisador é o coração do serviço de linguagem. As classes de linguagem MPF (estrutura de pacote gerenciada) exigem um analisador de idioma para selecionar informações sobre o código que está sendo exibido. Um analisador separa o texto em tokens léxicos e, em seguida, identifica esses tokens por tipo e funcionalidade.

## <a name="discussion"></a>Discussão
 Este é um método C#.

```csharp
namespace MyNamespace
{
    class MyClass
    {
        public void MyFunction(int arg1)
        {
            int var1 = arg1;
        }
    }
}
```

 Neste exemplo, os tokens são as palavras e as marcas de pontuação. Os tipos de tokens são os seguintes.

|Nome do Token|Tipo de token|
|----------------|----------------|
|namespace, classe, público, void, int|palavra-chave|
|=|operador|
|{ } ( ) ;|delimitador|
|MyNamespace, MyClass, MyFunction, arg1, var1|identificador|
|MyNamespace|namespace|
|MyClass|classe|
|MyFunction|method|
|arg1|parâmetro|
|var1|variável local|

 A função do analisador é identificar os tokens. Alguns tokens podem ter mais de um tipo. Depois que o analisador identificar os tokens, o serviço de idioma poderá usar as informações para fornecer recursos úteis, como realce de sintaxe, correspondência de chaves e operações do IntelliSense.

## <a name="types-of-parsers"></a>Tipos de analisadores
 Um analisador de serviço de linguagem não é o mesmo que um analisador usado como parte de um compilador. No entanto, esse tipo de analisador precisa usar um scanner e um analisador, da mesma maneira que um analisador de compilador.

- Um scanner é usado para identificar tipos de tokens. Estas informações são usadas para realçar a sintaxe e para identificar rapidamente tipos de tokens que podem disparar outras operações, por exemplo, correspondência de chave. Esse scanner é representado pela <xref:Microsoft.VisualStudio.Package.IScanner> interface.

- Um analisador é usado para descrever as funções e o escopo dos tokens. Essas informações são usadas em operações do IntelliSense para identificar elementos de linguagem, como métodos, variáveis, parâmetros e declarações, e fornecer listas de membros e assinaturas de método com base no contexto. Esse analisador também é usado para localizar pares de elementos de idioma correspondentes, como chaves e parênteses. Esse analisador é acessado por meio do <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe.

  A forma como você implementa um scanner e um analisador para o seu serviço de idioma é sua. Há vários recursos disponíveis que descrevem como funcionam os analisadores e como escrever seu próprio analisador. Além disso, vários produtos gratuitos e comerciais estão disponíveis para ajudar na criação de um analisador.

### <a name="the-parsesource-parser"></a>O analisador de análise
 Ao contrário de um analisador que é usado como parte de um compilador (onde os tokens são convertidos em alguma forma de código executável), um analisador de serviço de linguagem pode ser chamado por vários motivos diferentes e em muitos contextos diferentes. A forma como você implementa essa abordagem no <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe cabe a você. É importante ter em mente que o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método pode ser chamado em um thread em segundo plano.

> [!CAUTION]
> A <xref:Microsoft.VisualStudio.Package.ParseRequest> estrutura contém uma referência ao <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> objeto. Este <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> objeto não pode ser usado no thread em segundo plano. Na verdade, muitas das classes de MPF base não podem ser usadas no thread em segundo plano. Isso inclui as <xref:Microsoft.VisualStudio.Package.Source> <xref:Microsoft.VisualStudio.Package.ViewFilter> classes,, <xref:Microsoft.VisualStudio.Package.CodeWindowManager> e qualquer outra classe que se comunica direta ou indiretamente com a exibição.

 Esse analisador normalmente analisa o arquivo de origem inteiro na primeira vez em que é chamado ou quando o valor do motivo da análise de <xref:Microsoft.VisualStudio.Package.ParseReason> é fornecido. As chamadas subsequentes para o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método manipulam uma pequena parte do código analisado e podem ser executadas muito mais rapidamente usando os resultados da operação de análise completa anterior. O <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método comunica os resultados da operação de análise por meio dos <xref:Microsoft.VisualStudio.Package.AuthoringSink> objetos e <xref:Microsoft.VisualStudio.Package.AuthoringScope> . O <xref:Microsoft.VisualStudio.Package.AuthoringSink> objeto é usado para coletar informações para um motivo de análise específico, por exemplo, informações sobre as extensões de chaves ou assinaturas de método correspondentes que têm listas de parâmetros. O <xref:Microsoft.VisualStudio.Package.AuthoringScope> fornece coleções de declarações e assinaturas de método e também suporte para a opção ir para edição avançada (**ir para definição**, **ir para declaração**, **ir para referência**).

### <a name="the-iscanner-scanner"></a>O scanner isgravar
 Você também deve implementar um scanner que implementa o <xref:Microsoft.VisualStudio.Package.IScanner> . No entanto, como esse scanner funciona em uma base linha por linha por meio da <xref:Microsoft.VisualStudio.Package.Colorizer> classe, normalmente é mais fácil de implementar. No início de cada linha, o MPF dá à <xref:Microsoft.VisualStudio.Package.Colorizer> classe um valor a ser usado como uma variável de estado que é passada para o scanner. No final de cada linha, o verificador retorna a variável de estado atualizado. O MPF armazena em cache essas informações de estado para cada linha para que o verificador possa iniciar a análise de qualquer linha sem precisar iniciar no início do arquivo de origem. Essa verificação rápida de uma única linha permite que o editor forneça comentários rápidos ao usuário.

## <a name="parsing-for-matching-braces"></a>Análise para chaves correspondentes
 Este exemplo mostra o fluxo de controle para corresponder a uma chave de fechamento que o usuário tenha digitado. Nesse processo, o verificador usado para a colorização também é usado para determinar o tipo de token e se o token pode disparar uma operação de chave de correspondência. Se o gatilho for encontrado, o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método será chamado para localizar a chave correspondente. Por fim, as duas chaves são realçadas.

 Embora chaves sejam usadas nos nomes de gatilhos e motivos de análise, esse processo não está limitado a chaves reais. Há suporte para qualquer par de caracteres especificado para ser um par correspondente. Os exemplos incluem (e), \< and > e [e].

 Suponha que o serviço de linguagem dê suporte a chaves correspondentes.

1. O usuário digita uma chave de fechamento (}).

2. A chave é inserida no cursor no arquivo de origem e o cursor é avançado por um.

3. O <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> método na <xref:Microsoft.VisualStudio.Package.Source> classe é chamado com a chave de fechamento digitada.

4. O <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> método chama o <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> método na <xref:Microsoft.VisualStudio.Package.Source> classe para obter o token na posição logo antes da posição atual do cursor. Esse token corresponde à chave de fechamento digitada).

    1. O <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> método chama o <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> método no <xref:Microsoft.VisualStudio.Package.Colorizer> objeto para obter todos os tokens na linha atual.

    2. O <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> método chama o <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> método no <xref:Microsoft.VisualStudio.Package.IScanner> objeto com o texto da linha atual.

    3. O <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> método chama repetidamente o <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> método no <xref:Microsoft.VisualStudio.Package.IScanner> objeto para reunir todos os tokens da linha atual.

    4. O <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> método chama um método particular na <xref:Microsoft.VisualStudio.Package.Source> classe para obter o token que contém a posição desejada e passa a lista de tokens obtidos do <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> método.

5. O <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> método procura um sinalizador de gatilho de token de <xref:Microsoft.VisualStudio.Package.TokenTriggers> no token que é retornado do <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> método; ou seja, o token que representa a chave de fechamento).

6. Se o sinalizador de gatilho de <xref:Microsoft.VisualStudio.Package.TokenTriggers> for encontrado, o <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> método na <xref:Microsoft.VisualStudio.Package.Source> classe será chamado.

7. O <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> método inicia uma operação de análise com o valor da razão de análise de <xref:Microsoft.VisualStudio.Package.ParseReason> . Essa operação finalmente chama o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe. Se a análise assíncrona estiver habilitada, essa chamada para o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método ocorrerá em um thread em segundo plano.

8. Quando a operação de análise é concluída, um manipulador de conclusão interno (também conhecido como um método de retorno de chamada) chamado `HandleMatchBracesResponse` é chamado na <xref:Microsoft.VisualStudio.Package.Source> classe. Essa chamada é feita automaticamente pela <xref:Microsoft.VisualStudio.Package.LanguageService> classe base, não pelo analisador.

9. O `HandleMatchBracesResponse` método obtém uma lista de Spans do <xref:Microsoft.VisualStudio.Package.AuthoringSink> objeto que está armazenado no <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto. (Um Span é uma <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> estrutura que especifica um intervalo de linhas e caracteres no arquivo de origem.) Essa lista de Spans normalmente contém duas extensões, uma para as chaves de abertura e fechamento.

10. O `HandleBracesResponse` método chama o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> método no <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> objeto que está armazenado no <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto. Isso realça os intervalos fornecidos.

11. Se a <xref:Microsoft.VisualStudio.Package.LanguagePreferences> propriedade <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> estiver habilitada, o `HandleBracesResponse` método obterá o texto que é incluído pelo intervalo correspondente e exibirá os primeiros 80 caracteres desse intervalo na barra de status. Isso funciona melhor se o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método incluir o elemento de linguagem que acompanha o par correspondente. Para obter mais informações, consulte a propriedade <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>.

12. Concluído.

### <a name="summary"></a>Resumo
 A operação de chaves correspondentes normalmente é limitada a pares simples de elementos de linguagem. Elementos mais complexos, como percorridas correspondentes (" `if(...)` ", " `{` " e " `}` ", ou " `else` ", " `{` " e " `}` "), podem ser realçados como parte de uma operação de conclusão de palavras. Por exemplo, quando a palavra "else" for concluída, a instrução " `if` " correspondente poderá ser realçada. Se houver uma série de `if` / `else if` instruções, todas elas poderão ser realçadas usando o mesmo mecanismo que as chaves correspondentes. A <xref:Microsoft.VisualStudio.Package.Source> classe base já dá suporte a isso, da seguinte maneira: o verificador deve retornar o valor do gatilho de token <xref:Microsoft.VisualStudio.Package.TokenTriggers> combinado com o valor do gatilho <xref:Microsoft.VisualStudio.Package.TokenTriggers> para o token que está antes da posição do cursor.

 Para obter mais informações, consulte [correspondência de chaves em um serviço de idioma herdado](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md).

## <a name="parsing-for-colorization"></a>Análise para colorização
 A colorização do código-fonte é simples, apenas identifique o tipo de token e as informações de cor de retorno sobre esse tipo. A <xref:Microsoft.VisualStudio.Package.Colorizer> classe age como o intermediário entre o editor e o scanner para fornecer informações de cores sobre cada token. A <xref:Microsoft.VisualStudio.Package.Colorizer> classe usa o <xref:Microsoft.VisualStudio.Package.IScanner> objeto para ajudar a colorir uma linha e também para reunir informações de estado para todas as linhas no arquivo de origem. Nas classes de serviço de linguagem MPF, a <xref:Microsoft.VisualStudio.Package.Colorizer> classe não precisa ser substituída porque se comunica com o scanner somente por meio da <xref:Microsoft.VisualStudio.Package.IScanner> interface. Você fornece o objeto que implementa a <xref:Microsoft.VisualStudio.Package.IScanner> interface substituindo o <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método na <xref:Microsoft.VisualStudio.Package.LanguageService> classe.

 O <xref:Microsoft.VisualStudio.Package.IScanner> Verificador recebe uma linha de código-fonte por meio do <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> método. As chamadas para o <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> método são repetidas para obter o próximo token na linha até que a linha seja esgotada de tokens. Para a colorização, o MPF trata todo o código-fonte como uma sequência de linhas. Portanto, o verificador deve ser capaz de lidar com a origem que está chegando a ele como linhas. Além disso, qualquer linha pode ser passada para o scanner a qualquer momento, e a única garantia é que o verificador recebe a variável de estado da linha antes da linha a ser verificada.

 A <xref:Microsoft.VisualStudio.Package.Colorizer> classe também é usada para identificar gatilhos de token. Esses gatilhos informam ao MPF que um determinado token pode iniciar uma operação mais complexa, como preenchimento de palavras ou chaves correspondentes. Como a identificação desses gatilhos deve ser rápida e deve ocorrer em qualquer local, o verificador é mais adequado para essa tarefa.

 Para obter mais informações, consulte [colorir sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md).

## <a name="parsing-for-functionality-and-scope"></a>Análise de funcionalidade e escopo
 A análise da funcionalidade e do escopo requer mais esforço do que apenas identificar os tipos de tokens encontrados. O analisador precisa identificar não apenas o tipo de token, mas também a funcionalidade para a qual o token é usado. Por exemplo, um identificador é apenas um nome, mas em seu idioma, um identificador pode ser o nome de uma classe, namespace, método ou variável, dependendo do contexto. O tipo geral do token pode ser um identificador, mas o identificador também pode ter outros significados, dependendo do que é e onde ele está definido. Essa identificação exige que o analisador tenha um conhecimento mais extensivo sobre a linguagem que está sendo analisada. É aí que <xref:Microsoft.VisualStudio.Package.AuthoringSink> entra a classe. A <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe coleta informações sobre identificadores, métodos, pares de idiomas correspondentes (como chaves e parênteses) e processamentos de idiomas (semelhantes a pares de idiomas, exceto pelo fato de que há três partes, por exemplo, "" `foreach()` " `{` " e " `}` "). Além disso, você pode substituir a <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe para dar suporte à identificação de código, que é usada na validação antecipada de pontos de interrupção para que o depurador não precise ser carregado e a janela depuração **automática** , que mostra variáveis locais e parâmetros automaticamente quando um programa está sendo depurado e requer que o analisador identifique variáveis locais e parâmetros apropriados além daqueles apresentados pelo depurador.

 O <xref:Microsoft.VisualStudio.Package.AuthoringSink> objeto é passado para o analisador como parte do <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto e um novo <xref:Microsoft.VisualStudio.Package.AuthoringSink> objeto é criado toda vez que um novo <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto é criado. Além disso, o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método deve retornar um <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto, que é usado para lidar com várias operações do IntelliSense. O <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto mantém uma lista de declarações e uma lista de métodos, que é preenchida, dependendo do motivo da análise. A <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe deve ser implementada.

## <a name="see-also"></a>Confira também
- [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)
- [Visão geral do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-overview.md)
- [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)
- [Correspondência de chaves em um serviço de linguagem herdado](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)
