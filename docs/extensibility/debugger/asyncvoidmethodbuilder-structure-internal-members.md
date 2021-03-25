---
description: Este tópico descreve os membros internos da classe System. Runtime. CompilerServices. AsyncVoidMethodBuilder.
title: Estrutura AsyncVoidMethodBuilder-membros internos | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, AsyncVoidMethodBuilder structure [.NET Framework]
- AsyncVoidMethodBuilder structure [.NET Framework debug engines]
ms.assetid: fe2970ab-d4c5-4355-a8e4-772ee0a57178
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4097bce1f7fd90c5b73a3bb450a873561d76d9c1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055330"
---
# <a name="asyncvoidmethodbuilder-structure---internal-members"></a>Estrutura AsyncVoidMethodBuilder-membros internos
Este tópico descreve os membros internos da <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> classe. Para obter informações gerais sobre essa classe, consulte o <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> tópico de referência.

 **Namespace:** <xref:System.Runtime.CompilerServices?displayProperty=fullName>

 **Assembly:** mscorlib (no mscorlib.dll)

 Como você não pode acessar esses membros internos do .NET Framework, a sintaxe a seguir é fornecida em Common Intermediate Language (CIL).

## <a name="syntax"></a>Sintaxe

```csharp
.class public sequential ansi sealed beforefieldinit System.Runtime.CompilerServices.AsyncVoidMethodBuilder
       extends System.ValueType
       implements System.Runtime.CompilerServices.IAsyncMethodBuilder
```

## <a name="internal-members"></a>Membros internos

|Nome|Descrição|
|----------|-----------------|
|[Propriedade ObjectIdForDebugger](../../extensibility/debugger/asyncvoidmethodbuilder-objectidfordebugger-property.md)|Obtém um objeto que pode ser usado para identificar exclusivamente esse construtor para o depurador.|
|[campo de m_objectIdForDebugger](../../extensibility/debugger/asyncvoidmethodbuilder-m-objectidfordebugger-field.md)|Representa o objeto inicializado lentamente usado pelo depurador para identificar exclusivamente este construtor.|

## <a name="see-also"></a>Confira também
- <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder>
- [Elementos internos de extensão paralela para o .NET Framework](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
