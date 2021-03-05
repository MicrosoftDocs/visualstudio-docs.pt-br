---
description: Especifica se o mapa de endereço deve ser usado para converter endereços de símbolo.
title: IDiaAddressMap::put_addressMapEnabled | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::put_addressMapEnabled method
ms.assetid: 0f205337-4e59-4383-8059-7b1d207d6dcd
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 84878e83db15cfa5a9c68dccfec78536035cb70f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159510"
---
# <a name="idiaaddressmapput_addressmapenabled"></a>IDiaAddressMap::put_addressMapEnabled
Especifica se o mapa de endereço deve ser usado para converter endereços de símbolo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT put_addressMapEnabled ( 
   BOOL NewVal
);
```

#### <a name="parameters"></a>Parâmetros
 NewVal

no Defina como `TRUE` para habilitar a tradução de símbolos ou `FALSE` para desabilitar.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Os pós-processadores executáveis às vezes atualizam o executável. DIA contém um mecanismo para dar suporte à tradução de símbolos para o novo layout.

 Quando um arquivo PDB é carregado, o mapa de endereços armazenado no arquivo é habilitado. No entanto, há ocasiões em que um aplicativo cliente pode precisar fornecer seu próprio mapa de endereços chamando o método [IDiaAddressMap:: set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) . Se o `set_addressMap` método for bem-sucedido, o aplicativo cliente deverá chamar o `put_addressMapEnabled` método com um `NewVal` parâmetro de `TRUE` para habilitar o uso desse mapa de endereço.

 O estado atual do mapa de endereços que está sendo habilitado pode ser recuperado com uma chamada para o método [IDiaAddressMap:: get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md) .

## <a name="see-also"></a>Confira também
- [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)
- [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)
- [IDiaAddressMap::get_addressMapEnabled](../../debugger/debug-interface-access/idiaaddressmap-get-addressmapenabled.md)
