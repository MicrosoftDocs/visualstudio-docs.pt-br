---
title: Dados de documento e o documento de exibição em editores personalizados | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 2076f1a6c96aea717470fa1e955e5b9786f7fcc5
ms.sourcegitcommit: 06db1892fff22572f0b0a11994dc547c2b7e2a48
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39639809"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>Dados de documentos e exibição de documentos em editores personalizados
Um editor personalizado consiste em duas partes: um objeto de dados de documento e um objeto de exibição de documento. Como os nomes sugerem, o objeto de dados de documento representa os dados de texto a ser exibido. Da mesma forma, o objeto de exibição de documento (ou "view") representa uma ou mais janelas no qual exibir o objeto de dados do documento.  
  
## <a name="document-data-object"></a>Objeto de dados de documento  
 Um objeto de dados de documento é uma representação de dados de texto no buffer de texto. É um objeto COM que armazena o texto do documento e outras informações. O objeto de dados de documento também lida com persistência de documento e habilita vários modos de exibição de seus dados. Para saber mais, veja  
  
 <xref:EnvDTE80.Window2.DocumentData%2A> e [documentar Windows](../extensibility/internals/document-windows.md).  
  
 Designers e editores personalizados podem optar por usar o <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> sua próprias buffer personalizado ou objeto. <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> segue o modelo de incorporação simplificado para um editor padrão, dá suporte a vários modos de exibição e fornece interfaces de evento que são usados para gerenciar vários modos de exibição.  
  
## <a name="document-view-object"></a>Objeto de exibição de documento  
 Uma janela que exibe o código e outros textos é conhecida como um documento de exibição ou exibição. Quando você cria um editor, você pode escolher qualquer uma única exibição, no qual o texto é exibido em uma única janela. Ou você pode escolher um modo de exibição vários, no qual o texto é exibido em mais de uma janela. Sua escolha depende de seu aplicativo. Por exemplo, se você precisar de uma edição lado a lado, você escolheria vários do modo de exibição. Cada modo de exibição está associado uma entrada no ambiente de desenvolvimento integrado do (IDE) a tabela de documento (RDT) em execução. As janelas de exibição pertencem a um projeto ou um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> objeto.  
  
 Se seu editor dá suporte a vários modos de exibição de um objeto de dados de documento, em seguida, seus dados de documentos e objetos de exibição de documento devem ser separados. Caso contrário, eles podem ser agrupados. Para obter mais informações, consulte [dar suporte a vários modos de exibição de documento](../extensibility/supporting-multiple-document-views.md).  
  
 O IDE notifica exibições sobre eventos (por exemplo, quando uma solução que contém um documento é fechada), correspondendo a um identificador de item (ItemID) para cada entrada na tabela de documento em execução. Para obter mais informações sobre isso, consulte [tabela de documento em execução](../extensibility/internals/running-document-table.md).  
  
 Há duas opções para criar um modo de exibição para um editor personalizado. Um é o modelo de ativação in-loco, em que o modo de exibição está hospedado em uma janela usando um controle ActiveX ou um objeto de dados do documento. O segundo é o modelo de incorporação simplificado, em que o modo de exibição é hospedado pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> é implementada para lidar com comandos de janela. Para obter informações sobre o modelo de ativação no local, consulte [ativação in-loco](../extensibility/in-place-activation.md). Para obter informações sobre o modelo de incorporação simplificada, consulte [incorporação simplificada](../extensibility/simplified-embedding.md).  
  
## <a name="see-also"></a>Consulte também  
 [Suporte a vários modos de exibição de documento](../extensibility/supporting-multiple-document-views.md)   
 [Incorporação simplificada](../extensibility/simplified-embedding.md)   
 [Como: anexar exibições para dados de documento](../extensibility/how-to-attach-views-to-document-data.md)   
 [Gerenciamento de titular de bloqueio de documento](../extensibility/document-lock-holder-management.md)   
 [Modos de exibição únicos e com várias guias](../extensibility/single-and-multi-tab-views.md)   
 [Salvar um documento padrão](../extensibility/internals/saving-a-standard-document.md)   
 [Tabela de documento em execução e persistência](../extensibility/internals/persistence-and-the-running-document-table.md)   
 [Determinar qual editor abre um arquivo em um projeto](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)   
 [Fábricas de editor](../extensibility/editor-factories.md)