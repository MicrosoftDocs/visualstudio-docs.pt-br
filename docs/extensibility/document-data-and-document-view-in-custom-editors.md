---
title: Dados de documento e exibição de documento em editores personalizados | Microsoft Docs
description: Saiba mais sobre os componentes de um editor personalizado, que são o objeto de dados de documento e o objeto de exibição de documento.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], custom - document data and document view
ms.assetid: 71eea623-f566-4feb-84cd-ca1ba71bc493
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 391bec513f1f6d32d7ff2f87d70abdbf491ab8be
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105091234"
---
# <a name="document-data-and-document-view-in-custom-editors"></a>Dados de documento e exibição de documento em editores personalizados
Um editor personalizado consiste em duas partes: um objeto de dados de documento e um objeto de exibição de documento. Como os nomes sugerem, o objeto de dados do documento representa os dados de texto a serem exibidos. Da mesma forma, o objeto de exibição de documento (ou "exibição") representa uma ou mais janelas nas quais exibir o objeto de dados do documento.

## <a name="document-data-object"></a>Objeto de dados do documento
 Um objeto de dados de documento é uma representação de dados de texto no buffer de texto. É um objeto COM que armazena o texto do documento e outras informações. O objeto de dados de documento também manipula a persistência de documentos e permite várias exibições de seus dados. Para obter mais informações, consulte

 <xref:EnvDTE80.Window2.DocumentData%2A> e [janelas de documentos](../extensibility/internals/document-windows.md).

 Editores e designers personalizados podem optar por usar o <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> objeto ou seu próprio buffer personalizado. <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextBuffer> segue o modelo de incorporação simplificado para um editor padrão, dá suporte a várias exibições e fornece interfaces de eventos que são usadas para gerenciar várias exibições.

## <a name="document-view-object"></a>Objeto de exibição de documento
 Uma janela que exibe código e outro texto é conhecida como exibição de documento ou exibição. Ao criar um editor, você pode escolher uma única exibição, na qual o texto é exibido em uma única janela. Ou você pode escolher uma exibição múltipla, na qual o texto é exibido em mais de uma janela. Sua escolha depende do seu aplicativo. Por exemplo, se você precisar de edição lado a lado, escolha vários modos de exibição. Cada exibição é associada a uma entrada no IDE (ambiente de desenvolvimento integrado) que executa a tabela de documentos (RDT). As janelas de exibição pertencem a um projeto ou a um <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> objeto.

 Se o seu editor oferecer suporte a várias exibições de um objeto de dados de documento, os dados do documento e os objetos de exibição de documento deverão ser separados. Caso contrário, eles podem ser agrupados juntos. Para obter mais informações, consulte [suporte para vários modos de exibição de documento](../extensibility/supporting-multiple-document-views.md).

 O IDE notifica exibições sobre eventos (por exemplo, quando uma solução que contém um documento é fechada) combinando um ID de item (ItemID) para cada entrada na tabela de documentos em execução. Para obter mais informações sobre isso, consulte [executando a tabela de documentos](../extensibility/internals/running-document-table.md).

 Há duas opções para criar uma exibição para um editor personalizado. Um é o modelo de ativação in-loco, em que a exibição é hospedada em uma janela usando um controle ActiveX ou um objeto de dados de documento. O segundo é o modelo de incorporação simplificado, em que a exibição é hospedada pelo [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] e <xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane> é implementada para manipular comandos de janela. Para obter informações sobre o modelo de ativação in-loco, consulte [ativação in-loco](/previous-versions/visualstudio/visual-studio-2015/misc/in-place-activation?preserve-view=true&view=vs-2015). Para obter informações sobre o modelo de incorporação simplificada, consulte [incorporação simplificada](../extensibility/simplified-embedding.md).

## <a name="see-also"></a>Confira também

- [Suporte a exibições de vários documentos](../extensibility/supporting-multiple-document-views.md)
- [Incorporação simplificada](../extensibility/simplified-embedding.md)
- [Como anexar exibições aos dados do documento](../extensibility/how-to-attach-views-to-document-data.md)
- [Gerenciamento de titular de bloqueio de documento](../extensibility/document-lock-holder-management.md)
- [Exibições únicas e de várias guias](../extensibility/single-and-multi-tab-views.md)
- [Salvar um documento padrão](../extensibility/internals/saving-a-standard-document.md)
- [Persistência e a tabela de documentos em execução](../extensibility/internals/persistence-and-the-running-document-table.md)
- [Determinar qual editor abre um arquivo em um projeto](../extensibility/internals/determining-which-editor-opens-a-file-in-a-project.md)