---
title: IDiaStackWalker::getEnumFrames2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalker2::getEnumFrames2 method
ms.assetid: 73196d3f-112c-4b3a-997b-7c6b815d4afc
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 28e2f0ec5f176ab32e6bfed1e959f68c04550f67
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464852"
---
# <a name="idiastackwalkergetenumframes2"></a>IDiaStackWalker::getEnumFrames2
Recupera um enumerador de quadro de pilha para um tipo de plataforma específico.

## <a name="syntax"></a>Sintaxe

```C++

      HRESULT getEnumFrames2( 
   enum  CV_CPU_TYPE_e    cpuid,
   IDiaStackWalkHelper*   pHelper,
   IDiaEnumStackFrames**  ppEnum
);
```

#### <a name="parameters"></a>Parâmetros
 `cpuid`

no Um valor da enumeração de [enumeração de CV_CPU_TYPE_e](../../debugger/debug-interface-access/cv-cpu-type-e.md) , especificando o tipo de plataforma.

 `pHelper`

no O objeto auxiliar [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md) .

 `ppEnum`

fora Retorna um objeto [IDiaEnumStackFrames](../../debugger/debug-interface-access/idiaenumstackframes.md) que contém uma lista de objetos [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Para obter uma lista de quadros de pilha para apenas a plataforma x86, chame o método [IDiaStackWalker:: getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md) .

## <a name="see-also"></a>Veja também
- [IDiaStackWalker](../../debugger/debug-interface-access/idiastackwalker.md)
- [Enumeração CV_CPU_TYPE_e](../../debugger/debug-interface-access/cv-cpu-type-e.md)
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
- [IDiaStackWalker::getEnumFrames](../../debugger/debug-interface-access/idiastackwalker-getenumframes.md)