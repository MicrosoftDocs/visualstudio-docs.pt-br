---
title: Associar dados a controles em soluções do Office
description: Saiba como você pode associar controles de Windows Forms e de host em um Microsoft Office documento do Word ou planilha do Excel a uma fonte de dados.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio], connecting to data
- data, data binding
- data binding
- data binding, Office solutions
- data binding, controls
- Office applications [Office development in Visual Studio], data binding
- controls, data binding
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: ccc45e9ec389e265e69c81baaf569aa3eb3c978b
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825622"
---
# <a name="bind-data-to-controls-in-office-solutions"></a>Associar dados a controles em soluções do Office
  Você pode associar controles de Windows Forms e de *host* em um documento Microsoft Office Word ou Microsoft Office planilha do Excel a uma fonte de dados para que os controles exibam automaticamente os dados. Você pode associar dados a controles em projetos de nível de aplicativo e de documento.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Controles de host estendem objetos que estão nos modelos de objeto do Word e do Excel, como controles de conteúdo no Word e intervalos nomeados no Excel. Para obter mais informações, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

 Os controles Windows Forms e host usam o modelo de ligação de dados Windows Forms, que dá suporte tanto à vinculação de dados *simples* quanto à *vinculação de dados complexa* a fontes de dados, como conjuntos de dados e tabelas. Para obter informações completas sobre o modelo de associação de dados no Windows Forms, consulte [Associação de dados e Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms).

## <a name="simple-data-binding"></a>Vinculação de dados simples
 A vinculação de dados simples existe quando uma propriedade de controle está associada a um único elemento de dados, como um valor em uma tabela de dados. Por exemplo, o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle tem uma <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> propriedade que pode ser associada a um campo em um conjunto de uma. Quando o campo no conjunto de alterações é alterado, o valor no intervalo nomeado também é alterado. Todos os controles de host, exceto para o <xref:Microsoft.Office.Tools.Word.XMLNodes> controle, dão suporte à vinculação de dados simples. O <xref:Microsoft.Office.Tools.Word.XMLNodes> controle é uma coleção e, portanto, não oferece suporte à vinculação de dados.

 Para executar uma vinculação de dados simples a um controle de host, adicione um <xref:System.Windows.Forms.Binding> à `DataBindings` Propriedade do controle. Um <xref:System.Windows.Forms.Binding> objeto representa a associação simples entre um valor de Propriedade do controle e o valor de um elemento de dados.

 O exemplo a seguir demonstra como associar a <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> Propriedade a um elemento de dados em um projeto de nível de documento.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_BindableComponent/Sheet1.vb" id="Snippet4":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_BindableComponent/Sheet1.cs" id="Snippet4":::

 Para obter orientações que demonstram a vinculação de dados simples, consulte [passo a passos: vinculação de dados simples em um projeto de nível de documento](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md) para um projeto de nível de documento e [passo a passos: vinculação de dados simples no projeto de suplemento](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md) do VSTO para um projeto de suplemento do VSTO.

## <a name="complex-data-binding"></a>Vinculação de dados complexos
 A vinculação de dados complexa existe quando uma propriedade de controle está associada a mais de um elemento de dados, como várias colunas em uma tabela de dados. O <xref:Microsoft.Office.Tools.Excel.ListObject> controle para Excel é o único controle de host que dá suporte à ligação de dados complexa. Também há muitos Windows Forms controles que dão suporte à ligação de dados complexa, como o <xref:System.Windows.Forms.DataGridView> controle.

 Para executar uma vinculação de dados complexa, defina a `DataSource` Propriedade do controle como um objeto de fonte de dados com suporte pela Associação de dados complexa. Por exemplo, a <xref:Microsoft.Office.Tools.Excel.ListObject.DataSource%2A> Propriedade do <xref:Microsoft.Office.Tools.Excel.ListObject> controle pode ser associada a várias colunas em uma tabela de dados. Todos os dados na tabela de dados são exibidos no <xref:Microsoft.Office.Tools.Excel.ListObject> controle e, à medida que os dados na tabela de dados são alterados, o <xref:Microsoft.Office.Tools.Excel.ListObject> também é alterado. Para obter uma lista das fontes de dados que você pode usar para a ligação de dados complexa, consulte [fontes de dados com suporte pelo Windows Forms](/dotnet/framework/winforms/data-sources-supported-by-windows-forms).

 O exemplo de código a seguir cria um <xref:System.Data.DataSet> com dois <xref:System.Data.DataTable> objetos e popula uma das tabelas com dados. Em seguida, o código associa a <xref:Microsoft.Office.Tools.Excel.ListObject> à tabela que contém dados. Este exemplo é para um projeto de nível de documento do Excel.

 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_ExcelListObject/Trin_ExcelListObject.cs" id="Snippet18":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_ExcelListObject/Sheet1.vb" id="Snippet18":::

 Para obter orientações que demonstram a vinculação de dados complexa, consulte [passo a passos: vinculação de dados complexa em um projeto de nível de documento](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md) para um projeto de nível de documento e [passo a passos: ligação de dados complexa no projeto de suplemento](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md) do VSTO para um projeto de suplemento do VSTO.

## <a name="display-data-in-documents-and-workbooks"></a>Exibir dados em documentos e pastas de trabalho
 Em projetos de nível de documento, você pode usar a janela **fontes de dados** para adicionar controles vinculados a dados a seus documentos ou pastas de trabalho facilmente, da mesma maneira que o utiliza para Windows Forms. Para obter mais informações sobre como usar a janela **fontes de dados** , consulte [associar controles de Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md) e [adicionar novas fontes de dados](../data-tools/add-new-data-sources.md).

### <a name="drag-controls-from-the-data-sources-window"></a>Arrastar controles da janela fontes de dados
 Um controle é criado no documento quando você arrasta um objeto para ele na janela **fontes de dados** . O tipo de controle criado depende se você está associando uma única coluna de dados ou várias colunas de dados.

 Para o Excel, um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle é criado na planilha para cada campo individual e um <xref:Microsoft.Office.Tools.Excel.ListObject> controle é criado para cada intervalo de dados que inclui várias linhas e colunas. Você pode alterar esse padrão selecionando a tabela ou o campo na janela **fontes de dados** e escolhendo um controle diferente na lista suspensa.

 Um <xref:Microsoft.Office.Tools.Word.ContentControl> controle é adicionado aos documentos. O tipo de controle de conteúdo depende do tipo de dados do campo que você selecionou.

### <a name="bind-data-in-document-level-projects-at-design-time"></a>Associar dados em projetos de nível de documento em tempo de design
 Os tópicos a seguir mostram exemplos de vinculação de dados em tempo de design:

- [Como: preencher planilhas com dados de um banco de dado](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)

- [Como: popular documentos com dados de um banco de dado](../vsto/how-to-populate-documents-with-data-from-a-database.md)

- [Como: popular documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md)

- [Como: popular documentos com dados de serviços](../vsto/how-to-populate-documents-with-data-from-services.md)

- [Como rolar por registros de banco de dados em uma planilha](../vsto/how-to-scroll-through-database-records-in-a-worksheet.md)

### <a name="bind-data-in-vsto-add-in-projects"></a>Associar dados em projetos de suplemento do VSTO
 Em projetos de suplemento do VSTO, você pode adicionar controles somente em tempo de execução. Os tópicos a seguir mostram exemplos de vinculação de dados em tempo de execução:

- [Walkthrough: vinculação de dados simples no projeto de suplemento do VSTO](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)

- [Walkthrough: ligação de dados complexa no projeto de suplemento do VSTO](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md)

## <a name="update-data-that-is-bound-to-host-controls"></a>Atualizar dados associados a controles de host
 A vinculação de dados entre uma fonte de dados e um controle de host envolve uma atualização bidirecional de dados. Na vinculação de dados simples, as alterações na fonte de dados são refletidas automaticamente no controle de host, mas as alterações no controle de host exigem uma chamada explícita para atualizar a fonte de dados. O motivo é que, em alguns casos, as alterações em um campo associado a dados não são aceitas, a menos que sejam acompanhadas por alterações em outro campo associado a dados. Por exemplo, você pode ter dois campos, um para idade e outro para anos de experiência. A experiência não pode exceder a idade. Um usuário não pode atualizar a idade de 50 para 25 e, em seguida, a experiência de 30 a 10, a menos que ele faça as alterações ao mesmo tempo. Para resolver esse problema, os campos com vinculação de dados simples não são atualizados até que as atualizações sejam explicitamente enviadas pelo código.

 Para atualizar uma fonte de dados de controles de host que habilitam a vinculação de dados simples, você deve enviar atualizações para a fonte de dados na memória (como, por exemplo, um <xref:System.Data.DataSet> ou <xref:System.Data.DataTable> ) e para o banco de dado de back-end, se sua solução usar uma.

 Não é necessário atualizar explicitamente a fonte de dados na memória quando você executa uma vinculação de dados complexa usando o <xref:Microsoft.Office.Tools.Excel.ListObject> controle. Nesse caso, as alterações são enviadas automaticamente para a fonte de dados na memória sem código adicional.

 Para obter mais informações, consulte [como: atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md).

## <a name="see-also"></a>Consulte também
- [Associação de dados e Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms)
- [Como criar um controle de associação simples em um formulário do Windows](/dotnet/framework/winforms/how-to-create-a-simple-bound-control-on-a-windows-form)
- [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)
- [Salvar dados novamente no banco de dados](../data-tools/save-data-back-to-the-database.md)
- [Atualizar dados usando um TableAdapter](../data-tools/update-data-by-using-a-tableadapter.md)
- [Dados de cache](../vsto/caching-data.md)
- [Dados em soluções do Office](../vsto/data-in-office-solutions.md)
