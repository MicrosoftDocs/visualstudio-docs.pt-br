---
title: Interface IDebugProperty | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IDebugProperty interface
ms.assetid: 7e8f5341-23ef-4029-814d-f5c2307b9203
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 2888a6d781ecd501128545e483971a47859d9cda
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24727056"
---
# <a name="idebugproperty-interface"></a>Interface IDebugProperty
Usado para descrever a qualquer propriedade hierárquica da entidade que está sendo depurada que tem um nome, tipo e valor. Mais comumente, `IDebugProperty` é usado para descrever o resultado da avaliação de expressão, avaliação de instrução ou avaliação de registro.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
 A tabela a seguir mostra os métodos do `IDebugProperty` Interface.  
  
|Método|Descrição|  
|------------|-----------------|  
|[IDebugProperty::GetPropertyInfo](../../winscript/reference/idebugproperty-getpropertyinfo.md)|Obter o `DebugPropertyInfo` que descreve esse`IDebugProperty``.`|  
|[IDebugProperty::GetExtendedInfo](../../winscript/reference/idebugproperty-getextendedinfo.md)|Obtém as informações estendidas em uma propriedade.|  
|[IDebugProperty::SetValueAsString](../../winscript/reference/idebugproperty-setvalueasstring.md)|Define o valor de uma propriedade de uma cadeia de caracteres.|  
|[IDebugProperty::EnumMembers](../../winscript/reference/idebugproperty-enummembers.md)|Enumera os membros de uma propriedade.|  
|[IDebugProperty::GetParent](../../winscript/reference/idebugproperty-getparent.md)|Obtém o pai de uma propriedade.|  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: dbgprop.h