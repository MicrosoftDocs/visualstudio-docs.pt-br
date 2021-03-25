---
description: Sinaliza a IU do depurador do Visual Studio para avisar ao usuário que não foi possível localizar os símbolos para o executável iniciado.
title: IDebugNoSymbolsEvent2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugNoSymbolsEvent2 interface
ms.assetid: f6fb6388-47f6-4385-9ad5-95d62f9a7592
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7a060436575d51710fcef9c444ac843aa56195d0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058398"
---
# <a name="idebugnosymbolsevent2"></a>IDebugNoSymbolsEvent2
Sinaliza a interface de usuário do [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] depurador para avisar ao usuário que não foi possível localizar os símbolos para o executável iniciado.

## <a name="syntax"></a>Sintaxe

```
IDebugNoSymbolsEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Implementado por mecanismos de depuração e consumido pela [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] interface do usuário do depurador.

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
