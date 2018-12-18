---
title: Propriedade SCRIPTPROP_HOSTKEEPALIVE | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: bfa199f2-28ba-4320-bc0f-2320fad018bd
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: a39ae7100c5567d2b03b7998077b20b1078810aa
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24734136"
---
# <a name="scriptprophostkeepalive-property"></a>Propriedade SCRIPTPROP_HOSTKEEPALIVE
Usado para especificar se o mecanismo de script deve ser mantido totalmente funcional, se houver referências pendentes.  
  
 Use [IActiveScriptProperty::SetProperty](../../winscript/reference/iactivescriptproperty-setproperty.md) para definir essa propriedade como `true`. Se essa propriedade é definida como `true`, o mecanismo de script é mantido totalmente funcional, desde que exista pelo menos uma referência pendente para o mecanismo de script ou um `IDispatch` ponteiro para um objeto JavaScript criado usando o script mecanismo. Quando essa propriedade é definida como `true`, não foi explicitamente, você deve fechar ou redefinir o mecanismo de script usando o [IActiveScript::Close](../../winscript/reference/iactivescript-close.md) ou [IActiveScript::SetScriptState](../../winscript/reference/iactivescript-setscriptstate.md) métodos. A versão da última referência a um objeto de script desliga o mecanismo de script.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
#define SCRIPTPROP_HOSTKEEPALIVE 0x70000004  
```  
  
## <a name="requirements"></a>Requisitos  
 Esta propriedade aparece apenas na versão do activscp.idl que é instalado com o [!INCLUDE[win8](../../javascript/includes/win8-md.md)], com 2707082 KB para o Internet Explorer 8 em [!INCLUDE[win7](../../winscript/reference/includes/win7-md.md)], ou com 2722913 KB para o Internet Explorer 9 em [!INCLUDE[win7](../../winscript/reference/includes/win7-md.md)] ou [!INCLUDE[vista_first](../../winscript/reference/includes/vista-first-md.md)].