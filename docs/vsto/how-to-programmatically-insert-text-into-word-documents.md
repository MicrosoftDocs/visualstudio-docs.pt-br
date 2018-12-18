---
title: 'Como: programaticamente, inserir texto em documentos do Word'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ranges, inserting text in documents
- text [Office development in Visual Studio], inserting in documents
- ranges, replacing text in documents
- documents [Office development in Visual Studio], inserting text
- text [Office development in Visual Studio], replacing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: a602f50e9d3c439fc450c286923341dafff1e116
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49881658"
---
# <a name="how-to-programmatically-insert-text-into-word-documents"></a>Como: programaticamente, inserir texto em documentos do Word
  Há três formas principais para inserir texto em documentos do Microsoft Office Word:  
  
-   Inserir texto em um intervalo.  
  
-   Substitua o texto em um intervalo com o novo texto.  
  
-   Use o <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> método de um <xref:Microsoft.Office.Interop.Word.Selection> objeto a ser inserido texto na seleção ou cursor.  
  
> [!NOTE]  
>  Você também pode inserir texto em controles de conteúdo e indicadores. Para obter mais informações, consulte [controles de conteúdo](../vsto/content-controls.md) e [controle do indicador](../vsto/bookmark-control.md).  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
## <a name="insert-text-in-a-range"></a>Inserir texto em um intervalo  
 Use o <xref:Microsoft.Office.Interop.Word.Range.Text%2A> propriedade de um <xref:Microsoft.Office.Interop.Word.Range> objeto para inserir texto em um documento.  
  
### <a name="to-insert-text-in-a-range"></a>Para inserir texto em um intervalo  
  
1.  Especifique um intervalo no início de um documento e inserir o texto **novo texto**.  
  
     O exemplo de código a seguir pode ser usado em uma personalização no nível de documento.  
  
     [!code-vb[Trin_VstcoreWordAutomation#51](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#51)]
     [!code-csharp[Trin_VstcoreWordAutomation#51](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#51)]  
  
     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Esse código usa o documento ativo.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#51](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#51)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#51](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#51)]  
  
2.  Selecione o <xref:Microsoft.Office.Interop.Word.Range> objeto, que foi expandida de um caractere para o comprimento do texto inserido.  
  
     [!code-vb[Trin_VstcoreWordAutomation#52](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#52)]
     [!code-csharp[Trin_VstcoreWordAutomation#52](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#52)]  
  
## <a name="replace-text-in-a-range"></a>Substituir texto em um intervalo  
 Se o intervalo especificado contiver texto, todo o texto no intervalo é substituído pelo texto inserido.  
  
### <a name="to-replace-text-in-a-range"></a>Para substituir o texto em um intervalo  
  
1.  Criar um <xref:Microsoft.Office.Interop.Word.Range> objeto que consiste em 12 primeiros caracteres no documento.  
  
     O exemplo de código a seguir pode ser usado em uma personalização no nível de documento.  
  
     [!code-vb[Trin_VstcoreWordAutomation#53](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#53)]
     [!code-csharp[Trin_VstcoreWordAutomation#53](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#53)]  
  
     O exemplo de código a seguir pode ser usado em um suplemento do VSTO. Esse código usa o documento ativo.  
  
     [!code-vb[Trin_VstcoreWordAutomationAddIn#53](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#53)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#53](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#53)]  
  
2.  Substitua esses caracteres com a cadeia de caracteres **novo texto**.  
  
     [!code-vb[Trin_VstcoreWordAutomation#54](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#54)]
     [!code-csharp[Trin_VstcoreWordAutomation#54](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#54)]  
  
3.  Selecione o intervalo.  
  
     [!code-vb[Trin_VstcoreWordAutomation#55](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#55)]
     [!code-csharp[Trin_VstcoreWordAutomation#55](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#55)]  
  
## <a name="insert-text-using-typetext"></a>Inserir texto usando TypeText  
 O <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> método insere texto na seleção. <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A> se comporta de forma diferente, dependendo das opções definidas no computador do usuário. O código no procedimento a seguir declara uma <xref:Microsoft.Office.Interop.Word.Selection> variável de objeto e desativa o **sobrescrever** opção se ele está ligado. Se o **sobrescrever** opção é ativada, em seguida, qualquer texto ao lado do cursor será substituído.  
  
### <a name="to-insert-text-using-the-typetext-method"></a>Para inserir texto usando o método TypeText  
  
1. Declarar um <xref:Microsoft.Office.Interop.Word.Selection> variável de objeto.  
  
    [!code-vb[Trin_VstcoreWordAutomation#57](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#57)]
    [!code-csharp[Trin_VstcoreWordAutomation#57](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#57)]  
  
2. Desativar o **sobrescrever** opção se ele está ligado.  
  
    [!code-vb[Trin_VstcoreWordAutomation#58](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#58)]
    [!code-csharp[Trin_VstcoreWordAutomation#58](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#58)]  
  
3. Teste para ver se a seleção atual é um ponto de inserção.  
  
    Se for, o código insere usando uma frase <xref:Microsoft.Office.Interop.Word.Selection.TypeText%2A>e, em seguida, um parágrafo marca usando o <xref:Microsoft.Office.Interop.Word.Selection.TypeParagraph%2A> método.  
  
    [!code-vb[Trin_VstcoreWordAutomation#59](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#59)]
    [!code-csharp[Trin_VstcoreWordAutomation#59](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#59)]  
  
4. O código a **ElseIf** bloquear testa para ver se a seleção é uma seleção normal. Se for, em seguida, outro **se** bloquear testa para ver se o **ReplaceSelection** opção está ativada. Se for, o código usa o <xref:Microsoft.Office.Interop.Word.Selection.Collapse%2A> método de seleção para recolher a seleção para um ponto de inserção no início do bloco de texto selecionado. Insira o texto e uma marca de parágrafo.  
  
    [!code-vb[Trin_VstcoreWordAutomation#60](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#60)]
    [!code-csharp[Trin_VstcoreWordAutomation#60](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#60)]  
  
5. Se a seleção não for um ponto de inserção ou de um bloco de texto selecionado e, em seguida, o código na **Else** bloco não faz nada.  
  
    [!code-vb[Trin_VstcoreWordAutomation#61](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#61)]
    [!code-csharp[Trin_VstcoreWordAutomation#61](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#61)]  
  
   Você também pode usar o <xref:Microsoft.Office.Interop.Word.Selection.TypeBackspace%2A> método da <xref:Microsoft.Office.Interop.Word.Selection> objeto, que imita a funcionalidade dos **Backspace** em seu teclado. No entanto, quando se trata de inserção e manipulação de texto, o <xref:Microsoft.Office.Interop.Word.Range> objeto oferece mais controle.  
  
   O exemplo a seguir mostra todo o código. Para usar este exemplo, execute o código na `ThisDocument` ou `ThisAddIn` classe em seu projeto.  
  
   [!code-vb[Trin_VstcoreWordAutomation#56](../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#56)]
   [!code-csharp[Trin_VstcoreWordAutomation#56](../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#56)]  
  
## <a name="see-also"></a>Consulte também  
 [Como: Formatar o texto em documentos programaticamente](../vsto/how-to-programmatically-format-text-in-documents.md)   
 [Como: definir e selecionar intervalos em documentos programaticamente](../vsto/how-to-programmatically-define-and-select-ranges-in-documents.md)   
 [Como: estender programaticamente os intervalos em documentos](../vsto/how-to-programmatically-extend-ranges-in-documents.md)  
  
  