---
title: Analisadores de Roslyn e biblioteca de reconhecimento de código para ImmutableArrays | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
ms.assetid: 0b0afa22-3fca-4d59-908e-352464c1d903
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: e2af6141ae3b7a61805b2515f11f72f164389949
ms.sourcegitcommit: d7f232a7596420e40ff8051d42cdf90203af4a74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52821377"
---
# <a name="roslyn-analyzers-and-code-aware-library-for-immutablearrays"></a>Analisadores de Roslyn e biblioteca de reconhecimento de código para ImmutableArrays

O [.NET Compiler Platform](https://github.com/dotnet/roslyn) ("Roslyn") ajuda você a criar bibliotecas de código. Uma biblioteca de reconhecimento de código fornece funcionalidade que você pode usar e ferramentas (analisadores de Roslyn) para ajudá-lo a usar a biblioteca da melhor maneira ou para evitar erros. Este tópico mostra como criar um analisador Roslyn de mundo real para capturar erros comuns ao usar o [Immutable](https://www.nuget.org/packages/System.Collections.Immutable) pacote do NuGet. O exemplo também demonstra como fornecer uma correção de código para um problema de código encontrado pelo analisador. Usuários veem correções de código em que a lâmpada do Visual Studio da interface do usuário e podem aplicar uma correção para o código automaticamente.

## <a name="get-started"></a>Introdução

Você precisará do seguinte para compilar este exemplo:

* Visual Studio 2015 (não uma edição Express) ou uma versão posterior. Você pode usar a versão gratuita [Visual Studio Community Edition](https://visualstudio.microsoft.com/vs/community/)
* [SDK do Visual Studio](../extensibility/visual-studio-sdk.md). Você também pode, ao instalar o Visual Studio, verificar **ferramentas de extensibilidade do Visual Studio** sob **ferramentas comuns** para instalar o SDK ao mesmo tempo. Se você já tiver instalado o Visual Studio, você também pode instalar esse SDK indo até o menu principal **arquivo** > **New** > **projeto**, escolhendo **c#** no painel de navegação à esquerda e, em seguida, escolhendo **extensibilidade**. Quando você escolhe o "**instalar as ferramentas de extensibilidade do Visual Studio**" modelo de projeto de navegação estrutural, ele solicitará que você baixe e instale o SDK.
* [("Roslyn") do SDK do .NET compiler Platform](http://aka.ms/roslynsdktemplates). Você também pode instalar esse SDK indo até o menu principal **arquivo** > **New** > **projeto**, escolhendo **c#** no painel de navegação à esquerda e, em seguida, escolhendo **extensibilidade**. Quando você escolhe "**baixar o SDK do .NET Compiler Platform**" modelo de projeto de navegação estrutural, ele solicitará que você baixe e instale o SDK. Esse SDK inclui o [Roslyn Syntax Visualizer](https://github.com/dotnet/roslyn/wiki/Syntax%20Visualizer). Ajuda essa ferramenta útil que você a descobrir quais tipos de modelo de código você deve procurar em seu analisador. As chamadas de infraestrutura do analisador em seu código para tipos de modelo de código específico, para que seu código só é executada quando necessário e pode se concentrar apenas na análise de código relevante.

## <a name="whats-the-problem"></a>O que é o problema?

Imagine que você fornece uma biblioteca com ImmutableArray (por exemplo, <xref:System.Collections.Immutable.ImmutableArray%601?displayProperty=fullName>) dão suporte. Os desenvolvedores do c# tem muita experiência com as matrizes do .NET. No entanto, devido à natureza das técnicas de ImmutableArrays e otimização usada na implementação, intuitions do desenvolvedor c# fazer com que os usuários da sua biblioteca escrever códigos quebrados, conforme explicado abaixo. Além disso, os usuários não veem seus erros de tempo de execução, o que não é a experiência de qualidade que eles são usados no Visual Studio com o .NET para.

Os usuários estão familiarizados em escrever um código semelhante ao seguinte:

```csharp
var a1 = new int[0];
Console.WriteLine("a1.Length = { 0}", a1.Length);
var a2 = new int[] { 1, 2, 3, 4, 5 };
Console.WriteLine("a2.Length = { 0}", a2.Length);
```

Criando matrizes vazias preencherem com linhas subsequentes do código e usando a sintaxe do inicializador de coleção são familiares para C# os desenvolvedores. No entanto, escrever o mesmo código para uma ImmutableArray ocasiona uma falha no tempo de execução:

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = { 0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = { 0}", b2.Length);
```

É o primeiro erro devido da implementação de ImmutableArray usando um struct para encapsular o armazenamento de dados subjacente. Structs deve ter construtores sem parâmetros, de modo que `default(T)` expressões podem retornar structs com todos os zero ou membros de nulos. Quando o código acessa `b1.Length`, há um nulo de tempo de execução de desreferência erro porque não há nenhuma matriz de armazenamento subjacente na estrutura ImmutableArray. É a maneira correta de criar uma ImmutableArray vazia `ImmutableArray<int>.Empty`.

O erro com inicializadores de coleção acontece porque o `ImmutableArray.Add` método retorna novas instâncias de cada vez que você chamá-lo. Como ImmutableArrays nunca mudam, quando você adiciona um novo elemento, você obtém um novo objeto de ImmutableArray (que pode compartilhar o armazenamento por motivos de desempenho com uma ImmutableArray existente anteriormente). Porque `b2` aponta para a primeira ImmutableArray antes de chamar `Add()` cinco vezes, `b2` é um padrão ImmutableArray. Chamar comprimento nele também falhas com um valor nulo desreferência de erro. A maneira correta de inicializar uma ImmutableArray sem chamar o método Add manualmente é usar `ImmutableArray.CreateRange(new int[] {1, 2, 3, 4, 5})`.

## <a name="find-relevant-syntax-node-types-to-trigger-your-analyzer"></a>Localizar tipos de nó para disparar seu analisador de sintaxe relevante

 Para começar a criar o analisador, primeiro descobrir que tipo de SyntaxNode que você precisa ser pesquisado. Inicie o **Syntax Visualizer** no menu **exibição** > **Other Windows** > **Roslyn Syntax Visualizer**.

Coloque o cursor do editor na linha que declara `b1`. Você verá o Syntax Visualizer mostra a você em um `LocalDeclarationStatement` nó da árvore de sintaxe. Este nó tem um `VariableDeclaration`, que por sua vez tem uma `VariableDeclarator`, que por sua vez tem um `EqualsValueClause`e, finalmente, há um `ObjectCreationExpression`. Ao clicar na árvore do Syntax Visualizer de nós, a sintaxe na janela do editor realça para mostrar a você o código representado por esse nó. Os nomes dos tipos SyntaxNode sub correspondem aos nomes usados na gramática da linguagem c#.

## <a name="create-the-analyzer-project"></a>Criar o projeto do analisador

No menu principal, escolha **arquivo** > **New** > **projeto**. No **novo projeto** caixa de diálogo, em **c#** projetos na barra de navegação à esquerda, escolha **extensibilidade**e no painel direito, escolha o **analisador com Correção de código** modelo de projeto. Insira um nome e confirme se a caixa de diálogo.

O modelo é aberto um *DiagnosticAnalyzer.cs* arquivo. Escolha esse editor de guia de buffer. Este arquivo tem uma classe de analisador (formado do nome que você atribuiu o projeto) que deriva de `DiagnosticAnalyzer` (um tipo de API do Roslyn). Sua nova classe tem um `DiagnosticAnalyzerAttribute` declarar seu analisador é relevante para a linguagem c# para que o compilador detecta e carrega seu analisador.

```csharp
[DiagnosticAnalyzer(LanguageNames.CSharp)]
public class ImmutableArrayAnalyzerAnalyzer : DiagnosticAnalyzer
{}
```

Você pode implementar um analisador usando o Visual Basic que tem como alvo o código c#, e vice-versa. É mais importante no DiagnosticAnalyzerAttribute para escolher se o seu analisador tem como alvo um idioma ou ambos. Analisadores mais sofisticados que requerem a modelagem detalhada da linguagem só podem direcionar um único idioma. Se o seu analisador, por exemplo, só verifica os nomes de tipo ou membro público, é possível usar o modelo de linguagem comum que roslyn oferece em Visual Basic e c#. Por exemplo, o FxCop avisa que uma classe implementa <xref:System.Runtime.Serialization.ISerializable>, mas a classe não tem o <xref:System.SerializableAttribute> atributo é independente de linguagem e funciona em código Visual Basic e c#.

## <a name="initialize-the-analyzer"></a>Inicializar o analisador

 Role para baixo um pouco na `DiagnosticAnalyzer` classe para ver o `Initialize` método. O compilador chama esse método quando se ative um analisador. O método utiliza um `AnalysisContext` objeto que permite que o seu analisador para obter informações de contexto e registrar retornos de chamada para eventos para os tipos de código que você deseja analisar.

```csharp
public override void Initialize(AnalysisContext context) {}
```

Abrir uma nova linha neste método e o tipo de "contexto." Para ver uma lista de conclusão do IntelliSense. Você pode ver na lista de conclusão, existem várias `Register...` métodos para lidar com vários tipos de eventos. Por exemplo, o primeiro deles, `RegisterCodeBlockAction`, chamadas de volta ao seu código para um bloco, o que geralmente é o código entre chaves. Registrar-se para um bloco também chama de volta ao seu código para o inicializador de um campo, o valor fornecido para um atributo ou o valor de um parâmetro opcional.

Como outro exemplo, `RegisterCompilationStartAction`, chamadas de volta ao seu código no início de uma compilação, o que é útil quando você precisa coletar estado ao longo de vários locais. Você pode criar uma estrutura de dados, por exemplo, para coletar todos os símbolos usados, e cada vez que seu analisador é chamado novamente para alguns sintaxe ou símbolo, você pode salvar informações sobre cada local em sua estrutura de dados. Quando você estiver chamado novamente devido um encerramento de compilação, você pode analisar todos os locais que você salvou, por exemplo, para relatar os símbolos que o código usa de cada `using` instrução.

Usando o **Syntax Visualizer**, você aprendeu que você deseja ser chamado quando o compilador processa um ObjectCreationExpression. Use este código para definir o retorno de chamada:

```csharp
context.RegisterSyntaxNodeAction(c => AnalyzeObjectCreation(c),
                                 SyntaxKind.ObjectCreationExpression);
```

Você se registrar para um nó de sintaxe e filtrar apenas objeto criação nós de sintaxe. Por convenção, os autores do analisador usam um lambda ao registrar ações, que ajuda a manter os analisadores sem monitoração de estado. Você pode usar o recurso do Visual Studio **Generate From Usage** para criar o `AnalyzeObjectCreation` método. Isso gera o tipo correto de parâmetro de contexto para você muito.

## <a name="set-properties-for-users-of-your-analyzer"></a>Definir propriedades para os usuários do seu analisador

Para que seu analisador apareça na interface de usuário do Visual Studio adequadamente, procure e modifique a seguinte linha de código para identificar seu analisador:

```csharp
internal const string Category = "Naming";
```

Alteração `"Naming"` para `"API Guidance"`.

Em seguida localize e abra a *Resources* arquivo no seu projeto usando o **Gerenciador de soluções**. Você pode colocar em uma descrição para seu analisador, título, etc. Você pode alterar o valor para todos eles para `"Don't use ImmutableArray<T> constructor"` por enquanto. Você pode colocar a cadeia de caracteres de argumentos na sua cadeia de caracteres de formatação ({0}, {1}, etc.) e posteriormente, quando você chamar `Diagnostic.Create()`, você pode fornecer um `params` matriz de argumentos a serem passados.

## <a name="analyze-an-object-creation-expression"></a>Analisar uma expressão de criação de objeto

O `AnalyzeObjectCreation` método usa um tipo diferente de contexto fornecido pela estrutura de analisador de código. O `Initialize` do método `AnalysisContext` permite que você registre os retornos de chamada de ação para configurar o seu analisador. O `SyntaxNodeAnalysisContext`, por exemplo, tem um `CancellationToken` que você pode passar ao redor. Se um usuário começa a digitar no editor, o Roslyn cancelará analisadores em execução para salvar o trabalho e melhorar o desempenho. Como outro exemplo, este contexto tem uma propriedade de nó que retorna o nó de sintaxe de criação do objeto.

Obtém o nó, que é possível supor que é o tipo para o qual você filtrado a ação de nó de sintaxe:

```csharp
var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
```

### <a name="launch-visual-studio-with-your-analyzer-the-first-time"></a>Inicie o Visual Studio com o seu analisador na primeira vez

Inicie o Visual Studio, criando e executando o seu analisador (pressione **F5**). Porque a inicialização do projeto na **Gerenciador de soluções** é o projeto VSIX, executando as compilações de código, seu código e um VSIX e, em seguida, inicia o Visual Studio com esse VSIX instalado. Quando você inicia o Visual Studio dessa forma, ele é iniciado com um hive do registro distintas para que seu uso principal do Visual Studio não será afetado por suas instâncias de testes durante a criação de analisadores. Na primeira vez que você iniciar dessa forma, o Visual Studio faz várias inicializações semelhantes quando você primeiro iniciei o Visual Studio depois de instalá-lo.

Crie um projeto de console e, em seguida, insira o código de matriz para o método de principal de aplicativos de console:

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = {0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = {0}", b2.Length);
```

As linhas de código com `ImmutableArray` tiver linhas onduladas, porque você precisa obter o pacote do NuGet imutável e adicionar um `using` instrução ao seu código. Pressione o botão direito do ponteiro no nó do projeto na **Gerenciador de soluções** e escolha **Manage NuGet Packages**. No Gerenciador do NuGet, digite "Imutável" na caixa de pesquisa e escolha o item **Immutable** (não escolher **Immutable**) no painel esquerdo e pressione a  **Instalar** botão no painel direito. A instalação do pacote adiciona uma referência às referências de projeto.

Você ainda verá rabiscos vermelhos sob `ImmutableArray`, então, coloque o cursor nesse identificador e pressione **Ctrl**+**.** (ponto) para abrir o menu de correção sugerida e escolha Adicionar apropriado `using` instrução.

**Salve e feche** a segunda instância do Visual Studio por enquanto para colocá-lo em um estado limpo para continuar.

## <a name="finish-the-analyzer-using-edit-and-continue"></a>Concluir o analisador usando editar e continuar

Na primeira instância do Visual Studio, defina um ponto de interrupção no início de sua `AnalyzeObjectCreation` método pressionando **F9** com o cursor na primeira linha.

Inicie seu analisador novamente com **F5**e na segunda instância do Visual Studio, reabra o seu aplicativo de console que você criou a última vez.

Retornar para a primeira instância do Visual Studio no ponto de interrupção porque o compilador Roslyn viu uma expressão de criação de objeto e chamadas para o seu analisador.

**Obtém o nó de criação do objeto.** Ignorar a linha que define a `objectCreation` variável pressionando **F10**e, nas **janela imediata** avaliar a expressão `"objectCreation.ToString()"`. Você verá que a variável aponta para o nó de sintaxe é o código `"new ImmutableArray<int>()"`, apenas o que você está procurando.

**Obter ImmutableArray < T\> objeto de tipo.** Você precisa verificar se o tipo que está sendo criado é ImmutableArray. Primeiro, você obtém o objeto que representa esse tipo. Verificar o tipos usando o modelo semântico para garantir que você tem exatamente o tipo correto, e você não se comparam a cadeia de caracteres de `ToString()`. Insira a seguinte linha de código no final da função:

```csharp
var immutableArrayOfTType =
    context.SemanticModel
           .Compilation
           .GetTypeByMetadataName("System.Collections.Immutable.ImmutableArray`1");
```

Você designar tipos genéricos nos metadados entre acentos graves (') e o número de parâmetros genéricos. É por isso que você não vir "... ImmutableArray\<T > "no nome de metadados.

O modelo semântico tem muitas coisas úteis que permitem que você faça perguntas sobre símbolos, fluxo de dados, o tempo de vida de variável, etc. Roslyn separa nós de sintaxe do modelo semântico por vários motivos engineering (desempenho, modelagem de código com falha, etc.). Você deseja que o modelo de compilação para pesquisar informações contidas nas referências para comparação de precisão.

Você pode arrastar o ponteiro de execução amarelo no lado esquerdo da janela do editor. Arraste-o até a linha que define a `objectCreation` variável e passar sobre a nova linha de código usando **F10**. Se você passar o ponteiro do mouse sobre a variável `immutableArrayOfType`, você verá que encontramos o tipo exato no modelo semântico.

**Obtenha o tipo da expressão de criação de objeto.** "Type" é usado de algumas maneiras neste artigo, mas isso significa que se você tiver "nova Foo" expressão, você precisa obter um modelo de Foo. Você precisa obter o tipo da expressão de criação de objeto para ver se ele é o ImmutableArray\<T > tipo. Use o modelo semântico novamente para obter informações de símbolo para o tipo de símbolo (ImmutableArray) na expressão de criação de objeto. Insira a seguinte linha de código no final da função:

```csharp
var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as INamedTypeSymbol;
```

Porque seu analisador precisa lidar com código incompleto ou incorreto em buffers do editor (por exemplo, há uma falta `using` instrução), você deve verificar se há `symbolInfo` sendo `null`. Você precisa obter um tipo nomeado (INamedTypeSymbol) a partir do objeto de informações de símbolo para concluir a análise.

**Compare os tipos.** Como há um tipo genérico aberto de T, que estamos procurando e o tipo no código é um tipo genérico concreto, consultar as informações de símbolo para o qual o tipo é construído a partir (um tipo genérico aberto) e comparar esse resultado com `immutableArrayOfTType`. Digite o seguinte no final do método:

```csharp
if (symbolInfo != null &&
    symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
{}
```

**O diagnóstico de relatório.** O diagnóstico de emissão de relatórios é muito fácil. Você usa a regra criada para você no modelo de projeto, que é definido antes do método Initialize. Como essa situação no código é um erro, você pode alterar a linha que é inicializado a regra para substituir `DiagnosticSeverity.Warning` (Rabisco verde) com `DiagnosticSeverity.Error` (uma linha ondulada vermelha). Inicializa o restante da regra dos recursos que você editou perto do início do passo a passo. Você também precisa informar o local para o rabisco, que é o local da especificação de tipo da expressão de criação de objeto. Digite esse código de `if` bloco:

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
```

Sua função deve ser semelhante isso (talvez formatado de maneira diferente):

```csharp
private void AnalyzeObjectCreation(SyntaxNodeAnalysisContext context)
{
    var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
    var immutableArrayOfTType =
        context.SemanticModel
               .Compilation
               .GetTypeByMetadataName(
                   "System.Collections.Immutable.ImmutableArray`1");
    var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as
        INamedTypeSymbol;
    if (symbolInfo != null &&
        symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
    {
        context.ReportDiagnostic(
            Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
    }
}
```

Remova o ponto de interrupção para que você pode ver seu trabalho analyzer (e parar a retornar para a primeira instância do Visual Studio). Arraste o ponteiro de execução para o início do método e pressione **F5** para continuar a execução. Quando você alternar de volta para a segunda instância do Visual Studio, o compilador será iniciado examinar o código novamente, e ele chamará seu analisador. Você pode ver um rabisco sob `ImmutableType<int>`.

## <a name="adding-a-code-fix-for-the-code-issue"></a>Adicionando uma "correção de código" para o problema de código

Antes de começar, feche a segunda instância do Visual Studio e parar a depuração na primeira instância do Visual Studio (em que você está desenvolvendo o analyzer).

**Adicione uma nova classe.** Use o menu de atalho (botão direito do ponteiro) no nó do projeto na **Gerenciador de soluções** e optar por adicionar um novo item. Adicione uma classe chamada `BuildCodeFixProvider`. Essa classe precisa ser derivada de `CodeFixProvider`, e você precisará usar **Ctrl**+**.** (ponto) para invocar a correção de código que adiciona o correto `using` instrução. Essa classe também precisa ser anotada com `ExportCodeFixProvider` atributo e você precisará adicionar uma `using` instrução para resolver o `LanguageNames` enum. Você deve ter um arquivo de classe com o seguinte código nele:

```csharp
using Microsoft.CodeAnalysis;
using Microsoft.CodeAnalysis.CodeFixes;

namespace ImmutableArrayAnalyzer
{
    [ExportCodeFixProvider(LanguageNames.CSharp)]
    class BuildCodeFixProvider : CodeFixProvider
    {}
```

**Criar um stub de membros derivados.** Agora, coloque o cursor do editor no identificador `CodeFixProvider` e pressione **Ctrl**+**.** (ponto) para criar um stub a implementação para essa classe base abstrata. Isso gera uma propriedade e um método para você.

**Implementa a propriedade.** Preencha a `FixableDiagnosticIds` da propriedade `get` corpo pelo código a seguir:

```csharp
return ImmutableArray.Create(ImmutableArrayAnalyzerAnalyzer.DiagnosticId);
```

Roslyn reúne diagnósticos e correções por esses identificadores que são apenas cadeias de caracteres de correspondência. O modelo de projeto gerado uma ID de diagnóstico para você, e você é livre para alterá-lo. O código na propriedade retorna apenas a ID da classe do analisador.

**O método RegisterCodeFixAsync recebe um contexto.** O contexto é importante porque uma correção de código pode aplicar a vários diagnósticos, ou pode haver mais de um problema em uma linha de código. Se você digitar "contexto". no corpo do método, a lista de preenchimento do IntelliSense mostrará alguns membros úteis. Há um membro de CancellationToken que você pode verificar para ver se algo que deseja cancelar a correção. Há um membro de documento que tem muitos membros úteis e permite que você obtenha a objetos de modelo de projeto e solução. Há um Span membro que é o início e final do local do código especificado quando você relatou que o diagnóstico.

**Tornar o método a ser assíncrono.** A primeira coisa que você precisa fazer é corrigir a declaração de método gerado para ser um `async` método. A correção de código de stub a implementação de uma classe abstrata não inclui o `async` palavra-chave mesmo que o método retorna um `Task`.

**Obtenha a raiz da árvore de sintaxe.** Para modificar o código que você precisa para produzir uma nova árvore de sintaxe com as alterações a correção de código faz. Você precisa de `Document` de contexto para chamar `GetSyntaxRootAsync`. Isso é um método assíncrono porque não há trabalho desconhecido para obter a árvore de sintaxe, possivelmente incluindo obtendo o arquivo de disco, analisá-lo e criar o modelo de código do Roslyn para ele. IU do Visual Studio deve ser responsivo durante esse tempo, qual usando `async` habilita. Substitua a linha de código no método com o seguinte:

```csharp
var root = await context.Document
                        .GetSyntaxRootAsync(context.CancellationToken);
```

**Localize o nó com o problema.** Passe no alcance do contexto, mas o nó que você encontre pode não ser o código que você precisa alterar. O diagnóstico relatado fornecido somente o alcance para o identificador de tipo (em que a linha ondulada pertencia), mas você precisa substituir a expressão de criação de objeto inteiro, incluindo o `new` palavra-chave no início e os parênteses no final. Adicione o seguinte código ao seu método (e usar **Ctrl**+**.** Para adicionar um `using` instrução para `ObjectCreationExpressionSyntax`):

```csharp
var objectCreation = root.FindNode(context.Span)
                         .FirstAncestorOrSelf<ObjectCreationExpressionSyntax>();
```

**Registre-se a correção de código para a lâmpada da interface do usuário.** Quando você registra a correção de código, Roslyn se conecta à lâmpada do Visual Studio da interface do usuário automaticamente. Os usuários finais verão usarem **Ctrl**+**.** (período) quando seu analisador rabisca uma má `ImmutableArray<T>` uso do construtor. Como seu provedor de correção de código é executado somente quando há um problema, você pode supor que você tem a expressão de criação de objeto que estava procurando. Do parâmetro de contexto, você pode registrar a nova correção de código, adicionando o seguinte código ao final da `RegisterCodeFixAsync` método:

```csharp
context.RegisterCodeFix(
            CodeAction.Create("Use ImmutableArray<T>.Empty",
                              c => ChangeToImmutableArrayEmpty(objectCreation,
                                                               context.Document,
                                                               c)),
            context.Diagnostics[0]);
```

Você precisa colocar o cursor do editor do identificador `CodeAction`, em seguida, use **Ctrl**+**.** (ponto) para adicionar o apropriada `using` instrução para esse tipo.

Em seguida, coloque o cursor do editor na `ChangeToImmutableArrayEmpty` identificador e uso **Ctrl**+**.** novamente, para gerar o stub do método para você.

Este último trecho de código adicionados por você registra a correção de código, passando um `CodeAction` e a ID de diagnóstico para o tipo de problema encontrado. Neste exemplo, há apenas um ID de diagnóstico que esse código fornece correções para, portanto, você pode passar apenas o primeiro elemento da matriz de IDs de diagnóstico. Quando você cria o `CodeAction`, você passa o texto que a lâmpada da interface do usuário deve usar como uma descrição da correção do código. Você também pode passar em uma função que usa um CancellationToken e retorna um novo documento. O novo documento terá uma nova árvore de sintaxe que inclui seu código com patches que chama `ImmutableArray.Empty`. Este trecho de código usa uma lambda, de modo que ele pode se fechar sobre o nó de objectCreation e documento do contexto.

**Construa a nova árvore de sintaxe.** No `ChangeToImmutableArrayEmpty` cujo stub que você gerou anteriormente, insira a linha de código do método: `ImmutableArray<int>.Empty;`. Se você exibir o **Syntax Visualizer** janela da ferramenta novamente, você pode ver essa sintaxe é um nó do SimpleMemberAccessExpression. Isso é o que esse método precisa construir e retornar em um novo documento.

A primeira alteração `ChangeToImmutableArrayEmpty` é adicionar `async` antes de `Task<Document>` porque os geradores de código não é possível supor que o método deve ser assíncrono.

Preencha o corpo pelo código a seguir para que o método é semelhante ao seguinte:

```csharp
private async Task<Document> ChangeToImmutableArrayEmpty(
    ObjectCreationExpressionSyntax objectCreation, Document document,
    CancellationToken c)
{
    var generator = SyntaxGenerator.GetGenerator(document);
    var memberAccess =
        generator.MemberAccessExpression(objectCreation.Type, "Empty");
    var oldRoot = await document.GetSyntaxRootAsync(c);
    var newRoot = oldRoot.ReplaceNode(objectCreation, memberAccess);
    return document.WithSyntaxRoot(newRoot);
}
```

Você precisará colocar o cursor do editor na `SyntaxGenerator` identificador e uso **Ctrl**+**.** (ponto) para adicionar o apropriada `using` instrução para esse tipo.

Esse código usa `SyntaxGenerator`, que é um tipo útil para a criação de novo código. Depois de obter um gerador para o documento que tem o problema de código `ChangeToImmutableArrayEmpty` chamadas `MemberAccessExpression`, passando o tipo que tem o membro que desejamos acessar e passando o nome do membro como uma cadeia de caracteres.

Em seguida, o método de busca a raiz do documento, e como isso pode envolver trabalho arbitrário em geral, o código aguarda essa chamada e passa o token de cancelamento. Modelos de código do Roslyn são imutáveis, semelhante a trabalhar com uma cadeia de caracteres do .NET; Quando você atualiza a cadeia de caracteres, obtenha um novo objeto de cadeia de caracteres de retorno. Quando você chama `ReplaceNode`, você recebe um novo nó raiz. A maioria da árvore de sintaxe é compartilhado (porque é imutável), mas o `objectCreation` nó é substituído pelo `memberAccess` nó, bem como todos os nós pai até a raiz da árvore de sintaxe.

## <a name="try-your-code-fix"></a>Experimente a correção de código

Agora, você pode pressionar **F5** para executar o seu analisador em uma segunda instância do Visual Studio. Abra o projeto de console que você usou antes. Agora você verá a lâmpada aparecer onde sua nova expressão de criação de objeto é para `ImmutableArray<int>`. Se você pressionar **Ctrl**+**.** (período), em seguida, você verá seu código corrigir e você verá uma visualização de diferença do código gerado automaticamente na lâmpada da interface do usuário. Roslyn o criará para você.

**Dica de Pro:** se você iniciar a segunda instância do Visual Studio e você não vir a lâmpada com a correção de código, talvez seja necessário limpar o cache de componente do Visual Studio. A limpeza do cache força o Visual Studio para examinar novamente os componentes, portanto, o Visual Studio deve pegar seu componente mais recente. Primeiro, desligue a segunda instância do Visual Studio. Em seguida, na **Windows Explorer**, navegue até *%LOCALAPPDATA%\Microsoft\VisualStudio\15.0Roslyn\\*. (O "15.0" muda com a versão com o Visual Studio). Excluir o subdiretório *ComponentModelCache*.

## <a name="talk-video-and-finish-code-project"></a>Se comunicar com vídeo e concluir o projeto de código

Você pode ver neste exemplo, desenvolvidos e discutido mais detalhadamente em [essa conversa](https://channel9.msdn.com/events/Build/2015/3-725). Palestra demonstra o analisador de trabalho e orienta você por meio de compilá-lo.

Você pode ver o código concluído [aqui](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers). As subpastas *DoNotUseImmutableArrayCollectionInitializer* e *DoNotUseImmutableArrayCtor* cada um tem um arquivo c# para localizar problemas e correções de um arquivo c# que implementa o código que mostram-se das Visual Studio lâmpada da interface do usuário. Observe que o código concluído tem um pouco mais de abstração para evitar buscando a ImmutableArray\<T > tipo de objeto repetidamente. Ele usa aninhadas ações registradas para salvar o objeto de tipo em um contexto que está disponível sempre que as ações de sub (analisar a criação do objeto e analisar as inicializações de coleção) execute.

## <a name="see-also"></a>Consulte também

* [\\Palestra de \Build 2015](https://channel9.msdn.com/events/Build/2015/3-725)
* [Código completo no GitHub](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)
* [Vários exemplos no GitHub, agrupados em três tipos de analisadores](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)
* [Outros documentos no site do GitHub OSS](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
* [Regras do FxCop implementadas com analisadores de Roslyn no GitHub](https://github.com/dotnet/roslyn/tree/master/src/Diagnostics/FxCop)
