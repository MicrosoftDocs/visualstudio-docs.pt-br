---
title: 'IDiaSymbol:: get_platform | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_platform method
ms.assetid: dff1c1eb-bcb2-4275-bb07-f2fdc076d6fb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fe9da9a436604c869bb460dd6a30bf74c3c286f6
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462556"
---
# <a name="idiasymbolget_platform"></a>IDiaSymbol::get_platform
Recupera o tipo de plataforma para o qual o compiland foi compilado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_platform ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna um valor da enumeração de [enumeração CV_CPU_TYPE_e](../../debugger/debug-interface-access/cv-cpu-type-e.md) que especifica o tipo de plataforma para o qual o compiland foi compilado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração CV_CPU_TYPE_e](../../debugger/debug-interface-access/cv-cpu-type-e.md)