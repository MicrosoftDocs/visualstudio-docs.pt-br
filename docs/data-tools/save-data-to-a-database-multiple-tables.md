---
title: Salvar dados em um banco de dados (várias tabelas)
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- updating datasets, walkthroughs
- data [Visual Studio], saving
- saving data, walkthroughs
- data [Visual Studio], updating
ms.assetid: 7ebe03da-ce8c-4cbc-bac0-a2fde4ae4d07
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: c4e5ca1e9903089cbcc9daf99e8c8d49d170b1c8
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52388803"
---
# <a name="save-data-to-a-database-multiple-tables"></a>Salvar dados em um banco de dados (várias tabelas)

Um dos cenários mais comuns no desenvolvimento de aplicativos é exibir dados de um formulário em um aplicativo do Windows, editar e enviá-los atualizados de volta para o banco de dados. Essa explicação passo a passo cria um formulário que exibe dados de duas tabelas relacionadas e mostra como editar registros e salvar alterações no banco de dados. Este exemplo usa as tabelas `Customers` e `Orders` do banco de dados de exemplo Northwind.

Você pode salvar os dados em seu aplicativo de volta no banco de dados chamando o método `Update` de um TableAdapter. Quando você arrasta tabelas do **fontes de dados** janela em um formulário, o código necessário para salvar dados é adicionada automaticamente. Quaisquer tabelas adicionais que são adicionadas a um formulário exigem a adição manual desse código. Essa explicação passo a passo mostra como adicionar código para salvar atualizações de mais de uma tabela.

As tarefas ilustradas neste passo a passo incluem:

-   Criando um novo **aplicativo do Windows Forms** projeto.

-   Criando e configurando uma fonte de dados em seu aplicativo com o [Data Source Configuration Wizard](../data-tools/media/data-source-configuration-wizard.png).

-   Configurando os controles dos itens na [janela Data Sources](add-new-data-sources.md#data-sources-window). Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

-   Criando controles associados a dados arrastando itens da janela Fontes de Dados** para o formulário.

-   Modificando alguns registros em cada tabela no conjunto de dados.

-   Modificando o código para enviar os dados atualizados no conjunto de dados de volta ao banco de dados.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1. Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No **instalador do Visual Studio**, você pode instalar o SQL Server Express LocalDB como parte do **armazenamento de dados e processamento** carga de trabalho, ou como um componente individual.

2. Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (Pesquisador de objetos do SQL Server é instalado como parte dos **armazenamento de dados e processamento** carga de trabalho no instalador do Visual Studio.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    2. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="create-the-windows-forms-application"></a>Criar o aplicativo do Windows Forms

A primeira etapa é criar uma **aplicativo do Windows Forms**. Atribuir um nome para o projeto é opcional durante esta etapa, mas vamos dar a ele um nome de nós será salvar o projeto mais tarde.

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

4. Nomeie o projeto **UpdateMultipleTablesWalkthrough**e, em seguida, escolha **Okey**.

     O projeto UpdateMultipleTablesWalkthrough **é criado e adicionado ao Gerenciador de Soluções**.

## <a name="create-the-data-source"></a>Criar a fonte de dados

Esta etapa cria uma fonte de dados a partir de um banco de dados Northwind usando o Assistente de Configuração de Fonte de Dados **. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [como: instalar bancos de dados de exemplo](../data-tools/installing-database-systems-tools-and-samples.md).

1. Sobre o **dados** menu, selecione **Show Data Sources**.

   A janela Fontes de Dados** é aberta.

2. Na janela Fontes de Dados **, selecione Adicionar Nova Fonte de Dados** para iniciar o Assistente de Configuração de Fonte de Dados **.

3. Sobre o **escolher um tipo de fonte de dados** tela, selecione **banco de dados**e, em seguida, selecione **próxima**.

4. Sobre o **escolha sua Conexão de dados** tela, siga um destes procedimentos:

    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.

         -ou-

    -   Selecione Nova Conexão **para abrir a caixa de diálogo Adicionar/Modificar Conexão**.

5. Se seu banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, selecione **próxima**.

6. Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo**, selecione **próxima**.

7. Sobre o **Choose your Database Objects** , expanda o **tabelas** nó.

8. Selecione o **clientes** e **pedidos** tabelas e, em seguida, selecione **concluir**.

     O NorthwindDataSet **é adicionado ao projeto e as tabelas são exibidas na janela Fontes de Dados**.

## <a name="set-the-controls-to-be-created"></a>Defina os controles a serem criados

Para este passo a passo, os dados na `Customers` a tabela está em um **detalhes** layout onde os dados são exibidos em controles individuais. Os dados do `Orders` a tabela está em um **grade** layout que é exibido em um <xref:System.Windows.Forms.DataGridView> controle.

### <a name="to-set-the-drop-type-for-the-items-in-the-data-sources-window"></a>Definir o tipo de remoção dos itens na Janela Fontes de Dados

1. No **fontes de dados** janela, expanda o **clientes** nó.

2. Sobre o **clientes** nó, selecione **detalhes** na lista de controle para alterar o controle do **clientes** tabela para controles individuais. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).

## <a name="create-the-data-bound-form"></a>Criar o formulário de associação de dados

Você pode criar controles de associação de dados arrastando itens da janela Fontes de Dados** para um formulário.

1. Arraste o nó principal Clientes **da janela Fontes de Dados** para Form1.

     Os controles de associação de dados com rótulos descritivos são exibidos no formulário, juntamente com uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para registros de navegação. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), `CustomersTableAdapter`, <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.

2. Arraste o nó Ordens **relacionado da janela Fontes de Dados** para Form1 **.

    > [!NOTE]
    > O nó Ordens **relacionado está localizado abaixo da coluna Fax** e é um nó filho do nó Clientes **.

     Um controle <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Uma `OrdersTableAdapter` e <xref:System.Windows.Forms.BindingSource> aparecem na bandeja de componentes.

## <a name="add-code-to-update-the-database"></a>Adicione código para atualizar o banco de dados

É possível atualizar os bancos de dados chamando os métodos `Update` dos TableAdapters Clientes **e Ordens**. Por padrão, um manipulador de eventos para o **salve** botão do<xref:System.Windows.Forms.BindingNavigator> é adicionado ao código do formulário para enviar atualizações para o banco de dados. Este procedimento modifica o código para enviar atualizações na ordem correta. Isso elimina a possibilidade de gerar erros de integridade referencial. O código também implementa manipulação de erros com a quebra automática da chamada de atualização em um bloco try-catch. Você pode mudar o código para atender às necessidades do seu aplicativo.

> [!NOTE]
> Para maior clareza, este passo a passo não usa uma transação. No entanto, se você estiver atualizando dois ou mais tabelas relacionadas, inclua toda a lógica de atualização dentro de uma transação. Uma transação é um processo que garante que todas as alterações relacionadas a um banco de dados são bem-sucedidas antes que as alterações sejam confirmadas. Para obter mais informações, consulte [transações e simultaneidade](/dotnet/framework/data/adonet/transactions-and-concurrency).

### <a name="to-add-update-logic-to-the-application"></a>Para adicionar lógica de atualização ao aplicativo

1. Selecione o **salve** botão o <xref:System.Windows.Forms.BindingNavigator>. Isso abre o Editor de códigos para o `bindingNavigatorSaveItem_Click` manipulador de eventos.

2. Substitua o código no manipulador de eventos para chamar os métodos `Update` dos TableAdapters relacionados. O código a seguir primeiro cria três tabelas de dados temporárias para armazenar as informações de cada <xref:System.Data.DataRowState> (<xref:System.Data.DataRowState.Deleted>, <xref:System.Data.DataRowState.Added> e <xref:System.Data.DataRowState.Modified>). As atualizações são executadas na ordem correta. O código deve se parecer com o seguinte:

     [!code-vb[VbRaddataSaving#10](../data-tools/codesnippet/VisualBasic/save-data-to-a-database-multiple-tables_1.vb)]
     [!code-csharp[VbRaddataSaving#10](../data-tools/codesnippet/CSharp/save-data-to-a-database-multiple-tables_1.cs)]

## <a name="test-the-application"></a>Testar o aplicativo

1. Pressione **F5**.

2. Faça algumas alterações nos dados de um ou mais registros em cada tabela.

3. Selecione o **salvar** botão.

4. Confira os valores no banco de dados para verificar se as alterações foram salvas.

## <a name="see-also"></a>Consulte também

- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)