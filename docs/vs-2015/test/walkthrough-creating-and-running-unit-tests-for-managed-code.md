---
title: 'Passo a passo: Criando e executando testes de unidade para código gerenciado | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- unit tests, walkthrough
- unit tests, creating
- unit tests, generating
- unit tests, running
- unit tests, authoring
ms.assetid: 2b018b18-b412-4e0e-b0ee-b580a2f3ba9c
caps.latest.revision: 85
ms.author: gewarren
manager: douge
ms.openlocfilehash: 50d8190f386a4923fd05cbfaec137791bd9f2b5a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49874495"
---
# <a name="walkthrough-creating-and-running-unit-tests-for-managed-code"></a>Instruções passo a passo: criando e executando testes de unidade para código gerenciado
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo guiará você pela criação, execução e personalização de uma série de testes de unidade usando a estrutura de teste de unidade do Microsoft para código gerenciado e o Gerenciador de Testes do Visual Studio. Inicie com um projeto C# que está em desenvolvimento, crie testes que exercitem seu código, execute os testes e examine os resultados. Você pode alterar o código do seu projeto e executar novamente os testes.  
  
 Esse tópico contém as seguintes seções:  
  
 [Preparar o passo a passo](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Prepare_the_walkthrough)  
  
 [Criar um projeto de teste de unidade](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Create_a_unit_test_project)  
  
 [Criar a classe de teste](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Create_the_test_class)  
  
- [Requisitos de classe de teste](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Test_class_requirements)  
  
  [Criar o primeiro método de teste](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Create_the_first_test_method)  
  
- [Requisitos do método de teste](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Test_method_requirements)  
  
  [Compilar e executar o teste](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Build_and_run_the_test)  
  
  [Corrigir o código e executar novamente os testes](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Fix_your_code_and_rerun_your_tests)  
  
  [Usar testes da unidade para melhorar o código](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Use_unit_tests_to_improve_your_code)  
  
> [!NOTE]
>  Este passo a passo usa a estrutura de teste de unidade do Microsoft para código gerenciado. O Gerenciador de testes também pode executar testes em estruturas de teste de unidade de terceiros que têm adaptadores para o Gerenciador de Testes. Para obter mais informações, consulte [Instalar estruturas de teste de unidade de terceiros](../test/install-third-party-unit-test-frameworks.md)  
  
> [!NOTE]
>  Para obter informações sobre como executar testes de uma linha de comando, consulte [Passo a passo: Usando o utilitário de teste da linha de comando](http://msdn.microsoft.com/library/52c11992-9e94-4067-a4b7-59f19d69d867).  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   O projeto Banco. Consulte [Projeto de exemplo para criação de testes de unidade](../test/sample-project-for-creating-unit-tests.md).  
  
##  <a name="BKMK_Prepare_the_walkthrough"></a> Preparar o passo a passo  
  
1. Abra o Visual Studio.  
  
2. No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
    A caixa de diálogo **Novo Projeto** é exibida.  
  
3. Em **Modelos Instalados**, clique em **Visual C#**.  
  
4. Na lista de tipos de aplicativos, clique em **Biblioteca de Classes**.  
  
5. Na caixa **Nome**, digite `Bank` e clique em **OK**.  
  
   > [!NOTE]
   >  Se o nome "Banco" já foi usado, escolha outro nome para o projeto.  
  
    O novo projeto Banco é criado e exibido no Gerenciador de Soluções com o arquivo Class1.cs aberto no Editor de códigos.  
  
   > [!NOTE]
   >  Se o arquivo Class1. cs não estiver aberto no Editor de códigos, clique duas vezes no arquivo Class1.cs no Gerenciador de Soluções para abri-lo.  
  
6. Copie o código-fonte do [Projeto de exemplo para criar testes de unidade](../test/sample-project-for-creating-unit-tests.md).  
  
7. Substitua o conteúdo original de Class1.cs pelo código do [Projeto de exemplo para criar testes de unidade](../test/sample-project-for-creating-unit-tests.md).  
  
8. Salve o arquivo como BankAccount.cs  
  
9. No menu **Compilar**, clique em **Compilar Solução**.  
  
   Agora você tem um projeto chamado Banco. Ele contém o código-fonte para testes e as ferramentas para testá-lo. O namespace para o Banco, **BankAccountNS**, contém a classe pública **BankAccount**, cujos métodos você testará nos procedimentos a seguir.  
  
   Nesse início rápido, vamos nos concentrar no método `Debit`. O método Debit é chamado quando o dinheiro é retirado de uma conta e contém o seguinte código:  
  
```csharp  
// method under test  
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
  
##  <a name="BKMK_Create_a_unit_test_project"></a> Criar um projeto de teste de unidade  
 **Pré-requisito**: siga as etapas no procedimento [Preparar o passo a passo](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md#BKMK_Prepare_the_walkthrough).  
  
#### <a name="to-create-a-unit-test-project"></a>Para criar um projeto de teste de unidade  
  
1.  No menu **Arquivo** escolha **Adicionar** e depois escolha **Novo Projeto...**.  
  
2.  Na caixa de diálogo Novo Projeto, expanda **Instalado**, expanda **Visual C#** e escolha **Testar**.  
  
3.  Na lista de modelos, selecione **Projeto de Teste de Unidade**.  
  
4.  Na caixa **Nome**, insira BankTest e, em seguida, escolha **OK**.  
  
     O projeto **BankTests** é adicionado à solução **Bank**.  
  
5.  No projeto **BankTests** adicione uma referência à solução **Banco**.  
  
     No Gerenciador de Soluções, selecione **Referências** no projeto **BankTests** e escolha **Adicionar Referência...**  no menu de contexto.  
  
6.  Na caixa de diálogo Gerenciador de Referências, expanda **Solução** e marque o item **Banco**.  
  
##  <a name="BKMK_Create_the_test_class"></a> Criar a classe de teste  
 Precisamos de uma classe de teste para verificar a classe `BankAccount`. Podemos usar o UnitTest1.cs que foi gerado pelo modelo do projeto, mas devemos dar ao arquivo e à classe nomes mais descritivos. É possível fazer isso em uma única etapa, renomeando o arquivo no Gerenciador de Soluções.  
  
 **Renomeando um arquivo de classe**  
  
 No Gerenciador de Soluções, selecione o arquivo UnitTest1.cs no projeto BankTests. No menu de contexto, escolha **Renomear**e, em seguida, renomeie o arquivo como BankAccountTests.cs. Escolha **Sim** na caixa de diálogo que perguntará se você quiser renomear todas as referências no projeto para o elemento de código 'UnitTest1'. Esta etapa altera o nome da classe para `BankAccountTest`.  
  
 O arquivo BankAccountTests.cs agora contém o seguinte código:  
  
```csharp  
// unit test code  
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
  
 **Adicionar uma instrução de uso ao projeto em teste**  
  
 Podemos também adicionar uma instrução de uso à classe para permitir chamadas ao projeto em teste, sem usar nomes totalmente qualificados. Na parte superior do arquivo da classe, adicione:  
  
```csharp  
using BankAccountNS;  
```  
  
###  <a name="BKMK_Test_class_requirements"></a> Requisitos de classe de teste  
 Os requisitos mínimos para uma classe de teste são os seguintes:  
  
- O atributo `[TestClass]` é necessário na estrutura de teste de unidade do Microsoft para código gerenciado de qualquer classe que contenha métodos de teste de unidade que você queira executar no Gerenciador de Testes.  
  
- Cada método de teste que você queira executar com o Gerenciador de Testes deve ter o atributo `[TestMethod]`.  
  
  Pode haver outras classes em um projeto de teste de unidade que não têm o atributo `[TestClass]` e pode haver outros métodos em classes de teste que não têm o atributo `[TestMethod]`. Você pode usar essas classes e métodos em seus métodos de teste.  
  
##  <a name="BKMK_Create_the_first_test_method"></a> Criar o primeiro método de teste  
 Neste procedimento, vamos escrever métodos de teste de unidade para verificar o comportamento do método `Debit` da classe `BankAccount`. O método é listado acima.  
  
 Ao analisar o método em teste, podemos determinar que há pelo menos três comportamentos que precisam ser verificados:  
  
1. O método gerará uma [ArgumentOutOfRangeException] (<!-- TODO: review code entity reference <xref:assetId:///ArgumentOutOfRangeException?qualifyHint=False&amp;autoUpgrade=True>  -->) se o valor do débito for maior que o saldo.  
  
2. Ele também gerará `ArgumentOutOfRangeException` se o valor do débito for menor que zero.  
  
3. Se as verificações de 1.) e 2.) forem atendidas, o método subtrairá o valor do saldo da conta.  
  
   Em nosso primeiro teste, verificamos que um valor válido (menor que o saldo da conta e maior que zero) retira a quantidade correta da conta.  
  
#### <a name="to-create-a-test-method"></a>Para criar um método de teste  
  
1. Adicione uma instrução `BankAccountNS;` usando o arquivo BankAccountTests.cs.  
  
2. Adicione o seguinte método à classe `BankAccountTests`:  
  
   ```csharp  
   // unit test code  
   [TestMethod]  
   public void Debit_WithValidAmount_UpdatesBalance()  
   {  
       // arrange  
       double beginningBalance = 11.99;  
       double debitAmount = 4.55;  
       double expected = 7.44;  
       BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);  
  
       // act  
       account.Debit(debitAmount);  
  
       // assert  
       double actual = account.Balance;  
       Assert.AreEqual(expected, actual, 0.001, "Account not debited correctly");  
   }  
   ```  
  
   O método é bastante simples. Criamos um novo objeto `BankAccount` com um saldo inicial e, em seguida, retiramos um valor válido. Usamos a estrutura de teste de unidade do Microsoft para o método de código gerenciado <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.AreEqual%2A> para verificar se o saldo final é o que esperamos.  
  
###  <a name="BKMK_Test_method_requirements"></a> Requisitos do método de teste  
 Um método de teste deve atender aos seguintes requisitos:  
  
-   O método deve ser decorado com o atributo `[TestMethod]`.  
  
-   O método deve retornar `void`.  
  
-   O método não pode ter parâmetros.  
  
##  <a name="BKMK_Build_and_run_the_test"></a> Compilar e executar o teste  
  
#### <a name="to-build-and-run-the-test"></a>Para compilar e executar o teste  
  
1.  No menu **Compilar**, escolha **Compilar Solução**.  
  
     Se não houver erros, a janela UnitTestExplorer aparecerá com **Debit_WithValidAmount_UpdatesBalance** listado no grupo **Não Executar Testes**. Se o Gerenciador de testes não aparecer após um build bem-sucedido, escolha **Testar** no menu, escolha **Windows**e, em seguida, escolha **Gerenciador de Testes**.  
  
2.  Escolha **Executar Todos** para executar o teste. Conforme o teste é executado, a barra de status na parte superior da janela é animada. Ao final da execução de teste, a barra ficará verde se todos os métodos de teste forem aprovados ou vermelha, se algum teste falhar.  
  
3.  Nesse caso, o teste falha. O método de teste é movido para **Testes com Falha**. grupo. Selecione o método no Gerenciador de Testes para exibir os detalhes na parte inferior da janela.  
  
##  <a name="BKMK_Fix_your_code_and_rerun_your_tests"></a> Corrigir o código e executar novamente os testes  
 **Analisar os resultados de teste**  
  
 O resultado do teste contém uma mensagem que descreve a falha. Para o método `AreEquals`, a mensagem exibe o que era esperado (o parâmetro (<strong>esperado\<*XXX*></strong>) e o que foi de fato recebido (o parâmetro **real\<*YYY*>**). Esperávamos que o saldo diminuísse do saldo inicial, mas em vez disso, aumentou o valor da retirada.  
  
 Um reexame do código de débito mostra que o teste da unidade conseguiu encontrar um bug. A quantidade de retirada é adicionada ao saldo da conta, quando deveria ser subtraída.  
  
 **Corrigir o bug**  
  
 Para corrigir o erro, simplesmente substitua a linha  
  
```csharp  
m_balance += amount;  
```  
  
 with  
  
```csharp  
m_balance -= amount;  
```  
  
 **Executar novamente o teste**  
  
 No Gerenciador de testes, escolha **Executar Todos** para executar novamente o teste. A barra verde/vermelho fica verde e o teste é movido para o grupo **Testes Aprovados**.  
  
##  <a name="BKMK_Use_unit_tests_to_improve_your_code"></a> Usar testes de unidade para melhorar o código  
 Esta seção descreve como um processo iterativo de análise, desenvolvimento de testes de unidade e refatoração pode ajudá-lo a tornar seu código de produção mais robusto e eficiente.  
  
 **Analisar os problemas**  
  
 Depois de criar um método de teste para confirmar se um valor válido é corretamente deduzido no método `Debit`, podemos abordar os casos restantes em nossa análise original:  
  
1. O método lançará um `ArgumentOutOfRangeException` se o valor do débito for maior que o saldo.  
  
2. Ele também gerará `ArgumentOutOfRangeException` se o valor do débito for menor que zero.  
  
   **Criar os métodos de teste**  
  
   Uma primeira tentativa de criar um método de teste para solucionar esses problemas parece promissora:  
  
```csharp  
//unit test method  
[TestMethod]  
[ExpectedException(typeof(ArgumentOutOfRangeException))]  
public void Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange()  
{  
    // arrange  
    double beginningBalance = 11.99;  
    double debitAmount = -100.00;  
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);  
  
    // act  
    account.Debit(debitAmount);  
  
    // assert is handled by ExpectedException  
}  
  
```  
  
 Usamos o atributo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.ExpectedExceptionAttribute> para declarar que a direita exceção foi gerada. O atributo faz com que o teste falhe, a menos que uma `ArgumentOutOfRangeException` seja lançada. A execução do teste com valores positivos e negativos `debitAmount` e a modificação temporária do método em teste para lançar um <xref:System.ApplicationException> genérico quando o valor é menor que zero, demonstra que o teste se comporta corretamente. Para testar o caso quando o valor retirado é maior que o saldo, tudo o que precisamos fazer é:  
  
1. Criar um novo método de teste chamado `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange`.  
  
2. Copiar o corpo do método de `Debit_WhenAmountIsLessThanZero_ShouldThrowArgumentOutOfRange` para o novo método.  
  
3. Definir `debitAmount` para um número maior que o saldo.  
  
   **Executar os testes**  
  
   A execução dos dois métodos com valores diferentes de `debitAmount` demonstra que os testes lidam adequadamente com os casos restantes. A execução de todos os três testes confirma que todos os casos em nossa análise original são abordados corretamente.  
  
   **Continuar a análise**  
  
   No entanto, os dois últimos métodos de teste também são um pouco preocupantes. Não podemos ter certeza de qual é a condição lançada no código em teste quando um dos testes é executado. Seria útil uma forma de diferenciar as duas condições. À medida que pensamos mais no problema, torna-se evidente que saber qual condição foi violada aumentaria nossa confiança nos testes. Essas informações muito provavelmente seriam úteis para o mecanismo de produção que lida com a exceção, quando ela é lançada pelo método em teste. A geração de mais informações quando o método é lançado ajudaria a todos os interessados, mas o atributo `ExpectedException` não pode fornecer essas informações.  
  
   Observando novamente o método em teste, podemos ver que as instruções condicionais usam um construtor `ArgumentOutOfRangeException` que assume o nome do argumento como um parâmetro:  
  
```csharp  
throw new ArgumentOutOfRangeException("amount");  
```  
  
 Em uma pesquisa da Biblioteca MSDN, descobrimos que existe um construtor que dá informações muito mais ricas. <xref:System.ArgumentOutOfRangeException.%23ctor%2A>`(String, Object, String)` inclui o nome do argumento, o valor do argumento e uma mensagem definida pelo usuário. Podemos refatorar o método em teste para usar esse construtor. Melhor ainda, podemos usar membros de tipo disponíveis publicamente para especificar os erros.  
  
 **Refatorar o código em teste**  
  
 Primeiro, definimos duas constantes para as mensagens de erro no escopo da classe:  
  
```csharp  
// class under test  
public const string DebitAmountExceedsBalanceMessage = "Debit amount exceeds balance";  
public const string DebitAmountLessThanZeroMessage = "Debit amount less than zero";  
```  
  
 Depois, modificamos as duas instruções condicionais no método `Debit`:  
  
```csharp  
// method under test  
// ...  
    if (amount > m_balance)  
    {  
        throw new ArgumentOutOfRangeException("amount", amount, DebitAmountExceedsBalanceMessage);  
    }  
  
    if (amount < 0)  
    {  
        throw new ArgumentOutOfRangeException("amount", amount, DebitAmountLessThanZeroMessage);  
    }  
// ...  
```  
  
 **Refatorar os métodos de teste**  
  
 Em nosso método de teste, primeiro removemos o atributo `ExpectedException`. Em seu lugar, capturamos a exceção lançada e verificamos se ela foi lançada na instrução condicional correta. No entanto, agora devemos decidir entre duas opções para verificar as condições restantes. Por exemplo, no método `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange`, podemos executar uma das seguintes ações:  
  
- Declarar que a propriedade `ActualValue` da exceção (o segundo parâmetro do construtor `ArgumentOutOfRangeException`) é maior que o saldo inicial. Essa opção requer que testemos a propriedade `ActualValue` da exceção em relação à variável `beginningBalance` do método de teste e também requer que verifiquemos se `ActualValue` é maior que zero.  
  
- Declare que a mensagem (o terceiro parâmetro do construtor) inclui o `DebitAmountExceedsBalanceMessage` definido na classe `BankAccount`.  
  
  O método <xref:Microsoft.VisualStudio.TestTools.UnitTesting.StringAssert.Contains%2A?displayProperty=fullName> na estrutura de teste de unidade da Microsoft nos permite verificar a segunda opção sem os cálculos que são necessários para a primeira opção.  
  
  Uma segunda tentativa de revisão de `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` pode parecer com:  
  
```csharp  
[TestMethod]  
public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()  
{  
    // arrange  
    double beginningBalance = 11.99;  
    double debitAmount = 20.0;  
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);  
  
    // act  
    try  
    {  
        account.Debit(debitAmount);  
    }  
    catch (ArgumentOutOfRangeException e)  
    {  
        // assert  
        StringAssert.Contains(e.Message, BankAccount. DebitAmountExceedsBalanceMessage);  
    }  
}  
```  
  
 **Testar, gravar e analisar novamente**  
  
 Quando testamos novamente os métodos de teste com valores diferentes, encontramos os seguintes fatos:  
  
1. Se capturarmos o erro correto usando uma declaração em que `debitAmount` é maior que o saldo, a declaração `Contains` será aprovada, a exceção será ignorada e, portanto, o método de teste será aprovado. Esse é o comportamento que queremos.  
  
2. Se usarmos um `debitAmount` menor que 0, a declaração falhará porque a mensagem de erro errada é retornada. A declaração também falhará se apresentamos uma exceção temporária `ArgumentOutOfRange` em outro ponto do método no caminho do código em teste. Isso também é bom.  
  
3. Se o valor `debitAmount` for válido (ou seja, menor que o saldo mas maior que zero), nenhuma exceção será detectada, portanto, a declaração nunca é detectada. O método de teste é aprovado. Isso não é bom, pois queremos que o método de teste falhe se nenhuma exceção for lançada.  
  
   O terceiro fato é um bug em nosso método de teste. Para tentar resolver o problema, adicionamos uma declaração <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert.Fail%2A> no final do método de teste para lidar com o caso em que nenhuma exceção é lançada.  
  
   Mas novos testes mostram que agora o teste falhará se a exceção correta for detectada. A instrução catch redefine a exceção e o método continua a ser executado, falhando na nova declaração. Para resolver o novo problema, adicionamos uma instrução `return` após `StringAssert`. Novos testes confirmam que corrigimos os problemas. A versão final de `Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange` é semelhante à seguinte:  
  
```csharp  
[TestMethod]  
public void Debit_WhenAmountIsMoreThanBalance_ShouldThrowArgumentOutOfRange()  
{  
    // arrange  
    double beginningBalance = 11.99;  
    double debitAmount = 20.0;  
    BankAccount account = new BankAccount("Mr. Bryan Walton", beginningBalance);  
  
    // act  
    try  
    {  
        account.Debit(debitAmount);  
    }  
    catch (ArgumentOutOfRangeException e)  
    {  
        // assert  
        StringAssert.Contains(e.Message, BankAccount. DebitAmountExceedsBalanceMessage);  
        return;  
    }  
    Assert.Fail("No exception was thrown.");  
}  
  
```  
  
 Nesta seção final, o trabalho que fizemos melhorando o código de teste levou a métodos de teste mais robustos e informativos. Mais importante ainda, a análise extra também levou a códigos melhores em nosso projeto em teste.



