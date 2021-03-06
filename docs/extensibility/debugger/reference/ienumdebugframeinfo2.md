---
description: Essa interface enumera as estruturas FRAMEINFO.
title: IEnumDebugFrameInfo2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2
helpviewer_keywords:
- IEnumDebugFrameInfo2
ms.assetid: 994e30ad-435a-4f9e-9272-d96d9e01099c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c347b7cebd9b1417cd0a8e772cd8a247e975ea97
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102226378"
---
# <a name="ienumdebugframeinfo2"></a>IEnumDebugFrameInfo2
Essa interface enumera as estruturas [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) .

## <a name="syntax"></a>Sintaxe

```
IEnumDebugFrameInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 O mecanismo de depuração (DE) implementa essa interface para fornecer uma lista de estruturas que descreve a pilha de chamadas atual.

## <a name="notes-for-callers"></a>Observações para chamadores
 O Visual Studio chama [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) para obter essa interface sempre que um ponto de interrupção, uma exceção ou uma parada ocorre em um programa que está sendo depurado.

## <a name="methods-in-vtable-order"></a>Métodos em ordem vtable
 A tabela a seguir mostra os métodos de `IEnumDebugFrameInfo2` .

|Método|Descrição|
|------------|-----------------|
|[Próximo](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)|Recupera um número especificado de estruturas [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) em uma sequência de enumeração.|
|[Skip](../../../extensibility/debugger/reference/ienumdebugframeinfo2-skip.md)|Ignora um número especificado de estruturas [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) em uma sequência de enumeração.|
|[Redefinir](../../../extensibility/debugger/reference/ienumdebugframeinfo2-reset.md)|Redefine uma sequência de enumeração para o início.|
|[8i](../../../extensibility/debugger/reference/ienumdebugframeinfo2-clone.md)|Cria um enumerador que contém o mesmo estado de enumeração que o enumerador atual.|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)|Obtém o número de estruturas [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) em um enumerador.|

## <a name="remarks"></a>Comentários
 O Visual Studio obtém essa interface como a primeira etapa para manipular um ponto de interrupção, uma exceção ou uma pausa gerada pelo usuário no programa que está sendo depurado. A lista de estruturas [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md) representa a pilha de chamadas atual, com a chamada de função atual no início da lista e a chamada de função mais antiga no final da lista. Cada `FRAMEINFO` um representa um registro de ativação, um contexto no qual as expressões podem ser avaliadas e as variáveis locais são examinadas.

## <a name="requirements"></a>Requisitos
 Cabeçalho: msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>Confira também
- [Interfaces principais](../../../extensibility/debugger/reference/core-interfaces.md)
- [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
