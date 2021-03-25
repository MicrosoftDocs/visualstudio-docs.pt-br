---
title: Atingir um ponto de interrupção | Microsoft Docs
description: Este artigo descreve o processo que ocorre quando o mecanismo de depuração atinge um ponto de interrupção durante a execução ou a depuração.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], hitting breakpoints
- breakpoints, hitting
ms.assetid: a77816e3-b15b-46a0-90cd-be7242e4d6c9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: e093437fcc8b3e1e2663c2a46ebb3b70d32efbec
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059945"
---
# <a name="hit-a-breakpoint"></a>Atingir um ponto de interrupção
A seção a seguir descreve o processo quando o mecanismo de depuração (DE) atinge um ponto de interrupção durante a execução ou a depuração:

## <a name="troubleshoot-a-hit-breakpoint"></a>Solucionar um ponto de interrupção de clique

1. O DE envia uma interface [IDebugBreakpointEvent2](../../extensibility/debugger/reference/idebugbreakpointevent2.md) como um **EVENT_SYNC_STOP**.

2. O SDM (Gerenciador de depuração de sessão) chama [IDebugBreakpointEvent2::: EnumBreakpoints](../../extensibility/debugger/reference/idebugbreakpointevent2-enumbreakpoints.md) para obter o ponto de interrupção que foi atingido.

## <a name="see-also"></a>Confira também
- [Chamar eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
