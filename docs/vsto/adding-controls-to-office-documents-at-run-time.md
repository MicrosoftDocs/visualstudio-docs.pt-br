---
title: Adicionar controles a documentos do Office em tempo de execução
description: Saiba como você pode adicionar controles a um documento Microsoft Office Word e Microsoft Office pasta de trabalho do Excel em tempo de execução.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- host controls [Office development in Visual Studio], adding
- Windows Forms controls [Office development in Visual Studio], adding
- Office documents [Office development in Visual Studio, host controls
- user controls [Office development in Visual Studio], adding at run time
- documents [Office development in Visual Studio], Windows Forms controls
- document-level customizations [Office development in Visual Studio], host controls
- documents [Office development in Visual Studio], host controls
- document-level customizations [Office development in Visual Studio], Windows Forms controls
- controls [Office development in Visual Studio], adding at run time
- helper methods [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 64a4d4dcd2e6115a3b8093a0a9338cb126f49a28
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825128"
---
# <a name="add-controls-to-office-documents-at-run-time"></a>Adicionar controles a documentos do Office em tempo de execução
  Você pode adicionar controles a um documento Microsoft Office Word e Microsoft Office pasta de trabalho do Excel em tempo de execução. Você também pode removê-los em tempo de execução. Os controles que você adiciona ou remove em tempo de execução são chamados de *controles dinâmicos*.

 [!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

 Este tópico descreve os seguintes itens:

- [Gerencie controles em tempo de execução usando coleções de controle](#ControlsCollection).

- [Adicione controles de host a documentos](#HostControls).

- [Adicione controles de Windows Forms a documentos](#WindowsForms).

## <a name="manage-controls-at-run-time-by-using-control-collections"></a><a name="ControlsCollection"></a> Gerenciar controles em tempo de execução usando coleções de controle
 Para adicionar, obter ou remover controles em tempo de execução, use métodos auxiliares <xref:Microsoft.Office.Tools.Excel.ControlCollection> e <xref:Microsoft.Office.Tools.Word.ControlCollection> objetos.

 A maneira de acessar esses objetos depende do tipo de projeto que você está desenvolvendo:

- Em um projeto de nível de documento para Excel, use a <xref:Microsoft.Office.Tools.Excel.Worksheet.Controls%2A> propriedade das `Sheet1` `Sheet2` classes, e `Sheet3` . Para obter mais informações sobre essas classes, consulte a [planilha item de host](../vsto/worksheet-host-item.md).

- Em um projeto de nível de documento para o Word, use a <xref:Microsoft.Office.Tools.Word.Document.Controls%2A> propriedade da `ThisDocument` classe. Para obter mais informações sobre essa classe, consulte [documentar item de host](../vsto/document-host-item.md).

- Em um projeto de suplemento do VSTO para Excel ou Word, use a `Controls` propriedade de um <xref:Microsoft.Office.Tools.Excel.Worksheet> ou <xref:Microsoft.Office.Tools.Word.Document> que você gera em tempo de execução. Para obter mais informações sobre como gerar esses objetos em tempo de execução, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

### <a name="add-controls"></a>Adicionar controles
 Os <xref:Microsoft.Office.Tools.Excel.ControlCollection> <xref:Microsoft.Office.Tools.Word.ControlCollection> tipos e incluem métodos auxiliares que você pode usar para adicionar controles de host e controles de Windows Forms comuns a documentos e planilhas. Cada nome de método tem a `Add` *classe de controle* de formato, em que *classe de controle* é o nome de classe do controle que você deseja adicionar. Por exemplo, para adicionar um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle ao seu documento, use o <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddNamedRange%2A> método.

 O exemplo de código a seguir adiciona um <xref:Microsoft.Office.Tools.Excel.NamedRange> a `Sheet1` em um projeto de nível de documento para Excel.

 [!code-vb[Trin_ExcelWorkbookDynamicControls#3](../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/ThisWorkbook.vb#3)]
 [!code-csharp[Trin_ExcelWorkbookDynamicControls#3](../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/ThisWorkbook.cs#3)]
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/ThisWorkbook.vb" id="Snippet3":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/ThisWorkbook.cs" id="Snippet3":::


### <a name="access-and-delete-controls"></a>Acessar e excluir controles
 Você pode usar a `Controls` propriedade de um <xref:Microsoft.Office.Tools.Excel.Worksheet> ou <xref:Microsoft.Office.Tools.Word.Document> para iterar por todos os controles em seu documento, incluindo os controles adicionados em tempo de design. Os controles que você adiciona em tempo de design também são chamados de *controles estáticos*.

 Você pode remover controles dinâmicos chamando o `Delete` método do controle ou chamando o `Remove` método de cada coleção de controles. O exemplo de código a seguir usa o <xref:Microsoft.Office.Tools.Excel.ControlCollection.Remove%2A> método para remover um <xref:Microsoft.Office.Tools.Excel.NamedRange> de `Sheet1` em um projeto de nível de documento para o Excel.

 [!code-vb[Trin_ExcelWorkbookDynamicControls#4](../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/ThisWorkbook.vb#4)]
 [!code-csharp[Trin_ExcelWorkbookDynamicControls#4](../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/ThisWorkbook.cs#4)]
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/ThisWorkbook.vb" id="Snippet4":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/ThisWorkbook.cs" id="Snippet4":::


 Não é possível remover controles estáticos em tempo de execução. Se você tentar usar o `Delete` método ou `Remove` para remover um controle estático, um <xref:Microsoft.Office.Tools.CannotRemoveControlException> será gerado.

> [!NOTE]
> Não remova programaticamente os controles no `Shutdown` manipulador de eventos do documento. Os elementos da interface do usuário do documento não estão mais disponíveis quando o `Shutdown` evento é gerado. Se você quiser remover os controles antes que o documento seja fechado, adicione seu código ao manipulador de eventos para outro evento, como <xref:Microsoft.Office.Tools.Word.Document.BeforeClose> ou <xref:Microsoft.Office.Tools.Word.Document.BeforeSave> para Word, ou ou <xref:Microsoft.Office.Tools.Excel.Workbook.BeforeClose> <xref:Microsoft.Office.Tools.Excel.Workbook.BeforeSave> para Excel.

## <a name="add-host-controls-to-documents"></a><a name="HostControls"></a> Adicionar controles de host a documentos

Quando você adiciona de forma programática controles de host a documentos, deve fornecer um nome que identifique exclusivamente o controle e deve especificar onde adicionar o controle no documento. Para obter instruções específicas, consulte os seguintes tópicos:

- [Como adicionar controles ListObject a planilhas](../vsto/how-to-add-listobject-controls-to-worksheets.md)

- [Como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)

- [Como: adicionar controles de gráfico a planilhas](../vsto/how-to-add-chart-controls-to-worksheets.md)

- [Como: adicionar controles de conteúdo a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)

- [Como: adicionar controles de indicador a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md)

Para obter mais informações sobre controles de host, consulte [visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md).

Quando um documento é salvo e fechado, todos os controles de host criados dinamicamente são desconectados de seus eventos e perdem sua funcionalidade de ligação de dados. Você pode adicionar código à sua solução para recriar os controles de host quando o documento for reaberto. Para obter mais informações, consulte [manter controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md).

> [!NOTE]
> Os métodos auxiliares não são fornecidos para os seguintes controles de host, porque esses controles não podem ser adicionados programaticamente a documentos: <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> , <xref:Microsoft.Office.Tools.Word.XMLNode> e <xref:Microsoft.Office.Tools.Word.XMLNodes> .

## <a name="add-windows-forms-controls-to-documents"></a><a name="WindowsForms"></a> Adicionar controles de Windows Forms a documentos
 Ao adicionar programaticamente um controle de Windows Forms a um documento, você deve fornecer o local do controle e um nome que identifique exclusivamente o controle. O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] fornece métodos auxiliares para cada controle. Esses métodos são sobrecarregados para que você possa passar um intervalo ou coordenadas específicas para o local do controle.

 Quando um documento é salvo e fechado, todos os controles de Windows Forms criados dinamicamente são removidos do documento. Você pode adicionar código à sua solução para recriar os controles quando o documento for reaberto. Se você criar controles de Windows Forms dinâmicos usando um suplemento do VSTO, os wrappers ActiveX para os controles serão deixados no documento. Para obter mais informações, consulte [manter controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md).

> [!NOTE]
> Os controles de Windows Forms não podem ser adicionados programaticamente a documentos protegidos. Se você desproteger programaticamente um documento do Word ou planilha do Excel para adicionar um controle, deverá escrever código adicional para remover o wrapper ActiveX do controle quando o documento for fechado. O wrapper ActiveX do controle não é excluído automaticamente dos documentos protegidos.

### <a name="add-custom-controls"></a>Adicionar controles personalizados
 Se você quiser adicionar um <xref:System.Windows.Forms.Control> que não tem suporte dos métodos auxiliares disponíveis, como um controle de usuário personalizado, use os seguintes métodos:

- Para o Excel, use um dos <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddControl%2A> métodos de um <xref:Microsoft.Office.Tools.Excel.ControlCollection> objeto.

- Para o Word, use um dos <xref:Microsoft.Office.Tools.Word.ControlCollection.AddControl%2A> métodos de um <xref:Microsoft.Office.Tools.Word.ControlCollection> objeto.

  Para adicionar o controle, passe o <xref:System.Windows.Forms.Control> , um local para o controle e um nome que identifique exclusivamente o controle para o `AddControl` método. O `AddControl` método retorna um objeto que define como o controle interage com a planilha ou o documento. O `AddControl` método retorna um <xref:Microsoft.Office.Tools.Excel.ControlSite> (para Excel) ou um <xref:Microsoft.Office.Tools.Word.ControlSite> objeto (para Word).

  O exemplo de código a seguir demonstra como usar o <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddControl%2A> método para adicionar dinamicamente um controle de usuário personalizado a uma planilha em um projeto do Excel de nível de documento. Neste exemplo, o controle de usuário é nomeado `UserControl1` e o <xref:Microsoft.Office.Interop.Excel.Range> é nomeado `range1` . Para usar este exemplo, execute-o de uma `Sheet` classe *n* no projeto.

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet2":::
  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet2":::

### <a name="use-members-of-custom-controls"></a>Usar membros de controles personalizados
 Depois de usar um dos `AddControl` métodos para adicionar um controle a uma planilha ou documento, agora você tem dois objetos de controle diferentes:

- O <xref:System.Windows.Forms.Control> que representa o controle personalizado.

- O `ControlSite` `OLEObject` objeto, ou `OLEControl` que representa o controle depois que ele foi adicionado à planilha ou ao documento.

  Muitas propriedades e métodos são compartilhados entre esses controles. É importante que você acesse esses membros por meio do controle apropriado:

- Para acessar membros que pertencem somente ao controle personalizado, use o <xref:System.Windows.Forms.Control> .

- Para acessar membros compartilhados pelos controles, use o `ControlSite` `OLEObject` objeto, ou `OLEControl` .

  Se você acessar um membro compartilhado do <xref:System.Windows.Forms.Control> , ele poderá falhar sem aviso ou notificação ou poderá produzir resultados inválidos. Sempre use métodos ou propriedades do `ControlSite` objeto, `OLEObject` ou, `OLEControl` a menos que o método ou a propriedade necessária não esteja disponível; somente depois, você deve fazer referência a <xref:System.Windows.Forms.Control> .

  Por exemplo, a <xref:Microsoft.Office.Tools.Excel.ControlSite> classe e a <xref:System.Windows.Forms.Control> classe têm uma `Top` propriedade. Para obter ou definir a distância entre a parte superior do controle e a parte superior do documento, use a <xref:Microsoft.Office.Tools.Excel.ControlSite.Top%2A> propriedade de <xref:Microsoft.Office.Tools.Excel.ControlSite> , não a <xref:System.Windows.Forms.Control.Top%2A> Propriedade do <xref:System.Windows.Forms.Control> .

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/my excel chart/Sheet1.vb" id="Snippet3":::
  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingControlsExcelCS/Sheet1.cs" id="Snippet3":::

## <a name="see-also"></a>Consulte também
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Persistir controles dinâmicos em documentos do Office](../vsto/persisting-dynamic-controls-in-office-documents.md)
- [Como adicionar controles ListObject a planilhas](../vsto/how-to-add-listobject-controls-to-worksheets.md)
- [Como: adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)
- [Como: adicionar controles de gráfico a planilhas](../vsto/how-to-add-chart-controls-to-worksheets.md)
- [Como: adicionar controles de conteúdo a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)
- [Como: adicionar controles de indicador a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md)
- [Visão geral dos controles de Windows Forms em documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md)
- [Como: adicionar controles de Windows Forms a documentos do Office](../vsto/how-to-add-windows-forms-controls-to-office-documents.md)
