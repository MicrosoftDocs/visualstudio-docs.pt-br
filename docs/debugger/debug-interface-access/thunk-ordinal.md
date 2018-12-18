---
title: THUNK_ORDINAL | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Thunk_Ordinal enumeration
ms.assetid: 026f98a9-36b8-41ef-8a72-12d7cbc2d362
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: a92e0fa81bdfc7c33e790c5022c2fbe341d632be
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49847702"
---
# <a name="thunkordinal"></a>THUNK_ORDINAL
Designa os tipos de conversão.  
  
## <a name="syntax"></a>Sintaxe  
  
```C++  
typedef enum THUNK_ORDINAL {   
   THUNK_ORDINAL_NOTYPE,  
   THUNK_ORDINAL_ADJUSTOR,  
   THUNK_ORDINAL_VCALL,  
   THUNK_ORDINAL_PCODE,  
   THUNK_ORDINAL_LOAD   
  
   // trampoline thunk ordinals - only for use in Trampoline thunk symbols  
   THUNK_ORDINAL_TRAMP_INCREMENTAL,  
   THUNK_ORDINAL_TRAMP_BRANCHISLAND,  
} THUNK_ORDINAL;  
```  
  
## <a name="elements"></a>Elementos  
 THUNK_ORDINAL_NOTYPE  
 Conversão padrão.  
  
 THUNK_ORDINAL_ADJUSTOR  
 Um `this` thunk adjustor.  
  
 THUNK_ORDINAL_VCALL  
 Conversão de chamada virtual.  
  
 THUNK_ORDINAL_PCODE  
 Conversão de código de P.  
  
 THUNK_ORDINAL_LOAD  
 Conversão de carregamento de atraso.  
  
 THUNK_ORDINAL_TRAMP_INCREMENTAL  
 Conversão de trampoline incremental (uma conversão trampoline é usada para chamadas de rejeição do espaço de memória para outro).  
  
 THUNK_ORDINAL_TRAMP_BRANCHISLAND  
 Conversão de trampoline do ponto de ramificação.  
  
## <a name="remarks"></a>Comentários  
 Os valores nesta enumeração são retornados de uma chamada para o [idiasymbol:: Get_thunkordinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md) método.  
  
## <a name="requirements"></a>Requisitos  
 Cabeçalho: cvconst.h  
  
## <a name="see-also"></a>Consulte também  
 [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)   
 [IDiaSymbol::get_thunkOrdinal](../../debugger/debug-interface-access/idiasymbol-get-thunkordinal.md)