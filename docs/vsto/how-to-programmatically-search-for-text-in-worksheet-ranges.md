---
title: 'Como: Pesquisar por programação de texto em intervalos de planilhas'
description: Saiba como você pode usar o Visual Studio para Pesquisar texto de forma programática em intervalos de planilha do Microsoft Excel.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- worksheets, searching
- text [Office development in Visual Studio], searching in worksheets
- text searches, worksheets
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 762cb3fc35b43bfd3ad15aea669adff2d370b632
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827936"
---
# <a name="how-to-programmatically-search-for-text-in-worksheet-ranges"></a>Como: Pesquisar por programação de texto em intervalos de planilhas
  O <xref:Microsoft.Office.Interop.Excel.Range.Find%2A> método do <xref:Microsoft.Office.Interop.Excel.Range> objeto permite Pesquisar texto dentro do intervalo. Esse texto também pode ser qualquer uma das cadeias de caracteres de erro que podem aparecer em uma célula de planilha, como `#NULL!` ou `#VALUE!` . Para obter mais informações sobre cadeias de caracteres de erro, consulte [valores de erro de célula](/office/vba/excel/Concepts/Cells-and-Ranges/cell-error-values).

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

 O exemplo a seguir pesquisa um intervalo chamado `Fruits` e modifica a fonte de células que contêm a palavra "maçãs". Esse procedimento também usa o <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> método, que usa as configurações de pesquisa definidas anteriormente para repetir a pesquisa. Você especifica a célula após a qual Pesquisar e o <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> método manipula o restante.

> [!NOTE]
> A <xref:Microsoft.Office.Interop.Excel.Range.FindNext%2A> pesquisa do método volta para o início do intervalo de pesquisa depois que ele atingiu o final do intervalo. Seu código deve garantir que a pesquisa não seja encapsulada em um loop infinito. O procedimento de exemplo mostra uma maneira de lidar com isso usando a <xref:Microsoft.Office.Interop.Excel.Range.Address%2A> propriedade.

## <a name="to-search-for-text-in-a-worksheet-range"></a>Para Pesquisar texto em um intervalo de planilha

1. Declare variáveis para acompanhar todo o intervalo, o primeiro intervalo encontrado e o intervalo localizado atual.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet58":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet58":::

2. Procure a primeira correspondência, especificando todos os parâmetros, exceto a célula a ser pesquisada.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet59":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet59":::

3. Continue pesquisando contanto que haja correspondências.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet60":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet60":::

4. Compare o primeiro intervalo encontrado ( `firstFind` ) a **Nothing**. Se `firstFind` não contiver nenhum valor, o código armazenará o intervalo encontrado ( `currentFind` ).

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet61":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet61":::

5. Saia do loop se o endereço do intervalo encontrado corresponder ao endereço do primeiro intervalo encontrado.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet62":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet62":::

6. Defina a aparência do intervalo encontrado.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet63":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet63":::

7. Execute outra pesquisa.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet64":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet64":::

   O exemplo a seguir mostra o método Complete.

## <a name="example"></a>Exemplo
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet57":::
 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet57":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com intervalos](../vsto/working-with-ranges.md)
- [Como: aplicar estilos programaticamente a intervalos em pastas de trabalho](../vsto/how-to-programmatically-apply-styles-to-ranges-in-workbooks.md)
- [Como fazer referência programaticamente a intervalos de planilha no código](../vsto/how-to-programmatically-refer-to-worksheet-ranges-in-code.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
