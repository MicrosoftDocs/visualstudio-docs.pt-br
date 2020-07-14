---
title: Salvar dados em um banco de dados (várias tabelas)
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], updating
ms.assetid: 7ebe03da-ce8c-4cbc-bac0-a2fde4ae4d07
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b512263cd5d0ca8c83b0ba6848fb16feca1a71f6
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281637"
---
# <a name="save-data-to-a-database-multiple-tables"></a>Salvar dados em um banco de dados (várias tabelas)

Um dos cenários mais comuns no desenvolvimento de aplicativos é exibir dados de um formulário em um aplicativo do Windows, editar e enviá-los atualizados de volta para o banco de dados. Essa explicação passo a passo cria um formulário que exibe dados de duas tabelas relacionadas e mostra como editar registros e salvar alterações no banco de dados. Este exemplo usa as tabelas `Customers` e `Orders` do banco de dados de exemplo Northwind.

Você pode salvar os dados em seu aplicativo de volta no banco de dados chamando o método `Update` de um TableAdapter. Quando você arrasta tabelas da janela **fontes de dados** para um formulário, o código necessário para salvar os dados é adicionado automaticamente. Todas as tabelas adicionais que são adicionadas a um formulário exigem a adição manual desse código. Essa explicação passo a passo mostra como adicionar código para salvar atualizações de mais de uma tabela.

As tarefas ilustradas neste passo a passo incluem:

- Criando e configurando uma fonte de dados em seu aplicativo com o [Assistente de configuração de fonte de dados](../data-tools/media/data-source-configuration-wizard.png).

- Definindo os controles dos itens na [janela fontes de dados](add-new-data-sources.md#data-sources-window). Para obter mais informações, consulte [definir o controle a ser criado ao arrastar da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

- Criando controles associados a dados arrastando itens da janela **Fontes de Dados** para o formulário.

- Modificar alguns registros em cada tabela no conjunto de recursos.

- Modificando o código para enviar os dados atualizados no conjunto de dados de volta ao banco de dados.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passos usa SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver SQL Server Express LocalDB, instale-o na [SQL Server Express página de download](https://www.microsoft.com/sql-server/sql-server-editions-express)ou por meio do **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte da carga de trabalho de **armazenamento e processamento de dados** ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind seguindo estas etapas:

    1. No Visual Studio, abra a janela **pesquisador de objetos do SQL Server** . (O Pesquisador de Objetos do SQL Server é instalado como parte da carga de trabalho de **armazenamento e processamento de dados** no instalador do Visual Studio.) Expanda o nó **SQL Server** . Clique com o botão direito do mouse na instância do LocalDB e selecione **nova consulta**.

       Uma janela do editor de consultas é aberta.

    2. Copie o [script do Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) para a área de transferência. Esse script T-SQL cria o banco de dados Northwind a partir do zero e o preenche com os mesmos.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o botão **executar** .

       Após um curto período, a consulta terminará de ser executada e o banco de dados Northwind será criado.

## <a name="create-the-windows-forms-application"></a>Criar o aplicativo Windows Forms

Crie um novo projeto de **aplicativo Windows Forms** para C# ou Visual Basic. Nomeie o projeto **UpdateMultipleTablesWalkthrough**.

## <a name="create-the-data-source"></a>Criar a fonte de dados

Esta etapa cria uma fonte de dados com base em um banco de dados Northwind usando o **Assistente de Configuração de Fonte de Dados**. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [How to: Install exemplo databases](../data-tools/installing-database-systems-tools-and-samples.md).

1. No menu **dados** , selecione **mostrar fontes de dados**.

   A janela **Fontes de Dados** é aberta.

2. Na janela **fontes de dados** , selecione **Adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.

3. Na tela **escolher um tipo de fonte de dados** , selecione **banco**de dado e, em seguida, selecione **Avançar**.

4. Na tela **escolher sua conexão de dados** , siga um destes procedimentos:

    - Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

         -ou-

    - Selecione **Nova Conexão** para abrir a caixa de diálogo **Adicionar/Modificar Conexão**.

5. Se o seu banco de dados exigir uma senha, selecione a opção para incluir um dado confidencial e, em seguida, selecione **Avançar**.

6. Na **cadeia de conexão salvar no arquivo de configuração do aplicativo**, selecione **Avançar**.

7. Na tela **escolher seus objetos de banco de dados** , expanda o nó **tabelas** .

8. Selecione as tabelas **Customers** e **Orders** e, em seguida, selecione **Finish**.

     O **NorthwindDataSet** é adicionado ao projeto e as tabelas são exibidas na janela **Fontes de Dados**.

## <a name="set-the-controls-to-be-created"></a>Definir os controles a serem criados

Para esta explicação, os dados na `Customers` tabela estão em um layout de **detalhes** em que os dados são exibidos em controles individuais. Os dados da `Orders` tabela estão em um layout de **grade** que é exibido em um <xref:System.Windows.Forms.DataGridView> controle.

### <a name="to-set-the-drop-type-for-the-items-in-the-data-sources-window"></a>Definir o tipo de remoção dos itens na Janela Fontes de Dados

1. Na janela **fontes de dados** , expanda o nó **clientes** .

2. No nó **clientes** , selecione **detalhes** na lista de controles para alterar o controle da tabela **Customers** para controles individuais. Para obter mais informações, consulte [definir o controle a ser criado ao arrastar da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

## <a name="create-the-data-bound-form"></a>Criar o formulário associado a dados

Você pode criar os controles associados a dados arrastando itens da janela **fontes de dados** para o formulário.

1. Arraste o nó principal **Clientes** da janela **Fontes de Dados** para **Form1**.

     Os controles de associação de dados com rótulos descritivos são exibidos no formulário, juntamente com uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para registros de navegação. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), `CustomersTableAdapter` , <xref:System.Windows.Forms.BindingSource> e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja do componente.

2. Arraste o nó **Ordens** relacionado da janela **Fontes de Dados** para **Form1**.

    > [!NOTE]
    > O nó **Ordens** relacionado está localizado abaixo da coluna **Fax** e é um nó filho do nó **Clientes**.

     Um controle <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Um `OrdersTableAdapter` e <xref:System.Windows.Forms.BindingSource> aparecem na bandeja do componente.

## <a name="add-code-to-update-the-database"></a>Adicionar código para atualizar o banco de dados

É possível atualizar os bancos de dados chamando os métodos `Update` dos TableAdapters **Clientes** e **Ordens**. Por padrão, um manipulador de eventos para o botão **salvar** do <xref:System.Windows.Forms.BindingNavigator> é adicionado ao código do formulário para enviar atualizações para o banco de dados. Esse procedimento modifica o código para enviar atualizações na ordem correta. Isso elimina a possibilidade de gerar erros de integridade referencial. O código também implementa manipulação de erros com a quebra automática da chamada de atualização em um bloco try-catch. Você pode mudar o código para atender às necessidades do seu aplicativo.

> [!NOTE]
> Para maior clareza, este passo a passos não usa uma transação. No entanto, se você estiver atualizando duas ou mais tabelas relacionadas, inclua toda a lógica de atualização em uma transação. Uma transação é um processo que garante que todas as alterações relacionadas a um banco de dados sejam bem-sucedidas antes que as alterações sejam confirmadas. Para obter mais informações, consulte [Transações e simultaneidade](/dotnet/framework/data/adonet/transactions-and-concurrency).

### <a name="to-add-update-logic-to-the-application"></a>Para adicionar lógica de atualização ao aplicativo

1. Selecione o botão **salvar** no <xref:System.Windows.Forms.BindingNavigator> . Isso abre o editor de código para o `bindingNavigatorSaveItem_Click` manipulador de eventos.

2. Substitua o código no manipulador de eventos para chamar os métodos `Update` dos TableAdapters relacionados. O código a seguir primeiro cria três tabelas de dados temporárias para armazenar as informações de cada <xref:System.Data.DataRowState> (<xref:System.Data.DataRowState.Deleted>, <xref:System.Data.DataRowState.Added> e <xref:System.Data.DataRowState.Modified>). As atualizações são executadas na ordem correta. O código deve se parecer com o seguinte:

     [!code-vb[VbRaddataSaving#10](../data-tools/codesnippet/VisualBasic/save-data-to-a-database-multiple-tables_1.vb)]
     [!code-csharp[VbRaddataSaving#10](../data-tools/codesnippet/CSharp/save-data-to-a-database-multiple-tables_1.cs)]

## <a name="test-the-application"></a>Testar o aplicativo

1. Pressione **F5**.

2. Faça algumas alterações nos dados de um ou mais registros em cada tabela.

3. Selecione o botão **Salvar**.

4. Confira os valores no banco de dados para verificar se as alterações foram salvas.

## <a name="see-also"></a>Veja também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
