---
title: 'IDispatchEx:: GetNameSpaceParent | Microsoft Docs'
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- IDispatchEx.GetNameSpaceParent
apilocation:
- scrobj.dll
helpviewer_keywords:
- GetNameSpaceParent method
ms.assetid: 0b077d39-2fd6-4390-8cd5-128d9b8dc90c
caps.latest.revision: 8
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d2f47fab9831441e72a4ef3d4332a41c08e6a108
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72574076"
---
# <a name="idispatchexgetnamespaceparent"></a>IDispatchEx::GetNameSpaceParent
Recupera a interface para o pai do namespace de um objeto.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetNameSpaceParent(  
   IUnknown **ppunk  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `ppunk`  
 Endereço de um ponteiro de interface `IUnknown` que recebe a interface do pai do namespace.  
  
## <a name="return-value"></a>Valor retornado  
 Retorna `S_OK` se for bem-sucedido ou se um código de erro definido por OLE for diferente.  
  
## <a name="see-also"></a>Consulte também  
 [Interface IDispatchEx](../../winscript/reference/idispatchex-interface.md)