---
title: 'Passo a passo: usando um arquivo de configuração para definir uma fonte de dados | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
helpviewer_keywords:
- configuration files [Visual Studio ALM], defining data sources
- unit tests, walkthrough
- data sources, defining with configuration files
ms.assetid: 95fa5214-b12e-4e1f-84e5-cc4c2d86b0d7
caps.latest.revision: 34
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3f669c4dcfb91579ac50270914112cd6388e2743
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85547973"
---
# <a name="walkthrough-using-a-configuration-file-to-define-a-data-source"></a>Instruções passo a passo: usando um arquivo de configuração para definir uma fonte de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este passo a passo ilustra como usar uma fonte de dados definida em um arquivo app.config para testes de unidade. Você aprenderá como criar um arquivo app.config que defina uma fonte de dados que possa ser usada pela classe <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute>. As tarefas ilustradas nesta explicação passo a passo incluem o seguinte:

- Criando um arquivo app.config.

- Definindo uma seção de configuração personalizada.

- Definindo as cadeias de conexão.

- Definindo as fontes de dados.

- Acessando as fontes de dados usando a classe <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute>.

## <a name="prerequisites"></a>Pré-requisitos
 Para concluir esta explicação passo a passo, será necessário:

- Visual Studio Enterprise

- Microsoft Access ou Microsoft Excel para fornecer dados para pelo menos um dos métodos de teste.

- Uma solução do Visual Studio que contenha um projeto de teste.

## <a name="create-the-appconfig-file"></a>Criar o arquivo App.config

#### <a name="to-add-an-appconfig-file-to-the-project"></a>Como adicionar o arquivo app.config no projeto

1. Se o projeto de teste já tiver um arquivo app.config, vá para [definir uma seção de configuração personalizada](#DefineCustomConfigurationSection).

2. No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto de teste, aponte para **Adicionar** e clique em **Novo Item**.

     A janela **Adicionar Novo Item** é aberta.

3. Selecione o modelo de **Arquivo de Configuração de Aplicativo** e clique em **Adicionar**.

## <a name="define-a-custom-configuration-section"></a><a name="DefineCustomConfigurationSection"></a>Definir uma seção de configuração personalizada
 Examine o arquivo app.config. Ele contém pelo menos a declaração XML e um elemento raiz.

#### <a name="to-add-the-custom-configuration-section-to-the-appconfig-file"></a>Como adicionar a seção de configuração personalizada para o arquivo app.config

1. O elemento raiz de app.config deve ser o elemento `configuration`. Crie um elemento `configSections` dentro do elemento `configuration`. O `configSections` deve ser o primeiro elemento no arquivo app.config.

2. No elemento `configSections`, crie um elemento `section`.

3. No elemento `section`, adicione um atributo chamado `name` e atribua um valor igual a `microsoft.visualstudio.testtools` a ele. Adicione outro atributo chamado `type` e atribua a ele um valor igual a `Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection, Microsoft.VisualStudio.QualityTools.UnitTestFramework, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a`

   O elemento `section` deverá ser similar a esse:

```
<section name="microsoft.visualstudio.testtools" type="Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection, Microsoft.VisualStudio.QualityTools.UnitTestFramework, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"/>
```

> [!NOTE]
> O nome do assembly deve corresponder ao build do Microsoft Visual Studio .NET Framework que você está usando. Defina a versão para 9.0.0.0 se você estiver usando o Visual Studio .NET Framework 3.5. Se você estiver usando o Visual Studio .NET Framework 2.0, defina a versão para 8.0.0.0.

## <a name="define-connection-strings"></a>Definir as cadeias de conexão
 As cadeias de conexão definem as informações específicas do provedor para acessar fontes de dados. As cadeias de conexão definidas em arquivos de configuração fornecem informações do provedor de dados reutilizáveis em um aplicativo. Nesta seção, você criará duas cadeias de conexão que serão usadas por fontes de dados que são definidas na seção de configuração personalizada.

#### <a name="to-define-connection-strings"></a>Como definir as cadeias de conexão

1. Após o elemento `configSections`, crie um elemento `connectionStrings`.

2. No elemento `connectionStrings`, crie dois elementos `add`.

3. No primeiro elemento `add`, crie os seguintes atributos e valores para uma conexão a um banco de dados do Microsoft Access:

|Atributo|Valores|
|---------------|------------|
|`name`|`"MyJetConn"`|
|`connectionString`|`"Provider=Microsoft.Jet.OLEDB.4.0; Data Source=C:\testdatasource.accdb; Persist Security Info=False;"`|
|`providerName`|`"System.Data.OleDb"`|

 No segundo elemento `add`, crie os seguintes atributos e valores para uma conexão a uma planilha do Microsoft Excel:

|Atributo|Valores|
|-|-|
|`name`|`"MyExcelConn"`|
|`connectionString`|`"Dsn=Excel Files;dbq=data.xlsx;defaultdir=.; driverid=790;maxbuffersize=2048;pagetimeout=5"`|
|`providerName`|`"System.Data.Odbc"`|

 O elemento `connectionStrings` deverá ser similar a esse:

```xml
<connectionStrings>
    <add name="MyJetConn" connectionString="Provider=Microsoft.Jet.OLEDB.4.0; Data Source=C:\testdatasource.accdb; Persist Security Info=False;" providerName="System.Data.OleDb" />
    <add name="MyExcelConn" connectionString="Dsn=Excel Files;dbq=data.xlsx;defaultdir=.; driverid=790;maxbuffersize=2048;pagetimeout=5" providerName="System.Data.Odbc" />
</connectionStrings>
```

## <a name="define-data-sources"></a>Definir fontes de dados
 A seção de fontes de dados contém quatro atributos que são usados pelo mecanismo de teste para recuperar dados de uma fonte de dados.

- `name` define a identidade usada pelo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.DataSourceAttribute> para especificar qual fonte de dados será usada.

- `connectionString` identifica a cadeia de conexão criada na seção anterior Definir cadeias de conexão.

- `dataTableName` define a tabela ou a planilha que contém os dados a serem usados no teste.

- `dataAccessMethod` define a técnica para acessar valores de dados na fonte de dados.

  Nesta seção, você definirá duas fontes de dados para usar em um teste de unidade.

#### <a name="to-define-data-sources"></a>Como definir fontes de dados

1. Após o elemento `connectionStrings`, crie um elemento `microsoft.visualstudio.testtools`. Esta seção foi criada na seção Definir uma configuração personalizada.

2. No elemento `microsoft.visualstudio.testtools`, crie um elemento `dataSources`.

3. No elemento `dataSources`, crie dois elementos `add`.

4. No primeiro elemento `add`, crie os seguintes atributos e valores para uma fonte de dados do Microsoft Access:

|Atributo|Valor|
|---------------|------------|
|`name`|`"MyJetDataSource"`|
|`connectionString`|`"MyJetConn"`|
|`dataTableName`|`"MyDataTable"`|
|`dataAccessMethod`|`"Sequential"`|

 No segundo elemento `add`, crie os seguintes atributos e valores para uma fonte de dados do Microsoft Excel:

|Atributo|Valor|
|-|-|
|`Name`|`"MyExcelDataSource"`|
|`connectionString`|`"MyExcelConn"`|
|`dataTableName`|`"Sheet1$"`|
|`dataAccessMethod`|`"Sequential"`|

 O elemento `microsoft.visualstudio.testtools` deverá ser similar a esse:

```xml
<microsoft.visualstudio.testtools>
    <dataSources>
        <add name="MyJetDataSource" connectionString="MyJetConn" dataTableName="MyDataTable" dataAccessMethod="Sequential"/>
        <add name="MyExcelDataSource" connectionString="MyExcelConn" dataTableName="Sheet1$" dataAccessMethod="Sequential"/>
    </dataSources>
</microsoft.visualstudio.testtools>
```

 O arquivo app.config final deve ser semelhante a este:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <configSections>
        <section name="microsoft.visualstudio.testtools" type="Microsoft.VisualStudio.TestTools.UnitTesting.TestConfigurationSection, Microsoft.VisualStudio.QualityTools.UnitTestFramework, Version=8.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a"/>
    </configSections>
    <connectionStrings>
        <add name="MyJetConn" connectionString="Provider=Microsoft.Jet.OLEDB.4.0; Data Source=C:\testdatasource.accdb; Persist Security Info=False;" providerName="System.Data.OleDb" />
        <add name="MyExcelConn" connectionString="Dsn=Excel Files;dbq=data.xlsx;defaultdir=.; driverid=790;maxbuffersize=2048;pagetimeout=5" providerName="System.Data.Odbc" />
    </connectionStrings>
    <microsoft.visualstudio.testtools>
        <dataSources>
            <add name="MyJetDataSource" connectionString="MyJetConn" dataTableName="MyDataTable" dataAccessMethod="Sequential"/>
            <add name="MyExcelDataSource" connectionString="MyExcelConn" dataTableName="Sheet1$" dataAccessMethod="Sequential"/>
        </dataSources>
    </microsoft.visualstudio.testtools>
</configuration>
```

## <a name="create-a-unit-test-using-data-sources-defined-in-appconfig"></a>Criar um teste de unidade usando fontes de dados definidas no app.config
 Agora que um arquivo app.config foi definido, você criará um teste de unidade que usa dados localizados em fontes de dados que são definidas no arquivo app.config. Nesta seção, iremos:

- Criar fontes de dados localizadas no arquivo app.config.

- Usar as fontes de dados em dois métodos de teste que comparam os valores em cada fonte de dados.

#### <a name="to-create-a-microsoft-access-data-source"></a>Como criar uma fonte de dados do Microsoft Access

1. Crie um banco de dados do Microsoft Access chamado `testdatasource.accdb`.

2. Criar uma tabela e nomeie-a como `MyDataTable` em `testdatasource.accdb`.

3. Crie dois campos em `MyDataTable` chamados `Arg1` e `Arg2` usando o tipo de dados `Number`.

4. Adicione cinco entidades em `MyDataTable` com os seguintes valores para `Arg1` e `Arg2`, respectivamente: (10,50), (3,2), (6,0), (0,8) e (12312,1000).

5. Salve e feche o banco de dados.

6. Altere a cadeia de conexão para apontar para o local do banco de dados. Altere o valor de `Data Source` para refletir o local do banco de dados.

#### <a name="to-create-a-microsoft-excel-data-source"></a>Como criar uma fonte de dados do Microsoft Excel

1. Crie uma planilha do Microsoft Excel chamada `data.xlsx`.

2. Crie uma planilha chamada `Sheet1`, se ainda não existir em `data.xlsx`.

3. Crie dois cabeçalhos de coluna e nomeie-os como `Val1` e `Val2` em `Sheet1`.

4. Adicione cinco entidades em `Sheet1` com os seguintes valores para `Val1` e `Val2`, respectivamente: (1,1), (2,2), (3,3), (4,4) e (5,0).

5. Salve e feche a planilha.

6. Altere a cadeia de conexão para apontar para o local da planilha. Altere o valor de `dbq` para refletir o local da planilha.

#### <a name="to-create-a-unit-test-using-the-appconfig-data-sources"></a>Como criar um teste de unidade usando fontes de dados app.config

1. Adicione um teste de unidade ao projeto de teste.

     Para mais informações, consulte [Criar e executar testes de unidade para código existente](https://msdn.microsoft.com/e8370b93-085b-41c9-8dec-655bd886f173).

2. Substitua o conteúdo do teste de unidade gerado automaticamente pelo código a seguir:

    ```csharp
    using System;
    using Microsoft.VisualStudio.TestTools.UnitTesting;

    namespace TestProject1
    {
         [TestClass]
        public class UnitTest1
        {
            private TestContext context;

            public TestContext TestContext
            {
                get { return context; }
                set { context = value; }
            }

            [TestMethod()]
            [DeploymentItem("MyTestProject\\testdatasource.accdb")]
            [DataSource("MyJetDataSource")]
            public void MyTestMethod()
            {
                int a = Int32.Parse(context.DataRow["Arg1"].ToString());
                int b = Int32.Parse(context.DataRow["Arg2"].ToString());
                Assert.AreNotEqual(a, b, "A value was equal.");
            }

            [TestMethod()]
            [DeploymentItem("MyTestProject\\data.xlsx")]
            [DataSource("MyExcelDataSource")]
            public void MyTestMethod2()
            {
                Assert.AreEqual(context.DataRow["Val1"], context.DataRow["Val2"]);
            }
        }
    }
    ```

3. Examine os atributos DataSource. Observe os nomes de configuração do arquivo app.config.

4. Compile sua solução e execute testes MyTestMethod e MyTestMethod2.

> [!IMPORTANT]
> Implante itens como fontes de dados para que fiquem acessíveis para o teste no diretório de implantação.

## <a name="see-also"></a>Consulte Também
 [Teste de unidade seu código](../test/unit-test-your-code.md) [criando e executando testes de unidade para testar o código existente](https://msdn.microsoft.com/e8370b93-085b-41c9-8dec-655bd886f173) [no aplicativo](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac) [como criar um teste de unidade controlado por dados](../test/how-to-create-a-data-driven-unit-test.md)
