---
title: IDiaSession::findInlineeLinesByLinenum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
ms.assetid: cf32ae7c-a0c8-4800-bc8f-d64fdd15fb06
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: fe238f3bc66d6a7c5978c5d7cbebcd185fcd43d2
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2019
ms.locfileid: "72742220"
---
# <a name="idiasessionfindinlineelinesbylinenum"></a>IDiaSession::findInlineeLinesByLinenum
Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, no arquivo de origem e no número de linha especificados.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findInlineeLinesByVA ( 
   IDiaSymbol*           compiland,
   IDiaSourceFile*       file,
   DWORD                 linenum,
   DWORD                 column,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `compiland`

no Um objeto [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md) que representa o compiland no qual Pesquisar os números de linha. O parâmetro não pode ser `NULL`.

 `file`

no Um objeto [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) que representa o arquivo de origem no qual Pesquisar. O parâmetro não pode ser `NULL`.

 `linenum`

no Especifica um número de linha baseado em um.

> [!NOTE]
> Não é possível usar zero para especificar todas as linhas (use o método [IDiaSession:: findLines](../../debugger/debug-interface-access/idiasession-findlines.md) para localizar todas as linhas).

 `column`

no Especifica o número da coluna. Use zero para especificar todas as colunas. Uma coluna é um deslocamento de byte em uma linha.

 `ppResult`

fora Retorna um objeto [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md) que contém uma lista dos números de linha que foram recuperados.

## <a name="return-value"></a>Valor retornado
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Consulte também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)