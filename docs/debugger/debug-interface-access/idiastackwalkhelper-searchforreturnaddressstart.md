---
title: IDiaStackWalkHelper::searchForReturnAddressStart | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper::searchForReturnAddressStart method
ms.assetid: 0a33142e-5d31-44ea-874a-a2e94d95cbd2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 68fbecf9dd085ec229f42a5af12b48d1a712ee1f
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464677"
---
# <a name="idiastackwalkhelpersearchforreturnaddressstart"></a>IDiaStackWalkHelper::searchForReturnAddressStart
Pesquisa o quadro de ativação especificado em busca de um endereço de retorno no endereço de pilha especificado ou próximo dele.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT searchForReturnAddressStart( 
   IDiaFrameData*  frame,
   ULONGLONG       startAddress,
   ULONGLONG*      returnAddress
);
```

#### <a name="parameters"></a>Parâmetros
 `frame`

no Um objeto [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md) que representa o quadro de pilhas atual.

 `startAddress`

no Um endereço de memória virtual do qual começar a Pesquisar.

 `ReturnAddress`

fora Retorna o endereço de retorno de função mais próximo para `startAddress` .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [IDiaFrameData](../../debugger/debug-interface-access/idiaframedata.md)