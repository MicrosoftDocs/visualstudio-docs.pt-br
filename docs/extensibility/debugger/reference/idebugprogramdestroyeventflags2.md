---
description: Permite que um mecanismo de depuração substitua o comportamento padrão da interface do usuário do Visual Studio quando você encerra uma sessão de depuração.
title: IDebugProgramDestroyEventFlags2 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgramDestroyEventFlags2 interface
ms.assetid: d384ff71-dc71-40b9-a871-801f8b6a3418
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 02b2d934c2a556d3556d494368145e52a8c97394
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168186"
---
# <a name="idebugprogramdestroyeventflags2"></a>IDebugProgramDestroyEventFlags2
Permite que um mecanismo de depuração substitua o comportamento padrão da [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] interface do usuário quando você finaliza uma sessão de depuração.

## <a name="syntax"></a>Sintaxe

```
IDebugProgramDestroyEventFlags2 : IUnknown
```

## <a name="notes-for-implementers"></a>Notas para implementadores
 Essa interface é implementada pelos mecanismos de depuração. É útil para hosts que podem criar e destruir vários programas durante o tempo de vida de um processo.

## <a name="methods"></a>Métodos
 A tabela a seguir mostra os métodos de `IDebugProgramDestroyEventFlags2` .

|Método|Descrição|
|------------|-----------------|
|[GetFlags](../../../extensibility/debugger/reference/idebugprogramdestroyeventflags2-getflags.md)|Recupera os sinalizadores de destruição do programa.|

## <a name="remarks"></a>Comentários
 O comportamento padrão da [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] interface do usuário é voltar para o modo de design depois que todos os programas tiverem enviado um evento de destruição de programa. Essa interface permite que um mecanismo de depuração altere esse comportamento.

## <a name="requirements"></a>Requisitos
 Cabeçalho: Msdbg. h

 Namespace: Microsoft. VisualStudio. Debugger. Interop

 Assembly: Microsoft.VisualStudio.Debugger.Interop.dll
