---
title: Dados de documento e o documento de exibição em editores personalizados | Microsoft Docs
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
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
caps.latest.revision: 24
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 55f082711de306e9dd22fdf55e769282ad150f17
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51755296"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>Dados de documento e exibição de documentos em editores personalizados
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Um editor personalizado consiste em duas partes: um objeto de dados de documento e um objeto de exibição de documento. Como os nomes sugerem, o objeto de dados de documento representa os dados de texto a ser exibido, e o objeto de exibição de documento (ou "view") representa uma ou mais janelas no qual exibir o objeto de dados do documento.  
  
## <a name="document-data-object"></a>Objeto de dados de documento  
 Um objeto de dados de documento é uma representação de dados de texto no buffer de texto. É um objeto COM que armazena o texto do documento e outras informações, lida com persistência de documento e habilita a vários modos de exibição de seus dados. Para saber mais, veja  
  
 <xref:EnvDTE80.Window2.DocumentData%2A> e [documentar Windows](../extensibility/internals/document-windows.md).  
  
 Designers e editores personalizados podem optar por usar o <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> sua próprias buffer personalizado ou objeto. <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> segue o modelo de incorporação simplificado para um editor padrão, dá suporte a vários modos de exibição e fornece interfaces de evento que são usados para gerenciar vários modos de exibição.  
  
## <a name="document-view-object"></a>Objeto de exibição de documento  
 Uma janela que exibe o código e outros textos é conhecida como um documento de exibição ou exibição. Quando você cria um editor, você pode escolher uma única exibição, no qual o texto é exibido em uma única janela, ou uma exibição de várias, no qual o texto é exibido em mais de uma janela. Sua escolha depende de seu aplicativo. Por exemplo, se você precisar de uma edição lado a lado, você escolheria vários do modo de exibição. Cada modo de exibição está associado uma entrada no ambiente de desenvolvimento integrado do (IDE) a tabela de documento (RDT) em execução. As janelas de exibição pertencem a um projeto ou um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> objeto.  
  
 Se seu editor dá suporte a vários modos de exibição de um objeto de dados de documento, em seguida, seus dados de documentos e objetos de exibição de documento devem ser separados. Caso contrário, eles podem ser agrupados. Para obter mais informações, consulte [que dão suporte a várias exibições de documento](../extensibility/supporting-multiple-document-views.md).  
  
 O IDE notifica exibições sobre eventos (por exemplo, quando uma solução que contém um documento é fechada), correspondendo a um identificador de item (ItemID) para cada entrada na tabela de documento em execução. Para obter mais informações sobre isso, consulte [tabela de documento em execução](../extensibility/internals/running-document-table.md).  
  
 Há duas opções para criar um modo de exibição para um editor personalizado. Um é o modelo de ativação in-loco, em que o modo de exibição está hospedado em uma janela usando um controle ActiveX ou um objeto de dados do documento. O segundo é o modelo de incorporação simplificado, em que o modo de exibição é hospedado pelo [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] e <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> é implementada para lidar com comandos de janela. Para obter informações sobre o modelo de ativação no local, consulte [ativação in-loco](../misc/in-place-activation.md). Para obter informações sobre o modelo de incorporação simplificada, consulte [incorporação simplificada](../extensibility/simplified-embedding.md).  
  
## <a name="see-also"></a>Consulte também  
 [Suporte a vários modos de exibição de documento](../extensibility/supporting-multiple-document-views.md)   
 [Incorporação simplificada](../extensibility/simplified-embedding.md)   
 [Como: anexar exibições para dados de documentos](../extensibility/how-to-attach-views-to-document-data.md)   
 [Gerenciamento de titular de bloqueio de documento](../extensibility/document-lock-holder-management.md)   
 [Modos de exibição únicos e com várias guias](../extensibility/single-and-multi-tab-views.md)   
 [Salvar um documento padrão](../extensibility/internals/saving-a-standard-document.md)   
 [A tabela de documento em execução e persistência](../extensibility/internals/persistence-and-the-running-document-table.md)   
 [Determinar qual Editor abre um arquivo em um projeto](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)   
 [Fábricas de editor](../extensibility/editor-factories.md)

