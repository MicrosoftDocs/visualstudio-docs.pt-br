---
description: Recupera um arquivo de origem por identificador de arquivo de origem.
title: IDiaSession::findFileById | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSession::findFileById method
ms.assetid: 710efe04-78b5-4f3e-a1d8-f9b069063503
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1bf868f91d0eb8d1c80382632be40f348889ab12
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147852"
---
# <a name="idiasessionfindfilebyid"></a>IDiaSession::findFileById
Recupera um arquivo de origem por identificador de arquivo de origem.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT findFileById ( 
   DWORD            uniqueId,
   IDiaSourceFile** ppResult
);
```

#### <a name="parameters"></a>Parâmetros
 `uniqueId`

no Especifica o identificador do arquivo de origem.

 `ppResult`

fora Retorna um objeto [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md) que representa o arquivo de origem recuperado.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O identificador do arquivo de origem é um valor exclusivo usado internamente para a DIA SDK para tornar todos os arquivos de origem exclusivos. Normalmente, esse método é usado internamente para a DIA SDK.

## <a name="see-also"></a>Confira também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)
