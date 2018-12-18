---
title: 'Idiasymbol:: Get_registerid | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_registerId method
ms.assetid: f881e793-eb9e-48dc-a847-dd61d77174fc
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 0acc6d79e1e5da810e2f2da699df5d4def424df9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49861456"
---
# <a name="idiasymbolgetregisterid"></a>IDiaSymbol::get_registerId
Recupera o designador de registro do local quando o [enumeração LocationType](../../debugger/debug-interface-access/locationtype.md) é definido como `LocIsEnregistered`.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT get_registerId (   
   DWORD* pRetVal  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `pRetVal`  
 [out] Retorna o designador de registro do local.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna `S_FALSE` ou um código de erro.  
  
> [!NOTE]
>  Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.  
  
## <a name="remarks"></a>Comentários  
 Se o símbolo for em relação a um registro, ou seja, se o símbolo [enumeração LocationType](../../debugger/debug-interface-access/locationtype.md) é definido como `LocIsRegRel`, use o `get_registerId` método seguido por uma chamada para o [idiasymbol:: Get_offset](../../debugger/debug-interface-access/idiasymbol-get-offset.md) método para obter o deslocamento a partir do registro de onde se encontra o símbolo.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [Enumeração LocationType](../../debugger/debug-interface-access/locationtype.md)