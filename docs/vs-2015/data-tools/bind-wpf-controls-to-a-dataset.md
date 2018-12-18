---
title: Associar controles WPF a um conjunto de dados | Microsoft Docs
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
ms.assetid: 177420b9-568b-4dad-9d16-1b0e98a24d71
caps.latest.revision: 35
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 9b77e8211d8f76627f16f96abed8a61e6dae03d7
ms.sourcegitcommit: d462dd10746624ad139f1db04edd501e7737d51e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2018
ms.locfileid: "50219790"
---
# <a name="bind-wpf-controls-to-a-dataset"></a>Associar controles do WPF a um conjunto de dados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
Neste passo a passo, você criará um aplicativo WPF que contém controles de associação de dados. Os controles são associados a registros de produto que são encapsulados em um conjunto de dados. Você também adicionará botões para navegar pelos produtos e salvar alterações em registros de produtos.  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Criando um aplicativo WPF e um conjunto de dados gerado a partir de dados no banco de dados de exemplo AdventureWorksLT.  
  
- Criando um conjunto de controles ligados a dados ao arrastar uma tabela de dados das **fontes de dados** janela para uma janela no Designer do WPF.  
  
- Criando botões que navegam para a frente e para trás nos registros de produtos.  
  
- Criando um botão para salvar as alterações que os usuários fazem nos registros de produtos na tabela de dados e na fonte de dados subjacente.  
  
   [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
- [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]  
  
- Acesso a uma instância em execução do SQL Server ou SQL Server Express que tenha o banco de dados de exemplo AdventureWorksLT anexado a ele. Você pode baixar o banco de dados AdventureWorksLT a [site da CodePlex](http://go.microsoft.com/fwlink/?linkid=87843).  
  
  Conhecimento prévio dos conceitos a seguir também é útil, mas não é necessário para concluir o passo a passo:  
  
- Conjuntos de dados e TableAdapters. Para obter mais informações, consulte [ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md) e [visão geral de TableAdapter](../data-tools/tableadapter-overview.md).  
  
- Trabalhando com o WPF Designer. Para obter mais informações, consulte [WPF e Silverlight Designer Overview](http://msdn.microsoft.com/en-us/570b7a5c-0c86-4326-a371-c9b63378fc62).  
  
- Associação de dados do WPF. Para obter mais informações, consulte [Visão geral de vinculação de dados](http://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211).  
  
## <a name="create-the-project"></a>Criar o projeto  
 Crie um novo projeto WPF. O projeto exibirá registros de produtos.  
  
#### <a name="to-create-the-project"></a>Para criar o projeto  
  
1.  Inicie o Visual Studio.  
  
2.  No menu **Arquivo**, aponte para **Novo** e clique em **Projeto**.  
  
3.  Expandir **Visual Basic** ou **Visual c#** e, em seguida, selecione **Windows**.  
  
4.  Selecione o **aplicativo WPF** modelo de projeto.  
  
5.  No **nome** , digite `AdventureWorksProductsEditor` e clique em **Okey**.  
  
     O Visual Studio cria o `AdventureWorksProductsEditor` projeto.  
  
## <a name="create-a-dataset-for-the-application"></a>Criar um conjunto de dados para o aplicativo  
 Antes de criar controles associados a dados, você deve definir um modelo de dados para seu aplicativo e adicioná-lo para o **fontes de dados** janela. Neste passo a passo, você criará um conjunto de dados para usar como modelo de dados.  
  
#### <a name="to-create-a-dataset"></a>Para criar um conjunto de dados  
  
1.  Sobre o **dados** menu, clique em **Show Data Sources**.  
  
     O **fontes de dados** janela é aberta.  
  
2.  No **fontes de dados** janela, clique em **Add New Data Source**.  
  
     O **configuração de fonte de dados** assistente é aberto.  
  
3.  Sobre o **escolher um tipo de fonte de dados** página, selecione **banco de dados**e, em seguida, clique em **próxima**.  
  
4.  Sobre o **escolha um modelo de banco de dados** página, selecione **Dataset**e, em seguida, clique em **próxima**.  
  
5.  Sobre o **escolha sua Conexão de dados** , selecione uma das opções a seguir:  
  
    -   Se uma conexão de dados para o banco de dados de exemplo AdventureWorksLT estiver disponível na lista suspensa, selecione-o e, em seguida, clique em **próxima**.  
  
    -   Clique em **nova Conexão**e criar uma conexão ao banco de dados AdventureWorksLT.  
  
6.  Sobre o **salvar a cadeia de Conexão para o arquivo de configuração de aplicativo** página, selecione o **Sim, salvar a conexão como** caixa de seleção e, em seguida, clique em **próxima**.  
  
7.  Sobre o **Choose Your Database Objects** página, expanda **tabelas**e, em seguida, selecione o **produto (SalesLT)** tabela.  
  
8.  Clique em **Finalizar**.  
  
     Visual Studio adiciona um novo arquivo Adventureworksltdataset XSD ao projeto e ele adiciona um correspondente **AdventureWorksLTDataSet** de item para o **fontes de dados** janela. O arquivo AdventureWorksLTDataSet.xsd define um conjunto de dados tipado nomeado `AdventureWorksLTDataSet` e um TableAdapter nomeado `ProductTableAdapter`. A seguir neste passo a passo, você usará o `ProductTableAdapter` para preencher o conjunto de dados com dados e salvar as alterações no banco de dados.  
  
9. Compile o projeto.  
  
## <a name="edit-the-default-fill-method-of-the-tableadapter"></a>Editar o método de preenchimento padrão do TableAdapter  
 Para preencher o conjunto de dados com dados, use o método `Fill` do `ProductTableAdapter`. Por padrão, o método `Fill` preenche o `ProductDataTable` no `AdventureWorksLTDataSet` com todas as linhas de dados da tabela Produto. Você pode modificar esse método para retornar apenas um subconjunto das linhas. Para este passo a passo, modifique o método `Fill` para retornar somente linhas de produtos com fotos.  
  
#### <a name="to-load-product-rows-that-have-photos"></a>Para carregar as linhas de produtos que possuem fotos  
  
1.  Na **Gerenciador de soluções**, duas vezes no arquivo Adventureworksltdataset.  
  
     O designer de conjunto de dados é aberto.  
  
2.  No designer, clique com botão direito do **Fill,GetData()** de consulta e selecione **configurar**.  
  
     O **configuração do TableAdapter** assistente é aberto.  
  
3.  No **insira uma instrução SQL** página, adicione a seguinte cláusula WHERE após o `SELECT` instrução na caixa de texto.  
  
    ```  
    WHERE ThumbnailPhotoFileName <> 'no_image_available_small.gif'  
    ```  
  
4.  Clique em **Finalizar**.  
  
## <a name="define-the-user-interface"></a>Definir a interface do usuário  
 Adicione vários botões à janela, modificando o XAML no WPF Designer. A seguir neste passo a passo, você adicionará o código que permite aos usuários navegar e salvar alterações nos registros de produtos, usando esses botões.  
  
#### <a name="to-define-the-user-interface-of-the-window"></a>Para definir a interface do usuário da janela  
  
1.  Na **Gerenciador de soluções**, clique duas vezes em MainWindow. XAML.  
  
     A janela é aberta no WPF Designer.  
  
2.  Na exibição [!INCLUDE[TLA#tla_titlexaml](../includes/tlasharptla-titlexaml-md.md)] do designer, adicione o seguinte código entre as marcas `<Grid>`:  
  
    ```  
    <Grid.RowDefinitions>  
        <RowDefinition Height="75" />  
        <RowDefinition Height="625" />  
    </Grid.RowDefinitions>  
    <Button HorizontalAlignment="Left" Margin="22,20,0,24" Name="backButton" Width="75"><</Button>  
    <Button HorizontalAlignment="Left" Margin="116,20,0,24" Name="nextButton" Width="75">></Button>  
    <Button HorizontalAlignment="Right" Margin="0,21,46,24" Name="saveButton" Width="110">Save changes</Button>  
    ```  
  
3.  Compile o projeto.  
  
## <a name="createdata-bound-controls"></a>Controles associados a criar  
 Crie controles que exibem registros do cliente, arrastando o `Product` tabela do **fontes de dados** janela para o WPF Designer.  
  
#### <a name="to-create-data-bound-controls"></a>Para adicionar controles de associação de dados  
  
1.  No **fontes de dados** janela, clique no menu suspenso para o **produto** nó e selecione **detalhes**.  
  
2.  Expanda o **produto** nó.  
  
3.  Neste exemplo, alguns campos não serão exibidos, então, clique no menu suspenso ao lado de nós a seguir e selecione **None**:  
  
    -   ProductCategoryID  
  
    -   ProductModelID  
  
    -   ThumbnailPhotoFileName  
  
    -   rowguid  
  
    -   ModifiedDate  
  
4.  Clique no menu suspenso ao lado de **ThumbNailPhoto** nó e selecione **imagem**.  
  
    > [!NOTE]
    >  Por padrão, os itens na **fontes de dados** janela que representam as imagens têm seu controle padrão definido como **None**. Isso ocorre porque as imagens são armazenadas como matrizes de bytes em bancos de dados e as matrizes de bytes podem conter qualquer coisa, desde uma simples matriz de bytes até um arquivo executável de um aplicativo grande.  
  
5.  Dos **fontes de dados** janela, arraste a **produto** nó para a linha de grade sob a linha que contém os botões.  
  
     O Visual Studio gera XAML que define um conjunto de controles que estão associados a dados na **produtos** tabela. Também gera um código que carrega os dados. Para obter mais informações sobre o XAML e o código gerado, consulte [WPF associar controles a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md).  
  
6.  No designer, clique na caixa de texto ao lado de **ID do produto** rótulo.  
  
7.  No **propriedades** janela, selecione a caixa de seleção ao lado de **IsReadOnly** propriedade.  
  
## <a name="navigating-product-records"></a>Navegando nos registros de produto  
 Adicione o código que permite aos usuários percorrer os registros de produto usando o **\<** e **>** botões.  
  
#### <a name="to-enable-users-to-navigate-product-records"></a>Para permitir que os usuários naveguem nos registros do produto  
  
1.  No designer, clique duas vezes o **<** botão na superfície da janela.  
  
     Visual Studio abre o arquivo code-behind e cria um novo `backButton_Click` manipulador de eventos para o <xref:System.Windows.Controls.Primitives.ButtonBase.Click> eventos.  
  
2.  Modificar a `Window_Loaded` manipulador de eventos, portanto, o `ProductViewSource`, `AdventureWorksLTDataSet`, e `AdventureWorksLTDataSetProductTableAdapter` fora do método e acessíveis para o formulário inteiro. Declare apenas esses globais para o formulário e atribuí-los dentro de `Window_Loaded` manipulador de eventos semelhante à seguinte:  
  
     [!code-csharp[Data_WPFDATASET#1](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#1)]
     [!code-vb[Data_WPFDATASET#1](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#1)]  
  
3.  Adicione o seguinte código ao manipulador de eventos do `backButton_Click`:  
  
     [!code-csharp[Data_WPFDATASET#2](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#2)]
     [!code-vb[Data_WPFDATASET#2](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#2)]  
  
4.  Retorne ao designer e clique duas vezes o **>** botão.  
  
5.  Adicione o seguinte código ao manipulador de eventos do `nextButton_Click`:  
  
     [!code-csharp[Data_WPFDATASET#3](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#3)]
     [!code-vb[Data_WPFDATASET#3](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#3)]  
  
## <a name="savechanges-to-product-records"></a>Salvar alterações em registros de produtos  
 Adicione o código que permite aos usuários salvar alterações em registros de produtos usando o **salvar alterações** botão.  
  
#### <a name="to-add-the-ability-to-save-changes-to-product-records"></a>Para adicionar a capacidade de salvar as alterações em registros de produtos  
  
1.  No designer, clique duas vezes o **salvar alterações** botão.  
  
     Visual Studio abre o arquivo code-behind e cria um novo `saveButton_Click` manipulador de eventos para o <xref:System.Windows.Controls.Primitives.ButtonBase.Click> eventos.  
  
2.  Adicione o seguinte código ao manipulador de eventos do `saveButton_Click`:  
  
     [!code-csharp[Data_WPFDATASET#4](../snippets/csharp/VS_Snippets_ProTools/data_wpfdataset/cs/mainwindow.xaml.cs#4)]
     [!code-vb[Data_WPFDATASET#4](../snippets/visualbasic/VS_Snippets_ProTools/data_wpfdataset/vb/mainwindow.xaml.vb#4)]  
  
    > [!NOTE]
    >  Este exemplo usa o método `Save` do `TableAdapter` para salvar as alterações. Isso ocorre neste passo a passo, porque apenas uma tabela de dados está sendo alterada. Se for necessário salvar alterações em várias tabelas de dados, você pode também usar o método `UpdateAll` do `TableAdapterManager` que o Visual Studio gera com o seu conjunto de dados. Para obter mais informações, consulte [visão geral de TableAdapterManager](http://msdn.microsoft.com/library/33076d42-6b41-491a-ac11-6c6339aea650).  
  
## <a name="test-the-application"></a>Testar o aplicativo  
 Crie e execute o aplicativo. Verifique se você pode exibir e atualizar registros de produtos.  
  
#### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Pressione **F5**.  
  
     O aplicativo é compilado e executado. Verifique o seguinte:  
  
    -   As caixas de texto exibem dados do primeiro registro do produto que tem uma foto. Este produto tem o produto 713 ID e o nome **Long-Sleeve Logo Jersey, S**.  
  
    -   Você pode clicar na **>** ou **<** botões para navegar em outros registros de produto.  
  
2.  Em um dos registros de produto, alterar o **tamanho** valor e, em seguida, clique em **salvar alterações**.  
  
3.  Feche o aplicativo e, em seguida, reinicie o aplicativo pressionando **F5** no Visual Studio.  
  
4.  Navegue até o registro do produto que você alterou e verifique se a mudança persistiu.  
  
5.  Feche o aplicativo.  
  
## <a name="next-steps"></a>Próximas etapas  
 Depois de completar este passo a passo, você poderá realizar as seguintes tarefas relacionadas:  
  
-   Saiba como usar o **fontes de dados** janela no Visual Studio para associar o WPF controla a outros tipos de fontes de dados. Para obter mais informações, consulte [controles de WPF associar a um WCF data service](../data-tools/bind-wpf-controls-to-a-wcf-data-service.md).  
  
-   Saiba como usar o **fontes de dados** janela no Visual Studio para exibir dados relacionados (ou seja, os dados em uma relação pai-filho) em controles do WPF. Para obter mais informações, consulte [instruções passo a passo: exibindo dados relacionados em um aplicativo WPF](../data-tools/walkthrough-displaying-related-data-in-a-wpf-application.md).  
  
## <a name="see-also"></a>Consulte também  
 [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio1.md)   
 [Associar controles WPF a dados no Visual Studio](../data-tools/bind-wpf-controls-to-data-in-visual-studio2.md)   
 [Ferramentas de conjunto de dados no Visual Studio](../data-tools/dataset-tools-in-visual-studio.md)   
 [Visão de geral do Designer do Silverlight e WPF](http://msdn.microsoft.com/en-us/570b7a5c-0c86-4326-a371-c9b63378fc62)   
 [Visão geral da vinculação de dados](http://msdn.microsoft.com/library/c707c95f-7811-401d-956e-2fffd019a211)

