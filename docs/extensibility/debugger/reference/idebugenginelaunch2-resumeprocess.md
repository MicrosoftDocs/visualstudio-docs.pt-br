---
title: 'IDebugEngineLaunch2:: ResumeProcess | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2::ResumeProcess
helpviewer_keywords:
- IDebugEngineLaunch2::ResumeProcess
ms.assetid: 61ccc14e-75c6-44e7-aae4-57a9aac52089
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1cfd5e6c09c86a4c12c9fc8bbc3d0212887af279
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892808"
---
# <a name="idebugenginelaunch2resumeprocess"></a>IDebugEngineLaunch2::ResumeProcess
Retoma a execução do processo.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT ResumeProcess ( 
   IDebugProcess2* pProcess
);
```

```csharp
int ResumeProcess ( 
   IDebugProcess2 pProcess
);
```

## <a name="parameters"></a>Parâmetros
`pProcess`\
no Um objeto [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) que representa o processo a ser retomado.

## <a name="return-value"></a>Valor de retorno
 Se for bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
 Esse método é chamado depois que um processo é iniciado com uma chamada para o método [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) .

## <a name="see-also"></a>Confira também
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
