---
description: Esse método recupera o valor da variável local especificada como bytes brutos.
title: IDiaStackFrame::get_rawLVarInstanceValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackFrame::get_rawLVarInstanceValue method
ms.assetid: ce526259-85a6-475b-9274-0b3a21d95db2
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: dc7bc12fe8fd38fc02b6794b2026bce328d95511
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102147439"
---
# <a name="idiastackframeget_rawlvarinstancevalue"></a>IDiaStackFrame::get_rawLVarInstanceValue
Esse método recupera o valor da variável local especificada como bytes brutos.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_rawLVarInstanceValue(
   IDiaLVarInstance* pInstance,
   DWORD             cbDataMax,
   DWORD*            pcbData,
   BYTE*             pbData
);
```

#### <a name="parameters"></a>Parâmetros
 `pInstance`

no Um `IDiaLVarInstance` objeto que representa uma instância da variável local para o qual obter o valor.

 `cbDataMax`

no Número máximo de bytes no buffer apontado por `pbData` . Pode ser um máximo de 8 bytes ( `sizeof(ULONGLONG)` ).

 `pcbData`

fora Retorna o número real de bytes armazenados no buffer.

 `pbData`

fora Um buffer a ser preenchido com dados. Esse não pode ser `NULL`.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Confira também
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)
