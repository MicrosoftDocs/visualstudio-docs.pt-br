---
title: 'Idiaaddressmap:: Put_addressmapenabled | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_addressMapEnabled method
ms.assetid: 0f205337-4e59-4383-8059-7b1d207d6dcd
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6894cb14d2aee6a4e1999eab38e095911d51360d
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53876003"
---
# <a name="idiaaddressmapputaddressmapenabled"></a>IDiaAddressMap::put_addressMapEnabled
Especifica se o mapa de endereço deve ser usado para converter endereços de símbolo.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
HRESULT put_addressMapEnabled (   
   BOOL NewVal  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 NewVal  
 [in] Definido como `TRUE` para habilitar a conversão de símbolos, ou `FALSE` para desabilitar.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Pós-processadores de executáveis, às vezes, atualize o executável. DIA contém um mecanismo para dar suporte a tradução de símbolos para o novo layout.  
  
 Quando um arquivo PDB é carregado, armazenado no arquivo de mapa de endereço está habilitado. Há vezes, no entanto, quando um aplicativo cliente talvez seja necessário fornecer seu próprio mapa de endereço chamando o [idiaaddressmap:: Set_addressmap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) método. Se o `set_addressMap` método for bem-sucedido, o aplicativo cliente deve chamar o `put_addressMapEnabled` método com um `NewVal` parâmetro do `TRUE` para habilitar o uso desse mapa de endereço.  
  
 O estado atual do mapa de endereço que está sendo habilitado pode ser recuperado com uma chamada para o [idiaaddressmap:: Get_addressmapenabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md) método.  
  
## <a name="see-also"></a>Consulte também  
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)   
 [IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)