---
title: 'IDiaSourceFile:: get_compilands | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_compilands method
ms.assetid: 57deb50a-9c22-43ea-a80c-eab205997bc4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 89b3d85ab967185fb264491f57d6e6b59afad105
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465296"
---
# <a name="idiasourcefileget_compilands"></a>IDiaSourceFile::get_compilands
Recupera um enumerador de compilandos que têm números de linha referenciando este arquivo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_compilands ( 
   IDiaEnumSymbols** ppRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `ppRetVal`

fora Retorna um objeto [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md) que contém uma lista de todos os compilandos que têm números de linha referenciando esse arquivo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
- [IDiaEnumSymbols](../../debugger/debug-interface-access/idiaenumsymbols.md)