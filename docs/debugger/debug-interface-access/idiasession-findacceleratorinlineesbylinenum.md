---
description: Retorna uma enumeração de símbolos para quadros embutidos que correspondem ao local de origem especificado.
title: IDiaSession::findAcceleratorInlineesByLinenum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 386c87aa-f7b2-4d38-9dd6-fffba9ff01f0
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4ddb65e5041f19ad854eec271b22f3cbcab5a97c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147860"
---
# <a name="idiasessionfindacceleratorinlineesbylinenum"></a>IDiaSession::findAcceleratorInlineesByLinenum
Retorna uma enumeração de símbolos para quadros embutidos que correspondem ao local de origem especificado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findAcceleratorInlineeLinesByName ( 
   IDiaSymbol*           parent,
   IDiaSourceFile*       file,
   DWORD                 linenum,
   DWORD                 colnum,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `parent`

no Um `IDiaSymbol` que corresponde à função de stub do acelerador que precisa ser pesquisada.

 `file`

no O `IDiaSourceFile` do local de origem.

 `linenum`

no O número de linha do local de origem.

 `colnum`

no O número da coluna do local de origem.

 `ppResult`

fora Um ponteiro para um `IDiaEnumLineNumbers` ponteiro de interface que é inicializado com o resultado.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
