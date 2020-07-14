---
title: IDiaTable::get__NewEnum | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaTable::get__NewEnum method
ms.assetid: ee89bba8-5d5c-4a0b-aa0d-1aad56baa380
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 00586a85312b90a7cb6590adb3cdd41b465411d7
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85461311"
---
# <a name="idiatableget__newenum"></a>IDiaTable::get__NewEnum
Recupera a <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> versão deste enumerador.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get__NewEnum ( 
   IUnknown** pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `pRetVal`

fora Retorna a `IUnknown` interface que representa a <xref:System.Runtime.InteropServices.ComTypes.IEnumVARIANT> versão deste enumerador.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="see-also"></a>Veja também
- [IDiaTable](../../debugger/debug-interface-access/idiatable.md)