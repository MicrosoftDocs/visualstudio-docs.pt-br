---
title: Nós de programa | Microsoft Docs
description: Este artigo descreve a definição e a função de um nó de programa na arquitetura do depurador no Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
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
ms.openlocfilehash: 4c26fa95a5fedf325591ce517e7c12ecebcd705c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899076"
---
# <a name="program-nodes"></a>Nós do programa
Na arquitetura do depurador, um *nó de programa*:

- É uma descrição leve de um programa.

- Pode identificar a si mesmo e o processo no qual ele está sendo executado. Um nó de programa pode ser anexado, desacoplada de e descrever o DE (mecanismo de depuração) que o criou, se for o caso.

- É representado por uma interface [IDebugProgramNode2,](../../extensibility/debugger/reference/idebugprogramnode2.md) normalmente criada por uma PORTA ou DE. Os nós de programa são adicionados a uma porta chamando [AddProgramNode.](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) Quando um nó de programa é adicionado a uma porta, ele é adicionado ao processo que contém o programa que esse nó de programa representa.

  Algum tempo após o início de uma sessão de depuração, dependendo da implementação do pacote de depuração, os nós de programa são usados para criar programas correspondentes. Quando um processo é consultado para seus programas, os programas são enumerados, um para cada nó de programa.

  Antes que um programa seja anexado, o IDE precisa apenas de uma descrição leve do programa. Essas informações podem ser obtidas do nó do programa. Depois que o programa é anexado, o IDE exibe informações mais detalhadas, como uma lista de todos os threads em execução no programa. Essas informações são obtidas do próprio programa.

## <a name="see-also"></a>Confira também
- [Programas](../../extensibility/debugger/programs.md)
- [Processos](../../extensibility/debugger/processes.md)
- [Mecanismo de depuração](../../extensibility/debugger/debug-engine.md)
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [AddProgramNode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)
