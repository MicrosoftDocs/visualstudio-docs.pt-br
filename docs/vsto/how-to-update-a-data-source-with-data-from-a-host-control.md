---
title: 'Como: atualizar uma fonte de dados com dados de um controle de host'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- documents [Office development in Visual Studio], data source updates
- data [Office development in Visual Studio], updating a data source from a document
- host controls [Office development in Visual Studio], data source updates
- Office documents [Office development in Visual Studio, data sources
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8384b35583517a832763f5229d2b526ca10190ad
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541239"
---
# <a name="how-to-update-a-data-source-with-data-from-a-host-control"></a>Como: atualizar uma fonte de dados com dados de um controle de host
  Você pode associar um controle de host a uma fonte de dados e atualizar a fonte de dados com as alterações feitas nos dados no controle. Há duas etapas principais neste processo:

1. Atualize a fonte de dados na memória com os dados modificados no controle. Normalmente, a fonte de dados na memória é um <xref:System.Data.DataSet> , um <xref:System.Data.DataTable> ou algum outro objeto de dados.

2. Atualize o banco de dados com o dado alterado na fonte de dados na memória. Isso será aplicável somente se a fonte de dados estiver conectada a um banco de dado de back-end, como um SQL Server ou Microsoft Office banco de dados do Access.

   Para obter mais informações sobre controles de host e Associação de dados, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md) e [associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md).

   [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="update-the-in-memory-data-source"></a>Atualizar a fonte de dados na memória
 Por padrão, os controles de host que habilitam a vinculação de dados simples (como controles de conteúdo em um documento do Word ou um controle de intervalo nomeado em uma planilha do Excel) não salvam alterações de dados na fonte de dados na memória. Ou seja, quando um usuário final altera um valor em um controle de host e, em seguida, navega para fora do controle, o novo valor no controle não é salvo automaticamente na fonte de dados.

 Para salvar os dados na fonte de dados, você pode escrever o código que atualiza a fonte de dados em resposta a um evento específico em tempo de execução, ou você pode configurar o controle para atualizar automaticamente a fonte de dados quando o valor no controle for alterado.

 Você não precisa salvar <xref:Microsoft.Office.Tools.Excel.ListObject> as alterações na fonte de dados na memória. Quando você associa um <xref:Microsoft.Office.Tools.Excel.ListObject> controle aos dados, o <xref:Microsoft.Office.Tools.Excel.ListObject> controle salva automaticamente as alterações na fonte de dados na memória sem a necessidade de código adicional.

### <a name="to-update-the-in-memory-data-source-at-run-time"></a>Para atualizar a fonte de dados na memória em tempo de execução

- Chame o <xref:System.Windows.Forms.Binding.WriteValue%2A> método do <xref:System.Windows.Forms.Binding> objeto que associa o controle à fonte de dados.

     O exemplo a seguir salva as alterações feitas em um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle em uma planilha do Excel na fonte de dados. Este exemplo pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `namedRange1` com sua <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> propriedade associada a um campo em uma fonte de dados.

     [!code-csharp[Trin_VstcoreDataExcel#1](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#1)]
     [!code-vb[Trin_VstcoreDataExcel#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#1)]

### <a name="automatically-update-the-in-memory-data-source"></a>Atualizar automaticamente a fonte de dados na memória
 Você também pode configurar um controle para que ele atualize automaticamente a fonte de dados na memória. Em um projeto de nível de documento, você pode fazer isso usando o código ou o designer. Em um projeto de suplemento do VSTO, você deve usar o código.

#### <a name="to-set-a-control-to-automatically-update-the-in-memory-data-source-by-using-code"></a>Para definir um controle para atualizar automaticamente a fonte de dados na memória usando código

1. Use o modo System. Windows. Forms. DataSourceUpdateMode. OnPropertyChanged do <xref:System.Windows.Forms.Binding> objeto que associa o controle à fonte de dados. Há duas opções para atualizar a fonte de dados:

   - Para atualizar a fonte de dados quando o controle for validado, defina essa propriedade como System. Windows. Forms. DataSourceUpdateMode. OnValidation.

   - Para atualizar a fonte de dados quando o valor da propriedade associada a dados do controle for alterado, defina essa propriedade como System. Windows. Forms. DataSourceUpdateMode. OnPropertyChanged.

     > [!NOTE]
     > A opção System. Windows. Forms. DataSourceUpdateMode. OnPropertyChanged não se aplica aos controles de host do Word, pois o Word não oferece notificações de alteração de documento ou de alteração. No entanto, essa opção pode ser usada para controles de Windows Forms em documentos do Word.

     O exemplo a seguir configura um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle para atualizar automaticamente a fonte de dados quando o valor no controle é alterado. Este exemplo pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle chamado `namedRange1` com sua <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> propriedade associada a um campo em uma fonte de dados.

     [!code-csharp[Trin_VstcoreDataExcel#19](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#19)]
     [!code-vb[Trin_VstcoreDataExcel#19](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#19)]

#### <a name="to-set-a-control-to-automatically-update-the-in-memory-data-source-by-using-the-designer"></a>Para definir um controle para atualizar automaticamente a fonte de dados na memória usando o designer

1. No Visual Studio, abra o documento do Word ou a pasta de trabalho do Excel no designer.

2. Clique no controle para o qual você deseja atualizar automaticamente a fonte de dados.

3. Na janela **Propriedades** , expanda a propriedade **(DataBindings)** .

4. Ao lado da propriedade **(avançado)** , clique no botão de reticências (![captura de tela VisualStudioEllipsesButton](../vsto/media/vbellipsesbutton.png "Captura de tela de VisualStudioEllipsesButton")).

5. Na caixa de diálogo **formatação e Associação avançada** , clique na lista suspensa **modo de atualização da fonte de dados** e selecione um dos seguintes valores:

    - Para atualizar a fonte de dados quando o controle for validado, selecione **OnValidation**.

    - Para atualizar a fonte de dados quando o valor da propriedade associada a dados do controle for alterado, selecione **OnPropertyChanged**.

        > [!NOTE]
        > A opção **OnPropertyChanged** não se aplica a controles de host do Word, porque o Word não oferece notificações de alteração de documento ou de alteração. No entanto, essa opção pode ser usada para controles de Windows Forms em documentos do Word.

6. Feche a caixa de diálogo **formatação e Associação avançada** .

## <a name="update-the-database"></a>Atualizar o banco de dados
 Se a fonte de dados na memória estiver associada a um banco de dados, você deverá atualizar o banco de dado com as alterações feitas na fonte. Para obter mais informações sobre a atualização de um banco de dados, consulte salvar e atualizar dados [novamente](../data-tools/save-data-back-to-the-database.md) [usando um TableAdapter](../data-tools/update-data-by-using-a-tableadapter.md) .

### <a name="to-update-the-database"></a>Para atualizar o banco de dados

1. Chame o <xref:System.Windows.Forms.BindingSource.EndEdit%2A> método do <xref:System.Windows.Forms.BindingSource> para o controle.

     O <xref:System.Windows.Forms.BindingSource> é gerado automaticamente quando você adiciona um controle de vinculação de dados a um documento ou pasta de trabalho em tempo de design. O <xref:System.Windows.Forms.BindingSource> conecta o controle ao dataset tipado em seu projeto. Para obter mais informações, consulte [visão geral do componente BindingSource](/dotnet/framework/winforms/controls/bindingsource-component-overview).

     O exemplo de código a seguir pressupõe que seu projeto contém um <xref:System.Windows.Forms.BindingSource> nome `customersBindingSource` .

     [!code-csharp[Trin_VstcoreDataExcel#20](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#20)]
     [!code-vb[Trin_VstcoreDataExcel#20](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#20)]

2. Chame o `Update` método do TableAdapter gerado em seu projeto.

     O TableAdapter é gerado automaticamente quando você adiciona um controle de vinculação de dados a um documento ou pasta de trabalho em tempo de design. O TableAdapter conecta o dataset tipado em seu projeto ao banco de dados. Para obter mais informações, consulte [visão geral do TableAdapter](../data-tools/fill-datasets-by-using-tableadapters.md#tableadapter-overview).

     O exemplo de código a seguir pressupõe que você tenha uma conexão com a tabela Customers no banco de dados Northwind e que seu projeto contenha um TableAdapter chamado `customersTableAdapter` e um dataset tipado chamado `northwindDataSet` .

     [!code-csharp[Trin_VstcoreDataExcel#21](../vsto/codesnippet/CSharp/Trin_VstcoreDataExcelCS/Sheet1.cs#21)]
     [!code-vb[Trin_VstcoreDataExcel#21](../vsto/codesnippet/VisualBasic/Trin_VstcoreDataExcelVB/Sheet1.vb#21)]

## <a name="see-also"></a>Consulte também
- [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)
- [Salvar dados de volta no banco de dados](../data-tools/save-data-back-to-the-database.md)
- [Atualizar dados usando um TableAdapter](../data-tools/update-data-by-using-a-tableadapter.md)
- [Como rolar por registros de banco de dados em uma planilha](../vsto/how-to-scroll-through-database-records-in-a-worksheet.md)
- [Como: preencher planilhas com dados de um banco de dado](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)
- [Como: popular documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md)
- [Como: popular documentos com dados de um banco de dado](../vsto/how-to-populate-documents-with-data-from-a-database.md)
- [Como: popular documentos com dados de serviços](../vsto/how-to-populate-documents-with-data-from-services.md)
