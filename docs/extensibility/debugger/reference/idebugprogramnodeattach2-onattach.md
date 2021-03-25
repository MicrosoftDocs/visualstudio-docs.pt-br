---
description: Anexa ao programa associado ou adia o processo de anexação para o método Attach.
title: 'IDebugProgramNodeAttach2:: onattach | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramNodeAttach2::OnAttach
helpviewer_keywords:
- IDebugProgramNodeAttach2::OnAttach
ms.assetid: 5fe52761-a508-4ab5-abdb-334fb6590334
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 334a8e4bdf559e2d39d52a03dcf1a849f73af3e8
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087256"
---
# <a name="idebugprogramnodeattach2onattach"></a>IDebugProgramNodeAttach2::OnAttach
Anexa ao programa associado ou adia o processo de anexação para o método [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) .

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT OnAttach(
   [in] REFGUID guidProgramId
);
```

```csharp
int OnAttach(
   ref Guid guidProgramId
};
```

## <a name="parameters"></a>Parâmetros
`guidProgramId`\
[in] `GUID` para atribuir ao programa associado.

## <a name="return-value"></a>Valor Retornado
 Se for bem-sucedido, retornará `S_OK`. Retorna `S_FALSE` se o método [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) não deve ser chamado. Caso contrário, retornará um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é chamado durante o processo de anexo, antes que o método [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md) seja chamado. O `OnAttach` método pode executar o processo de anexo em si (nesse caso, esse método retorna `S_FALSE` ) ou adiar o processo de anexação para o `IDebugEngine2::Attach` método (o `OnAttach` método retorna `S_OK` ). Em qualquer evento, o `OnAttach` método pode definir o `GUID` do programa que está sendo depurado para o determinado `GUID` .

## <a name="see-also"></a>Confira também
- [IDebugProgramNodeAttach2](../../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [Attach](../../../extensibility/debugger/reference/idebugengine2-attach.md)
