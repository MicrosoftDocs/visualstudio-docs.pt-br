---
title: 'Idiaaddressmap:: Set_addressmap | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
helpviewer_keywords:
- IDiaAddressMap::set_addressMap method
ms.assetid: 81e82073-089b-43d5-af39-49d7a4907c7a
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: ea357cc04a2c0b1bce5882e1dd10cda8138a0b8c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756717"
---
# <a name="idiaaddressmapsetaddressmap"></a>IDiaAddressMap::set_addressMap
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Fornece um mapa de endereço para dar suporte a traduções de layout da imagem.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
HRESULT set_addressMap (   
   DWORD                     cbData,  
   struct DiaAddressMapEntry data[],  
   BOOL                      imagetoSymbols  
);  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `cbData`  
 [in] O número de elementos no `data` parâmetro.  
  
 `data[]`  
 [in] Uma matriz de [estrutura DiaAddressMapEntry](../../debugger/debug-interface-access/diaaddressmapentry.md) estruturas que definem o mapa de conversão.  
  
 `imagetoSymbols`  
 [in] `TRUE` se o `data` parâmetro define um mapa do novo layout de imagem ao layout original (conforme descrito pelos símbolos de depuração). `FALSE` Se `data` é um mapa para o novo layout da imagem tirado o layout original.  
  
## <a name="return-value"></a>Valor de retorno  
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.  
  
## <a name="remarks"></a>Comentários  
 Normalmente, o DIA recupera mapas de tradução de endereço do arquivo de banco de dados (. PDB) do programa. Se esses valores estiverem ausentes, o [idiaaddressmap:: Set_imageheaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md) método é chamado duas vezes, uma vez com o `imagetoSymbols` parâmetro definido como `TRUE` e uma vez com o `imagetoSymbols` parâmetro definido como `FALSE`. Conversões de mapa de endereço não podem ser habilitados usando o [idiaaddressmap:: Put_addressmapenabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md) método, a menos que ambos os mapas de tradução são fornecidos.  
  
## <a name="see-also"></a>Consulte também  
 [Estrutura DiaAddressMapEntry](../../debugger/debug-interface-access/diaaddressmapentry.md)   
 [IDiaAddressMap](../../debugger/debug-interface-access/idiaaddressmap.md)   
 [Idiaaddressmap:: Put_addressmapenabled](../../debugger/debug-interface-access/idiaaddressmap-put-addressmapenabled.md)   
 [IDiaAddressMap::set_imageHeaders](../../debugger/debug-interface-access/idiaaddressmap-set-imageheaders.md)



