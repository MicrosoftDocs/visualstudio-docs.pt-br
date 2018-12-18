---
title: 'Passo a passo: Associar dados a controles em um painel de ações do Word'
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
ms.openlocfilehash: 17daf186920be45a70200cd896a390ab74c4c6d0
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49873884"
---
# <a name="walkthrough-bind-data-to-controls-on-a-word-actions-pane"></a>Passo a passo: Associar dados a controles em um painel de ações do Word
  Este passo a passo demonstra a associação de dados a controles em um painel de ações no Word. Os controles de demonstram uma relação mestre/detalhes entre tabelas em um banco de dados do SQL Server.  
  
 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Criando um painel de ações com controles de formulários do Windows que estão associados aos dados.  
  
-   Usando uma relação mestre/detalhes para exibir dados nos controles.  
  
-   Mostre o painel de ações quando o aplicativo é aberto.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].  
  
-   Acesso a um servidor com o banco de dados de exemplo Northwind do SQL Server.  
  
-   Permissões para ler e gravar no banco de dados do SQL Server.  
  
## <a name="create-the-project"></a>Criar o projeto  
 A primeira etapa é criar um projeto de Documento do Word.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar um projeto de documento do Word com o nome **meu painel de ações do Word**. No assistente, selecione **criar um novo documento**.  
  
     Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     Visual Studio abre o novo documento do Word no designer e adiciona o **meu painel de ações do Word** projeto ao **Gerenciador de soluções**.  
  
## <a name="add-controls-to-the-actions-pane"></a>Adicionar controles ao painel de ações  
 Para este passo a passo, você precisa de um controle do painel de ações que contém controles de Windows Forms associado a dados. Adicionar uma fonte de dados para o projeto e, em seguida, arraste os controles do **fontes de dados** janela para o controle do painel Ações.  
  
### <a name="to-add-an-actions-pane-control"></a>Para adicionar um controle do painel Ações  
  
1.  Selecione o **meu painel de ações do Word** project no **Gerenciador de soluções**.  
  
2.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
3.  No **Adicionar Novo Item** caixa de diálogo, selecione **controle do painel Ações**, nomeie- **ActionsControl**e, em seguida, clique em **adicionar**.  
  
### <a name="to-add-a-data-source-to-the-project"></a>Para adicionar uma fonte de dados ao projeto  
  
1. Se o **fontes de dados** janela não estiver visível, exibi-lo, na barra de menus, escolhendo **exibição** > **Other Windows**  >   **Fontes de dados**.  
  
   > [!NOTE]  
   >  Se **Show Data Sources** não estiver disponível, clique no documento do Word e, em seguida, verifique novamente.  
  
2. Clique em **Add New Data Source** para iniciar o **Data Source Configuration Wizard**.  
  
3. Selecione **banco de dados** e, em seguida, clique em **próxima**.  
  
4. Selecione uma conexão de dados para o banco de dados do SQL Server de exemplo Northwind, ou adicionar uma nova conexão usando o **nova Conexão** botão.  
  
5. Clique em **Avançar**.  
  
6. Desmarque a opção para salvar a conexão se ela está selecionada e clique **próxima**.  
  
7. Expanda o **tabelas** nó na **objetos de banco de dados** janela.  
  
8. Marque a caixa de seleção ao lado de **fornecedores** e **produtos** tabelas.  
  
9. Clique em **Finalizar**.  
  
   O assistente adiciona as **fornecedores** tabela e **produtos** de tabela para o **fontes de dados** janela. Ele também adiciona um dataset tipado ao seu projeto que está visível no **Gerenciador de soluções**.  
  
### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>Para adicionar controles de Windows Forms associados a dados a um controle do painel Ações  
  
1.  No **fontes de dados** janela, expanda o **fornecedores** tabela.  
  
2.  Clique na seta suspensa na **nome da empresa** nó e selecione **ComboBox**.  
  
3.  Arraste **CompanyName** da **fontes de dados** janela para o controle do painel Ações.  
  
     Um <xref:System.Windows.Forms.ComboBox> controle é criado no controle do painel Ações. Ao mesmo tempo, uma <xref:System.Windows.Forms.BindingSource> nomeado `SuppliersBindingSource`, um adaptador de tabela e um <xref:System.Data.DataSet> são adicionados ao projeto na bandeja de componentes.  
  
4.  Selecione `SuppliersBindingNavigator` no **componente** bandeja e pressione **excluir**. Você não usará o `SuppliersBindingNavigator` neste passo a passo.  
  
    > [!NOTE]  
    >  Excluindo o `SuppliersBindingNavigator` não remove todo o código que foi gerado para ele. Você pode remover esse código.  
  
5.  Mover a caixa de combinação para que ele está sob o rótulo e a alteração a **tamanho** propriedade **171, 21**.  
  
6.  No **fontes de dados** janela, expanda o **produtos** tabela que é um filho do **fornecedores** tabela.  
  
7.  Clique na seta suspensa na **ProductName** nó e selecione **ListBox**.  
  
8.  Arraste **ProductName** para o controle do painel Ações.  
  
     Um <xref:System.Windows.Forms.ListBox> controle é criado no controle do painel Ações. Ao mesmo tempo, uma <xref:System.Windows.Forms.BindingSource> denominado `ProductBindingSource` e um adaptador de tabela são adicionados ao projeto na bandeja de componentes.  
  
9. Mover a caixa de listagem para que ele está sob o rótulo e a alteração a **tamanho** propriedade **171,95**.  
  
10. Arraste uma <xref:System.Windows.Forms.Button> do **caixa de ferramentas** para o painel de ações de controle e coloque-o abaixo da caixa de listagem.  
  
11. Clique com botão direito do <xref:System.Windows.Forms.Button>, clique em **propriedades** no menu de atalho e altere as propriedades a seguir.  
  
    |Propriedade|Valor|  
    |--------------|-----------|  
    |**Nome**|**Inserir**|  
    |**Texto**|**Inserir**|  
  
12. Redimensione o controle de usuário para ajustar os controles.  
  
## <a name="set-up-the-data-source"></a>Configurar a fonte de dados  
 Para configurar a fonte de dados, adicione código para o <xref:System.Windows.Forms.UserControl.Load> eventos do controle do painel Ações para preencher o controle com os dados do <xref:System.Data.DataTable>e defina o <xref:System.Windows.Forms.Binding.DataSource%2A> e <xref:System.Windows.Forms.BindingSource.DataMember%2A> propriedades para cada controle.  
  
### <a name="to-load-the-control-with-data"></a>Para carregar o controle com os dados  
  
1.  No <xref:System.Windows.Forms.UserControl.Load> manipulador de eventos do `ActionsControl` , adicione o código a seguir.  
  
     [!code-vb[Trin_VstcoreActionsPaneWord#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#1)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#1](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#1)]  
  
2.  No c#, você deve anexar o manipulador de eventos para o <xref:System.Windows.Forms.UserControl.Load> eventos. Você pode colocar esse código na `ActionsControl` construtor, após a chamada para `InitializeComponent`. Para obter mais informações sobre como criar manipuladores de eventos, consulte [como: criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#33](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#33)]  
  
### <a name="to-set-data-binding-properties-of-the-controls"></a>Definir as propriedades de associação de dados dos controles  
  
1.  Selecione o `CompanyNameComboBox` controle.  
  
2.  No **propriedades** janela, clique no botão à direita do **DataSource** propriedade e selecione **suppliersBindingSource**.  
  
3.  Clique no botão à direita do **DisplayMember** propriedade e selecione **CompanyName**.  
  
4.  Expanda o **DataBindings** propriedade, clique no botão à direita do **texto** propriedade e selecione **None**.  
  
5.  Selecione o `ProductNameListBox` controle.  
  
6.  No **propriedades** janela, clique no botão à direita do **DataSource** propriedade e selecione **productsBindingSource**.  
  
7.  Clique no botão à direita do **DisplayMember** propriedade e selecione **ProductName**.  
  
8.  Expanda o **DataBindings** propriedade, clique no botão à direita do **SelectedValue** propriedade e selecione **None**.  
  
## <a name="add-a-method-to-insert-data-into-a-table"></a>Adicione um método para inserir dados em uma tabela  
 A próxima tarefa é ler os dados os controles associados e popular uma tabela em seu documento do Word. Primeiro, crie um procedimento para formatar os cabeçalhos na tabela e, em seguida, adicione o `AddData` método para criar e formatar uma tabela do Word.  
  
### <a name="to-format-the-table-headings"></a>Para formatar os títulos de tabela  
  
1.  No `ActionsControl` de classe, crie um método para formatar os títulos da tabela.  
  
     [!code-vb[Trin_VstcoreActionsPaneWord#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#2)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#2](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#2)]  
  
### <a name="to-create-the-table"></a>Para criar a tabela  
  
1.  No `ActionsControl` de classe, escrever um método que criará uma tabela, se um existe e adicionar dados no painel Ações à tabela.  
  
     [!code-vb[Trin_VstcoreActionsPaneWord#3](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#3)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#3](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#3)]  
  
### <a name="to-insert-text-into-a-word-table"></a>Para inserir texto em uma tabela do Word  
  
1.  Adicione o seguinte código para o <xref:System.Windows.Forms.Control.Click> manipulador de eventos do **inserir** botão.  
  
     [!code-vb[Trin_VstcoreActionsPaneWord#4](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb#4)]
     [!code-csharp[Trin_VstcoreActionsPaneWord#4](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#4)]  
  
2.  No c#, você deve criar um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento do botão.  Você pode colocar esse código na <xref:System.Windows.Forms.UserControl.Load> manipulador de eventos do `ActionsControl` classe.  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#5](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs#5)]  
  
## <a name="show-the-actions-pane"></a>Mostrar o painel de ações  
 O painel de ações se torna visível depois que os controles são adicionados a ele.  
  
### <a name="to-show-the-actions-pane"></a>Para mostrar o painel de ações  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **ThisDocument. vb** ou **ThisDocument.cs**e, em seguida, clique em **Exibir código** no menu de atalho.  
  
2.  Criar uma nova instância do controle na parte superior do `ThisDocument` de classe para que ele se parece com o exemplo a seguir.  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#6](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#6)]
     [!code-vb[Trin_VstcoreActionsPaneWord#6](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#6)]  
  
3.  Adicione código para o <xref:Microsoft.Office.Tools.Word.Document.Startup> manipulador de eventos do `ThisDocument` para que ele se parece com o exemplo a seguir.  
  
     [!code-csharp[Trin_VstcoreActionsPaneWord#7](../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs#7)]
     [!code-vb[Trin_VstcoreActionsPaneWord#7](../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb#7)]  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Agora você pode testar seu documento para verificar se o painel de ações é exibida quando o documento é aberto. Testar a relação mestre/detalhes nos controles no painel Ações e certifique-se de que os dados são preenchidos em uma palavra tabela quando o **inserir** botão é clicado.  
  
### <a name="to-test-your-document"></a>Para testar o documento  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Confirme se o painel de ações está visível.  
  
3.  Selecione uma empresa na caixa de combinação e verificar se os itens na **produtos** alteração da caixa de lista.  
  
4.  Selecione um produto, clique em **inserir** no painel de ações e verificar se os detalhes do produto são adicionados à tabela no Word.  
  
5.  Inserir produtos adicionais de várias empresas.  
  
## <a name="next-steps"></a>Próximas etapas  
 Este passo a passo mostra as Noções básicas de vinculação de dados a controles em um painel de ações no Word. Estas são algumas tarefas que podem vir a seguir:  
  
-   Associando dados a controles no Excel. Para obter mais informações, consulte [instruções passo a passo: associar dados a controles em um painel de ações do Excel](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md).  
  
-   Implantar o projeto. Para obter mais informações, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral do painel de ações](../vsto/actions-pane-overview.md)   
 [Como: adicionar um painel de ações a documentos do Word ou pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)   
 [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)  
  
  