---
title: Janelas de documentos | Microsoft Docs
description: Saiba mais sobre as janelas de documentos no Visual Studio, incluindo como implementá-las e como a tabela de documentos em execução (RDT) controla seu status.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Visual Studio SDK, document windows
ms.assetid: 50081d48-987f-43db-8bf9-51b7cf76e9c0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: df7a797c0b4587698197412f49eef6bfab183a7a
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899908"
---
# <a name="document-windows"></a>Janelas de documentos
No Visual Studio, uma *janela de documento* é uma janela filho com quadros que está associada a uma janela MDI (interface de vários documentos). As janelas de documentos normalmente são usadas para a exibição e modificação do código-fonte ou do texto, mas também podem hospedar outros tipos funcionais. Janelas de documentos:

- Pode ser organizado em grupos de guias horizontais ou verticais separados no MDI pai para que vários arquivos possam ser exibidos ao mesmo tempo.

- Pode ser encaixado em qualquer ordem no MDI pai.

- Pode ser flutuante livremente.

- São vinculados em ordem de tabulação a outras janelas MDI.

  Os comandos para agrupamento, encaixe e flutuação podem ser encontrados no menu de atalho para uma guia de janela de documento.

  Para obter mais informações sobre o comportamento da janela no Visual Studio, consulte [Personalizar layouts de janela](../../ide/customizing-window-layouts-in-visual-studio.md).

## <a name="document-window-implementation"></a>Implementação da janela do documento
 As janelas de documentos são criadas com a implementação de um editor. A <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> interface cria janelas de documentos como parte da instanciação de um editor. Para obter mais informações, consulte [interfaces herdadas no editor](/previous-versions/visualstudio/visual-studio-2015/extensibility/legacy-interfaces-in-the-editor?preserve-view=true&view=vs-2015).

> [!NOTE]
> Para fornecer pontos de navegação para trás e para frente em uma janela, implemente a <xref:Microsoft.VisualStudio.Shell.Interop.IVsBackForwardNavigation> interface. O editor de texto usa marcadores de texto para identificar pontos de navegação no documento.

## <a name="the-running-document-table"></a>A tabela de documentos em execução
 O IDE usa a tabela de documentos em execução (RDT) para acompanhar o status de cada janela do documento. O RDT é o mecanismo pelo qual as janelas de documentos são notificadas sobre eventos, como quando uma solução é fechada ou quando um arquivo é editado. Para obter mais informações, consulte [executando a tabela de documentos](../../extensibility/internals/running-document-table.md).

## <a name="see-also"></a>Confira também
- [Carregamento de documento atrasado](../../extensibility/internals/delayed-document-loading.md)
