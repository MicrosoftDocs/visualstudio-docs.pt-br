---
title: IDiaSession::findInlineeLinesByVA | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: dffe6594-e0d1-4ed5-aeea-8773f88d82a6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0d28c00ea33f0dc07b6785691e9528c4e3b02421
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465709"
---
# <a name="idiasessionfindinlineelinesbyva"></a>IDiaSession::findInlineeLinesByVA
Recupera uma enumeração que permite que um cliente itere pelas informações de número de linha de todas as funções que são embutidas, direta ou indiretamente, pelo símbolo pai especificado e estão contidas no endereço virtual (VA) especificado.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findInlineeLinesByVA ( 
   IDiaSymbol*           parent,   ULONGLONG             va,   DWORD                 length,
   IDiaEnumLineNumbers** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `parent`

no Um `IDiaSymbol` objeto que representa o pai.

 `va`

no Especifica o endereço como um VA.

 `length`

no Especifica o intervalo de endereços, em número de bytes, a ser abordado com essa consulta.

 `ppResult`

fora Mantém um `IDiaEnumLineNumbers` objeto que contém a lista de números de linha recuperados.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)
- [Enumeração SymTagEnum](../../debugger/debug-interface-access/symtagenum.md)
- [IDiaEnumLineNumbers](../../debugger/debug-interface-access/idiaenumlinenumbers.md)