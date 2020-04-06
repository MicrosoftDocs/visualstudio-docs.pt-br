---
title: Término e Desapego | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debug engines, detaching from programs
ms.assetid: 268c1e51-6363-45d1-964c-1ab99bdfa4f9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 0b88255d618ce42fa55d878f192d31523ba3f83b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712490"
---
# <a name="termination-and-detaching"></a>Término e desapego
A seção a seguir descreve o término normal.

## <a name="discussion"></a>Discussão
 Depois que a interface [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) ou [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) continua, se não houver pontos de interrupção, exceções, erros de tempo de execução ou loops infinitos no aplicativo a ser depurado, o programa que está sendo depurado é executado até a conclusão. Este processo é uma rescisão normal.

 Você deve enviar um [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) para implementar o término normal. O término normal requer a execução do método [IDebugProgramDestroyEvent2::GetExitCode.](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md)

## <a name="see-also"></a>Confira também
- [Criando um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)
