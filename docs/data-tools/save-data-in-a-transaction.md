---
title: 'Passo a passo: salvar dados em uma transação'
ms.date: 09/08/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- System.Transactions namespace
- data [Visual Studio], saving in a transaction
- transactions, saving data
- Transactions namespace
- saving data
ms.assetid: 80260118-08bc-4b37-bfe5-9422ee7a1e4e
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: caeb06ac3f38293b493463ff456e222f148ef93a
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281624"
---
# <a name="walkthrough-save-data-in-a-transaction"></a>Passo a passo: salvar dados em uma transação

Este tutorial demonstra como salvar dados em uma transação usando o <xref:System.Transactions> namespace. Neste tutorial, você criará um aplicativo Windows Forms. Você usará o assistente de configuração de fonte de dados para criar um conjunto de dado para duas tabelas no banco de dados de exemplo Northwind. Você adicionará controles associados a dados a um Windows Form e modificará o código para o botão salvar do BindingNavigator para atualizar o banco de dados dentro de um TransactionScope.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passos usa SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver SQL Server Express LocalDB, instale-o na [SQL Server Express página de download](https://www.microsoft.com/sql-server/sql-server-editions-express)ou por meio do **instalador do Visual Studio**. No Instalador do Visual Studio, o SQL Server Express LocalDB pode ser instalado como parte da carga de **trabalho de desenvolvimento da área de trabalho do .net** ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind seguindo estas etapas:

    1. No Visual Studio, abra a janela **pesquisador de objetos do SQL Server** . (O Pesquisador de Objetos do SQL Server é instalado como parte da carga de trabalho de **armazenamento e processamento de dados** no instalador do Visual Studio.) Expanda o nó **SQL Server** . Clique com o botão direito do mouse na instância do LocalDB e selecione **nova consulta**.

       Uma janela do editor de consultas é aberta.

    2. Copie o [script do Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) para a área de transferência. Esse script T-SQL cria o banco de dados Northwind a partir do zero e o preenche com os mesmos.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o botão **executar** .

       Após um curto período, a consulta terminará de ser executada e o banco de dados Northwind será criado.

## <a name="create-a-windows-forms-application"></a>Criar um aplicativo do Windows Forms

A primeira etapa é criar um **aplicativo Windows Forms**.

1. No Visual Studio, no menu **Arquivo**, selecione **Novo** > **Projeto**.

2. Expanda o **Visual C#** ou **Visual Basic** no painel esquerdo e, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione o tipo de projeto **Windows Forms aplicativo** .

4. Nomeie o projeto **SavingDataInATransactionWalkthrough**e escolha **OK**.

     O projeto **SavingDataInATransactionWalkthrough** é criado e adicionado ao **Gerenciador de Soluções**.

## <a name="create-a-database-data-source"></a>Criar uma fonte de dados de banco

Esta etapa usa o **Assistente de configuração de fonte de dados** para criar uma fonte de dados com base nas `Customers` `Orders` tabelas e no banco de dados de exemplo Northwind.

1. Para abrir a janela **fontes de dados** , no menu **dados** , selecione **mostrar fontes de dados**.

2. Na janela **fontes de dados** , selecione **Adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.

3. Na tela **escolher um tipo de fonte de dados** , selecione **banco**de dado e, em seguida, selecione **Avançar**.

4. Na tela **escolher sua conexão de dados** , siga um destes procedimentos:

    - Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

         -ou-

    - Selecione **Nova Conexão** para inicializar a caixa de diálogo **Adicionar/Modificar Conexão** e criar uma conexão com o banco de dados Northwind.

5. Se o seu banco de dados exigir uma senha, selecione a opção para incluir um dado confidencial e, em seguida, selecione **Avançar**.

6. Na tela **salvar cadeia de conexão no arquivo de configuração do aplicativo** , selecione **Avançar**.

7. Na tela **escolher seus objetos de banco de dados** , expanda o nó **tabelas** .

8. Selecione as `Customers` tabelas e e `Orders` , em seguida, selecione **concluir**.

     O **NorthwindDataSet** é adicionado ao projeto e as tabelas `Customers` e `Orders` aparecem na janela **Fontes de Dados**.

## <a name="add-controls-to-the-form"></a>Adicionar controles ao formulário

Você pode criar os controles associados a dados arrastando itens da janela **fontes de dados** para o formulário.

1. Na janela **fontes de dados** , expanda o nó **clientes** .

2. Arraste o nó principal **Clientes** da janela **Fontes de Dados** para **Form1**.

   Um controle <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), `CustomersTableAdapter` , <xref:System.Windows.Forms.BindingSource> e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja do componente.

3. Arraste o nó **pedidos** relacionados (não o nó **pedidos** principais, mas o nó de tabela filho relacionado abaixo da coluna **fax** ) no formulário abaixo do **customersDataGridView**.

   Um <xref:System.Windows.Forms.DataGridView> aparece no formulário. Um `OrdersTableAdapter` e <xref:System.Windows.Forms.BindingSource> aparecem na bandeja do componente.

## <a name="add-a-reference-to-the-systemtransactions-assembly"></a>Adicionar uma referência ao assembly System. Transactions

As transações usam o namespace <xref:System.Transactions>. Uma referência do projeto ao assembly system.transactions não é adicionada por padrão, portanto, você precisa adicioná-la manualmente.

### <a name="to-add-a-reference-to-the-systemtransactions-dll-file"></a>Para adicionar uma referência ao arquivo DLL System.Transactions

1. No menu **Projeto**, selecione **Adicionar Referência**.

2. Selecione **System. Transactions** (na guia **.net** ) e, em seguida, selecione **OK**.

     Uma referência a **System.Transactions** é adicionada ao projeto.

## <a name="modify-the-code-in-the-bindingnavigators-saveitem-button"></a>Modificar o código no botão SaveItem do BindingNavigator

Para a primeira tabela descartada em seu formulário, o código é adicionado por padrão ao `click` evento do botão salvar no <xref:System.Windows.Forms.BindingNavigator> . É necessário adicionar manualmente o código para atualizar quaisquer tabelas adicionais. Para esta explicação, refatoro o código de salvamento existente do manipulador de eventos de clique do botão salvar. Também criamos mais alguns métodos para fornecer uma funcionalidade de atualização específica com base em se a linha precisa ser adicionada ou excluída.

### <a name="to-modify-the-auto-generated-save-code"></a>Para modificar o código salvar gerado automaticamente

1. Selecione o botão **salvar** no **CustomersBindingNavigator** (o botão com o ícone de disquete).

2. Substitua o método `CustomersBindingNavigatorSaveItem_Click` pelo seguinte código:

     [!code-vb[VbRaddataSaving#4](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_1.vb)]
     [!code-csharp[VbRaddataSaving#4](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_1.cs)]

A ordem para reconciliar as alterações aos dados relacionados é a seguinte:

- Excluir registros filho. (Nesse caso, exclua os registros da `Orders` tabela.)

- Excluir registros pai. (Nesse caso, exclua os registros da `Customers` tabela.)

- Inserir registros pai. (Nesse caso, insira registros na `Customers` tabela.)

- Inserir registros filho. (Nesse caso, insira registros na `Orders` tabela.)

### <a name="to-delete-existing-orders"></a>Para excluir pedidos existentes

- Adicione o seguinte método `DeleteOrders` a **Form1**:

     [!code-vb[VbRaddataSaving#5](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_2.vb)]
     [!code-csharp[VbRaddataSaving#5](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_2.cs)]

### <a name="to-delete-existing-customers"></a>Para excluir clientes existentes

- Adicione o seguinte método `DeleteCustomers` a **Form1**:

     [!code-vb[VbRaddataSaving#6](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_3.vb)]
     [!code-csharp[VbRaddataSaving#6](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_3.cs)]

### <a name="to-add-new-customers"></a>Para adicionar novos clientes

- Adicione o seguinte método `AddNewCustomers` a **Form1**:

     [!code-vb[VbRaddataSaving#7](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_4.vb)]
     [!code-csharp[VbRaddataSaving#7](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_4.cs)]

### <a name="to-add-new-orders"></a>Para adicionar novos pedidos

- Adicione o seguinte método `AddNewOrders` a **Form1**:

     [!code-vb[VbRaddataSaving#8](../data-tools/codesnippet/VisualBasic/save-data-in-a-transaction_5.vb)]
     [!code-csharp[VbRaddataSaving#8](../data-tools/codesnippet/CSharp/save-data-in-a-transaction_5.cs)]

## <a name="run-the-application"></a>Executar o aplicativo

Pressione **F5** para executar o aplicativo.

## <a name="see-also"></a>Veja também

- [Como salvar dados usando uma transação](../data-tools/save-data-by-using-a-transaction.md)
- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
