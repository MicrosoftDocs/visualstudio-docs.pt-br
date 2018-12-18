---
title: 'Passo a passo: Exibindo dados relacionados em um aplicativo WPF | Microsoft Docs'
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
- WPF, data binding in Visual Studio
- WPF data binding [Visual Studio], walkthroughs
- WPF Designer, data binding
ms.assetid: 5c48f188-e9c4-40a6-97d9-67cdb2f90127
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: ghogen
robots: noindex,nofollow
ms.openlocfilehash: 1fc90acf94fde0ef815fc3a487412bba8e8257ff
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49913131"
---
# <a name="walkthrough-displaying-related-data-in-a-wpf-application"></a>Instruções passo a passo: exibindo dados relacionados em um aplicativo WPF
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Neste passo a passo, você criará um aplicativo do WPF que exibe dados de tabelas de banco de dados que têm uma relação pai/filho. Os dados são encapsulados em entidades em um modelo de dados de entidade. A entidade pai contém informações de visão geral de um conjunto de pedidos. Cada propriedade dessa entidade é associada a um controle diferente no aplicativo. A entidade filho contém detalhes de cada pedido. Esse conjunto de dados está associado a um <xref:System.Windows.Controls.DataGrid> controle.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Criando um aplicativo WPF e um modelo de dados de entidade que é gerado a partir de dados no banco de dados de exemplo AdventureWorksLT.  
  
- Criando um conjunto de controles ligados a dados que exibem informações de visão geral de um conjunto de pedidos. Criar os controles arrastando uma entidade pai dos **fontes de dados** janela **WPF Designer**.  
  
- Criando um <xref:System.Windows.Controls.DataGrid> selecionado de controle que exibe os detalhes relacionados para cada ordem. Criar os controles arrastando uma entidade filho do **fontes de dados** janela para uma janela do **WPF designer**.  
  
   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
- Acesso a uma instância em execução do SQL Server ou SQL Server Express que tenha o banco de dados de exemplo AdventureWorksLT anexado a ele. Você pode baixar o banco de dados AdventureWorksLT a [site da CodePlex](http://go.microsoft.com/fwlink/?linkid=87843).  
  
  Conhecimento prévio dos conceitos a seguir também é útil, mas não é necessário para concluir o passo a passo:  
  
- Modelos de Dados de Entidade e o ADO.NET Entity Framework. Para obter mais informações, consulte [visão geral do Entity Framework](http://msdn.microsoft.com/library/a2166b3d-d8ba-4a0a-8552-6ba1e3eaaee0).  
  
- Trabalhando com o WPF Designer. Para obter mais informações, consulte [WPF e Silverlight Designer Overview](http://msdn.microsoft.com/en-us/570b7a5c-0c86-4326-a371-c9b63378fc62).  
  
- Associação de dados do WPF. Para obter mais informações, consulte [Visão geral de vinculação de dados](http://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211).  
  
## <a name="creating-the-project"></a>Criando o Projeto  
 Crie um novo projeto WPF para exibir os registros de pedido.  
  
#### <a name="to-create-a-new-wpf-project"></a>Para criar um novo projeto WPF  
  
1.  Inicie o Visual Studio.  
  
2.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
3.  Expandir **Visual c#** ou **Visual Basic**e, em seguida, selecione **Windows**.  
  
4.  Certifique-se de que **.NET Framework 4** está selecionado na caixa de combinação na parte superior da caixa de diálogo. O <xref:System.Windows.Controls.DataGrid> controle que você pode usar neste passo a passo está disponível apenas no .NET Framework 4.  
  
5.  Selecione o **aplicativo WPF** modelo de projeto.  
  
6.  Na caixa **Nome**, digite `AdventureWorksOrdersViewer`.  
  
7.  Clique em **OK**.  
  
     O Visual Studio cria o `AdventureWorksOrdersViewer` projeto.  
  
## <a name="creating-an-entity-data-model-for-the-application"></a>Criando um modelo de dados de entidade para o aplicativo  
 Antes de criar controles associados a dados, você deve definir um modelo de dados para seu aplicativo e adicioná-lo para o **fontes de dados** janela. Neste passo a passo, o modelo de dados é um modelo de dados de entidade.  
  
#### <a name="to-create-an-entity-data-model"></a>Para criar um Modelo de Dados de Entidade  
  
1. Sobre o **dados** menu, clique em **Add New Data Source** para abrir o **Data Source Configuration Wizard**.  
  
2. Sobre o **escolher um tipo de fonte de dados** , clique em **banco de dados**e, em seguida, clique em **próxima**.  
  
3. Sobre o **escolha um modelo de banco de dados** , clique em **modelo de dados de entidade**e, em seguida, clique em **próxima**.  
  
4. Sobre o **escolher conteúdo do modelo** , clique em **gerar a partir do banco de dados**e, em seguida, clique em **próxima**.  
  
5. Sobre o **escolha sua Conexão de dados** página, faça o seguinte:  
  
   - Se uma conexão de dados com o banco de dados de exemplo AdventureWorksLT estiver disponível na lista suspensa, selecione-a.  
  
      -ou-  
  
   - Clique em **nova Conexão** e criar uma conexão ao banco de dados AdventureWorksLT.  
  
     Certifique-se de que o **salvar configurações de conexão de entidade em App. config como** opção é selecionada e, em seguida, clique em **próxima**.  
  
6. Sobre o **Choose Your Database Objects** página, expanda **tabelas**e, em seguida, selecione as tabelas a seguir:  
  
   -   **SalesOrderDetail**  
  
   -   **SalesOrderHeader**  
  
7. Clique em **Finalizar**.  
  
8. Compile o projeto.  
  
## <a name="creating-data-bound-controls-that-display-the-orders"></a>Criar associação de dados controles que exibem as ordens  
 Crie controles que exibem registros de pedido, arrastando o `SalesOrderHeaders` entidade do **fontes de dados** janela para o WPF designer.  
  
#### <a name="to-create-data-bound-controls-that-display-the-order-records"></a>Para criar controles associados a dados que exibem os registros de pedido  
  
1. Na **Gerenciador de soluções**, clique duas vezes em MainWindow. XAML.  
  
    A janela é aberta no WPF Designer.  
  
2. Editar o XAML para que o **altura** e **largura** propriedades são definidas como 800  
  
3. No **fontes de dados** janela, clique no menu suspenso para o **SalesOrderHeaders** nó e selecione **detalhes**.  
  
4. Expanda o **SalesOrderHeaders** nó.  
  
5. Clique no menu suspenso ao lado **SalesOrderID** e selecione **ComboBox**.  
  
6. Para cada um dos seguintes nós filho do **SalesOrderHeaders** nó, clique no menu suspenso em seguida, no nó e selecione **None**:  
  
   - **RevisionNumber**  
  
   - **OnlineOrderFlag**  
  
   - **ShipToAddressID**  
  
   - **BillToAddressID**  
  
   - **CreditCardApprovalCode**  
  
   - **SubTotal**  
  
   - **TaxAmt**  
  
   - **Frete**  
  
   - **ROWGUID**  
  
   - **ModifiedDate**  
  
     Essa ação impede que o Visual Studio crie controles de associação de dados para esses nós na etapa seguinte. Para este passo a passo, pressupõe-se que o usuário final não precise ver esses dados.  
  
7. Dos **fontes de dados** janela, arraste a **SalesOrderHeaders** nó na janela de **o WPF Designer**.  
  
    O Visual Studio gera XAML que cria um conjunto de controles que estão associados a dados na **SalesOrderHeaders** entidade e o código que carrega os dados. Para obter mais informações sobre o XAML e o código gerado, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
8. No designer, clique na caixa de combinação lado a **ID do pedido de vendas** rótulo.  
  
9. No **propriedades** janela, selecione a caixa de seleção ao lado de **IsReadOnly** propriedade.  
  
## <a name="creating-a-datagrid-that-displays-the-order-details"></a>Criando um DataGrid que exibe os detalhes do pedido  
 Criar uma <xref:System.Windows.Controls.DataGrid> controle que exibe os detalhes do pedido, arrastando o `SalesOrderDetails` entidade entre a **fontes de dados** janela para o WPF designer.  
  
#### <a name="to-create-a-datagrid-that-displays-the-order-details"></a>Para criar um DataGrid que exibe os detalhes do pedido  
  
1. No **fontes de dados** janela, localize o **SalesOrderDetails** que é um filho do nó de **SalesOrderHeaders** nó.  
  
   > [!NOTE]
   >  Há também uma **SalesOrderDetails** nó que é um par da **SalesOrderHeaders** nó. Certifique-se de que você selecione o nó filho de **SalesOrderHeaders** nó.  
  
2. Expanda o filho **SalesOrderDetails** nó.  
  
3. Para cada um dos seguintes nós filho do **SalesOrderDetails** nó, clique no menu suspenso em seguida, no nó e selecione **None**:  
  
   - **SalesOrderID**  
  
   - **SalesOrderDetailID**  
  
   - **ROWGUID**  
  
   - **ModifiedDate**  
  
     Essa ação impede que o Visual Studio incluindo esses dados no <xref:System.Windows.Controls.DataGrid> controle que você criar na próxima etapa. Para este passo a passo, pressupõe-se que o usuário final não precise ver esses dados.  
  
4. Dos **fontes de dados** janela, arraste o filho **SalesOrderDetails** nó na janela de **o WPF Designer**.  
  
    O Visual Studio gera XAML para definir uma nova associação de dados <xref:System.Windows.Controls.DataGrid> controle e o controle aparece no designer. Visual Studio também atualiza o gerado `GetSalesOrderHeadersQuery` método no código code-behind para incluir os dados em de **SalesOrderDetails** entidade.  
  
## <a name="testing-the-application"></a>Testando o aplicativo  
 Compile e execute o aplicativo para verificar se ele exibe os registros de pedido.  
  
#### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Pressione **F5**.  
  
     O aplicativo é compilado e executado. Verifique o seguinte:  
  
    -   O **ID do pedido de vendas** caixa de combinação exibe **71774**. Isso é a primeira ID de pedido na entidade.  
  
    -   Para cada pedido de você selecionar o **ID do pedido de vendas** caixa de combinação, informações de ordem detalhadas são exibidas no <xref:System.Windows.Controls.DataGrid>.  
  
2.  Feche o aplicativo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de concluir este passo a passo, saiba como usar o **fontes de dados** janela no Visual Studio para associar o WPF controla a outros tipos de fontes de dados. Para obter mais informações, consulte [controles de WPF associar a um WCF data service](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md) e [WPF associar controles a um conjunto de dados](../data-tools/bind-wpf-controls-to-a-dataset.md).  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)   
 [Exibir dados relacionados em aplicativos WPF](../data-tools/display-related-data-in-wpf-applications.md)