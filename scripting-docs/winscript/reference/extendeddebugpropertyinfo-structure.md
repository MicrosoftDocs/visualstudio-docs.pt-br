---
title: Estrutura ExtendedDebugPropertyInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ExtendedDebugPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- ExtendedDebugPropertyInfo structure
ms.assetid: f2cf6477-454b-4d13-95da-ae4c90daa175
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 62b9f3b5877f7919a57e9747355276e438240796
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49888899"
---
# <a name="extendeddebugpropertyinfo-structure"></a>Estrutura ExtendedDebugPropertyInfo
Estende o `DebugPropertyInfo` estrutura com membros adicionais para caracterizar a propriedade estendida.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
typedef struct ExtendedDebugPropertyInfo{  
   DBGPROP_INFO_FLAGS  dwValidFields;  
   LPOLESTR  bstrName;  
   LPOLESTR  bstrType;  
   LPOLESTR  bstrValue;  
   LPOLESTR  bstrFullName;  
   DBGPROP_ATTRIB_FLAGS  dwAttrib;  
   IDebugProperty*  pDebugProp;  
   DWORD  nDISPID;  
   DWORD  nType;  
   VARIANT  varValue;  
   ILockBytes*  plbValue;  
   IDebugExtendedProperty*  pDebugExtProp;  
};  
```  
  
## <a name="members"></a>Membros  
 `dwValidFields`  
 Um tipo de dados enumerado usado para especificar quais campos são inicializados.  
  
 `bstrName`  
 O nome da propriedade dentro de um contexto.  
  
 `bstrType`  
 O tipo de propriedade como cadeia de caracteres formatada.  
  
 `bstrValue`  
 O valor da propriedade como uma cadeia de caracteres formatada.  
  
 `bstrFullName`  
 O nome completo da propriedade.  
  
 `dwAttrib`  
 Uma enumeração que especifica os sinalizadores para os atributos de propriedade de depuração.  
  
 `pDebugProp`  
 `IDebugProperty` objeto correspondente a este `ExtendedDebugPropertyInfo`.  
  
 `nDISPID`  
 A id de expedição.  
  
 `nType`  
 O tipo de propriedade estendida.  
  
 `varValue`  
 O valor da propriedade estendida se ele pode se ajustar na VARIANTE.  
  
 `plbValue`  
 Os bytes de dados reais do valor da propriedade.  
  
 `pDebugExtProp`  
 `IDebugExtendedProperty` objeto correspondente a este `ExtendedDebugPropertyInfo`.  
  
## <a name="see-also"></a>Consulte também  
 [Estrutura DebugPropertyInfo](../../winscript/reference/debugpropertyinfo-structure.md)   
 [Interface IDebugProperty](../../winscript/reference/idebugproperty-interface.md)   
 [Interface IDebugExtendedProperty](../../winscript/reference/idebugextendedproperty-interface.md)   
 [DBGPROP_ATTRIB_FLAGS](../../winscript/reference/dbgprop-attrib-flags.md)   
 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)