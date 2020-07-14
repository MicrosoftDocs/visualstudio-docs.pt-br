---
title: IDiaStackWalkHelper::put_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkHelper2::put_registerValue method
ms.assetid: 8f02ce54-ef59-455f-8aa6-dc26761c7aff
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d6a2fd6c7fbca54593a547a1f014fbe7726c814c
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464698"
---
# <a name="idiastackwalkhelperput_registervalue"></a>IDiaStackWalkHelper::put_registerValue
Define o valor de um registro.

## <a name="syntax"></a>Sintaxe

```C++
HRESULT put_registerValue ( 
   DWORD     index,
   ULONGLONG NewVal
);
```

#### <a name="parameters"></a>Parâmetros
 `index`

no Um valor da enumeração de [enumeração de CV_HREG_e](../../debugger/debug-interface-access/cv-hreg-e.md) especificando o registro no qual gravar.

 `NewVal`

no O novo valor de registro.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Apesar do tamanho do valor, uma implementação deve armazenar apenas o que o registro normalmente mantém. Por exemplo, um registro de 8 bits manteria apenas os 8 bits mais baixos do valor especificado.

## <a name="see-also"></a>Veja também
- [IDiaStackWalkHelper](../../debugger/debug-interface-access/idiastackwalkhelper.md)
- [Enumeração CV_HREG_e](../../debugger/debug-interface-access/cv-hreg-e.md)