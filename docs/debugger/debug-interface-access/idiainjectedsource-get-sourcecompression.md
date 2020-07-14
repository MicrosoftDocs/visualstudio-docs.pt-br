---
title: IDiaInjectedSource::get_sourceCompression | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaInjectedSource::get_sourceCompression method
ms.assetid: 854b142f-23a9-466c-bf7f-98e581d5abcd
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e32450e355d757081efaf66e7c5abaf179e7fd95
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85467018"
---
# <a name="idiainjectedsourceget_sourcecompression"></a>IDiaInjectedSource::get_sourceCompression
Recupera o indicador da compactação de origem usada.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_sourceCompression ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna o indicador da compactação de origem usada. Um valor de zero indica que nenhuma compactação de origem foi usada.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se não há suporte para essa propriedade. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 O valor retornado por esse método é específico para o compilador usado. Por exemplo, um compilador pode usar a codificação de comprimento de execução ou a compactação estilo Huffman.

## <a name="see-also"></a>Veja também
- [IDiaInjectedSource](../../debugger/debug-interface-access/idiainjectedsource.md)