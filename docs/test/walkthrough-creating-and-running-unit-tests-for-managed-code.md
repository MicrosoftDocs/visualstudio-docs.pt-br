---
title: Tutorial de teste de unidade C#
description: Saiba como criar, executar e personalizar uma série de testes de unidade usando a estrutura de teste de unidade da Microsoft para código gerenciado e o Visual Studio Test Explorer.
ms.custom: SEO-VS-2020
ms.date: 05/14/2019
ms.topic: conceptual
helpviewer_keywords:
- unit tests, walkthrough
- unit tests, creating
- unit tests, generating
- unit tests, running
- unit tests, authoring
ms.author: mikejo
manager: jmartens
ms.workload:
- dotnet
author: mikejo5000
ms.openlocfilehash: a6ab205b7f651f8bb5954bee4998602c79fd78e7
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683923"
---
# <a name="walkthrough-create-and-run-unit-tests-for-managed-code"></a>Passo a passo: Criar e executar testes de unidade para código gerenciado

Este artigo orienta você pela criação, execução e personalização de uma série de testes de unidade usando a estrutura de teste de unidade da Microsoft para código gerenciado e o **Gerenciador de Testes** do Visual Studio. Inicie com um projeto C# que está em desenvolvimento, crie testes que exercitem seu código, execute os testes e examine os resultados. Em seguida, você altera o código do projeto e executa os testes novamente.



## <a name="create-a-project-to-test"></a>Criar um projeto para teste

::: moniker range="vs-2017"

1. Abra o Visual Studio.

2. No menu **arquivo** , selecione **novo** > **projeto**.

   A caixa de diálogo **Novo Projeto** aparecerá.

3. Na categoria **Visual C#** > **.NET Core**, escolha o modelo de projeto **Aplicativo de Console (.NET Core)**.

4. Dê ao projeto o nome **Bank** e clique em **OK**.

   O projeto Bank é criado e exibido no **Gerenciador de Soluções** com o arquivo *Program.cs* aberto no editor de códigos.

   > [!NOTE]
   > Se *Program.cs* não estiver aberto no editor, clique duas vezes no arquivo *Program.cs* no **Gerenciador de Soluções** para abri-lo.

::: moniker-end

::: moniker range=">=vs-2019"

1. Abra o Visual Studio.

2. Na janela iniciar, escolha **criar um novo projeto**.

3. Pesquise e selecione o modelo de projeto de **aplicativo de console** em C# para .NET Core e clique em **Avançar**.

   > [!NOTE]
   > Se você não vir o modelo de **aplicativo de console** , poderá instalá-lo na janela **criar um novo projeto** . Na mensagem **Não encontrou o que precisa?**, escolha o link **Instalar mais ferramentas e recursos**. Em seguida, no Instalador do Visual Studio, escolha a carga de trabalho de **desenvolvimento multiplataforma do .NET Core**.

4. Nomeie o **banco** do projeto e clique em **Avançar**.

   Escolha a estrutura de destino recomendada (.NET Core 3,1) ou .NET 5 e, em seguida, escolha **criar**.

   O projeto Bank é criado e exibido no **Gerenciador de Soluções** com o arquivo *Program.cs* aberto no editor de códigos.

   > [!NOTE]
   > Se *Program.cs* não estiver aberto no editor, clique duas vezes no arquivo *Program.cs* no **Gerenciador de Soluções** para abri-lo.

::: moniker-end

5. Substitua o conteúdo do *Program.cs* pelo seguinte código C# que define uma classe, *BankAccount*:

   ```csharp
   using System;

   namespace BankAccountNS
   {
       /// <summary>
       /// Bank account demo class.
       /// </summary>
       public class BankAccount
       {
           private readonly string m_customerName;
           private double m_balance;

           private BankAccount() { }

           public BankAccount(string customerName, double balance)
           {
               m_customerName = customerName;
               m_balance = balance;
           }

           public string CustomerName
           {
               get { return m_customerName; }
           }

           public double Balance
           {
               get { return m_balance; }
           }

           public void Debit(double amount)
           {
               if (amount > m_balance)
               {
                   throw new ArgumentOutOfRangeException("amount");
               }

               if (amount < 0)
               {
                   throw new ArgumentOutOfRangeException("amount");
               }

               m_balance += amount; // intentionally incorrect code
           }

           public void Credit(double amount)
           {
               if (amount < 0)
               {
                   throw new ArgumentOutOfRangeException("amount");
               }

               m_balance += amount;
           }

           public static void Main()
           {
               BankAccount ba = new BankAccount("Mr. Bryan Walton", 11.99);

               ba.Credit(5.77);
               ba.Debit(11.22);
               Console.WriteLine("Current balance is ${0}", ba.Balance);
           }
       }
   }
   ```

6. Renomeie o arquivo como *BankAccount.cs* clicando com o botão direito do mouse e escolha **Renomear** na **Gerenciador de Soluções**.

7. No menu **Compilar** , clique em **Compilar solução** (ou pressione **Ctrl**  +  **Shift**  +  **B**).

Agora você tem um projeto com métodos que você pode testar. Neste artigo, os testes se concentram no método `Debit`. O método `Debit` é chamado quando o dinheiro é retirado de uma conta.

## <a name="create-a-unit-test-project"></a>Criar um projeto de teste de unidade

1. No menu **Arquivo**, selecione **Adicionar** > **Novo Projeto**.

   > [!TIP]
   > Você também pode clicar com o botão direito do mouse na solução no **Gerenciador de Soluções** e escolher **Adicionar** > **Novo Projeto**.

::: moniker range="vs-2017"

2. Na caixa de diálogo **novo projeto** , expanda **instalado**, expanda **Visual C#** e escolha **teste**.

3. Na lista de modelos, selecione **Projeto de Teste de MSTest (.NET Core)**.

4. Na caixa **Nome**, insira `BankTests` e, em seguida, selecione **OK**.

   O projeto **BankTests** é adicionado à solução **Bank**.

::: moniker-end

::: moniker range=">=vs-2019"

2. Digite **teste de unidade** na caixa de pesquisa, **Selecione C#** como o idioma e, em seguida, selecione o modelo projeto de **teste de unidade** C# para .NET Core e clique em **Avançar**.

   > [!NOTE]
   > A partir do Visual Studio 2019 versão 16,9, o nome do modelo de projeto MSTest mudou de **MSTest Unit Test Project (.NET Core)** para **projeto de teste de unidade**.

3. Nomeie o projeto **BankTests** e clique em **Avançar**.

4. Escolha a estrutura de destino recomendada (.NET Core 3,1) ou .NET 5 e, em seguida, escolha **criar**.

   O projeto **BankTests** é adicionado à solução **Bank**.

::: moniker-end

5. No projeto **BankTests** adicione uma referência ao projeto **Bank**.

   No **Gerenciador de Soluções**, selecione **Dependências** no projeto **BankTests** e, em seguida, escolha **Adicionar Referência** no menu de clique com o botão direito do mouse.

6. Na caixa de diálogo **Gerenciador de Referências**, expanda **Projetos**, selecione **Solução** e, em seguida, marque o item **Banco**.

7. Selecione **OK**.

## <a name="create-the-test-class"></a>Criar a classe de teste

Crie uma classe de teste para verificar a classe `BankAccount`. Use o arquivo *UnitTest1.cs* que foi gerado pelo modelo do projeto, mas dê ao arquivo e à classe nomes mais descritivos.

### <a name="rename-a-file-and-class"></a>Renomear um arquivo e uma classe

1. Para renomear o arquivo, em **Gerenciador de Soluções**, selecione o arquivo *UnitTest1.cs* no projeto BankTests. No menu do clique com o botão direito do mouse, escolha **renomear** (ou pressione **F2**) e renomeie o arquivo para *BankAccountTests.cs*.

::: moniker range="vs-2017"

2. Para renomear a classe, escolha **Sim** na caixa de diálogo que é exibida. Ela solicitará se você também deseja renomear as referências ao elemento de código.

::: moniker-end

::: moniker range=">=vs-2019"

2. Para renomear a classe, posicione o cursor sobre `UnitTest1` no editor de códigos, clique com o botão direito do mouse e escolha **renomear** (ou pressione **F2**). Digite **BankAccountTests** e, em seguida, pressione **Enter**.

::: moniker-end

O arquivo *BankAccountTests.cs* agora contém o código a seguir:

```csharp
using Microsoft.VisualStudio.TestTools.UnitTesting;

namespace BankTests
{
    [TestClass]
    public class BankAccountTests
    {
        [TestMethod]
        public void TestMethod1()
        {
        }
    }
}
```

### <a name="add-a-using-statement"></a>Adicionar uma instrução using

Adicione uma [ `using` instrução](/dotnet/csharp/language-reference/keywords/using-statement) à classe de teste para poder chamar o projeto em teste sem usar nomes totalmente qualificados. Na parte superior do arquivo da classe, adicione:

```csharp
using BankAccountNS;
```

### <a name="test-class-requirements"></a>Requisitos de classe de teste

Os requisitos mínimos para uma classe de teste são:

- O atributo `[TestClass]` é necessário em qualquer classe que contenha métodos de teste de unidade que você queira executar no Gerenciador de Testes.

- Cada método de teste que você deseja reconhecer com o Gerenciador de Testes precisa ter o atributo `[TestMethod]`.

Pode haver outras classes em um projeto de teste de unidade que não têm o atributo `[TestClass]` e pode haver outros métodos em classes de teste que não têm o atributo `[TestMethod]`. Você pode chamar essas classes e métodos dos seus métodos de teste.

## <a name="create-the-first-test-method"></a>Criar o primeiro método de teste

Neste procedimento, você escreverá métodos de teste de unidade para verificar o comportamento do método `Debit` da classe `BankAccount`.

Há pelo menos três comportamentos que precisam ser verificados:

- O método lançará um <xref:System.ArgumentOutOfRangeException> se o valor do débito for maior que o saldo.

- O método gerará um <xref:System.ArgumentOutOfRangeException> se o valor do débito for menor que zero.

- Se o valor do débito for válido, o método subtrairá o valor do débito do saldo da conta.

> [!TIP]
> Você pode excluir o método `TestMethod1` padrão, porque você não o usará neste passo a passo.

### <a name="to-create-a-test-method"></a>Para criar um método de teste

O primeiro teste verifica que um valor válido (ou seja, um que seja menor que o saldo da conta e maior que zero) retira a quantidade correta da conta. Adicione o seguinte método à classe `BankAccountTests`:

```csharp
[TestMethod]
public void Debit_WithValidAmount_UpdatesBalance()
{
    // Arrange
    double beginningBalance = 11.99;
    double debitAmount = 4.55;
    double expected = 7.44;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // Act
    account.Debit(debitAmount);

    // Assert
    double actual = account.Balance;
    Assert.AreEqual(expected, actual, 0.001, "Account not debited correctly");
}
```

O método é simples: ele define um novo objeto `BankAccount` com um saldo inicial e, em seguida, retira um valor válido. Ele usa o método <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A?displayProperty=nameWithType> para verificar se o saldo final é conforme o esperado.

### <a name="test-method-requirements"></a>Requisitos do método de teste

Um método de teste deve atender aos seguintes requisitos:

- Ele está decorado com o atributo `[TestMethod]`.

- Ele retorna `void`.

- Não pode ter parâmetros.

## <a name="build-and-run-the-test"></a>Criar e executar o teste

1. No menu **Compilar** , escolha **Compilar solução** (ou pressione **Ctrl**  +  **Shift**  +  **B**).

2. Se o **Gerenciador de testes** não estiver aberto, abra-o escolhendo **testar** o  >    >  **Gerenciador de testes** do Windows na barra de menus superior (ou pressione **Ctrl**  +  **E**, **T**).

3. Escolha **executar tudo** para executar o teste (ou pressione **Ctrl**  +  **R**, **V**).

   Durante a execução do teste, a barra de status na parte superior da janela **Gerenciador de Testes** fica animada. Ao final da execução de teste, a barra ficará verde se todos os métodos de teste forem aprovados ou vermelha, se algum teste falhar.

   Nesse caso, o teste falha.

4. Selecione o método no **Gerenciador de testes** para exibir os detalhes na parte inferior da janela.

## <a name="fix-your-code-and-rerun-your-tests"></a>Corrigir o código e executar os testes novamente

O resultado do teste contém uma mensagem que descreve a falha. Para o método `AreEqual`, a mensagem exibe o que era esperado e o que foi realmente recebido. Você esperava que o saldo diminuísse, mas em vez disso, ele aumentou pelo valor do saque.

O teste de unidade revelou um bug: o valor do saque foi *adicionado* ao saldo da conta quando deveria ser *subtraído*.

### <a name="correct-the-bug"></a>Corrigir o bug

Para corrigir o erro, no arquivo *BankAccount.cs*, substitua a linha:

```csharp
m_balance += amount;
```

por:

```csharp
m_balance -= amount;
```

### <a name="rerun-the-test"></a>Executar o teste novamente

No **Gerenciador de testes**, escolha **executar tudo** para executar novamente o teste (ou pressione **Ctrl**  +  **R**, **V**). A barra verde/vermelho fica verde para indicar que o teste foi aprovado.

![Gerenciador de Testes no Visual Studio 2019 mostrando a aprovação no teste](media/test-explorer-banktests-passed.png)

## <a name="use-unit-tests-to-improve-your-code"></a>Usar testes de unidade para melhorar o código

Esta seção descreve como um processo iterativo de análise, desenvolvimento de testes de unidade e refatoração pode ajudá-lo a tornar seu código de produção mais robusto e eficiente.

### <a name="analyze-the-issues"></a>Analisar os problemas

Você criou um método de teste para confirmar que um valor válido é deduzido corretamente no método `Debit`. Agora, verifique se o método gera uma <xref:System.ArgumentOutOfRangeException> se o valor do débito é:

- maior que o saldo ou
- menor que zero.

### <a name="create-and-run-new-test-methods"></a>Criar e executar novos métodos de teste

Crie um método de teste para verificar o comportamento correto quando o valor do débito é menor que zero:

```csharp
[TestMethod]
public void Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange()
{
    // Arrange
    double beginningBalance = 11.99;
    double debitAmount = -100.00;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // Act and assert
    Assert.ThrowsException<System.ArgumentOutOfRangeException>(() => account.Debit(debitAmount));
}
```

Use o método <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A> para declarar que a exceção correta foi gerada. Esse método faz com que o teste falhe, a menos que uma <xref:System.ArgumentOutOfRangeException> seja gerada. Se você modificar temporariamente o método em teste para gerar uma <xref:System.ApplicationException> mais genérica quando o valor do débito for menor que zero, o teste se comportará corretamente – ou seja, ele falhará.

Para testar o caso quando o valor retirado é maior que o saldo, realize as seguintes etapas:

1. Criar um novo método de teste chamado `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange`.

2. Copiar o corpo do método de `Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange` para o novo método.

3. Definir `debitAmount` para um número maior que o saldo.

Execute os dois testes e verifique se eles são aprovados.

### <a name="continue-the-analysis"></a>Continuar a análise

O método que está sendo testado pode ser melhorado ainda mais. Com a implementação atual, não temos como saber qual condição (`amount > m_balance` ou `amount < 0`) levou à exceção sendo lançada durante o teste. Nós sabemos apenas que um `ArgumentOutOfRangeException` foi lançado em algum lugar no método. Seria melhor se pudéssemos dizer qual condição em `BankAccount.Debit` fez com que a exceção fosse lançada (`amount > m_balance` ou `amount < 0`) para que possamos ter certeza de que nosso método está checando corretamente seus argumentos.

Observe novamente o método em teste (`BankAccount.Debit`) e veja que ambas as instruções condicionais usam um construtor `ArgumentOutOfRangeException` que apenas usa o nome do argumento como parâmetro:

```csharp
throw new ArgumentOutOfRangeException("amount");
```

Há um construtor que você pode usar que relata informações muito mais ricas: <xref:System.ArgumentOutOfRangeException.%23ctor(System.String,System.Object,System.String)> inclui o nome do argumento, o valor do argumento e uma mensagem definida pelo usuário. Refatore o método em teste para usar esse construtor. Melhor ainda, use membros de tipo disponíveis publicamente para especificar os erros.

### <a name="refactor-the-code-under-test"></a>Refatorar o código em teste

Primeiro, defina duas constantes para as mensagens de erro no escopo da classe. Coloque-os na classe em teste, `BankAccount`:

```csharp
public const string DebitAmountExceedsBalanceMessage = "Debit amount exceeds balance";
public const string DebitAmountLessThanZeroMessage = "Debit amount is less than zero";
```

Em seguida, modifique as duas instruções condicionais no método `Debit`:

```csharp
if (amount > m_balance)
{
    throw new System.ArgumentOutOfRangeException("amount", amount, DebitAmountExceedsBalanceMessage);
}

if (amount < 0)
{
    throw new System.ArgumentOutOfRangeException("amount", amount, DebitAmountLessThanZeroMessage);
}
```

### <a name="refactor-the-test-methods"></a>Refatorar os métodos de teste

Refatore os métodos de teste removendo a chamada a <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.ThrowsException%2A?displayProperty=nameWithType>. Encapsule a chamada a `Debit()` em um bloco `try/catch`, capture a exceção específica que é esperada e verifique a mensagem associada. O método <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Contains%2A?displayProperty=fullName> fornece a capacidade de comparar duas cadeias de caracteres.

Agora, o `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` pode ser parecido com este:

```csharp
[TestMethod]
public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()
{
    // Arrange
    double beginningBalance = 11.99;
    double debitAmount = 20.0;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // Act
    try
    {
        account.Debit(debitAmount);
    }
    catch (System.ArgumentOutOfRangeException e)
    {
        // Assert
        StringAssert.Contains(e.Message, BankAccount.DebitAmountExceedsBalanceMessage);
    }
}
```

### <a name="retest-rewrite-and-reanalyze"></a>Testar, gravar e analisar novamente

Atualmente, o método de teste não lida com todos os casos que deveria. Se o método em teste, o `Debit` método falhou ao lançar um <xref:System.ArgumentOutOfRangeException> quando o `debitAmount` era maior do que o saldo (ou menor que zero), o método de teste passaria. Isso não é bom, pois você deseja que o método de teste falhe se nenhuma exceção é gerada.

Esse é um bug no método de teste. Para resolver o problema, adicione uma declaração <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Fail%2A> ao final do método de teste para lidar com o caso em que nenhuma exceção é gerada.

Uma nova execução do teste mostra que agora o teste *falha* se a exceção correta é capturada. O bloco `catch` captura a exceção, mas o método continua sendo executado e ele falha na nova declaração <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Fail%2A>. Para resolver esse problema, adicione uma instrução `return` após a `StringAssert` no bloco `catch`. Uma nova execução do teste confirma que você corrigiu o problema. A versão final de `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` é parecida com esta:

```csharp
[TestMethod]
public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()
{
    // Arrange
    double beginningBalance = 11.99;
    double debitAmount = 20.0;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // Act
    try
    {
        account.Debit(debitAmount);
    }
    catch (System.ArgumentOutOfRangeException e)
    {
        // Assert
        StringAssert.Contains(e.Message, BankAccount.DebitAmountExceedsBalanceMessage);
        return;
    }

    Assert.Fail("The expected exception was not thrown.");
}
```

### <a name="conclusion"></a>Conclusão

As melhorias no código de teste levaram a métodos de teste mais robustos e informativos. Porém, o mais importante é que eles também melhoraram o código em teste.

> [!TIP]
> Este passo a passo usa a estrutura de teste de unidade do Microsoft para código gerenciado. O **Gerenciador de Testes** também pode executar testes em estruturas de teste de unidade de terceiros que têm adaptadores para o **Gerenciador de Testes**. Para obter mais informações, consulte [instalar estruturas de teste de unidade de](../test/install-third-party-unit-test-frameworks.md)terceiros.

## <a name="see-also"></a>Confira também

Para obter informações sobre como executar testes em uma linha de comando, confira [Opções de linha de comando de VSTest.Console.exe](vstest-console-options.md).
