---
title: IDebugProperty2::GetReference | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProperty2::GetReference
helpviewer_keywords:
- IDebugProperty2::GetReference method
ms.assetid: 2fa97d9b-c3d7-478e-ba5a-a933f40a0103
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9248ad59a564207befb0b0a3ff1c229840ee336b
ms.sourcegitcommit: 50f0c3f2763a05de8482b3579026d9c76c0e226c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65457724"
---
# <a name="idebugproperty2getreference"></a>IDebugProperty2::GetReference
Retorna uma referência para o valor da propriedade.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT GetReference(
   IDebugReference2** ppReference
);
```

```csharp
int GetReference(
   out IDebugReference2 ppReference
);
```

## <a name="parameters"></a>Parâmetros
 `ppRererence`\

 [out] Retorna um [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) objeto que representa uma referência para o valor da propriedade.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retornará `S_OK`; caso contrário, retorna um código de erro, geralmente `E_NOTIMPL` ou `E_GETREFERENCE_NO_REFERENCE`.

## <a name="see-also"></a>Consulte também
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)