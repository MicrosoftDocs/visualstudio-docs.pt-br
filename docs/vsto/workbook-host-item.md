---
title: Item de host da pasta de trabalho
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Excel workbooks
- Workbook host items
- host items [Office development in Visual Studio], Workbook
- workbooks, Excel
- Workbook host items, events
- workbooks
- Excel [Office development in Visual Studio], workbooks
- workbooks, events
- events [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b477b40425f7ded5fbaacf09aabc446ff207d86c
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35258162"
---
# <a name="workbook-host-item"></a>Item de host da pasta de trabalho
  O <xref:Microsoft.Office.Tools.Excel.Workbook> item de host é um tipo que estende o <xref:Microsoft.Office.Interop.Excel.Workbook> o tipo do assembly de interoperabilidade primário para o Excel. O <xref:Microsoft.Office.Tools.Excel.Workbook> item de host fornece todas as mesmas propriedades, métodos e eventos como um <xref:Microsoft.Office.Interop.Excel.Workbook> objeto, mas ele também fornece recursos adicionais.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 Em projetos de nível de documento, há um padrão <xref:Microsoft.Office.Tools.Excel.Workbook> item de host que representa a pasta de trabalho em seu projeto. Em projetos de suplemento do VSTO, você pode gerar <xref:Microsoft.Office.Tools.Excel.Workbook> hospedar itens em tempo de execução.  
  
## <a name="understand-the-workbook-host-item-in-document-level-projects"></a>Entender o item de host da pasta de trabalho em projetos de nível de documento  
 Para acessar a pasta de trabalho em seu projeto, use o `ThisWorkbook` classe. O `ThisWorkbook` classe fornece acesso a membros do <xref:Microsoft.Office.Tools.Excel.Workbook> item de host para executar tarefas básicas em sua personalização, como a execução de código quando a pasta de trabalho é aberta ou fechada. Para obter mais informações, consulte [personalizações no nível de documento do programa](../vsto/programming-document-level-customizations.md).  
  
 O `ThisWorkbook` classe fornece um local no qual você pode começar a escrever código em seu projeto. Como a classe fornece todas as mesmas propriedades, métodos e eventos como o <xref:Microsoft.Office.Interop.Excel.Workbook> do objeto no assembly de interoperabilidade primário para o Excel, você também pode usar `ThisWorkbook` para acessar o modelo de objeto do Excel. Para obter mais informações, consulte [visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md).  
  
 Clique duas vezes o **ThisWorkbook** item de projeto no **Gerenciador de soluções** para exibir o designer da pasta de trabalho e para exibir as propriedades e eventos da pasta de trabalho no **propriedades**janela.  
  
### <a name="limitations-of-the-workbook-host-item-in-document-level-projects"></a>Limitações do item de host de pasta de trabalho em projetos de nível de documento  
 Um projeto de nível de documento pode conter apenas um <xref:Microsoft.Office.Tools.Excel.Workbook> item de host (ou seja, o `ThisWorkbook` classe). Você não pode adicionar novas <xref:Microsoft.Office.Tools.Excel.Workbook> host de itens ao seu projeto em tempo de design, e você não pode criar novos <xref:Microsoft.Office.Tools.Excel.Workbook> hospedar itens em tempo de execução de uma personalização no nível de documento.  
  
 Se você criar uma nova pasta de trabalho do Excel em tempo de execução, ele será do tipo <xref:Microsoft.Office.Interop.Excel.Workbook>. Porque ele não é um item de host, ele não pode conter quaisquer controles de host ou controles de formulários do Windows. Para obter mais informações sobre como criar pastas de trabalho em tempo de execução, consulte [como: criar programaticamente novas pastas de trabalho](../vsto/how-to-programmatically-create-new-workbooks.md).  
  
 O <xref:Microsoft.Office.Tools.Excel.Workbook> item de host não age como um contêiner para controles de host. Portanto, você não pode adicionar todos os controles visíveis na pasta de trabalho, mas você pode adicionar componentes, como um <xref:System.Data.DataSet>, de modo que os componentes podem ser compartilhados por todas as planilhas. Em um projeto de nível de documento, os componentes disponíveis para a pasta de trabalho podem ser encontrados na **componente** guia, **dados** guia, e **todos os formulários do Windows** guia o  **Caixa de ferramentas**.  
  
> [!NOTE]  
>  As ferramentas de desenvolvimento do Office no Visual Studio não dão suporte a pastas de trabalho compartilhadas.  
  
## <a name="understand-workbook-host-items-in-vsto-add-in-projects"></a>Entender os itens de host da pasta de trabalho em projetos de suplemento do VSTO  
 Em projetos de suplemento do VSTO, você pode gerar um <xref:Microsoft.Office.Tools.Excel.Workbook> item de host em tempo de execução para qualquer pasta de trabalho que está aberto no Excel. Para gerar uma <xref:Microsoft.Office.Tools.Excel.Workbook> item de host, use o `GetVstoObject` método. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo e exemplos de desenvolvimento do office](../vsto/office-development-samples-and-walkthroughs.md)   
 [Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Item de host da planilha](../vsto/worksheet-host-item.md)   
 [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  