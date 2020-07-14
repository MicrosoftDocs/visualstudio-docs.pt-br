---
title: Criar um testes de unidade controlados por dados
ms.date: 05/08/2019
ms.topic: how-to
f1_keywords:
- vs.test.testresults.unittest.datadriven
- vs.test.testresults.unittest.datadriven.failure
helpviewer_keywords:
- unit tests, running
- unit tests, data-driven
- data-driven unit tests
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
author: mikejo5000
ms.openlocfilehash: 936c6b2ee9e05d059c09c2aa074829b35b6ca5fd
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85287981"
---
# <a name="how-to-create-a-data-driven-unit-test"></a>Como: criar um teste de unidade controlado por dados

Você pode usar a estrutura de teste de unidade da Microsoft para o código gerenciado para configurar um método de teste de unidade para recuperar valores de uma fonte de dados. O método é executado sucessivamente para cada linha na fonte de dados, o que facilita o teste de uma variedade de entradas usando um único método.

A criação de um teste de unidade orientado a dados envolve as seguintes etapas:

1. Criar uma fonte de dados que contém os valores a serem usados no método de teste. A fonte de dados pode ser de qualquer tipo que esteja registrado no computador que executa o teste.

2. Adicionar um campo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> privado e uma propriedade `TestContext` pública à classe de teste.

3. Criear um método de teste de unidade e adicionar um atributo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> a ele.

4. Usar o propriedade do indexador <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A> para recuperar os valores que você pode usar em um teste.

## <a name="the-method-under-test"></a>O método em teste

Por exemplo, vamos supor que você tenha:

1. Uma solução chamada `MyBank` que aceita e processa transações para diferentes tipos de contas.

2. Um projeto em `MyBank` chamado `BankDb` que gerencia as transações das contas.

3. Uma classe chamada `Maths` no projeto `BankDb` que executa as funções matemáticas para garantir que qualquer transação seja vantajosa para o banco.

4. Um projeto de teste de unidade chamado `BankDbTests` para testar o comportamento do componente `BankDb`.

5. Uma classe de teste de unidade chamada `MathsTests` para verificar o comportamento da classe `Maths`.

Testaremos um método em `Maths` que adiciona dois números inteiros usando um loop:

```csharp
public int AddIntegers(int first, int second)
{
    int sum = first;
    for( int i = 0; i < second; i++)
    {
        sum += 1;
    }
    return sum;
}
```

## <a name="create-a-data-source"></a>Criar uma fonte de dados

Para testar o método `AddIntegers`, crie uma fonte de dados que especifica um intervalo de valores para os parâmetros e a soma que você espera que seja retornada. Neste exemplo, criaremos um banco de dados do SQL Compact chamado `MathsData` e uma tabela chamada `AddIntegersData` que contém os seguintes nomes de coluna e valores

|FirstNumber|SecondNumber|SUM|
|-|------------------|-|
|0|1|1|
|1|1|2|
|2|-3|-1|

## <a name="add-a-testcontext-to-the-test-class"></a>Adicionar um TestContext à classe de teste

A estrutura de teste de unidade cria um objeto `TestContext` para armazenar as informações de fonte de dados de um teste orientado a dados. Em seguida, a estrutura define esse objeto como o valor da propriedade `TestContext` que você criou.

```csharp
private TestContext testContextInstance;
public TestContext TestContext
{
    get { return testContextInstance; }
    set { testContextInstance = value; }
}
```

Em seu método de teste, os dados são acessados por meio da propriedade do indexador `DataRow` do `TestContext`.

> [!NOTE]
> O .NET Core não dá suporte ao atributo [DataSource](xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute). Se tentar acessar os dados de teste dessa forma em um projeto de teste de unidade do .NET Core ou do UWP, você verá um erro semelhante a **"TestContext não contém uma definição para 'DataRow' e nenhum 'DataRow' do método de extensão acessível que aceita um primeiro argumento do tipo 'TestContext' pôde ser encontrado (alguma diretiva em uso ou uma referência de assembly está ausente?)"**.

## <a name="write-the-test-method"></a>Escrever o método de teste

O método de teste de `AddIntegers` é bastante simples. Para cada linha na fonte de dados, chame `AddIntegers` com os valores de coluna **FirstNumber** e **SecondNumber** como parâmetros e verifique o valor retornado no valor da coluna **Sum**:

```csharp
[DataSource(@"Provider=Microsoft.SqlServerCe.Client.4.0; Data Source=C:\Data\MathsData.sdf;", "Numbers")]
[TestMethod()]
public void AddIntegers_FromDataSourceTest()
{
    var target = new Maths();

    // Access the data
    int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);
    int y = Convert.ToInt32(TestContext.DataRow["SecondNumber"]);
    int expected = Convert.ToInt32(TestContext.DataRow["Sum"]);
    int actual = target.IntegerMethod(x, y);
    Assert.AreEqual(expected, actual,
        "x:<{0}> y:<{1}>",
        new object[] {x, y});
}
```

O método `Assert` inclui uma mensagem que exibe os valores `x` e `y` de uma iteração com falha. Por padrão, os valores declarados – `expected` e `actual` – já estão incluídos nos detalhes do teste com falha.

### <a name="specify-the-datasourceattribute"></a>Especificar o DataSourceAttribute

O atributo `DataSource` especifica a cadeia de conexão para a fonte de dados e o nome da tabela a ser usada no método de teste. As informações exatas na cadeia de conexão são diferentes, dependendo do tipo de fonte de dados que você está usando. Neste exemplo, usamos um banco de dados SqlServerCe.

```csharp
[DataSource(@"Provider=Microsoft.SqlServerCe.Client.4.0;Data Source=C:\Data\MathsData.sdf", "AddIntegersData")]
```

O atributo DataSource tem três construtores.

```csharp
[DataSource(dataSourceSettingName)]
```

Um construtor com um parâmetro usa informações de conexão que são armazenadas no arquivo de *app.config* para a solução. O *dataSourceSettingsName* é o nome do elemento XML no arquivo de configuração que especifica as informações de conexão.

O uso de um arquivo de *app.config* permite que você altere o local da fonte de dados sem fazer alterações no próprio teste de unidade. Para obter informações sobre como criar e usar um arquivo de *app.config* , consulte [Walkthrough: usando um arquivo de configuração para definir uma fonte de dados](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md)

```csharp
[DataSource(connectionString, tableName)]
```

O construtor `DataSource` com dois parâmetros especifica a cadeia de conexão da fonte de dados e o nome da tabela que contém os dados para o método de teste.

As cadeias de conexão dependem do tipo de fonte de dados, mas elas devem conter um elemento Provedor que especifica o nome invariável do provedor de dados.

```csharp
[DataSource(
    dataProvider,
    connectionString,
    tableName,
    dataAccessMethod
    )]
```

### <a name="use-testcontextdatarow-to-access-the-data"></a>Usar o TestContext.DataRow para acessar os dados

Para acessar os dados na tabela `AddIntegersData`, use o indexador `TestContext.DataRow`. `DataRow` é um objeto <xref:System.Data.DataRow>, para que seja possível recuperar valores de colunas por índice ou nomes de colunas. Como os valores são retornados como objetos, converta-os para o tipo apropriado:

```csharp
int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);
```

## <a name="run-the-test-and-view-results"></a>Executar o teste e exibir os resultados

Ao terminar de escrever um método de teste, compile o projeto de teste. O método de teste é exibido em **Gerenciador de Testes**, no grupo **Testes Não Executados**. À medida que você executa, escreve e executa novamente os testes, o **Gerenciador de testes** exibe os resultados em grupos de **testes com falha**, **aprovados**nos testes e **não executa testes**. Você pode escolher **executar tudo** para executar todos os seus testes ou escolher **executar** para escolher um subconjunto de testes a serem executados.

A barra de resultados de teste na parte superior do **Gerenciador de Testes** é animada enquanto o teste é executado. Ao final da execução de teste, a barra ficará verde se todos os testes passaram ou vermelha se algum dos testes falhou. Um resumo da execução de teste é exibido no painel detalhes na parte inferior da janela **Gerenciador de testes** . Selecione um teste para exibir seus detalhes no painel inferior.

> [!NOTE]
> Há um resultado para cada linha de dados e também um resumo de resultados. Se o teste foi aprovado em cada linha de dados, o resumo de execução mostra como **Aprovado**. Se o teste falhou em alguma linha de dados, o resumo de execução mostra como **Falha**.

Se você executou o método `AddIntegers_FromDataSourceTest` de nosso exemplo, a barra de resultados fica vermelha e o método de teste é movido para **Testes Reprovados**. Um teste controlado por dados falha se um dos métodos iterados da fonte de dados falha. Quando você escolhe um teste controlado por dados com falha na janela **Gerenciador de testes** , o painel Detalhes exibe os resultados de cada iteração identificada pelo índice de linha de dados. Em nosso exemplo, parece que o algoritmo `AddIntegers` não manipula valores negativos corretamente.

Quando o método em teste é corrigido e o teste é novamente executado, a barra de resultados ficará verde e o método de teste é movido para o grupo **Teste Aprovado**.

## <a name="see-also"></a>Veja também

- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute?displayProperty=fullName>
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext?displayProperty=fullName>
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A?displayProperty=fullName>
- <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=fullName>
- [Teste de unidade em seu código](../test/unit-test-your-code.md)
- [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md)
- [Escrever testes de unidade para o .NET com a estrutura de teste de unidade da Microsoft](../test/unit-test-your-code.md)
