---
title: 'IDebugProgramNode2:: GetHostMachineName_V7 | Microsoft Docs'
description: Esse é o método antigo, preterido para obter o nome do computador host usado antes do Visual Studio 2005.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNode2::GetHostMachineName
helpviewer_keywords:
- IDebugProgramNode2::GetHostMachineName_V7
- IDebugProgramNode2::GetHostMachineNameIDebugProgramNode2::GetHostMachineName
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 20d62c180848c4875fa3312e0194ebdb467a93ca
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053536"
---
# <a name="idebugprogramnode2gethostmachinename_v7"></a>IDebugProgramNode2::GetHostMachineName_V7

> [!Note]
> Preterido. NÃO USE.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetHostMachineName_V7 (
   BSTR* pbstrHostMachineName
);
```

```csharp
int GetHostMachineName_V7 (
   out string pbstrHostMachineName
);
```

## <a name="parameters"></a>Parâmetros

`pbstrHostMachineName`\
fora Retorna o nome do computador no qual o programa está em execução.

## <a name="return-value"></a>Valor Retornado

Uma implementação sempre deve retornar `E_NOTIMPL` .

## <a name="remarks"></a>Comentários

> [!WARNING]
> A partir do Visual Studio 2005, esse método não é mais usado e sempre deve retornar `E_NOTIMPL` .

## <a name="see-also"></a>Confira também

- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
