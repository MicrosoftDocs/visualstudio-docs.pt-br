---
description: Essa interface representa um erro ou um ponto de interrupção de aviso, como um local inválido, uma expressão inválida ou os motivos pelos quais o ponto de interrupção pendente não está associado (o código ainda não foi carregado e assim por diante).
title: IDebugErrorBreakpoint2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugErrorBreakpoint2
helpviewer_keywords:
- IDebugErrorBreakpoint2 interface
ms.assetid: 1f2a4b94-3713-46e9-8272-3917187792bd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9c2ceedbf0fad2141f978420909d31be2260818c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065925"
---
# <a name="idebugerrorbreakpoint2"></a>IDebugErrorBreakpoint2
Essa interface representa um erro ou um ponto de interrupção de aviso, como um local inválido, uma expressão inválida ou os motivos pelos quais o ponto de interrupção pendente não está associado (o código ainda não foi carregado e assim por diante).

## <a name="syntax"></a>Sintaxe

```
IDebugErrorBreakpoint2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Um mecanismo de depuração implementa essa interface como parte de seu suporte para pontos de interrupção. Essa interface é usada para relatar problemas com a associação de um ponto de interrupção.

## <a name="notes-for-callers"></a>Observações para chamadores
 Uma chamada para [GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md) obtém essa interface. Essa interface também pode ser retornada (como parte de uma lista representada por uma interface [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md) ) por uma chamada para [canbind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md) ou [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md).

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IDebugErrorBreakpoint2` .

|Método|Descrição|
|------------|-----------------|
|[GetPendingBreakpoint](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getpendingbreakpoint.md)|Obtém o ponto de interrupção pendente que causou o erro.|
|[GetBreakpointResolution](../../../extensibility/debugger/reference/idebugerrorbreakpoint2-getbreakpointresolution.md)|Obtém a resolução de erro de ponto de interrupção que descreve o erro.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [IDebugBreakpointErrorEvent2](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2.md)
- [GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)
- [IEnumDebugErrorBreakpoints2](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2.md)
- [Próximo](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-next.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpointResolution2](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2.md)
