---
title: 'Como: Pesquisar texto em intervalos de planilhas de forma programática'
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, searching
- text [Office development in Visual Studio], searching in worksheets
- text searches, worksheets
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: dba0ce5928b61b1ec6b5777e1922cc68f8ed57ee
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53826121"
---
# <a name="how-to-programmatically-search-for-text-in-worksheet-ranges"></a>Como: Pesquisar texto por meio de programação em intervalos de planilhas
  O <xref:Microsoft.Office.Interop.Excel.Range.Find%2A> método da <xref:Microsoft.Office.Interop.Excel.Range> objeto lhe permite pesquisar texto dentro do intervalo. Esse texto pode ser qualquer uma das cadeias de caracteres erro podem aparecer em uma célula de planilha, como também `#NULL!` ou `#VALUE!`. Para obter mais informações sobre cadeias de caracteres de erro, consulte [valores de erro de célula](/office/vba/excel/Concepts/Cells-and-Ranges/cell-error-values).  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 O exemplo a seguir pesquisa um intervalo nomeado `Fruits` e modifica a fonte para as células que contêm a palavra "apples". Esse procedimento também usa o <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> método, que usa o definido anteriormente configurações para repetir a pesquisa de pesquisa. Especifique a célula depois da qual pesquisar e o <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> método cuida do resto.  
  
> [!NOTE]  
>  O <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> pesquisa do método encapsula voltar ao início do intervalo de pesquisa após ele atingir o fim do intervalo. Seu código deve garantir que a pesquisa não quebra ao redor em um loop infinito. O procedimento de exemplo mostra uma maneira de lidar com isso usando o <xref:Microsoft.Office.Interop.Excel.Range.Address%2A> propriedade.  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [como fazer: Usar o método Find em um suplemento do Excel? ](http://go.microsoft.com/fwlink/?LinkID=130294).  
  
## <a name="to-search-for-text-in-a-worksheet-range"></a>Para pesquisar texto em um intervalo de planilha  
  
1. Declare variáveis para todo o intervalo, o primeiro intervalo encontrado e o intervalo encontrado atual do controle.  
  
    [!code-csharp[Trin_VstcoreExcelAutomation#58](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#58)]
    [!code-vb[Trin_VstcoreExcelAutomation#58](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#58)]  
  
2. Pesquisar a primeira correspondência, especificando todos os parâmetros, exceto a célula para pesquisar depois.  
  
    [!code-csharp[Trin_VstcoreExcelAutomation#59](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#59)]
    [!code-vb[Trin_VstcoreExcelAutomation#59](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#59)]  
  
3. Continue pesquisando enquanto há correspondências.  
  
    [!code-csharp[Trin_VstcoreExcelAutomation#60](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#60)]
    [!code-vb[Trin_VstcoreExcelAutomation#60](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#60)]  
  
4. Comparar o primeiro intervalo encontrado (`firstFind`) para **nada**. Se `firstFind` não contém nenhum valor, os repositórios de código fora do intervalo encontrado (`currentFind`).  
  
    [!code-csharp[Trin_VstcoreExcelAutomation#61](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#61)]
    [!code-vb[Trin_VstcoreExcelAutomation#61](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#61)]  
  
5. Sair do loop, se o endereço do intervalo encontrado corresponde ao endereço do primeiro intervalo encontrado.  
  
    [!code-csharp[Trin_VstcoreExcelAutomation#62](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#62)]
    [!code-vb[Trin_VstcoreExcelAutomation#62](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#62)]  
  
6. Defina a aparência do intervalo encontrado.  
  
    [!code-csharp[Trin_VstcoreExcelAutomation#63](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#63)]
    [!code-vb[Trin_VstcoreExcelAutomation#63](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#63)]  
  
7. Execute outra pesquisa.  
  
    [!code-csharp[Trin_VstcoreExcelAutomation#64](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#64)]
    [!code-vb[Trin_VstcoreExcelAutomation#64](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#64)]  
  
   O exemplo a seguir mostra o método complete.  
  
## <a name="example"></a>Exemplo  
 [!code-csharp[Trin_VstcoreExcelAutomation#57](../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs#57)]
 [!code-vb[Trin_VstcoreExcelAutomation#57](../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb#57)]  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhar com intervalos](../vsto/working-with-ranges.md)   
 [Como: Aplicar estilos a intervalos em pastas de trabalho programaticamente](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)   
 [Como: Por meio de programação se referir a intervalos de planilhas em código](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)   
 [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)  
