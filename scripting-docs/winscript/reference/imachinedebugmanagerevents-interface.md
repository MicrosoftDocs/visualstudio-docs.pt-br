---
title: Interface IMachineDebugManagerEvents | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IMachineDebugManagerEvents interface
ms.assetid: 468de2f4-49e0-4f6f-ba0c-0f5f6832c092
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 369dc8d182efe7bf9697454d0e4b1c9c1a10c027
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727626"
---
# <a name="imachinedebugmanagerevents-interface"></a>Interface IMachineDebugManagerEvents
Sinaliza as alterações na lista de aplicativos em execução mantida pelo gerenciador de depuração do computador. Essa interface pode ser usada pelo depurador IDE para exibir uma lista dinâmica de aplicativos.  
  
 Além dos métodos herdados de `IUnknown`, o `IMachineDebugManagerEvents` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IMachineDebugManagerEvents::onAddApplication](../../winscript/reference/imachinedebugmanagerevents-onaddapplication.md)|Manipula o evento quando um aplicativo é adicionado à execução lista de aplicativos.|  
|[IMachineDebugManagerEvents::onRemoveApplication](../../winscript/reference/imachinedebugmanagerevents-onremoveapplication.md)|Manipula o evento quando um aplicativo é removido a execução de lista de aplicativos.|