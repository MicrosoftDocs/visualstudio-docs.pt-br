---
title: Como criar um teste de unidade orientado a dados | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-devops-test
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.test.testresults.unittest.datadriven
- vs.test.testresults.unittest.datadriven.failure
helpviewer_keywords:
- unit tests, running
- unit tests, data-driven
- data-driven unit tests
ms.assetid: a0322bc5-02c8-4f9f-af43-100a60b1bd28
caps.latest.revision: 35
ms.author: gewarren
manager: douge
ms.openlocfilehash: eeb7efb0c7faa9a2493cfd3f91f6cc4e72408f4c
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49889354"
---
# <a name="how-to-create-a-data-driven-unit-test"></a>Como criar um teste de unidade orientado a dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ao usar a estrutura de teste de unidade da Microsoft para código gerenciado, você pode configurar um método de teste de unidade para recuperar valores usados no método de teste de uma fonte de dados. O método é executado sucessivamente para cada linha na fonte de dados, o que facilita o teste de uma variedade de entradas usando um único método.  
  
 Esse tópico contém as seguintes seções:  
  
- [O método em teste](../test/how-to-create-a-data-driven-unit-test.md#BKMK_The_method_under_test)  
  
- [Criar uma fonte de dados](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Creating_a_data_source)  
  
- [Adicionar um TestContext para a classe de teste](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Adding_a_TestContext_to_the_test_class)  
  
- [Escrever o método de teste](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Writing_the_test_method)  
  
  -   [Especificar o DataSourceAttribute](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Specifying_the_DataSourceAttribute)  
  
  -   [Usar o TestContext.DataRow para acessar os dados](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Using_TestContext_DataRow_to_access_the_data)  
  
- [Execução do teste e exibição dos resultados](../test/how-to-create-a-data-driven-unit-test.md#BKMK_Running_the_test_and_viewing_results)  
  
  A criação de um teste de unidade orientado a dados envolve as seguintes etapas:  
  
1.  Criar uma fonte de dados que contém os valores a serem usados no método de teste. A fonte de dados pode ser de qualquer tipo que esteja registrado no computador que executa o teste.  
  
2.  Adicionar um campo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext> privado e uma propriedade `TestContext` pública à classe de teste.  
  
3.  Criear um método de teste de unidade e adicionar um atributo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> a ele.  
  
4.  Usar o propriedade do indexador <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A> para recuperar os valores que você pode usar em um teste.  
  
##  <a name="BKMK_The_method_under_test"></a> O método em teste  
 Como exemplo, vamos supor que criamos:  
  
1. Uma solução chamada `MyBank` que aceita e processa transações para diferentes tipos de contas.  
  
2. Um projeto em `MyBank` chamado `BankDb` que gerencia as transações das contas.  
  
3. Uma classe chamada `Maths` no projeto `DbBank` que executa as funções matemáticas para garantir que qualquer transação seja vantajosa para o banco.  
  
4. Um projeto de teste de unidade chamado `BankDbTests` para testar o comportamento do componente `BankDb`.  
  
5. Uma classe de teste de unidade chamada `MathsTests` para verificar o comportamento da classe `Maths`.  
  
   Testaremos um método em `Maths` que acrescenta dois inteiros usando um loop:  
  
```  
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
  
##  <a name="BKMK_Creating_a_data_source"></a> Criar uma fonte de dados  
 Para testar o método `AddIntegers`, criamos uma fonte de dados que especifica um intervalo de valores para os parâmetros e a soma que você espera que seja retornada. Em nosso exemplo, criamos um banco de dados do Sql Compact chamado `MathsData` e uma tabela chamada `AddIntegersData` que contém os seguintes nomes de coluna e valores  
  
|FirstNumber|SecondNumber|Sum|  
|-----------------|------------------|---------|  
|0|1|1|  
|1|1|2|  
|2|-3|-1|  
  
##  <a name="BKMK_Adding_a_TestContext_to_the_test_class"></a> Adicionar um TestContext para a classe de teste  
 A estrutura de teste de unidade cria um objeto `TestContext` para armazenar as informações de fonte de dados de um teste orientado a dados. Em seguida, a estrutura define esse objeto como o valor da propriedade `TestContext` que criamos.  
  
```  
  
private TestContext testContextInstance;  
public TestContext TestContext  
{  
    get { return testContextInstance; }  
    set { testContextInstance = value; }  
}  
  
```  
  
 Em seu método de teste, os dados são acessados por meio da propriedade do indexador `DataRow` do `TestContext`.  
  
##  <a name="BKMK_Writing_the_test_method"></a> Escrever o método de teste  
 O método de teste de `AddIntegers` é bastante simples. Para cada linha na fonte de dados, chamamos `AddIntegers` com os valores de coluna **FirstNumber** e **SecondNumber** como parâmetros e verificamos o valor retornado no valor da coluna **Sum**:  
  
```  
  
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
  
 Observe que o método `Assert` inclui uma mensagem que exibe os valores `x` e `y` de uma iteração com falha. Por padrão, os valores declarados `expected` e `actual` já estão incluídos nos detalhes de uma teste com falha.  
  
###  <a name="BKMK_Specifying_the_DataSourceAttribute"></a> Especificar o DataSourceAttribute  
 O atributo `DataSource` especifica a cadeia de conexão para a fonte de dados e o nome da tabela a ser usada no método de teste. As informações exatas na cadeia de conexão são diferentes, dependendo do tipo de fonte de dados que você está usando. Neste exemplo, usamos um banco de dados SqlServerCe.  
  
```  
[DataSource(@"Provider=Microsoft.SqlServerCe.Client.4.0;Data Source=C:\Data\MathsData.sdf", "AddIntegersData")]  
```  
  
 O atributo DataSource tem três construtores.  
  
```  
[DataSource(dataSourceSettingName)]  
```  
  
 Um construtor com um parâmetro usa informações de conexão armazenadas no arquivo app.config para a solução. O *dataSourceSettingsName* é o nome do elemento XML no arquivo de configuração que especifica as informações de conexão.  
  
 Ao usar um arquivo app.config você pode alterar o local da fonte de dados sem fazer alterações no próprio teste de unidade. Para obter informações sobre como criar e usar um arquivo app.config, consulte [Passo a passo: usando um arquivo de configuração para definir uma fonte de dados](../test/walkthrough-using-a-configuration-file-to-define-a-data-source.md)  
  
```  
[DataSource(connectionString, tableName)]  
```  
  
 O construtor `DataSource` com dois parâmetros especifica a cadeia de conexão da fonte de dados e o nome da tabela que contém os dados para o método de teste.  
  
 As cadeias de conexão dependem do tipo de fonte de dados, mas elas devem conter um elemento Provedor que especifica o nome invariável do provedor de dados.  
  
```  
[DataSource(  
    dataProvider,   
    connectionString,   
    tableName,  
    dataAccessMethod  
    )]  
```  
  
###  <a name="BKMK_Using_TestContext_DataRow_to_access_the_data"></a> Usar o TestContext.DataRow para acessar os dados  
 Para acessar os dados na tabela `AddIntegersData`, use o indexador `TestContext.DataRow`. `DataRow` é um objeto <xref:System.Data.DataRow>, para que seja possível recuperar valores de colunas por índice ou nomes de colunas. Como os valores são retornados como objetos, é preciso convertê-los para o tipo apropriado:  
  
```  
int x = Convert.ToInt32(TestContext.DataRow["FirstNumber"]);  
  
```  
  
##  <a name="BKMK_Running_the_test_and_viewing_results"></a> Execução do teste e exibição dos resultados  
 Ao terminar de escrever um método de teste, compile o projeto de teste. O método de teste aparece na janela Gerenciador de Testes, no grupo **Testes Não Executados**. Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados em grupos de **Testes Reprovados**, **Testes Aprovados** e **Testes Não Executados**. Você pode escolher **Executar Tudo** para executar todos os testes ou **Executar...** para escolher um subconjunto de testes a serem executados.  
  
 A barra de resultados de teste na parte superior do Gerenciador é animada enquanto o teste é executado. Ao final da execução de teste, a barra ficará verde se todos os testes passaram ou vermelha se algum dos testes falhou. Um resumo da execução de teste é exibido no painel de detalhes na parte inferior da janela do Gerenciador de Testes. Selecione um teste para exibir seus detalhes no painel inferior.  
  
 Se você executou o método `AddIntegers_FromDataSourceTest` em nosso exemplo, a barra de resultados fica vermelha e o método de teste é movido para **Testes com falha**. Um teste orientado a dados falhará se qualquer um dos métodos de iteração da fonte de dados falhar. Ao escolher um teste orientado a dados que falhou na janela do Gerenciador de Testes, o painel de detalhes exibe os resultados de cada iteração, que é identificada pelo índice de linha de dados. Em nosso exemplo, parece que o algoritmo `AddIntegers` não manipula valores negativos corretamente.  
  
 Quando o método em teste é corrigido e o teste é novamente executado, a barra de resultados ficará verde e o método de teste é movido para o grupo **Teste Aprovado**.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute?displayProperty=fullName>   
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext?displayProperty=fullName>   
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestContext.DataRow%2A?displayProperty=fullName>   
 <xref:Microsoft.VisualStudio.TestTools.UnitTesting.Assert?displayProperty=fullName>   
 [Como criar e executar um teste de unidade](http://msdn.microsoft.com/en-us/5e0f43cf-5e51-48e2-9c98-0eb9324bdc48)   
 [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)   
 [Executar testes de unidade com o Gerenciador de Testes](../test/run-unit-tests-with-test-explorer.md)   
 [Escrevendo testes de unidade para .NET Framework com a estrutura de teste de unidade Microsoft para código gerenciado](../test/writing-unit-tests-for-the-dotnet-framework-with-the-microsoft-unit-test-framework-for-managed-code.md)



