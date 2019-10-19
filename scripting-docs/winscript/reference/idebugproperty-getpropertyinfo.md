---
title: 'IDebugProperty:: GetPropertyInfo | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugProperty.GetPropertyInfo
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugProperty::GetPropertyInfo
ms.assetid: b201c0c4-bff6-4285-880f-67be90584c5f
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: e0698e09cd9643322a237a81d971248577fd97e0
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72562331"
---
# <a name="idebugpropertygetpropertyinfo"></a>IDebugProperty::GetPropertyInfo
Obtém o valor de um `IDebugProperty` que descreve um método ou uma propriedade indexada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetPropertyInfo (  
   DBGPROP_INFO_FLAGSdwFields,  
   UINT nRadix,  
   DebugPropertyInfo* pPropertyInfo  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dwFields`  
 no Especifica as constantes de `DBGPROP_INFO_FLAGS` que determinam os campos a serem preenchidos na estrutura de `DebugPropertyInfo`.  
  
 `nRadix`  
 no Base a ser usada na formatação de qualquer informação numérica.  
  
 `pPropertyInfo`  
 fora Retorna a estrutura de `DebugPropertyInfo` que descreve a propriedade.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna um `HRESULT` válido, geralmente `S_OK`.  
  
## <a name="see-also"></a>Consulte também  
 @No__t_1 de [interface IDebugProperty](../../winscript/reference/idebugproperty-interface.md)  
 @No__t_1 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)  
 [Estrutura DebugPropertyInfo](../../winscript/reference/debugpropertyinfo-structure.md)