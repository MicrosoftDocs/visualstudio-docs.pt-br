---
title: Documentar Windows | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Visual Studio SDK, document windows
ms.assetid: 50081d48-987f-43db-8bf9-51b7cf76e9c0
caps.latest.revision: 18
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: d669485eb13c8d9f089a54dcbfcf92fac710f474
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51784579"
---
# <a name="document-windows"></a>Janelas de documento
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

No Visual Studio, uma *janela de documento* é uma janela com moldura filho que está associada uma janela de interface de documentos múltiplos (MDI). Janelas de documento normalmente são usadas para a exibição e modificação do código-fonte ou texto, mas eles também podem hospedar outros tipos de funcionais. Janelas de documento:  
  
- Podem ser organizados em grupos de guia horizontal ou vertical separada no pai MDI, para que vários arquivos podem ser exibidos ao mesmo tempo.  
  
- Podem ser encaixadas em qualquer ordem no pai MDI.  
  
- Pode ser flutuante livremente.  
  
- São vinculados na ordem de tabulação para outras janelas MDI.  
  
  Os comandos para agrupamento, Encaixando e flutuando podem ser encontrados no menu de atalho para uma guia da janela de documento.  
  
  Para obter mais informações sobre o comportamento de janela no Visual Studio, consulte [personalizando layouts de janela](../../ide/customizing-window-layouts-in-visual-studio.md).  
  
## <a name="document-window-implementation"></a>Implementação de janela de documento  
 Janelas de documento são criadas com a implementação de um editor. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> interface cria janelas de documentos como parte de criar uma instância de um editor. Para obter mais informações, consulte [Interfaces herdadas no Editor de](../../extensibility/legacy-interfaces-in-the-editor.md).  
  
> [!NOTE]
>  Para fornecer para trás e encaminhar os pontos em uma janela de navegação, implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsBackForwardNavigation> interface. O editor de texto usa marcadores de texto para identificar os pontos de navegação no documento.  
  
## <a name="the-running-document-table"></a>A tabela de documento em execução  
 O IDE usa a tabela de documento (RDT) em execução para acompanhar o status de cada janela de documento. O RDT é o mecanismo pelo qual documento windows são notificados sobre eventos, como quando uma solução é fechada ou quando um arquivo foi editado. Para obter mais informações, consulte [tabela de documento em execução](../../extensibility/internals/running-document-table.md).  
  
## <a name="see-also"></a>Consulte também  
 [Atraso no carregamento do documento](../../extensibility/internals/delayed-document-loading.md)

