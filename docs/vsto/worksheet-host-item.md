---
title: Item de host da planilha
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- host items [Office development in Visual Studio], Worksheet
- Excel [Office development in Visual Studio], worksheets
- Worksheet host items
- worksheets, events
- Worksheet host items, events
- Excel worksheets
- worksheets, Excel
- worksheets
- events [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 4052e7d9b096d9bae6671834369ece6d31bee4a0
ms.sourcegitcommit: 34f7d23ce3bd140dcae875b602d5719bb4363ed1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35258912"
---
# <a name="worksheet-host-item"></a>Item de host da planilha
  O <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host é um tipo que estende o <xref:Microsoft.Office.Interop.Excel.Worksheet> o tipo do assembly de interoperabilidade primário para o Excel. O <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host fornece todas as mesmas propriedades, métodos e eventos como um <xref:Microsoft.Office.Interop.Excel.Worksheet> objeto, mas ele também expõe eventos adicionais e atua como um contêiner para controles dos Windows Forms e controles de host.  
  
 [!INCLUDE[appliesto_xlalldocapp](../vsto/includes/appliesto-xlalldocapp-md.md)]  
  
 Em projetos de nível de documento, você pode adicionar <xref:Microsoft.Office.Tools.Excel.Worksheet> hospedar itens ao seu projeto em tempo de design. Em projetos de suplemento do VSTO, você pode gerar <xref:Microsoft.Office.Tools.Excel.Worksheet> hospedar itens em tempo de execução.  
  
## <a name="understand-worksheet-host-items-in-document-level-projects"></a>Entender os itens de host de planilha em projetos de nível de documento  
 Quando você cria um projeto de nível de documento para Excel, o Visual Studio cria automaticamente três <xref:Microsoft.Office.Tools.Excel.Worksheet> hospedar itens no projeto. Os nomes padrão das planilhas são `Sheet1`, `Sheet2`, e `Sheet3`. Se você criar um projeto com base em uma pasta de trabalho existente, o número de itens de host depende do número de planilhas na pasta de trabalho.  
  
 Essas classes de planilha dão acesso aos membros a <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host para executar tarefas básicas em sua personalização, como modificar o conteúdo de uma planilha. Você também pode usar essas classes para adicionar controles a planilhas. Combinando conjuntos diferentes de controles e escrevendo código, que você pode associar controles a dados, coletar informações do usuário e responder às ações do usuário. Para obter mais informações, consulte [personalizações no nível de documento do programa](../vsto/programming-document-level-customizations.md).  
  
 As classes de planilha fornecem um local no qual você pode começar a escrever código em seu projeto. Como a classe fornece todas as mesmas propriedades, métodos e eventos como o <xref:Microsoft.Office.Interop.Excel.Worksheet> do objeto no assembly de interoperabilidade primário para o Excel, você também pode usar essas classes para acessar o modelo de objeto do Excel. Para obter mais informações, consulte [visão geral do modelo de objeto do Excel](../vsto/excel-object-model-overview.md).  
  
 Em projetos de nível de documento, você pode adicionar adicionais <xref:Microsoft.Office.Tools.Excel.Worksheet> hospedar itens ao projeto em tempo de design, adicionando uma nova planilha na pasta de trabalho no designer.  
  
### <a name="rename-worksheets"></a>Renomear a planilhas  
 Em um projeto de nível de documento, você pode renomear as planilhas no designer do Visual Studio, mas isso altera apenas o nome de exibição da planilha. O nome programático ainda é o nome padrão da planilha. Se você renomear a planilha na **propriedades** janela, apenas o nome programático é alterada.  
  
### <a name="limitations-of-the-worksheet-host-item-in-document-level-projects"></a>Limitações do item de host de planilha em projetos de nível de documento  
 Você não pode criar novos <xref:Microsoft.Office.Tools.Excel.Worksheet> hospedar itens em tempo de execução em um projeto de nível de documento. Se você criar uma nova planilha do Excel em tempo de execução, ele será do tipo <xref:Microsoft.Office.Interop.Excel.Worksheet>. Porque ele não é um item de host, ele não pode conter quaisquer controles de host ou controles de formulários do Windows. Para obter mais informações sobre a criação de documentos em tempo de execução, consulte [como: adicionar novas planilhas a pastas de trabalho de forma programática](../vsto/how-to-programmatically-add-new-worksheets-to-workbooks.md).  
  
## <a name="understand-worksheet-host-items-in-vsto-add-in-projects"></a>Entender os itens de host de planilha em projetos de suplemento do VSTO  
 Em projetos de nível de aplicativo, você pode gerar um <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host em tempo de execução para qualquer planilha que está aberto no Excel. Você pode usar o <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host para adicionar controles à planilha associada, ou para manipular eventos que não estão disponíveis em <xref:Microsoft.Office.Interop.Excel.Worksheet> objetos.  
  
 Para gerar uma <xref:Microsoft.Office.Tools.Excel.Worksheet> item de host, use o `GetVstoObject` método. Para obter mais informações, consulte [documentos de estender o Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md).  
  
## <a name="see-also"></a>Consulte também  
 [Instruções passo a passo e exemplos de desenvolvimento do office](../vsto/office-development-samples-and-walkthroughs.md)   
 [Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)   
 [Controles em documentos do Office](../vsto/controls-on-office-documents.md)   
 [Adicionar controles a documentos do Office em tempo de execução](../vsto/adding-controls-to-office-documents-at-run-time.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Item de host da pasta de trabalho](../vsto/workbook-host-item.md)   
 [Automatizar o Excel usando objetos estendidos](../vsto/automating-excel-by-using-extended-objects.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)  
  
  