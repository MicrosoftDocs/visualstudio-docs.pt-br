---
title: IDebugProperty::EnumMembers | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDebugProperty.EnumMembers
apilocation:
- scrobj.dll
helpviewer_keywords:
- IDebugProperty::EnumMembers
ms.assetid: 8ce398a5-6452-4804-ae8f-5c54cd11c661
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 07ad47ee8d0232df5f528db659def421475e7b33
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49924226"
---
# <a name="idebugpropertyenummembers"></a>IDebugProperty::EnumMembers
Enumera os membros de uma propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT EnumMembers (  
   DBGPROP_INFO_FLAGSdwFieldSpec,  
   UINTnRadix,  
   REFIIDrefiid,  
   IEnumDebugPropertyInfo**ppEnum  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `dwFieldSpec`  
 [in] Especifica o `DBGPROP_INFO_FLAGS` constantes que determinam quais campos nas estruturas de propriedade de depuração enumerados são a serem preenchidos.  
  
 `nRadix`  
 [in] Base a ser usado na interpretação de todas as informações numéricas.  
  
 `refiid`  
 [in] Este IID é passado para o enumerador de filtragem. O IID é um dos `IDebugPropertyEnumType` interfaces que herdam de `IDebugPropertyEnumType_All`.  
  
 `ppEnum`  
 [out] Retorna o `IEnumDebugPropertyInfo` interface que enumera as propriedades do membro.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um válidas `HRESULT`, normalmente `S_OK`.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDebugProperty](../../winscript/reference/idebugproperty-interface.md)   
 [DBGPROP_INFO_FLAGS](../../winscript/reference/dbgprop-info-flags.md)   
 [Interface IDebugPropertyEnumType_All](../../winscript/reference/idebugpropertyenumtype-all-interface.md)   
 [Interface IEnumDebugPropertyInfo](../../winscript/reference/ienumdebugpropertyinfo-interface.md)