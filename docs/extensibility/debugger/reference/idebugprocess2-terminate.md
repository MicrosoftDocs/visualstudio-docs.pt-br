---
description: Encerra o processo.
title: 'IDebugProcess2:: Terminate | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Terminate
helpviewer_keywords:
- IDebugProcess2::Terminate
ms.assetid: 5e6bf373-0fe9-4321-b04a-473a65f664d9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9e26a4486e9c97638d20f9c634b66183824c2b39
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081640"
---
# <a name="idebugprocess2terminate"></a>IDebugProcess2::Terminate
Encerra o processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT Terminate( 
   void 
);
```

```csharp
int Terminate();
```

## <a name="return-value"></a>Valor retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Quando um processo é encerrado, todos os programas dentro desse processo são encerrados; nenhum tem permissão para executar qualquer outro código.

## <a name="see-also"></a>Confira também
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
