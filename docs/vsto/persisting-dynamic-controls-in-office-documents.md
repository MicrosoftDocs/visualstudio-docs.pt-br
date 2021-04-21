---
title: Persistir controles dinâmicos em documentos do Office
description: Saiba como você pode adicionar código à sua solução para recriar controles dinâmicos persistentes quando um usuário reabrir um documento fechado.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 9d42aa2d8594ed44e4fd4edbac8a0d64c4dc16da
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826142"
---
# <a name="persist-dynamic-controls-in-office-documents"></a>Persistir controles dinâmicos em documentos do Office

Os controles que são adicionados em tempo de execução não são persistidos quando o documento ou pasta de trabalho é salvo e fechado. O comportamento exato é diferente para controles de host e controles de Windows Forms. Em ambos os casos, você pode adicionar código à sua solução para recriar os controles quando o usuário reabrir o documento.

Os controles que você adiciona aos documentos em tempo de execução são chamados de *controles dinâmicos*. Para obter mais informações sobre controles dinâmicos, consulte [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md).

[!INCLUDE[appliesto_controls](../vsto/includes/appliesto-controls-md.md)]

## <a name="persist-host-controls-in-the-document"></a>Persistir controles de host no documento

Quando um documento é salvo e fechado, todos os controles de host dinâmicos são removidos do documento. Somente os objetos do Office nativos subjacentes permanecem atrás. Por exemplo, um <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> controle de host se torna um <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName> . Os objetos nativos do Office não estão conectados aos eventos de controle de host e não têm a funcionalidade de ligação de dados do controle de host.

A tabela a seguir lista o objeto nativo do Office que é deixado para trás em um documento para cada tipo de controle de host.

|Tipo de controle de host|Tipo de objeto do Office nativo|
|-----------------------|-------------------------------|
|<xref:Microsoft.Office.Tools.Excel.Chart>|<xref:Microsoft.Office.Interop.Excel.Chart>|
|<xref:Microsoft.Office.Tools.Excel.ListObject>|<xref:Microsoft.Office.Interop.Excel.ListObject>|
|<xref:Microsoft.Office.Tools.Excel.NamedRange>|<xref:Microsoft.Office.Interop.Excel.Range>|
|<xref:Microsoft.Office.Tools.Word.Bookmark>|<xref:Microsoft.Office.Interop.Word.Bookmark>|
|<xref:Microsoft.Office.Tools.Word.BuildingBlockGalleryContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ComboBoxContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.ContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DatePickerContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.DropDownListContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.GroupContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PictureContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.PlainTextContentControl><br /><br /> <xref:Microsoft.Office.Tools.Word.RichTextContentControl>|<xref:Microsoft.Office.Interop.Word.ContentControl>|

### <a name="re-create-dynamic-host-controls-when-documents-are-opened"></a>Recriar controles de host dinâmicos quando os documentos forem abertos

Você pode recriar controles de host dinâmicos no lugar de controles nativos existentes toda vez que um usuário abrir o documento. A criação de controles de host dessa maneira quando um documento é aberto simula a experiência que os usuários podem esperar.

Para recriar um controle de host para o Word ou um <xref:Microsoft.Office.Tools.Excel.NamedRange> <xref:Microsoft.Office.Tools.Excel.ListObject> controle de host ou para o Excel, use um `Add` \<*control class*> método de um <xref:Microsoft.Office.Tools.Excel.ControlCollection?displayProperty=fullName> <xref:Microsoft.Office.Tools.Word.ControlCollection?displayProperty=fullName> objeto ou. Use um método que tenha um parâmetro para o objeto do Office nativo.

Por exemplo, se você quiser criar um <xref:Microsoft.Office.Tools.Excel.ListObject?displayProperty=fullName> controle de host de um nativo existente <xref:Microsoft.Office.Interop.Excel.ListObject?displayProperty=fullName> quando o documento for aberto, use o <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddListObject%2A> método e passe o existente <xref:Microsoft.Office.Interop.Excel.ListObject> . O exemplo de código a seguir demonstra isso em um projeto de nível de documento para o Excel. O código recria um dinâmico <xref:Microsoft.Office.Tools.Excel.ListObject> que se baseia em um <xref:Microsoft.Office.Interop.Excel.ListObject> nome existente `MyListObject` na `Sheet1` classe.

:::code language="csharp" source="../vsto/codesnippet/CSharp/trin_excelworkbookdynamiccontrols4/Sheet1.cs" id="Snippet6":::
:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_excelworkbookdynamiccontrols4/Sheet1.vb" id="Snippet6":::

### <a name="re-create-chart"></a>Recriar gráfico

Para recriar um <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> controle de host, você deve primeiro excluir o nativo <xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName> e, em seguida, recriar o <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> usando o <xref:Microsoft.Office.Tools.Excel.ControlCollection.AddChart%2A> método. Não há nenhum `Add` \<*control class*> método que permita criar um novo <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> com base em um existente <xref:Microsoft.Office.Interop.Excel.Chart?displayProperty=fullName> .

Se você não excluir primeiro o nativo <xref:Microsoft.Office.Interop.Excel.Chart> , você criará um segundo gráfico duplicado ao recriar o <xref:Microsoft.Office.Tools.Excel.Chart?displayProperty=fullName> .

## <a name="persist-windows-forms-controls-in-documents"></a>Persistir controles de Windows Forms em documentos

Quando um documento é salvo e fechado, o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] automaticamente remove todos os controles de Windows Forms criados dinamicamente do documento. No entanto, o comportamento é diferente para projetos de suplemento no nível do documento e do VSTO.

Em personalizações em nível de documento, os controles e seus wrappers ActiveX subjacentes (que são usados para hospedar os controles no documento) são removidos na próxima vez em que o documento for aberto. Não há nenhuma indicação de que os controles já estavam lá.

Nos suplementos do VSTO, os controles são removidos, mas os invólucros do ActiveX permanecem no documento. Na próxima vez que o usuário abrir o documento, os invólucros do ActiveX ficarão visíveis. No Excel, os wrappers ActiveX exibem imagens dos controles à medida que aparecem na última vez em que o documento foi salvo. No Word, os wrappers ActiveX são invisíveis, a menos que o usuário clique neles, caso em que eles exibem uma linha pontilhada que representa a borda dos controles. Há várias maneiras pelas quais você pode remover os invólucros do ActiveX. Para obter mais informações, consulte [remover wrappers ActiveX em um suplemento](#removingActiveX).

### <a name="re-create-windows-forms-controls-when-documents-are-opened"></a>Recriar Windows Forms controles quando os documentos são abertos

Você pode recriar os controles de Windows Forms excluídos quando o usuário reabrir o documento. Para fazer isso, sua solução deve executar as seguintes tarefas:

1. Armazene informações sobre o tamanho, o local e o estado dos controles quando o documento for salvo ou fechado. Em uma personalização em nível de documento, você pode salvar os dados no cache de dados no documento. Em um suplemento do VSTO, você pode salvar os dados em uma parte XML personalizada no documento.

2. Crie novamente os controles em um evento que é gerado quando o documento é aberto. Em projetos de nível de documento, você pode fazer isso no `Sheet` *n* `_Startup` ou `ThisDocument_Startup` manipuladores de eventos. Em projetos de suplemento do VSTO, você pode fazer isso nos manipuladores de eventos para os <xref:Microsoft.Office.Interop.Excel.AppEvents_Event.WorkbookOpen> <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> eventos ou.

### <a name="remove-activex-wrappers-in-an-add-in"></a><a name="removingActiveX"></a> Remover wrappers ActiveX em um suplemento

Quando você adiciona controles de Windows Forms dinâmicos a documentos usando um suplemento do VSTO, você pode impedir que os wrappers do ActiveX sejam exibidos no documento na próxima vez que forem abertos das seguintes maneiras.

#### <a name="remove-activex-wrappers-when-the-document-is-opened"></a>Remover wrappers ActiveX quando o documento for aberto

Para remover todos os wrappers ActiveX, chame o `GetVstoObject` método para gerar um item de host para o <xref:Microsoft.Office.Interop.Word.Document> ou <xref:Microsoft.Office.Interop.Excel.Workbook> que representa o documento recentemente aberto. Por exemplo, para remover todos os wrappers ActiveX de um documento do Word, você pode chamar o `GetVstoObject` método para gerar um item de host para o <xref:Microsoft.Office.Interop.Word.Document> objeto que é passado ao manipulador de eventos para o <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen> evento.

Esse procedimento é útil quando você sabe que o documento será aberto somente em computadores que têm o suplemento do VSTO instalado. Se o documento puder ser passado para outros usuários que não têm o suplemento do VSTO instalado, considere remover os controles antes de fechar o documento.

O exemplo de código a seguir demonstra como chamar o `GetVstoObject` método quando o documento é aberto.

:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet11":::
:::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet11":::

Embora o `GetVstoObject` método seja usado principalmente para gerar um novo item de host em tempo de execução, esse método também limpa todos os wrappers ActiveX do documento na primeira vez que é chamado para um documento específico. Para obter mais informações sobre como usar o `GetVstoObject` método, consulte [estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).

Se o suplemento do VSTO criar controles dinâmicos quando o documento for aberto, o suplemento do VSTO já chamará o `GetVstoObject` método como parte do processo para criar os controles. Você não precisa adicionar uma chamada separada ao `GetVstoObject` método para remover os wrappers ActiveX nesse cenário.

#### <a name="remove-the-dynamic-controls-before-the-document-is-closed"></a>Remover os controles dinâmicos antes de fechar o documento

Seu suplemento do VSTO pode remover explicitamente cada controle dinâmico do documento antes de o documento ser fechado. Esse procedimento é útil para documentos que podem ser passados para outros usuários que não têm o suplemento do VSTO instalado.

O exemplo de código a seguir demonstra como remover todos os controles de Windows Forms de um documento do Word quando o documento é fechado.

:::code language="vb" source="../vsto/codesnippet/VisualBasic/trin_wordaddindynamiccontrols/ThisAddIn.vb" id="Snippet10":::
:::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_WordAddInDynamicControls/ThisAddIn.cs" id="Snippet10":::

## <a name="see-also"></a>Consulte também

- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
