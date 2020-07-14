---
title: IDiaSymbol::get_value | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_value method
ms.assetid: 2e40174a-2a61-4e5f-bb32-9e0ceec2178a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c9a36da3feecfe1af664e35fa50d616d2a94fb0a
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461507"
---
# <a name="idiasymbolget_value"></a>IDiaSymbol::get_value
Recupera o valor de uma constante.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_value (
    VARIANT* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
`pRetVal`

[entrada, saída] Um `VARIANT` objeto que é preenchido com o valor de uma constante.

## <a name="return-value"></a>Valor Retornado
Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno de `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
A variante fornecida deve ser inicializada antes de ser passada para esse método. Para obter mais informações, consulte o exemplo.

## <a name="example"></a>Exemplo

```C++
void ProcessValue(IDiaSymbol *pSymbol)
{
    VARIANT value;
    value.vt = VT_EMPTY;    // Initialize variant for use.
    if (pSymbol->get_value(&value) == S_OK)
    {
        // Do something with value.
    }
}

//----------------------------------------------------
// Alternate approach
void ProcessValue2(IDiaSymbol *pSymbol)
{
    CComVariant value;
    if (pSymbol->get_value(&value) == S_OK)
    {
        // Do something with value
    }
}
```

## <a name="see-also"></a>Confira também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
