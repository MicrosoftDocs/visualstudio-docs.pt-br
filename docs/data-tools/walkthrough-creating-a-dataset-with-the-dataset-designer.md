---
title: 'Instruções passo a passo: criando um conjunto de dados com o Designer de Conjunto de Dados'
ms.date: 09/11/2017
ms.topic: conceptual
helpviewer_keywords:
- datasets [Visual Basic], walkthroughs
- XML schemas, creating datasets
- data [Visual Studio], Dataset Designer
- Dataset Designer, walkthroughs
- datasets [Visual Basic], creating
author: gewarren
ms.author: gewarren
manager: douge
ms.prod: visual-studio-dev15
ms.technology: vs-data-tools
ms.workload:
- data-storage
ms.openlocfilehash: 32a093e59d918f34ddf5da9cbb5edb13c96b2777
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37117921"
---
# <a name="walkthrough-create-a-dataset-with-the-dataset-designer"></a>Passo a passo: Criar um conjunto de dados com o Designer de conjunto de dados

Neste passo a passo, você cria um conjunto de dados usando o **Dataset Designer**. O artigo o guiará durante o processo de criar um novo projeto e adicionar um novo **conjunto de dados** item a ele. Você aprenderá como criar tabelas com base em tabelas em um banco de dados sem usar um assistente.

## <a name="prerequisites"></a>Pré-requisitos

Este passo a passo usa o SQL Server Express LocalDB e o banco de dados de exemplo Northwind.

1.  Se você não tiver o SQL Server Express LocalDB, instalá-lo a partir de [página de download do SQL Server Express](https://www.microsoft.com/sql-server/sql-server-editions-express), ou por meio de **instalador do Visual Studio**. No instalador do Visual Studio, o SQL Server Express LocalDB pode ser instalado como parte dos **armazenamento de dados e processamento** carga de trabalho, ou como um componente individual.

2.  Instale o banco de dados de exemplo Northwind, seguindo estas etapas:

    1. No Visual Studio, abra o **SQL Server Object Explorer** janela. (Pesquisador de objetos do SQL Server é instalado como parte dos **armazenamento de dados e processamento** carga de trabalho no instalador do Visual Studio.) Expanda o **SQL Server** nó. Clique com botão direito na instância do LocalDB e selecione **nova consulta**.

       Abre uma janela do editor de consulta.

    2. Cópia de [script Transact-SQL Northwind](https://github.com/MicrosoftDocs/visualstudio-docs/blob/master/docs/data-tools/samples/northwind.sql?raw=true) na área de transferência. Este script T-SQL cria o banco de dados Northwind do zero e a preenche com dados.

    3. Cole o script T-SQL no editor de consultas e, em seguida, escolha o **Execute** botão.

       Após alguns instantes, a consulta termina a execução e o banco de dados Northwind é criado.

## <a name="create-a-new-windows-forms-application-project"></a>Criar um novo projeto de aplicativo do Windows Forms

1. No Visual Studio, sobre o **arquivo** menu, selecione **New** > **projeto**.

2. Expanda o **Visual c#** ou **Visual Basic** no painel esquerdo, em seguida, selecione **área de trabalho do Windows**.

3. No painel central, selecione a **aplicativo do Windows Forms** tipo de projeto.

4. Nomeie o projeto **como DatasetDesignerWalkthrough**e, em seguida, escolha **Okey**.

     O projeto para o Visual Studio adiciona **Gerenciador de soluções** e exibirá um novo formulário no designer.

## <a name="add-a-new-dataset-to-the-application"></a>Adicionar um novo conjunto de dados para o aplicativo

1.  Sobre o **Project** menu, selecione **Adicionar Novo Item**.

     A caixa de diálogo **Adicionar Novo Item** é exibida.

2.  No painel esquerdo, selecione **dados**, em seguida, selecione **conjunto de dados** no painel central.

3.  Nomeie o conjunto de dados **NorthwindDataset**e, em seguida, escolha **Add**.

     O Visual Studio adiciona um arquivo chamado **NorthwindDataSet** ao projeto e abre-o na **Dataset Designer**.

## <a name="create-a-data-connection-in-server-explorer"></a>Criar uma Conexão de dados no Gerenciador de servidores

1.  Sobre o **modo de exibição** menu, clique em **Gerenciador de servidores**.

2.  Na **Gerenciador de servidores**, clique no **conectar-se ao banco de dados** botão.

3.  Crie uma conexão ao banco de dados de exemplo Northwind.

## <a name="create-the-tables-in-the-dataset"></a>Criar as tabelas no conjunto de dados

Esta seção explica como adicionar tabelas ao conjunto de dados.

### <a name="to-create-the-customers-table"></a>Para criar a tabela Customers

1.  Expanda a conexão de dados que você criou na **Gerenciador de servidores**e, em seguida, expanda o **tabelas** nó.

2.  Arraste o **clientes** tabela de **Gerenciador de servidores** até o **Dataset Designer**.

     Um **clientes** tabela de dados e **CustomersTableAdapter** são adicionados ao conjunto de dados.

### <a name="to-create-the-orders-table"></a>Para criar a tabela Orders

-   Arraste o **pedidos** tabela de **Gerenciador de servidores** para o **Dataset Designer**.

     Uma **pedidos** tabela de dados, **OrdersTableAdapter**e a relação de dados entre o **clientes** e **pedidos** tabelas são adicionadas à conjunto de dados.

### <a name="to-create-the-orderdetails-table"></a>Para criar a tabela OrderDetails

-   Arraste o **detalhes do pedido** tabela de **Gerenciador de servidores** até o **Dataset Designer**.

     Uma **detalhes do pedido** tabela de dados **OrderDetailsTableAdapter**e uma relação de dados entre o **pedidos** e **OrderDetails** tabelas são adicionadas ao conjunto de dados.

## <a name="next-steps"></a>Próximas etapas

-   Salve o conjunto de dados.

-   Selecione os itens na **fontes de dados** janela e arrastá-los para um formulário. Para obter mais informações, consulte [controles de ligar o Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md).

-   Adicione mais consultas para os TableAdapters.

-   Adicionar lógica de validação para o <xref:System.Data.DataTable.ColumnChanging> ou <xref:System.Data.DataTable.RowChanging> eventos das tabelas de dados no conjunto de dados. Para obter mais informações, consulte [validar dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md).

## <a name="see-also"></a>Consulte também

- [Criar e configurar conjuntos de dados no Visual Studio](../data-tools/create-and-configure-datasets-in-visual-studio.md)
- [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)
- [Validar dados](../data-tools/validate-data-in-datasets.md)