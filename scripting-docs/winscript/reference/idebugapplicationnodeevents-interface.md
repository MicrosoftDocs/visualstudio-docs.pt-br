---
title: Interface IDebugApplicationNodeEvents | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugApplicationNodeEvents interface
ms.assetid: 02e0bb17-84ce-458b-bae6-608a9899e535
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 20d0fac68bb7cdb3d7f5cb6aac6b0ab67e373c84
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24726566"
---
# <a name="idebugapplicationnodeevents-interface"></a>Interface IDebugApplicationNodeEvents
Fornece a interface de eventos para a interface `IDebugApplicationNode`.  
  
 Além dos métodos herdados de `IUnknown`, o `IDebugApplicationNodeEvents` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugApplicationNodeEvents::onAddChild](../../winscript/reference/idebugapplicationnodeevents-onaddchild.md)|Manipula o evento quando um nó filho é adicionado a um objeto de nó de aplicativo de depuração.|  
|[IDebugApplicationNodeEvents::onRemoveChild](../../winscript/reference/idebugapplicationnodeevents-onremovechild.md)|Manipula o evento quando um nó filho é removido de um objeto de nó de aplicativo de depuração.|  
|[IDebugApplicationNodeEvents::onDetach](../../winscript/reference/idebugapplicationnodeevents-ondetach.md)|Manipula um evento indicando que o objeto de nó de aplicativo de depuração foi desanexado de um nó pai.|  
|[IDebugApplicationNodeEvents::onAttach](../../winscript/reference/idebugapplicationnodeevents-onattach.md)|Manipula um evento indicando que o objeto de nó de aplicativo de depuração foi anexado a um nó pai.|  
  
## <a name="see-also"></a>Consulte também  
 [IDebugApplicationNode Interface](../../winscript/reference/idebugapplicationnode-interface.md)