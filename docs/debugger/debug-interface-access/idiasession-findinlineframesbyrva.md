---
title: IDiaSession::findInlineFramesByRVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: ddb3ff0e-cb3d-4fa0-af56-f064b218b264
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8be9203b3ed22093863710eb7689b16226988efe
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465688"
---
# <a name="idiasessionfindinlineframesbyrva"></a>IDiaSession::findInlineFramesByRVA
Recupera uma enumeração que permite que um cliente Itere em todos os quadros embutidos em um endereço virtual relativo (RVA) específico.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findInlineFramesByRVA ( 
   IDiaSymbol*       parent,   DWORD             rva,
   IDiaEnumSymbols** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `parent`

no Um `IDiaSymbol` objeto que representa o pai.

 `rva`

no Especifica o endereço como um RVA.

 `ppResult`

fora Mantém um `IDiaEnumSymbols` objeto que contém a lista de quadros recuperados.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)