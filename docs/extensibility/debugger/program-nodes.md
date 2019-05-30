---
title: Nós de programa | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- program nodes, debugging context
- debugging [Debugging SDK], program nodes
- program nodes, adding
- program nodes, superceding
ms.assetid: 1c5a5c13-c14d-42c3-af11-4c63f1032c8d
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 084a386cc7d7f9c6d606e7015e593a4075ba53a9
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66351435"
---
# <a name="program-nodes"></a>Nós de programa
Na arquitetura do depurador, uma *nó do programa*:

- É uma descrição simples de um programa.

- Pode identificar em si e o processo que está executando no. Um nó de programa pode ser anexado para ser desanexado do e descrever o mecanismo de depuração (DES) que criou, se houver.

- É representado por um [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) interface, geralmente criado por uma porta ou DE. Nós de programa são adicionados a uma porta chamando [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md). Quando um nó do programa é adicionado a uma porta, ele é adicionado ao processo que contém o programa que representa este nó do programa.

  Em algum momento depois que uma sessão de depuração é iniciada, dependendo da implementação do pacote de depuração, nós de programa são usados para criar programas correspondentes. Quando um processo é consultado para seus programas, os programas são enumerados, uma para cada nó do programa.

  Antes de um programa estiver anexado a, o IDE precisa de apenas uma descrição simples do programa. Essas informações podem ser obtidas a partir do nó do programa. Depois que o programa é anexado ao, o IDE exibirá informações mais detalhadas, como uma lista de todos os threads em execução no programa. Essas informações são obtidas do programa em si.

## <a name="see-also"></a>Consulte também
- [Programas](../../extensibility/debugger/programs.md)
- [Processos](../../extensibility/debugger/processes.md)
- [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)