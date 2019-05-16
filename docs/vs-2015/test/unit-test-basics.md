---
title: Noções básicas de teste de unidade | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
f1_keywords:
- vs.UnitTest.CreateUnitTest
ms.assetid: a80ba9cd-4575-483c-b957-af7ed8dc7e20
caps.latest.revision: 29
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 63f6faf24c1b3ce3aeedd8d4b3c82e2b09a6f443
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65695347"
---
# <a name="unit-test-basics"></a>Noções básicas de teste de unidade
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Verifique se seu código está funcionando conforme o esperado criando e executando testes de unidade. Ele se chama teste de unidade porque a funcionalidade de seu programa é dividida em comportamentos distintos que podem ser testados individualmente como *unidades*. O Gerenciador de Testes do Visual Studio oferece uma maneira flexível e eficiente de executar seus testes de unidade e exibir seus resultados no Visual Studio. O Visual Studio instala as estruturas de teste de unidade da Microsoft para código gerenciado e nativo. Use uma *estrutura de teste de unidade* para criar testes de unidade, executá-los e relatar os resultados desses testes. Execute os testes de unidade novamente quando realizar alterações para testar se o código ainda está funcionando corretamente. Quando você usa o Visual Studio Enterprise, pode executar testes automaticamente após cada compilação.  
  
 O teste de unidade tem o maior efeito sobre a qualidade do código quando ele é parte integrante do fluxo de trabalho de desenvolvimento de software. Assim que você escrever uma função ou outro bloco de código do aplicativo, crie testes de unidade que verifique o comportamento do código em resposta a casos padrão, limite e incorretos de dados de entrada e verifique se não houve nenhuma suposição explícita ou implícita feita pelo código. Com o *desenvolvimento orientado por testes*, você cria os testes de unidade antes de escrever o código e, portanto, os testes de unidade são usados tanto como documentação de design quando especificações funcionais.  
  
 Você pode gerar os projetos de teste e métodos de teste rapidamente do seu código ou criar os testes manualmente conforme a necessidade. Quando você usar o IntelliTest para explorar seu código .NET, poderá gerar dados de teste e um conjunto de testes de unidade. Para cada instrução no código, é gerada uma entrada de teste para executar essa instrução. Descubra como [gerar testes de unidade para seu código](https://msdn.microsoft.com/library/dn823749.aspx).  
  
 O Gerenciador de Testes também pode executar estruturas de teste de unidade de código aberto e de terceiros que implementaram interfaces de complemento do Gerenciador de Testes. Você pode adicionar muitas dessas estruturas por meio do gerenciador de extensões do Visual Studio e da galeria do Visual Studio. Confira [Instalar estruturas de teste de unidade de terceiros](../test/install-third-party-unit-test-frameworks.md)  
  
- [Início rápido](#BKMK_Quick_starts)  
  
- [O exemplo da Solução MyBank](#BKMK_The_MyBank_Solution_example)  
  
- [Criar projetos de teste de unidade e métodos de teste](#BKMK_Creating_the_unit_test_projects)  
  
- [Escrever seus testes](#BKMK_Writing_your_tests)  
  
- [Executar testes de unidade no Gerenciador de Testes](#BKMK_Running_tests_in_Test_Explorer)  
  
- [Executar e exibir testes](#BKMK_Running_and_viewing_tests_from_the_Test_Explorer_toolbar)  
  
## <a name="BKMK_Unit_testing_overview"></a> Visão geral de teste de unidade  
  
### <a name="BKMK_Quick_starts"></a> Início rápido  
 Para obter uma introdução ao teste de unidade que leva você diretamente para a parte de codificação, confira um destes tópicos:  
  
- [Passo a passo: criação e execução de testes de unidade para código gerenciado](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)  
  
- [Início rápido: desenvolvimento orientado por testes com o Gerenciador de Testes](../test/quick-start-test-driven-development-with-test-explorer.md)  
  
- [Código nativo de testes de unidade com o Gerenciador de Testes](https://msdn.microsoft.com/8a09d6d8-3613-49d8-9ffe-11375ac4736c)  
  
## <a name="BKMK_The_MyBank_Solution_example"></a> O exemplo da Solução MyBank  
 Neste tópico, usamos o desenvolvimento de um aplicativo fictício chamado `MyBank` como exemplo. Você não precisa do código real para seguir as explicações neste tópico. Os métodos de teste são escritos em C# e apresentados usando o Microsoft Unit Testing Framework para Código Gerenciado. No entanto, os conceitos podem ser facilmente transferidos para outros idiomas e estruturas.  
  
 ![Solução MyBank](../test/media/ute-mybanksolution.png "UTE_MyBankSolution")  
  
 Nossa primeira tentativa de um projeto para o aplicativo `MyBank` inclui um componente de contas, que representa uma conta individual e suas transações com o banco, e um componente de banco de dados, que representa a funcionalidade de agregação e gerenciamento das contas individuais.  
  
 Criamos uma solução `MyBank` que contém dois projetos:  
  
- `Accounts`  
  
- `BankDb`  
  
  Nossa primeira tentativa de criação do projeto `Accounts` contém uma classe para manter informações básicas sobre uma conta, uma interface que especifica a funcionalidade comum dos tipos de conta, como depositar e sacar ativos da conta, e uma classe derivada da interface que representa uma conta corrente. Começamos os projetos Contas criando os seguintes arquivos de origem:  
  
- `AccountInfo.cs` define as informações básicas de uma conta.  
  
- `IAccount.cs` define uma interface padrão `IAccount` de uma conta, incluindo métodos de depósito e saque de ativos de uma conta e de recuperação do saldo da conta.  
  
- `CheckingAccount.cs` contém a classe `CheckingAccount` que implementa a interface `IAccounts` de uma conta corrente.  
  
  Sabemos por experiência própria que uma das coisas que um saque de conta corrente deve fazer é garantir que o valor sacado seja, no máximo, o que existe como saldo na conta. Podemos substituir o método `IAccount.Withdaw` na `CheckingAccount` por um método que verifica essa condição. O método pode ser mais ou menos assim:  
  
```csharp  
  
public void Withdraw(double amount)  
{  
    if(m_balance >= amount)  
    {  
        m_balance -= amount;  
    }  
    else  
    {  
        throw new ArgumentException(amount, "Withdrawal exceeds balance!")  
    }  
}  
  
```  
  
 Agora que temos alguns códigos, é hora de testar.  
  
## <a name="BKMK_Creating_the_unit_test_projects"></a> Criar projetos de teste de unidade e métodos de teste  
 Geralmente é mais rápido gerar o projeto de teste de unidade e os stubs de teste de unidade no seu código. Ou você pode optar por criar o projeto de teste de unidade e os testes manualmente, dependendo dos seus requisitos.  
  
 **Gerar o projeto de teste de unidade e os stubs de teste de unidade**  
  
1. Na janela do editor de código, clique com botão direito do mouse e escolha **Criar Testes de Unidade** no menu de contexto.  
  
    ![Na janela do editor, exiba o menu de contexto](../test/media/createunittestsrightclick.png "CreateUnitTestsRightClick")  
  
2. Clique em OK para aceitar os padrões e criar testes de unidade ou altere os valores usados para criar e nomear o teste de unidade de projeto e os testes de unidade. Você pode selecionar o código que é adicionado por padrão aos métodos de teste de unidade.  
  
    ![Clique com o botão direito do mouse no editor e escolha Criar Testes de Unidade](../test/media/createunittestsdialog.png "CreateUnitTestsDialog")  
  
3. Os stubs de teste de unidade são criados em um novo projeto de teste de unidade para todos os métodos na classe.  
  
    ![Os testes de unidade são criados](../test/media/createunittestsstubs.png "CreateUnitTestsStubs")  
  
4. Agora, avance para saber como [adicionar código aos métodos de teste de unidade](#BKMK_Writing_your_tests) a fim de fazer o teste de unidade ser relevante ou outros testes de unidade extra que você queira adicionar para testar seu código.  
  
   **Criar projeto de teste de unidade e testes de unidade manualmente**  
  
   Um projeto de teste de unidade geralmente espelha a estrutura de um projeto de código único. No exemplo MyBank, você adicionará dois projetos de teste de unidade chamados `AccountsTests` e `BankDbTests` à solução `MyBanks`. Os nomes de projeto de teste são arbitrários, mas convém adotar uma convenção de nomenclatura padrão.  
  
   **Para adicionar um projeto de teste de unidade a uma solução:**  
  
5. No menu **Arquivo**, escolha **Novo** e, em seguida, escolha **Projeto** (Teclado: Ctrl + Shift + N).  
  
6. Na caixa de diálogo Novo Projeto, expanda o nó **Instalado**, escolha o idioma que você deseja usar para o projeto de teste e escolha **Testar**.  
  
7. Para usar uma das estruturas de teste de unidade da Microsoft, escolha **Projeto de Teste de Unidade** na lista de modelos de projeto. Caso contrário, escolha o modelo de projeto da estrutura de teste de unidade que você deseja usar. Para testar o projeto `Accounts` do nosso exemplo, você deve nomear o projeto `AccountsTests`.  
  
   > [!WARNING]
   > Nem todas as estruturas de teste de unidade de código aberto e de terceiros fornecem um modelo de projeto do Visual Studio. Consulte o documento da estrutura para saber como criar um projeto.  
  
8. Em seu projeto de teste de unidade, adicione uma referência ao projeto de código em teste, neste caso, ao projeto Contas.  
  
    Para criar a referência ao projeto de código:  
  
   1. Selecione o projeto no Gerenciador de Soluções.  
  
   2. No menu **Projeto**, escolha **Adicionar Referência**.  
  
   3. Na caixa de diálogo Gerenciador de Referência, abra o nó **Solução** e escolha **Projetos**. Selecione o nome do projeto de código e feche a caixa de diálogo.  
  
   Cada projeto de teste de unidade contém classes que refletem os nomes das classes no projeto do código. Em nosso exemplo, o projeto `AccountsTests` contém as seguintes classes:  
  
- A classe `AccountInfoTests` contém os métodos de teste de unidade para a classe `AccountInfo` no projeto `BankAccount`  
  
- A classe `CheckingAccountTests` contém os métodos de teste de unidade para a classe `CheckingAccount`.  
  
## <a name="BKMK_Writing_your_tests"></a> Escrever seus testes  
 A estrutura de teste de unidade que você usa e o Visual Studio IntelliSense vão guiá-lo durante a criação do código para os testes de unidade de um projeto de código. Para poder executar no Gerenciador de Testes, a maioria das estruturas exige que você adicione atributos específicos para identificar os métodos de teste de unidade. As estruturas também fornecem uma maneira, geralmente por meio de instruções assert ou atributos de método, para indicar se o método de teste foi aprovado ou reprovado. Outros atributos identificam métodos de instalação opcionais que estão na inicialização da classe e antes de cada método de teste e dos métodos de subdivisão que serão executados após cada método de teste e antes que a classe seja destruída.  
  
 O padrão AAA (Arrange, Act, Assert) é uma maneira comum de escrever testes de unidade para um método em teste.  
  
- A seção **Organizar** (Arrange) de um método de teste de unidade inicializa os objetos e define o valor dos dados que são passados para o método sendo testado.  
  
- A seção **Agir** (Act) invoca o método sendo testado com os parâmetros organizados.  
  
- A seção **Declarar** (Assert) verifica se a ação do método em teste se comporta conforme o esperado.  
  
  Para testar o método `CheckingAccount.Withdraw` de nosso exemplo, podemos escrever dois testes: um que verifica o comportamento padrão do método e outro que verifica se um saque acima do saldo falhará. Na classe `CheckingAccountTests`, podemos adicionar os seguintes métodos:  
  
```csharp  
[TestMethod]  
public void Withdraw_ValidAmount_ChangesBalance()  
{  
    // arrange  
    double currentBalance = 10.0;  
    double withdrawal = 1.0;  
    double expected = 9.0;  
    var account = new CheckingAccount("JohnDoe", currentBalance);  
    // act  
    account.Withdraw(withdrawal);  
    double actual = account.Balance;  
    // assert  
    Assert.AreEqual(expected, actual);  
}  
  
[TestMethod]  
[ExpectedException(typeof(ArgumentException))]  
public void Withdraw_AmountMoreThanBalance_Throws()  
{  
    // arrange  
    var account = new CheckingAccount("John Doe", 10.0);  
    // act  
    account.Withdraw(20.0);  
    // assert is handled by the ExpectedException  
}  
  
```  
  
 Observe que `Withdraw_ValidAmount_ChangesBalance` usa uma instrução `Assert` explícita para determinar se o método de teste é aprovado ou reprovado, ao passo que `Withdraw_AmountMoreThanBalance_Throws` usa o atributo `ExpectedException` para determinar o êxito do método de teste. Nos bastidores, uma estrutura de teste de unidade encapsula os métodos de teste em instruções try/catch. Na maioria dos casos, se uma exceção é detectada, o método de teste falha e a exceção é ignorada. O atributo `ExpectedException` faz com que o método de teste seja aprovado se a exceção for gerada.  
  
 Para saber mais sobre o Microsoft Unit Testing Frameworks, confira um dos seguintes tópicos:  
  
- [Escrevendo testes de unidade para .NET Framework com a estrutura de teste de unidade Microsoft para código gerenciado](../test/writing-unit-tests-for-the-dotnet-framework-with-the-microsoft-unit-test-framework-for-managed-code.md)  
  
- [Escrevendo testes de unidade para C/C++ com o Microsoft Unit Testing Framework para C++](../test/writing-unit-tests-for-c-cpp-with-the-microsoft-unit-testing-framework-for-cpp.md)  
  
## <a name="set-timeouts-for-unit-tests"></a>Definir tempos limite para testes de unidade  
 Para definir um tempo limite em um método de teste individual:  
  
```csharp  
[TestMethod]  
[Timeout(2000)]  // Milliseconds  
public void My_Test()  
{ ...  
}  
```  
  
```vb  
  
```  
  
 Para definir o tempo limite como o máximo permitido:  
  
```csharp  
[TestMethod]  
[Timeout(TestTimeout.Infinite)]  // Milliseconds  
public void My_Test ()  
{ ...  
}  
```  
  
## <a name="BKMK_Running_tests_in_Test_Explorer"></a> Executar testes de unidade no Gerenciador de Testes  
 Quando você compila o projeto de teste, os testes são exibidos no Gerenciador de Testes. Se o Gerenciador de Testes não estiver visível, escolha **Teste** no menu do Visual Studio, escolha **Windows** e, em seguida, escolha **Gerenciador de Testes**.  
  
 ![Gerenciador de testes de unidade](../ide/media/ute-failedpassednotrunsummary.png "UTE_FailedPassedNotRunSummary")  
  
 Conforme você executa, grava e executa novamente os testes, o modo de exibição padrão do Gerenciador de Testes exibe os resultados em grupos **Testes Reprovados**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. Você pode escolher um cabeçalho de grupo para abrir o modo de exibição que exibe todos os testes no grupo.  
  
 Você também pode filtrar os testes em qualquer modo de exibição correspondendo o texto na caixa de pesquisa em nível global ou selecionando um dos filtros predefinidos. Você pode executar uma seleção de testes a qualquer momento. Os resultados de uma execução de teste aparecem imediatamente na barra de aprovação/reprovação na parte superior da janela do Gerenciador. Os detalhes do resultado de um método de teste são exibidos quando você seleciona o teste.  
  
### <a name="BKMK_Running_and_viewing_tests_from_the_Test_Explorer_toolbar"></a>Executar e exibir testes  
 A barra de ferramentas do Gerenciador de Testes ajuda você a descobrir, organizar e executar os testes desejados.  
  
 ![Executar testes na barra de ferramentas do Gerenciador de Testes](../test/media/ute-toolbar.png "UTE_ToolBar")  
  
 Você pode escolher **Executar Tudo** para executar todos os testes ou **Executar** para escolher um subconjunto de testes a serem executados. Depois de executar um conjunto de testes, um resumo da execução do teste é exibido na parte inferior da janela do Gerenciador de Testes. Selecione um teste para exibir seus detalhes no painel inferior. Escolha **Abrir Teste** no menu de contexto (teclado: F12) para exibir o código-fonte do teste selecionado.  
  
 Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o botão de alternância ![UTE&#95;parallelicon&#45;small](../test/media/ute-parallelicon-small.png "UTE_parallelicon-small") na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.  
  
### <a name="BKMK_Running_tests_after_every_build"></a> Executar testes depois de cada compilação  
  
> [!WARNING]
> A execução de testes de unidade após cada compilação só tem suporte no Visual Studio Enterprise.  
  
|||  
|-|-|  
|![Executar após a compilação](../test/media/ute-runafterbuild-btn.png "UTE_RunAfterBuild_btn")|Para executar os testes de unidade após cada compilação local, escolha **Teste** no menu padrão e escolha **Executar testes após compilação** na barra de ferramentas do Gerenciador de Testes.|  
  
### <a name="BKMK_Filtering_and_grouping_the_test_list"></a> Filtrar e agrupar a lista de teste  
 Quando você tiver um grande número de testes, pode digitar na caixa de pesquisa do Gerenciador de Testes para filtrar a lista por cadeia de caracteres especificada. Você pode restringir seu evento de filtro ainda mais escolhendo na lista de filtros.  
  
 ![Categorias de filtro de pesquisa](../test/media/ute-searchfilter.png "UTE_SearchFilter")  
  
|||  
|-|-|  
|![Botão de grupo do Gerenciador de Testes](../test/media/ute-groupby-btn.png "UTE_GroupBy_btn")|Para agrupar testes por categoria, escolha o botão **Agrupar por**.|  
  
 Para obter mais informações, consulte [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md)  
  
## <a name="qa"></a>PERGUNTAS E RESPOSTAS  
 **P: Como fazer para depurar testes de unidade?**  
  
 **R:** Use o Gerenciador de testes para iniciar uma sessão de depuração para seus testes. Passar pelo código com o depurador do Visual Studio permite-lhe navegar facilmente entre os testes de unidade e o projeto sendo testado. Para iniciar a depuração:  
  
1. No editor do Visual Studio, defina um ponto de interrupção em um ou mais métodos de teste que deseje depurar.  
  
   > [!NOTE]
   > Como os métodos de teste podem ser executados em qualquer ordem, defina pontos de interrupção em todos os métodos de teste que deseje depurar.  
  
2. No Gerenciador de Testes, selecione os métodos de teste e escolha **Depurar Testes Selecionados** no menu de atalho.  
  
   Obter mais detalhes sobre [como depurar testes de unidade](../debugger/debugging-in-visual-studio.md).  
  
   **P: Se eu estou usando TDD, como faço para gerar código de meus testes?**  
  
   **R:** Use o IntelliSense para gerar classes e métodos no código do projeto. Escreva uma instrução em um método de teste que chama a classe ou o método que você deseja gerar e abra o menu do IntelliSense na chamada. Se a chamada é um construtor da nova classe, escolha **Gerar novo tipo** no menu e siga o assistente para inserir a classe em seu projeto de código. Se a chamada é para um método, escolha **Gerar novo método** no menu IntelliSense.  
  
   ![Gerar menu Intellisense do Stub de Método](../test/media/ute-generatemethodstubintellisense.png "UTE_GenerateMethodStubIntellisense")  
  
   **P: Posso criar testes de unidade que usam vários conjuntos de dados como entrada para executar o teste?**  
  
   **R:** Sim. Os *métodos de teste voltados para dados* permitem que você teste um intervalo de valores com um método de teste de unidade. Use um atributo `DataSource` para o método de teste que especifica a fonte de dados e a tabela que contém os valores de variáveis que você deseja testar.  No corpo do método, atribua os valores de linha às variáveis usando o indexador `TestContext.DataRow[`*ColumnName*`]`.  
  
> [!NOTE]
> Esses procedimentos se aplicam somente ao teste de métodos que você escreve usando o Microsoft Unit Test Framework para código gerenciado. Se você estiver usando uma estrutura diferente, consulte a documentação dela para ver a funcionalidade equivalente.  
  
 Por exemplo, suponha que adicionamos um método desnecessário para a classe `CheckingAccount` chamada `AddIntegerHelper`. `AddIntegerHelper` adiciona dois números inteiros.  
  
 Para criar um teste voltado para dados para o método `AddIntegerHelper`, primeiro criamos um banco de dados do Access denominado `AccountsTest.accdb` e uma tabela chamada `AddIntegerHelperData`. A tabela `AddIntegerHelperData` define colunas para especificar o primeiro e o segundo operandos da adição e uma coluna para especificar o resultado esperado. Vamos preencher um número de linhas com valores apropriados.  
  
```csharp  
  
[DataSource(  
    @"Provider=Microsoft.ACE.OLEDB.12.0;Data Source=C:\Projects\MyBank\TestData\AccountsTest.accdb",   
    "AddIntegerHelperData"  
)]  
[TestMethod()]  
public void AddIntegerHelper_DataDrivenValues_AllShouldPass()  
{  
    var target = new CheckingAccount();  
    int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);  
    int y = Convert.ToInt32(TestContext.DataRow["SecondNumber"]);   
    int expected = Convert.ToInt32(TestContext.DataRow["Sum"]);  
    int actual = target.AddIntegerHelper(x, y);  
    Assert.AreEqual(expected, actual);  
}  
  
```  
  
 O método atribuído é executado uma vez para cada linha na tabela. O Gerenciador de Testes relata uma falha de teste para o método se uma das iterações falhar. O painel de detalhes de resultados de teste para o método mostra o método de status de aprovação/reprovação para cada linha de dados.  
  
 Saiba mais sobre [testes de unidade voltados para dados](../test/how-to-create-a-data-driven-unit-test.md).  
  
 **P: Posso exibir a quantidade de código que foi testada pelos meus testes de unidade?**  
  
 **R:** Sim. Você pode determinar a quantidade de código que realmente está sendo testada por seus testes de unidade usando a ferramenta de cobertura de código do Visual Studio. Há suporte para idiomas nativos e gerenciados e todas as estruturas de teste de unidade que podem ser executadas pela estrutura de teste de unidade.  
  
 Você pode executar a cobertura de código em testes selecionados ou em todos os testes em uma solução. A janela Resultados de Cobertura do Código exibe a porcentagem dos blocos que foram exercidos por linha, função, classe, namespace e módulo de código do produto.  
  
 Para executar a cobertura de código para métodos de teste em uma solução, escolha **Testes** no menu do Visual Studio e escolha **Analisar cobertura de código**.  
  
 Os resultados da cobertura aparecem na janela Resultados de Cobertura de Código.  
  
 ![Resultados de Cobertura de Código](../test/media/ute-codecoverageresults.png "UTE_CodeCoverageResults")  
  
 Saiba mais sobre [cobertura de código](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).  
  
 **P: Como posso testar métodos no meu código que possuem dependências externas?**  
  
 **R:** Sim. Se você tiver o Visual Studio Enterprise, o Microsoft Fakes pode ser usado com método de teste que você escrever usando estruturas de teste de unidade para código gerenciado.  
  
 O Microsoft Fakes usa duas abordagens a fim de criar classes substitutas para dependências externas.  
  
1. *Stubs* geram classes substitutas derivadas da interface pai da classe de dependência de destino. Os métodos stub podem ser substituídos por métodos virtuais públicos da classe de destino.  
  
2. *Shims* usam a instrumentação de tempo de execução para desviar as chamadas a um método de destino para um método shim substituto no caso de métodos não virtuais.  
  
   Em ambas as abordagens, você pode usar os representantes de chamadas gerados para o método de dependência a fim de especificar o comportamento desejado no método de teste.  
  
   Saiba mais sobre [como isolar métodos de teste de unidade com o Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md).  
  
   **P: Posso usar outras estruturas de teste de unidade para criar testes de unidade?**  
  
   **R:** Sim, siga estas etapas para [encontrar e instalar outras estruturas](../test/install-third-party-unit-test-frameworks.md). Depois de reiniciar o Visual Studio, reabra a solução para criar testes de unidade e selecione suas estruturas instaladas aqui:  
  
   ![Selecione outra estrutura de teste de unidade instalada](../test/media/createunittestsdialogextensions.png "CreateUnitTestsDialogExtensions")  
  
   Seu stubs de teste de unidade serão criados usando a estrutura selecionada.
