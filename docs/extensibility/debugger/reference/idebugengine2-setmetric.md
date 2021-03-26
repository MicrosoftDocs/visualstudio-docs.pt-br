---
description: Esse método define um valor de registro conhecido como uma métrica.
title: 'IDebugEngine2:: SETMETRIC | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine2:::SetMetric
helpviewer_keywords:
- IDebugEngine2:::SetMetric
ms.assetid: dcda4972-c32e-4693-a0e1-25d5c58b9782
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ec947a97506283b6d26f0e4cb26b06afb183dd57
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087880"
---
# <a name="idebugengine2setmetric"></a>IDebugEngine2::SetMetric
Esse método define um valor de registro conhecido como uma métrica.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT SetMetric(
   LPCOLESTR pszMetric,
   VARIANT   varValue
);
```

```csharp
int SetMetric(
   string pszMetric,
   object varValue
);
```

## <a name="parameters"></a>Parâmetros
`pszMetric`\
no O nome da métrica.

`varValue`\
no Especifica o valor da métrica.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Uma métrica é um valor de registro usado para alterar o comportamento de um mecanismo de depuração ou para anunciar a funcionalidade com suporte. Esse método pode encaminhar a chamada para a forma apropriada dos [auxiliares do SDK para a função de depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md) , `SetMetric` .

## <a name="see-also"></a>Confira também
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [Auxiliares do SDK para depuração](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
