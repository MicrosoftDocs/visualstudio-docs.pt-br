---
title: Use controles de Windows Forms em planilhas do Excel
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Windows Forms controls [Office development in Visual Studio], Excel
- Excel [Office development in Visual Studio], Windows Forms controls
- controls [Office development in Visual Studio], Window Forms controls
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: fd367087f48ababb390ddd87e289ec22258b4921
ms.sourcegitcommit: 4cd4aef53e7035d23e7d1d0f66f51ac8480622a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34767917"
---
# <a name="use-windows-forms-controls-on-excel-worksheets"></a>Use controles de Windows Forms em planilhas do Excel
  Você pode adicionar controles de formulários do Windows para suas pastas de trabalho do Microsoft Office Excel da mesma maneira que você adicione controles de formulários do Windows. Para obter informações gerais sobre como trabalhar com controles em documentos, consulte [controles do Windows Forms em Visão geral de documentos do Office](../vsto/windows-forms-controls-on-office-documents-overview.md).  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
## <a name="control-considerations-for-excel"></a>Considerações sobre o controle para o Excel  
 Há algumas considerações que são específicas para o Excel.  
  
### <a name="match-control-size-to-cell-size"></a>Tamanho do controle de correspondência para o tamanho da célula  
 Você pode definir o controle a ser redimensionado automaticamente quando o tamanho da célula pai for alterado. Para obter mais informações, consulte [como: redimensionar controles dentro das células da planilha](../vsto/how-to-resize-controls-within-worksheet-cells.md).  
  
### <a name="add-components-that-are-shared-by-all-worksheets"></a>Adicionar componentes que são compartilhados por todas as planilhas  
 Você pode adicionar os componentes que você deseja compartilhar entre todas as planilhas, como um <xref:System.Data.DataSet>, para o Designer de pasta de trabalho em vez de para planilhas. O componente será exibido na bandeja do componente.  
  
### <a name="formula-for-embedding-controls"></a>Fórmula para inserção de controles  
 Quando você seleciona um controle no Excel, você verá **=EMBED("WinForms.Control.Host","")** no **barra de fórmulas**. Esse texto é necessário e não deve ser excluído.  
  
## <a name="see-also"></a>Consulte também  
 [Como: redimensionar controles dentro das células da planilha](../vsto/how-to-resize-controls-within-worksheet-cells.md)   
 [Como: ocultar controles em planilhas durante a impressão](../vsto/how-to-hide-controls-on-worksheets-when-printing.md)   
 [Passo a passo: Alterar a formatação da planilha usando controles CheckBox](../vsto/walkthrough-changing-worksheet-formatting-using-checkbox-controls.md)   
 [Passo a passo: Exibir texto em uma caixa de texto em uma planilha usando um botão](../vsto/walkthrough-displaying-text-in-a-text-box-in-a-worksheet-using-a-button.md)   
 [Passo a passo: Atualizar um gráfico em uma planilha usando botões de opção](../vsto/walkthrough-updating-a-chart-in-a-worksheet-using-radio-buttons.md)  
  
  