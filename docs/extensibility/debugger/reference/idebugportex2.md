---
description: Essa interface permite que o SDM (Gerenciador de depuração de sessão) controle os programas e processos em execução em uma porta.
title: IDebugPortEx2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortEx2
helpviewer_keywords:
- IDebugPortEx2 interface
ms.assetid: 144724d0-38ee-4c9b-87ca-8a504371182b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 54da202e6bbaf08216b921afbde2e39f1da3a788
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102142785"
---
# <a name="idebugportex2"></a>IDebugPortEx2
Essa interface permite que o SDM (Gerenciador de depuração de sessão) controle os programas e processos em execução em uma porta.

## <a name="syntax"></a>Sintaxe

```
IDebugPortEx2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um fornecedor de porta personalizado implementa essa interface no mesmo objeto que implementa [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md).

## <a name="notes-for-callers"></a>Observações para chamadores
 O SDM chama [QueryInterface](/cpp/atl/queryinterface) na `IDebugPort2` interface para obter essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugPortEx2` .

|Método|Descrição|
|------------|-----------------|
|[LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md)|Inicia um arquivo executável.|
|[ResumeProcess](../../../extensibility/debugger/reference/idebugportex2-resumeprocess.md)|Retoma a execução de um processo.|
|[CanTerminateProcess](../../../extensibility/debugger/reference/idebugportex2-canterminateprocess.md)|Determina se um processo pode ser encerrado.|
|[TerminateProcess](../../../extensibility/debugger/reference/idebugportex2-terminateprocess.md)|Finaliza um processo.|
|[GetPortProcessId](../../../extensibility/debugger/reference/idebugportex2-getportprocessid.md)|Obtém a ID do processo da porta em si.|
|[GetProgram](../../../extensibility/debugger/reference/idebugportex2-getprogram.md)|Obtém um programa associado a um nó de programa.|

## <a name="remarks"></a>Comentários
 Essa interface normalmente é privada entre o SDM e o fornecedor de porta personalizada.

 Se desejado, um mecanismo de depuração (DE) pode procurar essa interface na interface [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md) passada para [LaunchSuspended](../../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md) e usar [LaunchSuspended](../../../extensibility/debugger/reference/idebugportex2-launchsuspended.md) para iniciar o programa. Isso não é um requisito, no entanto, e um DE pode fazer o que for necessário para iniciar o programa de solicitação.

## <a name="requirements"></a>Requisitos
 Cabeçalho: portpriv. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugPort2](../../../extensibility/debugger/reference/idebugport2.md)
