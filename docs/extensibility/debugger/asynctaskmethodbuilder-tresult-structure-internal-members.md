---
description: Este tópico descreve os membros internos da classe System. Runtime. CompilerServices. AsyncTaskMethodBuilder.
title: '&lt; &gt; Estrutura de TResult AsyncTaskMethodBuilder-membros internos | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- AsyncTaskMethodBuilder<TResult> structure [.NET Framework debug engines]
- debug engines, AsyncTaskMethodBuilder<TResult> structure [.NET Framework]
ms.assetid: 17ebc340-8170-4aff-bf54-dc4548c83632
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 35e1ca4d19727383bdd7c957bc59fd6b6568c9f5
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145645"
---
# <a name="asynctaskmethodbuilderlttresultgt-structure---internal-members"></a>&lt; &gt; Estrutura de TResult AsyncTaskMethodBuilder-membros internos
Este tópico descreve os membros internos da <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> classe. Para obter informações gerais sobre essa classe, consulte o <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> tópico de referência.

 **Namespace:** <xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **Assembly:** mscorlib (no mscorlib.dll)

 Como você não pode acessar esses membros internos do .NET Framework, a sintaxe a seguir é fornecida em Common Intermediate Language (CIL).

## <a name="syntax"></a>Sintaxe

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncTaskMethodBuilder`1<TResult>
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>Membros internos

|Nome|Descrição|
|----------|-----------------|
|[Propriedade ObjectIdForDebugger](../../extensibility/debugger/asynctaskmethodbuilder-tresult-objectidfordebugger-property.md)|Obtém um objeto que pode ser usado para identificar exclusivamente esse construtor para o depurador.|
|[campo de m_task](../../extensibility/debugger/asynctaskmethodbuilder-tresult-m-task-field.md)|Representa a tarefa interna inicializada lentamente.|

## <a name="see-also"></a>Confira também
- <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601>
- [Elementos internos de extensão paralela para o .NET Framework](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
