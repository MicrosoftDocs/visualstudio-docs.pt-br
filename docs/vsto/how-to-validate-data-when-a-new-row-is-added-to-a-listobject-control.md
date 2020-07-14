---
title: Validar dados quando uma nova linha for adicionada ao controle ListObject
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- controls [Office development in Visual Studio], validating data
- ListObject control, new row
- ListObject control, validating data
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 2b9ed8428f9dd0325678cb91a847609aed76f9b5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541161"
---
# <a name="how-to-validate-data-when-a-new-row-is-added-to-a-listobject-control"></a>Como validar dados quando uma nova linha é adicionada a um controle ListObject
  Os usuários podem adicionar novas linhas a um <xref:Microsoft.Office.Tools.Excel.ListObject> controle associado aos dados. Você pode validar os dados do usuário antes de confirmar as alterações na fonte de dados.

 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]

## <a name="data-validation"></a>Validação de dados
 Sempre que uma linha é adicionada a uma <xref:Microsoft.Office.Tools.Excel.ListObject> que está associada a dados, o <xref:Microsoft.Office.Tools.Excel.ListObject.BeforeAddDataBoundRow> evento é gerado. Você pode manipular esse evento para executar a validação de dados. Por exemplo, se seu aplicativo exigir que somente funcionários entre as idades de 18 e 65 possam ser adicionados à fonte de dados, verifique se a idade inserida cai dentro desse intervalo antes de a linha ser adicionada.

> [!NOTE]
> Você sempre deve verificar a entrada do usuário no servidor além do cliente. Para obter mais informações, consulte [proteger aplicativos cliente](/dotnet/framework/data/adonet/secure-client-applications).

### <a name="to-validate-data-when-a-new-row-is-added-to-data-bound-listobject"></a>Para validar dados quando uma nova linha é adicionada ao ListObject associado a dados

1. Crie variáveis para a ID e <xref:System.Data.DataTable> no nível de classe.

     [!code-csharp[Trin_VstcoreHostControlsExcel#8](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#8)]
     [!code-vb[Trin_VstcoreHostControlsExcel#8](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#8)]

2. Crie um novo <xref:System.Data.DataTable> e adicione colunas de exemplo e dados no `Startup` manipulador de eventos da `Sheet1` classe (em um projeto de nível de documento) ou `ThisAddIn` classe (em um projeto de suplemento do VSTO).

     [!code-csharp[Trin_VstcoreHostControlsExcel#9](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#9)]
     [!code-vb[Trin_VstcoreHostControlsExcel#9](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#9)]

3. Adicione código ao `list1_BeforeAddDataBoundRow` manipulador de eventos para verificar se a idade inserida cai dentro do intervalo aceitável.

     [!code-csharp[Trin_VstcoreHostControlsExcel#10](../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs#10)]
     [!code-vb[Trin_VstcoreHostControlsExcel#10](../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb#10)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.ListObject> nome existente `list1` na planilha na qual esse código é exibido.

## <a name="see-also"></a>Consulte também
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Controle ListObject](../vsto/listobject-control.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Como mapear colunas ListObject para dados](../vsto/how-to-map-listobject-columns-to-data.md)
