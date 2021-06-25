---
title: Modos operacionais | Microsoft Docs
description: Saiba mais sobre os três modos em que o IDE pode operar, que são modo de design, modo de executar e modo de quebra.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- debug engines, modes
ms.assetid: f69972d0-809d-40df-9da3-04738791391c
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 559df92545f4c14eb0575e7ef758e73028349b76
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899102"
---
# <a name="operational-modes"></a>Modos operacionais
Há três modos nos quais o IDE pode operar, da seguinte forma:

- [Modo de design](#vsconoperationalmodesanchor1)

- [Modo de executar](#vsconoperationalmodesanchor2)

- [Modo de interrupção](#vsconoperationalmodesanchor3)

  Como o DE (mecanismo de depuração) personalizado faz a transição entre esses modos é uma decisão de implementação que exige que você se familiarizar com os mecanismos de transição. O DE pode ou não implementar diretamente esses modos. Esses modos são, na verdade, modos de pacote de depuração que alternam com base na ação do usuário ou eventos do DE. Por exemplo, a transição do modo de executar para o modo de interrupção é impedida por um evento de interrupção do DE. A transição de quebra para o modo de execução ou modo de etapa é desagradada pelo usuário que executa operações como Etapa ou Executar. Para obter mais informações sobre transições de DE, consulte [Controle de execução](../../extensibility/debugger/control-of-execution.md).

## <a name="design-mode"></a><a name="vsconoperationalmodesanchor1"></a> Modo de design
 O modo de design é o estado não de Visual Studio depuração, durante o qual você pode definir recursos de depuração em seu aplicativo.

 Apenas alguns recursos de depuração são usados durante o modo de design. Um desenvolvedor pode optar por definir pontos de interrupção ou criar expressões de relógio. O DE nunca é carregado ou chamado enquanto o IDE está no modo de design. A interação com o DE ocorre somente durante os modos de executar e de quebra.

## <a name="run-mode"></a><a name="vsconoperationalmodesanchor2"></a> Modo de executar
 O modo de executar ocorre quando um programa é executado em uma sessão de depuração no IDE. O aplicativo é executado até o término, até que um ponto de interrupção seja atingido ou até que uma exceção seja lançada. Quando o aplicativo é executado para o encerramento, o DE faz a transição para o modo de design. Quando um ponto de interrupção é atingido ou uma exceção é lançada, o DE faz a transição para o modo de interrupção.

## <a name="break-mode"></a><a name="vsconoperationalmodesanchor3"></a> Modo de quebra
 O modo de quebra ocorre quando a execução do programa de depuração é suspensa. O modo de quebra oferece ao desenvolvedor um instantâneo do aplicativo no momento da quebra e permite que o desenvolvedor analise o estado do aplicativo e altere como o aplicativo será executado. O desenvolvedor pode exibir e editar o código, examinar ou modificar dados, reiniciar o aplicativo, encerrar a execução ou continuar a execução do mesmo ponto.

 O modo de interrupção é inserido quando o DE envia um evento de interrupção síncrono. Eventos de parada síncrona, também chamados de eventos de interrupção, notificam o SDM (gerenciador de depuração de sessão) e o IDE de que o aplicativo que está sendo depurado parou de executar o código. As interfaces [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) [e IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) são exemplos de eventos de interrupção.

 A interrupção de eventos é continuada por uma chamada para um dos seguintes métodos, que fazem a transição do depurador do modo de interrupção para o modo de executar ou etapa:

- [Executar](../../extensibility/debugger/reference/idebugprocess3-execute.md)

- [Step](../../extensibility/debugger/reference/idebugprocess3-step.md)

- [Continuar](../../extensibility/debugger/reference/idebugprocess3-continue.md)

### <a name="step-mode"></a><a name="vsconoperationalmodesanchor4"></a> Modo de etapa
 O modo de etapa ocorre quando o programa é etapas para a próxima linha de código ou para dentro, acima ou fora de uma função. Uma etapa é executada chamando o método [Step](../../extensibility/debugger/reference/idebugprocess3-step.md). Esse método requer `DWORD` s que especifiquem as enumerações [STEPUNIT](../../extensibility/debugger/reference/stepunit.md) e [STEPKIND](../../extensibility/debugger/reference/stepkind.md) como parâmetros de entrada.

 Quando o programa é executado com êxito para a próxima linha de código ou para uma função ou é executado para o cursor ou para um ponto de interrupção definido, o DE faz a transição automaticamente de volta para o modo de interrupção.

## <a name="see-also"></a>Confira também
- [Controle de execução](../../extensibility/debugger/control-of-execution.md)
