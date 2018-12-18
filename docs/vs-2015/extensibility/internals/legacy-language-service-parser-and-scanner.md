---
title: Analisador de serviço de linguagem herdada e Scanner | Microsoft Docs
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
- parsers, language services [managed package framework]
- language services [managed package framework], Parsers
ms.assetid: 1ac3de27-a23b-438d-9593-389e45839cfa
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: fd419c569a298afd37548fd7b85a23cad733e371
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51786387"
---
# <a name="legacy-language-service-parser-and-scanner"></a>Analisador e scanner do serviço de linguagem herdado
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O analisador é o coração do serviço de linguagem. As classes de linguagem da estrutura de pacote gerenciado (MPF) exigem um analisador de linguagem para selecionar as informações sobre o código que está sendo exibido. Um analisador separa o texto em tokens léxicos e, em seguida, identifica esses tokens por tipo e funcionalidade.  
  
## <a name="discussion"></a>Discussão  
 Este é um método em c#.  
  
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
  
 Neste exemplo, os tokens são as palavras e sinais de pontuação. Os tipos de tokens são da seguinte maneira.  
  
|Nome do token|Tipo de token|  
|----------------|----------------|  
|namespace, void público, de classe, int|keyword|  
|=|operator|  
|{ } ( ) ;|delimitador|  
|MyNamespace, MyClass, MyFunction, arg1, var1|identifier|  
|MyNamespace|namespace|  
|MyClass|classe|  
|MyFunction|method|  
|arg1|parâmetro|  
|var1|variável local|  
  
 A função do analisador é identificar os tokens. Alguns tokens podem ter mais de um tipo. Depois que o analisador identificou os tokens, o serviço de linguagem pode usar as informações para fornecer recursos úteis, como realce de sintaxe, a correspondência de chaves e as operações do IntelliSense.  
  
## <a name="types-of-parsers"></a>Tipos de analisadores  
 Um analisador de serviço de linguagem não é o mesmo que um analisador usado como parte de um compilador. No entanto, esse tipo de analisador precisa usar um scanner e um analisador, da mesma forma como um analisador de compilador.  
  
- Um scanner é usado para identificar os tipos de tokens. Essas informações são usadas para o realce de sintaxe e para identificar rapidamente os tipos de token que podem disparar outras operações, por exemplo, a correspondência de chaves. Este verificador é representado pelo <xref:Microsoft.VisualStudio.Package.IScanner> interface.  
  
- Um analisador é usado para descrever as funções e o escopo dos tokens. Essas informações são usadas em operações do IntelliSense para identificar elementos de linguagem, como métodos, variáveis, parâmetros e declarações e fornecer listas de membros e assinaturas de método com base no contexto. Esse parser também é usado para localizar pares correspondentes de elemento de linguagem, como chaves e parênteses. Esse analisador é acessado por meio de <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método no <xref:Microsoft.VisualStudio.Package.LanguageService> classe.  
  
  Como implementar um analisador e scanner do seu serviço de linguagem cabe a você. Vários recursos estão disponíveis que descrevem como os analisadores funcionam e como escrever seu próprio analisador. Além disso, vários produtos gratuitos e comerciais estão disponíveis que ajuda na criação de um analisador.  
  
### <a name="the-parsesource-parser"></a>O analisador ParseSource  
 Ao contrário de um analisador que é usado como parte de um compilador (no qual os tokens são convertidos em alguma forma de código executável), um analisador de serviço de linguagem pode ser chamado por muitas razões diferentes e em muitos contextos diferentes. Como você pode implementar essa abordagem na <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método no <xref:Microsoft.VisualStudio.Package.LanguageService> classe cabe a você. É importante ter em mente que o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método pode ser chamado em um thread em segundo plano.  
  
> [!CAUTION]
>  O <xref:Microsoft.VisualStudio.Package.ParseRequest> estrutura contém uma referência para o <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> objeto. Isso <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> objeto não pode ser usado no thread de segundo plano. Na verdade, muitas das classes base MPF não podem ser usadas no thread de segundo plano. Isso inclui o <xref:Microsoft.VisualStudio.Package.Source>, <xref:Microsoft.VisualStudio.Package.ViewFilter>, <xref:Microsoft.VisualStudio.Package.CodeWindowManager> classes e qualquer outra classe que direta ou indiretamente se comunica com o modo de exibição.  
  
 Esse analisador normalmente analisa a hora do arquivo a primeira de origem inteira ele é chamado ou quando a análise motivo, o valor de <xref:Microsoft.VisualStudio.Package.ParseReason> é fornecido. As chamadas subsequentes para o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método lidar com uma pequena parte do código analisado e pode ser executado muito mais rapidamente, usando os resultados da operação de análise completa anterior. O <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método comunica os resultados da operação de análise por meio de <xref:Microsoft.VisualStudio.Package.AuthoringSink> e <xref:Microsoft.VisualStudio.Package.AuthoringScope> objetos. O <xref:Microsoft.VisualStudio.Package.AuthoringSink> objeto é usado para coletar informações por um motivo específico de análise, por exemplo, informações sobre os intervalos de chaves ou assinaturas de método que possuem listas de parâmetros correspondentes. O <xref:Microsoft.VisualStudio.Package.AuthoringScope> fornece coleções de declarações e assinaturas de método e também suporte para ir para avançada opção Editar (**ir para definição**, **ir para declaração**, **ir para Fazer referência a**).  
  
### <a name="the-iscanner-scanner"></a>O Scanner IScanner  
 Você também deve implementar um scanner que implementa <xref:Microsoft.VisualStudio.Package.IScanner>. No entanto, porque este scanner opera em uma base linha por linha por meio de <xref:Microsoft.VisualStudio.Package.Colorizer> classe, é geralmente mais fácil de implementar. No início de cada linha, MPF oferece o <xref:Microsoft.VisualStudio.Package.Colorizer> um valor a ser usado como uma variável de estado que é passada para o verificador de classe. No final de cada linha, o scanner retorna a variável de estado atualizado. MPF armazena essas informações de estado para cada linha para que o scanner pode iniciar uma análise de qualquer linha sem ter que começar do início do arquivo de origem. Essa verificação rápida de uma única linha permite que o editor fornecer comentários rápidos para o usuário.  
  
## <a name="parsing-for-matching-braces"></a>Análise para chaves correspondentes  
 Este exemplo mostra o fluxo de controle para correspondência de uma chave de fechamento que o usuário digitou. Nesse processo, o que é usado para colorização de scanner também é usado para determinar o tipo de token e se o token pode disparar uma operação de correspondência de chaves. Se o gatilho for encontrado, o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método é chamado para localizar a chave correspondente. Por fim, as duas chaves são realçadas.  
  
 Mesmo que as chaves são usadas em nomes de gatilhos e analisar as razões, esse processo não é limitado a chaves reais. Há suporte para qualquer par de caracteres que é especificado como sendo um par correspondente. Os exemplos incluem (e), \< e >, e [e].  
  
 Suponha que o serviço de linguagem dá suporte a chaves correspondentes.  
  
1.  O usuário digita uma chave de fechamento (}).  
  
2.  A chave de abertura é inserido na posição do cursor no arquivo de origem e o cursor é avançado por um.  
  
3.  O <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> método no <xref:Microsoft.VisualStudio.Package.Source> classe é chamada com a chave de fechamento tipado.  
  
4.  O <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> chamadas de método de <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> método no <xref:Microsoft.VisualStudio.Package.Source> classe para obter o token na posição apenas antes da posição atual do cursor. Esse token corresponde da chave de fechamento tipada).  
  
    1.  O <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> chamadas de método de <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> método no <xref:Microsoft.VisualStudio.Package.Colorizer> objeto para obter todos os tokens na linha atual.  
  
    2.  O <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> chamadas de método de <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> método no <xref:Microsoft.VisualStudio.Package.IScanner> objeto com o texto da linha atual.  
  
    3.  O <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> repetidamente o método chama o <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> método no <xref:Microsoft.VisualStudio.Package.IScanner> objeto para reunir todos os tokens a partir da linha atual.  
  
    4.  O <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> método chama um método particular em de <xref:Microsoft.VisualStudio.Package.Source> classe para obter o token que contém a posição desejada e passa na lista de tokens obtidos do <xref:Microsoft.VisualStudio.Package.Colorizer.GetLineInfo%2A> método.  
  
5.  O <xref:Microsoft.VisualStudio.Package.Source.OnCommand%2A> método procura um sinalizador de token de gatilho de <xref:Microsoft.VisualStudio.Package.TokenTriggers> no token que é retornado o <xref:Microsoft.VisualStudio.Package.Source.GetTokenInfo%2A> método; ou seja, o token que representa a chave de fechamento).  
  
6.  Se o gatilho do sinalizador de <xref:Microsoft.VisualStudio.Package.TokenTriggers> for encontrado, o <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> método o <xref:Microsoft.VisualStudio.Package.Source> classe é chamada.  
  
7.  O <xref:Microsoft.VisualStudio.Package.Source.MatchBraces%2A> método inicia uma operação de análise com o valor de motivo de análise de <xref:Microsoft.VisualStudio.Package.ParseReason>. Essa operação, por fim, chama o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método no <xref:Microsoft.VisualStudio.Package.LanguageService> classe. Se a análise assíncrono está habilitado, essa chamada para o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método ocorre em um thread em segundo plano.  
  
8.  Quando a operação de análise for concluída, um manipulador de conclusão interno (também conhecido como um método de retorno de chamada) chamado `HandleMatchBracesResponse` é chamado no <xref:Microsoft.VisualStudio.Package.Source> classe. Essa chamada é feita automaticamente pelo <xref:Microsoft.VisualStudio.Package.LanguageService> base classe, não pelo analisador.  
  
9. O `HandleMatchBracesResponse` método obtém uma lista de intervalos da <xref:Microsoft.VisualStudio.Package.AuthoringSink> que é armazenado no objeto o <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto. (Um alcance é um <xref:Microsoft.VisualStudio.TextManager.Interop.TextSpan> estrutura que especifica um intervalo de linhas e os caracteres no arquivo de origem.) Esta lista de intervalos geralmente contém dois intervalos, cada um para as chaves de abertura e fechamento.  
  
10. O `HandleBracesResponse` chamadas de método de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView.HighlightMatchingBrace%2A> método na <xref:Microsoft.VisualStudio.TextManager.Interop.IVsTextView> objeto que é armazenado no <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto. Isso destaca os intervalos de determinado.  
  
11. Se o <xref:Microsoft.VisualStudio.Package.LanguagePreferences> propriedade <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A> estiver habilitada, o `HandleBracesResponse` método obtém o texto que é abrangido pela extensão correspondente e exibe os primeiros 80 caracteres do que se estendem por na barra de status. Isso funciona melhor se o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método inclui o elemento de linguagem que acompanha o par correspondente. Para obter mais informações, consulte a propriedade <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableShowMatchingBrace%2A>.  
  
12. Feito.  
  
### <a name="summary"></a>Resumo  
 A operação de correspondência de chaves é normalmente limitada aos pares simples de elementos de linguagem. Elementos mais complexos, como correspondência triplos ("`if(…)`","`{`"e"`}`", ou "`else`","`{`"e"`}`"), pode ser realçado como parte de uma operação de preenchimento automático de palavras. Por exemplo, quando a palavra "else" for concluída, a correspondência "`if`" instrução pode ser destacada. Se houvesse uma série de `if` / `else if` instruções, todos eles poderiam ser realçadas, usando o mesmo mecanismo como chaves correspondentes. O <xref:Microsoft.VisualStudio.Package.Source> classe base já oferece suporte a isso, da seguinte maneira: O scanner deve retornar o valor do token de gatilho <xref:Microsoft.VisualStudio.Package.TokenTriggers> combinado com o valor de gatilho <xref:Microsoft.VisualStudio.Package.TokenTriggers> para o token que está antes da posição do cursor.  
  
 Para obter mais informações, consulte [correspondência de chaves em um serviço de linguagem herdado](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md).  
  
## <a name="parsing-for-colorization"></a>Análise de colorização  
 Coloração de código-fonte é simples, basta identificar o tipo de informações de cores de token e retorno sobre o tipo. O <xref:Microsoft.VisualStudio.Package.Colorizer> classe atua como intermediário entre o editor e o scanner para fornecer informações sobre todos os tokens de cores. O <xref:Microsoft.VisualStudio.Package.Colorizer> classe usa o <xref:Microsoft.VisualStudio.Package.IScanner> objeto para ajudá-lo colorir uma linha e também para coletar informações de estado para todas as linhas no arquivo de origem. Nas classes de serviço de linguagem MPF, o <xref:Microsoft.VisualStudio.Package.Colorizer> classe não precisa ser substituída porque ele se comunica com o scanner somente por meio de <xref:Microsoft.VisualStudio.Package.IScanner> interface. Você fornecer o objeto que implementa o <xref:Microsoft.VisualStudio.Package.IScanner> interface por meio da substituição a <xref:Microsoft.VisualStudio.Package.LanguageService.GetScanner%2A> método o <xref:Microsoft.VisualStudio.Package.LanguageService> classe.  
  
 O <xref:Microsoft.VisualStudio.Package.IScanner> verificador está considerando uma linha do código-fonte por meio de <xref:Microsoft.VisualStudio.Package.IScanner.SetSource%2A> método. Chamadas para o <xref:Microsoft.VisualStudio.Package.IScanner.ScanTokenAndProvideInfoAboutIt%2A> método são repetidas para obter o próximo token na linha até que a linha está esgotada de tokens. Para colorização, MPF tratará todo código-fonte como uma sequência de linhas. Portanto, o scanner deve ser capaz de lidar com chegando até ele como linhas de código-fonte. Além disso, qualquer linha pode ser passada para o mecanismo de varredura a qualquer momento, e a única garantia é que o scanner recebe a variável de estado da linha de antes da linha prestes a ser verificado.  
  
 O <xref:Microsoft.VisualStudio.Package.Colorizer> classe também é usado para identificar os gatilhos de token. Esses disparadores informam MPF que um token específico pode iniciar uma operação mais complexa, como preenchimento automático de palavras ou chaves correspondentes. Como identificar tais gatilhos deve ser rápido e deve ocorrer em qualquer local, o scanner é mais adequado para essa tarefa.  
  
 Para obter mais informações, consulte [coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md).  
  
## <a name="parsing-for-functionality-and-scope"></a>Análise para funcionalidade e escopo  
 Análise de funcionalidades e escopo requer mais esforço do que apenas identificar os tipos de tokens que são encontrados. O analisador deve identificar não apenas o tipo de token, mas também a funcionalidade para a qual o token é usado. Por exemplo, um identificador é apenas um nome, mas em seu idioma, um identificador pode ser o nome de uma classe, namespace, método ou variável, dependendo do contexto. O tipo geral do token pode ser um identificador, mas o identificador também possuem outros significados, dependendo do que ele é e onde ele está definido. Essa identificação exige que o analisador para ter mais de um vasto conhecimento sobre o idioma que está sendo analisado. É aí que o <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe chega. O <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe coleta informações sobre identificadores, métodos, pares correspondentes de linguagem (como chaves e parênteses) e triplos de linguagem (semelhante a pares de idiomas, exceto que há três partes, por exemplo, "`foreach()`" "`{`"e"`}`"). Além disso, você pode substituir a <xref:Microsoft.VisualStudio.Package.AuthoringSink> classe para dar suporte à identificação de código, que é usada na validação antecipada de pontos de interrupção para que o depurador não tem de ser carregado, e o **Autos** janela de depuração, que mostra o local variáveis e parâmetros automaticamente quando um programa está sendo depurado e exige que o analisador para identificar parâmetros além daqueles que apresenta o depurador e variáveis locais apropriadas.  
  
 O <xref:Microsoft.VisualStudio.Package.AuthoringSink> objeto é passado para o analisador como parte do <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto e uma nova <xref:Microsoft.VisualStudio.Package.AuthoringSink> objeto é criado toda vez que um novo <xref:Microsoft.VisualStudio.Package.ParseRequest> objeto é criado. Além disso, o <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> método deve retornar um <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto, que é usado para manipular várias operações do IntelliSense. O <xref:Microsoft.VisualStudio.Package.AuthoringScope> objeto mantém uma lista de declarações e uma lista de métodos, ou que é preenchido, dependendo do motivo para análise. O <xref:Microsoft.VisualStudio.Package.AuthoringScope> classe deve ser implementado.  
  
## <a name="see-also"></a>Consulte também  
 [Implementando um serviço de linguagem herdado](../../extensibility/internals/implementing-a-legacy-language-service1.md)   
 [Visão geral do serviço de linguagem herdado](../../extensibility/internals/legacy-language-service-overview.md)   
 [Coloração de sintaxe em um serviço de linguagem herdado](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)   
 [Correspondência de chave em um serviço de linguagem herdado](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)

