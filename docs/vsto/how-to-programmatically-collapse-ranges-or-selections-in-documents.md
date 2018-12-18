---
title: 'Como: programaticamente recolher intervalos ou seleções em documentos'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- selections, collapsing
- documents [Office development in Visual Studio], collapsing ranges
- collapsing selections
- ranges, collapsing
- collapsing ranges
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: fee3c821c0b6a39c8dfb499caa00355aa008d413
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49906722"
---
# <a name="how-to-programmatically-collapse-ranges-or-selections-in-documents"></a>Como: programaticamente recolher intervalos ou seleções em documentos
  Se você estiver trabalhando com um <xref:Microsoft.Office.Interop.Word.Range> ou <xref:Microsoft.Office.Interop.Word.Selection> do objeto, você talvez queira alterar a seleção para um ponto de inserção antes de inserir texto, para evitar a substituição de texto existente. Tanto a <xref:Microsoft.Office.Interop.Word.Range> e <xref:Microsoft.Office.Interop.Word.Selection> objetos têm um método de recolher, que usa o <xref:Microsoft.Office.Interop.Word.WdCollapseDirection> valores de enumeração:  
  
- <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseStart> Recolhe a seleção para o início da seleção. Esse é o padrão se você não especificar um valor de enumeração.  
  
- <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseEnd> Recolhe a seleção até o final da seleção.  
  
  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="to-collapse-a-range-and-insert-new-text"></a>Para recolher um intervalo e inserir novo texto  
  
1. Criar um <xref:Microsoft.Office.Interop.Word.Range> objeto que consiste o primeiro parágrafo no documento.  
  
    O exemplo de código a seguir pode ser usado em uma personalização no nível de documento.  
  
    [!code-vb[Trin_VstcoreWordAutomation#46](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#46)]
    [!code-csharp[Trin_VstcoreWordAutomation#46](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#46)]  
  
    O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Esse código usa o documento ativo.  
  
    [!code-vb[Trin_VstcoreWordAutomationAddIn#46](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#46)]
    [!code-csharp[Trin_VstcoreWordAutomationAddIn#46](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#46)]  
  
2. Use o <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseStart> valor de enumeração para recolher o intervalo.  
  
    [!code-vb[Trin_VstcoreWordAutomation#47](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#47)]
    [!code-csharp[Trin_VstcoreWordAutomation#47](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#47)]  
  
3. Inserir o novo texto.  
  
    [!code-vb[Trin_VstcoreWordAutomation#48](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#48)]
    [!code-csharp[Trin_VstcoreWordAutomation#48](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#48)]  
  
4. Selecione o <xref:Microsoft.Office.Interop.Word.Range>.  
  
    [!code-vb[Trin_VstcoreWordAutomation#49](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#49)]
    [!code-csharp[Trin_VstcoreWordAutomation#49](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#49)]  
  
   Se você usar o <xref:Microsoft.Office.Interop.Word.WdCollapseDirection.wdCollapseEnd> valor de enumeração, o texto é inserido no início do parágrafo seguinte.  
  
   [!code-vb[Trin_VstcoreWordAutomation#50](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#50)]
   [!code-csharp[Trin_VstcoreWordAutomation#50](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#50)]  
  
   Você pode esperar que a inserção de uma nova frase pode inseri-la antes do marcador de parágrafo, mas que é o caso de não porque o intervalo original inclui o marcador de parágrafo. Para obter mais informações, consulte [como: excluir programaticamente marcas de parágrafo ao criar intervalos](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md).  
  
## <a name="document-level-customization-example"></a>Exemplo de personalização no nível de documento  
  
### <a name="to-collapse-a-range-in-a-document-level-customization"></a>Para recolher um intervalo em uma personalização no nível de documento  
  
1.  O exemplo a seguir mostra o método completo para uma personalização no nível de documento. Para usar esse código, executá-la na `ThisDocument` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomation#45](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#45)]
     [!code-csharp[Trin_VstcoreWordAutomation#45](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#45)]  
  
## <a name="vsto-add-in-example"></a>Exemplo de suplemento do VSTO  
  
### <a name="to-collapse-a-range-in-a-vsto-add-in"></a>Para recolher um intervalo em um suplemento do VSTO  
  
1.  O exemplo a seguir mostra o método completo para um suplemento do VSTO. Para usar esse código, executá-la na `ThisAddIn` classe em seu projeto.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#45](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#45)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#45](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#45)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: programaticamente, inserir texto em documentos do Word](../vsto/how-to-programmatically-insert-text-into-word-documents.md)   
 [Como: definir e selecionar intervalos em documentos programaticamente](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Como: recuperar caracteres iniciais e finais em intervalos de forma programática](../vsto/how-to-programmatically-retrieve-start-and-end-characters-in-ranges.md)   
 [Como: excluir programaticamente marcas de parágrafo ao criar intervalos](../vsto/how-to-programmatically-exclude-paragraph-marks-when-creating-ranges.md)   
 [Como: estender programaticamente os intervalos em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)   
 [Como: programaticamente redefinir intervalos em documentos do Word](../vsto/how-to-programmatically-reset-ranges-in-word-documents.md)  
  