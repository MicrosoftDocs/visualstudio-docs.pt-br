---
title: 'Tutorial: estender um aplicativo de console C# simples'
description: Saiba como desenvolver um aplicativo de console em C# no Visual Studio, passo a passo.
ms.custom: get-started
ms.date: 04/15/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: ghogen
ms.author: ghogen
manager: jmartens
monikerRange: '>=vs-2019'
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: cce069b1c4acb1784388b7afb06e810dbe826d59
ms.sourcegitcommit: 54aac5044a9853a435577acc5a134cb254494ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2021
ms.locfileid: "107584127"
---
# <a name="tutorial-extend-a-simple-c-console-app"></a>Tutorial: estender um aplicativo de console C# simples

Neste tutorial, você aprenderá a usar o Visual Studio para estender o aplicativo de console criado na primeira parte. Você aprenderá alguns dos recursos do Visual Studio que precisará para o desenvolvimento diário, como gerenciar vários projetos e fazer referência a pacotes de terceiros.

Se você acabou de concluir a [primeira parte](tutorial-console.md) desta série, você já tem o aplicativo de console da calculadora.  Para ignorar a parte 1, você pode começar abrindo o projeto de um repositório GitHub. O aplicativo de calculadora do C# está no [repositório vs-tutorial-Samples](https://github.com/MicrosoftDocs/vs-tutorial-samples), portanto, você pode apenas seguir as etapas no [tutorial: abrir um projeto de um repositório](../tutorial-open-project-from-repo.md) para começar.

## <a name="add-a-new-project"></a>Adicionar um novo projeto

O código do mundo real envolve muitos projetos trabalhando juntos em uma solução. Agora, vamos adicionar outro projeto ao aplicativo Calculator. Essa será uma biblioteca de classes que fornece algumas das funções de calculadora.

1. No Visual Studio, você pode usar o **arquivo** de comando de menu de nível superior  >  **Adicionar**  >  **novo projeto** para adicionar um novo projeto, mas você também pode clicar com o botão direito do mouse no nome do projeto existente (chamado de "nó do projeto") e abrir o menu de atalho do projeto (ou menu de contexto). Esse menu de atalho contém várias maneiras de adicionar funcionalidade aos seus projetos. Portanto, clique com o botão direito do mouse no nó do projeto em **Gerenciador de soluções** e escolha **Adicionar**  >  **novo projeto**.

1. Escolha a biblioteca de classes de modelo de projeto C# **(.net Standard)**.

   ![Captura de tela de seleção de modelo de projeto de biblioteca de classes](media/vs-2019/calculator2-add-project-dark.png)

1. Digite o nome do projeto **CalculatorLibrary** e escolha **criar**. Novamente, escolha .NET 3,1 quando solicitado. O Visual Studio cria o novo projeto e o adiciona à solução.

   ![Captura de tela de Gerenciador de Soluções com o projeto de biblioteca de classes CalculatorLibrary adicionado](media/vs-2019/calculator2-solution-explorer-with-class-library-dark2.png)

1. Em vez de ter *Class1. cs*, renomeie o arquivo **CalculatorLibrary. cs**. Você pode clicar no nome em **Gerenciador de soluções** para renomeá-lo ou clicar com o botão direito do mouse e escolher **renomear** ou pressionar a tecla **F2** .

   Você pode receber uma pergunta se deseja renomear todas as referências a `Class1` no arquivo. Não importa como você responde, já que você substituirá o código em uma etapa futura.

1. Agora, precisamos adicionar uma referência de projeto, para que o primeiro projeto possa usar APIs expostas pela nova biblioteca de classes.  Clique com o botão direito do mouse no nó **dependências** no primeiro projeto e escolha **Adicionar referência de projeto**.

   ![Captura de tela do item de menu Adicionar referência de projeto](media/vs-2019/calculator2-add-project-reference-dark.png)

   A caixa de diálogo **Gerenciador de Referências** é exibida. Essa caixa de diálogo permite que você adicione referências a outros projetos, bem como assemblies e DLLs COM que seus projetos precisam.

   ![Captura de tela da caixa de diálogo Gerenciador de referências](media/vs-2019/calculator2-ref-manager-dark.png)

1. Na caixa de diálogo **Gerenciador de referências** , marque a caixa de seleção do projeto **CalculatorLibrary** e escolha **OK**.  A referência do projeto é exibida em um nó **projetos** no **Gerenciador de soluções**.

   ![Captura de tela de Gerenciador de Soluções com referência de projeto](media/vs-2019/calculator2-solution-explorer-with-project-reference-dark2.png)

1. Em *Program. cs*, selecione a `Calculator` classe e todo o seu código e pressione **Ctrl + X** para recortá-lo de Program. cs. Em seguida, em **CalculatorLibrary**, em *CalculatorLibrary. cs*, Cole o código no `CalculatorLibrary` namespace. Em seguida, torne a classe Calculator `public` para expô-la fora da biblioteca. O código em *CalculatorLibrary. cs* agora deve ser semelhante ao seguinte código:

   ```csharp
   using System;

    namespace CalculatorLibrary
    {
        public class Calculator
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
    }
   ```

1. O primeiro projeto tem uma referência, mas você verá um erro que a chamada calculadora. DoOperation não resolve. Isso ocorre porque o CalculatorLibrary está em um namespace diferente, portanto, adicione `CalculatorLibrary` o namespace para uma referência totalmente qualificada.

   ```csharp
   result = CalculatorLibrary.Calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   Em vez disso, tente adicionar uma diretiva using ao início do arquivo:

   ```csharp
   using CalculatorLibrary;
   ```

   Essa alteração deve permitir que você remova o namespace CalculatorLibrary do site de chamada, mas agora há uma ambiguidade. É `Calculator` a classe em CalculatorLibrary ou é a calculadora do namespace?  Para resolver a ambiguidade, renomeie o namespace `CalculatorProgram` .

   ```csharp
   namespace CalculatorProgram
   ```

## <a name="reference-net-libraries-write-to-a-log"></a>Bibliotecas .NET de referência: gravar em um log

1. Suponha que agora você queira adicionar um log de todas as operações e gravá-la em um arquivo de texto. A `Trace` classe .NET fornece essa funcionalidade. (Também é útil para as técnicas básicas de depuração de impressão.)  A classe Trace está em System. Diagnostics e precisaremos de classes System.IO como `StreamWriter` , portanto, comece adicionando as diretivas using na parte superior de *CalculatorLibrary. cs*:

   ```csharp
   using System.IO;
   using System.Diagnostics;
   ```

1. Observando como a classe Trace é usada, você precisa manter em uma referência para a classe, que está associada a um FileStream. Isso significa que a calculadora funcionaria melhor como um objeto, então vamos adicionar um construtor no início da classe Calculator em *CalculatorLibrary. cs*.

   ```csharp
   public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculator.log");
            Trace.Listeners.Add(new TextWriterTraceListener(logFile));
            Trace.AutoFlush = true;
            Trace.WriteLine("Starting Calculator Log");
            Trace.WriteLine(String.Format("Started {0}", System.DateTime.Now.ToString()));
        }

    public double DoOperation(double num1, double num2, string op)
        {
   ```

1. E precisamos alterar o `DoOperation` método estático para um método de membro, portanto, remova a `static` palavra-chave.  Vamos também adicionar a saída a cada cálculo para o log, para que a dooperação se pareça com o seguinte código:

   ```csharp
   public double DoOperation(double num1, double num2, string op)
   {
        double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

        // Use a switch statement to do the math.
        switch (op)
        {
            case "a":
                result = num1 + num2;
                Trace.WriteLine(String.Format("{0} + {1} = {2}", num1, num2, result));
                break;
            case "s":
                result = num1 - num2;
                Trace.WriteLine(String.Format("{0} - {1} = {2}", num1, num2, result));
                break;
            case "m":
                result = num1 * num2;
                Trace.WriteLine(String.Format("{0} * {1} = {2}", num1, num2, result));
                break;
            case "d":
                // Ask the user to enter a non-zero divisor.
                if (num2 != 0)
                {
                    result = num1 / num2;
                    Trace.WriteLine(String.Format("{0} / {1} = {2}", num1, num2, result));
                }
                    break;
            // Return text for an incorrect option entry.
            default:
                break;
        }
        return result;
    }
   ```

1. Agora, de volta em *Program. cs*, a chamada estática é sinalizada com um ondulado vermelho. Para corrigi-lo, crie uma `calculator` variável adicionando a linha a seguir logo antes do `while (!endApp)` loop:

   ```csharp
   Calculator calculator = new Calculator();
   ```

   E modifique o site de chamada para da seguinte `DoOperation` maneira, para que isso referencie o objeto nomeado `calculator` em minúsculas, tornando essa invocação de membro, em vez de uma chamada para um método estático:

   ```csharp
   result = calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

1. Execute o programa novamente e, quando terminar, clique com o botão direito do mouse no nó do projeto e escolha **abrir pasta no explorador de arquivos** e navegue para baixo no explorador de arquivos até a pasta de saída. Pode ser *bin/Debug/netcoreapp 3.1* e abrir o arquivo *Calculator. log* .

    ```output
    Starting Calculator Log
    Started 7/9/2020 1:58:19 PM
    1 + 2 = 3
    3 * 3 = 9
    ```

Neste ponto, o *CalculatorLibrary. cs* deve ser semelhante ao seguinte:

```csharp
using System;
using System.IO;
using System.Diagnostics;


namespace CalculatorLibrary
{
    public class Calculator
    {

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculator.log");
            Trace.Listeners.Add(new TextWriterTraceListener(logFile));
            Trace.AutoFlush = true;
            Trace.WriteLine("Starting Calculator Log");
            Trace.WriteLine(String.Format("Started {0}", System.DateTime.Now.ToString()));
        }

        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.

            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    Trace.WriteLine(String.Format("{0} + {1} = {2}", num1, num2, result));
                    break;
                case "s":
                    result = num1 - num2;
                    Trace.WriteLine(String.Format("{0} - {1} = {2}", num1, num2, result));
                    break;
                case "m":
                    result = num1 * num2;
                    Trace.WriteLine(String.Format("{0} * {1} = {2}", num1, num2, result));
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        Trace.WriteLine(String.Format("{0} / {1} = {2}", num1, num2, result));
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            return result;
        }
    }
}
```

E *Program. cs* deve ser semelhante ao seguinte:

```csharp
using System;
using CalculatorLibrary;

namespace CalculatorProgram
{
   
    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            Calculator calculator = new Calculator();
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
                    result = calculator.DoOperation(cleanNum1, cleanNum2, op); 
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

## <a name="add-a-nuget-package-write-to-a-json-file"></a>Adicionar um pacote NuGet: gravar em um arquivo JSON

1. Agora suponha que desejamos gerar as operações em um formato JSON, um formato popular e portátil para armazenar dados de objeto. Para implementar essa funcionalidade, precisaremos fazer referência ao pacote NuGet Newtonsoft.Jsno. Os pacotes NuGet são o principal veículo para a distribuição de bibliotecas de classes .NET. Em **Gerenciador de soluções**, clique com o botão direito do mouse no nó **dependências** para o projeto CalculatorLibrary e escolha **gerenciar pacotes NuGet**.

   ![Captura de tela de gerenciar pacotes NuGet no menu de atalho](media/vs-2019/calculator2-manage-nuget-packages-dark2.png)

   O Gerenciador de pacotes NuGet é aberto.

   ![Captura de tela do Gerenciador de Pacotes NuGet](media/vs-2019/calculator2-nuget-package-manager-dark.png)

1. Procure Newtonsoft.Jsno pacote e escolha **instalar**.

   ![Captura de tela das informações do pacote NuGet do Newtonsoft](media/vs-2019/calculator2-nuget-newtonsoft-json-dark2.png)

   O pacote é baixado e adicionado ao seu projeto e uma nova entrada é exibida no nó referências em **Gerenciador de soluções**.

1. Adicione uma diretiva using para o System.IO e Newtonsoft.Jsno pacote no início de *CalculatorLibrary. cs*.

   ```csharp
   using Newtonsoft.Json;
   ```

1. Agora, substitua o construtor da calculadora pelo código a seguir e crie o objeto do membro JsonWriter:

   ```csharp
        JsonWriter writer;

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculatorlog.json");
            logFile.AutoFlush = true;
            writer = new JsonTextWriter(logFile);
            writer.Formatting = Formatting.Indented;
            writer.WriteStartObject();
            writer.WritePropertyName("Operations");
            writer.WriteStartArray();
        }
   ```

1. Modifique o `DoOperation` método para adicionar o código do gravador JSON:

   ```csharp
        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.
            writer.WriteStartObject();
            writer.WritePropertyName("Operand1");
            writer.WriteValue(num1);
            writer.WritePropertyName("Operand2");
            writer.WriteValue(num2);
            writer.WritePropertyName("Operation");
            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    writer.WriteValue("Add");
                    break;
                case "s":
                    result = num1 - num2;
                    writer.WriteValue("Subtract");
                    break;
                case "m":
                    result = num1 * num2;
                    writer.WriteValue("Multiply");
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        writer.WriteValue("Divide");
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            writer.WritePropertyName("Result");
            writer.WriteValue(result);
            writer.WriteEndObject();

            return result;
        }
   ```

1. Você precisará adicionar um método para concluir a sintaxe JSON quando o usuário terminar de inserir dados de operação.

   ```csharp
    public void Finish()
    {
        writer.WriteEndArray();
        writer.WriteEndObject();
        writer.Close();
    }
   ```

1. E em *Program. cs*, adicione uma chamada para concluir no final.

   ```csharp
            // And call to close the JSON writer before return
            calculator.Finish();
            return;
        }
   ```

1. Compile e execute o aplicativo e, depois de terminar de inserir algumas operações, feche o aplicativo corretamente usando o comando ' n'.  Agora, abra o calculatorlog.jsno arquivo e você verá algo semelhante ao seguinte:

   ```json
   {
    "Operations": [
        {
        "Operand1": 2.0,
        "Operand2": 3.0,
        "Operation": "Add",
        "Result": 5.0
        },
        {
        "Operand1": 3.0,
        "Operand2": 4.0,
        "Operation": "Multiply",
        "Result": 12.0
        }
    ]
   }
   ```

## <a name="debug-set-and-hit-a-breakpoint"></a>Depurar: definir e atingir um ponto de interrupção

O depurador do Visual Studio é uma ferramenta poderosa que permite executar o código passo a passo para encontrar o ponto exato em que você fez um erro de programação. Em seguida, você entende as correções que precisa fazer em seu código. O Visual Studio permite fazer alterações temporárias para que você possa continuar executando o programa.

1. Em *Program. cs*, clique na margem à esquerda do código a seguir (ou abra o menu de atalho e escolha **ponto** de interrupção  >  **Inserir ponto** de interrupção ou pressione **F9**):

   ```csharp
   result = calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   O círculo vermelho que aparece indica um ponto de interrupção. Você pode usar pontos de interrupção para pausar seu aplicativo e inspecionar o código. Você pode definir um ponto de interrupção em qualquer linha executável de código.

   ![Captura de tela da definição de um ponto de interrupção](media/vs-2019/calculator-2-debug-set-breakpoint.png)

1. Compile e execute o aplicativo.

1. No aplicativo em execução, digite alguns valores para o cálculo:

   - Para o primeiro número, digite **8** e insira-o.
   - Para o segundo número, digite **0** e insira-o.
   - Para o operador, vamos nos divertir; Digite **d** e insira-o.

   O aplicativo suspende onde você criou o ponto de interrupção, que é indicado pelo ponteiro amarelo à esquerda e o código realçado. O código realçado ainda não foi executado.

   ![Captura de tela de atingir um ponto de interrupção](media/vs-2019/calculator-2-debug-hit-breakpoint.png)

   Agora, com o aplicativo suspenso, você pode inspecionar o estado do aplicativo.

## <a name="debug-view-variables"></a>Depurar: exibir variáveis

1. No código realçado, passe o mouse sobre variáveis como `cleanNum1` e `op` . Você vê os valores atuais para essas variáveis ( `8` e `d` , respectivamente), que aparecem em DataTips.

   ![Captura de tela da exibição de um DataTip](media/vs-2019/calculator-2-debug-view-datatip.png)

   Ao depurar, verificar se as variáveis contêm os valores que você espera que elas tenham, muitas vezes, são essenciais para corrigir problemas.

2. No painel inferior, examine a janela **locais** . (Se estiver fechado, escolha **depurar**  >  **Windows**  >  **Locais** para abri-lo.)

   Na janela locais, você vê cada variável que está atualmente no escopo, juntamente com seu valor e tipo.

   ![Captura de tela da janela locais](media/vs-2019/calculator-2-debug-locals-window.png)

3. Examine a janela **automáticos** .

   A janela Autos é semelhante à janela **locais** , mas mostra as variáveis imediatamente precedentes e seguindo a linha de código atual em que seu aplicativo está em pausa.

   Em seguida, você executará o código na instrução do depurador uma por vez, que é chamada de *Stepping*.

## <a name="debug-step-through-code"></a>Depurar: percorrer código

1. Pressione **F11** (ou **depurar**  >  **etapa para dentro**).

   Usando o comando Step Into, o aplicativo executa a instrução atual e avança para a próxima instrução executável (geralmente a próxima linha de código). O ponteiro amarelo à esquerda sempre indica a instrução atual.

   ![Captura de tela do comando Step Into](media/vs-2019/calculator-2-debug-step-into.png)

   Você acabou de se deparar com o `DoOperation` método na `Calculator` classe.

1. Para obter uma visão hierárquica do fluxo do programa, examine a janela **pilha de chamadas** . (Se estiver fechado, escolha **depurar**  >  **Windows**  >  **Pilha de chamadas**.)

   ![Captura de tela da pilha de chamadas](media/vs-2019/calculator-2-debug-call-stack.png)

   Essa exibição mostra o `Calculator.DoOperation` método atual, indicado pelo ponteiro amarelo, e a segunda linha mostra a função que o chamou, do `Main` método em *Program. cs*. A janela **Pilha de Chamadas** mostra a ordem em que os métodos e as funções são chamados. Além disso, ele fornece acesso a vários recursos do depurador, como **ir para código-fonte**, no menu de atalho.

1. Pressione **F10** (ou **depurar**  >  **etapa**) várias vezes até que o aplicativo pause na `switch` instrução.

   ```csharp
   switch (op)
   {
   ```

   O comando Step Over é semelhante ao comando Step Into, exceto que, se a instrução atual chamar uma função, o depurador executará o código na função chamada e não suspenderá a execução até que a função retorne. O passo é uma maneira mais rápida de navegar no código se você não estiver interessado em uma função específica.

1. Pressione **F10** mais uma vez para que o aplicativo pause na linha de código a seguir.

   ```csharp
   if (num2 != 0)
   {
   ```

   Esse código verifica se há um caso de divisão por zero. Se o aplicativo continuar, ele emitirá uma exceção geral (um erro), mas digamos que você considere esse bug e queira fazer algo mais, como exibir o valor real retornado no console. Uma opção é usar um recurso do depurador chamado Edit-and-Continue para fazer alterações no código e, em seguida, continuar a depuração. No entanto, mostraremos um truque diferente para modificar temporariamente o fluxo de execução.

## <a name="debug-test-a-temporary-change"></a>Depurar: testar uma alteração temporária

1. Selecione o ponteiro amarelo, atualmente pausado na `if (num2 != 0)` instrução e arraste-o para a instrução a seguir.

   ```csharp
   result = num1 / num2;
   ```

   Ao fazer isso, o aplicativo ignora completamente a `if` instrução, para que você possa ver o que acontece quando você divide por zero.

1. Pressione **F10** para executar a linha de código.

1. Focalize a `result` variável e você verá que ela armazena um valor de `Infinity` .

   No C#, `Infinity` é o resultado quando você divide por zero.

1. Pressione **F5** (ou, **debug**  >  **continue Debugging**).

   O símbolo de infinito é exibido no console como o resultado da operação matemática.

1. Feche o aplicativo corretamente usando o comando ' n'.

## <a name="code-complete"></a>Conclusão do código

Aqui está o código completo para o arquivo *CalculatorLibrary. cs* , depois que todas as etapas forem concluídas:

```csharp
using System;
using System.IO;
using System.Diagnostics;
using Newtonsoft.Json;

namespace CalculatorLibrary
{
    public class Calculator
    {

        JsonWriter writer;

        public Calculator()
        {
            StreamWriter logFile = File.CreateText("calculatorlog.json");
            logFile.AutoFlush = true;
            writer = new JsonTextWriter(logFile);
            writer.Formatting = Formatting.Indented;
            writer.WriteStartObject();
            writer.WritePropertyName("Operations");
            writer.WriteStartArray();
        }

        public double DoOperation(double num1, double num2, string op)
        {
            double result = double.NaN; // Default value is "not-a-number" which we use if an operation, such as division, could result in an error.
            writer.WriteStartObject();
            writer.WritePropertyName("Operand1");
            writer.WriteValue(num1);
            writer.WritePropertyName("Operand2");
            writer.WriteValue(num2);
            writer.WritePropertyName("Operation");
            // Use a switch statement to do the math.
            switch (op)
            {
                case "a":
                    result = num1 + num2;
                    writer.WriteValue("Add");
                    break;
                case "s":
                    result = num1 - num2;
                    writer.WriteValue("Subtract");
                    break;
                case "m":
                    result = num1 * num2;
                    writer.WriteValue("Multiply");
                    break;
                case "d":
                    // Ask the user to enter a non-zero divisor.
                    if (num2 != 0)
                    {
                        result = num1 / num2;
                        writer.WriteValue("Divide");
                    }
                    break;
                // Return text for an incorrect option entry.
                default:
                    break;
            }
            writer.WritePropertyName("Result");
            writer.WriteValue(result);
            writer.WriteEndObject();

            return result;
        }

        public void Finish()
        {
            writer.WriteEndArray();
            writer.WriteEndObject();
            writer.Close();
        }
    }
}
```

E aqui está o código para *Program. cs*: 

```csharp
using System;
using CalculatorLibrary;

namespace CalculatorProgram
{
   
    class Program
    {
        static void Main(string[] args)
        {
            bool endApp = false;
            // Display title as the C# console calculator app.
            Console.WriteLine("Console Calculator in C#\r");
            Console.WriteLine("------------------------\n");

            Calculator calculator = new Calculator();
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
                    result = calculator.DoOperation(cleanNum1, cleanNum2, op); 
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
            calculator.Finish();
            return;
        }
    }
}
```

## <a name="next-steps"></a>Próximas etapas

Parabéns por concluir este tutorial. Para saber ainda mais, acompanhe os tutoriais a seguir.

> [!div class="nextstepaction"]
> [Continuar com mais tutoriais do C#](/dotnet/csharp/tutorials/)

> [!div class="nextstepaction"]
> [Continuar com a visão geral do IDE do Visual Studio](/../visual-studio-ide.md)

## <a name="see-also"></a>Confira também

- [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
- [Aprenda a depurar o código C# no Visual Studio](tutorial-debugger.md)
