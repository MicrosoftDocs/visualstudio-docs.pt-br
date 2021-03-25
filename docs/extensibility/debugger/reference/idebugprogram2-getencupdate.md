---
description: Esse método obtém a atualização do ENC (editar e continuar) para este programa.
title: 'IDebugProgram2:: GetENCUpdate | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetENCUpdate
helpviewer_keywords:
- IDebugProgram2::GetENCUpdate
ms.assetid: 9832aac8-6320-4fd8-91dd-2a0852febb00
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6d6b60c8b17a8db1420222a7242164ce1c0eedd1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105075920"
---
# <a name="idebugprogram2getencupdate"></a>IDebugProgram2::GetENCUpdate
Esse método obtém a atualização do ENC (editar e continuar) para este programa. Um mecanismo de depuração personalizado sempre retorna `E_NOTIMPL` .

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetENCUpdate( 
   IUnknown** ppUpdate
);
```

```csharp
int GetENCUpdate(
   out object ppUpdate
);
```

## <a name="parameters"></a>Parâmetros
`ppUpdate`\
fora Retorna uma interface interna que pode ser usada para atualizar este programa.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

> [!NOTE]
> Um mecanismo de depuração personalizado sempre deve retornar `E_NOTIMPL` .

## <a name="see-also"></a>Confira também
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
