---
title: Encerramento e desanexação | Microsoft Docs
description: A finalização normal significa que um programa que está sendo depurado é executado até a conclusão sem pontos de interrupção, exceções, erros de tempo de execução ou loops infinitos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- programs, termination events
- debug engines, detaching from programs
ms.assetid: 268c1e51-6363-45d1-964c-1ab99bdfa4f9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8662809b50dbfec3046af1d0d6b6fa151c3a33e0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105057826"
---
# <a name="termination-and-detaching"></a>Encerramento e desanexação
A seção a seguir descreve o encerramento normal.

## <a name="discussion"></a>Discussão
 Depois que a interface [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) ou [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) continuar, se não houver nenhum ponto de interrupção, exceções, erros em tempo de execução ou loops infinitos no aplicativo a ser depurado, o programa que está sendo depurado será executado até a conclusão. Esse processo é um encerramento normal.

 Você deve enviar um [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) para implementar o encerramento normal. A finalização normal requer a execução do método [IDebugProgramDestroyEvent2:: GetExitCode](../../extensibility/debugger/reference/idebugprogramdestroyevent2-getexitcode.md) .

## <a name="see-also"></a>Confira também
- [Criando um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)
