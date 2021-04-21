---
title: 'Walkthrough: vinculação de dados simples no projeto de suplemento do VSTO'
description: Saiba como você pode adicionar controles a um documento do Microsoft Word e associar os controles aos dados em tempo de execução.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], binding data
- data binding [Office development in Visual Studio], Word
- data [Office development in Visual Studio], simple binding data
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e1891173f10acfff74e0f7ef7ab17e29b258b80e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826831"
---
# <a name="walkthrough-simple-data-binding-in-vsto-add-in-project"></a>Walkthrough: vinculação de dados simples no projeto de suplemento do VSTO

Você pode associar dados a controles de host e controles de Windows Forms em projetos de suplemento do VSTO. Este tutorial demonstra como adicionar controles a um Microsoft Office documento do Word e associar os controles aos dados em tempo de execução.

[!INCLUDE[appliesto_wdallapp](../vsto/includes/appliesto-wdallapp-md.md)]

Este passo a passo ilustra as seguintes tarefas:

- Adicionar um <xref:Microsoft.Office.Tools.Word.ContentControl> a um documento em tempo de execução.

- Criar um <xref:System.Windows.Forms.BindingSource> que conecta o controle a uma instância de um DataSet.

- Habilitando o usuário a percorrer os registros e exibi-los no controle.

[!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos

Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].

- Acesso a uma instância em execução do SQL Server 2005 ou SQL Server 2005 Express que tem o `AdventureWorksLT` banco de dados de exemplo anexado a ele. Você pode baixar o `AdventureWorksLT` banco de dados do [repositório GitHub de exemplos de SQL Server](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks). Para obter mais informações sobre como anexar um banco de dados, consulte os seguintes tópicos:

  - Para anexar um banco de dados usando SQL Server Management Studio ou SQL Server Management Studio Express, consulte [como: anexar um banco de dados (SQL Server Management Studio)](/sql/relational-databases/databases/attach-a-database).

  - Para anexar um banco de dados usando a linha de comando, consulte [como: anexar um arquivo de banco de dados a SQL Server Express](/previous-versions/sql/).

## <a name="create-a-new-project"></a>Criar um novo projeto

A primeira etapa é criar um projeto de suplemento do VSTO do Word.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de suplemento do VSTO do Word com o nome **populando documentos de um banco de dados**, usando o Visual Basic ou o C#.

     Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre o arquivo *ThisAddIn. vb* ou *ThisAddIn. cs* e adiciona os **documentos populando de um projeto de banco de dados** para **Gerenciador de soluções**.

2. Se o seu projeto se destina ao [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou ao [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] , adicione uma referência ao assembly *Microsoft.Office.Tools.Word.v4.0.Utilities.dll* . Essa referência é necessária para adicionar programaticamente Windows Forms controles ao documento mais adiante neste guia.

## <a name="create-a-data-source"></a>Criar uma fonte de dados

Use a janela **Data Sources** para adicionar um conjunto de dados tipado ao seu projeto.

### <a name="to-add-a-typed-dataset-to-the-project"></a>Para adicionar um conjunto de um dataset tipado ao projeto

1. Se a janela **fontes de dados** não estiver visível, exiba-a por, na barra de menus, escolhendo **Exibir**  >  **outras**  >  **fontes de dados** do Windows.

2. Escolha **Adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.

3. Clique em **banco de dados** e em **Avançar**.

4. Se você tiver uma conexão existente com o `AdventureWorksLT` banco de dados, escolha essa conexão e clique em **Avançar**.

    Caso contrário, clique em **nova conexão** e use a caixa de diálogo **Adicionar conexão** para criar a nova conexão. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

5. Na página **salvar a cadeia de conexão no arquivo de configuração do aplicativo** , clique em **Avançar**.

6. Na página **escolher seus objetos de banco de dados** , expanda **tabelas** e selecione **cliente (tabela SalesLT)**.

7. Clique em **Concluir**.

    O arquivo *AdventureWorksLTDataSet. xsd* é adicionado ao **Gerenciador de soluções**. Esse arquivo define os seguintes itens:

   - Um dataset tipado chamado `AdventureWorksLTDataSet` . Esse DataSet representa o conteúdo da tabela **Customer (tabela SalesLT)** no banco de dados AdventureWorksLT.

   - Um TableAdapter chamado `CustomerTableAdapter` . Esse TableAdapter pode ser usado para ler e gravar dados no `AdventureWorksLTDataSet` . Para obter mais informações, consulte [visão geral do TableAdapter](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview).

     Você usará esses dois objetos posteriormente neste passo a passos.

## <a name="create-controls-and-binding-controls-to-data"></a>Criar controles e ligar controles a dados

A interface para exibir os registros de banco de dados neste passo a passos é básica e é criada diretamente dentro do documento. Uma <xref:Microsoft.Office.Tools.Word.ContentControl> exibe um único registro de banco de dados por vez, e dois <xref:Microsoft.Office.Tools.Word.Controls.Button> controles permitem que você role para frente e para trás pelos registros. O controle de conteúdo usa um <xref:System.Windows.Forms.BindingSource> para se conectar ao banco de dados.

Para obter mais informações sobre como ligar controles a dados, consulte [associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).

### <a name="to-create-the-interface-in-the-document"></a>Para criar a interface no documento

1. Na `ThisAddIn` classe, declare os seguintes controles para exibir e percorrer a `Customer` tabela do `AdventureWorksLTDataSet` banco de dados.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet1":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet1":::

2. No `ThisAddIn_Startup` método, adicione o código a seguir para inicializar o conjunto de dados, preencha o conjunto com informações do `AdventureWorksLTDataSet` banco de dados.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet2":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet2":::

3. Adicione o seguinte código ao `ThisAddIn_Startup` método. Isso gera um item de host que estende o documento. Para obter mais informações, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet3":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet3":::

4. Defina vários intervalos no início do documento. Esses intervalos identificam onde inserir texto e posicionar controles.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet4":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet4":::

5. Adicione os controles de interface aos intervalos definidos anteriormente.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet5":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet5":::

6. Associe o controle de conteúdo ao `AdventureWorksLTDataSet` usando o <xref:System.Windows.Forms.BindingSource> . Para desenvolvedores de C#, adicione dois manipuladores de eventos para os <xref:Microsoft.Office.Tools.Word.Controls.Button> controles.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet6":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet6":::

7. Adicione o código a seguir para navegar pelos registros do banco de dados.

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb" id="Snippet7":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs" id="Snippet7":::

## <a name="test-the-add-in"></a>Testar o suplemento

Quando você abre o Word, o controle de conteúdo exibe dados do `AdventureWorksLTDataSet` DataSet. Percorra os registros do banco de dados clicando nos botões **Avançar** e **anterior** .

### <a name="to-test-the-vsto-add-in"></a>Para testar o suplemento do VSTO

1. Pressione **F5**.

     Um controle de conteúdo chamado `customerContentControl` é criado e preenchido com dados. Ao mesmo tempo, um objeto DataSet chamado `adventureWorksLTDataSet` e um <xref:System.Windows.Forms.BindingSource> nomeado `customerBindingSource` são adicionados ao projeto. O <xref:Microsoft.Office.Tools.Word.ContentControl> é associado ao <xref:System.Windows.Forms.BindingSource> , que, por sua vez, é associado ao objeto DataSet.

2. Clique nos botões **Avançar** e **anterior** para percorrer os registros do banco de dados.

## <a name="see-also"></a>Consulte também

- [Dados em soluções do Office](../vsto/data-in-office-solutions.md)
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Como: preencher planilhas com dados de um banco de dado](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [Como: popular documentos com dados de um banco de dado](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [Como: popular documentos com dados de serviços](../vsto/how-to-populate-documents-with-data-from-services.md)
- [Como: popular documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [Como rolar por registros de banco de dados em uma planilha](../vsto/how-to-scroll-through-database-records-in-a-worksheet.md)
- [Como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Walkthrough: vinculação de dados simples em um projeto de nível de documento](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)
- [Walkthrough: ligação de dados complexa em um projeto de nível de documento](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
- [Visão geral de usar arquivos de banco de dados local em soluções do Office](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)
- [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Como: popular documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [Como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Visão geral de usar arquivos de banco de dados local em soluções do Office](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [Visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview)
