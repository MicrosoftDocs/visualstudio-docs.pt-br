---
title: LocationType | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- LocationType enumeration
ms.assetid: d3e1eedc-bfd3-4c91-881b-d69565138d0f
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e816ac9dca3c70e88ae023b4fda4edf0b99f9c96
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49872090"
---
# <a name="locationtype"></a>LocationType
Indica o tipo de informações de localização contidas em um símbolo.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
enum LocationType {   
   LocIsNull,  
   LocIsStatic,  
   LocIsTLS,  
   LocIsRegRel,  
   LocIsThisRel,  
   LocIsEnregistered,  
   LocIsBitField,  
   LocIsSlot,  
   LocIsIlRel,  
   LocInMetaData,  
   LocIsConstant,  
   LocTypeMax  
};  
```  
  
## <a name="elements"></a>Elementos  
 `LocIsNull`  
 Informações de localização não estão disponíveis.  
  
 `LocIsStatic`  
 Localização é estática.  
  
 `LocIsTLS`  
 Local está no armazenamento local de thread.  
  
 `LocIsRegRel`  
 Local é relativo ao registro.  
  
 `LocIsThisRel`  
 Local é `this`-relativo.  
  
 `LocIsEnregistered`  
 Localização é um registro.  
  
 `LocIsBitField`  
 Localização é um campo de bits.  
  
 `LocIsSlot`  
 Local é um slot de Microsoft Intermediate Language (MSIL).  
  
 `LocIsIlRel`  
 Local é relativo ao MSIL.  
  
 `LocInMetaData`  
 Local é nos metadados.  
  
 `LocIsConstant`  
 Localização é um valor constante.  
  
 `LocTypeMax`  
 O número de tipos de localização nesta enumeração.  
  
## <a name="remarks"></a>Comentários  
 As propriedades disponíveis para o [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) interface dependem do local do símbolo no arquivo de imagem. Para obter mais informações, consulte [locais de símbolos](../../debugger/debug-interface-access/symbol-locations.md).  
  
 Os valores nesta enumeração são retornados por uma chamada para o [idiasymbol:: Get_locationtype](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: cvconst.h  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)   
 [Idiasymbol:: Get_locationtype](../../debugger/debug-interface-access/idiasymbol-get-locationtype.md)   
 [Locais de símbolos](../../debugger/debug-interface-access/symbol-locations.md)