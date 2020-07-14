---
title: IDiaSession::findAcceleratorInlineesByName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: e203e5c2-6563-43fa-be56-3063955043ab
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: abd6f8afb7275503fa3de855575e9dcb6dad0fb3
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465842"
---
# <a name="idiasessionfindacceleratorinlineesbyname"></a>IDiaSession::findAcceleratorInlineesByName
Retorna uma enumeração de símbolos para quadros embutidos correspondentes ao nome da função embutida especificada.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findAcceleratorInlineeLinesByName ( 
   LPCOLESTR             name,
   DWORD                 option,
   IDiaEnumSymbols**     ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `name`

no O nome da função embutida a ser pesquisada.

 `option`

no As opções de pesquisa de nome a serem usadas durante a pesquisa de quadros embutidos que correspondem a `name` . Para obter mais informações, consulte [Enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md).

 `ppResult`

fora Um ponteiro para um `IDiaEnumSymbols` ponteiro de interface que é inicializado com o resultado.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Essa função procura Inlines apenas nas funções de stub do acelerador. Ele ignora os registros de procedimento C++ nativos.

## <a name="see-also"></a>Veja também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)