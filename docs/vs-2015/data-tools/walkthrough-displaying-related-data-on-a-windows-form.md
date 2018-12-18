---
title: 'Passo a passo: Exibindo dados relacionados em um formulário do Windows | Microsoft Docs'
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
- displaying data on forms, walkthroughs
- Windows Forms, displaying data
- data [Visual Studio], displaying on Windows Forms
- master-details lists, displaying on Windows Forms
- data [Visual Studio], master-details
- displaying tables, related data
- displaying table data
- displaying table information
ms.assetid: fc4b9055-2bf3-4028-8aad-9489820d69f6
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 882c8229c105920efe247a54e9525a262e6a3246
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49282666"
---
# <a name="walkthrough-displaying-related-data-on-a-windows-form"></a>Instruções passo a passo: exibindo dados relacionados em um Windows Form
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Em vários cenários de aplicativo, você deseja trabalhar com dados provenientes de mais de uma tabela e, geralmente, dados de tabelas relacionadas. Ou seja, você deseja trabalhar com um relacionamento pai-filho. Por exemplo, talvez você queira criar um formulário em que selecionar um registro do cliente exibe os pedidos desse cliente. Exibir os registros relacionados no formulário é possível ao configurar a propriedade <xref:System.Windows.Forms.BindingSource.DataSource%2A> do <xref:System.Windows.Forms.BindingSource> filho para o <xref:System.Windows.Forms.BindingSource> pai (não a tabela filha) e ao configurar a propriedade <xref:System.Windows.Forms.BindingSource.DataMember%2A> do <xref:System.Windows.Forms.BindingSource> filho para a relação de dados que une as tabelas pai e filha.  
  
 As tarefas ilustradas neste passo a passo incluem:  
  
-   Criando um **aplicativo do Windows** projeto.  
  
-   Criando e configurando um conjunto de dados em seu aplicativo com base nas `Customers` e `Orders` tabelas no banco de dados Northwind usando o [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f).  
  
-   Adicionando controles para exibir dados na tabela `Customers`.  
  
-   Adicionando controles para exibir os `Orders` com base no `Customer` selecionado.  
  
-   Testando o aplicativo ao selecionar clientes diferentes e verificar se os pedidos corretos são exibidos para o cliente selecionado.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind. Para configurar os bancos de dados, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="creating-the-project"></a>Criando o Projeto  
 A primeira etapa é criar uma **aplicativo do Windows**.  
  
#### <a name="to-create-the-windows-application-project"></a>Para criar o projeto de Aplicativo do Windows  
  
1.  Dos **arquivo** menu, crie um novo projeto.  
  
2.  Nomeie o projeto `RelatedDataWalkthrough`.  
  
3.  Selecione **aplicativo do Windows** e clique em **Okey**. Para obter mais informações, consulte [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
     O **RelatedDataWalkthrough** projeto é criado e adicionado ao **Gerenciador de soluções**.  
  
## <a name="creating-the-data-source"></a>Criando a Fonte de Dados  
 Esta etapa cria um conjunto de dados com base nas tabelas `Customers` e `Orders` do banco de dados de exemplo Northwind.  
  
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
  
8.  Selecione o **clientes** e **pedidos** tabelas e clique **concluir**.  
  
     O **NorthwindDataSet** é adicionado ao seu projeto e o **clientes** tabela aparece no **fontes de dados** janela.  
  
## <a name="creating-controls-to-display-data-from-the-customers-table"></a>Criando Controles para Exibir Dados com base na Tabela Customers  
  
#### <a name="to-create-controls-to-display-the-customer-data-parent-records"></a>Para criar controles a fim de exibir os dados do cliente (registros pai)  
  
1.  No **fontes de dados** janela, selecione a **clientes** de tabela e, em seguida, clique na seta suspensa.  
  
2.  Escolher **detalhes** no menu.  
  
3.  Arraste principal **clientes** nó a partir do **fontes de dados** janela para o topo da **Form1**.  
  
     Os controles de associação de dados com rótulos descritivos são exibidos no formulário, juntamente com uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para registros de navegação. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), [CustomersTableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
## <a name="creating-controls-to-display-data-from-the-orders-table"></a>Criando Controles para Exibir Dados da Tabela Orders  
 ![Janela de fontes de dados que mostra a relação](../data-tools/media/datasources2.gif "DataSources2")  
  
#### <a name="to-create-controls-to-display-the-orders-for-each-customer-child-records"></a>Para criar controles para exibir os pedidos de cada cliente (registros filho)  
  
-   No **fontes de dados** janela, expanda o **clientes** nó e selecione a última coluna na **clientes** tabela, que é um expansível **pedidos** nó e arraste-o para a parte inferior da **Form1**.  
  
     Um <xref:System.Windows.Forms.DataGridView> é adicionado ao formulário e um novo <xref:System.Windows.Forms.BindingSource> (`OrdersBindingSource`) e um TableAdapter (`OrdersTableAdapter`) são adicionados à bandeja de componentes.  
  
    > [!NOTE]
    >  Abra o [janela de propriedades](../ide/reference/properties-window.md) e selecione o **OrdersBindingSource**. Inspecione as propriedades <xref:System.Windows.Forms.BindingSource.DataSource%2A> e <xref:System.Windows.Forms.BindingSource.DataMember%2A> para ver como a associação está configurada para exibir registros relacionados. O <xref:System.Windows.Forms.BindingSource.DataSource%2A> está configurado como `CustomersBindingSource` (o <xref:System.Windows.Forms.BindingSource> da tabela pai), em vez da tabela `Orders`. A propriedade <xref:System.Windows.Forms.BindingSource.DataMember%2A> está configurada como `FK_Orders_Customers`, que é o nome do objeto <xref:System.Data.DataRelation> que relaciona as tabelas juntas.  
  
## <a name="testing-the-application"></a>Testando o aplicativo  
  
#### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Pressione F5 para executar o aplicativo.  
  
2.  Selecione diferentes clientes usando o **CustomersBindingNavigator** para verificar se os pedidos corretos são exibidos no <xref:System.Windows.Forms.DataGridView>.  
  
## <a name="next-steps"></a>Próximas etapas  
 Dependendo dos requisitos de aplicativo, existem várias etapas que você talvez queira realizar após criar um formulário de detalhes mestre. Uma melhoria que você poderia fazer neste passo a passo é:  
  
-   Filtrar os registros de `Customers` adicionando parametrização à tabela `Customers`. Para fazer isso, selecione qualquer controle que exibe dados do `Customers` de tabela, clique na marca inteligente e escolha **Add Query**. Conclua o [caixa de diálogo do construtor de critérios de pesquisa](http://msdn.microsoft.com/library/0b306b92-f35e-45ef-a4be-3f653cd00c3d). Para obter mais informações, consulte [como: adicionar uma consulta parametrizada a um aplicativo do Windows Forms](http://msdn.microsoft.com/library/13db4ad3-56b9-4a0b-b3a5-6a4ff84d4416).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo de dados](http://msdn.microsoft.com/library/15a88fb8-3bee-4962-914d-7a1f8bd40ec4)   
 [Janela Fontes de Dados](http://msdn.microsoft.com/library/0d20f699-cc95-45b3-8ecb-c7edf1f67992)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)   
 [Visão geral de TableAdapter](../data-tools/tableadapter-overview.md)   
 [Como: Exibir relacionados a dados em um Windows Forms Application](../data-tools/how-to-display-related-data-in-a-windows-forms-application.md)   
 [Visão geral do componente BindingSource](http://msdn.microsoft.com/library/be838caf-fcb0-4b68-827f-58b2c04b747f)   
 [Visão geral do controle BindingNavigator](http://msdn.microsoft.com/library/4423eede-f8d1-4d02-822f-5bf8432680d0)