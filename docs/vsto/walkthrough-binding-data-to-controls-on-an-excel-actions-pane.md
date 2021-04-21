---
title: 'Walkthrough: associar dados a controles em um painel de ações do Excel'
description: Associar dados a controles em um painel Ações no Microsoft Excel. Os controles demonstram uma relação mestre/detalhes entre tabelas em um banco de dados SQL Server.
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
ms.openlocfilehash: 377c3405211c91712f8754131d8379c3dae7e820
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824543"
---
# <a name="walkthrough-bind-data-to-controls-on-an-excel-actions-pane"></a>Walkthrough: associar dados a controles em um painel de ações do Excel
  Este tutorial demonstra a vinculação de dados a controles em um painel Ações no Microsoft Office Excel. Os controles demonstram uma relação mestre/detalhes entre tabelas em um banco de dados SQL Server.

 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Adicionando controles a uma planilha.

- Criando um controle do painel de ações.

- Adicionar controles de Windows Forms associados a dados a um controle do painel Ações.

- Mostrando o painel ações quando o aplicativo é aberto.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

- Acesso a um servidor com o banco de dados Northwind SQL Server exemplo.

- Permissões para ler e gravar no banco de dados de SQL Server.

## <a name="create-the-project"></a>Criar o projeto
 A primeira etapa é criar um projeto de pasta de trabalho do Excel.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de pasta de trabalho do Excel com o nome **meu painel Ações do Excel**. No assistente, selecione **criar um novo documento**. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre a nova pasta de trabalho do Excel no designer e adiciona o projeto do **painel minhas ações do Excel** a **Gerenciador de soluções**.

## <a name="add-a-new-data-source-to-the-project"></a>Adicionar uma nova fonte de dados ao projeto

### <a name="to-add-a-new-data-source-to-the-project"></a>Para adicionar uma nova fonte de dados ao projeto

1. Se a janela **fontes de dados** não estiver visível, exiba-a por, na barra de menus, escolhendo **Exibir**  >  **outras**  >  **fontes de dados** do Windows.

2. Escolha **Adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.

3. Selecione **banco de dados** e clique em **Avançar**.

4. Selecione uma conexão de dados para o exemplo da Northwind SQL Server Database ou adicione uma nova conexão usando o botão **nova conexão** .

5. Clique em **Próximo**.

6. Desmarque a opção para salvar a conexão, se ela estiver selecionada, e clique em **Avançar**.

7. Expanda o nó **tabelas** na janela **objetos de banco de dados** .

8. Marque a caixa de seleção ao lado da tabela **fornecedores** .

9. Expanda a tabela **produtos** e selecione **ProductName**, **CódigoDoFornecedor**, **QuantityPerUnit** e **PreçoUnitário**.

10. Clique em **Concluir**.

    O assistente adiciona a tabela de **fornecedores** e a tabela de **produtos** à janela **fontes de dados** . Ele também adiciona um conjunto de um dataset tipado ao seu projeto que está visível no **Gerenciador de soluções**.

## <a name="add-controls-to-the-worksheet"></a>Adicionar controles à planilha
 Em seguida, adicione um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle e um <xref:Microsoft.Office.Tools.Excel.ListObject> controle à primeira planilha.

### <a name="to-add-a-namedrange-control-and-a-listobject-control"></a>Para adicionar um controle NamedRange e um controle ListObject

1. Verifique se as **minhas ações do Excel Pane.xlsx** pasta de trabalho está aberta no designer do Visual Studio, com `Sheet1` exibido.

2. Na janela **fontes de dados** , expanda a tabela **fornecedores** .

3. Clique na seta suspensa no nó **nome da empresa** e, em seguida, clique em **NamedRange**.

4. Arraste **nome da empresa** da janela **fontes de dados** para a célula **a2** em `Sheet1` .

     Um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `CompanyNameNamedRange` é criado e o texto \<CompanyName> é exibido na célula **a2**. Ao mesmo tempo, um <xref:System.Windows.Forms.BindingSource> nome `suppliersBindingSource` , um adaptador de tabela e um <xref:System.Data.DataSet> são adicionados ao projeto. O controle está associado ao <xref:System.Windows.Forms.BindingSource> , que, por sua vez, está associado à <xref:System.Data.DataSet> instância.

5. Na janela **fontes de dados** , role para baixo as colunas que estão na tabela **fornecedores** . Na parte inferior da lista está a tabela **Products** ; está aqui porque é um filho da tabela **suppliers** . Selecione esta tabela de **produtos** , não a que está no mesmo nível que a tabela **fornecedores** e clique na seta suspensa exibida.

6. Clique em **ListObject** na lista suspensa e arraste a tabela **produtos** para a célula **a6** em `Sheet1` .

     Um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado `ProductNameListObject` é criado na célula **a6**. Ao mesmo tempo, um <xref:System.Windows.Forms.BindingSource> adaptador de `productsBindingSource` tabela e um nomeado são adicionados ao projeto. O controle está associado ao <xref:System.Windows.Forms.BindingSource> , que, por sua vez, está associado à <xref:System.Data.DataSet> instância.

7. Somente para C#, selecione **suppliersBindingSource** na bandeja de componentes e altere a propriedade **modificadores** para **interno** na janela **Propriedades** .

## <a name="add-controls-to-the-actions-pane"></a>Adicionar controles ao painel Ações
 Em seguida, você precisa de um controle do painel ações que tenha uma caixa de combinação.

### <a name="to-add-an-actions-pane-control"></a>Para adicionar um controle do painel Ações

1. Selecione o projeto do **painel minhas ações do Excel** em **Gerenciador de soluções**.

2. No menu **Projeto** , clique em **Adicionar Novo Item**.

3. Na caixa de diálogo **Adicionar novo item** , selecione **controle do painel Ações**, nomeie-o **ActionsControl** e clique em **Adicionar**.

### <a name="to-add-data-bound-windows-forms-controls-to-an-actions-pane-control"></a>Para adicionar controles de Windows Forms associados a dados a um controle do painel Ações

1. Nas guias **controles comuns** da caixa de **ferramentas**, arraste um <xref:System.Windows.Forms.ComboBox> controle para o controle do painel Ações.

2. Altere a propriedade **size** para **171, 21**.

3. Redimensione o controle de usuário para se ajustar à caixa de combinação.

## <a name="bind-the-control-on-the-actions-pane-to-data"></a>Associar o controle no painel ações aos dados
 Nesta seção, você definirá a fonte de dados do <xref:System.Windows.Forms.ComboBox> para a mesma fonte de dados que o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle na planilha.

### <a name="to-set-data-binding-properties-of-the-control"></a>Para definir as propriedades de vinculação de dados do controle

1. Clique com o botão direito do mouse no controle do painel Ações e clique em **Exibir código**.

2. Adicione o código a seguir ao <xref:System.Windows.Forms.UserControl.Load> evento do controle do painel Ações.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ActionsControl.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs" id="Snippet1":::

3. No C#, você deve criar um manipulador de eventos para o `ActionsControl` . Você pode posicionar esse código no `ActionsControl` Construtor. Para obter mais informações sobre como criar manipuladores de eventos, consulte [como criar manipuladores de eventos em projetos do Office](../vsto/how-to-create-event-handlers-in-office-projects.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ActionsControl.cs" id="Snippet2":::

## <a name="show-the-actions-pane"></a>Mostrar o painel Ações
 O painel ações não é visível até que você adicione o controle em tempo de execução.

#### <a name="to-show-the-actions-pane"></a>Para mostrar o painel Ações

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em *ThisWorkbook. vb* ou *ThisWorkbook. cs* e clique em **Exibir código**.

2. Crie uma nova instância do controle de usuário na `ThisWorkbook` classe.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet3":::

3. No <xref:Microsoft.Office.Tools.Excel.Workbook.Startup> manipulador de eventos do `ThisWorkbook` , adicione o controle ao painel Ações.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreActionsPaneExcelCS/ThisWorkbook.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreActionsPaneExcelVB/ThisWorkbook.vb" id="Snippet4":::

## <a name="test-the-application"></a>Testar o aplicativo
 Agora você pode testar seu documento para verificar se o painel Ações é aberto quando o documento é aberto e se os controles têm uma relação mestre/detalhes.

### <a name="to-test-your-document"></a>Para testar o documento

1. Pressione **F5** para executar o projeto.

2. Confirme se o painel Ações está visível.

3. Selecione uma empresa na caixa de listagem. Verifique se o nome da empresa está listado no <xref:Microsoft.Office.Tools.Excel.NamedRange> controle e se os detalhes do produto estão listados no <xref:Microsoft.Office.Tools.Excel.ListObject> controle.

4. Selecione várias empresas para verificar se os detalhes do produto e o nome da empresa são alterados conforme apropriado.

## <a name="next-steps"></a>Próximas etapas
 Estas são algumas tarefas que podem vir a seguir:

- Vinculação de dados a controles no Word. Para obter mais informações, consulte [Walkthrough: associar dados a controles em um painel de ações do Word](../vsto/walkthrough-binding-data-to-controls-on-a-word-actions-pane.md).

- Implantando o projeto. Para obter mais informações, consulte [implantar uma solução do Office usando o ClickOnce](../vsto/deploying-an-office-solution-by-using-clickonce.md).

## <a name="see-also"></a>Consulte também
- [Visão geral do painel Ações](../vsto/actions-pane-overview.md)
- [Como: gerenciar o layout de controle em painéis de ações](../vsto/how-to-manage-control-layout-on-actions-panes.md)
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
