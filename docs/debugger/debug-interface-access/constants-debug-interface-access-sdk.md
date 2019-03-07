---
title: Constantes (SDK de acesso à Interface de depuração) | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
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
ms.openlocfilehash: ed505499efcabd7173fea9d668cd9afa5ed6d925
ms.sourcegitcommit: d0425b6b7d4b99e17ca6ac0671282bc718f80910
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 02/21/2019
ms.locfileid: "56608572"
---
# <a name="constants-debug-interface-access-sdk"></a>Constantes (SDK de Acesso à Interface de Depuração)
Constantes de cadeia de caracteres podem ser usados para identificar várias seções de um arquivo de banco de dados (PDB) de depuração do programa por meio do DIA SDK.

## <a name="constants"></a>Constantes
A seguir é declarados como macros do C/C++.

|Macro|Valor|
|-----------|-----------|
|`DiaTable_Symbols`|L "Símbolos"|
|`DiaTable_Sections`|L "Seções"|
|`DiaTable_SrcFiles`|L"SourceFiles"|
|`DiaTable_LineNums`|L "LineNumbers"|
|`DiaTable_SegMap`|L"SegmentMap"|
|`DiaTable_Dbg`|L"Dbg"|
|`DiaTable_InjSrc`|L "InjectedSource"|
|`DiaTable_FrameData`|L"FrameData"|

## <a name="example"></a>Exemplo
Aqui está um exemplo que usa um dos seguintes símbolos:

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
Cabeçalho: dia2.h

## <a name="see-also"></a>Consulte também
- [Referência](../../debugger/debug-interface-access/debug-interface-access-sdk-reference.md)
- [Enumerações e estruturas](../../debugger/debug-interface-access/enumerations-and-structures.md)
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaEnumTables::Item](../../debugger/debug-interface-access/idiaenumtables-item.md)
