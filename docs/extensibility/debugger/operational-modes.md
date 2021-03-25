---
title: Modos operacionais | Microsoft Docs
description: Saiba mais sobre os três modos nos quais o IDE pode operar, que são o modo de design, o modo de execução e o modo de interrupção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, modes
ms.assetid: f69972d0-809d-40df-9da3-04738791391c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 563db644069731c5d74088dadf296933c36b0cc1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067836"
---
# <a name="operational-modes"></a>Modos operacionais
Há três modos nos quais o IDE pode operar, da seguinte maneira:

- [Modo de design](#vsconoperationalmodesanchor1)

- [Modo de execução](#vsconoperationalmodesanchor2)

- [Modo de interrupção](#vsconoperationalmodesanchor3)

  Como as transições do mecanismo DE depuração personalizado (DE) entre esses modos é uma decisão de implementação que exige que você esteja familiarizado com os mecanismos de transição. O DE maio ou não pode implementar esses modos diretamente. Esses modos são, na verdade, os modos de depuração que mudam com base na ação do usuário ou nos eventos de de. Por exemplo, a transição do modo de execução para o modo de interrupção é acionada por um evento de parada de de. A transição da interrupção para o modo de execução ou o modo de etapa é feito pelo usuário executando operações como Step ou execute. Para obter mais informações sobre transições, consulte [controle de execução](../../extensibility/debugger/control-of-execution.md).

## <a name="design-mode"></a><a name="vsconoperationalmodesanchor1"></a> Modo de design
 O modo de design é o estado de não execução da depuração do Visual Studio, durante o qual você pode definir recursos de depuração em seu aplicativo.

 Apenas alguns recursos de depuração são usados durante o modo de design. Um desenvolvedor pode optar por definir pontos de interrupção ou criar expressões de inspeção. O DE nunca é carregado ou chamado enquanto o IDE está no modo de design. Interação com o DE ocorre somente durante os modos DE execução e de interrupção.

## <a name="run-mode"></a><a name="vsconoperationalmodesanchor2"></a> Modo de execução
 O modo de execução ocorre quando um programa é executado em uma sessão de depuração no IDE. O aplicativo é executado até o encerramento, até que um ponto de interrupção seja atingido ou até que uma exceção seja gerada. Quando o aplicativo é executado até o encerramento, o DE faz a transição para o modo DE design. Quando um ponto de interrupção é atingido ou uma exceção é lançada, o DE faz a transição para o modo DE interrupção.

## <a name="break-mode"></a><a name="vsconoperationalmodesanchor3"></a> Modo de interrupção
 O modo de interrupção ocorre quando a execução do programa de depuração é suspensa. O modo de interrupção oferece ao desenvolvedor um instantâneo do aplicativo no momento da interrupção e permite que o desenvolvedor analise o estado do aplicativo e altere a forma como o aplicativo será executado. O desenvolvedor pode exibir e editar código, examinar ou modificar dados, reiniciar o aplicativo, encerrar a execução ou continuar a execução do mesmo ponto.

 O modo DE interrupção é inserido quando o DE envia um evento de interrupção síncrona. Eventos de interrupção síncronos, também chamados de eventos de interrupção, notificam o SDM (Gerenciador de depuração de sessão) e o IDE que o aplicativo que está sendo depurado parou de executar o código. As interfaces [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) e [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) são exemplos de como parar eventos.

 A interrupção de eventos é continuada por uma chamada para um dos seguintes métodos, que fazem a transição do depurador do modo de interrupção para o modo de execução ou etapa:

- [Executar](../../extensibility/debugger/reference/idebugprocess3-execute.md)

- [Step](../../extensibility/debugger/reference/idebugprocess3-step.md)

- [Continuar](../../extensibility/debugger/reference/idebugprocess3-continue.md)

### <a name="step-mode"></a><a name="vsconoperationalmodesanchor4"></a> Modo de etapa
 O modo de etapa ocorre quando o programa percorre a próxima linha de código, ou para dentro ou para fora de uma função. Uma etapa é executada chamando a [etapa](../../extensibility/debugger/reference/idebugprocess3-step.md)do método. Esse método requer `DWORD` s que especificam as enumerações [STEPUNIT](../../extensibility/debugger/reference/stepunit.md) e [STEPKIND](../../extensibility/debugger/reference/stepkind.md) como parâmetros de entrada.

 Quando o programa passa a funcionar com êxito para a próxima linha de código ou para uma função, ou é executado no cursor ou em um ponto de interrupção definido, o DE faz a transição de volta para o modo DE interrupção.

## <a name="see-also"></a>Confira também
- [Controle de execução](../../extensibility/debugger/control-of-execution.md)
