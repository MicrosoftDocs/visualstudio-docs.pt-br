---
title: IEnumDebugExtendedPropertyInfo::Skip | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.prod: windows-script-interfaces
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IEnumDebugExtendedPropertyInfo.Skip
apilocation:
- scrobj.dll
helpviewer_keywords:
- IEnumDebugExtendedPropertyInfo::Skip
ms.assetid: a0b4a9fc-e122-482b-9384-b83c460b61fe
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cc88f41e1c75a2b6616cc6aba363b8824605a696
ms.sourcegitcommit: 116e9614867e0b3c627ce9001012a4c39435a42b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2019
ms.locfileid: "54094829"
---
# <a name="ienumdebugextendedpropertyinfoskip"></a>IEnumDebugExtendedPropertyInfo::Skip
Ignora um número especificado de `ExtendedDebugPropertyInfo` estruturas em uma sequência de enumeração.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT Skip(  
   ULONG celt  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `celt`  
 [in] O número de `ExtendedDebugPropertyInfo` estruturas na sequência de enumeração para ignorar.  
  
## <a name="return-value"></a>Valor de retorno  
 Retorna um válidas `HRESULT`, normalmente `S_OK`. Retorna `S_FALSE` e define o ponteiro do elemento atual até o final da enumeração se `celt` é maior que o número de elementos à esquerda no enumerador.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IEnumDebugExtendedPropertyInfo](../../winscript/reference/ienumdebugextendedpropertyinfo-interface.md)   
 [Estrutura ExtendedDebugPropertyInfo](../../winscript/reference/extendeddebugpropertyinfo-structure.md)