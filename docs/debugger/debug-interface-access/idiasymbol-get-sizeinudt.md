---
title: IDiaSymbol::get_sizeInUdt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
ms.assetid: a82ab896-0185-46a4-b4d5-babfcc660fe1
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ba2f0351997b5f6a2a96cb035871b116b9180786
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461980"
---
# <a name="idiasymbolget_sizeinudt"></a>IDiaSymbol::get_sizeInUdt
Recupera o tamanho de um membro de um tipo definido pelo usuário.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_sizeInUdt(
   DWORD* pRetVal);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Um ponteiro para um `DWORD` que especifica o tamanho do membro.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)