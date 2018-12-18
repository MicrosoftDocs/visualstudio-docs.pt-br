---
title: Interface IScriptEntry | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IScriptEntry interface
ms.assetid: 86da3bc1-58b7-4d73-87ab-bc3ce34e3f41
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a785be8777cf3400f7723c24f1022bad6e22e330
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729806"
---
# <a name="iscriptentry-interface"></a>Interface IScriptEntry
Um objeto que implementa o `IScriptEntry` interface representa um bloco de script ou um objeto de função.  
  
 Além dos métodos herdados de `IScriptNode`, o `IScriptEntry` interface expõe os métodos a seguir.  
  
## <a name="methods-in-vtable-order"></a>Métodos na ordem Vtable  
  
|Método|Descrição|  
|------------|-----------------|  
|[IScriptEntry::GetBody](../../winscript/reference/iscriptentry-getbody.md)|Retorna o texto que corresponde ao corpo de um `IScriptEntry` miniscript, bloco de função ou bloco de script.|  
|[IScriptEntry::GetItemName](../../winscript/reference/iscriptentry-getitemname.md)|Retorna o nome do item que identifica um `IScriptEntry` objeto.|  
|[IScriptEntry::GetName](../../winscript/reference/iscriptentry-getname.md)|Para entradas que representam um único objeto (como uma função), retorna o nome do objeto.|  
|[IScriptEntry::GetRange](../../winscript/reference/iscriptentry-getrange.md)|Retorna a posição inicial e o comprimento de uma entrada.|  
|[IScriptEntry::GetSignature](../../winscript/reference/iscriptentry-getsignature.md)|Retorna informações de tipo para um `IScriptEntry` objeto de função.|  
|[IScriptEntry::GetText](../../winscript/reference/iscriptentry-gettext.md)|Retorna o texto que corresponde a um `IScriptEntry` bloco de script ou o código-fonte que está contido em um `IScriptScriptlet` manipulador de eventos.|  
|[IScriptEntry::SetBody](../../winscript/reference/iscriptentry-setbody.md)|Define o texto no corpo de um `IScriptEntry` bloco de script ou um `IScriptScriptlet` miniscript.|  
|[IScriptEntry::SetItemName](../../winscript/reference/iscriptentry-setitemname.md)|Define o nome do item que identifica um `IScriptEntry` objeto.|  
|[IScriptEntry::SetName](../../winscript/reference/iscriptentry-setname.md)|Para entradas que representam um único objeto (como uma função), define o nome do objeto.|  
|[IScriptEntry::SetSignature](../../winscript/reference/iscriptentry-setsignature.md)|Conjuntos de informações de tipo para um `IScriptEntry` objeto de função.|  
|[IScriptEntry::SetText](../../winscript/reference/iscriptentry-settext.md)|Define o texto que corresponde a um `IScriptEntry` bloco de script ou o código-fonte que está contido em um `IScriptScriptlet` manipulador de eventos.|  
  
## <a name="see-also"></a>Consulte também  
 [Active Script Authoring Interfaces](../../winscript/reference/active-script-authoring-interfaces.md)