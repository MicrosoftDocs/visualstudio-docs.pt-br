---
description: Representa um modificador opcional de depuração.
title: IDebugModOpt | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugModOpt interface
ms.assetid: ebd525e3-d140-4071-9d8c-41871de4125e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ffb235d58c254d130636da0f4b97961c11f9a372
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087893"
---
# <a name="idebugmodopt"></a>IDebugModOpt
Representa um modificador opcional de depuração.

## <a name="syntax"></a>Sintaxe

```
IDebugModOpt : IUnknown
```

## <a name="notes-for-callers"></a>Observações para chamadores
 Obtido de um objeto [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) que representa uma classe ou um método.

## <a name="methods"></a>Métodos
 Essa interface implementa o seguinte método:

|Método|Descrição|
|------------|-----------------|
|[GetModOpts](../../../extensibility/debugger/reference/idebugmodopt-getmodopts.md)|Recupera uma lista de modificadores opcionais.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: sh. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
