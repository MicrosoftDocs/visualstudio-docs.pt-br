---
title: Acesso global a objetos em projetos do Office
description: Saiba como você pode usar a classe Globals para acessar vários itens de projeto diferentes em tempo de execução de qualquer código no projeto.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- ThisDocument_Shutdown
- ThisDocument_Startup
- Globals class, object global access
- worksheets [Office development in Visual Studio], global access
- documents [Office development in Visual Studio], global access
- event handlers [Office development in Visual Studio]
- ThisWorkbook_Startup
- application-level addins [Office development in Visual Studio]
- addins [Office development in Visual Studio], events
- workbooks [Office development in Visual Studio], global access
- ThisWorkbook_Shutdown
- document-level customizations [Office development in Visual Studio]
- Startup event
- Shutdown event
- projects [Office development in Visual Studio], global access
- Office documents [Office development in Visual Studio, global access
- ThisAddin_Startup
- events [Office development in Visual Studio]
- ThisAddIn_Shutdown
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b939131f388642b452445e0afee0f5e38d2a5195
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825531"
---
# <a name="global-access-to-objects-in-office-projects"></a>Acesso global a objetos em projetos do Office
  Quando você cria um projeto do Office, o Visual Studio gera automaticamente uma classe chamada `Globals` no projeto. Você pode usar a `Globals` classe para acessar vários itens de projeto diferentes em tempo de execução de qualquer código no projeto.

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="how-to-use-the-globals-class"></a>Como usar a classe Globals
 `Globals` é uma classe estática que mantém referências a determinados itens em seu projeto. Usando a `Globals` classe, você pode acessar os seguintes itens de qualquer código no projeto em tempo de execução:

- As `ThisWorkbook` classes e `Sheet` *n* em uma pasta de trabalho ou projeto de modelo do Excel. Você pode acessar esses objetos usando as `Globals.ThisWorkbook` Propriedades e `Sheet` *n* .

- A `ThisDocument` classe em um documento do Word ou projeto de modelo. Você pode acessar esse objeto usando a `Globals.ThisDocument` propriedade.

- A `ThisAddIn` classe em um projeto de suplemento do VSTO. Você pode acessar esse objeto usando a `Globals.ThisAddIn` propriedade.

- Todas as faixas de projeto que você personalizou usando o designer de faixa de faixas. Você pode acessar as faixas de faixa usando a `Globals.Ribbons` propriedade. Para obter mais informações, consulte [acessar a faixa de visualização em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md).

- Todas as regiões de formulário do Outlook em um projeto de suplemento do VSTO do Outlook. Você pode acessar as regiões de formulário usando a `Globals.FormRegions` propriedade. Para obter mais informações, consulte [acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md).

- Um objeto de fábrica que permite que você crie controles de faixa de faixas e itens de host em tempo de execução em projetos direcionados ao [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] ou ao [!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] . Você pode acessar esse objeto usando a `Globals.Factory` propriedade. Esse objeto é uma instância de uma classe que implementa uma das seguintes interfaces:

  - [Microsoft. Office. Tools. Factory](xref:Microsoft.Office.Tools.Factory)

  - [Microsoft. Office. Tools. Excel. Factory](xref:Microsoft.Office.Tools.Excel.Factory)

  - [Microsoft. Office. Tools. Outlook. Factory](xref:Microsoft.Office.Tools.Outlook.Factory)

  - [Microsoft. Office. Tools. Word. Factory](xref:Microsoft.Office.Tools.Word.Factory)

  Por exemplo, você pode usar a `Globals.Sheet1` propriedade para inserir texto em um <xref:Microsoft.Office.Tools.Excel.NamedRange> controle em `Sheet1` quando um usuário clica em um botão no painel Ações em um projeto de nível de documento para o Excel.

  :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreProgrammingExcelVB/Sheet1.vb" id="Snippet1":::
  :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreProgrammingExcelCS/Sheet1.cs" id="Snippet1":::

 O código que tenta usar a `Globals` classe antes que o documento ou suplemento do VSTO seja inicializado pode gerar uma exceção de tempo de execução. Por exemplo, usar `Globals` quando declarar uma variável em nível de classe pode falhar porque a `Globals` classe pode não ser inicializada com referências a todos os itens de host antes que o objeto declarado seja instanciado.

> [!NOTE]
> A `Globals` classe nunca é inicializada em tempo de design, mas as instâncias de controle são criadas pelo designer. Isso significa que, se você criar um controle de usuário que usa uma propriedade da `Globals` classe de dentro de uma classe de controle de usuário, deverá verificar se a propriedade retorna **NULL** antes de tentar usar o objeto retornado.

## <a name="see-also"></a>Consulte também
- [Acessar a faixa de faixas em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)
- [Acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)
- [Visão geral de itens de host e controles de host](../vsto/host-items-and-host-controls-overview.md)
- [Item de host do documento](../vsto/document-host-item.md)
- [Item de host da pasta de trabalho](../vsto/workbook-host-item.md)
- [Item de host de planilha](../vsto/worksheet-host-item.md)
- [Escrever código em soluções do Office](../vsto/writing-code-in-office-solutions.md)
