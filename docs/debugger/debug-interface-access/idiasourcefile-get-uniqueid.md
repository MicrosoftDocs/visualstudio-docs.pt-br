---
description: Recupera um valor de chave de inteiro simples que é exclusivo para esta imagem.
title: IDiaSourceFile::get_uniqueId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_uniqueId method
ms.assetid: e0b8dbc0-6061-4f31-bead-2cd72be44e41
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0595e20518db1e977a75384c7aec3d1b8cef7716
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147572"
---
# <a name="idiasourcefileget_uniqueid"></a>IDiaSourceFile::get_uniqueId
Recupera um valor de chave de inteiro simples que é exclusivo para esta imagem.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_uniqueId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna um valor de chave de inteiro simples que é exclusivo para esta imagem.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Comparar chaves em vez de cadeias de caracteres pode acelerar o processamento de números de linha.

## <a name="see-also"></a>Confira também
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
