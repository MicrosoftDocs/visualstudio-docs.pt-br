---
title: Automatizar o Word usando objetos estendidos
ms.custom: ''
ms.date: 02/02/2017
ms.technology: office-development
ms.prod: visual-studio-dev15
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Word [Office development in Visual Studio], automating
- extended objects [Office development in Visual Studio], Word
- automation [Office development in Visual Studio], Word
- host items [Office development in Visual Studio], Word
- automating Word
- controls [Office development in Visual Studio], Word host controls
- host controls, Word
- host controls [Office development in Visual Studio], Word
- Word [Office development in Visual Studio], host controls
author: John-Hart
ms.author: johnhart
manager: douge
ms.workload:
- office
ms.openlocfilehash: 85d3adc2ff156f6967d7590788c749d0343c7c0f
ms.sourcegitcommit: 20c0991d737c540750c613c380cd4cf5bb07de51
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248139"
---
# <a name="automate-word-by-using-extended-objects"></a>Automatizar o Word usando objetos estendidos
  Ao desenvolver soluções do Word no Visual Studio, você pode usar *hospedar itens* e *controle de host*s em suas soluções. Esses são objetos que estendem alguns objetos comumente usados no modelo de objeto do Word (ou seja, o modelo de objeto que é exposto pelo assembly de interoperabilidade primário para o Word), como o <xref:Microsoft.Office.Interop.Word.Document> e <xref:Microsoft.Office.Interop.Word.ContentControl> objetos. Objetos estendidos se comportam como os objetos do Word se baseiam, mas adicionar eventos adicionais e recursos de ligação de dados para os objetos.  
  
 [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]  
  
 Itens de host e controles de host estão disponíveis no VSTO Add-ins e personalizações no nível do documento, embora o contexto no qual eles podem ser usados é diferente para cada tipo de solução. Para obter mais informações, consulte [hospedam itens e visão geral dos controles](../vsto/host-items-and-host-controls-overview.md).  
  
## <a name="document-host-item"></a>Item de host do documento  
 Word fornecem projetos acesso a <xref:Microsoft.Office.Tools.Word.Document> item de host. O <xref:Microsoft.Office.Tools.Word.Document> item de host atua como um contêiner para outros controles, incluindo controles de host e controles dos Windows Forms, e mantém informações sobre os controles em sua superfície. O <xref:Microsoft.Office.Tools.Word.Document> item de host também fornece a maioria dos mesmos membros que o <xref:Microsoft.Office.Interop.Word.Document> classe, que é a classe correspondente no modelo de objeto do Word.  
  
 Para obter mais informações, consulte [item de host do documento](../vsto/document-host-item.md).  
  
## <a name="word-host-controls"></a>controles de host do Word  
 Há vários controles de host para o Word que ajudam você a criar, organizar e automatizar a documentos. A maioria de sua funcionalidade envolve a importação, apresentando e proteção de dados. Os controles de host fornecem eventos e os recursos de vinculação de dados que não têm equivalentes no modelo de objeto nativo do Word.  
  
 Em projetos de nível de documento, você pode adicionar qualquer controle de host para o documento em tempo de design, ou você pode adicionar controles de conteúdo e controles de indicador em tempo de execução. Em projetos de suplemento do VSTO, você pode adicionar controles de conteúdo e controles de indicador para qualquer documento aberto no tempo de execução.  
  
 Para obter mais informações sobre os controles de host que você pode usar em projetos do Word, consulte os tópicos a seguir:  
  
-   [Controles de conteúdo](../vsto/content-controls.md)  
  
-   [Controle de indicador](../vsto/bookmark-control.md)  
  
-   [Controle XMLNode](../vsto/xmlnode-control.md)  
  
-   [Controle XMLNodes](../vsto/xmlnodes-control.md)  
  
## <a name="see-also"></a>Consulte também  
 [Como: Adicionar controles content a documentos do Word](../vsto/how-to-add-content-controls-to-word-documents.md)   
 [Como: Adicionar controles de indicador a documentos do Word](../vsto/how-to-add-bookmark-controls-to-word-documents.md)   
 [Como: Adicionar controles XMLNode a documentos do Word](../vsto/how-to-add-xmlnode-controls-to-word-documents.md)   
 [Como: Adicionar controles XMLNodes a documentos do Word](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)   
 [Como: Redimensionar controles de indicador](../vsto/how-to-resize-bookmark-controls.md)   
 [Passo a passo: Criar um modelo usando os controles de conteúdo](../vsto/walkthrough-creating-a-template-by-using-content-controls.md)   
 [Passo a passo: Associar controles de conteúdo a partes XML personalizadas](../vsto/walkthrough-binding-content-controls-to-custom-xml-parts.md)   
 [Passo a passo: Criar menus de atalho para indicadores](../vsto/walkthrough-creating-shortcut-menus-for-bookmarks.md)   
 [Soluções do Word](../vsto/word-solutions.md)   
 [Visão geral dos controles de host e de itens de host](../vsto/host-items-and-host-controls-overview.md)   
 [Limitações programáticas de itens de host e controles de host](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)   
 [Estender documentos do Word e pastas de trabalho do Excel em suplementos do VSTO em tempo de execução](../vsto/extending-word-documents-and-excel-workbooks-in-vsto-add-ins-at-run-time.md)  
  
  