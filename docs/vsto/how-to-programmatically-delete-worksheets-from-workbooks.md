---
title: 'Como: excluir programaticamente planilhas de pastas de trabalho'
description: Saiba como você pode excluir programaticamente qualquer planilha em uma pasta de trabalho do Microsoft Excel usando o item de host de planilha, por exemplo.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- workbooks, deleting worksheets
- worksheets, deleting
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f3413eaf82b323bc23164687dc3ae3ac0b9d3c48
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825934"
---
# <a name="how-to-programmatically-delete-worksheets-from-workbooks"></a>Como: excluir programaticamente planilhas de pastas de trabalho
  Você pode excluir qualquer planilha em uma pasta de trabalho. Para excluir uma planilha, use o item de host da planilha ou acesse a planilha usando a coleção planilhas da pasta de trabalho.

 [!INCLUDE[appliesto_xlalldocapp](includes/appliesto-xlalldocapp-md.md)]

## <a name="use-the-worksheet-host-item"></a>Usar o item de host da planilha
 Se a planilha foi adicionada em tempo de design em uma personalização em nível de documento, use o <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> método para excluir uma planilha especificada. O código a seguir exclui uma planilha de uma pasta de trabalho referenciando o item de host de planilha diretamente.

> [!IMPORTANT]
> Esse código é executado somente em projetos que você cria usando qualquer um dos seguintes modelos de projeto:
>
> - Pasta de trabalho do Excel 2013
> - Modelo do Excel 2013
> - Pasta de trabalho do Excel 2010
> - Modelo do Excel 2010
>
>   Se você quiser executar essa tarefa em qualquer outro tipo de projeto, deverá adicionar uma referência ao assembly **Microsoft. Office. Interop. Excel** e, em seguida, deverá usar classes desse assembly para abrir uma pasta de trabalho e excluir uma planilha. Para obter mais informações, consulte [como: direcionar aplicativos do Office por meio de assemblies de interoperabilidade primária](how-to-target-office-applications-through-primary-interop-assemblies.md) e [referência de assembly de interoperabilidade primária do Excel 2010](office-primary-interop-assemblies.md)

### <a name="to-delete-a-worksheet-by-using-a-worksheet-host-item"></a>Para excluir uma planilha usando um item de host de planilha

1. Chame o método <xref:Microsoft.Office.Tools.Excel.Worksheet.Delete%2A> de `Sheet1`.

     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet17":::
     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet17":::

## <a name="use-the-sheets-collection-of-the-excel-workbook"></a>Usar a coleção Sheets da pasta de trabalho do Excel
 Acesse planilhas por meio da <xref:Microsoft.Office.Interop.Excel.Sheets> coleção Microsoft Office Excel nos seguintes casos:

- Você deseja excluir uma planilha em um suplemento do VSTO.

- A planilha que você deseja excluir foi criada em tempo de execução em uma personalização no nível do documento.

  O código a seguir exclui uma planilha de uma pasta de trabalho fazendo referência à planilha por meio do número de índice da coleção de **planilhas** . Esse código pressupõe que uma nova planilha foi criada programaticamente.

> [!IMPORTANT]
> Se você quiser executar essa tarefa em qualquer outro tipo de projeto, deverá adicionar uma referência ao assembly **Microsoft. Office. Interop. Excel** e, em seguida, deverá usar classes desse assembly para abrir uma pasta de trabalho e excluir uma planilha. Para obter mais informações, consulte [como: direcionar aplicativos do Office por meio de assemblies de interoperabilidade primária](how-to-target-office-applications-through-primary-interop-assemblies.md) e [referência de assembly de interoperabilidade primária do Excel 2010](office-primary-interop-assemblies.md)

### <a name="to-delete-a-worksheet-by-using-the-sheets-collection-of-the-excel-workbook"></a>Para excluir uma planilha usando a coleção Sheets da pasta de trabalho do Excel

1. Chame o <xref:Microsoft.Office.Interop.Excel._Worksheet.Delete%2A> método da <xref:Microsoft.Office.Interop.Excel.Sheets> coleção.

     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreExcelAutomationCS/Sheet1.cs" id="Snippet18":::
     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreExcelAutomation/Sheet1.vb" id="Snippet18":::

## <a name="see-also"></a>Consulte também
- [Trabalhar com planilhas](working-with-worksheets.md)
- [Como: ocultar planilhas programaticamente](how-to-programmatically-hide-worksheets.md)
- [Como: mover planilhas programaticamente dentro de pastas de trabalho](how-to-programmatically-move-worksheets-within-workbooks.md)
- [Como: selecionar planilhas programaticamente](how-to-programmatically-select-worksheets.md)
- [Como: adicionar programaticamente novas planilhas a pastas de trabalho](how-to-programmatically-add-new-worksheets-to-workbooks.md)
- [Item de host de planilha](worksheet-host-item.md)
- [Acesso global a objetos em projetos do Office](global-access-to-objects-in-office-projects.md)
- [Limitações programáticas de itens de host e controles de host](programmatic-limitations-of-host-items-and-host-controls.md)
