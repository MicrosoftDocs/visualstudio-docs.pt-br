---
title: Conceitos básicos sobre o teste de unidade
description: Saiba como o Visual Studio Test Explorer fornece uma maneira flexível e eficiente para executar os testes de unidade e exibir seus resultados.
ms.custom: SEO-VS-2020
ms.date: 08/07/2019
ms.topic: conceptual
f1_keywords:
- vs.UnitTest.CreateUnitTest
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 755affbf52aa31539b35af4520f5a8d17254f776
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99962724"
---
# <a name="unit-test-basics"></a>Noções básicas de teste de unidade

Verifique se seu código está funcionando conforme o esperado criando e executando testes de unidade. Ele é chamado de teste de unidade porque você divide a funcionalidade do seu programa em comportamentos discretos que podem ser testados como *unidades* individuais. O Gerenciador de Testes do Visual Studio oferece uma maneira flexível e eficiente de executar seus testes de unidade e exibir seus resultados no Visual Studio. O Visual Studio instala as estruturas de teste de unidade da Microsoft para código gerenciado e nativo. Use uma *estrutura de teste de unidade* para criar testes de unidade, executá-los e relatar os resultados desses testes. Execute os testes de unidade novamente quando realizar alterações para testar se o código ainda está funcionando corretamente. O Visual Studio Enterprise pode fazer isso automaticamente com o [Live Unit Testing](live-unit-testing-intro.md), que detecta testes afetados pelas suas alterações de código e os executa em segundo plano enquanto você digita.

O teste de unidade tem o maior efeito sobre a qualidade do código quando é parte integrante do fluxo de trabalho de desenvolvimento de software. Assim que você escrever uma função ou outro bloco de código do aplicativo, crie testes de unidade que verifique o comportamento do código em resposta a casos padrão, limite e incorretos de dados de entrada e verifique se não houve nenhuma suposição explícita ou implícita feita pelo código. Com o *desenvolvimento orientado por testes*, você cria os testes de unidade antes de escrever o código e, portanto, os testes de unidade são usados tanto como documentação de design quando especificações funcionais.

O Gerenciador de Testes também pode executar estruturas de teste de unidade de código aberto e de terceiros que implementaram interfaces de complemento do Gerenciador de Testes. Você pode adicionar muitas dessas estruturas por meio do gerenciador de extensões do Visual Studio e da galeria do Visual Studio. Para obter mais informações, consulte [instalar estruturas de teste de unidade de](../test/install-third-party-unit-test-frameworks.md)terceiros.

Você pode gerar os projetos de teste e métodos de teste rapidamente do seu código ou criar os testes manualmente conforme a necessidade. Ao usar o IntelliTest para explorar o código .NET, você pode gerar dados de teste e um conjunto de testes de unidade. Para cada instrução no código, é gerada uma entrada de teste para executar essa instrução. Descubra como [gerar testes de unidade para o código .net](generate-unit-tests-for-your-code-with-intellitest.md).

## <a name="get-started"></a>Introdução

Para obter uma introdução ao teste de unidade que leva você diretamente para a parte de codificação, confira um destes tópicos:

- [Walkthrough: criar e executar testes de unidade para código .NET](../test/walkthrough-creating-and-running-unit-tests-for-managed-code.md)

- [Walkthrough: desenvolvimento controlado por testes com o Gerenciador de testes](../test/quick-start-test-driven-development-with-test-explorer.md)

- [Gravar testes de unidade para C/C++ no Visual Studio](../test/writing-unit-tests-for-c-cpp.md)

## <a name="the-mybank-solution-example"></a>O exemplo da solução MyBank

Neste artigo, usamos o desenvolvimento de um aplicativo fictício chamado `MyBank` como exemplo. Você não precisa do código real para seguir as explicações neste tópico. Os métodos de teste são gravados em C# e apresentados usando o Microsoft Unit Testing Framework para Código Gerenciado. No entanto, os conceitos podem ser facilmente transferidos para outros idiomas e estruturas.

::: moniker range="vs-2017"
![Solução MyBank](../test/media/ute_mybanksolution.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Solução MyBank 2019](../test/media/vs-2019/basics-mybank-solution.png)
::: moniker-end

Nossa primeira tentativa de um projeto para o aplicativo `MyBank` inclui um componente de contas, que representa uma conta individual e suas transações com o banco, e um componente de banco de dados, que representa a funcionalidade de agregação e gerenciamento das contas individuais.

Criamos uma solução `MyBank` que contém dois projetos:

- `Accounts`

- `BankDb`

Nossa primeira tentativa de criação do projeto `Accounts` contém uma classe para manter informações básicas sobre uma conta, uma interface que especifica a funcionalidade comum dos tipos de conta, como depositar e sacar ativos da conta, e uma classe derivada da interface que representa uma conta corrente. Começamos os projetos Contas criando os seguintes arquivos de origem:

- *AccountInfo.cs* define as informações básicas de uma conta.

- *IAccount.cs* define uma interface `IAccount` padrão de uma conta, incluindo métodos de depósito e saque de ativos de uma conta e de recuperação do saldo da conta.

- *CheckingAccount.cs* contém a classe `CheckingAccount` que implementa a interface `IAccount` de uma conta corrente.

Sabemos por experiência própria que uma das coisas que um saque de conta corrente deve fazer é garantir que o valor sacado seja, no máximo, o que existe como saldo na conta. Podemos substituir o método `IAccount.Withdraw` na `CheckingAccount` por um método que verifica essa condição. O método pode ser mais ou menos assim:

```csharp
public void Withdraw(double amount)
{
    if(m_balance >= amount)
    {
        m_balance -= amount;
    }
    else
    {
        throw new ArgumentException(nameof(amount), "Withdrawal exceeds balance!");
    }
}
```

Agora que temos alguns códigos, é hora de testar.

## <a name="create-unit-test-projects-and-test-methods"></a>Criar projetos de teste de unidade e métodos de teste

Para o C#, geralmente é mais rápido gerar o projeto de teste de unidade e os stubs de teste de unidade do seu código. Ou você pode optar por criar o projeto de teste de unidade e os testes manualmente, dependendo dos seus requisitos. Se você quiser criar testes de unidade a partir do código com uma estrutura de terceiros, precisará de uma dessas extensões instaladas: [NUnit](https://marketplace.visualstudio.com/items?itemName=NUnitDevelopers.TestGeneratorNUnitextension-18371) ou [xUnit](https://marketplace.visualstudio.com/items?itemName=YowkoTsai.xUnitnetTestGenerator). Se você não estiver usando o C#, pule esta seção e vá para [criar o projeto de teste de unidade e os testes de unidade manualmente](#create-the-unit-test-project-and-unit-tests-manually).

### <a name="generate-unit-test-project-and-unit-test-stubs"></a>Gerar o projeto de teste de unidade e os stubs de teste de unidade

1. Na janela do editor de código, clique com o botão direito do mouse e escolha [**Criar Testes de Unidade**](create-unit-tests-menu.md) no menu do clique com o botão direito.

   ::: moniker range="vs-2017"
   ![Na janela do editor, exiba o menu de contexto](../test/media/createunittestsrightclick.png)

   > [!NOTE]
   > O comando de menu **Criar Testes de Unidade** está disponível somente para código gerenciado direcionado ao .NET Framework (mas não ao .NET Core).
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![Na janela do editor, exiba o menu de contexto](../test/media/vs-2019/basics-create-unit-tests.png)

   > [!NOTE]
   > O comando de menu **criar testes de unidade** só está disponível para código C#.
   ::: moniker-end

2. Clique em **OK** para aceitar os padrões e criar os testes de unidade ou altere os valores usados para criar e nomear o projeto de teste de unidade e os testes de unidade. Você pode selecionar o código que é adicionado por padrão aos métodos de teste de unidade.

   ![Caixa de diálogo Criar Testes de Unidade no Visual Studio](../test/media/create-unit-tests.png)

3. Os stubs de teste de unidade são criados em um novo projeto de teste de unidade para todos os métodos na classe.

   ::: moniker range="vs-2017"
   ![Os testes de unidade são criados](../test/media/createunittestsstubs.png)
   ::: moniker-end
   ::: moniker range=">=vs-2019"
   ![Os testes de unidade são criados](../test/media/vs-2019/basics-test-stub.png)
   ::: moniker-end

4. Agora, avance para saber como [adicionar código aos métodos de teste de unidade](#write-your-tests) a fim de fazer o teste de unidade ser relevante ou outros testes de unidade extra que você queira adicionar para testar seu código.

### <a name="create-the-unit-test-project-and-unit-tests-manually"></a>Criar projeto de teste de unidade e testes de unidade manualmente

Um projeto de teste de unidade geralmente espelha a estrutura de um projeto de código único. No exemplo MyBank, você adicionará dois projetos de teste de unidade chamados `AccountsTests` e `BankDbTests` à solução `MyBanks`. Os nomes de projeto de teste são arbitrários, mas convém adotar uma convenção de nomenclatura padrão.

**Para adicionar um projeto de teste de unidade a uma solução:**

1. No **Gerenciador de Soluções**, clique com o botão direito do mouse na solução e escolha **Adicionar** > **Novo** **Projeto**.

::: moniker range="vs-2017"

2. Na caixa de diálogo **Novo Projeto**, expanda o nó **Instalado**, escolha a linguagem que deseja usar para o projeto de teste e clique em **Testar**.

3. Para usar uma das estruturas de teste de unidade da Microsoft, escolha **Projeto de Teste de Unidade** na lista de modelos de projeto. Caso contrário, escolha o modelo de projeto da estrutura de teste de unidade que você deseja usar. Para testar o projeto `Accounts` do nosso exemplo, você deve nomear o projeto `AccountsTests`.

   > [!NOTE]
   > Nem todas as estruturas de teste de unidade de código aberto e de terceiros fornecem um modelo de projeto do Visual Studio. Consulte o documento da estrutura para saber como criar um projeto.

::: moniker-end

::: moniker range=">=vs-2019"

2. Use a caixa de pesquisa de modelo de projeto para localizar um modelo de projeto de teste de unidade para a estrutura de teste que você deseja usar.

3. Na próxima página, dê um nome ao projeto. Para testar o projeto `Accounts` do nosso exemplo, você poderia nomear o projeto `AccountsTests`.

::: moniker-end

4. Em seu projeto de teste de unidade, adicione uma referência ao projeto de código em teste, neste caso, ao projeto Contas.

   Para criar a referência ao projeto de código:

   1. Selecione o projeto no **Gerenciador de Soluções**.

   2. No menu **Projeto**, escolha **Adicionar Referência**.

   3. Na caixa de diálogo **Gerenciador de Referências**, abra o nó **Solução** e escolha **Projetos**. Selecione o nome do projeto de código e feche a caixa de diálogo.

Cada projeto de teste de unidade contém classes que refletem os nomes das classes no projeto do código. Em nosso exemplo, o projeto `AccountsTests` contém as seguintes classes:

- A classe `AccountInfoTests` contém os métodos de teste de unidade para a classe `AccountInfo` no projeto `Accounts`

- A classe `CheckingAccountTests` contém os métodos de teste de unidade para a classe `CheckingAccount`.

## <a name="write-your-tests"></a>Escrever seus testes

A estrutura de teste de unidade que você usa e o Visual Studio IntelliSense vão guiá-lo durante a criação do código para os testes de unidade de um projeto de código. Para ser executada no **Gerenciador de Testes**, a maioria das estruturas exige a adição de atributos específicos para identificar métodos de teste de unidade. As estruturas também fornecem uma maneira, geralmente por meio de instruções assert ou atributos de método, para indicar se o método de teste foi aprovado ou reprovado. Outros atributos identificam métodos de instalação opcionais que estão na inicialização da classe e antes de cada método de teste e dos métodos de subdivisão que serão executados após cada método de teste e antes que a classe seja destruída.

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

    // assert
    Assert.AreEqual(expected, account.Balance);
}

[TestMethod]
public void Withdraw_AmountMoreThanBalance_Throws()
{
    // arrange
    var account = new CheckingAccount("John Doe", 10.0);

    // act and assert
    Assert.ThrowsException<System.ArgumentException>(() => account.Withdraw(20.0));
}
```

Para saber mais sobre as estruturas de testes de unidade da Microsoft, confira um dos seguintes tópicos:

- [Teste de unidade em seu código](unit-test-your-code.md)

- [Escrevendo testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md)

- [Usar a estrutura do MSTest em testes de unidade](using-microsoft-visualstudio-testtools-unittesting-members-in-unit-tests.md)

## <a name="set-timeouts-for-unit-tests"></a>Definir tempos limite para testes de unidade

Se estiver usando a estrutura do MSTest, use o <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TimeoutAttribute> para definir um tempo limite em um método de teste individual:

```csharp
[TestMethod]
[Timeout(2000)]  // Milliseconds
public void My_Test()
{ ...
}
```

Para definir o tempo limite como o máximo permitido:

```csharp
[TestMethod]
[Timeout(TestTimeout.Infinite)]  // Milliseconds
public void My_Test ()
{ ...
}
```

## <a name="run-tests-in-test-explorer"></a>Executar testes de unidade no Gerenciador de Testes

Quando você cria o projeto de teste, os testes são exibidos no **Gerenciador de Testes**. Se **o Gerenciador de testes** não estiver visível, escolha **testar** no menu do Visual Studio, escolha **Windows** e escolha **Gerenciador de testes** (ou pressione **Ctrl**  +  **E**, **T**).

::: moniker range="vs-2017"
![Gerenciador de Testes de Unidade](../test/media/ute_failedpassednotrunsummary.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Gerenciador de Testes de Unidade](../test/media/vs-2019/basics-test-explorer.png)
::: moniker-end

Conforme você executa, grava e executa novamente os testes, o **Gerenciador de Testes** pode exibir os resultados nos grupos **Testes com Falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. Você pode escolher diferentes opções de agrupamento na barra de ferramentas.

Você também pode filtrar os testes em qualquer modo de exibição correspondendo o texto na caixa de pesquisa em nível global ou selecionando um dos filtros predefinidos. Você pode executar uma seleção de testes a qualquer momento. Os resultados de uma execução de teste aparecem imediatamente na barra de aprovação/reprovação na parte superior da janela do Gerenciador. Os detalhes do resultado de um método de teste são exibidos quando você seleciona o teste.

### <a name="run-and-view-tests"></a>Executar e exibir testes

A barra de ferramentas do **Gerenciador de Testes** ajuda você a descobrir, organizar e executar os testes desejados.

::: moniker range="vs-2017"
![Executar testes na barra de ferramentas do Gerenciador de Testes](../test/media/ute_toolbar.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Executar testes na barra de ferramentas do Gerenciador de Testes](../test/media/vs-2019/test-explorer-toolbar-diagram-16-2.png)
::: moniker-end

Você pode escolher **executar tudo** para executar todos os seus testes (ou pressione **Ctrl**  +  **r**, **V**) ou escolher **executar** para escolher um subconjunto de testes a serem executados (**Ctrl**  +  **r**, **T**). Selecione um teste para exibir os detalhes no painel de detalhes do teste. Escolha **abrir teste** no menu do botão direito do mouse (teclado: **F12**) para exibir o código-fonte do teste selecionado.

::: moniker range="vs-2017"

Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o ![Captura de tela do botão de alternância de execução de teste paralelo na barra de ferramentas do Gerenciador de testes do Visual Studio.](../test/media/ute_parallelicon-small.png) botão de alternância na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.

::: moniker-end

::: moniker range=">=vs-2019"

Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo no menu de configurações da barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.

::: moniker-end

### <a name="run-tests-after-every-build"></a>Executar testes depois de cada compilação

::: moniker range="vs-2017"

|Botão|Descrição|
|-|-|
|![Executar após o build](../test/media/ute_runafterbuild_btn.png)|Para executar os testes de unidade após cada build local, escolha **Teste** no menu padrão e, em seguida, **Executar Testes após Build** na barra de ferramentas do **Gerenciador de Testes**.|

> [!NOTE]
> Executar testes de unidade após cada build requer o Visual Studio 2017 edição Enterprise ou o Visual Studio 2019. No Visual Studio 2019, o recurso está disponível nas edições Community e Professional, além da edição Enterprise.

::: moniker-end

::: moniker range=">=vs-2019"

Para executar os testes de unidade após cada build local, abra o ícone de configurações na barra de ferramentas do Gerenciador de Testes e selecione **Executar Testes após Build**.

::: moniker-end

### <a name="filter-and-group-the-test-list"></a>Filtrar e agrupar a lista de teste

Quando houver um grande número de testes, você poderá digitar na caixa de pesquisa do **Gerenciador de Testes** para filtrar a lista por uma cadeia de caracteres especificada. Você pode restringir seu evento de filtro ainda mais escolhendo na lista de filtros.

::: moniker range="vs-2017"
![Pesquisar categorias de filtro](../test/media/ute_searchfilter.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Pesquisar categorias de filtro](../test/media/vs-2019/test-explorer-search-filter-16-2.png)
::: moniker-end

|Botão|Descrição|
|-|-|
|![Botão de grupo do Gerenciador de Testes](../test/media/ute_groupby_btn.png)|Para agrupar testes por categoria, escolha o botão **Agrupar por**.|

Para obter mais informações, consulte [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md).

## <a name="qa"></a>Perguntas e respostas

**P: como posso depurar testes de unidade?**

**R:** Use o **Gerenciador de Testes** para iniciar uma sessão de depuração para os testes. Passar pelo código com o depurador do Visual Studio permite-lhe navegar facilmente entre os testes de unidade e o projeto sendo testado. Para iniciar a depuração:

1. No editor do Visual Studio, defina um ponto de interrupção em um ou mais métodos de teste que deseje depurar.

    > [!NOTE]
    > Como os métodos de teste podem ser executados em qualquer ordem, defina pontos de interrupção em todos os métodos de teste que deseje depurar.

2. No **Gerenciador de Testes**, selecione os métodos de teste e, em seguida, escolha **Depurar Testes Selecionados** no menu de atalho.

Obter mais detalhes sobre [como depurar testes de unidade](../debugger/debugger-feature-tour.md).

**P: se eu estiver usando TDD, como gerar código de meus testes?**

**R:** Use ações rápidas para gerar classes e métodos no código do projeto. Grave uma instrução em um método de teste que chame a classe ou o método que você deseja gerar e abra o menu de lâmpada exibido abaixo do erro. Se a chamada for a um construtor da nova classe, escolha **Gerar tipo** no menu e siga o assistente para inserir a classe em seu projeto de código. Se a chamada for a um método, escolha **Gerar método** no menu IntelliSense.

::: moniker range="vs-2017"
![Gerar menu de ação rápida do stub do método](../test/media/ute_generatemethodstubintellisense.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Gerar menu de ação rápida do stub do método](../test/media/vs-2019/basics-generate-method-tdd.png)
::: moniker-end

**P: posso criar testes de unidade que usam vários conjuntos de dados como entrada para executar o teste?**

**R:** Sim. Os *métodos de teste voltados para dados* permitem que você teste um intervalo de valores com um método de teste de unidade. Use um atributo `DataSource` para o método de teste que especifica a fonte de dados e a tabela que contém os valores de variáveis que você deseja testar.  No corpo do método, você atribui os valores de linha a variáveis usando o `TestContext.DataRow[`  `]` indexador ColumnName.

> [!NOTE]
> Esses procedimentos se aplicam somente ao teste de métodos que você escreve usando o Microsoft Unit Test Framework para código gerenciado. Se você estiver usando uma estrutura diferente, consulte a documentação dela para ver a funcionalidade equivalente.

Por exemplo, suponha que adicionamos um método desnecessário para a classe `CheckingAccount` chamada `AddIntegerHelper`. `AddIntegerHelper` adiciona dois números inteiros.

Para criar um teste controlado por dados para o método `AddIntegerHelper`, primeiro, criamos um banco de dados do Access chamado *AccountsTest.accdb* e uma tabela chamada `AddIntegerHelperData`. A tabela `AddIntegerHelperData` define colunas para especificar o primeiro e o segundo operandos da adição e uma coluna para especificar o resultado esperado. Vamos preencher um número de linhas com valores apropriados.

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

O método atribuído é executado uma vez para cada linha na tabela. O **Gerenciador de Testes** relata uma falha de teste para o método se uma das iterações falha. O painel de detalhes de resultados de teste para o método mostra o método de status de aprovação/reprovação para cada linha de dados.

Saiba mais sobre [testes de unidade voltados para dados](../test/how-to-create-a-data-driven-unit-test.md).

**P: posso exibir quanto do meu código é testado pelos meus testes de unidade?**

**R:** Sim. Você pode determinar a quantidade de código que realmente está sendo testada por seus testes de unidade usando a ferramenta de cobertura de código do Visual Studio no Visual Studio Enterprise. Há suporte para idiomas nativos e gerenciados e todas as estruturas de teste de unidade que podem ser executadas pela estrutura de teste de unidade.

Você pode executar a cobertura de código em testes selecionados ou em todos os testes em uma solução. A janela **Resultados da Cobertura de Código** exibe o percentual dos blocos de código de produto que foram exercidos por linha, função, classe, namespace e módulo.

Para executar a cobertura de código para métodos de teste em uma solução, escolha **teste**  >  **analisar cobertura de código para todos os testes**.

Os resultados da cobertura são exibidos na janela **Resultados da Cobertura de Código**.

![Resultados da cobertura de código](../test/media/ute_codecoverageresults.png)

Saiba mais sobre [cobertura de código](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).

**P: posso testar métodos no meu código que possuem dependências externas?**

**R:** Sim. Se você tiver o Visual Studio Enterprise, o Microsoft Fakes pode ser usado com método de teste que você escrever usando estruturas de teste de unidade para código gerenciado.

O Microsoft Fakes usa duas abordagens a fim de criar classes substitutas para dependências externas:

1. *Stubs* geram classes substitutas derivadas da interface pai da classe de dependência de destino. Os métodos stub podem ser substituídos por métodos virtuais públicos da classe de destino.

2. *Shims* usam a instrumentação de runtime para desviar as chamadas a um método de destino para um método shim substituto no caso de métodos não virtuais.

Em ambas as abordagens, você pode usar os representantes de chamadas gerados para o método de dependência a fim de especificar o comportamento desejado no método de teste.

Saiba mais sobre [como isolar métodos de teste de unidade com o Microsoft Fakes](../test/isolating-code-under-test-with-microsoft-fakes.md).

**P: posso usar outras estruturas de teste de unidade para criar testes de unidade?**

**R:** Sim, siga estas etapas para [encontrar e instalar outras estruturas](../test/install-third-party-unit-test-frameworks.md). Depois de reiniciar o Visual Studio, reabra a solução para criar testes de unidade e selecione suas estruturas instaladas aqui:

![Selecionar outra estrutura de teste de unidade instalada](../test/media/createunittestsdialogextensions.png)

Seu stubs de teste de unidade serão criados usando a estrutura selecionada.
