---
description: Esse método desabilita explicitamente editar e continuar neste processo (e todos os programas que ele contém).
title: IDebugProcess3::D isableENC | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::DisableENC
helpviewer_keywords:
- IDebugProcess3::DisableENC
ms.assetid: cffdbdac-4d76-4aeb-aa55-5d0410db99f1
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7f9c4a1e05cf7d4a98489daf0c2ee3377d54f417
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081614"
---
# <a name="idebugprocess3disableenc"></a>IDebugProcess3::DisableENC
Esse método desabilita explicitamente editar e continuar neste processo (e todos os programas que ele contém). Um fornecedor de porta personalizada sempre deve retornar `E_NOTIMPL` .

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT DisableENC(
   EncUnavailableReason reason
);
```

```csharp
   EncUnavailableReason reason
);
```

## <a name="parameters"></a>Parâmetros
`reason`\
no Um valor da enumeração [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md) .

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna o código de erro.

> [!NOTE]
> Um fornecedor de porta personalizada sempre deve retornar `E_NOTIMPL` .

## <a name="remarks"></a>Comentários
 Depois que editar e continuar estiver desabilitado para um processo, ele poderá ser habilitado novamente apenas reiniciando o processo.

## <a name="see-also"></a>Confira também
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)
