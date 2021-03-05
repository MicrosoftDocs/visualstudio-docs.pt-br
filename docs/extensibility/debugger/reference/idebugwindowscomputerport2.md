---
description: Permite consultar informações sobre o computador de destino.
title: IDebugWindowsComputerPort2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugWindowsComputerPort2 interface
ms.assetid: 25f327b8-0303-4268-88d1-74df630436aa
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a9c7e940c2284b5b39097226f9a5b0c3b34a0d18
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102222946"
---
# <a name="idebugwindowscomputerport2"></a>IDebugWindowsComputerPort2
Permite consultar informações sobre o computador de destino.

## <a name="syntax"></a>Sintaxe

```
IDebugWindowsComputerPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada por objetos de porta do Gerenciador de depuração de sessão.

## <a name="methods"></a>Métodos
 A tabela a seguir mostra os métodos de `IDebugWindowsComputerPort2` .

|Método|Descrição|
|------------|-----------------|
|[GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)|Recupera informações sobre o computador no qual o depurador está em execução.|

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
