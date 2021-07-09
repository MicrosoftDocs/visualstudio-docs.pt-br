---
title: 'Tutorial: Estender um aplicativo de console C# simples'
description: Saiba como desenvolver um aplicativo de console C# Visual Studio, passo a passo.
ms.custom: vs-acquisition, get-started
ms.date: 04/15/2021
ms.technology: vs-ide-general
ms.prod: visual-studio-windows
ms.topic: tutorial
ms.devlang: CSharp
author: j-martens
ms.author: jmartens
manager: jmartens
monikerRange: '>=vs-2019'
dev_langs:
- CSharp
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 84a79015dc4b1147f078b0a970df52c553189c92
ms.sourcegitcommit: 4e09130bcd55bb9cb8ad157507c23b67aa209fad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2021
ms.locfileid: "113549492"
---
# <a name="tutorial-extend-a-simple-c-console-app"></a>Tutorial: Estender um aplicativo de console C# simples

Neste tutorial, você aprenderá a usar o Visual Studio para estender o aplicativo de console criado na primeira parte. Você aprenderá alguns dos recursos Visual Studio que você precisará para o desenvolvimento diário, como gerenciar vários projetos e referenciar pacotes de terceiros.

Se você acabou de concluir [a primeira parte](tutorial-console.md) desta série, já tem o aplicativo de console calculadora.  Para ignorar a parte 1, você pode começar abrindo o projeto de um GitHub repo. O aplicativo Calculadora de C# está no [repo vs-tutorial-samples,](https://github.com/MicrosoftDocs/vs-tutorial-samples)portanto, você pode simplesmente seguir as etapas em Tutorial: Abrir um projeto de um [repo](../tutorial-open-project-from-repo.md) para começar.

## <a name="add-a-new-project"></a>Adicionar um novo projeto

O código do mundo real envolve muitos projetos trabalhando juntos em uma solução. Agora, vamos adicionar outro projeto ao aplicativo calculadora. Essa será uma biblioteca de classes que fornece algumas das funções de calculadora.

1. No Visual Studio, você pode usar o comando de menu de nível superior Arquivo Adicionar Novo Project para adicionar um novo projeto, mas também pode clicar com o botão direito do mouse no nome do projeto existente (chamado de "nó do projeto") e abrir o menu de atalho do projeto (ou menu de  >    >   contexto). Esse menu de atalho contém várias maneiras de adicionar funcionalidade aos seus projetos. Portanto, clique com o botão direito do mouse **no nó do projeto no Gerenciador de Soluções** e escolha **Adicionar** Novo  >  **Project**.

1. Escolha o modelo de projeto C# **Biblioteca de classes (.NET Standard)**.

   ![Captura de tela da seleção de modelo de projeto da Biblioteca de Classes](media/vs-2019/calculator2-add-project-dark.png)

1. Digite o nome do **projeto CalculatorLibrary** e escolha **Criar**. Novamente, escolha .NET 3.1 quando solicitado. Visual Studio cria o novo projeto e o adiciona à solução.

   ![Captura de tela Gerenciador de Soluções projeto de biblioteca de classes CalculatorLibrary adicionado](media/vs-2019/calculator2-solution-explorer-with-class-library-dark2.png)

1. Em vez de *ter Class1.cs*, renomeie o **arquivo CalculatorLibrary.cs**. Você pode clicar no  nome no Gerenciador de Soluções renomeá-lo ou clicar com o botão direito do mouse e escolher Renomear **ou** pressionar a **tecla F2.**

   Você pode ser perguntado se deseja renomear quaisquer referências `Class1` a no arquivo. Não importa como você responde, pois você substituirá o código em uma etapa futura.

1. Agora precisamos adicionar uma referência de projeto para que o primeiro projeto possa usar APIs expostas pela nova biblioteca de classes.  Clique com o botão direito do mouse no **nó Dependências** no primeiro projeto e escolha **Adicionar Project Referência.**

   ![Captura de tela do item de menu Adicionar Project Referência](media/vs-2019/calculator2-add-project-reference-dark.png)

   A caixa de diálogo **Gerenciador de Referências** é exibida. Essa caixa de diálogo permite adicionar referências a outros projetos, bem como assemblies e DLLs COM de que seus projetos precisam.

   ![Captura de tela da caixa de diálogo Gerenciador de Referências](media/vs-2019/calculator2-ref-manager-dark.png)

1. Na caixa **de diálogo Gerenciador** de Referências, marque a caixa de seleção do projeto **CalculatorLibrary** e escolha **OK.**  A referência do projeto aparece em **um nó Projetos** no **Gerenciador de Soluções**.

   ![Captura de tela da Gerenciador de Soluções com referência de projeto](media/vs-2019/calculator2-solution-explorer-with-project-reference-dark2.png)

1. Em *Program.cs,* selecione a classe e todo o código `Calculator` e pressione **CTRL+X** para recortá-la de Program.cs. Em **seguida, em CalculatorLibrary**, *em CalculatorLibrary.cs,* colar o código no `CalculatorLibrary` namespace . Em seguida, faça com que a classe Calculadora `public` a exponha fora da biblioteca. O código em *CalculatorLibrary.cs* agora deve ser semelhante ao seguinte código:

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

1. O primeiro projeto tem uma referência, mas você verá um erro que a chamada Calculator.DoOperation não resolve. Isso porque CalculatorLibrary está em um namespace diferente, portanto, adicione `CalculatorLibrary` o namespace para uma referência totalmente qualificada.

   ```csharp
   result = CalculatorLibrary.Calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   Tente adicionar uma diretiva using ao início do arquivo:

   ```csharp
   using CalculatorLibrary;
   ```

   Essa alteração deve permitir que você remova o namespace CalculatorLibrary do site de chamada, mas agora há uma ambiguidade. A `Calculator` classe em CalculatorLibrary ou a Calculadora é o namespace?  Para resolver a ambiguidade, renomeie o namespace `CalculatorProgram` .

   ```csharp
   namespace CalculatorProgram
   ```

## <a name="reference-net-libraries-write-to-a-log"></a>Bibliotecas .NET de referência: gravar em um log

1. Suponha que agora você queira adicionar um log de todas as operações e escrevê-lo em um arquivo de texto. A classe .NET `Trace` fornece essa funcionalidade. (Também é útil para técnicas básicas de depuração de impressão.)  A classe Trace está em System.Diagnostics e precisamos de classes System.IO como , portanto, comece adicionando as diretivas using na parte superior `StreamWriter` de *CalculatorLibrary.cs:*

   ```csharp
   using System.IO;
   using System.Diagnostics;
   ```

1. Observando como a classe Trace é usada, você precisa manter uma referência para a classe , que está associada a um fluxo de arquivos. Isso significa que a calculadora funcionaria melhor como um objeto, portanto, vamos adicionar um construtor no início da classe Calculadora em *CalculatorLibrary.cs*.

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

1. E precisamos alterar o método estático `DoOperation` em um método de membro, portanto, remova a palavra-chave `static` .  Vamos também adicionar a saída a cada cálculo para o log, para que o DoOperation se pareça com o seguinte código:

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

1. Agora, em *Program.cs*, a chamada estática é sinalizada com uma linha vermelha. Para corrigi-lo, crie `calculator` uma variável adicionando a seguinte linha logo antes do `while (!endApp)` loop:

   ```csharp
   Calculator calculator = new Calculator();
   ```

   E modifique o site de chamada para da seguinte forma, de modo que isso referencia o objeto chamado em letras minúsculas, tornando isso uma invocação de membro, em vez de uma chamada para um `DoOperation` `calculator` método estático:

   ```csharp
   result = calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

1. Execute o programa novamente e, quando terminar, clique com o botão direito do mouse no nó do projeto e escolha Abrir pasta no Explorador de Arquivos **e,** em seguida, navegue para baixo Explorador de Arquivos para a pasta de saída. Pode ser *bin/Debug/netcoreapp3.1* e abrir o *arquivo calculator.log.*

    ```output
    Starting Calculator Log
    Started 7/9/2020 1:58:19 PM
    1 + 2 = 3
    3 * 3 = 9
    ```

Neste ponto, *CalculatorLibrary.cs* deve ter esta aparência:

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

E *Program.cs* deve ser semelhante ao seguinte:

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

## <a name="add-a-nuget-package-write-to-a-json-file"></a>Adicionar um NuGet: gravar em um arquivo JSON

1. Agora, suponha que desejamos a saída das operações em um formato JSON, um formato popular e portátil para armazenar dados de objeto. Para implementar essa funcionalidade, será necessário fazer referência ao NuGet pacote Newtonsoft.Jsem. NuGet pacotes são o veículo principal para distribuição de bibliotecas de classes .NET. No **Gerenciador de Soluções**, clique com  o botão direito do mouse no nó Dependências do projeto CalculatorLibrary e escolha Gerenciar **NuGet Pacotes**.

   ![Captura de tela de Gerenciar NuGet pacotes no menu de atalho](media/vs-2019/calculator2-manage-nuget-packages-dark2.png)

   O NuGet Gerenciador de Pacotes é aberto.

   ![Captura de tela do Gerenciador de Pacotes NuGet](media/vs-2019/calculator2-nuget-package-manager-dark.png)

1. Pesquise Newtonsoft.Jsno pacote e escolha **Instalar**.

   ![Captura de tela das informações do pacote NuGet Newtonsoft](media/vs-2019/calculator2-nuget-newtonsoft-json-dark2.png)

   O pacote é baixado e adicionado ao seu projeto e uma nova entrada aparece no nó Referências **no Gerenciador de Soluções**.

1. Adicione uma diretiva using para o System.IO e Newtonsoft.Jsno pacote no início de *CalculatorLibrary.cs*.

   ```csharp
   using Newtonsoft.Json;
   ```

1. Agora, substitua o construtor da Calculadora pelo código a seguir e crie o objeto membro JsonWriter:

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

1. Modifique `DoOperation` o método para adicionar o código de autor JSON:

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

1. Você precisará adicionar um método para concluir a sintaxe JSON depois que o usuário terminar de inserir dados de operação.

   ```csharp
    public void Finish()
    {
        writer.WriteEndArray();
        writer.WriteEndObject();
        writer.Close();
    }
   ```

1. E em *Program.cs*, adicione uma chamada para Concluir no final.

   ```csharp
            // And call to close the JSON writer before return
            calculator.Finish();
            return;
        }
   ```

1. Crie e execute o aplicativo e, depois de terminar de inserir algumas operações, feche o aplicativo corretamente usando o comando 'n'.  Agora, abra o calculatorlog.jsno arquivo e você verá algo parecido com o seguinte:

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

O Visual Studio depurador é uma ferramenta poderosa que permite executar o código passo a passo, para encontrar o ponto exato em que você errou na programação. Em seguida, você entende quais correções você precisa fazer em seu código. Visual Studio permite que você faça alterações temporárias para que você possa continuar executando o programa.

1. Em *Program.cs*, clique na margem à esquerda do código a seguir (ou abra o menu de atalho e escolha Ponto de Interrupção Inserir Ponto de Interrupção ou  >  pressione **F9**):

   ```csharp
   result = calculator.DoOperation(cleanNum1, cleanNum2, op);
   ```

   O círculo vermelho que aparece indica um ponto de interrupção. Você pode usar pontos de interrupção para pausar seu aplicativo e inspecionar o código. Você pode definir um ponto de interrupção em qualquer linha de código executável.

   ![Captura de tela da configuração de um ponto de interrupção](media/vs-2019/calculator-2-debug-set-breakpoint.png)

1. Compile e execute o aplicativo.

1. No aplicativo em execução, digite alguns valores para o cálculo:

   - Para o primeiro número, digite **8** e insira-o.
   - Para o segundo número, digite **0** e insira-o.
   - Para o operador , vamos nos divertido; digite **d** e insira-o.

   O aplicativo suspende o local em que você criou o ponto de interrupção, que é indicado pelo ponteiro amarelo à esquerda e pelo código realçado. O código realçado ainda não foi executado.

   ![Captura de tela de atingir um ponto de interrupção](media/vs-2019/calculator-2-debug-hit-breakpoint.png)

   Agora, com o aplicativo suspenso, você pode inspecionar o estado do aplicativo.

## <a name="debug-view-variables"></a>Depurar: exibir variáveis

1. No código realçado, passe o mouse sobre variáveis como `cleanNum1` e `op` . Você verá os valores atuais dessas variáveis ( `8` e `d` , respectivamente), que aparecem em DataTips.

   ![Captura de tela da exibição de uma DataTip](media/vs-2019/calculator-2-debug-view-datatip.png)

   Durante a depuração, verificar se as variáveis têm os valores que você espera que eles mantenha geralmente é essencial para corrigir problemas.

2. No painel inferior, veja a janela **Locais.** (Se estiver fechado, escolha **Depurar**  >  **Windows**  >  **Locais para** abri-lo.)

   Na janela Locais, você verá cada variável que está atualmente no escopo, juntamente com seu valor e tipo.

   ![Captura de tela da janela Locais](media/vs-2019/calculator-2-debug-locals-window.png)

3. Veja a **janela Autos.**

   A janela Autos é  semelhante à janela Locais, mas mostra as variáveis imediatamente anteriores e seguindo a linha de código atual em que seu aplicativo está em pausa.

   Em seguida, você executará o código no depurador uma instrução por vez, que é chamada de *etapa*.

## <a name="debug-step-through-code"></a>Depurar: passo a passo do código

1. Pressione **F11** (ou **Depurar**  >  **Etapa em**).

   Usando o comando Step Into, o aplicativo executa a instrução atual e avança para a próxima instrução executável (geralmente a próxima linha de código). O ponteiro amarelo à esquerda sempre indica a instrução atual.

   ![Captura de tela do comando step-into](media/vs-2019/calculator-2-debug-step-into.png)

   Você acabou de entrar no `DoOperation` método na `Calculator` classe .

1. Para obter uma análise hierárquica do fluxo do programa, veja a janela **Pilha de** Chamada. (Se estiver fechado, escolha **Depurar**  >  **Windows**  >  **Pilha de chamada**.)

   ![Captura de tela da pilha de chamada](media/vs-2019/calculator-2-debug-call-stack.png)

   Essa exibição mostra o método atual, indicado pelo ponteiro amarelo, e a segunda linha mostra a função que a chamou do método `Calculator.DoOperation` `Main` em *Program.cs*. A janela **Pilha de Chamadas** mostra a ordem em que os métodos e as funções são chamados. Além disso, ele fornece acesso a muitos recursos do depurador, como Ir para **Código-Fonte,** no menu de atalho.

1. Pressione **F10** (ou **Depurar** Passo a Passo  >  ) várias vezes até que o aplicativo pause a `switch` instrução .

   ```csharp
   switch (op)
   {
   ```

   O comando Step Over é semelhante ao comando Step Into, exceto que, se a instrução atual chamar uma função, o depurador executará o código na função chamada e não suspenderá a execução até que a função retorne. O Step Over é uma maneira mais rápida de navegar pelo código se você não estiver interessado em uma função específica.

1. Pressione **F10** mais uma vez para que o aplicativo pause na linha de código a seguir.

   ```csharp
   if (num2 != 0)
   {
   ```

   Esse código verifica se há um caso de divisão por zero. Se o aplicativo continuar, ele lançará uma exceção geral (um erro), mas digamos que você considere isso um bug e queira fazer outra coisa, como exibir o valor retornado real no console. Uma opção é usar um recurso de depurador chamado Editar e continuar para fazer alterações no código e, em seguida, continuar a depuração. No entanto, mostraremos um truque diferente para modificar temporariamente o fluxo de execução.

## <a name="debug-test-a-temporary-change"></a>Depurar: testar uma alteração temporária

1. Selecione o ponteiro amarelo, atualmente em pausa na `if (num2 != 0)` instrução e arraste-o para a instrução a seguir.

   ```csharp
   result = num1 / num2;
   ```

   Ao fazer isso, o aplicativo ignora completamente a instrução para que você possa ver o que acontece `if` quando você divide por zero.

1. Pressione **F10** para executar a linha de código.

1. Passe o mouse `result` sobre a variável e você verá que ela armazena um valor de `Infinity` .

   Em C#, `Infinity` é o resultado quando você divide por zero.

1. Pressione **F5** (ou, **Depurar**  >  **Continuar Depuração).**

   O símbolo Infinito aparece no console como resultado da operação matemática.

1. Feche o aplicativo corretamente usando o comando 'n'.

## <a name="code-complete"></a>Conclusão do código

Este é o código completo para o arquivo *CalculatorLibrary.cs,* depois que todas as etapas foram concluídas:

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

E este é o código para *Program.cs:* 

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
> [Continuar com a Visual Studio do IDE](/../visual-studio-ide.md)

## <a name="see-also"></a>Confira também

- [C# IntelliSense](../../ide/visual-csharp-intellisense.md)
- [Aprenda a depurar o código C# no Visual Studio](tutorial-debugger.md)
