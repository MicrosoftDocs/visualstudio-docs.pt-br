---
description: Obtém o GUID para este processo.
title: 'IDebugProcess2:: getprocessid | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::GetProcessId
helpviewer_keywords:
- IDebugProcess2::GetProcessId
ms.assetid: d5b6f03c-d49d-4b83-b072-016ac3124f5f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0b42b6f029ee6bbffdb1c59c55a2781d87d450d9
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081744"
---
# <a name="idebugprocess2getprocessid"></a>IDebugProcess2::GetProcessId
Obtém o GUID para este processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetProcessId(
   GUID* pguidProcessId
);
```

```csharp
int GetProcessId(
   out Guid pguidProcessId
);
```

## <a name="parameters"></a>Parâmetros
`pguidProcessId`\
fora Retorna o GUID deste processo.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 O GUID (identificador global exclusivo) identifica esse processo de todos os outros processos em execução no sistema.

## <a name="see-also"></a>Confira também
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
