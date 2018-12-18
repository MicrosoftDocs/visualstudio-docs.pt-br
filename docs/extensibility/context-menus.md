---
title: Menus de contexto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- editors [Visual Studio SDK], legacy - context menus
ms.assetid: 44fd9e6a-6d42-4aba-80ba-f37fa0070f1d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: afd67578bee63408b50e402fb0bd8b29be3fc6eb
ms.sourcegitcommit: 25a62c2db771f938e3baa658df8b1ae54a960e4f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2018
ms.locfileid: "39232527"
---
# <a name="context-menus"></a>Menus de contexto
Menus de contexto são exibidos quando um usuário clica com o botão direito em uma região ativa da área de cliente e limpar quando o botão direito do mouse é liberado.  
  
## <a name="editor-context-menus"></a>Menus de contexto do Editor  
 Interceptando `ECMD_SHOWCONTEXTMENU`, seu serviço de linguagem pode controlar os menus de contexto serão exibido no editor. Para exibir seu próprio menu de contexto, lidar com esse comando quando ele é passado para seus <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIShell.ShowContextMenu%2A>. Se você não tratar esse comando, o IDE exibirá um menu de contexto padrão fornecido para o editor. Você também pode controlar o conteúdo do menu de contexto em uma base por marcador. Para obter mais informações sobre isso, consulte [usar marcadores de texto com a API herdada](../extensibility/using-text-markers-with-the-legacy-api.md) e [interceptar comandos do serviço de linguagem herdado](../extensibility/internals/intercepting-legacy-language-service-commands.md).  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolver um serviço de linguagem herdado](../extensibility/internals/developing-a-legacy-language-service.md)   
 [Ampliar menus e comandos](../extensibility/extending-menus-and-commands.md)