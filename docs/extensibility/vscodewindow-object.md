---
title: Objeto VSCodeWindow | Microsoft Docs
description: Saiba mais sobre janelas de código, que são janelas de documentos especializadas que podem incluir uma ou mais exibições de texto, geralmente o objeto VsTextView.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- VSCodeWindow
helpviewer_keywords:
- views [Visual Studio SDK], VSCodeWindow object
- VsCodeWindow object
ms.assetid: cf5fe926-e784-4098-bc01-cac49c7c55c6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 77839bf80f30de3177f647795ffb89aa3e103d58
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062415"
---
# <a name="vscodewindow-object"></a>Objeto VSCodeWindow
Uma janela de código é uma janela de documento especializada que pode incluir uma ou mais exibições de texto, geralmente o <xref:Microsoft.VisualStudio.TextManager.Interop.VsTextView> objeto.

 Em termos de arquitetura, a janela de código é uma janela de documento que está dentro de um quadro de janela. Funcionalmente, a janela de código é simplesmente uma janela de documento com recursos adicionais. No modo MDI (interface de vários documentos), a janela de código é o quadro filho MDI. Para obter mais informações, consulte [Personalizando janelas de código usando a API herdada](/previous-versions/visualstudio/visual-studio-2015/extensibility/customizing-code-windows-by-using-the-legacy-api?preserve-view=true&view=vs-2015).

 A tabela a seguir inclui as interfaces no <xref:Microsoft.VisualStudio.TextManager.Interop.VsCodeWindow> objeto.

|Método|Descrição|
|------------|-----------------|
|<xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>|Fornece um mecanismo de acesso genérico para localizar um serviço que um GUID (identificador global exclusivo) identifica.|
|<xref:Microsoft.VisualStudio.TextManager.Interop.IVsCodeWindow>|Representa um filho MDI (interface de vários documentos) que contém uma ou mais exibições de código.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsWindowPane>|Preenche um quadro de janela.|

## <a name="see-also"></a>Confira também
- <xref:Microsoft.VisualStudio.OLE.Interop.IServiceProvider>
- [Edição de figuras](https://www.microsoft.com/download/details.aspx?id=55984)