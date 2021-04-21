---
title: 'Como: adicionar linhas e colunas programaticamente a tabelas do Word'
description: Saiba como você pode usar o método Add do objeto Rows para adicionar linhas à tabela. Você também pode usar o método Add do objeto Columns para adicionar colunas.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- rows [Office development in Visual Studio], adding to Word tables
- tables [Office development in Visual Studio], adding rows and columns
- columns [Office development in Visual Studio], adding to Word tables
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7cac3e11f73e53441f1bcf20c67dd5659a49a1b0
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828417"
---
# <a name="how-to-programmatically-add-rows-and-columns-to-word-tables"></a>Como: adicionar linhas e colunas programaticamente a tabelas do Word
  Em uma Microsoft Office tabela do Word, as células são organizadas em linhas e colunas. Você pode usar o <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> método do <xref:Microsoft.Office.Interop.Word.Rows> objeto para adicionar linhas à tabela e o <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> método do <xref:Microsoft.Office.Interop.Word.Columns> objeto para adicionar colunas.

 [!INCLUDE[appliesto_wdalldocapp](includes/appliesto-wdalldocapp-md.md)]

## <a name="document-level-customization-examples"></a>Exemplos de personalização no nível do documento
 Os exemplos de código a seguir podem ser usados em uma personalização em nível de documento. Para usar esses exemplos, execute-os da `ThisDocument` classe em seu projeto. Esses exemplos pressupõem que o documento associado à sua personalização já tenha pelo menos uma tabela.

> [!IMPORTANT]
> Esse código é executado somente em projetos que você cria usando qualquer um dos seguintes modelos de projeto:
>
> - Documento do Word 2013
> - Modelo do Word 2013
> - Documento do Word 2010
> - Modelo do Word 2010
>
>   Se você quiser executar essa tarefa em qualquer outro tipo de projeto, deverá adicionar uma referência ao assembly **Microsoft. Office. Interop. Word** e, em seguida, deverá usar classes desse assembly para adicionar linhas e colunas a tabelas. Para obter mais informações, consulte [como: direcionar aplicativos do Office por meio de assemblies de interoperabilidade primária](how-to-target-office-applications-through-primary-interop-assemblies.md) e [referência de assembly de interoperabilidade primária do Word 2010](office-primary-interop-assemblies.md)

### <a name="to-add-a-row-to-a-table"></a>Para adicionar uma linha a uma tabela

1. Use o <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> método para adicionar uma linha à tabela.

     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet95":::
     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet95":::

### <a name="to-add-a-column-to-a-table"></a>Para adicionar uma coluna a uma tabela

1. Use o <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> método e, em seguida, use o <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A> método para fazer com que todas as colunas tenham a mesma largura.

     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet96":::
     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet96":::

## <a name="vsto-add-in-examples"></a>Exemplos de suplemento do VSTO
 Os exemplos de código a seguir podem ser usados em um suplemento do VSTO. Para usar os exemplos, execute-os a partir da `ThisAddIn` classe em seu projeto. Esses exemplos pressupõem que o documento ativo já tenha pelo menos uma tabela.

> [!IMPORTANT]
> Esse código é executado somente em projetos que você cria usando modelos de suplemento do VSTO do Word.
>
> Se você quiser executar essa tarefa em qualquer outro tipo de projeto, deverá adicionar uma referência ao assembly **Microsoft. Office. Interop. Word** e, em seguida, deverá usar classes desse assembly para adicionar linhas e colunas a tabelas. Para obter mais informações, consulte [como: direcionar aplicativos do Office por meio de assemblies de interoperabilidade primária](how-to-target-office-applications-through-primary-interop-assemblies.md) e [referência de assembly de interoperabilidade primária do Word 2010](office-primary-interop-assemblies.md)

### <a name="to-add-a-row-to-a-table"></a>Para adicionar uma linha a uma tabela

1. Use o <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> método para adicionar uma linha à tabela.

     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet95":::
     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet95":::

### <a name="to-add-a-column-to-a-table"></a>Para adicionar uma coluna a uma tabela

1. Use o <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> método e, em seguida, use o <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A> método para fazer com que todas as colunas tenham a mesma largura.

     :::code language="vb" source="codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb" id="Snippet96":::
     :::code language="csharp" source="codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs" id="Snippet96":::

## <a name="see-also"></a>Consulte também
- [Como: criar tabelas do Word programaticamente](how-to-programmatically-create-word-tables.md)
- [Como: adicionar texto e formatação programaticamente a células em tabelas do Word](how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)
- [Como: preencher programaticamente tabelas do Word com propriedades do documento](how-to-programmatically-populate-word-tables-with-document-properties.md)
