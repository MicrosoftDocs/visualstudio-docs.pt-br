---
description: Essa interface representa um único quadro de pilha em uma pilha de chamadas em um thread específico.
title: IDebugStackFrame2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2
helpviewer_keywords:
- IDebugStackFrame2 interface
ms.assetid: bd212a6a-dcc6-4756-a77a-e8dfda38b104
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f9675627bf3044258a532ca91768619f2c6de3ba
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053250"
---
# <a name="idebugstackframe2"></a>IDebugStackFrame2
Essa interface representa um único quadro de pilha em uma pilha de chamadas em um thread específico.

## <a name="syntax"></a>Sintaxe

```
IDebugStackFrame2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface para representar um quadro de pilha.

## <a name="notes-for-callers"></a>Observações para chamadores
 Chame [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) para recuperar uma interface [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md) . Chame [Next](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md) para recuperar uma estrutura [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) que contém a `IDebugStackFrame2` interface.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugStackFrame2` .

|Método|Descrição|
|------------|-----------------|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|Obtém o contexto do código para este quadro de pilhas.|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|Obtém o contexto do documento para este quadro de pilhas.|
|[GetName](../../../extensibility/debugger/reference/idebugstackframe2-getname.md)|Obtém o nome do quadro de pilhas.|
|[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)|Obtém uma descrição do quadro de pilhas.|
|[GetPhysicalStackRange](../../../extensibility/debugger/reference/idebugstackframe2-getphysicalstackrange.md)|Obtém uma representação dependente de computador do intervalo de endereços físicos associados a um quadro de pilha.|
|[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)|Obtém um contexto de avaliação para fazer a avaliação de expressão dentro do contexto atual de um quadro de pilha e thread.|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugstackframe2-getlanguageinfo.md)|Obtém o idioma associado a um quadro de pilha.|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)|Obtém uma descrição das propriedades associadas a um registro de ativação.|
|[EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)|Cria um enumerador para propriedades de quadro de pilha.|
|[GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)|Obtém o thread associado a um quadro de pilha.|

## <a name="remarks"></a>Comentários
 Essa interface é obtida somente quando o programa que está sendo depurado foi interrompido em um ponto de interrupção (causado por um ponto de interrupção definido pelo usuário ou uma exceção). A partir dessa interface, um contexto de expressão pode ser obtido para avaliar expressões, uma lista de registros pode ser retornada ou a pilha de chamadas pode ser obtida e examinada.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
