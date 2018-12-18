---
title: Script ativo constantes, enumerações e códigos de erro | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: aab24471-5817-45c0-be07-ffe4648923ed
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: bb4165a5471c8e79827f0f7605cef575e82bab75
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24641566"
---
# <a name="active-script-constants-enumerations-and-error-codes"></a>Constantes, enumerações e códigos de erro do script ativo
Esta seção descreve as enumerações e códigos de erro usados nos mecanismos de script do Windows.  
  
## <a name="constants"></a>Constantes  
  
|Constante|Descrição|  
|--------------|-----------------|  
|[Constantes SCRIPTTHREADID](../../winscript/reference/scriptthreadid-constants.md)|Especifica o tipo de segmento.|  
  
## <a name="properties"></a>Propriedades  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|[Propriedade SCRIPTPROP_HOSTKEEPALIVE](../../winscript/reference/scriptprop-hostkeepalive-property.md)|Usado para especificar se o mecanismo de script deve ser mantido totalmente funcional, se houver referências pendentes.|  
  
## <a name="enumerations"></a>Enumerações  
  
|Enumeração|Descrição|  
|-----------------|-----------------|  
|[Enumeração SCRIPTGCTYPE](../../winscript/reference/scriptgctype-enumeration.md)|O tipo de coleta de lixo para executar.|  
|[Enumeração SCRIPTLANGUAGEVERSION](../../winscript/reference/scriptlanguageversion-enumeration.md)|Especifica os possíveis versões de script.|  
|[Enumeração SCRIPTSTATE](../../winscript/reference/scriptstate-enumeration.md)|Especifica o estado de um mecanismo de script.|  
|||  
|[Enumeração SCRIPTTHREADSTATE](../../winscript/reference/scriptthreadstate-enumeration.md)|Especifica o estado de um thread em um mecanismo de script.|  
|[Enumeração SCRIPTTRACEINFO](../../winscript/reference/scripttraceinfo-enumeration.md)|Representa o evento de script que está sendo rastreado. Usado no [: Sendscripttraceinfo método](../../winscript/reference/iactivescriptsitetraceinfo-sendscripttraceinfo-method.md).|  
|[Enumeração SCRIPTUICHANDLING](../../winscript/reference/scriptuichandling-enumeration.md)|Representa a maneira que o controle de interface do usuário deve ser tratado.|  
|[Enumeração SCRIPTUICITEM](../../winscript/reference/scriptuicitem-enumeration.md)|Representa o tipo de item de interface do usuário. Usado no [método Iactivescriptsiteuicontrol:](../../winscript/reference/iactivescriptsiteuicontrol-getuibehavior-method.md).|  
  
## <a name="error-codes"></a>Códigos de erro  
  
|Código do erro|Descrição|  
|----------------|-----------------|  
|[Código de erro SCRIPT_E_PROPAGATE](../../winscript/reference/script-e-propagate-error-code.md)|Um erro de script está sendo propagado para o chamador, que pode estar em um thread diferente.|  
|[Código de erro SCRIPT_E_RECORDED](../../winscript/reference/script-e-recorded-error-code.md)|Um erro foi passado entre o mecanismo de script e o host.|  
|[Código de erro SCRIPT_E_REPORTED](../../winscript/reference/script-e-reported-error-code.md)|O mecanismo de script relatou uma exceção sem tratamento no host.|  
  
## <a name="see-also"></a>Consulte também  
 [Interfaces de script ativo](../../winscript/reference/active-script-interfaces.md)