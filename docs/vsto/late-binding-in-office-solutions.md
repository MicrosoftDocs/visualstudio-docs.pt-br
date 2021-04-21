---
title: Associação tardia em soluções do Office
description: Saiba como alguns tipos em modelos de objeto dentro de Microsoft Office aplicativos fornecem funcionalidade disponível por meio de recursos de ligação tardia.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- objects [Office development in Visual Studio], casting
- types [Office development in Visual Studio], casting
- automation [Office development in Visual Studio], casting objects
- casting, object to specific type
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: e618dcd0cc699b4626f825890cf0fc8bd7ddd853
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107823880"
---
# <a name="late-binding-in-office-solutions"></a>Associação tardia em soluções do Office
  Alguns tipos nos modelos de objeto dos aplicativos do Office fornecem funcionalidade que está disponível por meio de recursos de ligação tardia. Por exemplo, alguns métodos e propriedades podem retornar tipos diferentes de objetos, dependendo do contexto do aplicativo do Office, e alguns tipos podem expor diferentes métodos ou propriedades em diferentes contextos.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 Visual Basic projetos em que **Option Strict** é off e projetos Visual C# que visam o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] podem trabalhar diretamente com tipos que empregam esses recursos de ligação tardia.

## <a name="implicit-and-explicit-casting-of-object-return-values"></a>Conversão implícita e explícita de valores de retorno de objeto
 Muitos métodos e propriedades na Microsoft Office valores de retorno dos PIAs (assemblies de interoperabilidade primária) <xref:System.Object> , pois podem retornar vários tipos diferentes de objetos. Por exemplo, a <xref:Microsoft.Office.Tools.Excel.Workbook.ActiveSheet%2A> propriedade retorna um <xref:System.Object> porque seu valor de retorno pode ser <xref:Microsoft.Office.Interop.Excel.Worksheet> um <xref:Microsoft.Office.Interop.Excel.Chart> objeto ou, dependendo da planilha ativa.

 Quando um método ou uma propriedade retorna um <xref:System.Object> , você deve converter explicitamente (em Visual Basic) o objeto para o tipo correto em projetos Visual Basic em que **Option Strict** está on. Você não precisa converter explicitamente <xref:System.Object> valores de retorno em projetos Visual Basic em que **Option Strict** é off.

 Na maioria dos casos, a documentação de referência lista os possíveis tipos de valor de retorno para um membro que retorna um <xref:System.Object> . A conversão ou conversão do objeto habilita o IntelliSense para o objeto no editor de códigos.

 Para obter informações sobre conversão em Visual Basic, confira [conversões implícitas e explícitas &#40;Visual Basic&#41;](/dotnet/visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions) e a [função CType &#40;](/dotnet/visual-basic/language-reference/functions/ctype-function)Visual Basic&#41;.

### <a name="examples"></a>Exemplos
 O exemplo de código a seguir demonstra como converter um objeto em um tipo específico em um projeto de Visual Basic em que **Option Strict** está on. Nesse tipo de projeto, você deve converter explicitamente a <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A> propriedade em um <xref:Microsoft.Office.Interop.Excel.Range> . Este exemplo requer um projeto do Excel de nível de documento com uma classe de planilha chamada `Sheet1` .

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb" id="Snippet9":::

 O exemplo de código a seguir demonstra como converter implicitamente um objeto em um tipo específico em um projeto Visual Basic em que **Option Strict** está off ou em um projeto do Visual C# que tem como alvo o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] . Nesses tipos de projetos, a <xref:Microsoft.Office.Tools.Excel.WorksheetBase.Cells%2A> propriedade é implicitamente convertida para um <xref:Microsoft.Office.Interop.Excel.Range> . Este exemplo requer um projeto do Excel de nível de documento com uma classe de planilha chamada `Sheet1` .

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb" id="Snippet10":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/Sheet1.cs" id="Snippet10":::

## <a name="access-members-that-are-available-only-through-late-binding"></a>Acessar membros que estão disponíveis somente por meio da associação tardia
 Algumas propriedades e métodos nos PIAs do Office estão disponíveis somente por meio da associação tardia. Em projetos de Visual Basic em que **Option Strict** é off ou em projetos do Visual C# que visam o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou o [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] , você pode usar os recursos de associação tardia nesses idiomas para acessar os membros de ligação tardia. Em projetos de Visual Basic em que **Option Strict** está on, você deve usar Reflection para acessar esses membros.

### <a name="examples"></a>Exemplos
 O exemplo de código a seguir demonstra como acessar membros de associação tardia em um projeto Visual Basic em que **Option Strict** está off ou em um projeto do Visual C# que tem como alvo o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] . Este exemplo acessa a propriedade **nome** de associação tardia da caixa de diálogo **Abrir arquivo** no Word. Para usar este exemplo, execute-o da `ThisDocument` `ThisAddIn` classe ou em um projeto do Word.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet122":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet122":::

 O exemplo de código a seguir demonstra como usar a reflexão para realizar a mesma tarefa em um projeto de Visual Basic em que **Option Strict** está on.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet102":::

## <a name="see-also"></a>Consulte também
- [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)
- [Parâmetros opcionais em soluções do Office](../vsto/optional-parameters-in-office-solutions.md)
- [Use o guia de programação do tipo &#40;C&#35; dinâmico&#41;](/dotnet/csharp/programming-guide/types/using-type-dynamic)
- [Instrução Option Strict](/dotnet/visual-basic/language-reference/statements/option-strict-statement)
- [Reflexão (C#)](/dotnet/csharp/programming-guide/concepts/reflection)
- [Reflexão (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/reflection)
- [Projetar e criar soluções do Office](../vsto/designing-and-creating-office-solutions.md)
