---
title: Controle XmlMappedRange
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLMappedRange control, data binding
- XMLMappedRange control
- XMLMappedRange control, events
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 9cf21ceda64fe79996e05426a3379972c3c4be33
ms.sourcegitcommit: 6944ceb7193d410a2a913ecee6f40c6e87e8a54b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/06/2018
ms.locfileid: "35670145"
---
# <a name="xmlmappedrange-control"></a>Controle XmlMappedRange
  O <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle é um intervalo que é criado somente quando um elemento de esquema não repetição é mapeado para uma célula no Microsoft Office Excel. Por exemplo, quando o `maxOccurs` atributo de um elemento de esquema é igual a 1. Depois que o Visual Studio cria o intervalo mapeado de XML, você pode programar em relação a ela diretamente sem ter que percorrer o modelo de objeto do Excel. Você só pode excluir um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle dentro do Excel quando o mapeamento do elemento é removido.  
  
 [!INCLUDE[appliesto_xlalldoc](../vsto/includes/appliesto-xlalldoc-md.md)]  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [como fazer o mapeamento de i: usar XML no Excel?](http://go.microsoft.com/fwlink/?LinkID=130288).  
  
## <a name="bind-data-to-the-control"></a>Associar dados ao controle  
 Um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle dá suporte à associação a um campo de dados único (associação de dados simples). O <xref:Microsoft.Office.Tools.Excel.ListObject> pode de controle dá suporte à vinculação de dados complexos e é criado automaticamente quando um elemento de esquema de repetição é mapeado para uma célula. Para obter mais informações, consulte [controle ListObject](../vsto/listobject-control.md).  
  
 O <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle está vinculado a uma fonte de dados usando o <xref:System.Windows.Forms.Control.DataBindings%2A> propriedade. Quando um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> é adicionado a uma célula de planilha, Visual Studio automaticamente gera um conjunto de dados a partir dos dados em células mapeadas e associa o controle a esse conjunto de dados. A propriedade de associação de dados padrão do <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> é <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Value2%2A>.  
  
 Se os dados no conjunto de dados associados são atualizados por meio de qualquer mecanismo, o <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle reflete as alterações.  
  
## <a name="formatting"></a>Formatação  
 Você pode aplicar a mesma formatação em um <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle que você pode aplicar a um <xref:Microsoft.Office.Interop.Excel.Range>. Isso inclui as bordas, fontes, formato de número e estilos.  
  
## <a name="events"></a>Eventos  
 Os eventos disponíveis para o <xref:Microsoft.Office.Tools.Excel.XmlMappedRange> controle são:  
  
-   <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeDoubleClick>  
  
-   <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BeforeRightClick>  
  
-   <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.BindingContextChanged>  
  
-   <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Change>  
  
-   <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Selected>  
  
-   <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.Deselected>  
  
-   <xref:System.ComponentModel.Component.Disposed>  
  
-   <xref:Microsoft.Office.Tools.Excel.XmlMappedRange.SelectionChange>  
  
## <a name="see-also"></a>Consulte também  
 [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Como: adicionar controles XMLMappedRange a planilhas](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)   
 [Associar dados a controles em soluções do Office](../vsto/binding-data-to-controls-in-office-solutions.md)   
 [Como: mapear esquemas para planilhas dentro do Visual Studio](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  