---
title: Corrigir bugs escrevendo um melhor código C#
description: Compreender como escrever códigos melhores com menos bugs
ms.custom:
- debug-experiments
- seodec18
ms.date: 11/20/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a2e3aaebd02754556f028f53a190160f502ef9ca
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53051669"
---
# <a name="fix-bugs-by-writing-better-c-code-using-visual-studio"></a>Corrigir bugs, escrevendo melhor C# o código usando o Visual Studio

Depurar o código pode ser demorado – e, às vezes, frustrante – tarefa. Leva tempo para saber como depurar com eficiência, mas um IDE avançado como o Visual Studio pode tornar seu trabalho muito mais fácil. Um IDE pode ajudar você a depurar seu código mais rapidamente e não apenas isso, mas ele também pode ajudar você escreve códigos melhores com menos erros. Nosso objetivo neste artigo é fornecer uma visão holística do processo de depuração, para que você saiba quando usar o analisador de código, quando uso o depurador e quando usar outras ferramentas.  

Neste artigo, falamos sobre aproveitando o IDE para tornar suas sessões de depuração mais produtivo. Abordemos a várias tarefas, como:

* Preparar o seu código para depuração, aproveitando o analisador de código do IDE

* Como corrigir exceções (erros de tempo de execução)

* Como minimizar os bugs por meio de codificação de intenção

* Quando usar o depurador

Para demonstrar essas tarefas, vamos mostrar alguns dos tipos mais comuns de erros e bugs que você encontrará ao tentar depurar seus aplicativos. Embora o código de exemplo é C#, as informações conceituais for geralmente aplicáveis a C++, Visual Basic, JavaScript e outras linguagens com suporte pelo Visual Studio (exceto onde observado). As capturas de tela estão em C#.

## <a name="follow-along-using-the-sample-app"></a>Acompanhar usando o aplicativo de exemplo

Se você preferir, você pode criar um aplicativo de console do .NET Framework ou .NET Core que contém os bugs exatos e erros que descrevemos aqui, e você pode segui-lo e fazer as correções por conta própria.

Para criar o aplicativo, abra o Visual Studio e escolha **arquivo > Novo projeto**. Sob **Visual C#** , escolha **área de trabalho do Windows** ou **.NET Core**e, em seguida, no painel central, escolha uma **aplicativo de Console**. Digite um nome como **Console_Parse_JSON** e clique em **Okey**. O Visual Studio cria o projeto. Cole a [código de exemplo](#sample-code) para o projeto *Program.cs* arquivo.

> [!NOTE]
> Se o modelo de projeto do **Aplicativo de Console** não for exibido, clique no link **Abrir Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento de área de trabalho do .NET** (ou a carga de trabalho **Desenvolvimento multiplataforma do .NET Core**) e escolha **Modificar**.

## <a name="find-the-red-and-green-squiggles"></a>Localize as linhas onduladas vermelhas e verdes!

Antes de tentar iniciar o aplicativo de exemplo e executar o depurador, verifique o código no editor de códigos para linhas onduladas vermelhas e verdes. Elas representam erros e avisos que são identificados pelo analisador de código do IDE. Os rabiscos vermelhos são erros de tempo de compilação, que você deve corrigir antes de você pode executar o código. As linhas onduladas verdes são avisos. Embora muitas vezes, você pode executar seu aplicativo sem corrigir os avisos, eles podem ser uma fonte de bugs e você muitas vezes economizar tempo e problemas investigando-los. Esses avisos e erros também aparecem na **Error List** janela, se você preferir uma exibição de lista.

No aplicativo de exemplo, você pode ver várias rabiscos vermelhos que você precisa corrigir e um verde que você examinar. Aqui está o primeiro erro.

![Erro ao mostrar como um rabisco vermelho](../debugger/media/write-better-code-red-squiggle.png)

Para corrigir esse erro, você verá outro recurso do IDE, representado por um ícone de lâmpada.

## <a name="check-the-light-bulb"></a>Verifique a lâmpada!

O primeiro Rabisco vermelho representa um erro de tempo de compilação. Passe o mouse sobre ele e você verá a mensagem ```The name `Encoding` does not exist in the current context```.

Observe que esse erro mostra um ícone de lâmpada à esquerda inferior. Junto com o ícone de chave de fenda ![ícone de chave de fenda](../ide/media/screwdriver-icon.png), o ícone de lâmpada ![ícone de lâmpada](../ide/media/light-bulb-icon.png) representa ações rápidas que podem ajudar você a corrigir ou refatorar o código embutido. A lâmpada representa problemas que você *deve* corrigir. A chave de fenda é para os problemas que você pode optar por corrigir. Use a primeira correção sugerida para resolver esse erro, clicando em **usando System. Text** à esquerda.

![Use a lâmpada para corrigir o código](../debugger/media/write-better-code-missing-include.png)

Quando você clica neste item, o Visual Studio adiciona o `using System.Text` instrução na parte superior dos *Program.cs* arquivo e o Rabisco vermelho desaparece. (Quando você não sabe o que fará uma correção sugerida, escolha o **visualizar alterações** link à direita antes de aplicar a correção.)

O erro anterior é comum que você geralmente corrigem adicionando um novo `using` instrução ao seu código. Há vários erros comuns, semelhantes a esta, como ```The type or namespace `Name` cannot be found.``` esses tipos de erros podem indicar uma referência de assembly ausente (com o botão direito no projeto, escolha **Add** > **referência**), um nome digitado incorretamente ou uma biblioteca ausente que você precisará adicionar o usando o NuGet (clique com botão direito no projeto e escolha **gerenciar pacotes NuGet**).

## <a name="fix-the-errors-and-warnings"></a>Corrija os erros e avisos

Há alguns rabiscos mais examinar nesse código. Aqui, você pode ver um erro de conversão de tipo comum. Ao passar o mouse sobre o rabisco, verá que o código está tentando converter uma cadeia de caracteres em um int, o qual não há suporte para a menos que você adicione código explícito para fazer a conversão.

![Erro de conversão de tipo](../debugger/media/write-better-code-conversion-error.png)

Porque o analisador de código não é possível adivinhar sua intenção, não há nenhum lâmpadas para ajudá-lo neste momento. Para corrigir esse erro, você precisa saber a intenção do código. Neste exemplo, não é muito difícil ver que `points` deve ser um valor numérico (inteiro), uma vez que você está tentando adicionar `points` para `totalpoints`.

Para corrigir esse erro, altere o `points` membro o `User` classe desta:

```csharp
[DataMember]
internal string points;
```

para isto:

```csharp
[DataMember]
internal int points;
```

As linhas curvadas vermelhas no editor de códigos desaparecem.

Em seguida, passe o mouse sobre o verde ondulado na declaração do `points` membro de dados. O analisador de código informa que a variável nunca seja atribuída um valor.

![Mensagem de aviso de variável não atribuída](../debugger/media/write-better-code-warning-message.png)

Normalmente, isso representa um problema que precisa ser corrigido. No entanto, no aplicativo de exemplo você está de fato armazenando dados na `points` variável durante o processo de desserialização e, em seguida, adicionando esse valor para o `totalpoints` membro de dados. Neste exemplo, você conhece a intenção do código e ignore o aviso. No entanto, se você deseja eliminar o aviso, você pode substituir o código a seguir:

```csharp
item.totalpoints = users[i].points;
```

com isso:

```csharp
item.points = users[i].points;
item.totalpoints += users[i].points;
```

O Rabisco verde desaparece.

## <a name="fix-an-exception"></a>Corrigir uma exceção

Quando tiver corrigido os rabiscos vermelhos e resolvido – ou pelo menos investigado – o todas as linhas onduladas verdes, você está pronto para iniciar o depurador e executar o aplicativo.

Pressione **F5** (**Depurar > Iniciar Depuração**) ou o botão **Iniciar Depuração** ![Iniciar Depuração](../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração") na barra de ferramentas Depurar.

Neste ponto, o aplicativo de exemplo gera um `SerializationException` exceção (um erro de tempo de execução). Ou seja, o aplicativo restringe nos dados que ele está tentando serializar. Como você iniciou o aplicativo no modo de depuração (o depurador é anexado), o auxiliar de exceção do depurador leva você diretamente para o código que lançou a exceção e fornece a você uma mensagem de erro úteis.

![Ocorre uma SerializationException](../debugger/media/write-better-code-serialization-exception.png)

A mensagem de erro instrui você que o valor `4o` não pode ser analisado como um número inteiro. Neste exemplo, você sabe os dados são inválidos: `4o` deve ser `40`. No entanto, se você não estiver no controle dos dados em um cenário real (digamos que você estiver obtendo-lo de um serviço da web), o que fazer sobre isso? Como consertar isso?

Quando você atinge uma exceção, você precisa fazer algumas perguntas (e responder uma):

* É apenas um bug que você pode corrigir a essa exceção? Ou

* Essa exceção é algo que os usuários podem encontrar?

Se for a primeira opção, corrija o bug. (No aplicativo de exemplo, isso significa que corrigir os dados ruins.) Se for o último, você talvez precise lidar com a exceção no seu código usando um `try/catch` bloco (vamos examinar outras possíveis correções na próxima seção). No aplicativo de exemplo, substitua o código a seguir:

```csharp
users = ser.ReadObject(ms) as User[];
```

com este código:

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

Um `try/catch` bloco tem alguns custos, portanto, você só deseja usá-los quando você realmente precisa deles, ou seja, onde (a) que podem ocorrer na versão de lançamento do aplicativo e onde de desempenho (b) a documentação para o método indica que você deve verificar o exceção (supondo que a documentação está completa!). Em muitos casos, você pode manipular uma exceção adequadamente e o usuário nunca precisará saber sobre ele.

Aqui estão algumas dicas importantes para tratamento de exceções:

* Evite usar um bloco catch vazio, como `catch (Exception) {}`, que não utilize a ação apropriada para expor ou manipular um erro. Um bloco catch vazio ou não informativas pode ocultar exceções e pode tornar seu código mais difícil de depurar em vez de mais fácil.

* Use o `try/catch` bloco de função específica que gerou a exceção (`ReadObject`, no aplicativo de exemplo). Se você usá-lo em torno de uma parte maior de código, você acaba ocultando o local do erro. Por exemplo, não use o `try/catch` bloco em torno da chamada à função pai `ReadToObject`, mostrada aqui, ou você não saberá exatamente onde ocorreu a exceção.

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

* Para funções não familiares que você incluir em seu aplicativo, expecially aqueles interagindo com dados externos (por exemplo, uma solicitação da web), verifique a documentação para ver quais exceções a função é provavelmente lançará. Isso pode ser informações críticas para tratamento de erro apropriado e para depurar seu aplicativo.

Para o aplicativo de exemplo, corrigir a `SerializationException` no `GetJsonData` método alterando `4o` para `40`.

## <a name="clarify-your-code-intent-by-using-assert"></a>Esclarecer a intenção do código, usando assert

Clique no botão **Reiniciar** ![Reiniciar Aplicativo](../debugger/media/dbg-tour-restart.png "RestartApp") na barra de ferramentas Depurar (**Ctrl** + **Shift** + **F5**). Isso reinicia o aplicativo em menos etapas. Você ver a saída a seguir na janela do console.

![Valor nulo na saída](../debugger/media/write-better-code-using-assert-null-output.png)

Você pode ver algo nesta saída que não é exatamente isso. **nome da** e **lastname** para o terceiro registro estão em branco!

Isso é um bom momento para falar sobre uma prática de codificação úteis, normalmente subutilizada, que é usar `assert` as instruções em suas funções. Adicionando o código a seguir, você incluir uma verificação de tempo de execução para ter certeza de que `firstname` e `lastname` não são `null`. Substitua o código a seguir no `UpdateRecords` método:

```csharp
if (existingUser == false)
{
    User user = new User();
    user.firstname = users[i].firstname;
    user.lastname = users[i].lastname;
```

com isso:

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

Adicionando `assert` declarações como essa para suas funções durante o processo de desenvolvimento, você pode ajudar a especificar a intenção do seu código. No exemplo anterior, podemos especificar o seguinte:

* Uma cadeia de caracteres válida é necessária para o primeiro nome
* Uma cadeia de caracteres válida é necessária para o último nome

Especificando a intenção dessa forma, você deve impor seus requisitos. Isso é um método simples e útil que você pode usar a superfície bugs durante o desenvolvimento. (`assert` instruções também são usadas como o elemento principal em testes de unidade.)

Clique no botão **Reiniciar** ![Reiniciar Aplicativo](../debugger/media/dbg-tour-restart.png "RestartApp") na barra de ferramentas Depurar (**Ctrl** + **Shift** + **F5**).

> [!NOTE]
> O `assert` código está ativo somente em uma compilação de depuração.

Quando você reiniciar, o depurador faz uma pausa sobre o `assert` instrução, porque a expressão `users[i].firstname != null` é avaliada como `false` em vez de `true`.

![Assert é resolvida como false](../debugger/media/write-better-code-using-assert.png)

O `assert` erro indica que há um problema que você precisa investigar. `assert` pode abranger muitos cenários em que você não vir necessariamente uma exceção. Neste exemplo, o usuário não verá uma exceção e um `null` valor é adicionado como `firstname` em sua lista de registros. Isso pode causar problemas posteriormente (como você verá na saída do console) e pode ser mais difícil de depurar.

> [!NOTE]
> Em cenários em que você chama um método na `null` valor, um `NullReferenceException` resultados. Normalmente, você deseja evitar o uso de um `try/catch` bloquear para uma exceção geral, ou seja, uma exceção que não esteja ligada à função da biblioteca específica. Qualquer objeto pode lançar um `NullReferenceException`. Se você não tiver certeza, verifique a documentação para a função de biblioteca.

Durante o processo de depuração, é bom para manter um determinado `assert` instrução até que você saiba que você precisa substituí-lo com uma correção de código real. Digamos que você decidir que o usuário pode encontrar a exceção em um build de versão do aplicativo. Nesse caso, você deve refatorar o código para certificar-se de que seu aplicativo não lançar uma exceção fatal ou resultar em algum outro erro. Portanto, para corrigir esse código, substitua o código a seguir:

```csharp
if (existingUser == false)
{
    User user = new User();
```

com este código:

```csharp
if (existingUser == false && users[i].firstname != null && users[i].lastname != null)
{
    User user = new User();
```

Ao usar esse código, você atender aos seus requisitos de código e certifique-se de que um registro com um `firstname` ou `lastname` valor `null` não é adicionado aos dados.

Neste exemplo, adicionamos dois `assert` instruções dentro de um loop. Normalmente, ao usar `assert`, é melhor adicionar `assert` instruções no ponto de entrada (início) de uma função ou método. Você está vendo o `UpdateRecords` método no aplicativo de exemplo. Nesse método, você sabe que problemas se qualquer um dos argumentos de método estiver `null`, portanto, verifique-os com um `assert` instrução no ponto de entrada da função.

```csharp
public static void UpdateRecords(List<User> db, User[] users)
{
    Debug.Assert(db != null);
    Debug.Assert(users != null);
```

Para as instruções anteriores, a sua intenção é que você carregue os dados existentes (`db`) e recuperar novos dados (`users`) antes de atualizar qualquer coisa.

Você pode usar `assert` com qualquer tipo de expressão que resolve `true` ou `false`. Portanto, por exemplo, você pode adicionar um `assert` instrução como esta.

```csharp
Debug.Assert(users[0].points > 0);
```

O código anterior é útil se você quiser especificar a intenção do seguinte: um novo valor de ponto de maior que zero (0) é necessário para atualizar o registro do usuário.

## <a name="inspect-your-code-in-the-debugger"></a>Inspecionar o código no depurador

Okey, agora que você corrigiu críticos tudo que há de errado com o aplicativo de exemplo, você pode mover para outras coisas importantes!

Mostramos a você o auxiliar de exceção do depurador, mas o depurador é uma ferramenta muito mais poderosa que também permite fazer outras coisas, como percorrer seu código e inspecionar suas variáveis. Esses recursos mais poderosos são úteis em muitos cenários, especialmente o seguinte:

* Você está tentando isolar um bug de tempo de execução em seu código, mas não é possível fazer isso usando os métodos e ferramentas abordadas anteriormente.

* Você deseja validar seu código, ou seja, assisti-lo enquanto ele é executado para garantir que ele está se comportando da maneira que você espera e fazendo o que você deseja.

    É instrutivo observar seu código enquanto ele é executado. Você pode aprender mais sobre seu código dessa maneira e normalmente pode identificar os bugs antes que eles quaisquer sintomas óbvias de manifesto.

Para saber como usar os recursos essenciais do depurador, consulte [depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md).

## <a name="fix-performance-issues"></a>Corrigir problemas de desempenho

Bugs de outro tipo incluem código ineficiente que faz com que seu aplicativo seja executado lentamente ou usar muita memória. Em geral, otimizando o desempenho é algo que você pode fazer mais tarde no desenvolvimento de seu aplicativo. No entanto, você poderá encontrar problemas de desempenho no início (por exemplo, você ver que alguma parte do seu aplicativo está sendo executado lentamente), e talvez você precise testar seu aplicativo com as ferramentas de criação de perfil desde o início. Para obter mais informações sobre ferramentas como a ferramenta de uso da CPU e o analisador de memória de criação de perfil, consulte [primeiro, examine as ferramentas de criação de perfil](../profiling/profiling-feature-tour.md).

## <a name="sample-code"></a> Código de exemplo

O código a seguir tem alguns bugs que você pode corrigir o problema usando o IDE do Visual Studio. Aqui, o aplicativo é um aplicativo simple que simula a obtenção de dados JSON de alguma operação desserializar os dados a um objeto e a atualização de uma lista simples com os novos dados.

```csharp
using System;
using System.Collections.Generic;
using System.Runtime.Serialization.Json;
using System.Runtime.Serialization;
using System.IO;

namespace Console_Parse_JSON_DotNetCore
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

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu como evitar e corrigir muitos bugs comuns em seu código e quando usar o depurador. Em seguida, saiba mais sobre como usar o depurador do Visual Studio para corrigir bugs.

> [!div class="nextstepaction"]
> [Depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md)
