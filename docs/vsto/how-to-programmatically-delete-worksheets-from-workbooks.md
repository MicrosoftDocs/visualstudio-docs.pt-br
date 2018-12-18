---
title: 'Como: excluir planilhas de pastas de trabalho de forma programática'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, deleting worksheets
- worksheets, deleting
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 73c501d545f76012b63bde291001b38c214c3eb6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49950219"
---
# <a name="how-to-programmatically-delete-worksheets-from-workbooks"></a>Como: excluir planilhas de pastas de trabalho de forma programática
  Você pode excluir qualquer planilha em uma pasta de trabalho. Para excluir uma planilha, use o item de host da planilha ou acessar a planilha usando a coleção de planilhas da pasta de trabalho.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="use-the-worksheet-host-item"></a>Use o item de host da planilha  
 Se a planilha foi adicionada em tempo de design em uma personalização no nível de documento, use o <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> método para excluir uma planilha especificada. O código a seguir exclui uma planilha de uma pasta de trabalho referenciando o item de host da planilha diretamente.  
  
> [!IMPORTANT]
>  Esse código é executado apenas em projetos que você cria usando qualquer um dos modelos de projeto a seguir:  
> 
> - Pasta de trabalho do Excel 2013  
> - Modelo do Excel 2013  
> - Pasta de trabalho do Excel 2010  
> - Modelo do Excel 2010  
> 
>   Se você quiser executar essa tarefa em qualquer outro tipo de projeto, você deve adicionar uma referência para o **Interop** assembly e, em seguida, você deve usar classes do assembly para abrir uma pasta de trabalho e excluir uma planilha. Para obter mais informações, consulte [como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md) e [referência de assembly de interoperabilidade primária do Excel 2010](http://go.microsoft.com/fwlink/?LinkId=189585).  
  
### <a name="to-delete-a-worksheet-by-using-a-worksheet-host-item"></a>Para excluir uma planilha usando um item de host da planilha  
  
1.  Chame o método <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> de `Sheet1`.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#17](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#17)]
     [!code-vb[Trin_VstcoreExcelAutomation#17](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#17)]  
  
## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Usar a coleção de planilhas da pasta de trabalho do Excel  
 Acessar planilhas por meio do Microsoft Office Excel <xref:Microsoft.Office.Interop.Excel.Sheets> coleção nos seguintes casos:  
  
- Você deseja excluir uma planilha em um suplemento do VSTO.  
  
- A planilha que você deseja excluir foi criada em tempo de execução em uma personalização no nível de documento.  
  
  O código a seguir exclui uma planilha de uma pasta de trabalho referenciando a folha até o número de índice do **folhas** coleção. Esse código supõe que uma nova planilha foi criada por meio de programação.  
  
> [!IMPORTANT]  
>  Se você quiser executar essa tarefa em qualquer outro tipo de projeto, você deve adicionar uma referência para o **Interop** assembly e, em seguida, você deve usar classes do assembly para abrir uma pasta de trabalho e excluir uma planilha. Para obter mais informações, consulte [como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md) e [referência de assembly de interoperabilidade primária do Excel 2010](http://go.microsoft.com/fwlink/?LinkId=189585).  
  
### <a name="to-delete-a-worksheet-by-using-the-sheets-collection-of-the-excel-workbook"></a>Para excluir uma planilha usando a coleção de planilhas da pasta de trabalho do Excel  
  
1.  Chame o <xref:Microsoft.Office.Interop.Excel._Worksheet.Delete%2A> método da <xref:Microsoft.Office.Interop.Excel.Sheets> coleção.  
  
     [!code-csharp[Trin_VstcoreExcelAutomation#18](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#18)]
     [!code-vb[Trin_VstcoreExcelAutomation#18](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#18)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com planilhas](../vsto/working-with-worksheets.md)   
 [Como: ocultar planilhas programaticamente](../vsto/how-to-programmatically-hide-worksheets.md)   
 [Como: mover planilhas em pastas de trabalho de forma programática](../vsto/how-to-programmatically-move-worksheets-within-workbooks.md)   
 [Como: Selecionar planilhas programaticamente](../vsto/how-to-programmatically-select-worksheets.md)   
 [Como: adicionar novas planilhas a pastas de trabalho programaticamente](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md)   
 [Item de host da planilha](../vsto/worksheet-host-item.md)   
 [Acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  