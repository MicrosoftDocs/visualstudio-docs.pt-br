---
title: Interface IMachineDebugManagerCookie | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IMachineDebugManagerCookie interface
ms.assetid: 04770935-3ccf-41e9-b0c1-c78376ab1e3c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a03b959a7eb09f3b85530bbba07d1d2dc7f8948a
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729616"
---
# <a name="imachinedebugmanagercookie-interface"></a>Interface IMachineDebugManagerCookie
Como o `IMachineDebugManager` interface, o `IMachineDebugManagerCookie` interface oferece suporte a cookies de depuração.  
  
 Essa interface (juntamente com o `IDebugCookie` interface) que scripts sejam executados em um processo do depurador de script sem a necessidade de que o depurador controlar desses scripts.  
  
 Um depurador de script chama o `IDebugCookie::SetDebugCookie` método no processo de depuração Manager (PDM). Em seguida, o PDM envia esse cookie junto com qualquer solicitação para adicionar ou remover um aplicativo de script ou de máquina depurar Manager (MDM), usando os métodos do `IMachineDebugManagerCookie` interface. O MDM notifica cada depurador da alteração, exceto aquele que tem esse cookie.  
  
 Além dos métodos herdados de `IUnknown`, o `IMachineDebugManagerCookie` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IMachineDebugManagerCookie::AddApplication](../../winscript/reference/imachinedebugmanagercookie-addapplication.md)|Adiciona um aplicativo para a execução lista de aplicativos.|  
|[IMachineDebugManagerCookie::EnumApplications](../../winscript/reference/imachinedebugmanagercookie-enumapplications.md)|Retorna um enumerador da lista atual de execução de aplicativos.|  
|[IMachineDebugManagerCookie::RemoveApplication](../../winscript/reference/imachinedebugmanagercookie-removeapplication.md)|Remove um aplicativo de execução de lista de aplicativos.|  
  
## <a name="see-also"></a>Consulte também  
 [Interface IMachineDebugManager](../../winscript/reference/imachinedebugmanager-interface.md)   
 [Interface IDebugCookie](../../winscript/reference/idebugcookie-interface.md)