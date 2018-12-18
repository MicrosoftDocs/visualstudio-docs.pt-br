---
title: Associar dados a controles em soluções do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
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
manager: douge
ms.workload:
- office
ms.openlocfilehash: 5b5d7a52e4f8b9e6c9741d3b62bc18b2d4cb66f7
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248014"
---
# <a name="bind-data-to-controls-in-office-solutions"></a>Associar dados a controles em soluções do Office
  Você pode associar controles dos Windows Forms e *hospedar controles* em um documento do Microsoft Office Word ou planilha do Microsoft Office Excel para uma fonte de dados para que os controles exibem automaticamente os dados. Você pode associar dados a controles em projetos de nível de aplicativo e o nível de documento.  
  
 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]  
  
 Controles de host estendem objetos nos modelos de objeto Word e Excel, como controles de conteúdo no Word e intervalos nomeados em Excel. Para obter mais informações, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
 Windows Forms e controles de host a usar o modelo de vinculação de dados do Windows Forms, que dá suporte a ambos *associação de dados simples* e *vinculação de dados complexos* para fontes de dados como conjuntos de dados e tabelas de dados. Para obter informações completas sobre o modelo de vinculação de dados no Windows Forms, consulte [associação de dados e o Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms).  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [como fazer: Consumir dados do banco de dados no Excel? ](http://go.microsoft.com/fwlink/?LinkID=130287).  
  
## <a name="simple-data-binding"></a>Vinculação de dados simples  
 Associação de dados simples existe quando uma propriedade de controle é associada a um elemento de dados, como um valor em uma tabela de dados. Por exemplo, o <xref:Microsoft.Office.Tools.Excel.NamedRange> controle tem um <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> propriedade que pode ser associada a um campo em um conjunto de dados. Quando o campo no conjunto de dados é alterado, o valor do intervalo nomeado também muda. Todos hospedam controles, exceto para o <xref:Microsoft.Office.Tools.Word.XMLNodes> controlar, dão suporte à vinculação de dados simples. O <xref:Microsoft.Office.Tools.Word.XMLNodes> controle é uma coleção e, portanto, ele não oferece suporte a associação de dados.  
  
 Para executar ligação de dados simples para um controle de host, adicione uma <xref:System.Windows.Forms.Binding> para o `DataBindings` propriedade do controle. Um <xref:System.Windows.Forms.Binding> objeto representa a associação simple entre um valor da propriedade do controle e o valor de um elemento de dados.  
  
 O exemplo a seguir demonstra como associar o <xref:Microsoft.Office.Tools.Excel.NamedRange.Value2%2A> propriedade para um elemento de dados em um projeto de nível de documento.  
  
 [!code-vb[Trin_BindableComponent#4](../vsto/codesnippet/VisualBasic/Trin_BindableComponent/Sheet1.vb#4)]
 [!code-csharp[Trin_BindableComponent#4](../vsto/codesnippet/CSharp/Trin_BindableComponent/Sheet1.cs#4)]  
  
 Para instruções passo a passo que demonstra a associação de dados simples, consulte [passo a passo: Associação de dados simples em um projeto de nível de documento](../vsto/walkthrough-simple-data-binding-in-a-document-level-project.md) para um projeto de nível de documento e [passo a passo: Associação de dados simples no projeto do suplemento do VSTO](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md) para um projeto de suplemento do VSTO.  
  
## <a name="complex-data-binding"></a>Vinculação de dados complexos  
 Associação de dados complexos existe quando uma propriedade de controle é associada a mais de um elemento de dados, como várias colunas em uma tabela de dados. O <xref:Microsoft.Office.Tools.Excel.ListObject> controlar para Excel é o único controle de host que dá suporte à vinculação de dados complexos. Também há muitos controles de formulários do Windows que oferecem suporte a vinculação de dados complexos, como o <xref:System.Windows.Forms.DataGridView> controle.  
  
 Para executar ligação de dados complexos, defina o `DataSource` propriedade do controle para um objeto de fonte de dados que é compatível com a vinculação de dados complexos. Por exemplo, o <xref:Microsoft.Office.Tools.Excel.ListObject.DataSource%2A> propriedade do <xref:Microsoft.Office.Tools.Excel.ListObject> controle pode ser associado a várias colunas em uma tabela de dados. Todos os dados na tabela de dados aparece na <xref:Microsoft.Office.Tools.Excel.ListObject> controle e como os dados nas alterações de dados de tabela, o <xref:Microsoft.Office.Tools.Excel.ListObject> também será alterado. Para obter uma lista das fontes de dados que você pode usar para vinculação de dados complexos, consulte [fontes de dados com suporte do Windows Forms](/dotnet/framework/winforms/data-sources-supported-by-windows-forms).  
  
 O exemplo de código a seguir cria uma <xref:System.Data.DataSet> com dois <xref:System.Data.DataTable> objetos e preenche uma das tabelas com dados. O código, em seguida, associa o <xref:Microsoft.Office.Tools.Excel.ListObject> à tabela que contém dados. Este exemplo é para um projeto de nível de documento do Excel.  
  
 [!code-csharp[Trin_ExcelListObject#18](../vsto/codesnippet/CSharp/Trin_ExcelListObject/Trin_ExcelListObject.cs#18)]
 [!code-vb[Trin_ExcelListObject#18](../vsto/codesnippet/VisualBasic/Trin_ExcelListObject/Sheet1.vb#18)]  
  
 Para instruções passo a passo que demonstram a vinculação de dados complexos, consulte [passo a passo: Associação de dados complexos em um projeto de nível de documento](../vsto/walkthrough-complex-data-binding-in-a-document-level-project.md) para um projeto de nível de documento e [passo a passo: Associação de dados complexos no projeto do suplemento do VSTO](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md) para um projeto de suplemento do VSTO.  
  
## <a name="display-data-in-documents-and-workbooks"></a>Exibir dados em documentos e pastas de trabalho  
 Em projetos de nível de documento, você pode usar o **fontes de dados** janela para adicionar controles ligados a dados para seus documentos ou pastas de trabalho com facilidade, da mesma forma que você pode usá-lo para o Windows Forms. Para obter mais informações sobre como usar o **fontes de dados** janela, consulte [controla a associar o Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md) e [adicionar novas fontes de dados](../data-tools/add-new-data-sources.md).  
  
### <a name="drag-controls-from-the-data-sources-window"></a>Arrastar controles da janela fontes de dados  
 Um controle é criado no documento quando você arrasta um objeto para ele partir de **fontes de dados** janela. O tipo de controle que é criado depende se você estiver associando a uma única coluna de dados ou de várias colunas de dados.  
  
 Para Excel, uma <xref:Microsoft.Office.Tools.Excel.NamedRange> controle é criado na planilha para cada campo individual e um <xref:Microsoft.Office.Tools.Excel.ListObject> controle é criado para cada intervalo de dados que inclui várias linhas e colunas. Você pode alterar esse padrão, selecionando a tabela ou campo na **fontes de dados** janela e, em seguida, escolhendo um controle diferente na lista suspensa.  
  
 Um <xref:Microsoft.Office.Tools.Word.ContentControl> controle é adicionado aos documentos. O tipo de controle de conteúdo depende o tipo de dados do campo que você selecionou.  
  
### <a name="bind-data-in-document-level-projects-at-design-time"></a>Associar dados no nível de documento em tempo de design  
 Os tópicos a seguir mostram exemplos de associação de dados em tempo de design:  
  
-   [Como: Preencher planilhas com dados de um banco de dados](../vsto/how-to-populate-worksheets-with-data-from-a-database.md)  
  
-   [Como: Preencher documentos com dados de um banco de dados](../vsto/how-to-populate-documents-with-data-from-a-database.md)  
  
-   [Como: Preencher documentos com dados de objetos](../vsto/how-to-populate-documents-with-data-from-objects.md)  
  
-   [Como: Preencher documentos com dados de serviços](../vsto/how-to-populate-documents-with-data-from-services.md)  
  
-   [Como: Percorrer os registros de banco de dados em uma planilha](../vsto/how-to-scroll-through-database-records-in-a-worksheet.md)  
  
### <a name="bind-data-in-vsto-add-in-projects"></a>Vincular dados em projetos de suplemento do VSTO  
 Em projetos de suplemento do VSTO, você pode adicionar controles apenas em tempo de execução. Os tópicos a seguir mostram exemplos de associação de dados em tempo de execução:  
  
-   [Passo a passo: Associação de dados simples no projeto do suplemento do VSTO](../vsto/walkthrough-simple-data-binding-in-vsto-add-in-project.md)  
  
-   [Passo a passo: Associação de dados complexos no projeto do suplemento do VSTO](../vsto/walkthrough-complex-data-binding-in-vsto-add-in-project.md)  
  
## <a name="update-data-that-is-bound-to-host-controls"></a>Atualizar os dados associados a controles de host  
 Associação de dados entre uma fonte de dados e um controle de host envolve uma atualização de dados bidirecional. Associação de dados simples, as alterações na fonte de dados são refletidas automaticamente no controle de host, mas as alterações no controle de host exigem uma chamada explícita para atualizar a fonte de dados. O motivo é que em alguns casos, as alterações em um campo de associação de dados não são aceitos, a menos que eles são acompanhados por alterações em outro campo de associação de dados. Por exemplo, você pode ter dois campos, um para idade e um para anos de experiência. Experiência não pode exceder a idade. Um usuário não é possível atualizar a idade de 50 para 25 e, em seguida, a experiência de 30 a 10, a menos que ele ou ela faz as alterações ao mesmo tempo. Para resolver esse problema, os campos com associação de dados simples não são atualizados até que as atualizações são enviadas explicitamente pelo código.  
  
 Para atualizar uma fonte de dados dos controles de host que permitem a vinculação de dados simples, você deve enviar atualizações para a fonte de dados na memória (como uma <xref:System.Data.DataSet> ou <xref:System.Data.DataTable>) e para o banco de dados de back-end, se sua solução usa um.  
  
 Você não precisará atualizar explicitamente a fonte de dados na memória quando você executa a associação de dados complexos usando o <xref:Microsoft.Office.Tools.Excel.ListObject> controle. Nesse caso, as alterações são automaticamente enviadas à fonte de dados na memória sem código adicional.  
  
 Confira mais informações em [Como: Atualizar uma fonte de dados com dados de um controle de host](../vsto/how-to-update-a-data-source-with-data-from-a-host-control.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como faço Consumir dados do banco de dados no Excel?](http://go.microsoft.com/fwlink/?LinkID=130287)   
 [Vinculação de dados e do Windows Forms](/dotnet/framework/winforms/data-binding-and-windows-forms)   
 [Como: Criar um controle associado simples em um formulário do Windows](/dotnet/framework/winforms/how-to-create-a-simple-bound-control-on-a-windows-form)   
 [Associar controles do Windows Forms a dados no Visual Studio](../data-tools/bind-windows-forms-controls-to-data-in-visual-studio.md)   
 [Salvar dados no banco de dados](../data-tools/save-data-back-to-the-database.md)    
 [Atualizar dados usando um TableAdapter](../data-tools/update-data-by-using-a-tableadapter.md)    
 [Dados de cache](../vsto/caching-data.md)   
 [Dados em soluções do Office](../vsto/data-in-office-solutions.md)  
  
  