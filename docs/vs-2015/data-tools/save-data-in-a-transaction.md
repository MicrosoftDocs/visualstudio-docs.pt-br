---
title: Salvar dados em uma transação | Microsoft Docs
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
- System.Transactions namespace
- data [Visual Studio], saving in a transaction
- transactions, saving data
- Transactions namespace
- saving data
ms.assetid: 80260118-08bc-4b37-bfe5-9422ee7a1e4e
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: b0912ffbe2a9a82ac5efbd3b2ca6ba3566ce5b02
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219296"
---
# <a name="save-data-in-a-transaction"></a>Salvar dados em uma transação
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Este passo a passo demonstra como salvar dados em uma transação usando o <xref:System.Transactions> namespace. Este exemplo usa as tabelas `Customers` e `Orders` do banco de dados de exemplo Northwind.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este passo a passo requer acesso ao banco de dados de exemplo Northwind. Para obter informações sobre como configurar o banco de dados de exemplo Northwind, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="create-a-windows-application"></a>Criar um aplicativo do Windows  
 A primeira etapa é criar uma **aplicativo do Windows**.  
  
#### <a name="to-create-the-new-windows-project"></a>Para criar o novo projeto do Windows  
  
1.  No Visual Studio, sobre o **arquivo** menu, crie uma nova **projeto**.  
  
2.  Nomeie o projeto **SavingDataInATransactionWalkthrough**.  
  
3.  Selecione **aplicativo do Windows**e, em seguida, selecione **Okey**. Para obter mais informações, consulte [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
     O **SavingDataInATransactionWalkthrough** projeto é criado e adicionado ao **Gerenciador de soluções**.  
  
## <a name="create-a-database-data-source"></a>Criar uma fonte de dados do banco de dados  
 Esta etapa usa a [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f) para criar uma fonte de dados com base nas `Customers` e `Orders` tabelas no banco de dados de exemplo Northwind.  
  
#### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1.  Sobre o **dados** menu, selecione**Show Data Sources**.  
  
2.  No **fontes de dados** janela, selecione **Add New Data Source** para iniciar o **Data Source Configuration Wizard**.  
  
3.  Sobre o **escolher um tipo de fonte de dados**tela, selecione **banco de dados**e, em seguida, selecione **próxima**.  
  
4.  Sobre o **escolha sua Conexão de dados**tela faça o seguinte:  
  
    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.  
  
         -ou-  
  
    -   Selecione **nova Conexão** para iniciar o **Adicionar/Modificar Conexão** caixa de diálogo caixa e criar uma conexão ao banco de dados Northwind.  
  
5.  Se seu banco de dados exigir uma senha, selecione a opção para incluir dados confidenciais e, em seguida, selecione **próxima**.  
  
6.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** tela, selecione **próxima**.  
  
7.  Sobre o **Choose your Database Objects** , expanda o **tabelas** nó.  
  
8.  Selecione o `Customers` e `Orders` tabelas e, em seguida, selecione **concluir**.  
  
     O **NorthwindDataSet** é adicionado ao seu projeto e o `Customers` e `Orders` as tabelas aparecem no **fontes de dados** janela.  
  
## <a name="addcontrols-to-the-form"></a>Addcontrols ao formulário  
 Você pode criar os controles ligados a dados arrastando itens dos **fontes de dados** window para seu formulário.  
  
#### <a name="to-create-data-bound-controls-on-the-windows-form"></a>Para criar dados de associação de controles do formulário do Windows  
  
-   No **fontes de dados** janela, expanda o **clientes** nó.  
  
-   Arraste principal **clientes** nó a partir do **fontes de dados** window para **Form1**.  
  
     Um controle <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramentas (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no formulário. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), [CustomersTableAdapter](../data-tools/tableadapter-overview.md),<xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
-   Arraste relacionado **pedidos** nó (não principal **pedidos** nó, mas o nó de tabela filha relacionada abaixo de **Fax** coluna) para o formulário abaixo o  **CustomersDataGridView**.  
  
     Um <xref:System.Windows.Forms.DataGridView> aparece no formulário. Uma [OrdersTableAdapter](../data-tools/tableadapter-overview.md) e <xref:System.Windows.Forms.BindingSource> aparecem na bandeja de componentes.  
  
## <a name="add-a-reference-to-the-systemtransactions-assembly"></a>Adicione uma referência ao assembly System. Transactions  
 As transações usam o namespace <xref:System.Transactions>. Uma referência do projeto ao assembly system.transactions não é adicionada por padrão, portanto, você precisa adicioná-la manualmente.  
  
#### <a name="to-add-a-reference-to-the-systemtransactions-dll-file"></a>Para adicionar uma referência ao arquivo DLL System.Transactions  
  
1.  Sobre o **Project** menu, selecione**adicionar referência**.  
  
2.  Selecione **System. Transactions**(sobre o **.NET** guia) e, em seguida, selecione **Okey**.  
  
     Uma referência a **System. Transactions** é adicionado ao projeto.  
  
## <a name="modifythe-code-in-the-bindingnavigators-saveitem-button"></a>Código de Modifythe no botão SaveItem do BindingNavigator  
 Para a primeira tabela arrastada para seu formulário, o código é adicionado por padrão para o `click` no botão de evento do salvamento a <xref:System.Windows.Forms.BindingNavigator>. É necessário adicionar manualmente o código para atualizar quaisquer tabelas adicionais. Para este passo a passo, podemos refatorar o código salvar existente manipulador de eventos de clique do botão. Além disso, podemos criar mais alguns métodos para fornecer a funcionalidade de atualização específica com base em se a linha precisa ser adicionada ou excluída.  
  
#### <a name="to-modify-the-auto-generated-save-code"></a>Para modificar o código salvar gerado automaticamente  
  
1. Selecione o **salve** botão a **CustomersBindingNavigator** (o botão com o ícone de disquete).  
  
2. Substitua o método `CustomersBindingNavigatorSaveItem_Click` pelo seguinte código:  
  
    [!code-csharp[VbRaddataSaving#4](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#4)]
    [!code-vb[VbRaddataSaving#4](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#4)]  
  
   A ordem para reconciliar as alterações aos dados relacionados é a seguinte:  
  
-   Exclua registros filho. (Nesse caso, exclua registros do `Orders` tabela.)  
  
-   Exclua registros pais. (Nesse caso, exclua registros do `Customers` tabela.)  
  
-   Inserir registros pais. (Nesse caso, insira registros no `Customers` tabela.)  
  
-   Inserir registros filhos. (Nesse caso, insira registros no `Orders` tabela.)  
  
#### <a name="to-delete-existing-orders"></a>Para excluir pedidos existentes  
  
-   Adicione o seguinte `DeleteOrders` método **Form1**:  
  
     [!code-csharp[VbRaddataSaving#5](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#5)]
     [!code-vb[VbRaddataSaving#5](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#5)]  
  
#### <a name="to-delete-existing-customers"></a>Para excluir clientes existentes  
  
-   Adicione o seguinte `DeleteCustomers` método **Form1**:  
  
     [!code-csharp[VbRaddataSaving#6](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#6)]
     [!code-vb[VbRaddataSaving#6](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#6)]  
  
#### <a name="to-add-new-customers"></a>Para adicionar novos clientes  
  
-   Adicione o seguinte `AddNewCustomers` método **Form1**:  
  
     [!code-csharp[VbRaddataSaving#7](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#7)]
     [!code-vb[VbRaddataSaving#7](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#7)]  
  
#### <a name="to-add-new-orders"></a>Para adicionar novos pedidos  
  
-   Adicione o seguinte `AddNewOrders` método **Form1**:  
  
     [!code-csharp[VbRaddataSaving#8](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataSaving/CS/Form2.cs#8)]
     [!code-vb[VbRaddataSaving#8](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataSaving/VB/Form2.vb#8)]  
  
## <a name="run-the-application"></a>Executar o aplicativo  
  
#### <a name="to-run-the-application"></a>Para executar o aplicativo  
  
-   Selecione **F5** para executar o aplicativo.  
  
## <a name="see-also"></a>Consulte também  
 [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)

