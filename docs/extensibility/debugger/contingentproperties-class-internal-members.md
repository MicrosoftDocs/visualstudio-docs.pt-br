---
description: Contém propriedades adicionais para um objeto System. Threading. Tasks. Task.
title: Classe contingentproperties-membros internos | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ContingentProperties class [.NET Framework debug engines]
- debug engines, ContingentProperties class [.NET Framework]
ms.assetid: c49d1362-ab1c-4b6d-9950-fcae40e0e66b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 295b8c3b33059811e665e362c9894103b47c422d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054992"
---
# <a name="contingentproperties-class---internal-members"></a>Classe contingentproperties-membros internos
Contém propriedades adicionais para um <xref:System.Threading.Tasks.Task> objeto.

 **Namespace:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **Assembly:** mscorlib (no mscorlib.dll)

 Como você não pode acessar esses membros internos do .NET Framework, a sintaxe a seguir é fornecida em Common Intermediate Language (CIL).

## <a name="syntax"></a>Sintaxe

```csharp
.class auto ansi nested assembly beforefieldinit ContingentProperties
       extends System.Object
```

## <a name="members"></a>Membros

### <a name="fields"></a>Campos

|Nome|Descrição|
|----------|-----------------|
|[m_children](../../extensibility/debugger/m-children-field.md)|A lista de tarefas filho que são registradas com esta tarefa.|

## <a name="remarks"></a>Comentários
 O .NET Framework Inicializa os campos dessa classe somente quando eles são necessários.

## <a name="see-also"></a>Confira também
- [Elementos internos de extensão paralela para o .NET Framework](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
