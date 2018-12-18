---
title: IActiveScriptSiteWindow | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptSiteWindow interface
ms.assetid: 96d5c493-2c0b-47e2-848b-4a8dacdcd65c
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3043a3c36b2f1ebdf439f22b1de19dd559e50cfa
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24725126"
---
# <a name="iactivescriptsitewindow"></a>IActiveScriptSiteWindow
Essa interface é implementada por hosts que oferecem suporte a uma interface do usuário no mesmo objeto como [IActiveScriptSite](../../winscript/reference/iactivescriptsite.md) . Hosts que não oferecem suporte a uma interface de usuário, como servidores, não implementa o `IActiveScriptSiteWindow` interface. O mecanismo de script acessa essa interface chamando `QueryInterface` de `IActiveScriptSite`.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IActiveScriptSiteWindow::GetWindow](../../winscript/reference/iactivescriptsitewindow-getwindow.md)|Recupera o identificador de janela que pode atuar como o proprietário de uma janela pop-up que o mecanismo de script deve ser exibido.|  
|[IActiveScriptSiteWindow::EnableModeless](../../winscript/reference/iactivescriptsitewindow-enablemodeless.md)|Faz com que o host habilitar ou desabilitar a janela principal, bem como todas as caixas de diálogo sem janela restrita.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de script ativo](../../winscript/reference/active-script-interfaces.md)