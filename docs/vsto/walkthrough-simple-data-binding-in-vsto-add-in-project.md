---
title: 'Passo a passo: Associação de dados simples no projeto do suplemento do VSTO'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data [Office development in Visual Studio], binding data
- data binding [Office development in Visual Studio], Word
- data [Office development in Visual Studio], simple binding data
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 0373bcba5cecbbc47451f3ad050ba0ea44a12246
ms.sourcegitcommit: be938c7ecd756a11c9de3e6019a490d0e52b4190
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50672659"
---
# <a name="walkthrough-simple-data-binding-in-vsto-add-in-project"></a>Passo a passo: Associação de dados simples no projeto de suplemento do VSTO

Você pode associar dados a controles de host e controles de formulários do Windows em projetos de suplemento do VSTO. Este passo a passo demonstra como adicionar controles a um documento do Microsoft Office Word e ligar os controles a dados em tempo de execução.

[!INCLUDE[appliesto_wdallapp](../vsto/includes/appliesto-wdallapp-md.md)]

Esta explicação passo a passo ilustra as seguintes tarefas:

-   Adicionando um <xref:Microsoft.Office.Tools.Word.ContentControl> a um documento em tempo de execução.

-   Criando um <xref:System.Windows.Forms.BindingSource> que conecta o controle a uma instância de um conjunto de dados.

-   Permitindo que o usuário percorrer os registros e exibi-los no controle.

[!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos

Você precisa dos seguintes componentes para concluir esta instrução passo a passo:

-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

-   [!INCLUDE[Word_15_short](../vsto/includes/word-15-short-md.md)] ou [!INCLUDE[Word_14_short](../vsto/includes/word-14-short-md.md)].

-   Acesso ao executar uma instância do SQL Server 2005 ou SQL Server 2005 Express que tem o `AdventureWorksLT` o banco de dados de exemplo está anexado a ele. Você pode baixar o `AdventureWorksLT` do banco de dados do [site da CodePlex](http://go.microsoft.com/fwlink/?LinkId=115611). Para obter mais informações sobre como anexar um banco de dados, consulte os tópicos a seguir:

    -   Para anexar um banco de dados usando o SQL Server Management Studio ou o SQL Server Management Studio Express, consulte [como: anexar um banco de dados (SQL Server Management Studio)](/sql/relational-databases/databases/attach-a-database).

    -   Para anexar um banco de dados usando a linha de comando, consulte [como: anexar um arquivo de banco de dados para o SQL Server Express](/previous-versions/sql/).

## <a name="create-a-new-project"></a>Criar um novo projeto

A primeira etapa é criar um projeto de suplemento do VSTO do Word.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1.  Criar um projeto de suplemento do VSTO do Word com o nome **Populando documentos de um banco de dados**, usando o Visual Basic ou c#.

     Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     O Visual Studio abre o *ThisAddIn. vb* ou *ThisAddIn.cs* de arquivos e adiciona os **Populando documentos de um banco de dados** projeto ao **Gerenciador de soluções** .

2.  Se o projeto está destinado a [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)], adicione uma referência para o *Microsoft.Office.Tools.Word.v4.0.Utilities.dll* assembly. Essa referência é necessária para adicionar controles Windows Forms de forma programática para o documento mais tarde neste passo a passo.

## <a name="create-a-data-source"></a>Criar uma fonte de dados

Use o **fontes de dados** janela para adicionar um conjunto de dados tipado ao seu projeto.

### <a name="to-add-a-typed-dataset-to-the-project"></a>Para adicionar um dataset tipado ao projeto

1. Se o **fontes de dados** janela não estiver visível, exibi-lo, na barra de menus, escolhendo **exibição** > **Other Windows**  >   **Fontes de dados**.

2. Escolher **Add New Data Source** para iniciar o **Data Source Configuration Wizard**.

3. Clique em **banco de dados**e, em seguida, clique em **próxima**.

4. Se você tiver uma conexão existente para o `AdventureWorksLT` do banco de dados, escolha essa conexão e clique em **próxima**.

    Caso contrário, clique em **nova Conexão**e usar o **Adicionar Conexão** caixa de diálogo para criar a nova conexão. Para obter mais informações, consulte [adicionar novas conexões](../data-tools/add-new-connections.md).

5. No **salvar a cadeia de Conexão no arquivo de configuração de aplicativo** , clique em **próxima**.

6. No **Choose Your Database Objects** página, expanda **tabelas** e selecione **cliente (SalesLT)**.

7. Clique em **Finalizar**.

    O *Adventureworksltdataset* arquivo é adicionado ao **Gerenciador de soluções**. Esse arquivo define os seguintes itens:

   - Um dataset tipado chamado `AdventureWorksLTDataSet`. Esse conjunto de dados representa o conteúdo do **Customer (SalesLT)** tabela no banco de dados AdventureWorksLT.

   - Um TableAdapter nomeado `CustomerTableAdapter`. Este TableAdapter pode ser usado para ler e gravar dados no `AdventureWorksLTDataSet`. Para obter mais informações, consulte [visão geral de TableAdapter](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview).

     Você usará dois desses objetos posteriormente neste passo a passo.

## <a name="create-controls-and-binding-controls-to-data"></a>Criar controles e controles de vinculação de dados

A interface para exibir os registros do banco de dados neste passo a passo é básica, e ele é criado dentro do documento. Uma <xref:Microsoft.Office.Tools.Word.ContentControl> exibe um registro de banco de dados individual por vez e dois <xref:Microsoft.Office.Tools.Word.Controls.Button> controles permitem que você percorra registros e para trás. O controle de conteúdo usa um <xref:System.Windows.Forms.BindingSource> para se conectar ao banco de dados.

Para obter mais informações sobre controles de vinculação de dados, consulte [ligar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).

### <a name="to-create-the-interface-in-the-document"></a>Para criar a interface do documento

1.  No `ThisAddIn` classe, declare os seguintes controles para exibir e percorra o `Customer` tabela do `AdventureWorksLTDataSet` banco de dados.

     [!code-vb[Trin_WordAddInDatabase#1](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#1)]
     [!code-csharp[Trin_WordAddInDatabase#1](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#1)]

2.  No `ThisAddIn_Startup` método, adicione o seguinte código para inicializar o conjunto de dados, preencher o conjunto de dados com informações do `AdventureWorksLTDataSet` banco de dados.

     [!code-vb[Trin_WordAddInDatabase#2](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#2)]
     [!code-csharp[Trin_WordAddInDatabase#2](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#2)]

3.  Adicione o seguinte código ao método de `ThisAddIn_Startup` . Isso gera um item de host que estende o documento. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

     [!code-vb[Trin_WordAddInDatabase#3](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#3)]
     [!code-csharp[Trin_WordAddInDatabase#3](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#3)]

4.  Defina vários intervalos no início do documento. Esses intervalos identificam onde inserir texto e coloque controles.

     [!code-vb[Trin_WordAddInDatabase#4](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#4)]
     [!code-csharp[Trin_WordAddInDatabase#4](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#4)]

5.  Adicione os controles de interface para os intervalos definidos anteriormente.

     [!code-vb[Trin_WordAddInDatabase#5](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#5)]
     [!code-csharp[Trin_WordAddInDatabase#5](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#5)]

6.  Associar o controle de conteúdo `AdventureWorksLTDataSet` usando o <xref:System.Windows.Forms.BindingSource>. Para desenvolvedores do c#, adicione dois manipuladores de eventos para o <xref:Microsoft.Office.Tools.Word.Controls.Button> controles.

     [!code-vb[Trin_WordAddInDatabase#6](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#6)]
     [!code-csharp[Trin_WordAddInDatabase#6](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#6)]

7.  Adicione o código a seguir para navegar pelos registros de banco de dados.

     [!code-vb[Trin_WordAddInDatabase#7](../vsto/codesnippet/VisualBasic/trin_wordaddindatabase/ThisAddIn.vb#7)]
     [!code-csharp[Trin_WordAddInDatabase#7](../vsto/codesnippet/CSharp/trin_wordaddindatabase/ThisAddIn.cs#7)]

## <a name="test-the-add-in"></a>Testar o suplemento

Quando você abre o Word, o controle de conteúdo exibe dados do `AdventureWorksLTDataSet` conjunto de dados. Percorrer os registros de banco de dados clicando o **próxima** e **Previous** botões.

### <a name="to-test-the-vsto-add-in"></a>Para testar o suplemento do VSTO

1.  Pressione **F5**.

     Um controle de conteúdo chamado `customerContentControl` é criada e preenchida com dados. Ao mesmo tempo, um objeto de conjunto de dados chamado `adventureWorksLTDataSet` e uma <xref:System.Windows.Forms.BindingSource> denominado `customerBindingSource` são adicionados ao projeto. O <xref:Microsoft.Office.Tools.Word.ContentControl> está associado a <xref:System.Windows.Forms.BindingSource>, que por sua vez é associado ao objeto de conjunto de dados.

2.  Clique o **próxima** e **Previous** botões para percorrer os registros do banco de dados.

## <a name="see-also"></a>Consulte também

- [Dados em soluções do Office](../vsto/data-in-office-solutions.md)
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Como: preencher planilhas com dados de um banco de dados](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [Como: preencher documentos com dados de um banco de dados](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [Como: preencher documentos com dados de serviços](../vsto/how-to-populate-documents-with-data-from-services.md)
- [Como: preencher documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [Como: percorrer registros do banco de dados em uma planilha](../vsto/how-to-scroll-through-database-records-in-a-worksheet.md)
- [Como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Passo a passo: Associação de dados simples em um projeto de nível de documento](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md)
- [Passo a passo: Vinculação de dados complexos em um projeto de nível de documento](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md)
- [Usar arquivos de banco de dados local na visão geral das soluções do Office](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [Adicionar novas fontes de dados](../data-tools/add-new-data-sources.md)
- [Associando controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Como: preencher documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [Como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md)
- [Usar arquivos de banco de dados local na visão geral das soluções do Office](../vsto/using-local-database-files-in-office-solutions-overview.md)
- [Visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview)