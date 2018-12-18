---
title: Automatizar o Excel usando objetos estendidos
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel [Office development in Visual Studio], automating
- automation [Office development in Visual Studio], Excel
- host controls, Excel
- Excel [Office development in Visual Studio], host controls
- extended objects [Office development in Visual Studio], Excel
- host controls [Office development in Visual Studio], Excel
- automating Excel
- host items [Office development in Visual Studio], Excel
- controls [Office development in Visual Studio], Excel host controls
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: 0a74c5a62cc2e14615db8dd17c9a34a7e54178e7
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248040"
---
# <a name="automate-excel-by-using-extended-objects"></a>Automatizar o Excel usando objetos estendidos
  Ao desenvolver soluções do Excel no Visual Studio, você pode usar *hospedar itens* e *controle de host*s em suas soluções. Esses são objetos que estendem alguns objetos comumente usados no modelo de objeto do Excel (ou seja, o modelo de objeto que é exposto pelo assembly de interoperabilidade primário para Excel), como o <xref:Microsoft.Office.Interop.Excel.Worksheet> e <xref:Microsoft.Office.Interop.Excel.Range> objetos. Objetos estendidos se comportam como os objetos do Excel se baseiam, mas adicionar recursos adicionais, como novos eventos e recursos de ligação de dados para os objetos.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 Itens de host e controles de host estão disponíveis em ambas as suplemento do VSTO e o nível de documento personalizações, embora o contexto no qual eles podem ser usados é diferente para cada tipo de solução. Para obter mais informações, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
## <a name="excel-host-items"></a>Itens de host do Excel  
 Projetos do Excel fornecem acesso a vários itens de host:  
  
-   <xref:Microsoft.Office.Tools.Excel.Worksheet>. Este item de host contém e representa uma planilha em seu projeto. Ele também atua como um contêiner para controles gerenciados, incluindo controles de host e controles dos Windows Forms, e mantém informações sobre os controles em sua superfície. Para obter mais informações, consulte [item de host da planilha](../vsto/worksheet-host-item.md).  
  
-   <xref:Microsoft.Office.Tools.Excel.Workbook>. Este item de host representa a pasta de trabalho em seu projeto e atua como um contêiner para os componentes que são compartilhados por todas as planilhas na pasta de trabalho. Para obter mais informações, consulte [item de host da pasta de trabalho](../vsto/workbook-host-item.md).  
  
-   <xref:Microsoft.Office.Tools.Excel.ChartSheet>. Uma planilha do Excel que contém apenas um gráfico e expõe eventos de item neste host.  
  
     Quando você adiciona uma folha de gráfico em tempo de design como uma nova folha em seu projeto de personalização no nível de documento do Microsoft Office Excel, o Visual Studio cria automaticamente um <xref:Microsoft.Office.Tools.Excel.ChartSheet> item de host.  
  
     Embora um <xref:Microsoft.Office.Tools.Excel.ChartSheet> item de host é uma planilha do Excel, é possível adicionar todos os controles a planilha de gráfico. Se você quiser ter outros controles em uma planilha com um gráfico, não use uma planilha de gráfico. Em vez disso, você pode colocar um gráfico como um objeto incorporado em uma planilha, usando o <xref:Microsoft.Office.Tools.Excel.Chart> controle de host. Para obter mais informações, consulte [controle gráfico](../vsto/chart-control.md).  
  
## <a name="excel-host-controls"></a>controles de host do Excel  
 Há vários controles de host para Excel que ajudam você a criar, organizar e automatizar as pastas de trabalho e planilhas. Os controles de host fornecem eventos e os recursos de vinculação de dados que não têm equivalentes no modelo de objeto nativo do Excel.  
  
 Para obter mais informações sobre os controles de host que você pode usar em projetos do Excel, consulte os tópicos a seguir:  
  
-   [Controle de gráfico](../vsto/chart-control.md)  
  
-   [Controle ListObject](../vsto/listobject-control.md)  
  
-   [Controle NamedRange](../vsto/namedrange-control.md)  
  
-   [Controle XmlMappedRange](../vsto/xmlmappedrange-control.md)  
  
## <a name="see-also"></a>Consulte também  
 [Como: Preencher controles ListObject com dados](../vsto/how-to-fill-listobject-controls-with-data.md)   
 [Como: Adicionar controles Chart a planilhas](../vsto/how-to-add-chart-controls-to-worksheets.md)   
 [Como: Adicionar controles ListObject a planilhas](../vsto/how-to-add-listobject-controls-to-worksheets.md)   
 [Como: Adicionar controles NamedRange a planilhas](../vsto/how-to-add-namedrange-controls-to-worksheets.md)   
 [Como: Adicionar controles XMLMappedRange a planilhas](../vsto/how-to-add-xmlmappedrange-controls-to-worksheets.md)   
 [Como: Redimensionar controles NamedRange](../vsto/how-to-resize-namedrange-controls.md)   
 [Como: Redimensionar controles ListObject](../vsto/how-to-resize-listobject-controls.md)   
 [Como: Validar dados quando uma nova linha é adicionada a um controle ListObject](../vsto/how-to-validate-data-when-a-new-row-is-added-to-a-listobject-control.md)   
 [Como: Mapear colunas ListObject para dados](../vsto/how-to-map-listobject-columns-to-data.md)   
 [Passo a passo: Programe em eventos de um controle NamedRange](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)   
 [Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)   
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  
