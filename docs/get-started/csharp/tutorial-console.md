---
title: 'Tutorial: Criar um aplicativo de console C# simples '
description: Saiba como criar aplicativos de console em C# do Visual Basic no Visual Studio, passo a passo.
ms.custom: vs-acquisition, get-started
ms.date: 02/10/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: j-martens
ms.author: jmartens
manager: jmartens
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 20732b0d7fb09de6079b0c1b7b06d2ae89802a5b
ms.sourcegitcommit: e7629e132a4d2fad6bb5869e4d68d9dbeeae9631
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2021
ms.locfileid: "113649183"
---
# <a name="tutorial-create-a-simple-c-console-app-in-visual-studio-part-1-of-2"></a>Tutorial: Criar um aplicativo de console C# simples Visual Studio (parte 1 de 2)

Neste tutorial, você usará o Visual Studio para criar e executar um aplicativo de console C# e explorar alguns recursos do IDE (ambiente de desenvolvimento integrado) do Visual Studio enquanto faz isso. Este tutorial é a parte 1 de uma série de tutoriais de duas partes.

Neste tutorial, você irá:

> [!div class="checklist"]
> * Crie um Visual Studio projeto.
> * Crie um aplicativo de console C#.
> * Depure o aplicativo.
> * Feche seu aplicativo.
> * Inspecione o código completo.

[Na parte 2,](tutorial-console-part-2.md)você estenderá esse aplicativo com projetos adicionais, truques de depuração e referenciar pacotes de terceiros.

## <a name="prerequisites"></a>Pré-requisitos

Você deve ter o Visual Studio instalado.

::: moniker range="vs-2017"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2019"

Se você ainda não tiver instalado o Visual Studio, acesse a página [Visual Studio downloads](https://visualstudio.microsoft.com/downloads) para instalá-lo gratuitamente.

::: moniker-end

::: moniker range="vs-2022"

Se você ainda não instalou o Visual Studio 2022 Preview, acesse a página de downloads do [Visual Studio 2022 Preview](https://visualstudio.microsoft.com/vs/preview/vs2022) para instalá-lo gratuitamente.

::: moniker-end

## <a name="create-a-project"></a>Criar um projeto

Para começar, criaremos um projeto de aplicativo em C#. O tipo de projeto inclui todos os arquivos de modelo que você precisará, mesmo sem adicionar nada!

::: moniker range="vs-2017"

1. Abra o Visual Studio 2017.

2. Na barra de menus superior, escolha **Arquivo**  >    >  **Novo Project**.
   (Como alternativa, pressione **Ctrl** + **Shift** + **N**).

3. No painel esquerdo da caixa de diálogo **Novo Projeto**, expanda **C#** e, em seguida, escolha **.NET Core**. No painel central, escolha **Aplicativo de Console (.NET Core)**. Em seguida, nomeia a Calculadora **_de arquivos_**.

   ![Modelo de projeto do aplicativo do console (.NET Core) na caixa de diálogo Novo projeto no IDE do Visual Studio](./media/new-project-csharp-calculator-console-app.png)

### <a name="add-a-workload-optional"></a>Adicionar uma carga de trabalho (opcional)

Se o modelo de projeto **Aplicativo do Console (.NET Core)** não for exibido, você poderá obtê-lo adicionando a carga de trabalho **Desenvolvimento .NET Core de multiplataforma**. Veja aqui como fazer isso.

#### <a name="option-1-use-the-new-project-dialog-box"></a>Opção 1: usar a caixa de diálogo Novo Projeto

1. Selecione o link **Abrir o Instalador do Visual Studio** no painel esquerdo da caixa de diálogo **Novo Projeto**.

   ![Escolha o link Abrir Instalador do Visual Studio na caixa de diálogo Novo Projeto](./media/csharp-open-visual-studio-installer-generic-dark.png)

1. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento multiplaforma do .NET Core** e, em seguida, selecione **Modificar**.

   ![Carga de trabalho de desenvolvimento multiplaforma do .NET Core no Instalador do Visual Studio](./media/dot-net-core-xplat-dev-workload.png)

#### <a name="option-2-use-the-tools-menu-bar"></a>Opção 2: usar a barra de menus Ferramentas

1. Cancele a caixa **de diálogo Novo Project** e, na barra de menus superior, escolha **Ferramentas** Obter Ferramentas > **e Recursos**.

1. O Instalador do Visual Studio é iniciado. Escolha a carga de trabalho **Desenvolvimento multiplaforma do .NET Core** e, em seguida, selecione **Modificar**.

::: moniker-end

::: moniker range=">=vs-2019"

1. Abra o Visual Studio.

1. Na janela inicial, escolha **Criar um novo projeto.**

   ![Exibir a janela 'Criar um novo projeto'](../../get-started/media/vs-2019/create-new-project-dark-theme.png)

1. Na janela **Criar um novo projeto,** escolha **C#** na lista Idioma. Em seguida, **Windows** na lista Plataforma e **Console** na lista de tipos de projeto. 

   Depois de aplicar os filtros de tipo de idioma, plataforma e projeto, escolha o **modelo Aplicativo** de Console e, em seguida, **escolha Próximo**.

    :::image type="content" source="./media/vs-2019/csharp-create-new-project-console-net-core.png" alt-text="Escolha o modelo de C# para o Aplicativo de Console (.NET Framework)":::

   > [!NOTE]
   > Se você não vir o modelo **Aplicativo de Console,** poderá instalá-lo na **janela Criar um novo** projeto. Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**.
   >
   > ![O link 'Instalar mais ferramentas e recursos' da mensagem 'Não encontrou o que precisa?' na janela 'Criar novo projeto'](../../get-started/media/vs-2019/not-finding-what-looking-for.png) 
   > 
   > Em seguida, no Instalador do Visual Studio, escolha a carga de trabalho de **desenvolvimento multiplataforma do .NET Core**.
   >
   > ![Carga de trabalho de desenvolvimento multiplaforma do .NET Core no Instalador do Visual Studio](./media/dot-net-core-xplat-dev-workload.png)
   >
   > Depois disso, escolha o botão **Modificar** no Instalador do Visual Studio. Pode ser solicitado que você salve seu trabalho; nesse caso, faça isso. Em seguida, escolha **Continuar** para instalar a carga de trabalho. Em seguida, retorne para a etapa 2 deste procedimento para "[Criar um projeto](#create-a-project)".

1. Na janela **Configurar seu novo projeto**, digite ou insira *Calculadora* na caixa **Nome do projeto**. Em seguida, escolha **Próximo.**

    :::image type="content" source="./media/vs-2019/csharp-name-your-calculator-project.png" alt-text="Na janela &quot;Configurar seu novo projeto&quot;, dê ao projeto o nome 'Calculadora'":::
   
1. Na janela **Informações adicionais,** **o .NET Core 3.1** já deve estar selecionado para sua estrutura de destino. Caso não, selecione **.NET Core 3.1**. Em seguida, escolha **Criar**.

    :::image type="content" source="./media/vs-2019/csharp-target-framework.png" alt-text="na janela &quot;Na janela &quot;Informações adicionais&quot;, certifique-se de que o .NET Core 3.1 está selecionado":::

   O Visual Studio abre seu novo projeto, que inclui o código "Olá, Mundo" padrão.

::: moniker-end

## <a name="create-the-app"></a>Criar o aplicativo

Primeiro, exploraremos os cálculos matemáticos básicos de inteiro em C#. Em seguida, adicionaremos o código para criar uma calculadora básica. Depois disso, depuraremos o aplicativo para encontrar e corrigir erros. E, por fim, refinaremos o código para torná-lo mais eficiente.

### <a name="explore-integer-math"></a>Explorar a matemática de inteiros

Vamos começar com alguns cálculos matemáticos básicos de inteiro em C#.

1. No editor de códigos, exclua o código padrão "Olá, Mundo".

    ![Excluir o código padrão Olá, Mundo do novo aplicativo de calculadora](./media/csharp-console-calculator-deletehelloworld.png)

   Especificamente, exclua a linha com o texto: `Console.WriteLine("Hello World!");`.

1. Em seu lugar, digite o seguinte código:

    ```csharp
            int a = 42;
            int b = 119;
            int c = a + b;
            Console.WriteLine(c);
            Console.ReadKey();
    ```

    Observe que quando você faz isso, o recurso IntelliSense no Visual Studio oferece a opção de preencher automaticamente a entrada.

    > [!NOTE]
    > A animação a seguir não se destina a duplicar o código anterior. Ele destina-se apenas a mostrar como o recurso de preenchimento automático funciona.

    ![Animação de código de matemática de inteiro que mostra o recurso de preenchimento automático do IntelliSense no IDE do Visual Studio](./media/integer-math-intellisense.gif)

1. Escolha o botão **verde Iniciar** ao lado de **Calculadora** para criar e executar seu programa ou pressione **F5**.

   ![Escolha o botão Calculadora para executar o aplicativo na barra de ferramentas](./media/csharp-console-calculator-button.png)

   Uma janela do console é aberta mostrando a soma de 42 + 119, que é **161**.

    ![Janela do console mostrando os resultados de matemática de inteiros](./media/csharp-console-integer-math.png)

1. **(Opcional)** Você pode alterar o operador para alterar o resultado. Por exemplo, você pode alterar o operador `+` na linha de código `int c = a + b;` para `-` em uma subtração, `*` para multiplicação ou `/` para divisão. Em seguida, quando você executar o programa, o resultado também será alterado.

1. Feche a janela do console.

### <a name="add-code-to-create-a-calculator"></a>Adicionar código para criar uma calculadora

Vamos continuar com a adição de um conjunto mais complexo de código de calculadora ao seu projeto.

1. Exclua todo o código exibido no editor de códigos.

1. Insira ou cole o seguinte novo código no editor de códigos:

    ```csharp
    using System;

    namespace Calculator
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Declare variables and then initialize to zero.
                int num1 = 0; int num2 = 0;

                // Display title as the C# console calculator app.
                Console.WriteLine("Console Calculator in C#\r");
                Console.WriteLine("------------------------\n");

                // Ask the user to type the first number.
                Console.WriteLine("Type a number, and then press Enter");
                num1 = Convert.ToInt32(Console.ReadLine());

                // Ask the user to type the second number.
                Console.WriteLine("Type another number, and then press Enter");
                num2 = Convert.ToInt32(Console.ReadLine());

                // Ask the user to choose an option.
                Console.WriteLine("Choose an option from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                // Use a switch statement to do the math.
                switch (Console.ReadLine())
                {
                    case "a":
                        Console.WriteLine($"Your result: {num1} + {num2} = " + (num1 + num2));
                        break;
                    case "s":
                        Console.WriteLine($"Your result: {num1} - {num2} = " + (num1 - num2));
                        break;
                    case "m":
                        Console.WriteLine($"Your result: {num1} * {num2} = " + (num1 * num2));
                        break;
                    case "d":
                        Console.WriteLine($"Your result: {num1} / {num2} = " + (num1 / num2));
                        break;
                }
                // Wait for the user to respond before closing.
                Console.Write("Press any key to close the Calculator console app...");
                Console.ReadKey();
            }
        }
    }
    ```

1. Escolha **Calculadora** para executar seu programa ou pressione **F5**.

   ![Escolha o botão Calculadora para executar o aplicativo na barra de ferramentas](./media/csharp-console-calculator-button.png)

   Uma janela do console é aberta.

1. Exiba o aplicativo na janela do console e, em seguida, siga os prompts para adicionar os números **42** e **119**.

   O aplicativo deverá ser semelhante à seguinte captura de tela:

    ![Janela do console mostrando o aplicativo de Calculadora que inclui prompts de quais ações devem ser executadas](./media/csharp-console-calculator.png)

### <a name="add-functionality-to-the-calculator"></a>Adicionar funcionalidade à calculadora

Ajustaremos o código para adicionar mais funcionalidade.

### <a name="add-decimals"></a>Adicionar decimais

Atualmente, o aplicativo de calculadora aceita e retorna números inteiros. No entanto, ele será mais preciso se adicionarmos um código que permita decimais.

Como mostrado na captura de tela a seguir, se você executar o aplicativo e dividir o número 42 pelo número 119, o resultado será 0 (zero), o que não é exato.

![Janela do console mostrando o aplicativo de Calculadora que não retorna um numeral decimal como resultado](./media/csharp-console-calculator-nodecimal.png)

Vamos corrigir o código para que ele identifique decimais.

1. Pressione **Ctrl**  +  **H** para abrir o controle **Localizar e substituir** .

1. Altere cada instância da variável `int` para `float`.

   Verifique se ativou/desativou as opções **Diferenciar maiúsculas de minúsculas** (**Alt**+**C**) e **Coincidir palavra inteira** (**Alt**+**W**) no controle **Localizar e substituir**.

    ![Animação do controle Localizar e Substituir que mostra como alterar a variável int para float](./media/find-replace-control-animation.gif)

1. Execute novamente o aplicativo de calculadora e divida o número **42** pelo número **119**.

   Observe que o aplicativo agora retorna um numeral decimal em vez de zero.

    ![Janela do console mostrando o aplicativo de Calculadora que agora retorna um numeral decimal como resultado](./media/csharp-console-calculator-decimal.png)

No entanto, o aplicativo produz apenas um resultado decimal. Vamos fazer mais alguns ajustes no código, de modo que o aplicativo possa calcular decimais também.

1. Use o controle **Localizar e substituir** (**Ctrl**  +  **H**) para alterar cada instância da `float` variável para `double` e para alterar cada instância do `Convert.ToInt32` método para `Convert.ToDouble` .

1. Execute o aplicativo de calculadora e divida o número **42,5** pelo número **119,75**.

   Observe que o aplicativo agora aceita valores decimais e retorna um numeral decimal mais longo como resultado.

    ![Janela do console mostrando o aplicativo de Calculadora que agora aceita números decimais e retorna um numeral decimal mais longo como resultado](./media/csharp-console-calculator-usedecimals.png)

    (Corrigiremos o número de casas decimais na seção [Revisar o código](#revise-the-code).)

## <a name="debug-the-app"></a>Depurar o aplicativo

Melhoramos nosso aplicativo de calculadora básica, mas ele ainda não é à prova de falhas para tratar exceções, como erros de entrada do usuário.

Por exemplo, se você tentar dividir um número por zero ou inserir um caractere alfa quando o aplicativo espera um caractere numérico (ou vice-versa), o aplicativo pode parar de funcionar, retornar um erro ou retornar um resultado não numérico inesperado.

Vamos examinar alguns erros comuns de entrada do usuário, localizá-los no depurador se eles aparecerem e corrigi-los no código.

> [!TIP]
> Para obter mais informações sobre o depurador e como ele funciona, confira a página [Introdução ao depurador do Visual Studio](../../debugger/debugger-feature-tour.md).

### <a name="fix-the-divide-by-zero-error"></a>Corrigir o erro de "divisão por zero"

Quando você tenta dividir um número por zero, o aplicativo de console pode congelar e, em seguida, mostrar o que há de errado no editor de código.

   ![captura de tela do editor de código Visual Studio mostrando uma linha realçada em amarelo e um erro sem tratamento de exceção para ' tentativa de dividir por zero '.](./media/csharp-console-calculator-dividebyzero-error.png)

> [!NOTE]
> Às vezes, o aplicativo não congela e o depurador não mostrará um erro de divisão por zero. Em vez disso, o aplicativo pode retornar um resultado não numérico inesperado, como um símbolo de infinito. A correção de código a seguir ainda se aplica.

Vamos alterar o código para tratar esse erro.

1. Exclua o código exibido diretamente entre `case "d":` e o comentário `// Wait for the user to respond before closing`.

1. Substitua-o pelo seguinte código:

   ```csharp
            // Ask the user to enter a non-zero divisor until they do so.
                while (num2 == 0)
                {
                    Console.WriteLine("Enter a non-zero divisor: ");
                    num2 = Convert.ToInt32(Console.ReadLine());
                }
                Console.WriteLine($"Your result: {num1} / {num2} = " + (num1 / num2));
                break;
        }
    ```

   Depois que você adicionar o código, a seção com a instrução `switch` deverá ser semelhante à seguinte captura de tela:

   ![A seção alterada e revisada no editor de códigos do Visual Studio](./media/csharp-console-calculator-switch-code.png)

Agora, quando você dividir qualquer número por zero, o aplicativo solicitará outro número. Melhor ainda: não irá parar de perguntar até que você forneça um número diferente de zero.

   ![captura de tela do editor de código Visual Studio mostrando o código para a instrução switch com a verificação de entrada de um divisor diferente de zero adicionado.](./media/csharp-console-calculator-dividebyzero.png)

### <a name="fix-the-format-error"></a>Corrigir o erro de "formato"

Se você inserir um caractere alfa quando o aplicativo esperar um caractere numérico (ou vice-versa), o aplicativo de console congelará. Em seguida, o Visual Studio mostra o que há de errado no editor de códigos.

   ![O editor de códigos do Visual Studio mostra um erro de formato](./media/csharp-console-calculator-format-error.png)

Para corrigir esse erro, precisamos refatorar o código que inserimos anteriormente.

#### <a name="revise-the-code"></a>Revisar o código

Em vez de depender da classe `program` para tratar todo o código, dividiremos nosso aplicativo em duas classes: `Calculator` e `Program`.

A classe `Calculator` fará a maior parte do trabalho de cálculo e a classe `Program` cuidará do trabalho de captura de erros e da interface do usuário.

Vamos começar.

1. Exclua tudo no `Calculator` namespace entre suas chaves de abertura e fechamento:

    ```csharp
    using System;

    namespace Calculator
    {
        
    }
    ```

1. Depois, adicione uma nova classe `Calculator`, da seguinte maneira:

    ```csharp
    class Calculator
    {
        public static double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    break;
                case "s":
                    result = num1 - num2;
                    break;
                case "m":
                    result = num1 * num2;
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            return result;
        }
    }

    ```

1. Em seguida, adicione uma nova classe `Program`, da seguinte maneira:

    ```csharp
    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            while (!endApp)
            {
                // Declare variables and set to empty.
                string numInput1 = "";
                string numInput2 = "";
                double result = 0;

                // Ask the user to type the first number.
                Console.Write("Type a number, and then press Enter: ");
                numInput1 = Console.ReadLine();

                double cleanNum1 = 0;
                while (!double.TryParse(numInput1, out cleanNum1))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput1 = Console.ReadLine();
                }

                // Ask the user to type the second number.
                Console.Write("Type another number, and then press Enter: ");
                numInput2 = Console.ReadLine();

                double cleanNum2 = 0;
                while (!double.TryParse(numInput2, out cleanNum2))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput2 = Console.ReadLine();
                }

                // Ask the user to choose an operator.
                Console.WriteLine("Choose an operator from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                string op = Console.ReadLine();

                try
                {
                    result = Calculator.DoOperation(cleanNum1, cleanNum2, op);
                    if (double.IsNaN(result))
                    {
                        Console.WriteLine("This operation will result in a mathematical error.\n");
                    }
                    else Console.WriteLine("Your result: {0:0.##}\n", result);
                }
                catch (Exception e)
                {
                    Console.WriteLine("Oh no! An exception occurred trying to do the math.\n - Details: " + e.Message);
                }

                Console.WriteLine("------------------------\n");

                // Wait for the user to respond before closing.
                Console.Write("Press 'n' and Enter to close the app, or press any other key and Enter to continue: ");
                if (Console.ReadLine() == "n") endApp = true;

                Console.WriteLine("\n"); // Friendly linespacing.
            }
            return;
        }
    }
    ```

1. Escolha **Calculadora** para executar seu programa ou pressione **F5**.

1. Siga os prompts e divida o número **42** pelo número **119**. O aplicativo deverá ser semelhante à seguinte captura de tela:

    ![Janela do console mostrando o aplicativo de Calculadora refatorado que inclui prompts de quais ações devem ser executadas e tratamento de erro para entradas incorretas](./media/csharp-console-calculator-refactored.png)

    Observe que você tem a opção de inserir mais equações até optar por fechar o aplicativo de console. Além disso, reduzimos também o número de casas decimais no resultado.

## <a name="close-the-app"></a>Feche o aplicativo

1. Se você ainda não fez isso, feche o aplicativo de calculadora.

1. Feche o painel **Saída** no Visual Studio.

   ![Fechar o painel Saída no Visual Studio](./media/csharp-calculator-close-output-pane.png)

1. em Visual Studio, pressione **Ctrl** + **S** para salvar seu aplicativo.

1. Feche o Visual Studio.

## <a name="review-code-complete"></a>Revisão: código concluído

Durante este tutorial, fizemos muitas alterações no aplicativo de calculadora. O aplicativo agora manipula recursos de computação com mais eficiência e trata a maioria dos erros de entrada do usuário.

Este é o código completo, tudo em um só lugar:

```csharp

using System;

namespace Calculator
{
    class Calculator
    {
        public static double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    break;
                case "s":
                    result = num1 - num2;
                    break;
                case "m":
                    result = num1 * num2;
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            return result;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            while (!endApp)
            {
                // Declare variables and set to empty.
                string numInput1 = "";
                string numInput2 = "";
                double result = 0;

                // Ask the user to type the first number.
                Console.Write("Type a number, and then press Enter: ");
                numInput1 = Console.ReadLine();

                double cleanNum1 = 0;
                while (!double.TryParse(numInput1, out cleanNum1))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput1 = Console.ReadLine();
                }

                // Ask the user to type the second number.
                Console.Write("Type another number, and then press Enter: ");
                numInput2 = Console.ReadLine();

                double cleanNum2 = 0;
                while (!double.TryParse(numInput2, out cleanNum2))
                {
                    Console.Write("This is not valid input. Please enter an integer value: ");
                    numInput2 = Console.ReadLine();
                }

                // Ask the user to choose an operator.
                Console.WriteLine("Choose an operator from the following list:");
                Console.WriteLine("\ta - Add");
                Console.WriteLine("\ts - Subtract");
                Console.WriteLine("\tm - Multiply");
                Console.WriteLine("\td - Divide");
                Console.Write("Your option? ");

                string op = Console.ReadLine();

                try
                {
                    result = Calculator.DoOperation(cleanNum1, cleanNum2, op);
                    if (double.IsNaN(result))
                    {
                        Console.WriteLine("This operation will result in a mathematical error.\n");
                    }
                    else Console.WriteLine("Your result: {0:0.##}\n", result);
                }
                catch (Exception e)
                {
                    Console.WriteLine("Oh no! An exception occurred trying to do the math.\n - Details: " + e.Message);
                }

                Console.WriteLine("------------------------\n");

                // Wait for the user to respond before closing.
                Console.Write("Press 'n' and Enter to close the app, or press any other key and Enter to continue: ");
                if (Console.ReadLine() == "n") endApp = true;

                Console.WriteLine("\n"); // Friendly linespacing.
            }
            return;
        }
    }
}

```

## <a name="next-steps"></a>Próximas etapas

:::moniker range="vs-2017"

Continue com mais tutoriais:

> [!div class="nextstepaction"]
> [Tutoriais do C#](/dotnet/csharp/tutorials)

> [!div class="nextstepaction"]
> [Fazer um tour pelo IDE do Visual Studio](../visual-studio-ide.md)

:::moniker-end

:::moniker range=">=vs-2019"

Continue com a segunda parte deste tutorial:

> [!div class="nextstepaction"]
> [Tutorial parte 2: usando vários projetos e pacotes de terceiros](tutorial-console-part-2.md)
:::moniker-end

Além de interesse:

- [Continuar com mais tutoriais do C#](/dotnet/csharp/tutorials/)
- [início rápido: criar um aplicativo web ASP.NET Core](../../ide/quickstart-aspnet-core.md)
- [Aprenda a depurar o código C# no Visual Studio](tutorial-debugger.md)
- Orientações sobre como [criar e executar testes de unidade](../../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)
- [Executar um programa em C#](run-program.md)
- [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
- [continuar com Visual Studio visão geral do IDE](/../visual-studio-ide.md)