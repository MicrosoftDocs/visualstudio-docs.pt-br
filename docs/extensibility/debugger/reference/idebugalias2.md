---
description: Representa um alias numérico para uma variável e permite que um avaliador de expressão (EE) obtenha o domínio do aplicativo para o alias.
title: IDebugAlias2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugAlias2 interface
ms.assetid: 5252dcbb-8bfe-4d8a-a8e5-b022b194df19
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f383e31f43e1e6422892547d66af533c2f4ab87f
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143851"
---
# <a name="idebugalias2"></a>IDebugAlias2
> [!IMPORTANT]
> No Visual Studio 2015, essa maneira de implementar avaliadores de expressão é preterida. Para obter informações sobre como implementar avaliadores de expressão CLR, consulte os [avaliadores de expressão CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) e [exemplo de avaliador de expressão gerenciada](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample).

 Representa um alias numérico para uma variável e permite que um avaliador de expressão (EE) obtenha o domínio do aplicativo para o alias.

## <a name="syntax"></a>Sintaxe

```
IDebugAlias2 : IDebugAlias
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada pelo mecanismo DE depuração gerenciado (DE).

## <a name="methods"></a>Métodos
 Além dos métodos na interface [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) , essa interface implementa o seguinte método:

|Método|Descrição|
|------------|-----------------|
|[GetAppDomainId](../../../extensibility/debugger/reference/idebugalias2-getappdomainid.md)|Recupera o identificador para o domínio do aplicativo.|

## <a name="remarks"></a>Comentários
 Um alias é um número decimal na forma de cadeia de caracteres seguido pelo caractere #, por exemplo, 1001 #.

## <a name="requirements"></a>Requisitos
 Cabeçalho: EE. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
