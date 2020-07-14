---
title: IDiaStackWalkFrame::p ut_registerValue | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
dev_langs:
- C++
helpviewer_keywords:
- IDiaStackWalkFrame::put_registerValue method
ms.assetid: 2d8b79b6-7240-43fe-b24e-e4ff3e2c15b0
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 39fc87a6120768eaf1251d81512cbb19f025b7f3
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85464831"
---
# <a name="idiastackwalkframeput_registervalue"></a>IDiaStackWalkFrame::put_registerValue
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

## <a name="see-also"></a>Veja também
- [IDiaStackWalkFrame](../../debugger/debug-interface-access/idiastackwalkframe.md)
- [Enumeração CV_HREG_e](../../debugger/debug-interface-access/cv-hreg-e.md)