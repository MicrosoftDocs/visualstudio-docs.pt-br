---
description: Essa interface representa um processo em execução e seus programas.
title: IDebugProcess3 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3
helpviewer_keywords:
- IDebugProcess3 interface
ms.assetid: 7bd6b952-cf34-4e66-b8f6-d472dac3748f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d08169b196e01b5e2a7effdfe54829d17a970ef3
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105076505"
---
# <a name="idebugprocess3"></a>IDebugProcess3
Essa interface representa um processo em execução e seus programas. Essa interface existe como uma substituição para vários métodos na interface [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) . Ele fornece controle sobre todos os programas no processo.

> [!NOTE]
> Os métodos [continue](../../../extensibility/debugger/reference/idebugprogram2-continue.md), [Execute](../../../extensibility/debugger/reference/idebugprogram2-execute.md)e [Step](../../../extensibility/debugger/reference/idebugprogram2-step.md) são preteridos e não devem mais ser usados. Em vez disso, use os métodos correspondentes na `IDebugProcess3` interface.

## <a name="syntax"></a>Sintaxe

```
IDebugProcess3 : IDebugProcess2
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada por um fornecedor de porta personalizado para gerenciar programas como um grupo. Quando os programas são gerenciados como um grupo, você pode controlar sua execução e estabelecer um idioma para um avaliador de expressão. Essa interface deve ser implementada pelo fornecedor da porta.

## <a name="notes-for-callers"></a>Observações para chamadores
 Essa interface é chamada principalmente pelo SDM (Gerenciador de depuração de sessão) para interagir com um grupo de programas identificados nesse processo.

 Chame [QueryInterface](/cpp/atl/queryinterface) em uma interface [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md) para obter essa interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos herdados de [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md), `IDebugProcess3` o implementa os métodos a seguir.

|Método|Descrição|
|------------|-----------------|
|[Continuar](../../../extensibility/debugger/reference/idebugprocess3-continue.md)|Continua a execução ou percorrendo um processo.|
|[Executar](../../../extensibility/debugger/reference/idebugprocess3-execute.md)|Inicia a execução de um processo.|
|[Step](../../../extensibility/debugger/reference/idebugprocess3-step.md)|Etapas encaminhar uma instrução ou instrução no processo.|
|[GetDebugReason](../../../extensibility/debugger/reference/idebugprocess3-getdebugreason.md)|Obtém o motivo pelo qual o processo foi iniciado para depuração.|
|[SetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-sethostingprocesslanguage.md)|Define o idioma de hospedagem para que o mecanismo de depuração possa carregar o avaliador de expressão apropriado.|
|[GetHostingProcessLanguage](../../../extensibility/debugger/reference/idebugprocess3-gethostingprocesslanguage.md)|Recupera o idioma definido atualmente para este processo.|
|[DisableENC](../../../extensibility/debugger/reference/idebugprocess3-disableenc.md)|Desabilita a edição e continuação (ENC) para este processo.<br /><br /> Um fornecedor de porta personalizado não implementa esse método (ele sempre deve retornar `E_NOTIMPL` ).|
|[GetENCAvailableState](../../../extensibility/debugger/reference/idebugprocess3-getencavailablestate.md)|Obtenha o estado ENC para esse processo.<br /><br /> Um fornecedor de porta personalizado não implementa esse método (ele sempre deve retornar `E_NOTIMPL` ).|
|[GetEngineFilter](../../../extensibility/debugger/reference/idebugprocess3-getenginefilter.md)|Recupera uma matriz de identificadores exclusivos para os mecanismos de depuração disponíveis.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
