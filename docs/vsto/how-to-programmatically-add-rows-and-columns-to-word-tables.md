---
title: 'Como: adicionar linhas e colunas programaticamente a tabelas do Word'
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0097692c77d0b472c808876e9017b514b6416fc6
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85538067"
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

     [!code-vb[Trin_VstcoreWordAutomation#95](codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#95)]
     [!code-csharp[Trin_VstcoreWordAutomation#95](codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#95)]

### <a name="to-add-a-column-to-a-table"></a>Para adicionar uma coluna a uma tabela

1. Use o <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> método e, em seguida, use o <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A> método para fazer com que todas as colunas tenham a mesma largura.

     [!code-vb[Trin_VstcoreWordAutomation#96](codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb#96)]
     [!code-csharp[Trin_VstcoreWordAutomation#96](codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs#96)]

## <a name="vsto-add-in-examples"></a>Exemplos de suplemento do VSTO
 Os exemplos de código a seguir podem ser usados em um suplemento do VSTO. Para usar os exemplos, execute-os a partir da `ThisAddIn` classe em seu projeto. Esses exemplos pressupõem que o documento ativo já tenha pelo menos uma tabela.

> [!IMPORTANT]
> Esse código é executado somente em projetos que você cria usando modelos de suplemento do VSTO do Word.
>
> Se você quiser executar essa tarefa em qualquer outro tipo de projeto, deverá adicionar uma referência ao assembly **Microsoft. Office. Interop. Word** e, em seguida, deverá usar classes desse assembly para adicionar linhas e colunas a tabelas. Para obter mais informações, consulte [como: direcionar aplicativos do Office por meio de assemblies de interoperabilidade primária](how-to-target-office-applications-through-primary-interop-assemblies.md) e [referência de assembly de interoperabilidade primária do Word 2010](office-primary-interop-assemblies.md)

### <a name="to-add-a-row-to-a-table"></a>Para adicionar uma linha a uma tabela

1. Use o <xref:Microsoft.Office.Interop.Word.Rows.Add%2A> método para adicionar uma linha à tabela.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#95](codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#95)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#95](codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#95)]

### <a name="to-add-a-column-to-a-table"></a>Para adicionar uma coluna a uma tabela

1. Use o <xref:Microsoft.Office.Interop.Word.Columns.Add%2A> método e, em seguida, use o <xref:Microsoft.Office.Interop.Word.Columns.DistributeWidth%2A> método para fazer com que todas as colunas tenham a mesma largura.

     [!code-vb[Trin_VstcoreWordAutomationAddIn#96](codesnippet/VisualBasic/Trin_VstcoreWordAutomationAddIn/ThisAddIn.vb#96)]
     [!code-csharp[Trin_VstcoreWordAutomationAddIn#96](codesnippet/CSharp/Trin_VstcoreWordAutomationAddIn/ThisAddIn.cs#96)]

## <a name="see-also"></a>Consulte também
- [Como: criar tabelas do Word programaticamente](how-to-programmatically-create-word-tables.md)
- [Como: adicionar texto e formatação programaticamente a células em tabelas do Word](how-to-programmatically-add-text-and-formatting-to-cells-in-word-tables.md)
- [Como: preencher programaticamente tabelas do Word com propriedades do documento](how-to-programmatically-populate-word-tables-with-document-properties.md)
