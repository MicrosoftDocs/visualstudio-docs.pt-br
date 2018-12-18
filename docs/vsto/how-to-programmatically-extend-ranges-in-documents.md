---
title: 'Como: estender programaticamente os intervalos em documentos'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, extending
- documents [Office development in Visual Studio], extending ranges
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 810f65cbb021845c4fa659cd785e83e8c979376d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49888665"
---
# <a name="how-to-programmatically-extend-ranges-in-documents"></a>Como: programaticamente estender intervalos em documentos
  Depois de definir uma <xref:Microsoft.Office.Interop.Word.Range> do objeto em um documento do Microsoft Office Word, alterar seus pontos inicial e final usando o <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> e <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> métodos. O <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> e <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> métodos usam os mesmos dois argumentos *unidade* e *contagem*. O *contagem* argumento é o número de unidades a serem movidas e o *unidade* argumento pode ser um dos seguintes <xref:Microsoft.Office.Interop.Word.WdUnits> valores:  
  
- <xref:Microsoft.Office.Interop.Word.WdUnits.wdCharacter>  
  
- <xref:Microsoft.Office.Interop.Word.WdUnits.wdWord>  
  
- <xref:Microsoft.Office.Interop.Word.WdUnits.wdSentence>  
  
- <xref:Microsoft.Office.Interop.Word.WdUnits.wdParagraph>  
  
- <xref:Microsoft.Office.Interop.Word.WdUnits.wdSection>  
  
- <xref:Microsoft.Office.Interop.Word.WdUnits.wdStory>  
  
- <xref:Microsoft.Office.Interop.Word.WdUnits.wdCell>  
  
- <xref:Microsoft.Office.Interop.Word.WdUnits.wdColumn>  
  
- <xref:Microsoft.Office.Interop.Word.WdUnits.wdRow>  
  
- <xref:Microsoft.Office.Interop.Word.WdUnits.wdTable>  
  
  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
  O exemplo a seguir define um intervalo de sete caracteres. Ele move a posição inicial dos caracteres de intervalo de sete, em seguida, após a posição inicial do original. Como a posição final do intervalo também era sete caracteres após a posição inicial, o resultado é um intervalo que consiste em caracteres. O código, em seguida, move os sete caracteres do final posição após a posição final atual.  
  
## <a name="to-extend-a-range"></a>Para estender um intervalo  
  
1.  Defina um intervalo de caracteres. Para obter mais informações, consulte [como: definir e selecionar intervalos em documentos programaticamente](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md).  
  
     O exemplo de código a seguir pode ser usado em uma personalização no nível de documento.  
  
     [!code-vb[Trin_VstcoreWordAutomation#39](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#39)]
     [!code-csharp[Trin_VstcoreWordAutomation#39](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#39)]  
  
     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Este exemplo usa o documento ativo.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#39](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#39)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#39](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#39)]  
  
2.  Use o <xref:Microsoft.Office.Interop.Word.Range.MoveStart%2A> método da <xref:Microsoft.Office.Interop.Word.Range> objeto para mover a posição de início do intervalo.  
  
     [!code-vb[Trin_VstcoreWordAutomation#40](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#40)]
     [!code-csharp[Trin_VstcoreWordAutomation#40](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#40)]  
  
3.  Use o <xref:Microsoft.Office.Interop.Word.Range.MoveEnd%2A> método da <xref:Microsoft.Office.Interop.Word.Range> objeto para mover a posição final do intervalo.  
  
     [!code-vb[Trin_VstcoreWordAutomation#41](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#41)]
     [!code-csharp[Trin_VstcoreWordAutomation#41](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#41)]  
  
## <a name="document-level-customization-code"></a>Código de personalização de nível de documento  
  
### <a name="to-extend-a-range-in-a-document-level-customization"></a>Para estender um intervalo em uma personalização no nível de documento  
  
1.  O exemplo a seguir mostra o código completo para uma personalização no nível de documento. Para usar esse código, executá-la na `ThisDocument` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomation#38](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#38)]
     [!code-csharp[Trin_VstcoreWordAutomation#38](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#38)]  
  
## <a name="vsto-add-in-code"></a>Código de suplemento do VSTO  
  
### <a name="to-extend-a-range-in-an-application-level-vsto-add-in"></a>Para estender um intervalo em um suplemento do VSTO do nível de aplicativo  
  
1.  O exemplo a seguir mostra o código completo para um suplemento do VSTO. Para usar esse código, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#38](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#38)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#38](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#38)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: programaticamente redefinir intervalos em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)   
 [Como: programaticamente recolher intervalos ou seleções em documentos](../vsto/how-to-programmatically-collapse-ranges-or-selections-in-documents.md)   
 [Como: definir e selecionar intervalos em documentos programaticamente](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Como: recuperar caracteres iniciais e finais em intervalos de forma programática](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)   
 [Como: excluir programaticamente marcas de parágrafo ao criar intervalos](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)  
  