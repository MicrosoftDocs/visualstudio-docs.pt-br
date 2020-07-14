---
title: 'IDiaTable:: item | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::Item method
ms.assetid: eae11b26-4807-400c-be25-e85bbc0c6b20
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 18efd1113d66d36b99dd33eb3e79cb0cc7e8bb05
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461297"
---
# <a name="idiatableitem"></a>IDiaTable::Item
Recupera uma referência à entrada especificada na tabela.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT Item ( 
   DWORD      index,
   IUnknown** element
);
```

#### <a name="parameters"></a>Parâmetros
 `index`

no O índice da entrada da tabela no intervalo de 0 a `count` -1, em que `count` é retornado pelo método [IDiaTable:: get_Count](../../debugger/debug-interface-access/idiatable-get-count.md).

 `element`

fora Retorna um `IUnknown` objeto que representa a entrada da tabela especificada.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Uma tabela representa uma coleção de objetos. Dependendo desses objetos, o parâmetro do elemento pode ser convertido na interface apropriada. Por exemplo, se uma tabela contiver objetos [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md) , o parâmetro do elemento poderá ser convertido na `IDiaSegment` interface.

 É uma abordagem mais comum para chamar o `QueryInterface` método na interface [IDiaTable](../../debugger/debug-interface-access/idiatable.md) para a interface do enumerador apropriada e usar os métodos específicos do enumerador para acessar o conteúdo da tabela. Consulte a interface [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md) para obter um exemplo.

## <a name="see-also"></a>Veja também
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)
- [IDiaTable::get_Count](../../debugger/debug-interface-access/idiatable-get-count.md)
- [IDiaSegment](../../debugger/debug-interface-access/idiasegment.md)
- [IDiaEnumInjectedSources](../../debugger/debug-interface-access/idiaenuminjectedsources.md)