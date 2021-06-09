---
title: Criar um Windows Form para pesquisar dados
description: Leia um exemplo de como criar um Windows Form para pesquisar dados. Crie o aplicativo Windows Form, a fonte de dados e o formulário. Adicionar parametrização. Testar o aplicativo.
ms.custom: SEO-VS-2020
ms.date: 06/07/2021
ms.topic: conceptual
helpviewer_keywords:
- Windows Forms, searching data
- Windows Forms, displaying data
- parameters, displaying filtered data
- data [Visual Studio], parameterizing queries
- data [Visual Studio], searching
ms.assetid: 65ca79a9-7458-466c-af55-978cd24c549e
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- data-storage
ms.openlocfilehash: 2ce9d3eeebf42855ad69f02b2d72330190a2b390
ms.sourcegitcommit: 01a411cd7ae3488b7b979a947bca92fd296a98e9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111761089"
---
# <a name="create-a-windows-form-to-search-data"></a>Criar um Windows Form para pesquisar dados

Um cenário de aplicativo comum exibirá dados selecionados em um formulário. Por exemplo, você pode querer exibir os pedidos de um cliente específico ou os detalhes de um pedido específico. Nesse cenário, um usuário insere informações em um formulário e uma consulta é executada com a entrada do usuário como parâmetro, ou seja, os dados são selecionados com base em uma consulta parametrizada. A consulta retorna apenas os dados que satisfazem os critérios inseridos pelo usuário. Este passo a passo mostra como criar uma consulta que retorna clientes de uma cidade específica, como mudar a interface do usuário para que os usuários possam inserir o nome de uma cidade e pressionar um botão para executar a consulta.

O uso de consultas parametrizadas ajuda a tornar seu aplicativo eficiente, permitindo que o banco de dados funcione melhor, filtrando registros rapidamente. Por outro lado, se você solicitar uma tabela de banco de dados inteira, transferi-la pela rede e usar a lógica do aplicativo para encontrar os registros que deseja, o aplicativo poderá ficar lento e ineficiente.

Você pode adicionar consultas parametrizadas a qualquer TableAdapter (e controles para aceitar valores de parâmetro e executar a consulta), usando a **caixa** de diálogo Construtor de Critérios de Pesquisa. Abra a caixa de diálogo selecionando o comando **Adicionar Consulta** no menu **Dados** (ou em qualquer marcação inteligente de TableAdapter).

As tarefas ilustradas neste passo a passo incluem:

- Criando e configurando a fonte de dados em seu aplicativo com o assistente **de Configuração da Fonte de** Dados.

- Definir o tipo de soltar dos itens na janela **Fontes de** Dados.

- Criar controles que exibem dados arrastando itens da janela **Fontes de Dados** para um formulário.

- Adicionar controles para exibir os dados no formulário.

- Concluindo a caixa **de diálogo Construtor de Critérios** de Pesquisa.

- Inserindo parâmetros no formulário e executando a consulta parametrizada.

> [!NOTE]
> Os procedimentos neste artigo se aplicam somente a projetos .NET Framework Windows Forms, não a projetos de Windows Forms .NET Core.

## <a name="prerequisites"></a>Pré-requisitos

Você deve ter a **carga de trabalho armazenamento e processamento de** dados instalada. Consulte [Modificar Visual Studio](../install/modify-visual-studio.md).

Este passo a passo usa SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver SQL Server Express LocalDB, instale-o na página [de download do](https://www.microsoft.com/sql-server/sql-server-editions-express)SQL Server Express ou por meio do **Instalador do Visual Studio**. No **Instalador do Visual Studio**, você pode instalar SQL Server Express LocalDB como parte  da carga de trabalho armazenamento e processamento de dados ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind seguindo estas etapas:

    1. No Visual Studio, abra a **Pesquisador de Objetos do SQL Server** janela. (Pesquisador de Objetos do SQL Server é instalado como parte da carga de trabalho armazenamento e **processamento** de dados no **Instalador do Visual Studio**.) Expanda **o SQL Server** nó. Clique com o botão direito do mouse na instância do LocalDB e **selecione Nova Consulta**.

       Uma janela do editor de consultas é aberta.

    2. Copie o [script Transact-SQL northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) para a área de transferência. Esse script T-SQL cria o banco de dados Northwind do zero e o popula com dados.

    3. Colar o script T-SQL no editor de consultas e, em seguida, escolha o **botão** Executar.

       Após um curto período, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="create-the-windows-forms-application"></a>Criar o Windows Forms aplicativo

:::moniker range="vs-2017"

Crie um novo **Windows Forms (.NET Framework)** para C# ou Visual Basic. Nomeie o projeto **WindowsSearchForm**.

## <a name="create-the-data-source"></a>Criar a fonte de dados

Esta etapa cria uma fonte de dados por meio de um banco de dados usando o assistente de **Configuração de Fonte de Dados**:

1. Para abrir a **janela Fontes de** Dados, no menu **Dados,** clique **em Mostrar Fontes de Dados**.

2. Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o assistente de **Configuração de Fonte de Dados**.

3. Selecione **Banco de Dados** na página **Escolher um Tipo de Fonte de Dados** e, em seguida, clique em **Avançar**.

4. Na página **Escolher sua Conexão de** Dados, faça o seguinte:

    - Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

    - Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

5. Se o banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **Avançar**.

6. Na página **Salvar cadeia de conexão no arquivo configuração de aplicativo,** clique em **Próximo.**

7. Na página **Escolher seus Objetos de Banco de** Dados, expanda o nó **Tabelas.**

8. Selecione a tabela **Clientes** e clique em **Concluir**.

     O **NorthwindDataSet** é adicionado ao seu projeto e a tabela **Clientes** aparece na janela **Fontes de Dados**.

:::moniker-end

:::moniker range=">=vs-2019"

Crie um novo **Windows Forms (.NET Framework)** para C# ou Visual Basic. Nomeie o projeto **WindowsSearchForm**.

## <a name="create-the-data-source"></a>Criar a fonte de dados

Esta etapa cria uma fonte de dados por meio de um banco de dados usando o assistente de **Configuração de Fonte de Dados**:

1. Para abrir a **janela Fontes de** Dados, use a pesquisa rápida (**Ctrl** + **Q**) e pesquise **Fontes de Dados**.

1. Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o assistente de **Configuração de Fonte de Dados**.

1. Selecione **Banco de Dados** na página **Escolher um Tipo de Fonte de Dados** e, em seguida, clique em **Avançar**.

1. Na tela **Escolher um Modelo de Banco** de Dados, escolha Conjuntos **de** dados e clique em **Próximo.**

1. Na página **Escolher sua Conexão de** Dados, faça o seguinte:

    - Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

    - Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

1. Na página **Salvar cadeia de conexão no arquivo configuração de aplicativo,** clique em **Próximo.**

1. Na página **Escolher seus Objetos de Banco de** Dados, expanda o nó **Tabelas.**

1. Selecione a tabela **Clientes** e clique em **Concluir**.

     O **NorthwindDataSet** é adicionado ao seu projeto e a tabela **Clientes** aparece na janela **Fontes de Dados**.

:::moniker-end

## <a name="create-the-form"></a> Criar o formulário

Você pode criar controles de associação de dados arrastando itens da janela **Fontes de Dados** para um formulário:

1. Certifique-se de que Windows Forms designer tenha o foco ativo e se a janela **Fontes de** Dados está aberta e fixada.

1. Expanda o nó **Clientes** na janela **Fontes de Dados**.

1. Arraste o nó **Clientes** da janela **Fontes de Dados** para o formulário.

     Um <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), CustomersTableAdapter, <xref:System.Windows.Forms.BindingSource> e <xref:System.Windows.Forms.BindingNavigator> são exibidos na bandeja de componentes.

## <a name="add-parameterization-search-functionality-to-the-query"></a>Adicionar parametrização (funcionalidade de pesquisa) à consulta

Você pode adicionar uma cláusula WHERE à consulta original usando a caixa de diálogo Construtor de **Critérios de** Pesquisa:

1. Logo abaixo da superfície de design do formulário, selecione o  botão **customersTableAdapter** e, na janela Propriedades, escolha **Adicionar Consulta...**.

2. Digite **FillByCity** na área **Novo nome da consulta** na caixa de diálogo Construtor de **Critérios de** Pesquisa.

3. Adicione `WHERE City = @City` à consulta na área **Texto da Consulta**.

     A consulta deve ser semelhante ao seguinte:

     ```sql
     SELECT CustomerID, CompanyName, ContactName, ContactTitle,
          Address, City, Region, PostalCode, Country, Phone, Fax
     FROM Customers
     WHERE City = @City
     ```

    > [!NOTE]
    > As fontes de OLE DB de dados usam o ponto de interrogação ('?') para denotar parâmetros, portanto, a cláusula WHERE teria esta aparência: `WHERE City = ?` .

4. Clique em **OK** para fechar a caixa de diálogo **Construtor de Critérios de Pesquisa**.

     Um **FillByCityToolStrip** é adicionado ao formulário.

## <a name="test-the-application"></a>Testar o aplicativo

A execução do aplicativo abre o formulário e o torna pronto para assumir o parâmetro como entrada:

1. Pressione **F5** para executar o aplicativo.

2. Digite **Londres** na caixa de texto **Cidade** e clique em **FillByCity**.

     A grade de dados é preenchida com clientes que atendem aos critérios. Neste exemplo, a grade de dados exibe os clientes que têm o valor **Londres** na coluna **Cidade**.

## <a name="next-steps"></a>Próximas etapas

Dependendo dos requisitos de aplicativo, existem várias etapas que você talvez queira realizar após criar um formulário parametrizado. Entre algumas das melhorias que você poderia fazer nessa explicação passo a passo estão:

- Adicionar controles que exibem dados relacionados. Para obter mais informações, [consulte Relações em conjuntos de dados](relationships-in-datasets.md).

- Editando o conjunto de dados para adicionar ou remover objetos de banco de dados. Para obter mais informações, consulte [Create and configure datasets (Criar e configurar conjuntos de dados)](../data-tools/create-and-configure-datasets-in-visual-studio.md).

## <a name="see-also"></a>Confira também

- [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
