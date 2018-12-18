---
title: IScriptEntry::GetRange | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IScriptEntry.GetRange
apilocation:
- scrobj.dll
helpviewer_keywords:
- IScriptEntry::GetRange
ms.assetid: 3ac18f0a-b470-4f4d-b8f5-2da3fdef74f1
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0ae0ee34298e03fdd2e9c6bc841d9fbe90967e8f
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24729036"
---
# <a name="iscriptentrygetrange"></a>IScriptEntry::GetRange
Retorna a posição inicial e o comprimento de uma entrada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetRange(  
   ULONG              *pichMin  
   ULONG              *pcch  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pichMin`  
 [out] Para `IScriptEntry` objetos que especificam um bloco de script, retornará 0.  
  
 Para `IScriptEntry` objetos que especificam um objeto de função, retorna a posição inicial da função no bloco de script atual.  
  
 Para `IScriptScriptlet` objetos, retorna 0.  
  
 `pcch`  
 [out] Para `IScriptEntry` objetos que especificam um bloco de script, retorna o comprimento do texto.  
  
 Para `IScriptEntry` objetos que especificam um objeto de função, retorna o comprimento da definição da função.  
  
 Para `IScriptScriptlet` objetos, retorna o comprimento da entrada.  
  
## <a name="return-value"></a>Valor de retorno  
 Um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|O método foi bem-sucedido.|  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [IScriptEntry Interface](../../winscript/reference/iscriptentry-interface.md)