---
title: IDiaSymbol::get_virtualTableShapeId | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaSymbol::get_virtualTableShapeId method
ms.assetid: cbee9944-817a-4805-9c08-fac8e0da58b7
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e46a9188e4189359118eaf1ea4891c903c1f47a8
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461381"
---
# <a name="idiasymbolget_virtualtableshapeid"></a>IDiaSymbol::get_virtualTableShapeId
Recupera o identificador de símbolo de forma da tabela virtual do símbolo.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_virtualTableShapeId ( 
   DWORD* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna a ID do símbolo da forma da tabela virtual do símbolo.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna `S_FALSE` ou um código de erro.

> [!NOTE]
> Um valor de retorno `S_FALSE` significa que a propriedade não está disponível para o símbolo.

## <a name="remarks"></a>Comentários
 O identificador é um valor exclusivo criado pelo DIA SDK para marcar todos os símbolos como exclusivos.

## <a name="see-also"></a>Veja também
- [IDiaSymbol](../../debugger/debug-interface-access/idiasymbol.md)