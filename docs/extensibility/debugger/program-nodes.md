---
title: Nós de programa | Microsoft Docs
description: Este artigo descreve a definição e a função de um nó de programa na arquitetura do depurador no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- program nodes, debugging context
- debugging [Debugging SDK], program nodes
- program nodes, adding
- program nodes, superceding
ms.assetid: 1c5a5c13-c14d-42c3-af11-4c63f1032c8d
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5658026b60006a58ba168ca713028b9876a3c57d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094621"
---
# <a name="program-nodes"></a>Nós de programa
Na arquitetura do depurador, um *nó de programa*:

- É uma descrição leve de um programa.

- Pode identificar a si mesmo e o processo em que ele está sendo executado. Um nó de programa pode ser anexado a, ser desanexado do e descrever o mecanismo de depuração (DE) que o criou, se houver.

- É representado por uma interface [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) , normalmente criada por uma ou uma porta. Nós de programa são adicionados a uma porta chamando [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md). Quando um nó de programa é adicionado a uma porta, ele é adicionado ao processo que contém o programa que esse nó de programa representa.

  Um pouco depois que uma sessão de depuração é iniciada, dependendo da implementação do pacote de depuração, os nós de programa são usados para criar programas correspondentes. Quando um processo é consultado para seus programas, os programas são enumerados, um para cada nó de programa.

  Antes que um programa seja anexado ao, o IDE precisa apenas de uma descrição leve do programa. Essas informações podem ser obtidas no nó do programa. Quando o programa estiver anexado ao, o IDE exibirá informações mais detalhadas, como uma lista de todos os threads em execução no programa. Essas informações são obtidas do próprio programa.

## <a name="see-also"></a>Confira também
- [Programas](../../extensibility/debugger/programs.md)
- [Processos](../../extensibility/debugger/processes.md)
- [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
