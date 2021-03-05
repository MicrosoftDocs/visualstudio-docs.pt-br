---
description: Essa interface representa a posição inicial de uma instrução de código.
title: IDebugCodeContext2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCodeContext2
helpviewer_keywords:
- IDebugCodeContext2 interface
ms.assetid: 3670439e-2171-405d-9d77-dedb0f1cba93
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 228b6e84ca2f85803c4a248b966698b822bb572f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102164091"
---
# <a name="idebugcodecontext2"></a>IDebugCodeContext2
Essa interface representa a posição inicial de uma instrução de código. Para a maioria das arquiteturas de tempo de execução hoje, um contexto de código pode ser considerado como um endereço no fluxo de execução de um programa.

## <a name="syntax"></a>Sintaxe

```
IDebugCodeContext2 : IDebugMemoryContext2
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração implementa essa interface para relacionar a posição de uma instrução de código a uma posição de documento.

## <a name="notes-for-callers"></a>Observações para chamadores
 Os métodos em várias interfaces retornam essa interface, geralmente, [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md). Ele também é amplamente usado com a interface [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md) , bem como informações de resolução de ponto de interrupção.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 Além dos métodos na interface [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) , essa interface implementa os seguintes métodos:

|Método|Descrição|
|------------|-----------------|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugcodecontext2-getdocumentcontext.md)|Obtém o contexto do documento que corresponde ao contexto do código ativo.|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugcodecontext2-getlanguageinfo.md)|Obtém as informações de idioma para este contexto de código.|

## <a name="remarks"></a>Comentários
 A principal diferença entre uma `IDebugCodeContext2` interface e uma interface [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) é que uma `IDebugCodeContext2` é sempre alinhada com a instrução. Isso significa que um `IDebugCodeContext2` está sempre apontando para o início de uma instrução, enquanto um `IDebugMemoryContext2` pode apontar para qualquer byte de memória na arquitetura de tempo de execução. `IDebugCodeContext2` é incrementado por instruções em vez de pelo tamanho de armazenamento básico (normalmente byte).

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [GetDisassemblyStream](../../../extensibility/debugger/reference/idebugprogram2-getdisassemblystream.md)
- [CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)
- [SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)
- [Próximo](../../../extensibility/debugger/reference/ienumdebugcodecontexts2-next.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
