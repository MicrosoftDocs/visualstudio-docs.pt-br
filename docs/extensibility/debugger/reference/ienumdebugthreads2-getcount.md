---
description: Retorna o número de elementos na enumeração de threads.
title: 'IEnumDebugThreads2:: GetCount | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugThreads2::GetCount
helpviewer_keywords:
- IEnumDebugThreads2::GetCount
ms.assetid: 81b7f139-d24e-4040-9adc-d664d77563ba
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: aaa9c670b3f09985edb34f2165f000861c12a31c
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102225845"
---
# <a name="ienumdebugthreads2getcount"></a>IEnumDebugThreads2::GetCount
Retorna o número de elementos na enumeração.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetCount(
   ULONG* pcelt
);
```

```csharp
int GetCount(
   out uint pcelt
);
```

## <a name="parameters"></a>Parâmetros
`pcelt`\
fora Retorna o número de elementos na enumeração.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método não faz parte da interface de enumeração com personalizada que especifica que apenas os `Next` métodos, `Clone` , `Skip` e `Reset` precisam ser implementados.

## <a name="see-also"></a>Confira também
- [IEnumDebugThreads2](../../../extensibility/debugger/reference/ienumdebugthreads2.md)
