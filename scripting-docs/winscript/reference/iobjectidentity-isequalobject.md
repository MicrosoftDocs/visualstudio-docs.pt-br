---
title: IObjectIdentity::IsEqualObject | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IObjectIdentity.IsEqualObject
apilocation:
- scrobj.dll
helpviewer_keywords:
- IsEqualObject method
ms.assetid: 78c5c5c2-d299-4036-986c-7c1d87cbe7cd
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 52e386055e458568f8d4076a37489b7b2397f399
ms.sourcegitcommit: aadb9588877418b8b55a5612c1d3842d4520ca4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2017
ms.locfileid: "24728596"
---
# <a name="iobjectidentityisequalobject"></a>IObjectIdentity::IsEqualObject
Determina se um objeto é igual ao objeto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT IsEqualObject(  
  IUnknown*punk  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `punk`  
 [in] Endereço do objeto a ser comparado com o objeto atual.  
  
## <a name="return-value"></a>Valor de retorno  
 O método retorna um `HRESULT`. Os possíveis valores incluem, mas sem limitação, aqueles na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|`S_OK`|Os objetos são iguais.|  
|`S_FALSE`|Os objetos não são iguais.|  
  
## <a name="remarks"></a>Comentários  
 Uma implementação de `IsEqualObject` método deve retornar `S_OK` somente se os objetos são idênticos.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IObjectIdentity](../../winscript/reference/iobjectidentity-interface.md)