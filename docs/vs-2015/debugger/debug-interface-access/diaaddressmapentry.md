---
title: DiaAddressMapEntry | Microsoft Docs
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
- DiaAddressMapEntry enumeration
ms.assetid: 5d0ae226-981d-4541-a801-fc4993fe663b
caps.latest.revision: 12
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: fa2824b7fbd10e7628e5c6b0a016615620933df9
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51756244"
---
# <a name="diaaddressmapentry"></a>DiaAddressMapEntry
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Descreve uma entrada em um mapa de endereço.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp#  
struct DiaAddressMapEntry {   
   DWORD rva,  
   DWORD rvaTo  
};  
```  
  
## <a name="elements"></a>Elementos  
 `rva`  
 Um endereço virtual relativo (RVA) na imagem A.  
  
 `rvaTo`  
 O endereço virtual relativo `rva` é mapeado para imagem B.  
  
## <a name="remarks"></a>Comentários  
 Um mapa de endereço fornece uma tradução do layout de uma imagem (A) para outro (B). Uma matriz de `DiaAddressMapEntry` estruturas classificadas por `rva` define um mapa de endereço.  
  
 Para converter um endereço `addrA`, na imagem de um para um endereço, `addrB`, na imagem B, execute as seguintes etapas:  
  
1. O mapa para a entrada de pesquisa `e`, com o maior `rva` menor ou igual a `addrA`.  
  
2. Definir `delta = addrA – e.rva`.  
  
3. Definir `addrB = e.rvaTo + delta`.  
  
   Uma matriz de `DiaAddressMapEntry` estruturas é passada para o [idiaaddressmap:: Set_addressmap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: dia2.h  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaAddressMap::set_addressMap](../../debugger/debug-interface-access/idiaaddressmap-set-addressmap.md)



