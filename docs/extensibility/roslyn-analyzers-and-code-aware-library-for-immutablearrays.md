---
title: Analisadores de Roslyn e bibliotecas com reconhecimento de código para ImmutableArrays
description: Saiba como criar um analisador de Roslyn do mundo real para capturar erros comuns ao usar o pacote NuGet System. Collections. imutável.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0b0afa22-3fca-4d59-908e-352464c1d903
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e3bdcc9c35f5acaf9937bd18b0160f9e5a58161c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105060571"
---
# <a name="roslyn-analyzers-and-code-aware-library-for-immutablearrays"></a>Analisadores de Roslyn e biblioteca com reconhecimento de código para ImmutableArrays

O [.net Compiler Platform](https://github.com/dotnet/roslyn) ("Roslyn") ajuda você a criar bibliotecas com reconhecimento de código. Uma biblioteca com reconhecimento de código fornece a funcionalidade que você pode usar e ferramentas (analisadores Roslyn) para ajudá-lo a usar a biblioteca da melhor maneira ou para evitar erros. Este tópico mostra como criar um analisador de Roslyn do mundo real para capturar erros comuns ao usar o pacote NuGet [System. Collections. imutável](https://www.nuget.org/packages/System.Collections.Immutable) . O exemplo também demonstra como fornecer uma correção de código para um problema de código encontrado pelo analisador. Os usuários veem correções de código na interface do usuário da lâmpada do Visual Studio e podem aplicar uma correção para o código automaticamente.

## <a name="get-started"></a>Introdução

Você precisa do seguinte para compilar este exemplo:

* Visual Studio 2015 (não é uma edição Express) ou uma versão posterior. Você pode usar o [Visual Studio Community Edition](https://visualstudio.microsoft.com/vs/community/) gratuito
* [SDK do Visual Studio](../extensibility/visual-studio-sdk.md). Você também pode, ao instalar o Visual Studio, verificar **ferramentas de extensibilidade do Visual Studio** em **ferramentas comuns** para instalar o SDK ao mesmo tempo. Se você já tiver instalado o Visual Studio, também poderá instalar esse SDK indo até o **arquivo** de menu principal  >  **novo**  >  **projeto**, escolhendo **C#** no painel de navegação à esquerda e escolhendo **extensibilidade**. Quando você escolhe o modelo de projeto de navegação estrutural "**instalar o ferramentas de extensibilidade do Visual Studio**", ele solicita que você baixe e instale o SDK.
* [SDK do .net Compiler Platform ("Roslyn")](https://marketplace.visualstudio.com/items?itemName=VisualStudioProductTeam.NETCompilerPlatformSDK). Você também pode instalar esse SDK indo até o **arquivo** de menu principal  >  **novo**  >  **projeto**, escolhendo **C#** no painel de navegação esquerdo e, em seguida, escolhendo **extensibilidade**. Quando você escolhe "**baixar o modelo de projeto breadcrumb do SDK do .net Compiler Platform**", ele solicita que você baixe e instale o SDK. Este SDK inclui o [Syntax Visualizer Roslyn](https://github.com/dotnet/roslyn/blob/master/docs/wiki/Syntax-Visualizer.md). Essa ferramenta útil ajuda a descobrir quais tipos de modelo de código você deve procurar em seu analisador. A infraestrutura do analisador chama seu código para tipos de modelo de código específicos, para que seu código seja executado somente quando necessário e possa se concentrar apenas na análise de código relevante.

## <a name="whats-the-problem"></a>Qual é o problema?

Imagine que você forneça uma biblioteca com suporte a ImmutableArray (por exemplo, <xref:System.Collections.Immutable.ImmutableArray%601?displayProperty=fullName> ). Os desenvolvedores de C# têm muita experiência com as matrizes .NET. No entanto, devido à natureza das técnicas de ImmutableArrays e otimização usadas na implementação, as intuições do desenvolvedor de C# fazem com que os usuários da sua biblioteca escrevam código quebrado, conforme explicado abaixo. Além disso, os usuários não veem seus erros até o tempo de execução, que não é a experiência de qualidade em que eles são usados no Visual Studio com o .NET.

Os usuários estão familiarizados com a escrita de código como o seguinte:

```csharp
var a1 = new int[0];
Console.WriteLine("a1.Length = { 0}", a1.Length);
var a2 = new int[] { 1, 2, 3, 4, 5 };
Console.WriteLine("a2.Length = { 0}", a2.Length);
```

Criar matrizes vazias para preencher com linhas de código subsequentes e usar a sintaxe do inicializador de coleção é familiar para os desenvolvedores de C#. No entanto, escrever o mesmo código para uma falha de ImmutableArray no tempo de execução:

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = { 0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = { 0}", b2.Length);
```

O primeiro erro ocorre devido à implementação do ImmutableArray usando uma struct para encapsular o armazenamento de dados subjacente. As structs devem ter construtores sem parâmetros para que `default(T)` as expressões possam retornar structs com todos os membros zero ou nulos. Quando o código acessa `b1.Length` , há um erro de desreferência nula de tempo de execução porque não há nenhuma matriz de armazenamento subjacente no struct ImmutableArray. A maneira correta de criar um ImmutableArray vazio é `ImmutableArray<int>.Empty` .

O erro com inicializadores de coleção ocorre porque o `ImmutableArray.Add` método retorna novas instâncias cada vez que você a chama. Como ImmutableArrays nunca é alterado, quando você adiciona um novo elemento, você obtém um novo objeto ImmutableArray (que pode compartilhar o armazenamento por motivos de desempenho com um ImmutableArray existente anteriormente). Como `b2` aponta para o primeiro ImmutableArray antes de chamar `Add()` cinco vezes, `b2` é um ImmutableArray padrão. O comprimento da chamada nele também falha com um erro de cancelamento de referência nulo. A maneira correta de inicializar um ImmutableArray sem chamar manualmente Add é usar `ImmutableArray.CreateRange(new int[] {1, 2, 3, 4, 5})` .

## <a name="find-relevant-syntax-node-types-to-trigger-your-analyzer"></a>Localizar tipos de nó de sintaxe relevantes para disparar seu analisador

 Para começar a criar o analisador, primeiro descubra o tipo de SyntaxNode que você precisa procurar. Inicie o **Syntax Visualizer** no menu **Exibir**  >  **outros**  >  **Roslyn** do Windows Syntax Visualizer.

Coloque o cursor do editor na linha que declara `b1` . Você verá a Syntax Visualizer mostra que você está em um `LocalDeclarationStatement` nó da árvore de sintaxe. Esse nó tem um `VariableDeclaration` , que, por sua vez, tem um `VariableDeclarator` , que por sua vez tem um `EqualsValueClause` , e finalmente há um `ObjectCreationExpression` . À medida que você clica na árvore de Syntax Visualizer de nós, a sintaxe na janela do editor é destacada para mostrar o código representado por esse nó. Os nomes dos subtipos SyntaxNode correspondem aos nomes usados na gramática do C#.

## <a name="create-the-analyzer-project"></a>Criar o projeto do analisador

No menu principal, escolha **arquivo**  >  **novo**  >  **projeto**. Na caixa de diálogo **novo projeto** , em projetos **C#** na barra de navegação à esquerda, escolha **extensibilidade** e, no painel direito, escolha o **analisador com** o modelo de projeto de correção de código. Insira um nome e confirme a caixa de diálogo.

O modelo abre um arquivo *DiagnosticAnalyzer. cs* . Escolha essa guia buffer do editor. Esse arquivo tem uma classe do analisador (formada pelo nome que você deu ao projeto) derivado de `DiagnosticAnalyzer` (um tipo de API Roslyn). Sua nova classe tem um `DiagnosticAnalyzerAttribute` declarando que o analisador é relevante para a linguagem C# para que o compilador descubra e carregue seu analisador.

```csharp
[DiagnosticAnalyzer(LanguageNames.CSharp)]
public class ImmutableArrayAnalyzerAnalyzer : DiagnosticAnalyzer
{}
```

Você pode implementar um analisador usando Visual Basic que tem como alvo o código C#, e vice-versa. É mais importante no DiagnosticAnalyzerAttribute escolher se o analisador tem como alvo um idioma ou ambos. Analisadores mais sofisticados que exigem modelagem detalhada do idioma só podem ter como alvo um único idioma. Se o analisador, por exemplo, verificar apenas nomes de tipo ou nomes de membros públicos, pode ser possível usar as ofertas Roslyn de modelo de linguagem comum em Visual Basic e C#. Por exemplo, o FxCop avisa que uma classe implementa <xref:System.Runtime.Serialization.ISerializable> , mas a classe não tem o <xref:System.SerializableAttribute> atributo é independente de linguagem e funciona para o código de Visual Basic e C#.

## <a name="initialize-the-analyzer"></a>Inicializar o analisador

 Role um pouco na `DiagnosticAnalyzer` classe para ver o `Initialize` método. O compilador chama esse método ao ativar um analisador. O método usa um `AnalysisContext` objeto que permite que o seu analisador Obtenha informações de contexto e registre retornos de chamada para eventos para os tipos de código que você deseja analisar.

```csharp
public override void Initialize(AnalysisContext context) {}
```

Abra uma nova linha nesse método e digite "Context". para ver uma lista de conclusão do IntelliSense. Você pode ver na lista de conclusão que há muitos `Register...` métodos para lidar com vários tipos de eventos. Por exemplo, o primeiro, `RegisterCodeBlockAction` , retorna ao seu código para um bloco, que geralmente é um código entre chaves. O registro para um bloco também retorna ao seu código para o inicializador de um campo, o valor fornecido para um atributo ou o valor de um parâmetro opcional.

Como outro exemplo, `RegisterCompilationStartAction` o retorna ao seu código no início de uma compilação, o que é útil quando você precisa coletar o estado em vários locais. Você pode criar uma estrutura de dados, digamos, para coletar todos os símbolos usados e sempre que seu analisador for chamado de volta para alguma sintaxe ou símbolo, você poderá salvar informações sobre cada local na estrutura de dados. Quando for chamado de volta devido ao término da compilação, você poderá analisar todos os locais que salvou, por exemplo, para relatar quais símbolos o código usa de cada `using` instrução.

Usando o **Syntax Visualizer**, você aprendeu que deseja ser chamado quando o compilador processa uma objectcreationname. Você usa este código para configurar o retorno de chamada:

```csharp
context.RegisterSyntaxNodeAction(c => AnalyzeObjectCreation(c),
                                 SyntaxKind.ObjectCreationExpression);
```

Você se registra em um nó de sintaxe e filtra apenas nós de sintaxe de criação de objetos. Por convenção, os autores do analisador usam um lambda ao registrar ações, o que ajuda a manter os analisadores sem monitoração de estado. Você pode usar a geração de recursos do Visual Studio a **partir do uso** para criar o `AnalyzeObjectCreation` método. Isso gera o tipo correto de parâmetro de contexto também.

## <a name="set-properties-for-users-of-your-analyzer"></a>Definir propriedades para usuários do seu analisador

Para que seu analisador seja exibido na interface do usuário do Visual Studio adequadamente, procure e modifique a seguinte linha de código para identificar seu analisador:

```csharp
internal const string Category = "Naming";
```

Alterar `"Naming"` para `"API Guidance"`.

Em seguida, localize e abra o arquivo *Resources. resx* em seu projeto usando o **Gerenciador de soluções**. Você pode inserir uma descrição para seu analisador, título, etc. Você pode alterar o valor para todos eles para `"Don't use ImmutableArray<T> constructor"` por enquanto. Você pode colocar argumentos de formatação de cadeia de caracteres na cadeia de caracteres ( {0} , {1} , etc.) e, posteriormente, ao chamar `Diagnostic.Create()` , você pode fornecer uma `params` matriz de argumentos a serem passados.

## <a name="analyze-an-object-creation-expression"></a>Analisar uma expressão de criação de objeto

O `AnalyzeObjectCreation` método usa um tipo diferente de contexto fornecido pela estrutura do analisador de código. O `Initialize` método `AnalysisContext` permite que você registre retornos de chamada de ação para configurar o analisador. O `SyntaxNodeAnalysisContext` , por exemplo, tem um `CancellationToken` que você pode percorrer. Se um usuário começar a digitar no editor, o Roslyn cancelará a execução de analisadores para salvar o trabalho e melhorar o desempenho. Como outro exemplo, esse contexto tem uma propriedade node que retorna o nó de sintaxe de criação de objeto.

Obtenha o nó, que você pode assumir é o tipo para o qual você filtrou a ação do nó de sintaxe:

```csharp
var objectCreation = (ObjectCreationExpressionSyntax)context.Node;
```

### <a name="launch-visual-studio-with-your-analyzer-the-first-time"></a>Iniciar o Visual Studio com o analisador pela primeira vez

Inicie o Visual Studio criando e executando seu analisador (pressione **F5**). Como o projeto de inicialização no **Gerenciador de soluções** é o projeto VSIX, executar seu código cria seu código e um VSIX e, em seguida, inicia o Visual Studio com esse VSIX instalado. Quando você inicia o Visual Studio dessa forma, ele é iniciado com um hive de registro distinto para que seu uso principal do Visual Studio não seja afetado por suas instâncias de teste durante a criação de analisadores. Na primeira vez que você iniciar dessa forma, o Visual Studio fará várias inicializações semelhantes a quando você iniciou o Visual Studio pela primeira vez depois de instalá-lo.

Crie um projeto de console e, em seguida, insira o código de matriz em seu método principal de aplicativos de console:

```csharp
var b1 = new ImmutableArray<int>();
Console.WriteLine("b1.Length = {0}", b1.Length);
var b2 = new ImmutableArray<int> { 1, 2, 3, 4, 5 };
Console.WriteLine("b2.Length = {0}", b2.Length);
```

As linhas de código `ImmutableArray` têm ondulado porque você precisa obter o pacote NuGet imutável e adicionar uma `using` instrução ao seu código. Pressione o botão de ponteiro à direita no nó do projeto na **Gerenciador de soluções** e escolha **gerenciar pacotes NuGet**. No Gerenciador do NuGet, digite "imutável" na caixa de pesquisa e escolha o item **System. Collections. imutável** (não escolha **Microsoft. BCL. imutável**) no painel esquerdo e pressione o botão **instalar** no painel direito. A instalação do pacote adiciona uma referência às referências do projeto.

Você ainda verá ondulados vermelhos em `ImmutableArray` , portanto, coloque o cursor nesse identificador e pressione **Ctrl** + **.** (ponto) para abrir o menu de correção sugerido e escolher Adicionar a instrução apropriada `using` .

**Salve tudo e feche** a segunda instância do Visual Studio por enquanto para colocá-lo em um estado limpo para continuar.

## <a name="finish-the-analyzer-using-edit-and-continue"></a>Concluir o analisador usando editar e continuar

Na primeira instância do Visual Studio, defina um ponto de interrupção no início do `AnalyzeObjectCreation` método pressionando **F9** com o cursor na primeira linha.

Inicie o analisador novamente com **F5** e, na segunda instância do Visual Studio, abra novamente o aplicativo de console que você criou na última vez.

Você retorna à primeira instância do Visual Studio no ponto de interrupção porque o compilador Roslyn viu uma expressão de criação de objeto e se chamou em seu analisador.

**Obtenha o nó de criação do objeto.** Percorra a linha que define a `objectCreation` variável pressionando **F10** e, na **janela imediata** , avalie a expressão `"objectCreation.ToString()"` . Você verá que o nó de sintaxe que a variável aponta é o código `"new ImmutableArray<int>()"` , apenas o que você está procurando.

**Obter ImmutableArray<\> objeto de tipo T.** Você precisa verificar se o tipo que está sendo criado é ImmutableArray. Primeiro, você obtém o objeto que representa esse tipo. Você verifica os tipos usando o modelo semântico para garantir que tem exatamente o tipo correto e não compara a cadeia de caracteres de `ToString()` . Insira a seguinte linha de código no final da função:

```csharp
var immutableArrayOfTType =
    context.SemanticModel
           .Compilation
           .GetTypeByMetadataName("System.Collections.Immutable.ImmutableArray`1");
```

Você designa tipos genéricos em metadados com acentos (') e o número de parâmetros genéricos. É por isso que você não vê "... ImmutableArray \<T> "no nome de metadados.

O modelo semântico tem muitas coisas úteis que permitem fazer perguntas sobre símbolos, fluxo de dados, tempo de vida variável etc. O Roslyn separa os nós de sintaxe do modelo semântico para vários motivos de engenharia (desempenho, modelagem de código errôneo, etc.). Você deseja que o modelo de compilação pesquise informações contidas em referências para uma comparação precisa.

Você pode arrastar o ponteiro de execução amarela no lado esquerdo da janela do editor. Arraste-o para a linha que define a `objectCreation` variável e percorra sua nova linha de código usando **F10**. Se você passar o ponteiro do mouse sobre a variável `immutableArrayOfType` , verá que encontramos o tipo exato no modelo semântico.

**Obter o tipo da expressão de criação de objeto.** "Type" é usado de algumas maneiras neste artigo, mas isso significa que se você tiver a expressão "New foo", precisará obter um modelo de foo. Você precisa obter o tipo da expressão de criação de objeto para ver se ele é o \<T> tipo ImmutableArray. Use o modelo semântico novamente para obter informações de símbolo para o símbolo de tipo (ImmutableArray) na expressão de criação de objeto. Insira a seguinte linha de código no final da função:

```csharp
var symbolInfo = context.SemanticModel.GetSymbolInfo(objectCreation.Type).Symbol as INamedTypeSymbol;
```

Como seu analisador precisa manipular código incompleto ou incorreto nos buffers do editor (por exemplo, há uma `using` instrução ausente), você deve verificar se ele `symbolInfo` está sendo `null` . Você precisa obter um tipo nomeado (INamedTypeSymbol) do objeto de informações de símbolo para concluir a análise.

**Compare os tipos.** Como há um tipo genérico aberto de T que estamos procurando e o tipo no código é um tipo genérico concreto, você consulta as informações de símbolo para o que o tipo é construído (um tipo genérico aberto) e compara esse resultado com `immutableArrayOfTType` . Insira o seguinte no final do método:

```csharp
if (symbolInfo != null &&
    symbolInfo.ConstructedFrom.Equals(immutableArrayOfTType))
{}
```

**Relatar o diagnóstico.** Relatar o diagnóstico é muito fácil. Você usa a regra criada para você no modelo de projeto, que é definida antes do método Initialize. Como essa situação no código é um erro, você pode alterar a linha que a regra inicializada para substituir `DiagnosticSeverity.Warning` (rabisco verde) com `DiagnosticSeverity.Error` (ondulado vermelho). O restante da regra é inicializado a partir dos recursos que você editou perto do início do passo a passos. Você também precisa relatar o local para o rabisco, que é o local da especificação de tipo da expressão de criação de objeto. Insira este código no `if` bloco:

```csharp
context.ReportDiagnostic(Diagnostic.Create(Rule, objectCreation.Type.GetLocation()));
```

Sua função deve ser parecida com esta (talvez formatada de forma diferente):

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

Remova o ponto de interrupção para que você possa ver seu analisador funcionando (e pare de retornar para a primeira instância do Visual Studio). Arraste o ponteiro de execução para o início do método e pressione **F5** para continuar a execução. Quando você alternar de volta para a segunda instância do Visual Studio, o compilador começará a examinar o código novamente e ele chamará seu analisador. Você pode ver um rabisco em `ImmutableType<int>` .

## <a name="adding-a-code-fix-for-the-code-issue"></a>Adicionar uma "correção de código" para o problema de código

Antes de começar, feche a segunda instância do Visual Studio e interrompa a depuração na primeira instância do Visual Studio (em que você está desenvolvendo o analisador).

**Adicione uma nova classe.** Use o menu de atalho (botão do ponteiro à direita) no nó do projeto na **Gerenciador de soluções** e escolha Adicionar um novo item. Adicione uma classe chamada `BuildCodeFixProvider` . Essa classe precisa derivar de `CodeFixProvider` e você precisará usar **Ctrl** + **.** (ponto) para invocar a correção de código que adiciona a `using` instrução correta. Essa classe também precisa ser anotada com `ExportCodeFixProvider` o atributo e você precisará adicionar uma `using` instrução para resolver a `LanguageNames` enumeração. Você deve ter um arquivo de classe com o seguinte código:

```csharp
using Microsoft.CodeAnalysis;
using Microsoft.CodeAnalysis.CodeFixes;

namespace ImmutableArrayAnalyzer
{
    [ExportCodeFixProvider(LanguageNames.CSharp)]
    class BuildCodeFixProvider : CodeFixProvider
    {}
```

**Stub de membros derivados.** Agora, coloque o cursor do editor no identificador `CodeFixProvider` e pressione **Ctrl** + **.** (ponto) para desfragmentar a implementação para essa classe base abstrata. Isso gera uma propriedade e um método para você.

**Implemente a propriedade.** Preencha o `FixableDiagnosticIds` corpo da propriedade `get` com o seguinte código:

```csharp
return ImmutableArray.Create(ImmutableArrayAnalyzerAnalyzer.DiagnosticId);
```

O Roslyn reúne diagnósticos e correções combinando esses identificadores, que são apenas cadeias de caracteres. O modelo de projeto gerou uma ID de diagnóstico para você e você está livre para alterá-la. O código na propriedade apenas retorna a ID da classe do analisador.

**O método RegisterCodeFixAsync usa um contexto.** O contexto é importante porque uma correção de código pode ser aplicada a vários diagnósticos ou pode haver mais de um problema em uma linha de código. Se você digitar "Context". no corpo do método, a lista de conclusão do IntelliSense mostrará alguns membros úteis. Há um membro CancellationToken que você pode verificar para ver se algo deseja cancelar a correção. Há um membro de documento que tem muitos membros úteis e permite que você obtenha os objetos de modelo de projeto e de solução. Há um membro span que é o início e o fim do local do código especificado quando você relatou o diagnóstico.

**Faça com que o método seja assíncrono.** A primeira coisa que você precisa fazer é corrigir a declaração do método gerado como um `async` método. A correção de código para arranque a implementação de uma classe abstrata não inclui a `async` palavra-chave, embora o método retorne um `Task` .

**Obtenha a raiz da árvore de sintaxe.** Para modificar o código, você precisa produzir uma nova árvore de sintaxe com as alterações feitas por sua correção de código. Você precisa do `Document` contexto a ser chamado `GetSyntaxRootAsync` . Esse é um método assíncrono porque há um trabalho desconhecido para obter a árvore de sintaxe, possivelmente incluindo obter o arquivo do disco, analisá-lo e criar o modelo de código Roslyn para ele. A interface do usuário do Visual Studio deve ser responsiva durante esse tempo, o que usa `async` habilitações. Substitua a linha de código no método pelo seguinte:

```csharp
var root = await context.Document
                        .GetSyntaxRootAsync(context.CancellationToken);
```

**Localize o nó com o problema.** Você passa a extensão do contexto, mas o nó que você encontrar pode não ser o código que você precisa alterar. O diagnóstico relatado forneceu apenas o span para o identificador de tipo (onde o rabisco pertencia), mas você precisa substituir toda a expressão de criação de objeto, incluindo a `new` palavra-chave no início e os parênteses no final. Adicione o código a seguir ao seu método (e use **Ctrl** + **.** para adicionar uma `using` instrução para `ObjectCreationExpressionSyntax` ):

```csharp
var objectCreation = root.FindNode(context.Span)
                         .FirstAncestorOrSelf<ObjectCreationExpressionSyntax>();
```

**Registre sua correção de código para a interface do usuário de lâmpada.** Quando você registra sua correção de código, o Roslyn conecta-se automaticamente à interface do usuário de lâmpada do Visual Studio. Os usuários finais verão que podem usar **Ctrl** + **.** (ponto) quando o analisador rabisca um uso inadequado de `ImmutableArray<T>` Construtor. Como seu provedor de correção de código só é executado quando há um problema, você pode pressupor que tem a expressão de criação de objeto que estava procurando. No parâmetro de contexto, você pode registrar a nova correção de código adicionando o seguinte código ao final do `RegisterCodeFixAsync` método:

```csharp
context.RegisterCodeFix(
            CodeAction.Create("Use ImmutableArray<T>.Empty",
                              c => ChangeToImmutableArrayEmpty(objectCreation,
                                                               context.Document,
                                                               c)),
            context.Diagnostics[0]);
```

Você precisa posicionar o cursor do editor no identificador e, `CodeAction` em seguida, usar **Ctrl** + **.** (ponto) para adicionar a `using` instrução apropriada para esse tipo.

Em seguida, coloque o cursor do editor no `ChangeToImmutableArrayEmpty` identificador e use **Ctrl** + **.** novamente para gerar esse stub de método para você.

Este último trecho de código que você adicionou registra a correção de código passando um `CodeAction` e a ID de diagnóstico para o tipo de problema encontrado. Neste exemplo, há apenas uma ID de diagnóstico para a qual esse código fornece correções para que você possa apenas passar o primeiro elemento da matriz de IDs de diagnóstico. Ao criar o `CodeAction` , você passa o texto que a interface do usuário da lâmpada deve usar como uma descrição da correção do código. Você também passa uma função que usa um CancellationToken e retorna um novo documento. O novo documento tem uma nova árvore de sintaxe que inclui o código com patch que chama `ImmutableArray.Empty` . Esse trecho de código usa um lambda para que possa fechar o nó objectcreation e o documento do contexto.

**Construa a nova árvore de sintaxe.** No `ChangeToImmutableArrayEmpty` método cujo stub você gerou anteriormente, insira a linha de código: `ImmutableArray<int>.Empty;` . Se você exibir a janela de ferramentas de **Syntax Visualizer** novamente, poderá ver que essa sintaxe é um nó SimpleMemberAccessExpression. É isso que esse método precisa construir e retornar em um novo documento.

A primeira alteração para `ChangeToImmutableArrayEmpty` é adicionar `async` antes `Task<Document>` porque os geradores de código não podem pressupor que o método deve ser Async.

Preencha o corpo com o código a seguir para que o método tenha uma aparência semelhante à seguinte:

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

Será necessário colocar o cursor do editor no `SyntaxGenerator` identificador e usar **Ctrl** + **.** (ponto) para adicionar a `using` instrução apropriada para esse tipo.

Esse código usa `SyntaxGenerator` , que é um tipo útil para construir um novo código. Depois de obter um gerador para o documento que tem o problema de código, `ChangeToImmutableArrayEmpty` chama `MemberAccessExpression` , passando o tipo que tem o membro que desejamos acessar e passando o nome do membro como uma cadeia de caracteres.

Em seguida, o método busca a raiz do documento e, como isso pode envolver um trabalho arbitrário no caso geral, o código aguarda essa chamada e passa o token de cancelamento. Os modelos de código Roslyn são imutáveis, como trabalhar com uma cadeia de caracteres .NET; ao atualizar a cadeia de caracteres, você obtém um novo objeto de cadeia de caracteres em retorno. Ao chamar `ReplaceNode` , você obtém um novo nó raiz. A maior parte da árvore de sintaxe é compartilhada (porque é imutável), mas o `objectCreation` nó é substituído pelo `memberAccess` nó, bem como todos os nós pai até a raiz da árvore de sintaxe.

## <a name="try-your-code-fix"></a>Experimente a correção de código

Agora você pode pressionar **F5** para executar o analisador em uma segunda instância do Visual Studio. Abra o projeto de console que você usou antes. Agora você deve ver a lâmpada exibida onde é a nova expressão de criação de objeto `ImmutableArray<int>` . Se você pressionar **Ctrl** + **.** (período), você verá sua correção de código e verá uma visualização de diferença de código gerada automaticamente na interface do usuário da lâmpada. O Roslyn o cria para você.

**Dica de pro:** Se você iniciar a segunda instância do Visual Studio e não vir a lâmpada com a correção do código, talvez seja necessário limpar o cache de componentes do Visual Studio. Limpar o cache força o Visual Studio a examinar novamente os componentes, portanto, o Visual Studio deve selecionar o componente mais recente. Primeiro, desligue a segunda instância do Visual Studio. Em seguida, no **Windows Explorer**, navegue *até \\ %LocalAppData%\Microsoft\VisualStudio\16.0Roslyn*. (O "16,0" muda de versão para versão com o Visual Studio.) Exclua o subdiretório *ComponentModelCache*.

## <a name="talk-video-and-finish-code-project"></a>Converse com o vídeo e o projeto de código de conclusão

Você pode ver este exemplo desenvolvido e abordado mais adiante nesta [conversa](https://channel9.msdn.com/events/Build/2015/3-725). A palestra demonstra o analisador de trabalho e orienta você pela sua criação.

Você pode ver todo o código concluído [aqui](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers). As subpastas *DoNotUseImmutableArrayCollectionInitializer* e *DoNotUseImmutableArrayCtor* têm um arquivo c# para encontrar problemas e um arquivo c# que implementa as correções de código que aparecem na interface do usuário da lâmpada do Visual Studio. Observe que o código concluído tem um pouco mais de abstração para evitar buscar o \<T> objeto do tipo ImmutableArray repetidamente. Ele usa ações registradas aninhadas para salvar o objeto de tipo em um contexto que está disponível sempre que as subações (analisar criação de objeto e as inicializações de coleção de análise) são executadas.

## <a name="see-also"></a>Confira também

* [\\\Build 2015 Talk](https://channel9.msdn.com/events/Build/2015/3-725)
* [Código concluído no GitHub](https://github.com/DustinCampbell/CoreFxAnalyzers/tree/master/Source/CoreFxAnalyzers)
* [Vários exemplos no GitHub, agrupados em três tipos de analisadores](https://github.com/dotnet/roslyn/blob/master/docs/analyzers/Analyzer%20Samples.md)
* [Outros documentos no site de OSS do GitHub](https://github.com/dotnet/roslyn/tree/master/docs/analyzers)
* [Regras do FxCop implementadas com analisadores Roslyn no GitHub](https://github.com/dotnet/roslyn/tree/master/src/Features/Core/Portable/Diagnostics/Analyzers)
