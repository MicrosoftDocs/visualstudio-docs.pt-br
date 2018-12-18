---
title: Passar dados entre formulários
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- walkthroughs [Windows Forms], data
- walkthroughs [Visual Studio], data
- data [Visual Studio], passing between forms
- forms, passing data between
- Windows Forms, walkthroughs
ms.assetid: 78bf038b-9296-4fbf-b0e8-d881d1aff0df
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 4a0d248f59754d3f46e8fab0e0924c36a80b0d89
ms.sourcegitcommit: 81e9d90843ead658bc73b30c869f25921d99e116
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2018
ms.locfileid: "52305540"
---
# <a name="pass-data-between-forms"></a>Passar dados entre formulários

Este passo a passo fornece instruções detalhadas de como passar os dados de um formulário para outro. Usando as tabelas customers e orders do Northwind, um formulário que os usuários selecionem um cliente e um segundo formulário exibe os pedidos do cliente selecionado. Este passo a passo mostra como criar um método no segundo formulário que recebe dados do primeiro formulário.

> [!NOTE]
> Este passo a passo demonstra apenas uma maneira de passar dados entre formulários. Há outras opções para passar dados para um formulário, incluindo a criação de um segundo construtor para receber dados, ou criando uma propriedade pública que pode ser definida com os dados do primeiro formulário.

As tarefas ilustradas neste passo a passo incluem:

-   Criando um novo **aplicativo do Windows Forms** projeto.

-   Criando e configurando um conjunto de dados com o [Data Source Configuration Wizard](../data-tools/media/data-source-configuration-wizard.png).

-   Selecionando o controle a ser criado no formulário ao arrastar itens da janela **Fontes de Dados**. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

-   Criar controles associados a dados arrastando itens da janela **Fontes de Dados** para um formulário.

-   Criar um segundo formulário com uma grade para exibir dados.

-   Criar uma consulta TableAdapter para buscar pedidos de um cliente específico.

-   Passar dados entre formulários.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1.  Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No instalador do Visual Studio, o SQL Server Express LocalDB pode ser instalado como parte dos **armazenamento de dados e processamento** carga de trabalho, ou como um componente individual.

2.  Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (Pesquisador de objetos do SQL Server é instalado como parte dos **armazenamento de dados e processamento** carga de trabalho no instalador do Visual Studio.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    2. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="create-the-windows-forms-app-project"></a>Criar o projeto de aplicativo do Windows Forms

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

4. Nomeie o projeto **PassingDataBetweenForms**e, em seguida, escolha **Okey**.

     O projeto **PassingDataBetweenForms** é criado e adicionado ao **Gerenciador de Soluções**.

## <a name="create-the-data-source"></a>Criar a fonte de dados

1.  Para abrir o **fontes de dados** janela diante de **dados** menu, clique em **Mostrar fontes de dados**.

2.  Na janela **Fontes de Dados**, selecione **Adicionar Nova Fonte de Dados** para iniciar o assistente de **Configuração de Fonte de Dados**.

3.  Selecione **Banco de Dados** na página **Escolher um Tipo de Fonte de Dados** e, em seguida, clique em **Avançar**.

4.  Na página **Escolha um Modelo de Banco de Dados**, verifique se o **Conjunto de dados** foi especificado e clique em **Avançar**.

5.  Na página **Escolha a Conexão de Dados**, faça o seguinte:

    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

    -   Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão**.

6.  Se o banco de dados exigir uma senha e a opção para incluir dados confidenciais estiver habilitada, clique em **Avançar**.

7.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** , clique em **próxima**.

8.  Sobre o **Choose your Database Objects** página, expanda o **tabelas** nó.

9. Selecione as tabelas **Customers** e **Orders** e, em seguida, clique em **Finalizar**.

     O **NorthwindDataSet** é adicionado ao projeto e as tabelas **Customers** e **Orders** aparecem na janela **Fontes de Dados**.

## <a name="create-the-first-form-form1"></a>Criar o primeiro formulário (Form1)

Você pode criar uma grade de associação de dados (um controle <xref:System.Windows.Forms.DataGridView>), arrastando o nó **Clientes** da janela **Fontes de Dados** para o formulário.

### <a name="to-create-a-data-bound-grid-on-the-form"></a>Para criar uma grade de associação de dados no formulário

-   Arraste o nó principal **Clientes** da janela **Fontes de Dados** para **Form1**.

     Um <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no **Form1**. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), CustomersTableAdapter, <xref:System.Windows.Forms.BindingSource> e <xref:System.Windows.Forms.BindingNavigator> são exibidos na bandeja de componentes.

## <a name="create-the-second-form"></a>Criar o segundo formulário

Crie um segundo formulário para passar dados.

1.  No menu **Projeto**, escolha **Adicionar Formulário do Windows**.

2.  Deixe o nome padrão **Form2** e clique em **Adicionar**.

3.  Arraste o nó principal **Pedidos** da janela **Fontes de Dados** para **Form2**.

     Um <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no **Form2**. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), CustomersTableAdapter, <xref:System.Windows.Forms.BindingSource> e <xref:System.Windows.Forms.BindingNavigator> são exibidos na bandeja de componentes.

4.  Exclua o **OrdersBindingNavigator** da bandeja de componentes.

     O **OrdersBindingNavigator** desaparece do **Form2**.

## <a name="add-a-tableadapter-query"></a>Adicionar uma consulta do TableAdapter

Adicione uma consulta TableAdapter ao Form2 para carregar pedidos do cliente selecionado no Form1.

1.  Clique duas vezes no arquivo **NorthwindDataSet.xsd** no **Gerenciador de Soluções**.

2.  Clique com o botão direito do mouse no **OrdersTableAdapter** e selecione **Adicionar Consulta**.

3.  Deixe a opção padrão **Usar instruções SQL** e clique em **Avançar**.

4.  Deixe a opção padrão **SELECT que retorna linhas** e clique em **Avançar**.

5.  Adicione uma cláusula WHERE à consulta para retornar `Orders` com base no `CustomerID`. A consulta deve ser semelhante ao seguinte:

    ```sql
    SELECT OrderID, CustomerID, EmployeeID, OrderDate, RequiredDate, ShippedDate, ShipVia, Freight, ShipName, ShipAddress, ShipCity, ShipRegion, ShipPostalCode, ShipCountry
    FROM Orders
    WHERE CustomerID = @CustomerID
    ```

    > [!NOTE]
    > Verifique a sintaxe de parâmetro correta para o seu banco de dados. Por exemplo, no Microsoft Access, a cláusula WHERE seria algo como: `WHERE CustomerID = ?`.

6.  Clique em **Avançar**.

7.  Para o **preencha um nome de DataTableMethod**, tipo `FillByCustomerID`.

8.  Desmarque a opção **Retornar uma DataTable** e clique em **Avançar**.

9. Clique em **Finalizar**.

## <a name="create-a-method-on-form2-to-pass-data-to"></a>Criar um método no Form2 para passar dados para

1.  Clique com o botão direito do mouse no **Form2** e selecione **Exibir Código** para abrir o **Form2** no **Editor de Códigos**.

2.  Adicione o seguinte código ao **Form2** depois do método `Form2_Load`:

     [!code-vb[VbRaddataDisplaying#1](../data-tools/codesnippet/VisualBasic/pass-data-between-forms_1.vb)]
     [!code-csharp[VbRaddataDisplaying#1](../data-tools/codesnippet/CSharp/pass-data-between-forms_1.cs)]

## <a name="create-a-method-on-form1-to-pass-data-and-display-form2"></a>Criar um método no Form1 para passar dados e exibir o Form2

1.  No **Form1**, clique com o botão direito do mouse na grade de dados do Cliente e clique em **Propriedades**.

2.  Na janela **Propriedades**, clique em **Eventos**.

3.  Clique duas vezes no evento **CellDoubleClick**.

     O Editor de Códigos é exibido.

4.  Atualize a definição de método para corresponder ao seguinte exemplo:

     [!code-csharp[VbRaddataDisplaying#2](../data-tools/codesnippet/CSharp/pass-data-between-forms_2.cs)]
     [!code-vb[VbRaddataDisplaying#2](../data-tools/codesnippet/VisualBasic/pass-data-between-forms_2.vb)]

## <a name="run-the-app"></a>Executar o aplicativo

-   Pressione **F5** para executar o aplicativo.

-   Clique duas vezes em um registro de cliente no **Form1** para abrir o **Form2** com pedidos do cliente.

## <a name="next-steps"></a>Próximas etapas

Dependendo dos requisitos de aplicativo, existem várias etapas que você talvez queira realizar após passar dados entre formulários. Entre algumas das melhorias que você poderia fazer nessa explicação passo a passo estão:

-   Editando o conjunto de dados para adicionar ou remover objetos de banco de dados. Para obter mais informações, consulte [Create and configure datasets (Criar e configurar conjuntos de dados)](../data-tools/create-and-configure-datasets-in-visual-studio.md).

-   Adicionar funcionalidade para salvar dados de volta no banco de dados. Para obter mais informações, consulte [salvar dados no banco de dados](../data-tools/save-data-back-to-the-database.md).

## <a name="see-also"></a>Consulte também

- [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)