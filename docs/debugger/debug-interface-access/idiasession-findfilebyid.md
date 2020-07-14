---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1893a361ab4043ad5969a7fa899c07fe18253b9a
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85465828"
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

## <a name="see-also"></a>Veja também
- [IDiaSession](../../debugger/debug-interface-access/idiasession.md)
- [IDiaSession::findFile](../../debugger/debug-interface-access/idiasession-findfile.md)
- [IDiaSourceFile](../../debugger/debug-interface-access/idiasourcefile.md)