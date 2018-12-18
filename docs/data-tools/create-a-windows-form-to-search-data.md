---
title: Criar um Windows Form para pesquisar dados
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Windows Forms, searching data
- Windows Forms, displaying data
- parameters, displaying filtered data
- data [Visual Studio], parameterizing queries
- data [Visual Studio], searching
ms.assetid: 65ca79a9-7458-466c-af55-978cd24c549e
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 15cfd136050d9a0e3fca89964c5a9712b7b5ae06
ms.sourcegitcommit: 0cdd8e8a53fb4fd5e869f07c35204419fa12783d
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2018
ms.locfileid: "53159887"
---
# <a name="create-a-windows-form-to-search-data"></a>Criar um Windows Form para pesquisar dados

Um cenário de aplicativo comum exibirá dados selecionados em um formulário. Por exemplo, você pode querer exibir os pedidos de um cliente específico ou os detalhes de um pedido específico. Nesse cenário, um usuário insere informações em um formulário e uma consulta é executada com a entrada do usuário como parâmetro, ou seja, os dados são selecionados com base em uma consulta parametrizada. A consulta retorna apenas os dados que satisfazem os critérios inseridos pelo usuário. Este passo a passo mostra como criar uma consulta que retorna clientes de uma cidade específica, como mudar a interface do usuário para que os usuários possam inserir o nome de uma cidade e pressionar um botão para executar a consulta.

O uso de consultas parametrizadas ajuda a tornar seu aplicativo eficiente, permitindo que o banco de dados funcione melhor, filtrando registros rapidamente. Por outro lado, se você solicitar uma tabela de banco de dados inteira, transferi-la pela rede e usar a lógica do aplicativo para encontrar os registros que deseja, o aplicativo poderá ficar lento e ineficiente.

Você pode adicionar consultas parametrizadas a qualquer TableAdapter (e controles para aceitar valores de parâmetro e executar a consulta), usando o **construtor de critérios de pesquisa** caixa de diálogo. Abra a caixa de diálogo selecionando o comando **Adicionar Consulta** no menu **Dados** (ou em qualquer marcação inteligente de TableAdapter).

As tarefas ilustradas neste passo a passo incluem:

-   Criando um novo **aplicativo do Windows Forms** projeto.

-   Criando e configurando a fonte de dados em seu aplicativo com o **configuração de fonte de dados** assistente.

-   Definição do tipo subjacente dos itens na **fontes de dados** janela.

-   Criar controles que exibem dados arrastando itens da janela **Fontes de Dados** para um formulário.

-   Adicionar controles para exibir os dados no formulário.

-   Concluindo a **construtor de critérios de pesquisa** caixa de diálogo.

-   Inserir parâmetros no formulário e executar a consulta parametrizada.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1.  Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte do **armazenamento de dados e processamento** carga de trabalho, ou como um componente individual.

2.  Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (Pesquisador de objetos do SQL Server é instalado como parte dos **armazenamento de dados e processamento** carga de trabalho na **instalador do Visual Studio**.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    2. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="create-the-windows-forms-application"></a>Criar o aplicativo do Windows Forms

A primeira etapa é criar um aplicativo Windows Forms. Atribuir um nome para o projeto é opcional nesta etapa, mas você dar a ele um nome aqui porque você salvará o projeto mais tarde:

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

4. Nomeie o projeto **WindowsSearchForm**e, em seguida, escolha **Okey**.

     O projeto **WindowsSearchForm** é criado e adicionado ao **Gerenciador de Soluções**.

## <a name="create-the-data-source"></a>Criar a fonte de dados

Esta etapa cria uma fonte de dados por meio de um banco de dados usando o assistente de **Configuração de Fonte de Dados**:

1.  Para abrir o **fontes de dados** janela diante de **dados** menu, clique em **Mostrar fontes de dados**.

2.  Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o assistente de **Configuração de Fonte de Dados**.

3.  Selecione **Banco de Dados** na página **Escolher um Tipo de Fonte de Dados** e, em seguida, clique em **Avançar**.

4.  Na página **Escolha a Conexão de Dados**, faça o seguinte:

    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

    -   Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

5.  Se o banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **Avançar**.

6.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** , clique em **próxima**.

7.  Sobre o **Choose your Database Objects** página, expanda o **tabelas** nó.

8.  Selecione a tabela **Clientes** e clique em **Concluir**.

     O **NorthwindDataSet** é adicionado ao seu projeto e a tabela **Clientes** aparece na janela **Fontes de Dados**.

## <a name="create-the-form"></a>Criar o formulário

Você pode criar controles de associação de dados arrastando itens da janela **Fontes de Dados** para um formulário:

1.  Expanda o nó **Clientes** na janela **Fontes de Dados**.

2.  Arraste o nó **Clientes** da janela **Fontes de Dados** para o formulário.

     Um <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), CustomersTableAdapter, <xref:System.Windows.Forms.BindingSource> e <xref:System.Windows.Forms.BindingNavigator> são exibidos na bandeja de componentes.

## <a name="add-parameterization-search-functionality-to-the-query"></a>Adicionar parametrização (funcionalidade Pesquisar) à consulta

Você pode adicionar uma cláusula WHERE à consulta original usando o **construtor de critérios de pesquisa** caixa de diálogo:

1.  Selecione o controle <xref:System.Windows.Forms.DataGridView> e escolha **Adicionar Consulta** no menu **Dados**.

2.  Tipo de **FillByCity** na **nome da nova consulta** área na **Pesquisar Construtor de critérios** caixa de diálogo.

3.  Adicione `WHERE City = @City` à consulta na área **Texto da Consulta**.

     A consulta deve ser semelhante ao seguinte:

     ```sql
     SELECT CustomerID, CompanyName, ContactName, ContactTitle,
          Address, City, Region, PostalCode, Country, Phone, Fax
     FROM Customers
     WHERE City = @City
     ```

    > [!NOTE]
    > Fontes de dados do Access e o OLE DB usam o ponto de interrogação ('? ') para denotar parâmetros, portanto, a cláusula WHERE seria algo como este: `WHERE City = ?`.

4.  Clique em **OK** para fechar a caixa de diálogo **Construtor de Critérios de Pesquisa**.

     Um **FillByCityToolStrip** é adicionado ao formulário.

## <a name="test-the-application"></a>Testar o aplicativo

Executando o aplicativo abre o formulário e o torna pronto para receber o parâmetro como entrada:

1.  Pressione **F5** para executar o aplicativo.

2.  Digite **Londres** na caixa de texto **Cidade** e clique em **FillByCity**.

     A grade de dados é preenchida com os clientes que atendem aos critérios. Neste exemplo, a grade de dados exibe os clientes que têm o valor **Londres** na coluna **Cidade**.

## <a name="next-steps"></a>Próximas etapas

Dependendo dos requisitos de aplicativo, existem várias etapas que você talvez queira realizar após criar um formulário parametrizado. Entre algumas das melhorias que você poderia fazer nessa explicação passo a passo estão:

-   Adicionar controles que exibem dados relacionados. Para obter mais informações, consulte [relacionamentos em conjuntos de dados](relationships-in-datasets.md).

-   Editando o conjunto de dados para adicionar ou remover objetos de banco de dados. Para obter mais informações, consulte [Create and configure datasets (Criar e configurar conjuntos de dados)](../data-tools/create-and-configure-datasets-in-visual-studio.md).

## <a name="see-also"></a>Consulte também

- [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
