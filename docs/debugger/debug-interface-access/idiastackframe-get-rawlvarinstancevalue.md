---
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5a45568ea62a767d06a33c324f0f05a1f697e93f
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464978"
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

## <a name="see-also"></a>Veja também
- [IDiaStackFrame](../../debugger/debug-interface-access/idiastackframe.md)