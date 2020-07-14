---
title: CV_call_e | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- CV_call_e enumeration
ms.assetid: f230560b-4243-432d-8f19-46df112043b9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: afab1aef58616bfa925fd9f37aacf195eb569c96
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462137"
---
# <a name="cv_call_e"></a>CV_call_e
Especifica a Convenção de chamada para uma função.

> [!NOTE]
> Somente os valores de enumeração mais comuns são documentados aqui. A enumeração completa está disponível no arquivo de cabeçalho cvconst. h.

## <a name="syntax"></a>Syntax

```C++
typedef enum CV_call_e {
    CV_CALL_NEAR_C    = 0x00,
    CV_CALL_NEAR_FAST = 0x04,
    CV_CALL_NEAR_STD  = 0x07,
    CV_CALL_NEAR_SYS  = 0x09,
    CV_CALL_THISCALL  = 0x0b,
    CV_CALL_CLRCALL   = 0x16
} CV_call_e;
```

## <a name="elements"></a>Elementos
CV_CALL_NEAR_C especifica uma Convenção de chamada de função usando um push próximo da direita para a esquerda. A função de chamada limpa a pilha.

CV_CALL_NEAR_FAST especifica uma Convenção de chamada de função usando um push próximo da esquerda para a direita com registros. A função chamada usa a soma dos bytes de parâmetro para limpar a pilha.

CV_CALL_NEAR_STD especifica uma Convenção de chamada de função usando uma chamada quase padrão (Push da direita para a esquerda).

CV_CALL_NEAR_SYS especifica uma Convenção de chamada de função usando uma chamada do sistema próxima.

CV_CALL_THISCALL especifica uma Convenção de chamada de função usando `this` Call ( `this` ponteiro passado no registro).

CV_CALL_CLRCALL especifica uma Convenção de chamada de função usada pelo CLR (Common Language Runtime) (também conhecido como Convenção de chamada de código gerenciado).

## <a name="remarks"></a>Comentários
Os valores nessa enumeração são retornados por uma chamada para o método [IDiaSymbol:: get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md) .

## <a name="requirements"></a>Requisitos
Cabeçalho: cvconst. h

## <a name="see-also"></a>Veja também
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [IDiaSymbol::get_callingConvention](../../debugger/debug-interface-access/idiasymbol-get-callingconvention.md)
