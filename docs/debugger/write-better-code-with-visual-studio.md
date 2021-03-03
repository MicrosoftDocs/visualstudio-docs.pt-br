---
title: Técnicas e ferramentas de depuração
description: Escreva código melhor com menos bugs usando o Visual Studio para corrigir exceções, corrigir erros e melhorar seu código
ms.custom:
- debug-experiment
- seodec18
ms.date: 02/14/2020
ms.topic: conceptual
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5fd3d8e17d90cde50f583dfc0393debf460de7f6
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101684073"
---
# <a name="debugging-techniques-and-tools-to-help-you-write-better-code"></a>Ferramentas e técnicas de depuração para ajudá-lo a escrever código melhor

Corrigir bugs e erros em seu código pode ser uma tarefa demorada e, às vezes, frustrante. Leva tempo para aprender a depurar com eficiência, mas um eficiente IDE, como o Visual Studio, pode tornar seu trabalho muito mais fácil. Um IDE pode ajudá-lo a corrigir erros e depurar seu código mais rapidamente, e não apenas isso, mas também pode ajudá-lo a escrever código melhor com menos bugs. Nosso objetivo neste artigo é fornecer uma visão holística do processo de "correção de bugs", de modo que você saberá quando usar o analisador de código, quando usar o depurador, como corrigir exceções e como codificar para a intenção. Se você já sabe que precisa usar o depurador, consulte [a primeira olhada no depurador](../debugger/debugger-feature-tour.md).

Neste artigo, falamos sobre como aproveitar o IDE para tornar suas sessões de codificação mais produtivas. Podemos abordar várias tarefas, como:

* Prepare seu código para depuração aproveitando o analisador de código do IDE

* Como corrigir exceções (erros de tempo de execução)

* Como minimizar bugs codificando a intenção (usando Assert)

* Quando usar o depurador

Para demonstrar essas tarefas, mostramos alguns dos tipos mais comuns de erros e bugs que você encontrará ao tentar depurar seus aplicativos. Embora o código de exemplo seja C#, as informações conceituais geralmente são aplicáveis ao C++, Visual Basic, JavaScript e a outras linguagens compatíveis com o Visual Studio (exceto quando indicado). As capturas de tela estão em C#.

## <a name="create-a-sample-app-with-some-bugs-and-errors-in-it"></a>Criar um aplicativo de exemplo com alguns bugs e erros nele

O código a seguir tem alguns bugs que você pode corrigir usando o IDE do Visual Studio. O aplicativo aqui é um aplicativo simples que simula a obtenção de dados JSON de alguma operação, desserializando os dados para um objeto e atualizando uma lista simples com os novos dados.

Para criar o aplicativo:

1. Você deve ter o Visual Studio instalado e a carga de trabalho de **desenvolvimento da plataforma cruzada do .NET Core** instalada.

    Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/) para instalá-lo gratuitamente.

    Se você precisar instalar a carga de trabalho, mas já tiver o Visual Studio, clique em **ferramentas**  >  **obter ferramentas e recursos**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** e escolha **Modificar**.

1. Abra o Visual Studio.

    ::: moniker range=">=vs-2019"
    Na janela iniciar, escolha **criar um novo projeto**. Digite **console** na caixa de pesquisa e, em seguida, escolha o **aplicativo de console** para .NET Core. Escolha **Próxima**. Digite um nome de projeto como **Console_Parse_JSON** e clique em **Avançar** ou **criar**, a opção que estiver disponível.

    Para o .NET Core, escolha a estrutura de destino recomendada (.NET Core 3,1) ou .NET 5 e, em seguida, escolha **criar**.

    Se você não vir o **aplicativo de console** para o modelo de projeto do .NET Core, vá para **ferramentas**  >  **obter ferramentas e recursos**, o que abre o instalador do Visual Studio. Escolha a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** e escolha **Modificar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **novo projeto** , em **Visual C#**, escolha **aplicativo de console** e, no painel central, escolha **aplicativo de console (.NET Core)**. Digite um nome como **Console_Parse_JSON** e clique em **OK**.

    Se você não vir o modelo de projeto do **aplicativo de console (.NET Core)** , vá para **ferramentas**  >  **obter ferramentas e recursos**, o que abre o instalador do Visual Studio. Escolha a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** e escolha **Modificar**.
    ::: moniker-end

    O Visual Studio criará o console do projeto, que será aberto no Gerenciador de Soluções no painel direito.

1. Substitua o código padrão no arquivo *Program.cs* do projeto pelo código de exemplo abaixo.

```csharp
using System;
using System.Collections.Generic;
using System.Runtime.Serialization.Json;
using System.Runtime.Serialization;
using System.IO;

namespace Console_Parse_JSON
{
    class Program
    {
        static void Main(string[] args)
        {
            var localDB = LoadRecords();
            string data = GetJsonData();

            User[] users = ReadToObject(data);

            UpdateRecords(localDB, users);

            for (int i = 0; i < users.Length; i++)
            {
                List<User> result = localDB.FindAll(delegate (User u) {
                    return u.lastname == users[i].lastname;
                    });
                foreach (var item in result)
                {
                    Console.WriteLine($"Matching Record, got name={item.firstname}, lastname={item.lastname}, age={item.totalpoints}");
                }
            }

            Console.ReadKey();
        }

        // Deserialize a JSON stream to a User object.
        public static User[] ReadToObject(string json)
        {
            User deserializedUser = new User();
            User[] users = { };
            MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(json));
            DataContractJsonSerializer ser = new DataContractJsonSerializer(users.GetType());

            users = ser.ReadObject(ms) as User[];

            ms.Close();
            return users;
        }

        // Simulated operation that returns JSON data.
        public static string GetJsonData()
        {
            string str = "[{ \"points\":4o,\"firstname\":\"Fred\",\"lastname\":\"Smith\"},{\"lastName\":\"Jackson\"}]";
            return str;
        }

        public static List<User> LoadRecords()
        {
            var db = new List<User> { };
            User user1 = new User();
            user1.firstname = "Joe";
            user1.lastname = "Smith";
            user1.totalpoints = 41;

            db.Add(user1);

            User user2 = new User();
            user2.firstname = "Pete";
            user2.lastname = "Peterson";
            user2.totalpoints = 30;

            db.Add(user2);

            return db;
        }
        public static void UpdateRecords(List<User> db, User[] users)
        {
            bool existingUser = false;

            for (int i = 0; i < users.Length; i++)
            {
                foreach (var item in db)
                {
                    if (item.lastname == users[i].lastname && item.firstname == users[i].firstname)
                    {
                        existingUser = true;
                        item.totalpoints += users[i].points;

                    }
                }
                if (existingUser == false)
                {
                    User user = new User();
                    user.firstname = users[i].firstname;
                    user.lastname = users[i].lastname;
                    user.totalpoints = users[i].points;

                    db.Add(user);
                }
            }
        }
    }

    [DataContract]
    internal class User
    {
        [DataMember]
        internal string firstname;

        [DataMember]
        internal string lastname;

        [DataMember]
        // internal double points;
        internal string points;

        [DataMember]
        internal int totalpoints;
    }
}
```

## <a name="find-the-red-and-green-squiggles"></a>Encontre os rabiscos vermelho e verde!

Antes de tentar iniciar o aplicativo de exemplo e executar o depurador, verifique o código no editor de código para os rabiscos vermelho e verde. Elas representam erros e avisos identificados pelo analisador de código do IDE. Os ondulados vermelhos são erros de tempo de compilação, que você deve corrigir antes de poder executar o código. Os rabiscos verdes são avisos. Embora você possa executar o aplicativo com frequência sem corrigir os avisos, eles podem ser uma fonte de bugs e, muitas vezes, você economiza tempo e problemas investigando-os. Esses avisos e erros também aparecem na janela de **lista de erros** , se você preferir uma exibição de lista.

No aplicativo de exemplo, você verá vários rabiscos vermelhos que precisam ser corrigidos e um verde que você examinará. Aqui está o primeiro erro.

![Erro ao mostrar como um ondulado vermelho](../debugger/media/write-better-code-red-squiggle.png)

Para corrigir esse erro, você examinará outro recurso do IDE, representado pelo ícone de lâmpada.

## <a name="check-the-light-bulb"></a>Verifique a lâmpada!

O primeiro ondulado vermelho representa um erro de tempo de compilação. Passe o mouse sobre ele e você verá a mensagem ```The name `Encoding` does not exist in the current context``` .

Observe que esse erro mostra um ícone de lâmpada à esquerda inferior. Junto com o ícone de chave de fenda ícone ![ ](../ide/media/screwdriver-icon.png) , o ícone de lâmpada do ícone de lâmpada ![ ](../ide/media/light-bulb-icon.png) representa ações rápidas que podem ajudá-lo a corrigir ou refatorar o código embutido. A lâmpada representa problemas que você *deve* corrigir. A chave de fenda é para problemas que você pode optar por corrigir. Use a primeira correção sugerida para resolver esse erro clicando em **usar System. Text** à esquerda.

![Usar a lâmpada para corrigir o código](../debugger/media/write-better-code-missing-include.png)

Quando você clica neste item, o Visual Studio adiciona a `using System.Text` instrução na parte superior do arquivo *Program.cs* e o ondulado vermelho desaparece. (Quando você não tiver certeza do que uma correção sugerida fará, escolha o link **Visualizar alterações** à direita antes de aplicar a correção.)

O erro anterior é um comum que você geralmente corrige adicionando uma nova `using` instrução ao seu código. Há vários erros semelhantes e comuns a este, como ```The type or namespace `Name` cannot be found.``` esses tipos de erros podem indicar uma referência de assembly ausente (clique com o botão direito do mouse no projeto, escolha **Adicionar**  >  **referência**), um nome com erros de ortografia ou uma biblioteca ausente que você precisa adicionar (para C#, clique com o botão direito do mouse no projeto e escolha **gerenciar pacotes NuGet**).

## <a name="fix-the-remaining-errors-and-warnings"></a>Corrigir os erros e avisos restantes

Há mais alguns rabiscos a serem examinados neste código. Aqui, você verá um erro de conversão de tipo comum. Ao passar o mouse sobre o rabisco, você verá que o código está tentando converter uma cadeia de caracteres em um int, o que não tem suporte, a menos que você adicione um código explícito para fazer a conversão.

![Erro de conversão de tipo](../debugger/media/write-better-code-conversion-error.png)

Como o analisador de código não pode adivinhar sua intenção, não há lâmpadas leves para ajudá-lo nesse tempo. Para corrigir esse erro, você precisa saber a intenção do código. Neste exemplo, não é muito difícil ver que `points` deve ser um valor numérico (inteiro), já que você está tentando adicionar `points` a `totalpoints` .

Para corrigir esse erro, altere o `points` membro da `User` classe deste:

```csharp
[DataMember]
internal string points;
```

para isto:

```csharp
[DataMember]
internal int points;
```

As linhas vermelhas onduladas no editor de códigos desaparecem.

Em seguida, passe o mouse sobre o rabisco verde na declaração do `points` membro de dados. O analisador de código informa à variável que nunca é atribuído um valor.

![Mensagem de aviso para variável não atribuída](../debugger/media/write-better-code-warning-message.png)

Normalmente, isso representa um problema que precisa ser corrigido. No entanto, no aplicativo de exemplo, você está realmente armazenando dados na `points` variável durante o processo de desserialização e, em seguida, adicionando esse valor ao `totalpoints` membro de dados. Neste exemplo, você sabe a intenção do código e pode ignorar com segurança o aviso. No entanto, se você quiser eliminar o aviso, poderá substituir o seguinte código:

```csharp
item.totalpoints = users[i].points;
```

por este:

```csharp
item.points = users[i].points;
item.totalpoints += users[i].points;
```

O rabisco verde desaparece.

## <a name="fix-an-exception"></a>Corrigir uma exceção

Quando você tiver corrigido todos os rabiscos vermelhos e resolvidos, ou pelo menos investigado, todos os rabiscos verdes, você estará pronto para iniciar o depurador e executar o aplicativo.

Pressione **F5** (**debug > iniciar depuração**) ou o botão **Iniciar Depuração** ![Iniciar Depuração](../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração") na barra de ferramentas Depurar.

Neste ponto, o aplicativo de exemplo gera uma `SerializationException` exceção (um erro de tempo de execução). Ou seja, o aplicativo obstru os dados que ele está tentando serializar. Como você iniciou o aplicativo no modo de depuração (depurador anexado), o auxiliar de exceção do depurador leva você diretamente ao código que gerou a exceção e fornece uma mensagem de erro útil.

![Uma Serializaexception ocorre](../debugger/media/write-better-code-serialization-exception.png)

A mensagem de erro instrui você que o valor `4o` não pode ser analisado como um inteiro. Portanto, neste exemplo, você sabe que os dados são inválidos: `4o` deve ser `40` . No entanto, se você não estiver no controle dos dados em um cenário real (digamos que você esteja obtendo de um serviço Web), o que fazer a respeito? Como consertar isso?

Ao chegar a uma exceção, você precisa fazer (e responder) algumas perguntas:

* Essa exceção é apenas um bug que você pode corrigir? Ou,

* Essa exceção é algo que os usuários podem encontrar?

Se for o primeiro, corrija o bug. (No aplicativo de exemplo, isso significa corrigir os dados inválidos.) Se for o último, talvez seja necessário manipular a exceção em seu código usando um `try/catch` bloco (examinaremos outras estratégias possíveis na próxima seção). No aplicativo de exemplo, substitua o seguinte código:

```csharp
users = ser.ReadObject(ms) as User[];
```

por este código:

```csharp
try
{
    users = ser.ReadObject(ms) as User[];
}
catch (SerializationException)
{
    Console.WriteLine("Give user some info or instructions, if necessary");
    // Take appropriate action for your app
}
```

Um `try/catch` bloco tem algum custo de desempenho, portanto, você só desejará usá-los quando realmente precisar deles, ou seja, onde (a) eles podem ocorrer na versão de lançamento do aplicativo e onde (b) a documentação do método indica que você deve verificar a exceção (supondo que a documentação esteja completa!). Em muitos casos, você pode manipular uma exceção de forma adequada e o usuário nunca precisará saber sobre ela.

Aqui estão algumas dicas importantes para a manipulação de exceções:

* Evite usar um bloco catch vazio, como `catch (Exception) {}` , que não executa a ação apropriada para expor ou tratar um erro. Um bloco catch vazio ou não informativo pode ocultar exceções e pode tornar seu código mais difícil de Depurar em vez de mais fácil.

* Use o `try/catch` bloco em volta da função específica que lança a exceção ( `ReadObject` , no aplicativo de exemplo). Se você usá-lo em uma parte maior do código, acabará ocultando o local do erro. Por exemplo, não use o `try/catch` bloco ao contrário da chamada para a função pai `ReadToObject` , mostrada aqui, ou você não saberá exatamente onde ocorreu a exceção.

    ```csharp
    // Don't do this
    try
    {
        User[] users = ReadToObject(data);
    }
    catch (SerializationException)
    {
    }
    ```

* Para funções desconhecidas que você inclui em seu aplicativo, especialmente aquelas que interagem com dados externos (como uma solicitação da Web), consulte a documentação para ver quais exceções a função provavelmente gerará. Isso pode ser uma informação crítica para tratamento de erros adequado e para depurar seu aplicativo.

Para o aplicativo de exemplo, corrija o `SerializationException` no `GetJsonData` método alterando `4o` para `40` .

## <a name="clarify-your-code-intent-by-using-assert"></a>Esclarecer sua intenção de código usando Assert

Clique no botão **reiniciar** ![aplicativo de reinicialização](../debugger/media/dbg-tour-restart.png "RestartApp") na barra de ferramentas depurar (**Ctrl**  +  **Shift**  +  **F5**). Isso reinicia o aplicativo em menos etapas. Você verá a seguinte saída na janela do console.

![Valor nulo na saída](../debugger/media/write-better-code-using-assert-null-output.png)

Você pode ver algo nessa saída que não está bem certo. o **nome** e o **sobrenome** do terceiro registro estão em branco!

Esse é um bom momento para falar sobre uma prática de codificação útil, geralmente subutilizada, que é usar `assert` instruções em suas funções. Ao adicionar o código a seguir, você inclui uma verificação de tempo de execução para verificar se o `firstname` e o `lastname` não são `null` . Substitua o seguinte código no `UpdateRecords` método:

```csharp
if (existingUser == false)
{
    User user = new User();
    user.firstname = users[i].firstname;
    user.lastname = users[i].lastname;
```

por este:

```csharp
// Also, add a using statement for System.Diagnostics at the start of the file.
Debug.Assert(users[i].firstname != null);
Debug.Assert(users[i].lastname != null);
if (existingUser == false)
{
    User user = new User();
    user.firstname = users[i].firstname;
    user.lastname = users[i].lastname;
```

Ao adicionar `assert` instruções como essa às suas funções durante o processo de desenvolvimento, você pode ajudar a especificar a intenção do seu código. No exemplo anterior, especificamos o seguinte:

* Uma cadeia de caracteres válida é necessária para o primeiro nome
* Uma cadeia de caracteres válida é necessária para o último nome

Ao especificar a intenção dessa forma, você impõe suas necessidades. Esse é um método simples e útil que você pode usar para surgir bugs durante o desenvolvimento. ( `assert` as instruções também são usadas como o elemento principal em testes de unidade.)

Clique no botão **reiniciar** ![aplicativo de reinicialização](../debugger/media/dbg-tour-restart.png "RestartApp") na barra de ferramentas depurar (**Ctrl**  +  **Shift**  +  **F5**).

> [!NOTE]
> O `assert` código está ativo somente em uma compilação de depuração.

Quando você reinicia, o depurador pausa na `assert` instrução, porque a expressão `users[i].firstname != null` é avaliada como `false` em vez de `true` .

![Assert é resolvido para false](../debugger/media/write-better-code-using-assert.png)

O `assert` erro informa que há um problema que você precisa investigar. `assert` o pode abranger muitos cenários em que você não vê necessariamente uma exceção. Neste exemplo, o usuário não verá uma exceção e um `null` valor será adicionado como `firstname` em sua lista de registros. Isso pode causar problemas posteriormente (como você vê na saída do console) e pode ser mais difícil de depurar.

> [!NOTE]
> Em cenários em que você chama um método no `null` valor, um `NullReferenceException` resultado. Normalmente, você deseja evitar o uso de um `try/catch` bloco para uma exceção geral, ou seja, uma exceção que não esteja vinculada à função de biblioteca específica. Qualquer objeto pode lançar um `NullReferenceException` . Verifique a documentação da função de biblioteca se você não tiver certeza.

Durante o processo de depuração, é bom manter uma instrução específica `assert` até que você saiba que precisa substituí-la por uma correção de código real. Digamos que você decida que o usuário pode encontrar a exceção em uma compilação de versão do aplicativo. Nesse caso, você deve refatorar o código para garantir que seu aplicativo não lance uma exceção fatal ou resulte em algum outro erro. Portanto, para corrigir esse código, substitua o código a seguir:

```csharp
if (existingUser == false)
{
    User user = new User();
```

por este código:

```csharp
if (existingUser == false && users[i].firstname != null && users[i].lastname != null)
{
    User user = new User();
```

Ao usar esse código, você preenche os requisitos de código e verifica se um registro com um `firstname` `lastname` valor ou de `null` não é adicionado aos dados.

Neste exemplo, adicionamos as duas `assert` instruções dentro de um loop. Normalmente, ao usar `assert` o, é melhor adicionar `assert` instruções no ponto de entrada (início) de uma função ou método. No momento, você está vendo o `UpdateRecords` método no aplicativo de exemplo. Nesse método, você saberá que está com problemas se qualquer um dos argumentos do método for `null` , portanto, verifique-os com uma `assert` instrução no ponto de entrada da função.

```csharp
public static void UpdateRecords(List<User> db, User[] users)
{
    Debug.Assert(db != null);
    Debug.Assert(users != null);
```

Para as instruções anteriores, sua intenção é que você carregue os dados existentes ( `db` ) e recupere novos dados ( `users` ) antes de atualizar qualquer coisa.

Você pode usar `assert` com qualquer tipo de expressão que resolva para `true` ou `false` . Portanto, por exemplo, você pode adicionar uma `assert` instrução como esta.

```csharp
Debug.Assert(users[0].points > 0);
```

O código anterior será útil se você quiser especificar a seguinte intenção: um novo valor de ponto maior que zero (0) é necessário para atualizar o registro do usuário.

## <a name="inspect-your-code-in-the-debugger"></a>Inspecione seu código no depurador

OK, agora que você corrigiu tudo o que está errado com o aplicativo de exemplo, você pode passar para outras coisas importantes!

Mostramos o auxiliar de exceção do depurador, mas o depurador é uma ferramenta muito mais poderosa que também permite que você faça outras coisas como percorrer seu código e inspecionar suas variáveis. Esses recursos mais poderosos são úteis em muitos cenários, especialmente os seguintes:

* Você está tentando isolar um bug de tempo de execução em seu código, mas não é possível fazer isso usando métodos e ferramentas anteriormente discutidos.

* Você deseja validar seu código, ou seja, observá-lo enquanto ele é executado para verificar se ele está se comportando da maneira esperada e fazendo o que você deseja.

    É instrutivo observar seu código enquanto ele é executado. Você pode aprender mais sobre seu código dessa maneira e, muitas vezes, pode identificar bugs antes de manifestar quaisquer sintomas óbvios.

Para saber como usar os recursos essenciais do depurador, consulte [Depurando para iniciantes absolutos](../debugger/debugging-absolute-beginners.md).

## <a name="fix-performance-issues"></a>Corrigir problemas de desempenho

Os bugs de outro tipo incluem código ineficiente que faz com que seu aplicativo seja executado lentamente ou use muita memória. Em geral, otimizar o desempenho é algo que você faz mais tarde no desenvolvimento de seu aplicativo. No entanto, você pode encontrar problemas de desempenho antecipadamente (por exemplo, você vê que alguma parte do seu aplicativo está em execução lenta), e talvez seja necessário testar seu aplicativo com as ferramentas de criação de perfil no início. Para obter mais informações sobre ferramentas de criação de perfil, como a ferramenta de uso da CPU e o analisador de memória, consulte [primeira análise das ferramentas de criação de perfil](../profiling/profiling-feature-tour.md).

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu como evitar e corrigir muitos bugs comuns em seu código e quando usar o depurador. Em seguida, saiba mais sobre como usar o depurador do Visual Studio para corrigir bugs.

> [!div class="nextstepaction"]
> [Depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md)
