---
title: IDiaEnumSegments | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaEnumSegments interface
ms.assetid: 0c9edd5e-b9ce-43e1-a791-cd4c5d16d923
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cd6a0716d0bae5a223cff3439834c87b9650e7a5
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467942"
---
# <a name="idiaenumsegments"></a>IDiaEnumSegments
Enumera os vários segmentos contidos na fonte de dados.

## <a name="syntax"></a>Syntax

```
IDiaEnumSegments : IUnknown
```

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
A tabela a seguir mostra os métodos de `IDiaEnumSegments` .

|Método|Descrição|
|------------|-----------------|
|[IDiaEnumSegments::get__NewEnum](../../debugger/debug-interface-access/idiaenumsegments-get-newenum.md)|Recupera a versão da [interface IEnumVARIANT](/previous-versions/windows/desktop/api/oaidl/nn-oaidl-ienumvariant) deste enumerador.|
|[IDiaEnumSegments::get_Count](../../debugger/debug-interface-access/idiaenumsegments-get-count.md)|Recupera o número de segmentos.|
|[IDiaEnumSegments::Item](../../debugger/debug-interface-access/idiaenumsegments-item.md)|Recupera um segmento por meio de um índice.|
|[IDiaEnumSegments::Next](../../debugger/debug-interface-access/idiaenumsegments-next.md)|Recupera um número especificado de segmentos na sequência de enumeração.|
|[IDiaEnumSegments::Skip](../../debugger/debug-interface-access/idiaenumsegments-skip.md)|Ignora um número especificado de segmentos em uma sequência de enumeração.|
|[IDiaEnumSegments::Reset](../../debugger/debug-interface-access/idiaenumsegments-reset.md)|Redefine uma sequência de enumeração para o início.|
|[IDiaEnumSegments::Clone](../../debugger/debug-interface-access/idiaenumsegments-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração que o enumerador atual.|

## <a name="remarks"></a>Comentários

## <a name="notes-for-callers"></a>Observações para chamadores
Obtenha essa interface chamando o `QueryInterface` método em um objeto [IDiaTable](../../debugger/debug-interface-access/idiatable.md) . Consulte o exemplo para obter detalhes.

## <a name="example"></a>Exemplo
Este exemplo mostra como obter a `IDiaEnumSections` interface de uma tabela. Para obter um exemplo mais completo de como usar segmentos, consulte a interface [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) .

```C++
void ShowSegments(IDiaTable *pTable, IDiaSession *pSession)
{
    CComPtr<IDiaEnumSegments> pSegments;
    if ( SUCCEEDED( pTable->QueryInterface(
                                __uuidof( IDiaEnumSegments ),
                                (void**)&pSegments )
                  )
       )
    {
        // Do something with this enumeration
    }
}
```

## <a name="requirements"></a>Requisitos
Cabeçalho: dia2. h

Biblioteca: diaguids. lib

DLL: msdia80.dll

## <a name="see-also"></a>Veja também
- [Interfaces (SDK de Acesso à Interface de Depuração)](../../debugger/debug-interface-access/interfaces-debug-interface-access-sdk.md)
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
