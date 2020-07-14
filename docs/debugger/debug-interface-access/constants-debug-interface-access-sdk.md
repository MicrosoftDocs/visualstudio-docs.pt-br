---
title: Constantes (debug interface Access SDK) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- constants, DIA SDK
- DIA SDK, constants
ms.assetid: aca4ec77-bc08-4cdd-a6ce-8d4a28ea5ea3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3fa6037253141df1111ef3bc57fac9c718d826dc
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85462235"
---
# <a name="constants-debug-interface-access-sdk"></a>Constantes (SDK de Acesso à Interface de Depuração)
Essas constantes de cadeia de caracteres podem ser usadas para identificar várias seções de um arquivo PDB (banco de dados de depuração de programa) por meio do DIA SDK.

## <a name="constants"></a>Constantes
Os itens a seguir são declarados como macros C/C++.

|Macro|Valor|
|-----------|-----------|
|`DiaTable_Symbols`|L "Symbols"|
|`DiaTable_Sections`|L "seções"|
|`DiaTable_SrcFiles`|L"SourceFiles"|
|`DiaTable_LineNums`|L "LineNumbers"|
|`DiaTable_SegMap`|L"SegmentMap"|
|`DiaTable_Dbg`|L"Dbg"|
|`DiaTable_InjSrc`|L "InjectedSource"|
|`DiaTable_FrameData`|L"FrameData"|

## <a name="example"></a>Exemplo
Aqui está um exemplo que usa um destes símbolos:

```C++
HRESULT GetSymbolTable(IDiaEnumTables *pEnumTables, IDiaTable **pTable)
{
    HRESULT hr;
    VARIANT var;
    var.vt      = VT_BSTR;
    var.bstrVal = SysAllocString( DiaTable_Symbols );
    hr = pEnumTables->Item( var, pTable );
    return(hr);
}
```

## <a name="requirements"></a>Requisitos
Cabeçalho: dia2. h

## <a name="see-also"></a>Veja também
- [Referência](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
