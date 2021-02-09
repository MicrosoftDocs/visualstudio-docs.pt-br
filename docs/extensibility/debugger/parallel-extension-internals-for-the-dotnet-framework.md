---
title: Elementos internos de extensão paralela para o .NET Framework | Microsoft Docs
description: Esses recursos descrevem tipos, métodos e campos internos de classes usados para implementar um depurador personalizado para as extensões paralelas para o .NET Framework.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, internals [.NET Framework]
ms.assetid: 93e07cfa-91fa-464c-b866-8bf5570411df
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b3c17c36112d383528e97c1eb04c858b89406c36
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2021
ms.locfileid: "99900318"
---
# <a name="parallel-extension-internals-for-the-net-framework"></a>Elementos internos de extensão paralela para o .NET Framework
Esta seção descreve os tipos internos, os métodos e os campos de classes que ajudam a implementar um depurador personalizado para as extensões paralelas para o .NET Framework.

## <a name="in-this-section"></a>Nesta seção
 [Classe de tarefa](../../extensibility/debugger/task-class-internal-members.md) Descreve os membros de dados internos da <xref:System.Threading.Tasks.Task?displayProperty=fullName> classe.

 [Classe TaskScheduler](../../extensibility/debugger/taskscheduler-class-internal-members.md) Descreve os membros de dados internos da <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName> classe.

 [Classe contingentproperties](../../extensibility/debugger/contingentproperties-class-internal-members.md) Descreve os membros de dados internos da `System.Threading.Tasks.ContingentProperties` classe.

 [Estrutura AsyncTaskMethodBuilder](../../extensibility/debugger/asynctaskmethodbuilder-structure-internal-members.md) Descreve os membros internos da <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder> estrutura.

 [A \<TResult> estrutura AsyncTaskMethodBuilder](../../extensibility/debugger/asynctaskmethodbuilder-tresult-structure-internal-members.md) descreve os membros internos da <xref:System.Runtime.CompilerServices.AsyncTaskMethodBuilder%601> estrutura.

 [Estrutura AsyncVoidMethodBuilder](../../extensibility/debugger/asyncvoidmethodbuilder-structure-internal-members.md) Descreve os membros internos da <xref:System.Runtime.CompilerServices.AsyncVoidMethodBuilder> estrutura.

## <a name="see-also"></a>Confira também
- <xref:System.Threading.Tasks.Task?displayProperty=fullName>
- <xref:System.Threading.Tasks.TaskScheduler?displayProperty=fullName>
- [Extensibilidade do depurador do Visual Studio](../../extensibility/debugger/visual-studio-debugger-extensibility.md)
- [Programação paralela](/dotnet/standard/parallel-programming/index)
