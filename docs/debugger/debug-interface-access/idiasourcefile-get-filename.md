---
title: IDiaSourceFile::get_fileName | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- IDiaSourceFile::get_fileName method
ms.assetid: a5cb8927-23c6-469e-8f78-f2787d85dba4
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e6f57454be3690f36cbf1addddb3d51bb01a39f2
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62838344"
---
# <a name="idiasourcefilegetfilename"></a>IDiaSourceFile::get_fileName
Recupera o nome do arquivo de origem.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_fileName ( 
   BSTR* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

[out] Retorna o nome do arquivo de origem.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Consulte também
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)