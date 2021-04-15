---
title: Depurando código para iniciantes absolutos
description: Se você estiver depurando pela primeira vez, conheça alguns princípios para ajudá-lo a executar seu aplicativo no modo de depuração com o Visual Studio
ms.date: 02/14/2020
ms.topic: tutorial
helpviewer_keywords:
- debugger
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: ee849354d82b11b8d94a737a2b546f686d04d34a
ms.sourcegitcommit: 3985d0ae8d6332f4682c82a10897763173d52961
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2021
ms.locfileid: "107386031"
---
# <a name="how-to-debug-for-absolute-beginners"></a>Como depurar para iniciantes absolutos

Sem falha, o código que escrevemos como desenvolvedores de software nem sempre faz o que esperamos. Às vezes, ele faz algo completamente diferente! Quando isso acontece, a próxima tarefa é descobrir por que e, embora possamos ficar tentados a simplesmente encarar nosso código por horas, é muito mais fácil e eficiente usar uma ferramenta de depuração ou depurador.

Um depurador, infelizmente, não é algo que possa revelar magicamente todos os problemas ou "bugs" em nosso código. *Depuração* significa executar o código passo a passo em uma ferramenta de depuração, como o Visual Studio, para localizar o ponto exato em que você cometeu um erro de programação. Você entenderá quais correções são necessárias para fazer em seu código e as ferramentas de depuração geralmente permitem que você faça alterações temporárias para poder continuar executando o programa.

Usar um depurador com eficiência é também uma habilidade que leva tempo e prática, mas é definitivamente uma tarefa fundamental para todo desenvolvedor de software. Neste artigo, introduziremos os princípios fundamentais da depuração e forneceremos dicas para você começar.

## <a name="clarify-the-problem-by-asking-yourself-the-right-questions"></a>Esclarecer o problema fazendo as perguntas certas a si mesmo

Isso ajuda a esclarecer o problema com o qual você se deparou antes de tentar corrigi-lo. Esperamos que você já se deparou com um problema em seu código, caso contrário, você não estaria aqui tentando descobrir como depurá-lo! Portanto, antes de iniciar a depuração, verifique se você identificou o problema que está tentando resolver:

* O que você esperava que seu código fizesse?

* Em vez disso, o que aconteceu?

    Se você se deparou com um erro (exceção) ao executar seu aplicativo, isso pode ser algo bom! Uma exceção é um evento inesperado encontrado ao executar o código, geralmente um erro de algum tipo. Uma ferramenta de depuração pode levá-lo ao local exato em seu código em que a exceção ocorreu e pode ajudá-lo a investigar possíveis correções.

    Se outra coisa aconteceu, qual é o sintoma do problema? Você já suspeita onde esse problema ocorreu em seu código? Por exemplo, se o código exibir um texto, mas o texto estiver incorreto, você saberá que seus dados são inválidos ou que o código que define o texto de exibição tem algum tipo de bug. Percorrendo o código em um depurador, é possível examinar toda e cada alteração em suas variáveis para descobrir exatamente quando e como os valores incorretos são atribuídos.

## <a name="examine-your-assumptions"></a>Examinar suas suposições

Antes de investigar um bug ou um erro, pense nas suposições que fizeram você esperar determinado resultado. Suposições ocultas ou desconhecidas poderão atrapalhar a identificação de um problema mesmo quando você estiver olhando bem para a causa do problema em um depurador. Você pode ter uma longa lista de possíveis suposições! Veja algumas perguntas para fazer a si mesmo para desafiar suas suposições.

* Você está usando a API certa (ou seja, o objeto, função, método ou propriedade certa)? Uma API que você está usando pode não fazer o que você acha que ela faz. (Depois de analisar a chamada à API no depurador, corrigi-la pode exigir uma viagem para a documentação para ajudar a identificar a API correta.)

* Você está usando uma API corretamente? Talvez você tenha usado a API certa, mas não a usou da maneira correta.

* Seu código contém algum erro de digitação? Alguns erros de digitação, como um simples erro de ortografia de um nome de variável, podem ser difíceis de ver, principalmente ao trabalhar com linguagens que não exigem que variáveis sejam declaradas antes de serem usadas.

* Você fez uma alteração em seu código e supôs que ela não está relacionada ao problema que você está vendo?

* Você esperava que um objeto ou variável contivesse um determinado valor (ou um determinado tipo de valor) diferente do que realmente aconteceu?

* Você conhece a intenção do código? Geralmente é mais difícil depurar o código de outra pessoa. Se não for seu código, poderá ser que você precise passar um tempo aprendendo exatamente o que o código faz antes de poder depurá-lo efetivamente.

    > [!TIP]
    > Ao escrever o código, comece aos poucos e com um código que funciona! (Um bom código de exemplo é útil aqui.) Às vezes, é mais fácil corrigir um conjunto de código grande ou complicado, começando com uma pequena parte do código que demonstra a tarefa principal que você está tentando atingir. Em seguida, será possível modificar ou adicionar código de forma incremental, testando se há erros em cada ponto.

Questionando suas suposições, você pode reduzir o tempo que leva para encontrar um problema em seu código. Você também pode reduzir o tempo necessário para corrigir um problema.

## <a name="step-through-your-code-in-debugging-mode-to-find-where-the-problem-occurred"></a>Percorrer seu código no modo de depuração para encontrar onde o problema ocorreu

Quando normalmente você executa um aplicativo, você vê erros e resultados incorretos somente depois que o código foi executado. Um programa também pode ser encerrado inesperadamente sem informar o porquê.

Executar um aplicativo dentro do depurador, também chamado de *modo de depuração*, significa que o depurador monitora ativamente tudo que está acontecendo conforme o programa é executado. Isso também permite pausar o aplicativo a qualquer momento para examinar seu estado e percorrer seu código linha por linha para observar todos os detalhes à medida que acontecem.

No Visual Studio, você entra no modo de depuração usando **F5** (ou o comando **debug**  >  **Start Debugging** menu ou o botão **Iniciar Depuração** ![inicia a depuração](../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração") na barra de ferramentas Depurar). Se ocorrerem exceções, o Auxiliar de Exceção do Visual Studio levará você ao ponto exato em que a exceção ocorreu e fornecerá outras informações úteis. Para obter mais informações de como tratar exceções no código, confira [Técnicas e ferramentas de depuração](../debugger/write-better-code-with-visual-studio.md).

Se você não recebeu uma exceção, você provavelmente tem uma boa ideia de onde procurar o problema em seu código. É aí que você usa os *pontos de interrupção* com o depurador para ter uma oportunidade de examinar o código mais cuidadosamente. Pontos de interrupção são o recurso mais básico e essencial da depuração confiável. Um ponto de interrupção indica onde o Visual Studio deve pausar seu código em execução para você poder examinar os valores das variáveis ou o comportamento da memória ou a sequência na qual o código é executado.

No Visual Studio, é possível definir rapidamente um ponto de interrupção clicando na margem esquerda ao lado de uma linha de código. Ou coloque o cursor em uma linha e pressione **F9**.

Para ajudar a ilustrar esses conceitos, nós o levamos por meio de um código de exemplo que já tem vários bugs. Estamos usando o C#, mas os recursos de depuração são aplicáveis ao Visual Basic, C++, JavaScript, Python e a outras linguagens com suporte. O código de exemplo para Visual Basic também é fornecido, mas as capturas de tela estão em C#.

### <a name="create-a-sample-app-with-some-bugs"></a>Criar um aplicativo de exemplo (com alguns bugs)

Em seguida, criaremos um aplicativo que tem alguns bugs.

1. Você deve ter o Visual Studio instalado e a carga de trabalho de **desenvolvimento da plataforma cruzada do .NET Core** instalada.

    Se você ainda não instalou o Visual Studio, vá para a página de [downloads do Visual Studio](https://visualstudio.microsoft.com/downloads/) para instalá-lo gratuitamente.

    Se você precisar instalar a carga de trabalho, mas já tiver o Visual Studio, clique em **ferramentas**  >  **obter ferramentas e recursos**. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** e escolha **Modificar**.

1. Abra o Visual Studio.

    ::: moniker range=">=vs-2019"
    Na janela iniciar, escolha **criar um novo projeto**. Digite **console** na caixa de pesquisa, selecione **C#** ou **Visual Basic** como o idioma e, em seguida, escolha **aplicativo de console** para .NET Core. Escolha **Próxima**. Digite um nome de projeto como **ConsoleApp_FirstApp** e clique em **Avançar**.

    Escolha a estrutura de destino recomendada (.NET Core 3,1) ou .NET 5 e, em seguida, escolha **criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Na barra de menus superior, escolha **arquivo**  >  **novo**  >  **projeto**. No painel esquerdo da caixa de diálogo **novo projeto** , em **Visual C#** ou **Visual Basic**, escolha **aplicativo de console** e, no painel central, escolha o **aplicativo de console (.NET Core)**. Digite um nome como **ConsoleApp_FirstApp** e clique em **OK**.
    ::: moniker-end

    Se você não vir o modelo de projeto de **aplicativo de console** para .NET Core, vá para **ferramentas**  >  **obter ferramentas e recursos**, o que abre o instalador do Visual Studio. Escolha a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** e escolha **Modificar**.

    O Visual Studio criará o console do projeto, que será aberto no Gerenciador de Soluções no painel direito.

1. Em *Program. cs* (ou *Program. vb*), substitua todo o código padrão pelo código a seguir. (Selecione a guia idioma correto primeiro, C# ou Visual Basic.)

   #### <a name="c"></a>[C#](#tab/csharp)

    ```csharp
    using System;
    using System.Collections.Generic;

    namespace ConsoleApp_FirstApp
    {
        class Program
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Welcome to Galaxy News!");
                IterateThroughList();
                Console.ReadKey();
            }

            private static void IterateThroughList()
            {
                var theGalaxies = new List<Galaxy>
            {
                new Galaxy() { Name="Tadpole", MegaLightYears=400, GalaxyType=new GType('S')},
                new Galaxy() { Name="Pinwheel", MegaLightYears=25, GalaxyType=new GType('S')},
                new Galaxy() { Name="Cartwheel", MegaLightYears=500, GalaxyType=new GType('L')},
                new Galaxy() { Name="Small Magellanic Cloud", MegaLightYears=.2, GalaxyType=new GType('I')},
                new Galaxy() { Name="Andromeda", MegaLightYears=3, GalaxyType=new GType('S')},
                new Galaxy() { Name="Maffei 1", MegaLightYears=11, GalaxyType=new GType('E')}
            };

                foreach (Galaxy theGalaxy in theGalaxies)
                {
                    Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears + ",  " + theGalaxy.GalaxyType);
                }

                // Expected Output:
                //  Tadpole  400,  Spiral
                //  Pinwheel  25,  Spiral
                //  Cartwheel, 500,  Lenticular
                //  Small Magellanic Cloud .2,  Irregular
                //  Andromeda  3,  Spiral
                //  Maffei 1,  11,  Elliptical
            }
        }

        public class Galaxy
        {
            public string Name { get; set; }

            public double MegaLightYears { get; set; }
            public object GalaxyType { get; set; }

        }

        public class GType
        {
            public GType(char type)
            {
                switch(type)
                {
                    case 'S':
                        MyGType = Type.Spiral;
                        break;
                    case 'E':
                        MyGType = Type.Elliptical;
                        break;
                    case 'l':
                        MyGType = Type.Irregular;
                        break;
                    case 'L':
                        MyGType = Type.Lenticular;
                        break;
                    default:
                        break;
                }
            }
            public object MyGType { get; set; }
            private enum Type { Spiral, Elliptical, Irregular, Lenticular}
        }
    }
    ```

   #### <a name="visual-basic"></a>[Visual Basic](#tab/visualbasic)

    ```vb
    Imports System
    Imports System.Collections.Generic

    Namespace ConsoleApp_FirstApp
        Friend Class Program
            Public Shared Sub Main(ByVal args As String())
                Console.WriteLine("Welcome to Galaxy News!")
                Call IterateThroughList()
                Console.ReadKey()
            End Sub

            Private Shared Sub IterateThroughList()
                Dim theGalaxies = New List(Of Galaxy) From {
                    New Galaxy() With {
                        .Name = "Tadpole",
                        .MegaLightYears = 400,
                        .GalaxyType = New GType("S"c)
                    },
                    New Galaxy() With {
                        .Name = "Pinwheel",
                        .MegaLightYears = 25,
                        .GalaxyType = New GType("S"c)
                    },
                    New Galaxy() With {
                        .Name = "Cartwheel",
                        .MegaLightYears = 500,
                        .GalaxyType = New GType("L"c)
                    },
                    New Galaxy() With {
                        .Name = "Small Magellanic Cloud",
                        .MegaLightYears = 0.2,
                        .GalaxyType = New GType("I"c)
                    },
                    New Galaxy() With {
                        .Name = "Andromeda",
                        .MegaLightYears = 3,
                        .GalaxyType = New GType("S"c)
                    },
                    New Galaxy() With {
                        .Name = "Maffei 1",
                        .MegaLightYears = 11,
                        .GalaxyType = New GType("E"c)
                    }
                }
    
                For Each theGalaxy As Galaxy In theGalaxies
                    Console.WriteLine(theGalaxy.Name & "  " & theGalaxy.MegaLightYears & ",  " & theGalaxy.GalaxyType)
                Next

            End Sub
        End Class
    
        Public Class Galaxy
            Public Property Name As String
            Public Property MegaLightYears As Double
            Public Property GalaxyType As Object
        End Class
    
        Public Class GType
    
            Shared Operator &(ByVal left As String, ByVal right As GType) As String
                Return New String(left & right.ToString())
            End Operator
            Public Sub New(ByVal type As Char)
                Select Case type
                    Case "S"c
                        MyGType = GType.Type.Spiral
                    Case "E"c
                        MyGType = GType.Type.Elliptical
                    Case "l"c
                        MyGType = GType.Type.Irregular
                    Case "L"c
                        MyGType = GType.Type.Lenticular
                    Case Else
                End Select
    
            End Sub
    
            Private _MyGType As String
            Public Property MyGType As Object
                Get
                    Return _MyGType
                End Get
                Set(ByVal value As Object)
                    _MyGType = value.ToString()
                End Set
            End Property
    
            Private Enum Type
                Spiral
                Elliptical
                Irregular
                Lenticular
            End Enum
        End Class
    End Namespace
    ```

    ---

    Nossa intenção para esse código é exibir o nome da galáxia, a distância até ela e o tipo de galáxia. Tudo isso em uma lista. Para depurar, é importante entender a intenção do código. Veja o formato para uma linha na lista que desejamos mostrar na saída:

    *nome da galáxia*, *distância*, *tipo de galáxia*.

### <a name="run-the-app"></a>Executar o aplicativo

1. Pressione **F5** ou o botão **Iniciar Depuração** ![Iniciar Depuração](../debugger/media/dbg-tour-start-debugging.png "Iniciar Depuração") na barra de ferramentas depurar, localizada acima do editor de códigos.

    O aplicativo é iniciado e não há exceções mostradas pelo depurador. No entanto, a saída que você vê na janela do console é não o que você espera. Esta é a saída esperada:

    ```
    Tadpole  400,  Spiral
    Pinwheel  25,  Spiral
    Cartwheel, 500,  Lenticular
    Small Magellanic Cloud .2,  Irregular
    Andromeda  3,  Spiral
    Maffei 1,  Elliptical
    ```

    Mas, em vez disso, vemos o seguinte:

    ```
    Tadpole  400,  ConsoleApp_FirstApp.GType
    Pinwheel  25,  ConsoleApp_FirstApp.GType
    Cartwheel, 500,  ConsoleApp_FirstApp.GType
    Small Magellanic Cloud .2,  ConsoleApp_FirstApp.GType
    Andromeda  3,  ConsoleApp_FirstApp.GType
    Maffei 1, 11,  ConsoleApp_FirstApp.GType
    ```

    Examinando a saída e nosso código, sabemos que `GType` é o nome da classe que armazena o tipo de galáxia. Estamos tentando mostrar o tipo de galáxia real (como "Espiral"), não o nome de classe!

### <a name="debug-the-app"></a>Depurar o aplicativo

1. Com o aplicativo ainda em execução, defina um ponto de interrupção clicando na margem esquerda ao lado da chamada de método `Console.WriteLine` nesta linha de código.

    #### <a name="c"></a>[C#](#tab/csharp)

    ```csharp
    foreach (Galaxy theGalaxy in theGalaxies)
    {
        Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears + ",  " + theGalaxy.GalaxyType);
    }
    ```

    #### <a name="visual-basic"></a>[Visual Basic](#tab/visualbasic)

    ```vb
    For Each theGalaxy As Galaxy In theGalaxies
        Console.WriteLine(theGalaxy.Name & "  " & theGalaxy.MegaLightYears & ",  " & theGalaxy.GalaxyType)
    Next
    ```

    ---
    Quando você definir o ponto de interrupção, um ponto vermelho será exibido na margem esquerda.

    Como vemos um problema na saída, começaremos a depuração examinando o código anterior que define a saída no depurador.

1. Clique no botão **reiniciar** ![aplicativo de reinicialização](../debugger/media/dbg-tour-restart.png "RestartApp") na barra de ferramentas depurar (**Ctrl**  +  **Shift**  +  **F5**).

    O aplicativo fará uma pausa no ponto de interrupção que você definir. O realce amarelo indica onde o depurador está em pausa (a linha de código amarela ainda não foi executada).

1. Passe o mouse sobre a variável `GalaxyType` à direita e, em seguida, à esquerda do ícone de chave inglesa, expanda `theGalaxy.GalaxyType`. Você verá que `GalaxyType` contém uma propriedade `MyGType` e que o valor da propriedade é definido como `Spiral`.

    ![Captura de tela do depurador do Visual Studio com uma linha de código em amarelo e um menu expandido abaixo da propriedade Galaxy. Galaxytype no final da linha.](../debugger/media/beginners-inspect-variable.png)

    "Espiral" é, na verdade, o valor correto que você estava aguardando para imprimir no console! Portanto, é um bom começo você poder acessar esse valor neste código ao executar o aplicativo. Nesse cenário, estamos usando a API incorreta. Veremos se podemos corrigir isso durante a execução do código no depurador.

1. No mesmo código, ainda durante a depuração, coloque o cursor no final de `theGalaxy.GalaxyType` e altere-o para `theGalaxy.GalaxyType.MyGType`. Embora seja possível fazer essa alteração, o editor de códigos mostra um erro que indica que não é possível compilar esse código. (No Visual Basic, você não verá o erro e esta seção de código funciona)

    ![Captura de tela do depurador do Visual Studio com uma linha de código realçada em vermelho e uma caixa de mensagem editar e continuar com o botão Editar selecionado.](../debugger/media/beginners-edit.png)

   > [!NOTE]
   > Para depurar o código de exemplo Visual Basic, ignore as próximas etapas até que você seja instruído a clicar no botão **reiniciar** ![aplicativo](../debugger/media/dbg-tour-restart.png "RestartApp") de reinicialização.

1. Clique em **Editar** na caixa de mensagem **Editar e continuar**. Você vê uma mensagem de erro agora na janela **Lista de Erros**. O erro indica que o `'object'` não contém uma definição para `MyGType`.

    ![Captura de tela do depurador do Visual Studio com uma linha de código realçada em vermelho e uma janela de Lista de Erros com dois erros listados.](../debugger/media/beginners-no-definition.png)

    Mesmo que definamos cada galáxia com um objeto de tipo `GType` (que tem a propriedade `MyGType`), o depurador não reconhece o objeto `theGalaxy` como um objeto de tipo `GType`. O que está havendo? Você deseja examinar qualquer código que define o tipo de galáxia. Quando você fizer isso, verá que a classe `GType` definitivamente tem uma propriedade de `MyGType`, mas algo não está certo. A mensagem de erro sobre `object` acaba sendo a pista; para o interpretador de linguagem, o tipo parece ser um objeto do tipo `object`, em vez de um objeto do tipo `GType`.

1. Examinando seu código com relação à definição do tipo de galáxia, você acha que a propriedade `GalaxyType` da classe `Galaxy` é especificada como `object`, em vez de `GType`.

    ```csharp
    public object GalaxyType { get; set; }
    ```

1. Altere o código anterior para isto:

    ```csharp
    public GType GalaxyType { get; set; }
    ```

1. Clique no botão **reiniciar** ![aplicativo de reinicialização](../debugger/media/dbg-tour-restart.png "RestartApp") na barra de ferramentas depurar (**Ctrl**  +  **Shift**  +  **F5**) para recompilar o código e reiniciar.

    Agora, quando o depurador for pausado no `Console.WriteLine`, será possível focalizar `theGalaxy.GalaxyType.MyGType` e ver que o valor foi devidamente definido.

1. Remova o ponto de interrupção clicando no círculo do ponto de interrupção na margem esquerda (ou clique com o botão direito do mouse e escolha ponto de interrupção de exclusão de **ponto** de interrupção  >  ) e pressione **F5** para continuar.

    O aplicativo é executado e exibe a saída. Ele parece muito bom agora, mas você percebe uma coisa; você esperava que a galáxia Pequena Nuvem de Magalhães fosse exibida como uma galáxia irregular na saída do console, mas ele mostra nenhum tipo de galáxia.

    ```
    Tadpole  400,  Spiral
    Pinwheel  25,  Spiral
    Cartwheel, 500,  Lenticular
    Small Magellanic Cloud .2,
    Andromeda  3,  Spiral
    Maffei 1,  Elliptical
    ```

1. Defina um ponto de interrupção nesta linha de código antes da instrução switch (antes da instrução SELECT em Visual Basic).

    #### <a name="c"></a>[C#](#tab/csharp)

    ```csharp
    public GType(char type)
    ```

    #### <a name="visual-basic"></a>[Visual Basic](#tab/visualbasic)

    ```vb
    Public Sub New(ByVal type As Char)
    ```

    ---

    Esse código é onde o tipo de galáxia foi definido, portanto, queremos examiná-la mais de perto.

1. Clique no botão **reiniciar** ![aplicativo de reinicialização](../debugger/media/dbg-tour-restart.png "RestartApp") na barra de ferramentas depurar (**Ctrl**  +  **Shift**  +  **F5**) para reiniciar.

    O depurador é pausado na linha de código em que você definiu o ponto de interrupção.

1. Passe o mouse sobre a variável `type`. Você verá um valor de `S` (seguindo o código de caractere). Você está interessado em um valor de `I`, uma vez que você sabe que é um tipo de galáxia irregular.

1. Pressione **F5** e passe o mouse sobre a variável `type` novamente. Repita essa etapa até que você veja um valor de `I` na variável `type`.

    ![Captura de tela do depurador do Visual Studio com uma linha de código em amarelo e uma pequena janela mostrando o valor da variável de tipo como 73 ' I '.](../debugger/media/beginners-inspecting-data.png)

1. Agora pressione **F11** (**Depurar** > **Intervir** ou o botão **Intervir** na Barra de ferramentas de depuração).

    **F11** avança o depurador (e executa o código) uma instrução por vez. **F10** (**Depuração parcial**) é um comando semelhante e ambos são extremamente úteis ao aprender a usar o depurador.

1. Pressione **F11** até parar na linha de código na `switch` instrução para obter um valor de ' I ' ( `Select` instrução para Visual Basic). Aqui, você vê um claro problema decorrente de um erro de digitação. Você esperava que o código avançasse para onde ele é definido `MyGType` como um tipo irregular do Galaxy, mas o depurador, em vez disso, ignora esse código completamente e pausa na `default` seção da `switch` instrução ( `Else` instrução no Visual Basic).

    ![Localizar um erro de digitação](../debugger/media/beginners-typo.png)

    Examinando o código, você vê um erro de digitação na instrução `case 'l'`. Ela deverá ser `case 'I'`.

1. Clique no código de `case 'l'` e substitua-o por `case 'I'`.

1. Remova o ponto de interrupção e, em seguida, clique no botão **Reiniciar** para reiniciar o aplicativo.

    Os bugs são corrigidos agora e você vê a Saída esperada!

    Pressione qualquer tecla para concluir o aplicativo.

## <a name="summary"></a>Resumo

Quando você vir um problema, use o depurador e os [comandos de etapa](../debugger/navigating-through-code-with-the-debugger.md) como **F10** e **F11** para localizar a região de código com o problema.

> [!NOTE]
> Se for difícil identificar a região do código em que o problema ocorre, defina um ponto de interrupção no código executado antes de o problema ocorrer e, em seguida, use os comandos de etapa até que você veja o manifesto do problema. Também é possível usar [tracepoints](../debugger/using-breakpoints.md#BKMK_Print_to_the_Output_window_with_tracepoints) para registrar as mensagens na janela de **Saída**. Examinando as mensagens registradas (e observando quais mensagens ainda não foram registradas!), geralmente é possível isolar a região do código com o problema. Talvez você precise repetir esse processo várias vezes para restringir esse conjunto.

Quando você encontrar a região de código com o problema, use o depurador para investigar. Para encontrar a causa de um problema, inspecione o código do problema durante a execução de seu aplicativo no depurador:

* [Inspecione variáveis](../debugger/view-data-values-in-data-tips-in-the-code-editor.md) e verifique se elas contêm o tipo de valores que devem conter. Se você encontrar um valor incorreto, descubra onde o valor incorreto foi definido (para localizar onde o valor foi definido, talvez precise reiniciar o depurador, examinar a [pilha de chamadas](../debugger/how-to-use-the-call-stack-window.md) ou ambos).

* Verifique se o seu aplicativo está executando o código que você espera. (Por exemplo, no aplicativo de exemplo, esperávamos que o código para a instrução de opção definisse o tipo de galáxia como Irregular, mas o aplicativo ignorou o código devido ao erro de digitação.)

> [!TIP]
> Use um depurador para ajudá-lo a encontrar bugs. Uma ferramenta de depuração poderá localizar bugs *para você* somente se conhecer a intenção do seu código. Uma ferramenta só poderá conhecer a intenção do seu código se você, o desenvolvedor, expressar essa intenção. Gravar [testes de unidade](../test/improve-code-quality.md) é como se faz isso.

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu alguns conceitos gerais de depuração. Em seguida, é possível começar a aprender mais sobre o depurador.

> [!div class="nextstepaction"]
> [Introdução ao depurador](../debugger/debugger-feature-tour.md)
