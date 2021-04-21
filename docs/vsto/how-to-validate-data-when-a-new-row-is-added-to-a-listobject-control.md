---
title: Validar dados quando uma nova linha for adicionada ao controle ListObject
description: Saiba como você pode usar o Visual Studio para validar dados quando uma nova linha é adicionada a um controle ListObject.
ms.custom: SEO-VS-2020
titleSuffix: ''
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a7002cdc0787850fc7be5a782f3cf3a2101d7593
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825713"
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

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet8":::

2. Crie um novo <xref:System.Data.DataTable> e adicione colunas de exemplo e dados no `Startup` manipulador de eventos da `Sheet1` classe (em um projeto de nível de documento) ou `ThisAddIn` classe (em um projeto de suplemento do VSTO).

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet9":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet9":::

3. Adicione código ao `list1_BeforeAddDataBoundRow` manipulador de eventos para verificar se a idade inserida cai dentro do intervalo aceitável.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreHostControlsExcelCS/Sheet1.cs" id="Snippet10":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreHostControlsExcelVB/Sheet1.vb" id="Snippet10":::

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo de código pressupõe que você tenha um <xref:Microsoft.Office.Tools.Excel.ListObject> nome existente `list1` na planilha na qual esse código é exibido.

## <a name="see-also"></a>Consulte também
- [Estenda documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)
- [Controles em documentos do Office](../vsto/controls-on-office-documents.md)
- [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)
- [Controle ListObject](../vsto/listobject-control.md)
- [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)
- [Como mapear colunas ListObject para dados](../vsto/how-to-map-listobject-columns-to-data.md)
