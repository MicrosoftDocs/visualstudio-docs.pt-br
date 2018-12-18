---
title: 'Passo a passo: Criando um TableAdapter com várias consultas | Microsoft Docs'
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
- TableAdapter queries, creating
- data [Visual Studio], TableAdapters
- TableAdapters, creating
- data [Visual Studio], walkthroughs
- queries [Visual Studio], TableAdapters
ms.assetid: f784dc4d-d514-4ade-8226-f8271c5b1ed8
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 4226fc805ed0335109d0a6b98f1235ae46de1664
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49206694"
---
# <a name="walkthrough-creating-a-tableadapter-with-multiple-queries"></a>Instruções passo a passo: criando um TableAdapter com várias consultas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Neste passo a passo, você criará um TableAdapter em um conjunto de dados usando o [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f). O passo a passo leva você por meio do processo de criação de uma segunda consulta na [TableAdapter](../data-tools/tableadapter-overview.md) usando o [editando TableAdapters](../data-tools/editing-tableadapters.md) dentro a [Dataset Designer](../data-tools/creating-and-editing-typed-datasets.md).  
  
 As tarefas ilustradas neste passo a passo incluem:  
  
-   Criando um novo **aplicativo do Windows** projeto.  
  
-   Criar e configurar uma fonte de dados em seu aplicativo, criando um dataset com o **Data Source Configuration Wizard**.  
  
-   Abrindo o conjunto de dados novo a **Dataset Designer**.  
  
-   Adicionando consultas ao TableAdapter com o **Assistente de configuração de consulta do TableAdapter**.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind (versão SQL Server ou Access). Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="creating-a-new-windows-application"></a>Criando um novo Aplicativo do Windows  
 A primeira etapa é criar um aplicativo do Windows.  
  
#### <a name="to-create-a-new-windows-application-project"></a>Para criar um novo projeto de Aplicativo do Windows  
  
1.  Na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], do **arquivo** menu, crie um novo projeto.  
  
2.  Escolha uma linguagem de programação a **tipos de projeto** painel.  
  
3.  Clique em **aplicativo do Windows** na **modelos** painel.  
  
4.  Nomeie o projeto `TableAdapterQueriesWalkthrough`e, em seguida, clique em **Okey**.  
  
     O projeto para o Visual Studio adiciona **Gerenciador de soluções** e exibe um novo formulário no designer.  
  
## <a name="creating-a-database-data-source-with-a-tableadapter"></a>Criando uma fonte de dados do banco de dados com um TableAdapter  
 Esta etapa cria uma fonte de dados usando o **Data Source Configuration Wizard** com base no `Customers` tabela no banco de dados de exemplo Northwind. É preciso ter acesso ao banco de dados de exemplo Northwind para criar a conexão. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
#### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1.  Sobre o **dados** menu, clique em **Show Data Sources**.  
  
2.  No **fontes de dados** janela, selecione **Add New Data Source** para iniciar o **Data Source Configuration Wizard**.  
  
3.  Selecione **banco de dados** sobre o **escolher um tipo de fonte de dados** página e, em seguida, clique em **próxima**.  
  
4.  Sobre o **escolha sua Conexão de dados** página faça o seguinte:  
  
    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.  
  
         -ou-  
  
    -   Selecione **nova Conexão** para iniciar o **Adicionar/Modificar Conexão** caixa de diálogo.  
  
5.  Se seu banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, clique em **próxima**.  
  
6.  Clique em **próxima** sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** página.  
  
7.  Expanda o **tabelas** nó na **Choose your Database Objects** página.  
  
8.  Selecione o **clientes** tabela e, em seguida, clique em **concluir**.  
  
     O **NorthwindDataSet** é adicionado ao seu projeto e o **clientes** tabela aparece no **fontes de dados** janela.  
  
## <a name="opening-the-dataset-in-the-dataset-designer"></a>Abrindo o conjunto de dados no Designer de Conjunto de Dados  
  
#### <a name="to-open-the-dataset-in-the-dataset-designer"></a>Para abrir o conjunto de dados no Designer de Conjunto de Dados  
  
1.  Clique com botão direito **NorthwindDataset** na **fontes de dados** janela.  
  
2.  No menu de atalho, escolha **Editar DataSet com Designer**.  
  
     O NorthwindDataset é aberto na **Dataset Designer**.  
  
## <a name="adding-a-second-query-to-the-customerstableadapter"></a>Adicionando uma segunda consulta ao CustomersTableAdapter  
 O assistente criou o conjunto de dados com um **clientes** tabela de dados e **CustomersTableAdapter**. Esta seção do passo a passo adiciona uma segunda consulta para o **CustomersTableAdapter**.  
  
#### <a name="to-add-a-query-to-the-customerstableadapter"></a>Para adicionar uma consulta ao CustomersTableAdapter  
  
1.  Arraste uma **consulta** da **conjunto de dados** guia da **caixa de ferramentas** para o **clientes** tabela.  
  
     O [editando TableAdapters](../data-tools/editing-tableadapters.md) é aberta.  
  
2.  Selecione **usar instruções SQL**e, em seguida, clique em **próxima**.  
  
3.  Selecione **SELECT que retorna linhas**e, em seguida, clique em **próxima**.  
  
4.  Adicione uma cláusula WHERE à consulta para que se leia:  
  
    ```  
    SELECT CustomerID, CompanyName, ContactName, ContactTitle, Address, City, Region, PostalCode, Country, Phone, Fax   
    FROM Customers   
    WHERE City = @City  
    ```  
  
    > [!NOTE]
    >  Se você estiver usando a versão Access do Northwind, substitua o @City parâmetro com um ponto de interrogação. (`SELECT CustomerID, CompanyName, ContactName, ContactTitle, Address, City, Region, PostalCode, Country, Phone, Fax FROM Customers WHERE City = ?`)  
  
5.  Sobre o **escolha métodos para gerar** página, nomeie o **preencher uma DataTable** método `FillByCity`.  
  
    > [!NOTE]
    >  O método **retornar uma DataTable** não é usado neste passo a passo, portanto, você pode desmarcar a caixa de seleção ou deixe o nome padrão.  
  
6.  Clique em **próxima** e conclua o assistente.  
  
     O **FillByCity** consulta é adicionada para o **CustomersTableAdapter**.  
  
## <a name="adding-code-to-execute-the-additional-query-on-the-form"></a>Adicionando código para executar a consulta adicional ao formulário  
  
#### <a name="to-execute-the-query"></a>Para executar a consulta  
  
1.  Selecione **Form1** na **Gerenciador de soluções**e clique em **View Designer**.  
  
2.  Arraste o **clientes** nó a partir do **fontes de dados** janela para **Form1**.  
  
3.  Alterar a exibição de código, selecionando **código** da **exibição** menu.  
  
4.  Substitua o código no manipulador de eventos `Form1_Load` pelo código abaixo para executar a consulta `FillByCity`.  
  
     [!code-csharp[VbRaddataTableAdapters#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataTableAdapters/CS/Form1.cs#1)]
     [!code-vb[VbRaddataTableAdapters#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataTableAdapters/VB/Form1.vb#1)]  
  
## <a name="running-the-application"></a>Executando o aplicativo  
  
#### <a name="to-run-the-application"></a>Para executar o aplicativo  
  
-   Pressione F5.  
  
-   A grade é preenchida por clientes com um valor `City` de `Seattle`.  
  
## <a name="next-steps"></a>Próximas etapas  
  
### <a name="to-add-functionality-to-your-application"></a>Para adicionar funcionalidade ao seu aplicativo  
  
-   Adicione um controle <xref:System.Windows.Forms.TextBox> e um controle <xref:System.Windows.Forms.Button> e passe o valor na caixa de texto para a consulta. (`CustomersTableAdapter.FillByCity(NorthwindDataSet.Customers, TextBox1.Text)`).  
  
-   Adicione a lógica de validação ao evento <xref:System.Data.DataTable.ColumnChanging> ou <xref:System.Data.DataTable.RowChanging> das tabelas de dados no conjunto de dados. Para obter mais informações, consulte [validar dados em conjuntos de dados](../data-tools/validate-data-in-datasets.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Criar e configurar TableAdapters](../data-tools/create-and-configure-tableadapters.md)   
 [Como: criar consultas TableAdapter](../data-tools/how-to-create-tableadapter-queries.md)   
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Conectando-se a dados no Visual Studio](../data-tools/connecting-to-data-in-visual-studio.md)   
 [Preparando o aplicativo para receber dados](http://msdn.microsoft.com/library/c17bdb7e-c234-4f2f-9582-5e55c27356ad)   
 [Buscando dados no aplicativo](../data-tools/fetching-data-into-your-application.md)   
 [Associar controles a dados no Visual Studio](../data-tools/bind-controls-to-data-in-visual-studio.md)   
 [Editando dados no aplicativo](../data-tools/editing-data-in-your-application.md)