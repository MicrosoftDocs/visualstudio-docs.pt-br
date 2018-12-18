---
title: 'Passo a passo: Associar dados a controles em um painel de ações do Excel'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], data binding
- actions panes [Office development in Visual Studio], data binding
- data binding [Office development in Visual Studio], smart documents
- data binding [Office development in Visual Studio], actions panes
- actions panes [Office development in Visual Studio], binding controls
- smart documents [Office development in Visual Studio], data binding
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 8fbc1baa66dc98b2c5eec27c2a86e0fde3c5e967
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942641"
---
# <a name="walkthrough-bind-data-to-controls-on-an-excel-actions-pane"></a>Passo a passo: Associar dados a controles em um painel de ações do Excel
  Este passo a passo demonstra a associação de dados a controles em um painel de ações no Microsoft Office Excel. Os controles de demonstram uma relação mestre/detalhes entre tabelas em um banco de dados do SQL Server.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Adicionando controles a uma planilha.  
  
-   Criando um controle do painel Ações.  
  
-   Adicionando controles de Windows Forms associados a dados para um controle do painel Ações.  
  
-   Quando o aplicativo é aberto, mostrando o painel de ações.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].  
  
-   Acesso a um servidor com o banco de dados de exemplo Northwind do SQL Server.  
  
-   Permissões para ler e gravar no banco de dados do SQL Server.  
  
## <a name="create-the-project"></a>Criar o projeto  
 A primeira etapa é criar um projeto de pasta de trabalho do Excel.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de pasta de trabalho do Excel com o nome **meu painel de ações do Excel**. No assistente, selecione **criar um novo documento**. Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o **meu painel de ações do Excel** projeto ao **Gerenciador de soluções**.  
  
## <a name="add-a-new-data-source-to-the-project"></a>Adicionar uma nova fonte de dados ao projeto  
  
### <a name="to-add-a-new-data-source-to-the-project"></a>Para adicionar uma nova fonte de dados ao projeto  
  
1. Se o **fontes de dados** janela não estiver visível, exibi-lo, na barra de menus, escolhendo **exibição** > **Other Windows**  >   **Fontes de dados**.  
  
2. Escolher **Add New Data Source** para iniciar o **Data Source Configuration Wizard**.  
  
3. Selecione **banco de dados** e, em seguida, clique em **próxima**.  
  
4. Selecione uma conexão de dados para o banco de dados do SQL Server de exemplo Northwind, ou adicionar uma nova conexão usando o **nova Conexão** botão.  
  
5. Clique em **Avançar**.  
  
6. Desmarque a opção para salvar a conexão se ela está selecionada e clique **próxima**.  
  
7. Expanda o **tabelas** nó na **objetos de banco de dados** janela.  
  
8. Marque a caixa de seleção ao lado de **fornecedores** tabela.  
  
9. Expanda o **produtos** de tabela e selecione **ProductName**, **SupplierID**, **QuantityPerUnit**, e **UnitPrice**.  
  
10. Clique em **Finalizar**.  
  
    O assistente adiciona as **fornecedores** tabela e **produtos** de tabela para o **fontes de dados** janela. Ele também adiciona um dataset tipado ao seu projeto que está visível no **Gerenciador de soluções**.  
  
## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha  
 Em seguida, adicione uma <xref:Microsoft.Office.Tools.Excel.NamedRange> controle e um <xref:Microsoft.Office.Tools.Excel.ListObject> controle para a primeira planilha.  
  
### <a name="to-add-a-namedrange-control-and-a-listobject-control"></a>Para adicionar um controle NamedRange e um controle ListObject  
  
1.  Verifique se que o **Meus Pane.xlsx de ações do Excel** pasta de trabalho é aberta no designer do Visual Studio, com `Sheet1` exibido.  
  
2.  No **fontes de dados** janela, expanda o **fornecedores** tabela.  
  
3.  Clique na seta suspensa na **nome da empresa** nó e clique **NamedRange**.  
  
4.  Arraste **nome da empresa** da **fontes de dados** janela à célula **A2** em `Sheet1`.  
  
     Um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `CompanyNameNamedRange` é criado e o texto \<CompanyName > aparece na célula **A2**. Ao mesmo tempo, uma <xref:System.Windows.Forms.BindingSource> nomeado `suppliersBindingSource`, um adaptador de tabela e um <xref:System.Data.DataSet> são adicionados ao projeto. O controle é associado à <xref:System.Windows.Forms.BindingSource>, que por sua vez é associado a <xref:System.Data.DataSet> instância.  
  
5.  No **fontes de dados** , role para baixo após as colunas que estão sob o **fornecedores** tabela. Na parte inferior da lista é o **produtos** tabela; ele está aqui porque ele é um filho do **fornecedores** tabela. Selecione esta opção **produtos** da tabela, não aquela que está no mesmo nível que o **fornecedores** de tabela e, em seguida, clique na seta suspensa exibida.  
  
6.  Clique em **ListObject** na lista suspensa e, em seguida, arraste o **produtos** tabela para a célula **A6** em `Sheet1`.  
  
     Um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado `ProductNameListObject` é criado na célula **A6**. Ao mesmo tempo, uma <xref:System.Windows.Forms.BindingSource> denominado `productsBindingSource` e um adaptador de tabela são adicionados ao projeto. O controle é associado à <xref:System.Windows.Forms.BindingSource>, que por sua vez é associado a <xref:System.Data.DataSet> instância.  
  
7.  Apenas para c#, selecione **suppliersBindingSource** na bandeja de componentes e altere o **modificadores** propriedade a ser **interno** no **propriedades** janela.  
  
## <a name="add-controls-to-the-actions-pane"></a>Adicionar controles ao painel de ações  
 Em seguida, você precisa de um controle do painel de ações que tenha uma caixa de combinação.  
  
### <a name="to-add-an-actions-pane-control"></a>Para adicionar um controle do painel Ações  
  
1.  Selecione o **meu painel de ações do Excel** project no **Gerenciador de soluções**.  
  
2.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
3.  No **Adicionar Novo Item** caixa de diálogo, selecione **controle do painel Ações**, nomeie- **ActionsControl**e clique em **adicionar**.  
  
### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>Para adicionar controles de Windows Forms associados a dados a um controle do painel Ações  
  
1.  Dos **controles comuns** guias da **caixa de ferramentas**, arraste um <xref:System.Windows.Forms.ComboBox> controle para o controle do painel Ações.  
  
2.  Alterar o **tamanho** propriedade **171, 21**.  
  
3.  Redimensione o controle de usuário de acordo com a caixa de combinação.  
  
## <a name="bind-the-control-on-the-actions-pane-to-data"></a>Associar o controle no painel de ações aos dados  
 Nesta seção, você definirá a fonte de dados do <xref:System.Windows.Forms.ComboBox> à mesma fonte de dados como o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle na planilha.  
  
### <a name="to-set-data-binding-properties-of-the-control"></a>Definir as propriedades de associação de dados do controle  
  
1.  O controle do painel de ações com o botão direito e, em seguida, clique em **Exibir código**.  
  
2.  Adicione o seguinte código para o <xref:System.Windows.Forms.UserControl.Load> eventos do controle do painel Ações.  
  
     [!code-vb[Trin_VstcoreActionsPaneExcel#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ActionsControl.vb#1)]
     [!code-csharp[Trin_VstcoreActionsPaneExcel#1](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs#1)]  
  
3.  No c#, você deve criar um manipulador de eventos para o `ActionsControl`. Você pode colocar esse código no `ActionsControl` construtor. Para obter mais informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  
  
     [!code-csharp[Trin_VstcoreActionsPaneExcel#2](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs#2)]  
  
## <a name="show-the-actions-pane"></a>Mostrar o painel de ações  
 O painel de ações não estarão visível até que você adicione o controle em tempo de execução.  
  
#### <a name="to-show-the-actions-pane"></a>Para mostrar o painel de ações  
  
1.  Na **Gerenciador de soluções**, clique com botão direito *ThisWorkbook. vb* ou *ThisWorkbook.cs*e, em seguida, clique em **Exibir código**.  
  
2.  Criar uma nova instância do controle de usuário na `ThisWorkbook` classe.  
  
     [!code-csharp[Trin_VstcoreActionsPaneExcel#3](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs#3)]
     [!code-vb[Trin_VstcoreActionsPaneExcel#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb#3)]  
  
3.  No <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> manipulador de eventos do `ThisWorkbook`, adicione o controle ao painel de ações.  
  
     [!code-csharp[Trin_VstcoreActionsPaneExcel#4](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs#4)]
     [!code-vb[Trin_VstcoreActionsPaneExcel#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb#4)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Agora você pode testar seu documento para verificar se o painel de ações é aberto quando o documento é aberto e que os controles têm uma relação mestre/detalhes.  
  
### <a name="to-test-your-document"></a>Para testar o documento  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Confirme se o painel de ações está visível.  
  
3.  Selecione uma empresa na caixa de listagem. Verifique se o nome da empresa é listado na <xref:Microsoft.Office.Tools.Excel.NamedRange> controle e que os detalhes do produto estão listados no <xref:Microsoft.Office.Tools.Excel.ListObject> controle.  
  
4.  Selecione várias empresas para verificar o nome da empresa e detalhes do produto alterar conforme apropriado.  
  
## <a name="next-steps"></a>Próximas etapas  
 Estas são algumas tarefas que podem vir a seguir:  
  
-   Associando dados a controles no Word. Para obter mais informações, consulte [instruções passo a passo: associar dados a controles em um painel de ações do Word](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md).  
  
-   Implantar o projeto. Para obter mais informações, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do painel de ações](../vsto/actions-pane-overview.md)   
 [Como: gerenciar o layout do controle em painéis de ações](../vsto/how-to-manage-control-layout-on-actions-panes.md)   
 [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)  
  
  