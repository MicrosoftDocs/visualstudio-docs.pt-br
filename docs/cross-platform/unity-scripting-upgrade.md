---
title: Usar o .NET 4.x no Unity
author: therealjohn
ms.author: johmil
ms.date: 08/29/2018
ms.topic: how-to
ms.assetid: E2C9420F-A5D5-4472-9020-2B63FB27A133
ms.technology: vs-unity-tools
ms.workload:
- unity
ms.openlocfilehash: e824951556124f080f14cdd9f440037decf5146f
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815130"
---
# <a name="using-net-4x-in-unity"></a>Usar o .NET 4.x no Unity

C# e .NET, as tecnologias subjacentes ao script do Unity, continuam a receber atualizações, uma vez que a Microsoft as lançou originalmente em 2002. Mas os desenvolvedores do Unity podem não estar cientes do fluxo constante de novos recursos adicionados à linguagem C# e ao .NET Framework. Isso ocorre porque antes do Unity 2017.1, o Unity tem usado um runtime de script equivalente ao .NET 3.5, que ficou anos sem atualizações.

Com o lançamento do Unity 2017.1, o Unity introduziu uma versão experimental do seu runtime de script atualizado para uma versão compatível com o .NET 4.6 e o C# 6. No Unity 2018.1, o runtime equivalente ao .NET 4.x não é mais considerado experimental, enquanto o runtime equivalente ao .NET 3.5 mais antigo agora é considerado como a versão herdada. E com o lançamento do Unity 2018.3, o Unity está projetando tornar o runtime de script atualizado a seleção padrão, além de atualizar mais, para o C# 7. Para obter mais informações e as atualizações mais recentes sobre este roteiro, leia a [postagem de blog](https://blogs.unity3d.com/2018/07/11/scripting-runtime-improvements-in-unity-2018-2/) do Unity ou acesse seu [Fórum de visualizações de script experimental](https://forum.unity.com/forums/experimental-scripting-previews.107/). Enquanto isso, confira as seções abaixo para saber mais sobre os novos recursos disponíveis com o runtime de script do .NET 4.x.

## <a name="prerequisites"></a>Pré-requisitos

* [Unity 2017.1 ou superior](https://unity3d.com/) (2018.2 recomendado)
* [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)

## <a name="enabling-the-net-4x-scripting-runtime-in-unity"></a>Habilitar o runtime de script do .NET 4.x no Unity

Para habilitar o runtime de script do .NET 4.x, execute as seguintes etapas:

1. Abra as PlayerSettings no Inspetor do Unity, selecionando **Editar > Configurações do projeto > Player**.

1. No cabeçalho **Configuração**, clique no menu suspenso **Versão do Runtime de Script** e selecione **Equivalente ao .NET 4.x**. Será solicitado que você reinicie o Unity.

![Selecionar o equivalente do .NET 4.x](media/vstu_scripting-runtime-version.png)

## <a name="choosing-between-net-4x-and-net-standard-20-profiles"></a>Escolher entre perfis do .NET 4.x e do .NET Standard 2.0

Depois de mudar para o runtime de script equivalente ao .NET 4.x, você pode especificar o **Nível de compatibilidade de API** usando o menu suspenso nas PlayerSettings (**Editar &gt; Configurações do projeto &gt; Player**). Há duas opções:

* **.NET Standard 2,0**. Esse perfil corresponde ao [perfil do .NET Standard 2.0](https://github.com/dotnet/standard/blob/master/docs/versions/netstandard2.0.md) publicado pela .NET Foundation. O Unity recomenda o .NET Standard 2.0 para novos projetos. Ele é menor do que o .NET 4.x, o que é vantajoso para plataformas com restrições de tamanho. Além disso, o Unity se comprometeu a dar suporte a esse perfil em todas as plataformas compatíveis com o Unity.

* **.NET 4. x**. Esse perfil fornece acesso à mais recente API do .NET 4. Ele inclui todo o código disponível nas bibliotecas de classes do .NET Framework e também dá suporte a perfis do .NET Standard 2.0. Se seu projeto requer uma parte da API não incluída no perfil do .NET Standard 2.0, use o perfil do .NET 4.x. No entanto, algumas partes dessa API podem não ser compatíveis com todas as plataformas do Unity.

Você pode ler mais sobre essas opções na [postagem de blog](https://blogs.unity3d.com/2018/03/28/updated-scripting-runtime-in-unity-2018-1-what-does-the-future-hold/) do Unity.

### <a name="adding-assembly-references-when-using-the-net-4x-api-compatibility-level"></a>Adicionar referências de assembly ao usar o nível de compatibilidade de API do .NET 4.x

Ao usar a configuração do .NET Standard 2.0 no menu suspenso **Nível de compatibilidade de API**, todos os assemblies no perfil de API são referenciados e utilizáveis. No entanto, ao usar o perfil maior do .NET 4.x, alguns dos assemblies que acompanham o Unity não são referenciados por padrão. Para usar essas APIs, você deve adicionar manualmente uma referência de assembly. Você pode exibir os assemblies com os quais o Unity é fornecido no diretório **MonoBleedingEdge/lib/mono** da instalação do editor do Unity:

![Diretório MonoBleedingEdge](media/vstu_monobleedingedge.png)

Por exemplo, se estiver usando o perfil do .NET 4.x e desejar usar `HttpClient`, você deverá adicionar uma referência de assembly para System.Net.Http.dll. Sem ele, o compilador reclamará que uma referência de assembly está ausente:

![referência de assembly ausente](media/vstu_missing-reference.png)

O Visual Studio regenera os arquivos .csproj e .sln para projetos do Unity cada vez que eles são abertos. Como resultado, não será possível adicionar referências de assembly diretamente no Visual Studio, porque elas serão perdidas ao reabrir o projeto. Em vez disso, é preciso usar um arquivo de texto especial denominado **mcs.rsp**:

1. Crie um novo arquivo de texto chamado **mcs.rsp** no diretório **Ativos** da raiz do projeto do Unity.

1. Na primeira linha no arquivo de texto vazio, digite: `-r:System.Net.Http.dll` e, em seguida, salve o arquivo. Você pode substituir "System.Net.Http.dll" com qualquer assembly incluído no qual uma referência pode estar ausente.

1. Reinicie o editor do Unity.

## <a name="taking-advantage-of-net-compatibility"></a>Aproveitando a compatibilidade do .NET

Além dos novos recursos de linguagem de programação e de sintaxe do C#, o runtime de script do .NET 4.x oferece aos usuários do Unity acesso a uma enorme biblioteca de pacotes do .NET que são incompatíveis com o runtime de script do .NET 3.5 herdado.

### <a name="add-packages-from-nuget-to-a-unity-project"></a>Adicionar pacotes do NuGet a um projeto do Unity

O [NuGet](https://www.nuget.org/) é o gerenciador de pacotes para o .NET. O NuGet é integrado ao Visual Studio. No entanto, os projetos do Unity exigem um processo especial para adicionar pacotes NuGet. Isso ocorre porque quando você abre um projeto no Unity, seus arquivos de projeto do Visual Studio são regenerados, desfazendo configurações necessárias. Para adicionar um pacote NuGet ao seu projeto Unity, faça o seguinte:

1. Procure no NuGet para localizar um pacote compatível que você deseja adicionar (.NET Standard 2.0 ou .NET 4.x). Este exemplo demonstra a adição do [Json.NET](https://www.nuget.org/packages/Newtonsoft.Json/), um pacote popular para trabalhar com JSON, a um projeto do .NET Standard 2.0.

1. Clique no botão **Download**:

    ![botão download](media/vstu_nuget-download.png)

1. Localize o arquivo baixado e altere a extensão dele de **.nupkg** para **.zip**.

1. Dentro do arquivo zip, navegue até o diretório **lib/netstandard2.0** e copie o arquivo **Newtonsoft.Json.dl**.

1. Na pasta **Ativos** na raiz do projeto do Unity, crie uma nova pasta chamada **Plugins**. Plugins é um nome de pasta especial no Unity. Veja a [documentação do Unity](https://docs.unity3d.com/Manual/Plugins.html) para obter mais informações.

1. Cole o arquivo **Newtonsoft.Json.dll** no diretório **Plugins** do projeto do Unity.

1. Crie um arquivo chamado **link.xml** no diretório **Ativos** do seu projeto do Unity e adicione o XML a seguir.  Isso garantirá que o processo de remoção de código de bytes do Unity não remova os dados necessários ao exportar para uma plataforma IL2CPP.  Embora esta etapa seja específica para essa biblioteca, você poderá encontrar problemas com outras bibliotecas que usam reflexão de maneiras semelhantes.  Para obter mais informações, consulte a [documentação do Unity](https://docs.unity3d.com/Manual/IL2CPP-BytecodeStripping.html) sobre esse tópico.

    ```xml
    <linker>
      <assembly fullname="System.Core">
        <type fullname="System.Linq.Expressions.Interpreter.LightLambda" preserve="all" />
      </assembly>
    </linker>
    ```

Com tudo pronto, agora você pode usar o pacote Json.NET.

```csharp
using Newtonsoft.Json;
using UnityEngine;

public class JSONTest : MonoBehaviour
{
    class Enemy
    {
        public string Name { get; set; }
        public int AttackDamage { get; set; }
        public int MaxHealth { get; set; }
    }
    private void Start()
    {
        string json = @"{
            'Name': 'Ninja',
            'AttackDamage': '40'
            }";

        var enemy = JsonConvert.DeserializeObject<Enemy>(json);

        Debug.Log($"{enemy.Name} deals {enemy.AttackDamage} damage.");
        // Output:
        // Ninja deals 40 damage.
    }
}
```

Esse é um exemplo simples do uso de uma biblioteca sem dependências. Quando os pacotes do NuGet dependem de outros pacotes do NuGet, você precisa baixar essas dependências manualmente e adicioná-las ao projeto da mesma maneira.

## <a name="new-syntax-and-language-features"></a>Novos recursos de linguagem e de sintaxe

Usar o runtime de script atualizado dá aos desenvolvedores do Unity acesso a C# 6 e a uma série de novos recursos de linguagem e de sintaxe.

### <a name="auto-property-initializers"></a>Inicializadores de propriedade automática

No runtime de script do Unity .NET 3.5, a sintaxe de propriedade automática torna mais fácil definir rapidamente as propriedades não inicializadas, mas a inicialização precisa ocorrer em outro lugar no seu script. Agora, com o runtime .NET 4.x, é possível inicializar as propriedades automáticas na mesma linha:

```csharp
// .NET 3.5
public int Health { get; set; } // Health has to be initialized somewhere else, like Start()

// .NET 4.x
public int Health { get; set; } = 100;
```

### <a name="string-interpolation"></a>Interpolação de cadeia de caracteres

Com o runtime mais antigo do .NET 3.5, a concatenação de cadeia de caracteres exigia uma sintaxe estranha. Agora, com o tempo de execução do .NET 4. x, o recurso de [ `$` interpolação de cadeia de caracteres](/dotnet/csharp/language-reference/tokens/interpolated) permite que as expressões sejam inseridas em cadeias em uma sintaxe mais direta e legível:

```csharp
// .NET 3.5
Debug.Log(String.Format("Player health: {0}", Health)); // or
Debug.Log("Player health: " + Health);

// .NET 4.x
Debug.Log($"Player health: {Health}");
```

### <a name="expression-bodied-members"></a>Membros aptos para expressão

Com a mais nova sintaxe C# disponível no runtime do .NET 4.x, [expressões lambda](/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions) podem substituir o corpo de funções para torná-las mais sucintas:

```csharp
// .NET 3.5
private int TakeDamage(int amount)
{
    return Health -= amount;
}

// .NET 4.x
private int TakeDamage(int amount) => Health -= amount;
```

Você também pode usar membros aptos para expressão em propriedades somente leitura:

```csharp
// .NET 4.x
public string PlayerHealthUiText => $"Player health: {Health}";
```

### <a name="task-based-asynchronous-pattern-tap"></a>Padrão assíncrono baseado em tarefa (TAP)

A [programação assíncrona](/dotnet/csharp/async) permite que operações demoradas sejam realizadas sem que isso faça com que o aplicativo pare de responder. Essa funcionalidade também permite que seu código aguarde a conclusão de operações demoradas antes de continuar com código que dependa dos resultados dessas operações. Por exemplo, você poderia esperar o carregamento de um arquivo ou a conclusão de uma operação de rede.

No Unity, a programação assíncrona normalmente é feita com [corrotinas](https://docs.unity3d.com/Manual/Coroutines.html). No entanto, desde o C# 5, o método preferencial de programação assíncrona no desenvolvimento do .NET é o [TAP (Padrão Assíncrono Baseado em Tarefa)](/dotnet/standard/asynchronous-programming-patterns/task-based-asynchronous-pattern-tap) usando o `async` e palavras-chave `await` com [System.Threading.Task](/dotnet/api/system.threading.tasks.task). Em resumo, em uma função `async`, você pode `await` a conclusão de uma tarefa sem bloquear a atualização do resto do seu aplicativo:

```csharp
// Unity coroutine
using UnityEngine;
public class UnityCoroutineExample : MonoBehaviour
{
    private void Start()
    {
        StartCoroutine(WaitOneSecond());
        DoMoreStuff(); // This executes without waiting for WaitOneSecond
    }
    private IEnumerator WaitOneSecond()
    {
        yield return new WaitForSeconds(1.0f);
        Debug.Log("Finished waiting.");
    }
}
```

```csharp
// .NET 4.x async-await
using UnityEngine;
using System.Threading.Tasks;
public class AsyncAwaitExample : MonoBehaviour
{
    private async void Start()
    {
        Debug.Log("Wait.");
        await WaitOneSecondAsync();
        DoMoreStuff(); // Will not execute until WaitOneSecond has completed
    }
    private async Task WaitOneSecondAsync()
    {
        await Task.Delay(TimeSpan.FromSeconds(1));
        Debug.Log("Finished waiting.");
    }
}
```

O TAP é um assunto complexo, com nuances específicas do Unity que os desenvolvedores devem considerar. Como resultado, o TAP não é uma substituição universal para corrotinas no Unity; no entanto, é outra ferramenta que se pode aproveitar. O escopo desse recurso está além do abordado por este artigo, mas algumas dicas e práticas recomendadas gerais são fornecidas abaixo.

#### <a name="getting-started-reference-for-tap-with-unity"></a>Referência de introdução ao TAP com o Unity

Estas dicas podem ajudar você a começar a usar o TAP no Unity:

* As funções assíncronas destinadas a serem aguardadas devem ter o tipo de retorno [`Task`](/dotnet/api/system.threading.tasks.task) ou [`Task<TResult>`](/dotnet/api/system.threading.tasks.task-1) .
* Funções assíncronas que retornam uma tarefa devem ter o sufixo **"Async"** acrescentado aos seus nomes. O sufixo "Async" ajuda a indicar que uma função deve sempre ser aguardada.
* Use somente o tipo de retorno `async void` para funções que disparam funções assíncronas do código síncrono tradicional. Essas funções em si não podem ser esperadas e não devem ter o sufixo "Async" em seus nomes.
* O Unity usa o UnitySynchronizationContext para garantir que funções assíncronas sejam executadas no thread principal por padrão. A API do Unity não está acessível fora do thread principal.
* É possível executar tarefas em threads em segundo plano com métodos como [`Task.Run`](https://msdn.microsoft.com/library/hh195051.aspx) e [`Task.ConfigureAwait(false)`](https://msdn.microsoft.com/library/system.threading.tasks.task.configureawait.aspx) . Essa técnica é útil para o descarregamento de operações onerosas do thread principal para aprimorar o desempenho. No entanto, o uso de threads em segundo plano pode levar a problemas difíceis de depurar, tais como [condições de corrida](https://wikipedia.org/wiki/Race_condition).
* A API do Unity não está acessível fora do thread principal.
* Tarefas que usam threads não são compatíveis com builds WebGL do Unity.

#### <a name="differences-between-coroutines-and-tap"></a>Diferenças entre corrotinas e TAP

Há algumas diferenças importantes entre corrotinas e TAP/async-await:

* As corrotinas não podem retornar valores, mas `Task<TResult>` pode.
* Você não pode colocar um `yield` em uma instrução try-catch, tornando o tratamento de erro difícil com as corrotinas. No entanto, o try-catch funciona com o TAP.
* O recurso de co-rotina do Unity não está disponível nas classes que não derivam de MonoBehaviour. TAP é ótimo para programação assíncrona nessas classes.
* Atualmente, o Unity não sugere TAP como uma substituição completa de corrotinas. A criação de perfil é a única maneira de saber os resultados específicos de uma abordagem em relação à outra para qualquer projeto.

> [!NOTE]
> Desde o Unity 2018.2, métodos assíncronos com pontos de interrupção de depuração não são totalmente compatíveis; no entanto, [essa funcionalidade é esperada no Unity 2018.3](https://twitter.com/jbevain/status/900043560665235456).

### <a name="nameof-operator"></a>operador nameof

O operador `nameof` obtém o nome de cadeia de caracteres de uma variável, tipo ou membro. Alguns casos em que `nameof` é útil são o registro de erros e a obtenção do nome da cadeia de caracteres de uma enumeração:

```csharp
// Get the string name of an enum:
enum Difficulty {Easy, Medium, Hard};
private void Start()
{
    Debug.Log(nameof(Difficulty.Easy));
    RecordHighScore("John");
    // Output:
    // Easy
    // playerName
}
// Validate parameter:
private void RecordHighScore(string playerName)
{
    Debug.Log(nameof(playerName));
    if (playerName == null) throw new ArgumentNullException(nameof(playerName));
}
```

### <a name="caller-info-attributes"></a>Atributos de informações do chamador

Os [atributos de informações do chamador](/dotnet/csharp/programming-guide/concepts/caller-information) fornecem informações sobre o chamador de um método. Você deve fornecer um valor padrão para cada parâmetro que você deseja usar com um atributo de informações do chamador:

```csharp
private void Start ()
{
    ShowCallerInfo("Something happened.");
}
public void ShowCallerInfo(string message,
        [System.Runtime.CompilerServices.CallerMemberName] string memberName = "",
        [System.Runtime.CompilerServices.CallerFilePath] string sourceFilePath = "",
        [System.Runtime.CompilerServices.CallerLineNumber] int sourceLineNumber = 0)
{
    Debug.Log($"message: {message}");
    Debug.Log($"member name: {memberName}");
    Debug.Log($"source file path: {sourceFilePath}");
    Debug.Log($"source line number: {sourceLineNumber}");
}
// Output:
// Something happened
// member name: Start
// source file path: D:\Documents\unity-scripting-upgrade\Unity Project\Assets\CallerInfoTest.cs
// source line number: 10
```

### <a name="using-static"></a>Using static

[Using static](/dotnet/csharp/language-reference/keywords/using-static) permite que você use funções estáticas sem digitar seu nome de classe. Com o using static, você poderá economizar espaço e tempo se precisar usar várias funções estáticas da mesma classe:

```csharp
// .NET 3.5
using UnityEngine;
public class Example : MonoBehaviour
{
    private void Start ()
    {
        Debug.Log(Mathf.RoundToInt(Mathf.PI));
        // Output:
        // 3
    }
}
```

```csharp
// .NET 4.x
using UnityEngine;
using static UnityEngine.Mathf;
public class UsingStaticExample: MonoBehaviour
{
    private void Start ()
    {
        Debug.Log(RoundToInt(PI));
        // Output:
        // 3
    }
}
```

## <a name="il2cpp-considerations"></a>Considerações de IL2CPP

Ao exportar seu jogo para plataformas como iOS, o Unity usará seu mecanismo IL2CPP para "transcompilar" o IL para código C++ que é então compilado usando o compilador nativo da plataforma de destino. Nesse cenário, há vários recursos do .NET que não são compatíveis, tais como partes de reflexão e o uso da palavra-chave `dynamic`. Embora você possa controlar o uso desses recursos em seu próprio código, você pode encontrar problemas ao usar DLLs de terceiros e SDKs que não foram escritos com o Unity e o IL2CPP em mente. Para obter mais informações sobre esse tópico, veja a documentação sobre [restrições de script](https://docs.unity3d.com/Manual/ScriptingRestrictions.html) no site do Unity.

Além disso, conforme mencionado no exemplo de Json.NET acima, o Unity tentará retirar o código não utilizado durante o processo de exportação de IL2CPP.  Embora isso normalmente não seja um problema, com bibliotecas que usam reflexão, ele pode remover acidentalmente Propriedades ou métodos que serão chamados em tempo de execução que não podem ser determinados no momento da exportação.  Para corrigir esses problemas, adicione um arquivo **link.xml** ao seu projeto que contém uma lista de assemblies e namespaces nos quais não executar o processo de remoção.  Para obter detalhes completos, veja a [documentação do Unity sobre a remoção de código de bytes](https://docs.unity3d.com/Manual/IL2CPP-BytecodeStripping.html).

## <a name="net-4x-sample-unity-project"></a>Projeto do Unity de exemplo do .NET 4.x

A amostra contém exemplos de vários recursos do .NET 4.x. Você pode baixar o projeto ou exibir o código-fonte no [GitHub](https://github.com/Microsoft/unity-scripting-upgrade).

## <a name="additional-resources"></a>Recursos adicionais

* [Blog do Unity – aprimoramentos de runtime de script no Unity 2018.2](https://blogs.unity3d.com/2018/07/11/scripting-runtime-improvements-in-unity-2018-2/)
* [Histórico da linguagem C#](/dotnet/csharp/whats-new/csharp-version-history)
* [Novidades no C# 6](/dotnet/csharp/whats-new/csharp-6)
* [Programação assíncrona no Unity, usando co-rotina e TAP](/archive/blogs/appconsult/unity-coroutine-tap-en-us)
* [Async-Await em vez de corrotinas no Unity 2017](http://www.stevevermeulen.com/index.php/2017/09/using-async-await-in-unity3d-2017/)
* [Fórum do Unity – visualizações de script Experimental](https://forum.unity.com/forums/experimental-scripting-previews.107/)
