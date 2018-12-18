---
title: Persistir controles dinâmicos em documentos do Office
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office documents [Office development in Visual Studio, Windows Forms controls
- Office documents [Office development in Visual Studio, host controls
- controls [Office development in Visual Studio], persisting in the document
- Windows Forms controls [Office development in Visual Studio], persisting in the document
- documents [Office development in Visual Studio], Windows Forms controls
- documents [Office development in Visual Studio], host controls
- host controls [Office development in Visual Studio], persisting in the document
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b77310f797db3eb031bc311f4fc68bc7fd6b4c56
ms.sourcegitcommit: 0bf2aff6abe485e3fe940f5344a62a885ad7f44e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37059228"
---
# <a name="persist-dynamic-controls-in-office-documents"></a>Persistir controles dinâmicos em documentos do Office

Controles que são adicionados em tempo de execução não são persistidos quando o documento ou pasta de trabalho é salvo e fechada. O comportamento exato é diferente para controles dos Windows Forms e controles de host. Em ambos os casos, você pode adicionar código à sua solução para recriar os controles quando o usuário é reaberto o documento.

Controles que você adicionar a documentos em tempo de execução são chamados *controles dinâmicos*. Para obter mais informações sobre controles dinâmicos, consulte [adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="persist-host-controls-in-the-document"></a>Persistir controles de host no documento

Quando um documento é salvo e, em seguida, fechado, todos os controles de host dinâmico são removidos do documento. Somente nativo Office objetos subjacentes permanecem no local. Por exemplo, uma <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> controle de host se torna um <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName>. Os objetos nativos do Office não estão conectados aos eventos de controle de host, e eles não têm a funcionalidade de associação de dados do controle de host.

A tabela a seguir lista o objeto nativo do Office que é deixado para trás em um documento para cada tipo de controle de host.

|Tipo de controle de host|Tipo de objeto nativo do Office|
|-----------------------|-------------------------------|
|<xref:Microsoft.Office.Tools.Excel.Chart>|<xref:Microsoft.Office.Interop.Excel.Chart>|
|<xref:Microsoft.Office.Tools.Excel.ListObject>|<xref:Microsoft.Office.Interop.Excel.ListObject>|
|<xref:Microsoft.Office.Tools.Excel.NamedRange>|<xref:Microsoft.Office.Interop.Excel.Range>|
|<xref:Microsoft.Office.Tools.Word.Bookmark>|<xref:Microsoft.Office.Interop.Word.Bookmark>|
|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DatePickerContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DropDownListContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.GroupContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PictureContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PlainTextContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|<xref:Microsoft.Office.Interop.Word.ContentControl>|

### <a name="re-create-dynamic-host-controls-when-documents-are-opened"></a>Recriar controles de host dinâmico quando documentos são abertos

Novamente, você pode criar controles de host dinâmico no lugar de controles nativos existentes sempre que um usuário abre o documento. Criando controles de host dessa maneira, quando um documento é aberto simula a experiência que os usuários podem esperar.

Para recriar um controle de host para o Word, ou um <xref:Microsoft.Office.Tools.Excel.NamedRange> ou <xref:Microsoft.Office.Tools.Excel.ListObject> controle de host para o Excel, use um `Add` \< *controlar classe*> método de um <xref:Microsoft.Office.Tools.Excel.ControlCollection?displayProperty=fullName> ou <xref:Microsoft.Office.Tools.Word.ControlCollection?displayProperty=fullName> objeto. Use um método que tem um parâmetro para o objeto nativo do Office.

Por exemplo, se você quiser criar uma <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> hospedar o controle de um existente native <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName> quando o documento for aberto, use o <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddListObject%2A> método e passar existente <xref:Microsoft.Office.Interop.Excel.ListObject>. O exemplo de código a seguir demonstra isso em um projeto de nível de documento para Excel. O código cria novamente dinâmico <xref:Microsoft.Office.Tools.Excel.ListObject> que se baseia em uma existente <xref:Microsoft.Office.Interop.Excel.ListObject> denominado `MyListObject` no `Sheet1` classe.

[!code-csharp[Trin_ExcelWorkbookDynamicControls#6](../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/Sheet1.cs#6)]
[!code-vb[Trin_ExcelWorkbookDynamicControls#6](../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/Sheet1.vb#6)]

### <a name="re-create-chart"></a>Crie o gráfico novamente

Para recriar uma <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> hospedar o controle, você deve primeiro excluir nativo <xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName>e, em seguida, recrie o <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> usando o <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddChart%2A> método. Não há nenhuma `Add` \< *classe de controle*> que permite que você crie um novo método <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> com base em um existente <xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName>.

Se você não excluir primeiro nativo <xref:Microsoft.Office.Interop.Excel.Chart>, em seguida, você criará um gráfico de segundo, duplicado ao recriar o <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName>.

## <a name="persist-windows-forms-controls-in-documents"></a>Persistir controles Windows Forms em documentos

Quando um documento é salvo e, em seguida, fechado, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] remove automaticamente todos os controles de Windows Forms criados dinamicamente do documento. No entanto, o comportamento é diferente para o nível de documento e projetos de suplemento do VSTO.

Em personalizações no nível do documento, os controles e seus wrappers do ActiveX subjacentes (que são usadas para hospedar os controles no documento) são removidos na próxima vez em que o documento é aberto. Não há nenhuma indicação de que os controles foram já existe.

No VSTO Add-ins, os controles são removidos, mas os wrappers de ActiveX permanecem no documento. Na próxima vez que o usuário abre o documento, os wrappers de ActiveX são visíveis. No Excel, os wrappers de ActiveX exibem imagens dos controles, como apareceram a última vez em que o documento foi salvo. No Word, os ActiveX wrappers são invisíveis, a menos que o usuário clica neles, caso em que eles exibem uma linha pontilhada que representa a borda dos controles. Há várias maneiras que você pode remover os wrappers do ActiveX. Para obter mais informações, consulte [remover Wrappers de ActiveX em um suplemento](#removingActiveX).

### <a name="re-create-windows-forms-controls-when-documents-are-opened"></a>Recriar controles dos Windows Forms quando documentos são abertos

Novamente, você pode criar controles de formulários do Windows excluídos quando o usuário é reaberto o documento. Para fazer isso, sua solução deve executar as seguintes tarefas:

1.  Store informações sobre o tamanho, o local e o estado dos controles quando o documento é salvo ou fechado. Em uma personalização no nível de documento, você pode salvar os dados para o cache de dados no documento. Em um suplemento VSTO, você pode salvar os dados a uma parte XML personalizada no documento.

2.  Recrie os controles em um evento que é gerado quando o documento é aberto. Em projetos de nível de documento, você pode fazer isso na `Sheet` *n* `_Startup` ou `ThisDocument_Startup` manipuladores de eventos. Em projetos de suplemento do VSTO, você pode fazer no evento manipuladores para o <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookOpen> ou <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> eventos.

###  <a name="removingActiveX"></a> Remover os wrappers de ActiveX em um suplemento

Quando você adiciona controles dinâmicos do Windows Forms a documentos usando um suplemento do VSTO, você pode impedir que os wrappers de ActiveX para os controles que aparecem no documento na próxima vez que ele é aberto das seguintes maneiras.

#### <a name="remove-activex-wrappers-when-the-document-is-opened"></a>Remover wrappers do ActiveX quando o documento é aberto.

Para remover todos os invólucros de ActiveX, chame o `GetVstoObject` método para gerar um item de host para o <xref:Microsoft.Office.Interop.Word.Document> ou <xref:Microsoft.Office.Interop.Excel.Workbook> que representa o documento aberto recentemente. Por exemplo, para remover todos os invólucros de ActiveX de um documento do Word, você pode chamar o `GetVstoObject` método para gerar um item de host para o <xref:Microsoft.Office.Interop.Word.Document> objeto é passado para o manipulador de eventos para o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> eventos.

Esse procedimento é útil quando você souber que o documento será aberto somente em computadores que têm o suplemento VSTO instalado. Se o documento pode ser passado para outros usuários que não têm o suplemento VSTO instalado, considere remover os controles antes de fechar o documento em vez disso.

O exemplo de código a seguir demonstra como chamar o `GetVstoObject` método quando o documento é aberto.

[!code-vb[Trin_WordAddInDynamicControls#11](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#11)]
[!code-csharp[Trin_WordAddInDynamicControls#11](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#11)]

Embora o `GetVstoObject` método é usado principalmente para gerar um novo item de host em tempo de execução, esse método também limpa todos os invólucros de ActiveX do documento na primeira vez que ele é chamado de um documento específico. Para obter mais informações sobre como usar o `GetVstoObject` método, consulte [pastas de trabalho do Excel em suplementos do VSTO em tempo de execução e de documentos do Word estender](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

Se o suplemento do VSTO cria controles dinâmicos quando o documento for aberto, o suplemento do VSTO já chamará o `GetVstoObject` método como parte do processo para criar os controles. Não é preciso adicionar uma chamada separada para o `GetVstoObject` método para remover os wrappers de ActiveX nesse cenário.

#### <a name="remove-the-dynamic-controls-before-the-document-is-closed"></a>Remova os controles dinâmicos antes do documento é fechado

O suplemento do VSTO pode remover explicitamente cada controle dinâmico do documento antes do documento é fechado. Esse procedimento é útil para documentos que podem ser passados para outros usuários que não têm o suplemento VSTO instalado.

O exemplo de código a seguir demonstra como remover todos os controles de formulários do Windows de um documento do Word, quando o documento é fechado.

[!code-vb[Trin_WordAddInDynamicControls#10](../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb#10)]
[!code-csharp[Trin_WordAddInDynamicControls#10](../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs#10)]

## <a name="see-also"></a>Consulte também

- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
