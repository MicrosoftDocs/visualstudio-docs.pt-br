---
title: IScriptEntry::SetItemName | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.SetItemName
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::SetItemName
ms.assetid: 9551a7ec-38f8-466a-9722-09367763f380
caps.latest.revision: 11
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 483d3cdc1c8b8de9342003a99427fc2c727ad67f
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729296"
---
# <a name="iscriptentrysetitemname"></a>IScriptEntry::SetItemName
Define o nome do item que identifica um `IScriptEntry` objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT SetItemName(  
   LPCOLESTR          psz  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `psz`  
 [in] O endereço de um buffer que contém o nome do item. O nome do item é usado pelo host para identificar a entrada.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
|`E_FAIL`|O método não foi bem-sucedida.|  
  
## <a name="remarks"></a>Comentários  
 Para `IScriptEntry` objetos, esse método retornará `S_OK`.  
  
 Para `IScriptScriptlet` objetos (que derivam de `IScriptEntry`), esse método retornará `E_FAIL`. Para `IScriptScriptlet` objetos, o nome do item é definido por [IActiveScriptAuthor::AddScriptlet](../../winscript/reference/iactivescriptauthor-addscriptlet.md) e não pode ser alterado.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IScriptEntry](../../winscript/reference/iscriptentry-interface.md)   
 [IScriptEntry::GetItemName](../../winscript/reference/iscriptentry-getitemname.md)