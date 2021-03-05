---
description: Usado por um mecanismo DE depuração (DE) para iniciar e encerrar programas.
title: IDebugEngineLaunch2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineLaunch2
helpviewer_keywords:
- IDebugEngineLaunch2 interface
ms.assetid: 5eaf2ad8-3fbf-446e-b48b-5327ad3f5255
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f03b4754d1648dc8a184d59e5e8b0f038a000bf2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153463"
---
# <a name="idebugenginelaunch2"></a>IDebugEngineLaunch2
Usado por um mecanismo DE depuração (DE) para iniciar e encerrar programas.

## <a name="syntax"></a>Sintaxe

```
IDebugEngineLaunch2 : IDebugEngine2
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada por um personalizado DE se tiver requisitos especiais para iniciar um processo que não pode ser manipulado inteiramente por uma porta personalizada. Normalmente, esse é o caso quando o DE faz parte de um intérprete e o processo que está sendo depurado é um script: o intérprete precisa ser iniciado primeiro e, em seguida, o script é carregado e iniciado. Uma porta pode iniciar o intérprete, mas o script pode exigir tratamento especial (que é onde o DE tem uma função). Essa interface é implementada somente se houver requisitos exclusivos para iniciar um programa que uma porta personalizada não possa manipular.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é chamada pelo SDM (Gerenciador de depuração de sessão) se o SDM puder obter essa interface da interface [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) (usando QueryInterface). Se essa interface puder ser obtida, o SDM saberá que o DE tem requisitos especiais e chamará essa interface para iniciar o programa, em vez de fazer com que a porta o inicialize.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugEngineLaunch2` .

|Método|Descrição|
|------------|-----------------|
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)|Inicia um processo por meio do de.|
|[ResumeProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-resumeprocess.md)|Retoma a execução do processo.|
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-canterminateprocess.md)|Determina se um processo pode ser encerrado.|
|[TerminateProcess](../../../extensibility/debugger/reference/idebugenginelaunch2-terminateprocess.md)|Finaliza um processo.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
