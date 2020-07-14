---
title: IDiaSession::findInlineesByName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: 9860336d-f703-4ecb-bfc4-3f5beb175a76
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cdb35b9c61ddf347ee85553f69536d3757138ebe
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465702"
---
# <a name="idiasessionfindinlineesbyname"></a>IDiaSession::findInlineesByName
Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções embutidas que correspondem a um nome especificado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findInlineesByName ( 
   LPCOLESTR             name,
   DWORD                 option,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `name`

no Especifica o nome a ser usado para comparação.

 `option`

no Especifica as opções de comparação aplicadas à pesquisa de nomes. Os valores da enumeração de [Enumeração NameSearchOptions](../../debugger/debug-interface-access/namesearchoptions.md) podem ser usados sozinhos ou em combinação.

 `ppResult`

fora Retorna um objeto [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) que contém uma lista dos números de linha que foram recuperados.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)