---
title: 'Walkthrough: associar dados a controles em um painel de ações do Word'
description: Associar dados a controles em um painel Ações no Microsoft Word. Os controles demonstram uma relação mestre/detalhes entre tabelas em um banco de dados SQL Server.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: d94891520695117c7a395f81feda81e52f909fe6
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824491"
---
# <a name="walkthrough-bind-data-to-controls-on-a-word-actions-pane"></a>Walkthrough: associar dados a controles em um painel de ações do Word
  Este tutorial demonstra a vinculação de dados a controles em um painel Ações no Word. Os controles demonstram uma relação mestre/detalhes entre tabelas em um banco de dados SQL Server.

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Criar um painel de ações com controles de Windows Forms que são associados a dados.

- Usando uma relação mestre/detalhes para exibir dados nos controles.

- Mostrar o painel ações quando o aplicativo for aberto.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].

- Acesso a um servidor com o banco de dados Northwind SQL Server exemplo.

- Permissões para ler e gravar no banco de dados de SQL Server.

## <a name="create-the-project"></a>Criar o projeto
 A primeira etapa é criar um projeto de Documento do Word.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de documento do Word com o nome **My Word Actions painel**. No assistente, selecione **criar um novo documento**.

     Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre o novo documento do Word no designer e adiciona o projeto do **painel minhas ações do Word** a **Gerenciador de soluções**.

## <a name="add-controls-to-the-actions-pane"></a>Adicionar controles ao painel Ações
 Para este passo a passos, você precisa de um controle do painel ações que contém controles de Windows Forms associados a dados. Adicione uma fonte de dados ao projeto e arraste os controles da janela **fontes de dados** para o controle do painel Ações.

### <a name="to-add-an-actions-pane-control"></a>Para adicionar um controle do painel Ações

1. Selecione o projeto do **painel minhas ações do Word** no **Gerenciador de soluções**.

2. No menu **Projeto** , clique em **Adicionar Novo Item**.

3. Na caixa de diálogo **Adicionar novo item** , selecione **controle do painel Ações**, nomeie-o **ActionsControl** e clique em **Adicionar**.

### <a name="to-add-a-data-source-to-the-project"></a>Para adicionar uma fonte de dados ao projeto

1. Se a janela **fontes de dados** não estiver visível, exiba-a por, na barra de menus, escolhendo **Exibir**  >  **outras**  >  **fontes de dados** do Windows.

   > [!NOTE]
   > Se **mostrar fontes de dados** não estiver disponível, clique no documento do Word e, em seguida, verifique novamente.

2. Clique em **Adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.

3. Selecione **banco de dados** e clique em **Avançar**.

4. Selecione uma conexão de dados para o exemplo da Northwind SQL Server Database ou adicione uma nova conexão usando o botão **nova conexão** .

5. Clique em **Próximo**.

6. Desmarque a opção para salvar a conexão, se ela estiver selecionada, e clique em **Avançar**.

7. Expanda o nó **tabelas** na janela **objetos de banco de dados** .

8. Marque a caixa de seleção ao lado das tabelas **fornecedores** e **produtos** .

9. Clique em **Concluir**.

   O assistente adiciona a tabela de **fornecedores** e a tabela de **produtos** à janela **fontes de dados** . Ele também adiciona um conjunto de um dataset tipado ao seu projeto que está visível no **Gerenciador de soluções**.

### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>Para adicionar controles de Windows Forms associados a dados a um controle do painel Ações

1. Na janela **fontes de dados** , expanda a tabela **fornecedores** .

2. Clique na seta suspensa no nó **nome da empresa** e selecione **ComboBox**.

3. Arraste **CompanyName** da janela **fontes de dados** para o controle do painel Ações.

     Um <xref:System.Windows.Forms.ComboBox> controle é criado no controle do painel Ações. Ao mesmo tempo, um <xref:System.Windows.Forms.BindingSource> nome `SuppliersBindingSource` , um adaptador de tabela e um <xref:System.Data.DataSet> são adicionados ao projeto na bandeja de componentes.

4. Selecione `SuppliersBindingNavigator` na bandeja do **componente** e pressione **excluir**. Você não usará o `SuppliersBindingNavigator` nesta explicação.

    > [!NOTE]
    > Excluir o `SuppliersBindingNavigator` não remove todo o código que foi gerado para ele. Você pode remover este código.

5. Mova a caixa de combinação de forma que ela esteja sob o rótulo e altere a propriedade **tamanho** para **171, 21**.

6. Na janela **fontes de dados** , expanda a tabela **produtos** que é um filho da tabela **fornecedores** .

7. Clique na seta suspensa no nó **NomeDoProduto** e selecione **ListBox**.

8. Arraste **ProductName** para o controle do painel Ações.

     Um <xref:System.Windows.Forms.ListBox> controle é criado no controle do painel Ações. Ao mesmo tempo, um <xref:System.Windows.Forms.BindingSource> adaptador de `ProductBindingSource` tabela e um nomeado são adicionados ao projeto na bandeja de componentes.

9. Mova a caixa de listagem para que ela fique sob o rótulo e altere a propriedade **size** para **171, 95**.

10. Arraste um <xref:System.Windows.Forms.Button> da caixa de **ferramentas** para o controle do painel Ações e coloque-o abaixo da lista.

11. Clique com o botão direito do mouse em <xref:System.Windows.Forms.Button> , clique em **Propriedades** no menu de atalho e altere as propriedades a seguir.

    |Propriedade|Valor|
    |--------------|-----------|
    |**Nome**|**Inserção**|
    |**Text**|**Inserção**|

12. Redimensione o controle de usuário para ajustá-lo aos controles.

## <a name="set-up-the-data-source"></a>Configurar a fonte de dados
 Para configurar a fonte de dados, adicione o código ao <xref:System.Windows.Forms.UserControl.Load> evento do controle painel Ações para preencher o controle com dados do e <xref:System.Data.DataTable> definir as <xref:System.Windows.Forms.Binding.DataSource%2A> <xref:System.Windows.Forms.BindingSource.DataMember%2A> Propriedades e para cada controle.

### <a name="to-load-the-control-with-data"></a>Para carregar o controle com dados

1. No <xref:System.Windows.Forms.UserControl.Load> manipulador de eventos da `ActionsControl` classe, adicione o código a seguir.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet1":::

2. No C#, você deve anexar o manipulador de eventos ao <xref:System.Windows.Forms.UserControl.Load> evento. Você pode posicionar esse código no `ActionsControl` Construtor, após a chamada para `InitializeComponent` . Para obter mais informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet33":::

### <a name="to-set-data-binding-properties-of-the-controls"></a>Para definir as propriedades de vinculação de dados dos controles

1. Selecione o controle `CompanyNameComboBox`.

2. Na janela **Propriedades** , clique no botão à direita da propriedade **DataSource** e selecione **suppliersBindingSource**.

3. Clique no botão à direita da propriedade **DisplayMember** e selecione **CompanyName**.

4. Expanda a propriedade **DataBindings** , clique no botão à direita da propriedade **Text** e selecione **nenhum**.

5. Selecione o controle `ProductNameListBox`.

6. Na janela **Propriedades** , clique no botão à direita da propriedade **DataSource** e selecione **ProductsBindingSource**.

7. Clique no botão à direita da propriedade **DisplayMember** e selecione **ProductName**.

8. Expanda a propriedade **DataBindings** , clique no botão à direita da propriedade **SelectedValue** e selecione **nenhum**.

## <a name="add-a-method-to-insert-data-into-a-table"></a>Adicionar um método para inserir dados em uma tabela
 A próxima tarefa é ler os dados dos controles associados e preencher uma tabela em seu documento do Word. Primeiro, crie um procedimento para formatar os cabeçalhos na tabela e, em seguida, adicione o `AddData` método para criar e formatar uma tabela do Word.

### <a name="to-format-the-table-headings"></a>Para formatar os títulos de tabela

1. Na `ActionsControl` classe, crie um método para formatar os cabeçalhos da tabela.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet2":::

### <a name="to-create-the-table"></a>Para criar a tabela

1. Na `ActionsControl` classe, escreva um método que criará uma tabela se ela ainda não existir e adicione dados do painel Ações à tabela.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet3":::

### <a name="to-insert-text-into-a-word-table"></a>Para inserir texto em uma tabela do Word

1. Adicione o código a seguir ao <xref:System.Windows.Forms.Control.Click> manipulador de eventos do botão **Inserir** .

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ActionsControl.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet4":::

2. No C#, você deve criar um manipulador de eventos para o <xref:System.Windows.Forms.Control.Click> evento do botão.  Você pode posicionar esse código no <xref:System.Windows.Forms.UserControl.Load> manipulador de eventos da `ActionsControl` classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ActionsControl.cs" id="Snippet5":::

## <a name="show-the-actions-pane"></a>Mostrar o painel Ações
 O painel ações se torna visível depois que os controles são adicionados a ele.

### <a name="to-show-the-actions-pane"></a>Para mostrar o painel Ações

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **ThisDocument. vb** ou **ThisDocument. cs** e clique em **Exibir código** no menu de atalho.

2. Crie uma nova instância do controle na parte superior da `ThisDocument` classe para que ela se pareça com o exemplo a seguir.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet6":::

3. Adicione código ao <xref:Microsoft.Office.Tools.Word.Document.Startup> manipulador de eventos do `ThisDocument` para que ele seja semelhante ao exemplo a seguir.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneWordCS/ThisDocument.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneWordVB/ThisDocument.vb" id="Snippet7":::

## <a name="test-the-application"></a>Testar o aplicativo
 Agora você pode testar seu documento para verificar se o painel Ações aparece quando o documento é aberto. Teste a relação mestre/detalhes nos controles do painel Ações e certifique-se de que os dados sejam preenchidos em uma tabela do Word quando o botão **Inserir** for clicado.

### <a name="to-test-your-document"></a>Para testar o documento

1. Pressione **F5** para executar o projeto.

2. Confirme se o painel Ações está visível.

3. Selecione uma empresa na caixa de combinação e verifique se os itens na caixa de listagem **produtos** são alterados.

4. Selecione um produto, clique em **Inserir** no painel Ações e verifique se os detalhes do produto foram adicionados à tabela no Word.

5. Insira produtos adicionais de várias empresas.

## <a name="next-steps"></a>Próximas etapas
 Este tutorial mostra as noções básicas de vinculação de dados a controles em um painel Ações no Word. Estas são algumas tarefas que podem vir a seguir:

- Vinculação de dados a controles no Excel. Para obter mais informações, consulte [Walkthrough: associar dados a controles em um painel de ações do Excel](../vsto/walkthrough-binding-data-to-controls-on-an-excel-actions-pane.md).

- Implantando o projeto. Para obter mais informações, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).

## <a name="see-also"></a>Consulte também
- [Visão geral do painel Ações](../vsto/actions-pane-overview.md)
- [Como: adicionar um painel de ações a documentos do Word ou a pastas de trabalho do Excel](../vsto/how-to-add-an-actions-pane-to-word-documents-or-excel-workbooks.md)
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
