---
title: 'Passo a passo: Criando um conjunto de dados com o Designer de conjunto de dados | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- datasets [Visual Basic], walkthroughs
- XML schemas, creating datasets
- data [Visual Studio], Dataset Designer
- Dataset Designer, walkthroughs
- datasets [Visual Basic], creating
ms.assetid: 12360f54-db6c-45d2-a91f-fee43214b555
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: d77d63cc82b7af6281183b3eae67d09b0454fffb
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49868255"
---
# <a name="walkthrough-creating-a-dataset-with-the-dataset-designer"></a>Instruções passo a passo: criando um conjunto de dados com o Designer de Conjunto de Dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Neste passo a passo, você irá criar um conjunto de dados usando o **Dataset Designer**. Ela levará você pelo processo de criação de um novo projeto e adicionando um novo **conjunto de dados** item a ele. Você aprenderá como criar tabelas com base em tabelas em um banco de dados sem usar um assistente.  
  
 As tarefas ilustradas neste passo a passo incluem:  
  
- Criando um novo **aplicativo do Windows** projeto.  
  
- Adicionando um vazio **conjunto de dados** item ao projeto.  
  
- Criar e configurar uma fonte de dados em seu aplicativo, criando um dataset com o **Dataset Designer**.  
  
- Criando uma conexão para o banco de dados Northwind **Gerenciador de servidores**.  
  
- Criando tabelas com TableAdapters no conjunto de dados com base em tabelas no banco de dados.  
  
  [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind (versão SQL Server ou Access). Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="creating-a-new-windows-application-project"></a>Criar um novo projeto de aplicativo do Windows  
  
#### <a name="to-create-a-new-windows-application-project"></a>Para criar um novo projeto de Aplicativo do Windows  
  
1.  Dos **arquivo** menu, crie um novo projeto.  
  
2.  Escolha uma linguagem de programação a **tipos de projeto** painel.  
  
3.  Clique em **aplicativo do Windows** na **modelos** painel.  
  
4.  Nomeie o projeto `DatasetDesignerWalkthrough`e, em seguida, clique em **Okey**.  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Adicionar o projeto para **Gerenciador de soluções** e exibirá um novo formulário no designer.  
  
## <a name="adding-a-new-dataset-to-the-application"></a>Adicionando um novo conjunto de dados para o aplicativo  
  
#### <a name="to-add-a-new-dataset-item-to-the-project"></a>Para adicionar um novo item de conjunto de dados ao projeto  
  
1.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
     A caixa de diálogo **Adicionar Novo Item** é exibida.  
  
2.  No **modelos** caixa da **Adicionar Novo Item** caixa de diálogo, clique em **conjunto de dados**.  
  
3.  Nomeie o conjunto de dados `NorthwindDataset`e, em seguida, clique em **Add**.  
  
     [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Adiciona um arquivo chamado **NorthwindDataSet** ao projeto e abri-lo na **Dataset Designer**.  
  
## <a name="creating-a-data-connection-in-server-explorer"></a>Criando uma Conexão de dados no Gerenciador de servidores  
  
#### <a name="to-create-a-connection-to-the-northwind-database"></a>Para criar uma conexão ao banco de dados Northwind  
  
1.  Sobre o **modo de exibição** menu, clique em **Gerenciador de servidores**.  
  
2.  Na **Gerenciador de servidores**, clique no **conectar-se ao banco de dados** botão.  
  
3.  Crie uma conexão ao banco de dados de exemplo Northwind.  
  
    > [!NOTE]
    >  Você pode conectar-se para a versão SQL Server ou Access do Northwind para este passo a passo.  
  
## <a name="creating-the-tables-in-the-dataset"></a>A criação de tabelas no conjunto de dados  
 Esta seção explicará como adicionar tabelas ao conjunto de dados.  
  
#### <a name="to-create-the-customers-table"></a>Para criar a tabela Customers  
  
1.  Expanda a conexão de dados que você criou na **Gerenciador de servidores**e, em seguida, expanda o **tabelas** nó.  
  
2.  Arraste o **clientes** tabela de **Gerenciador de servidores** até o **Dataset Designer**.  
  
     Um **clientes** tabela de dados e **CustomersTableAdapter** são adicionados ao conjunto de dados.  
  
#### <a name="to-create-the-orders-table"></a>Para criar a tabela Orders  
  
-   Arraste o **pedidos** tabela de **Gerenciador de servidores** para o **Dataset Designer**.  
  
     Uma **pedidos** tabela de dados, **OrdersTableAdapter**e a relação de dados entre o **clientes** e **pedidos** tabelas são adicionadas à conjunto de dados.  
  
#### <a name="to-create-the-orderdetails-table"></a>Para criar a tabela OrderDetails  
  
-   Arraste o **detalhes do pedido** tabela de **Gerenciador de servidores** até o **Dataset Designer**.  
  
     Uma **detalhes do pedido** tabela de dados **Order DetailsTableAdapter**e uma relação de dados entre o **pedidos** e **detalhes do pedido** tabelas são adicionadas ao conjunto de dados.  
  
## <a name="next-steps"></a>Próximas etapas  
  
### <a name="to-add-functionality-to-your-application"></a>Para adicionar funcionalidade ao seu aplicativo  
  
-   Salve o conjunto de dados.  
  
-   Selecione os itens na **fontes de dados** janela e arrastá-los para um formulário. Para obter mais informações, consulte [controles de ligar o Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md).  
  
-   Adicione mais consultas para os TableAdapters. Para obter mais informações, consulte [como: criar consultas do TableAdapter](../data-tools/how-to-create-tableadapter-queries.md).  
  
-   Adicionar lógica de validação para o <xref:System.Data.DataTable.ColumnChanging> ou <xref:System.Data.DataTable.RowChanging> eventos das tabelas de dados no conjunto de dados. Para obter mais informações, consulte [validar dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)   
 [Validando dados](http://msdn.microsoft.com/library/b3a9ee4e-5d4d-4411-9c56-c811f2b4ee7e)   
 [Salvando dados](../data-tools/saving-data.md)