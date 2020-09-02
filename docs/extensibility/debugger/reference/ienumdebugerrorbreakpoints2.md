---
title: IEnumDebugErrorBreakpoints2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugErrorBreakpoints2
helpviewer_keywords:
- IEnumDebugErrorBreakpoints2
ms.assetid: ffdad73d-969a-45ef-9ad1-7f5d3b814018
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ea841a095964b71e301e966bfd0a10c8f7c0c65d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80716888"
---
# <a name="ienumdebugerrorbreakpoints2"></a>IEnumDebugErrorBreakpoints2
Essa interface enumera os pontos de interrupção de erro associados a um ponto de interrupção pendente.

## <a name="syntax"></a>Syntax

```
IEnumDebugErrorBreakpoints2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface como parte de seu suporte para pontos de interrupção.

## <a name="notes-for-callers"></a>Observações para chamadores
 O Visual Studio chama [Unbind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md) para obter essa interface representando uma lista de pontos de interrupção que não podem ser associados, ou [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md) para obter essa interface representando uma lista de pontos de interrupção que não foram associados.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IEnumDebugErrorBreakpoints2` .

|Método|Descrição|
|------------|-----------------|
|[Próximo](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-next.md)|Recupera um número especificado de pontos de interrupção de erro em uma sequência de enumeração.|
|[Ignorar](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-skip.md)|Ignora um número especificado de pontos de interrupção de erro em uma sequência de enumeração.|
|[Redefinir](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-reset.md)|Redefine uma sequência de enumeração para o início.|
|[Clone](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração que o enumerador atual.|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugerrorbreakpoints2-getcount.md)|Obtém o número de pontos de interrupção de erro em um enumerador.|

## <a name="remarks"></a>Comentários
 Essa interface contém uma lista de interfaces [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) , cada uma delas descreve um ponto de interrupção que não pôde ser associado e por que ele não pôde ser associado. O Visual Studio usa a `IEnumDebugErrorBreakpoint2` interface para atualizar os pontos de interrupção mostrados no IDE.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Principais interfaces](../../../extensibility/debugger/reference/core-interfaces.md)
- [CanBind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-canbind.md)
- [EnumErrorBreakpoints](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-enumerrorbreakpoints.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
