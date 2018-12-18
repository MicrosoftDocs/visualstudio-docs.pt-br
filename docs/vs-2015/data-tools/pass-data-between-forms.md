---
title: Passar dados entre formulários | Microsoft Docs
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
- walkthroughs [Windows Forms], data
- walkthroughs [Visual Studio], data
- data [Visual Studio], passing between forms
- forms, passing data between
- Windows Forms, walkthroughs
ms.assetid: 78bf038b-9296-4fbf-b0e8-d881d1aff0df
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: a9f28902673018a4ae90fbb2ed83e741be99fbfc
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49204822"
---
# <a name="pass-data-between-forms"></a>Passar dados entre formulários
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Este passo a passo fornece instruções detalhadas de como passar os dados de um formulário para outro. Usando as tabelas customers e orders do Northwind, um formulário que os usuários selecionem um cliente e um segundo formulário exibe os pedidos do cliente selecionado. Este passo a passo mostra como criar um método no segundo formulário que recebe dados do primeiro formulário.  
  
> [!NOTE]
>  Este passo a passo demonstra apenas uma maneira de passar dados entre formulários. Há outras opções para passar dados para um formulário, incluindo a criação de um segundo construtor para receber dados, ou criando uma propriedade pública que pode ser definida com os dados do primeiro formulário.  
  
 As tarefas ilustradas neste passo a passo incluem:  
  
-   Criando um novo **aplicativo do Windows** projeto.  
  
-   Criando e configurando um conjunto de dados com o [Data Source Configuration Wizard](http://msdn.microsoft.com/library/c4df7de5-5da0-4064-940c-761dd6d9e28f).  
  
-   Selecionando o controle a ser criado no formulário ao arrastar itens dos **fontes de dados** janela. Para obter mais informações, consulte [definir o controle a ser criado quando arrastado da janela fontes de dados](../data-tools/set-the-control-to-be-created-when-dragging-from-the-data-sources-window.md).  
  
-   Criando um controle associado a dados arrastando itens dos **fontes de dados** janela em um formulário.  
  
-   Criar um segundo formulário com uma grade para exibir dados.  
  
-   Criar uma consulta TableAdapter para buscar pedidos de um cliente específico.  
  
-   Passar dados entre formulários.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para concluir este passo a passo, você precisará de:  
  
-   Acesso ao banco de dados de exemplo Northwind. Para obter mais informações, consulte [como: instalar os bancos de dados de exemplo](../data-tools/how-to-install-sample-databases.md).  
  
## <a name="create-the-windows-application"></a>Criar o aplicativo do Windows  
  
#### <a name="to-create-the-new-windows-project"></a>Para criar o novo projeto do Windows  
  
1.  Dos **arquivo** menu, crie um novo projeto.  
  
2.  Nomeie o projeto `PassingDataBetweenForms`.  
  
3.  Selecione **aplicativo do Windows Forms**e clique em **Okey**. Para obter mais informações, consulte [aplicativos cliente](http://msdn.microsoft.com/library/2dfb50b7-5af2-4e12-9bbb-c5ade0e39a68).  
  
     O **PassingDataBetweenForms** projeto é criado e adicionado ao **Gerenciador de soluções**.  
  
## <a name="create-the-data-source"></a>Criar a fonte de dados  
  
#### <a name="to-create-the-data-source"></a>Para criar a fonte de dados  
  
1.  Sobre o **dados** menu, clique em **Show Data Sources**.  
  
2.  No **fontes de dados** janela, selecione **Add New Data Source** para iniciar o **configuração de fonte de dados** assistente.  
  
3.  Selecione **banco de dados** sobre o **escolher um tipo de fonte de dados** página e, em seguida, clique em **próxima**.  
  
4.  No **escolha um modelo de banco de dados** página, verifique **Dataset** é especificado e, em seguida, clique em **próxima**.  
  
5.  Sobre o **escolha sua Conexão de dados** página, faça o seguinte:  
  
    -   Se uma conexão de dados com o banco de dados de exemplo Northwind estiver disponível na lista suspensa, selecione-o.  
  
    -   Selecione **nova Conexão** para iniciar o **Adicionar/Modificar Conexão** caixa de diálogo.  
  
6.  Se seu banco de dados exigir uma senha e se a opção para incluir dados confidenciais é ativada, selecione a opção e, em seguida, clique em **próxima**.  
  
7.  Sobre o **salvar a cadeia de caracteres de conexão para o arquivo de configuração de aplicativo** , clique em **próxima**.  
  
8.  Sobre o **Choose your Database Objects** página, expanda o **tabelas** nó.  
  
9. Selecione o **clientes** e **pedidos** tabelas e clique **concluir**.  
  
     O **NorthwindDataSet** é adicionado ao seu projeto e o **clientes** e **pedidos** tabelas aparecem no **fontes de dados** janela.  
  
## <a name="create-the-first-form-form1"></a>Criar o primeiro formulário (Form1)  
 Você pode criar uma grade de associação de dados (um <xref:System.Windows.Forms.DataGridView> controle), arrastando o **clientes** nó a partir de **fontes de dados** janela para o formulário.  
  
#### <a name="to-create-a-data-bound-grid-on-the-form"></a>Para criar uma grade de associação de dados no formulário  
  
-   Arraste principal **clientes** nó a partir do **fontes de dados** window para **Form1**.  
  
     Um <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramenta (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no **Form1**. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), [CustomersTableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
## <a name="create-the-second-form-form2"></a>Criar o segundo formulário (Form2)  
  
#### <a name="to-create-a-second-form-to-pass-the-data-to"></a>Para criar um segundo formulário para o qual passar os dados  
  
1.  No menu **Projeto**, escolha **Adicionar Formulário do Windows**.  
  
2.  Deixe o nome padrão **Form2**e clique em **Add**.  
  
3.  Arraste principal **pedidos** nó a partir do **fontes de dados** window para **Form2**.  
  
     Um <xref:System.Windows.Forms.DataGridView> e uma faixa de ferramenta (<xref:System.Windows.Forms.BindingNavigator>) para navegação em registros são exibidos no **Form2**. Um [NorthwindDataSet](../data-tools/dataset-tools-in-visual-studio.md), [CustomersTableAdapter](../data-tools/tableadapter-overview.md), <xref:System.Windows.Forms.BindingSource>, e <xref:System.Windows.Forms.BindingNavigator> aparecem na bandeja de componentes.  
  
4.  Excluir o **OrdersBindingNavigator** da bandeja de componentes.  
  
     O **OrdersBindingNavigator** desaparece da **Form2**.  
  
## <a name="add-a-tableadapter-query-to-form2-to-load-orders-for-the-selected-customer-on-form1"></a>Adicionar uma consulta TableAdapter ao Form2 para carregar pedidos do cliente selecionado no Form1  
  
#### <a name="to-create-a-tableadapter-query"></a>Para criar uma consulta do TableAdapter  
  
1.  Clique duas vezes o **NorthwindDataSet** arquivo no **Gerenciador de soluções**.  
  
2.  Clique com botão direito do **OrdersTableAdapter**e selecione **Add Query**.  
  
3.  Deixe a opção padrão **usar instruções SQL**e, em seguida, clique em **próxima**.  
  
4.  Deixe a opção padrão **SELECT que retorna linhas**e, em seguida, clique em **próxima**.  
  
5.  Adicionar uma cláusula WHERE à consulta, para retornar `Orders` baseia o `CustomerID`. A consulta deve ser semelhante ao seguinte:  
  
    ```  
    SELECT OrderID, CustomerID, EmployeeID, OrderDate, RequiredDate, ShippedDate, ShipVia, Freight, ShipName, ShipAddress, ShipCity, ShipRegion, ShipPostalCode, ShipCountry  
    FROM Orders   
    WHERE CustomerID = @CustomerID  
    ```  
  
    > [!NOTE]
    >  Verifique a sintaxe de parâmetro correta para o seu banco de dados. Por exemplo, no Microsoft Access, a cláusula WHERE seria algo como: `WHERE CustomerID = ?`.  
  
6.  Clique em **Avançar**.  
  
7.  Para o **preencha um nome de DataTableMethod**, tipo `FillByCustomerID`.  
  
8.  Desmarque a **retornar uma DataTable** opção e, em seguida, clique em **próxima**.  
  
9. Clique em **Finalizar**.  
  
## <a name="create-a-method-on-form2-to-pass-data-to"></a>Criar um método no Form2 para passar dados para  
  
#### <a name="to-create-a-method-to-pass-data-to"></a>Para criar um método para o qual passar dados  
  
1.  Clique com botão direito **Form2**e selecione **Exibir código** para abrir **Form2** no **Editor de códigos**.  
  
2.  Adicione o seguinte código ao **Form2** depois que o `Form2_Load` método:  
  
     [!code-csharp[VbRaddataDisplaying#1](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form2.cs#1)]
     [!code-vb[VbRaddataDisplaying#1](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form2.vb#1)]  
  
## <a name="create-a-method-on-form1-to-pass-data-and-display-form2"></a>Criar um método no Form1 para passar dados e exibir o Form2  
  
#### <a name="to-create-a-method-to-pass-data-to-form2"></a>Para criar um método para passar dados para o Form2  
  
1.  Na **Form1**, clique com botão direito da grade de dados do cliente e, em seguida, clique em **propriedades**.  
  
2.  Na janela **Propriedades**, clique em **Eventos**.  
  
3.  Clique duas vezes o **CellDoubleClick** eventos.  
  
     O Editor de Códigos é exibido.  
  
4.  Atualize a definição de método para corresponder ao seguinte exemplo:  
  
     [!code-csharp[VbRaddataDisplaying#2](../snippets/csharp/VS_Snippets_VBCSharp/VbRaddataDisplaying/CS/Form1.cs#2)]
     [!code-vb[VbRaddataDisplaying#2](../snippets/visualbasic/VS_Snippets_VBCSharp/VbRaddataDisplaying/VB/Form1.vb#2)]  
  
## <a name="run-the-application"></a>Executar o aplicativo  
  
#### <a name="to-run-the-application"></a>Para executar o aplicativo  
  
-   Pressione F5 para executar o aplicativo.  
  
-   Clique duas vezes em um registro de cliente no **Form1** para abrir **Form2** com pedidos do cliente.  
  
## <a name="next-steps"></a>Próximas etapas  
 Dependendo dos requisitos de aplicativo, existem várias etapas que você talvez queira realizar após passar dados entre formulários. Entre algumas das melhorias que você poderia fazer nessa explicação passo a passo estão:  
  
-   Editar o conjunto de dados, para adicionar ou remover objetos de banco de dados. Para obter mais informações, consulte [Create and configure datasets (Criar e configurar conjuntos de dados)](../data-tools/create-and-configure-datasets-in-visual-studio.md).  
  
-   Adicionar funcionalidade para salvar dados de volta no banco de dados. Para obter mais informações, consulte [salvar dados no banco de dados](../data-tools/save-data-back-to-the-database.md).  
  
## <a name="see-also"></a>Consulte também  
 [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)

