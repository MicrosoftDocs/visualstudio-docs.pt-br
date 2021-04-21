---
title: 'Walkthrough: ligação de dados complexa no projeto de suplemento do VSTO'
description: Saiba como adicionar controles a uma planilha do Microsoft Excel e associar os controles aos dados em tempo de execução.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data binding [Office development in Visual Studio], Excel
- data [Office development in Visual Studio], binding data
- complex data [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 49f87968c545e9fcca7548cd2fbda866d18b660b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826350"
---
# <a name="walkthrough-complex-data-binding-in-vsto-add-in-project"></a>Walkthrough: ligação de dados complexa no projeto de suplemento do VSTO
  Você pode associar dados a controles de host e controles de Windows Forms em projetos de suplemento do VSTO. Este tutorial demonstra como adicionar controles a uma Microsoft Office planilha do Excel e associar os controles aos dados em tempo de execução.

 [!INCLUDE[appliesto_xlallapp](../vsto/includes/appliesto-xlallapp-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Adicionar um <xref:Microsoft.Office.Tools.Excel.ListObject> controle a uma planilha em tempo de execução.

- Criar um <xref:System.Windows.Forms.BindingSource> que conecta o controle a uma instância de um DataSet.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Excel_15_short](../vsto/includes/excel-15-short-md.md)] ou [!INCLUDE[Excel_14_short](../vsto/includes/excel-14-short-md.md)].

- Acesso a uma instância em execução do SQL Server 2005 ou SQL Server 2005 Express que tem o `AdventureWorksLT` banco de dados de exemplo anexado a ele. Você pode baixar o `AdventureWorksLT` banco de dados do [repositório GitHub de exemplos de SQL Server](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks). Para obter mais informações sobre como anexar um banco de dados, consulte os seguintes tópicos:

  - Para anexar um banco de dados usando SQL Server Management Studio ou SQL Server Management Studio Express, consulte [como: anexar um banco de dados (SQL Server Management Studio)](/sql/relational-databases/databases/attach-a-database).

  - Para anexar um banco de dados usando a linha de comando, consulte [como: anexar um arquivo de banco de dados a SQL Server Express](/previous-versions/sql/).

## <a name="create-a-new-project"></a>Criar um novo projeto
 A primeira etapa é criar um projeto de suplemento do VSTO do Excel.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de suplemento do VSTO do Excel com o nome **populando planilhas de um banco de dados**, usando Visual Basic ou C#.

     Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre `ThisAddIn.vb` o `ThisAddIn.cs` arquivo ou e adiciona as **planilhas populando de um** projeto de banco de dados para **Gerenciador de soluções**.

## <a name="create-a-data-source"></a>Criar uma fonte de dados
 Use a janela **Data Sources** para adicionar um conjunto de dados tipado ao seu projeto.

### <a name="to-add-a-typed-dataset-to-the-project"></a>Para adicionar um conjunto de um dataset tipado ao projeto

1. Se a janela **fontes de dados** não estiver visível, exiba-a por, na barra de menus, escolhendo **Exibir**  >  **outras**  >  **fontes de dados** do Windows.

2. Escolha **Adicionar nova fonte de dados** para iniciar o **Assistente de configuração de fonte de dados**.

3. Clique em **banco de dados** e em **Avançar**.

4. Se você tiver uma conexão existente com o `AdventureWorksLT` banco de dados, escolha essa conexão e clique em **Avançar**.

    Caso contrário, clique em **nova conexão** e use a caixa de diálogo **Adicionar conexão** para criar a nova conexão. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

5. Na página **salvar a cadeia de conexão no arquivo de configuração do aplicativo** , clique em **Avançar**.

6. Na página **escolher seus objetos de banco de dados** , expanda **tabelas** e selecione **Endereço (tabela SalesLT)**.

7. Clique em **Concluir**.

    O arquivo *AdventureWorksLTDataSet. xsd* é adicionado ao **Gerenciador de soluções**. Esse arquivo define os seguintes itens:

   - Um dataset tipado chamado `AdventureWorksLTDataSet` . Esse DataSet representa o conteúdo da tabela **Address (tabela SalesLT)** no banco de dados AdventureWorksLT.

   - Um TableAdapter chamado `AddressTableAdapter` . Esse TableAdapter pode ser usado para ler e gravar dados no `AdventureWorksLTDataSet` . Para obter mais informações, consulte [visão geral do TableAdapter](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview).

     Você usará esses dois objetos posteriormente neste passo a passos.

## <a name="create-controls-and-bind-controls-to-data"></a>Criar controles e associar controles a dados
 Para este guia, o <xref:Microsoft.Office.Tools.Excel.ListObject> controle exibe todos os dados na tabela que você selecionou assim que o usuário abre a pasta de trabalho. O objeto de lista usa um <xref:System.Windows.Forms.BindingSource> para conectar o controle ao banco de dados.

 Para obter mais informações sobre como ligar controles a dados, consulte [associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).

### <a name="to-add-the-list-object-dataset-and-table-adapter"></a>Para adicionar o objeto de lista, conjunto de tabelas e adaptador de tabela

1. Na `ThisAddIn` classe, declare os seguintes controles para exibir a `Address` tabela do conjunto de um `AdventureWorksLTDataSet` .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb" id="Snippet1":::

2. No `ThisAddIn_Startup` método, adicione o código a seguir para inicializar o DataSet e preencher o conjunto de dados com as informações do `AdventureWorksLTDataSet` DataSet.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb" id="Snippet2":::

3. Adicione o seguinte código ao `ThisAddIn_Startup` método. Isso gera um item de host que estende a planilha. Para obter mais informações, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb" id="Snippet3":::

4. Crie um intervalo e adicione o <xref:Microsoft.Office.Tools.Excel.ListObject> controle.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb" id="Snippet4":::

5. Associe o objeto de lista ao `AdventureWorksLTDataSet` usando o <xref:System.Windows.Forms.BindingSource> . Passe os nomes das colunas que você deseja associar ao objeto de lista.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelAddInDatabase_O12/ThisAddIn.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelAddInDatabase_O12/ThisAddIn.vb" id="Snippet5":::

## <a name="test-the-add-in"></a>Testar o suplemento
 Quando você abrir o Excel, o <xref:Microsoft.Office.Tools.Excel.ListObject> controle exibirá os dados da `Address` tabela do `AdventureWorksLTDataSet` DataSet.

### <a name="to-test-the-vsto-add-in"></a>Para testar o suplemento do VSTO

- Pressione **F5**.

     Um <xref:Microsoft.Office.Tools.Excel.ListObject> controle chamado `addressListObject` é criado na planilha. Ao mesmo tempo, um objeto DataSet chamado `adventureWorksLTDataSet` e um <xref:System.Windows.Forms.BindingSource> nomeado `addressBindingSource` são adicionados ao projeto. O <xref:Microsoft.Office.Tools.Excel.ListObject> é associado ao <xref:System.Windows.Forms.BindingSource> , que, por sua vez, é associado ao objeto DataSet.

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
- [Visão geral de usar arquivos de banco de dados local em soluções do Office](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [Visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview)
