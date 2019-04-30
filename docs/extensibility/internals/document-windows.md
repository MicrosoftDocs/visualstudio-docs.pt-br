---
title: Documentar Windows | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio SDK, document windows
ms.assetid: 50081d48-987f-43db-8bf9-51b7cf76e9c0
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 490c39b9e97ad6a55ca2d1695d31b85ecc13dc57
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63418592"
---
# <a name="document-windows"></a>Janelas de documento
No Visual Studio, uma *janela de documento* é uma janela com moldura filho que está associada uma janela de interface de documentos múltiplos (MDI). Janelas de documento normalmente são usadas para a exibição e modificação do código-fonte ou texto, mas eles também podem hospedar outros tipos de funcionais. Janelas de documento:

- Podem ser organizados em grupos de guia horizontal ou vertical separada no pai MDI, para que vários arquivos podem ser exibidos ao mesmo tempo.

- Podem ser encaixadas em qualquer ordem no pai MDI.

- Pode ser flutuante livremente.

- São vinculados na ordem de tabulação para outras janelas MDI.

  Os comandos para agrupamento, Encaixando e flutuando podem ser encontrados no menu de atalho para uma guia da janela de documento.

  Para obter mais informações sobre o comportamento de janela no Visual Studio, consulte [Personalizar layouts de janela](../../ide/customizing-window-layouts-in-visual-studio.md).

## <a name="document-window-implementation"></a>Implementação de janela de documento
 Janelas de documento são criadas com a implementação de um editor. O <xref:Microsoft.VisualStudio.Shell.Interop.IVsEditorFactory> interface cria janelas de documentos como parte de criar uma instância de um editor. Para obter mais informações, consulte [herdado interfaces no editor de](../../extensibility/legacy-interfaces-in-the-editor.md).

> [!NOTE]
> Para fornecer para trás e encaminhar os pontos em uma janela de navegação, implementar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsBackForwardNavigation> interface. O editor de texto usa marcadores de texto para identificar os pontos de navegação no documento.

## <a name="the-running-document-table"></a>A tabela de documento em execução
 O IDE usa a tabela de documento de execução (RDT) para acompanhar o status de cada janela de documento. O RDT é o mecanismo pelo qual documento windows são notificados sobre eventos, como quando uma solução é fechada ou quando um arquivo foi editado. Para obter mais informações, consulte [tabela de documento em execução](../../extensibility/internals/running-document-table.md).

## <a name="see-also"></a>Consulte também
- [Atraso de carregamento do documento](../../extensibility/internals/delayed-document-loading.md)