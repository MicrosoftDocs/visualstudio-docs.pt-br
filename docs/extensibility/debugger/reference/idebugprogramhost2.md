---
description: Essa interface fornece informações de host (processo) sobre um programa.
title: IDebugProgramHost2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2
helpviewer_keywords:
- IDebugProgramHost2 interface
ms.assetid: 2c37b3aa-97a9-4665-8709-edd917f18cb1
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 109cca0cc3d12d8bf14da848774042fe346f0f1e
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168108"
---
# <a name="idebugprogramhost2"></a>IDebugProgramHost2
Essa interface fornece informações de host (processo) sobre um programa.

## <a name="syntax"></a>Sintaxe

```
IDebugProgramHost2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração implementa essa interface no mesmo objeto que a interface [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) para fornecer informações sobre o processo de hospedagem. Essa é uma interface opcional.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [QueryInterface](/cpp/atl/queryinterface) em uma `IDebugProgram2` interface para obter essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugProgramHost2` .

|Método|Descrição|
|------------|-----------------|
|[GetHostName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostname.md)|Obtém o título, nome amigável ou nome de arquivo do processo de hospedagem deste programa.|
|[GetHostId](../../../extensibility/debugger/reference/idebugprogramhost2-gethostid.md)|Obtém o identificador do processo de hospedagem deste programa.|
|[GetHostMachineName](../../../extensibility/debugger/reference/idebugprogramhost2-gethostmachinename.md)|Obtém o nome do computador no qual o processo de hospedagem deste programa está sendo executado.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
