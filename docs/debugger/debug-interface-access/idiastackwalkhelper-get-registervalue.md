---
title: IDiaStackWalkHelper::get_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::get_registerValue method
ms.assetid: 46ac5eee-73a3-44a1-8635-6c58ba193cb6
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3fb78b4cbdfa2130731e3847b1a3325ab4cb3eac
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464719"
---
# <a name="idiastackwalkhelperget_registervalue"></a>IDiaStackWalkHelper::get_registerValue
Recupera o valor de um registro.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT get_registerValue ( 
   DWORD      index,
   ULONGLONG* pRetVal
);
```

#### <a name="parameters"></a>Parâmetros
 `index`

no Um valor da enumeração de [enumeração de CV_HREG_e](../../debugger/debug-interface-access/cv-hreg-e.md) especificando para qual registro obter o valor.

 `pRetVal`

fora Retorna o valor atual do registro.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Apesar do tamanho do `pRetVal` parâmetro, uma implementação deve armazenar apenas o que o registro normalmente mantém. Por exemplo, um registro de 8 bits mantém apenas os 8 bits mais baixos do valor especificado. Esse valor de 8 bits é expandido para 64 bits quando retornado desse método.

## <a name="see-also"></a>Veja também
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [Enumeração CV_HREG_e](../../debugger/debug-interface-access/cv-hreg-e.md)