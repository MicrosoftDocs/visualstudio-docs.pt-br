---
description: Pesquisa o quadro de ativação especificado em busca de um endereço de retorno no endereço especificado ou próximo dele.
title: IDiaStackWalkFrame::searchForReturnAddressStart | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::searchForReturnAddressStart method
ms.assetid: 47660b9b-6e4f-4dfa-88ab-63dce28f7412
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 49beac1d7f7c998b5ad3a73222903830a934bc9c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158904"
---
# <a name="idiastackwalkframesearchforreturnaddressstart"></a>IDiaStackWalkFrame::searchForReturnAddressStart
Pesquisa o quadro de ativação especificado em busca de um endereço de retorno no endereço especificado ou próximo dele.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT searchForReturnAddressStart ( 
   IDiaFrameData* frame,
   ULONGLONG      startAddress,
   ULONGLONG*     returnAddress
);
```

#### <a name="parameters"></a>Parâmetros
 `frame`

no Um objeto [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) que representa o quadro de pilhas atual.

 `startAddress`

no Um endereço de memória virtual do qual começar a Pesquisar.

 `returnAddress`

fora Retorna o endereço de retorno de função mais próximo para `startAddress` .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)
