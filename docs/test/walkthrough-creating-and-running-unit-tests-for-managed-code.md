---
title: Criar e executar testes de unidade para código gerenciado
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- unit tests, walkthrough
- unit tests, creating
- unit tests, generating
- unit tests, running
- unit tests, authoring
ms.author: gewarren
manager: douge
ms.workload:
- dotnet
author: gewarren
ms.openlocfilehash: 13488619b38f5fd974d793d56f6a8d8cf86f15c1
ms.sourcegitcommit: 0cf1e63b6e0e6a0130668278489b21a6e5038084
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39469107"
---
# <a name="walkthrough-create-and-run-unit-tests-for-managed-code"></a>Passo a passo: Criar e executar testes de unidade para código gerenciado

Este artigo orienta você pela criação, execução e personalização de uma série de testes de unidade usando a estrutura de teste de unidade da Microsoft para código gerenciado e o **Gerenciador de Testes** do Visual Studio. Inicie com um projeto C# que está em desenvolvimento, crie testes que exercitem seu código, execute os testes e examine os resultados. Em seguida, você pode alterar o código do projeto e executar os testes novamente.

> [!NOTE]
> Este passo a passo usa a estrutura de teste de unidade do Microsoft para código gerenciado. O **Gerenciador de Testes** também pode executar testes em estruturas de teste de unidade de terceiros que têm adaptadores para o **Gerenciador de Testes**. Para obter mais informações, consulte [Instalar estruturas de teste de unidade de terceiros](../test/install-third-party-unit-test-frameworks.md)

Para obter informações sobre como executar testes em uma linha de comando, confira [Opções de linha de comando de VSTest.Console.exe](vstest-console-options.md).

## <a name="prerequisites"></a>Pré-requisitos

- O projeto Banco. Confira [Projeto de exemplo para criação de testes de unidade](../test/sample-project-for-creating-unit-tests.md).

## <a name="create-a-project-to-test"></a>Criar um projeto para teste

1. Abra o Visual Studio.

2. No menu **Arquivo**, selecione **Novo** > **Projeto**.

   A caixa de diálogo **Novo Projeto** é exibida.

3. Em **Modelos Instalados**, clique em **Visual C#**.

4. Na lista de tipos de aplicativos, clique em **Biblioteca de Classes**.

5. Na caixa **Nome**, digite **Bank** e, em seguida, clique em **OK**.

   O novo projeto Bank é criado e exibido no **Gerenciador de Soluções** com o arquivo *Class1.cs* aberto no editor de códigos.

   > [!NOTE]
   > Se *Class1.cs* não estiver aberto no Editor de Códigos, clique duas vezes no arquivo *Class1.cs* no **Gerenciador de Soluções** para abri-lo.

6. Copie o código-fonte do [Projeto de exemplo para criação de testes de unidade](../test/sample-project-for-creating-unit-tests.md) e substitua o conteúdo original de *Class1.cs* pelo código copiado.

7. Salve o arquivo como *BankAccount.cs*.

8. No menu **Compilar**, clique em **Compilar Solução**.

Agora você tem um projeto chamado Banco. Ele contém o código-fonte para testes e as ferramentas para testá-lo. O namespace de Bank, BankAccountNS, contém a classe pública BankAccount, cujos métodos você testará nos procedimentos a seguir.

Neste artigo, os testes se concentram no método Debit. O método Debit é chamado quando o dinheiro é retirado de uma conta. Esta é a definição do método:

```csharp
// Method to be tested.
public void Debit(double amount)
{
    if(amount > m_balance)
    {
        throw new ArgumentOutOfRangeException("amount");
    }
    if (amount < 0)
    {
        throw new ArgumentOutOfRangeException("amount");
    }
    m_balance += amount;
}
```

## <a name="create-a-unit-test-project"></a>Crie um projeto de teste de unidade

1. No menu **Arquivo**, selecione **Adicionar** > **Novo Projeto**.

2. Na caixa de diálogo **Novo Projeto**, expanda **Instalado**, expanda **Visual C#** e, em seguida, escolha **Teste**.

3. Na lista de modelos, selecione **Projeto de Teste de Unidade**.

4. Na caixa **Nome**, insira `BankTests` e, em seguida, selecione **OK**.

   O projeto **BankTests** é adicionado à solução **Bank**.

5. No projeto **BankTests** adicione uma referência ao projeto **Bank**.

   No **Gerenciador de Soluções**, selecione **Referências** no projeto **BankTests** e, em seguida, escolha **Adicionar Referência** no menu de contexto.

6. Na caixa de diálogo **Gerenciador de Referências**, expanda **Solução** e, em seguida, marque o item **Banco**.

## <a name="create-the-test-class"></a>Criar a classe de teste

Crie uma classe de teste para verificar a classe `BankAccount`. Use o arquivo *UnitTest1.cs* que foi gerado pelo modelo do projeto, mas dê ao arquivo e à classe nomes mais descritivos. Faça isso em uma única etapa renomeando o arquivo no **Gerenciador de Soluções**.

### <a name="rename-a-class-file"></a>Renomear um arquivo de classe

No **Gerenciador de Soluções**, selecione o arquivo *UnitTest1.cs* no projeto BankTests. No menu de contexto, escolha **Renomear** e, em seguida, renomeie o arquivo como *BankAccountTests.cs*. Escolha **Sim** na caixa de diálogo que pergunta se você deseja renomear todas as referências ao elemento de código `UnitTest1` no projeto.

Esta etapa altera o nome da classe para `BankAccountTests`. O arquivo *BankAccountTests.cs* agora contém o seguinte código:

```csharp
using System;
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

### <a name="add-a-using-statement-to-the-project-under-test"></a>Adicionar uma instrução using ao projeto em teste

Adicione também uma instrução `using` à classe para permitir chamadas ao projeto em teste, sem usar nomes totalmente qualificados. Na parte superior do arquivo da classe, adicione:

```csharp
using BankAccountNS;
```

### <a name="test-class-requirements"></a>Requisitos de classe de teste

Os requisitos mínimos para uma classe de teste são:

- O atributo `[TestClass]` é necessário na estrutura de teste de unidade do Microsoft para código gerenciado de qualquer classe que contenha métodos de teste de unidade que você queira executar no Gerenciador de Testes.

- Cada método de teste que você deseja executar com o Gerenciador de Testes precisa ter o atributo `[TestMethod]`.

Pode haver outras classes em um projeto de teste de unidade que não têm o atributo `[TestClass]` e pode haver outros métodos em classes de teste que não têm o atributo `[TestMethod]`. Você pode usar essas classes e métodos em seus métodos de teste.

## <a name="create-the-first-test-method"></a>Criar o primeiro método de teste

Neste procedimento, você escreverá métodos de teste de unidade para verificar o comportamento do método `Debit` da classe `BankAccount`. O método `Debit` é mostrado anteriormente neste artigo.

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

O método é simples: ele define um novo objeto `BankAccount` com um saldo inicial e, em seguida, retira um valor válido. Ele usa o método <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A> para verificar se o saldo final é conforme o esperado.

### <a name="test-method-requirements"></a>Requisitos do método de teste

Um método de teste deve atender aos seguintes requisitos:

- Ele está decorado com o atributo `[TestMethod]`.

- Ele retorna `void`.

- Não pode ter parâmetros.

## <a name="build-and-run-the-test"></a>Criar e executar o teste

1. No menu **Compilar**, escolha **Compilar Solução**.

   Se não houver erros, o **Gerenciador de Testes** será exibido com **Debit_WithValidAmount_UpdatesBalance** listado no grupo **Não Executar Testes**.

   > [!TIP]
   > Se o **Gerenciador de Testes** não for exibido após um build bem-sucedido, escolha **Testar** no menu, **Windows** e, em seguida, **Gerenciador de Testes**.

2. Escolha **Executar Todos** para executar o teste. Durante a execução do teste, a barra de status na parte superior da janela fica animada. Ao final da execução de teste, a barra ficará verde se todos os métodos de teste forem aprovados ou vermelha, se algum teste falhar.

3. Nesse caso, o teste falha. O método de teste é movido para o grupo **Testes com Falha**. Selecione o método no **Gerenciador de Testes** para exibir os detalhes na parte inferior da janela.

## <a name="fix-your-code-and-rerun-your-tests"></a>Corrigir o código e executar os testes novamente

### <a name="analyze-the-test-results"></a>Analisar os resultados de teste

O resultado do teste contém uma mensagem que descreve a falha. Para o método `AreEqual`, a mensagem exibe o que era esperado (o parâmetro **Expected\<*value*>**) e o que foi, de fato, recebido (o parâmetro **Actual\<*value*>**). Você esperava que o saldo diminuísse, mas em vez disso, ele aumentou pelo valor do saque.

O teste de unidade revelou um bug: o valor do saque foi *adicionado* ao saldo da conta quando deveria ser *subtraído*.

### <a name="correct-the-bug"></a>Corrigir o bug

Para corrigir o erro, substitua a linha:

```csharp
m_balance += amount;
```

por:

```csharp
m_balance -= amount;
```

### <a name="rerun-the-test"></a>Executar o teste novamente

No **Gerenciador de Testes**, escolha **Executar Todos** para executar o teste novamente. A barra verde/vermelho fica verde para indicar que o teste foi aprovado, e o teste é movido para o grupo **Testes Aprovados**.

## <a name="use-unit-tests-to-improve-your-code"></a>Usar testes de unidade para melhorar o código

Esta seção descreve como um processo iterativo de análise, desenvolvimento de testes de unidade e refatoração pode ajudá-lo a tornar seu código de produção mais robusto e eficiente.

### <a name="analyze-the-issues"></a>Analisar os problemas

Você criou um método de teste para confirmar que um valor válido é deduzido corretamente no método `Debit`. Agora, verifique se o método gera uma <xref:System.ArgumentOutOfRangeException> se o valor do débito é:

- maior que o saldo ou
- menor que zero.

### <a name="create-the-test-methods"></a>Criar os métodos de teste

Crie um método de teste para verificar o comportamento correto quando o valor do débito é menor que zero:

```csharp
[TestMethod]
[ExpectedException(typeof(ArgumentOutOfRangeException))]
public void Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange()
{
    // Arrange
    double beginningBalance = 11.99;
    double debitAmount = -100.00;
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);

    // Act
    account.Debit(debitAmount);

    // Assert is handled by the ExpectedException attribute on the test method.
}
```

Use o atributo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute> para declarar que a exceção certa foi gerada. O atributo faz com que o teste falhe, a menos que uma <xref:System.ArgumentOutOfRangeException> seja lançada. Se você modificar temporariamente o método em teste para gerar uma <xref:System.ApplicationException> mais genérica quando o valor do débito for menor que zero, o teste se comportará corretamente – ou seja, ele falhará.

Para testar o caso quando o valor retirado é maior que o saldo, realize as seguintes etapas:

1. Criar um novo método de teste chamado `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange`.

2. Copiar o corpo do método de `Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange` para o novo método.

3. Definir `debitAmount` para um número maior que o saldo.

### <a name="run-the-tests"></a>Executar os testes

A execução dos dois métodos de teste demonstra que os testes funcionam corretamente.

### <a name="continue-the-analysis"></a>Continuar a análise

No entanto, os dois últimos métodos de teste também são preocupantes. Você não pode ter certeza de qual condição no método em teste gera a exceção quando um dos testes é executado. Uma forma de diferenciar as duas condições, que é um valor de débito negativo ou um valor maior que o saldo, aumentará a confiança nos testes.

Observe novamente o método em teste e veja que ambas as instruções condicionais usam um construtor `ArgumentOutOfRangeException` que apenas usa o nome do argumento como parâmetro:

```csharp
throw new ArgumentOutOfRangeException("amount");
```

Há um construtor que você pode usar que relata informações muito mais ricas: <xref:System.ArgumentOutOfRangeException.%23ctor(System.String,System.Object,System.String)> inclui o nome do argumento, o valor do argumento e uma mensagem definida pelo usuário. Refatore o método em teste para usar esse construtor. Melhor ainda, use membros de tipo disponíveis publicamente para especificar os erros.

### <a name="refactor-the-code-under-test"></a>Refatorar o código em teste

Primeiro, defina duas constantes para as mensagens de erro no escopo da classe. Coloque-as na classe em teste, BankAccount:

```csharp
public const string DebitAmountExceedsBalanceMessage = "Debit amount exceeds balance";
public const string DebitAmountLessThanZeroMessage = "Debit amount is less than zero";
```

Em seguida, modifique as duas instruções condicionais no método `Debit`:

```csharp
    if (amount > m_balance)
    {
        throw new ArgumentOutOfRangeException("amount", amount, DebitAmountExceedsBalanceMessage);
    }

    if (amount < 0)
    {
        throw new ArgumentOutOfRangeException("amount", amount, DebitAmountLessThanZeroMessage);
    }
```

### <a name="refactor-the-test-methods"></a>Refatorar os métodos de teste

Remova o atributo do método de teste `ExpectedException` e, em vez disso, capture a exceção gerada e verifique sua mensagem associada. O método <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Contains%2A?displayProperty=fullName> fornece a capacidade de comparar duas cadeias de caracteres.

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
    catch (ArgumentOutOfRangeException e)
    {
        // Assert
        StringAssert.Contains(e.Message, BankAccount.DebitAmountExceedsBalanceMessage);
    }
}
```

### <a name="retest-rewrite-and-reanalyze"></a>Testar, gravar e analisar novamente

Suponha que haja um bug no método em teste e que o método `Debit` ainda não gerou uma <xref:System.ArgumentOutOfRangeException>. Desconsidere a geração da mensagem correta com a exceção. Atualmente, o método de teste não lida com esse caso. Se o valor `debitAmount` for válido (ou seja, menor que o saldo mas maior que zero), nenhuma exceção será capturada e, portanto, a declaração nunca será acionada. Ainda assim, o método de teste é aprovado. Isso não é bom, pois você deseja que o método de teste falhe se nenhuma exceção é gerada.

Esse é um bug no método de teste. Para resolver o problema, adicione uma declaração <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Fail%2A> ao final do método de teste para lidar com o caso em que nenhuma exceção é gerada.

Mas uma nova execução do teste mostra que agora o teste *falha* se a exceção correta é capturada. O bloco `catch` captura a exceção, mas o método continua sendo executado e ele falha na nova declaração <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Fail%2A>. Para resolver esse problema, adicione uma instrução `return` após a `StringAssert` no bloco `catch`. Uma nova execução do teste confirma que você corrigiu o problema. A versão final de `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` é parecida com esta:

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
    catch (ArgumentOutOfRangeException e)
    {
        // Assert
        StringAssert.Contains(e.Message, BankAccount.DebitAmountExceedsBalanceMessage);
        return;
    }

    Assert.Fail("The expected exception was not thrown.");
}
```

As melhorias no código de teste levaram a métodos de teste mais robustos e informativos. Porém, o mais importante é que eles também melhoraram o código em teste.
