---
title: 'Como: adicionar linhas e colunas de forma programática a tabelas do Word'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- rows [Office development in Visual Studio], adding to Word tables
- tables [Office development in Visual Studio], adding rows and columns
- columns [Office development in Visual Studio], adding to Word tables
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: fca44524c3a7c7f10e855eaf62e8b77dc225ae01
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49818673"
---
# <a name="how-to-programmatically-add-rows-and-columns-to-word-tables"></a>Como: adicionar linhas e colunas de forma programática a tabelas do Word
  Em uma tabela do Microsoft Office Word, as células são organizadas em linhas e colunas. Você pode usar o <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> método da <xref:Microsoft.Office.Interop.Word.Rows> objeto para adicionar linhas à tabela e o <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> método da <xref:Microsoft.Office.Interop.Word.Columns> objeto para adicionar colunas.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="document-level-customization-examples"></a>Exemplos de personalização de nível de documento  
 Os exemplos de código a seguir podem ser usados em uma personalização no nível de documento. Para usar esses exemplos, executá-los pelo `ThisDocument` classe em seu projeto. Esses exemplos pressupõem que o documento associado à sua personalização já tem pelo menos uma tabela.  
  
> [!IMPORTANT]
>  Esse código é executado apenas em projetos que você cria usando qualquer um dos modelos de projeto a seguir:  
> 
> - Documento do Word 2013  
> - Modelo do Word 2013  
> - Documento do Word 2010  
> - Modelo do Word 2010  
> 
>   Se você quiser executar essa tarefa em qualquer outro tipo de projeto, você deve adicionar uma referência para o **Interop** assembly e, em seguida, você deve usar classes do assembly para adicionar linhas e colunas a tabelas. Para obter mais informações, consulte [como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md) e [referência de assembly de interoperabilidade primária do Word 2010](http://go.microsoft.com/fwlink/?LinkId=189588).  
  
### <a name="to-add-a-row-to-a-table"></a>Para adicionar uma linha em uma tabela  
  
1.  Use o <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> método para adicionar uma linha à tabela.  
  
     [!code-vb[Trin_VstcoreWordAutomation#95](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#95)]
     [!code-csharp[Trin_VstcoreWordAutomation#95](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#95)]  
  
### <a name="to-add-a-column-to-a-table"></a>Para adicionar uma coluna a uma tabela  
  
1.  Use o <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> método e, em seguida, use o <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A> método para fazer a mesma largura de todas as colunas.  
  
     [!code-vb[Trin_VstcoreWordAutomation#96](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#96)]
     [!code-csharp[Trin_VstcoreWordAutomation#96](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#96)]  
  
## <a name="vsto-add-in-examples"></a>Exemplos de suplemento do VSTO  
 Os exemplos de código a seguir podem ser usados em um suplemento do VSTO. Para usar os exemplos, executá-los pelo `ThisAddIn` classe em seu projeto. Esses exemplos pressupõem que o documento ativo já tem pelo menos uma tabela.  
  
> [!IMPORTANT]  
>  Esse código é executado apenas em projetos que você cria usando modelos de suplemento do VSTO do Word.  
>   
>  Se você quiser executar essa tarefa em qualquer outro tipo de projeto, você deve adicionar uma referência para o **Interop** assembly e, em seguida, você deve usar classes do assembly para adicionar linhas e colunas a tabelas. Para obter mais informações, consulte [como: aplicativos do Office de destino por meio de assemblies de interoperabilidade primários](../vsto/how-to-target-office-applications-through-primary-interop-assemblies.md) e [referência de assembly de interoperabilidade primária do Word 2010](http://go.microsoft.com/fwlink/?LinkId=189588).  
  
### <a name="to-add-a-row-to-a-table"></a>Para adicionar uma linha em uma tabela  
  
1.  Use o <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> método para adicionar uma linha à tabela.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#95](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#95)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#95](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#95)]  
  
### <a name="to-add-a-column-to-a-table"></a>Para adicionar uma coluna a uma tabela  
  
1.  Use o <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> método e, em seguida, use o <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A> método para fazer a mesma largura de todas as colunas.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#96](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#96)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#96](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#96)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: criar tabelas do Word de forma programática](../vsto/how-to-programmatically-create-word-tables.md)   
 [Como: adicionar texto e formatação a células em tabelas do Word programaticamente](../vsto/how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)   
 [Como: programaticamente preencher tabelas do Word com propriedades do documento](../vsto/how-to-programmatically-populate-word-tables-with-document-properties.md)  
  
  