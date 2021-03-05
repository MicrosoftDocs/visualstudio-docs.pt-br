---
description: Esse método adiciona um nó de programa para cada mecanismo de depuração especificado.
title: 'IDebugProcessEx2:: AddImplicitProgramNodes | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes
helpviewer_keywords:
- IDebugProcessEx2::AddImplicitProgramNodes method
ms.assetid: 8b491b00-f9e7-45b3-9115-fe58c3464289
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e3a4c6446c2106d79dd14fc0378fc848eac3df18
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102159985"
---
# <a name="idebugprocessex2addimplicitprogramnodes"></a>IDebugProcessEx2::AddImplicitProgramNodes
Esse método adiciona um nó de programa para cada mecanismo de depuração especificado.

## <a name="syntax"></a>Sintaxe

```cpp
HRESULT AddImplicitProgramNodes(
   REFGUID guidLaunchingEngine,
   GUID*   rgguidSpecificEngines,
   DWORD   celtSpecificEngines
);
```

```csharp
int AddImplicitProgramNodes(
   ref Guid guidLaunchingEngine,
   Guid[]   rgguidSpecificEngines,
   uint     celtSpecificEngines
);
```

## <a name="parameters"></a>Parâmetros
`guidLaunchingEngine`\
no O `GUID` de a é usado para iniciar programas (e é considerado para adicionar seus próprios nós de programa).

`rgguidSpecificEngines`\
no Matriz de `GUID` s de des para a qual os nós de programa serão adicionados.

`celtSpecificEngines`\
no O número de `GUID` s na `rgguidSpecificEngines` matriz.

## <a name="return-value"></a>Valor Retornado
 Se bem-sucedido, retorna `S_OK` ; caso contrário, retorna um código de erro.

## <a name="remarks"></a>Comentários
- [Nós de programa](../../../extensibility/debugger/program-nodes.md) serão adicionados para cada um dos listados em `rgguidSpecificEngines` — excluindo o mecanismo de inicialização (como fornecido em `guidLaunchingEngine` ), que é considerado para adicionar seu próprio nó de programa quando ele inicia um programa.

## <a name="see-also"></a>Confira também
- [IDebugProgramEx2](../../../extensibility/debugger/reference/idebugprogramex2.md)
- [Nós de programa](../../../extensibility/debugger/program-nodes.md)
