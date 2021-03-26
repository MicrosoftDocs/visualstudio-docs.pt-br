---
title: Excluindo um ponto de interrupção | Microsoft Docs
description: Saiba como o Gerenciador de depuração de sessão remove um ponto de interrupção pendente e todos os pontos de interrupção associados a ele quando um ponto de interrupção pendente é excluído.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- breakpoints, deleting
- debugging [Debugging SDK], deleting breakpoints
ms.assetid: 75a046cc-d20a-4c79-ad2d-1f18426ac5d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1d8e0d68f32ece7760805c05fd281b0e62a70003
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097273"
---
# <a name="deleting-a-breakpoint"></a>Excluindo um ponto de interrupção
O seguinte descreve o processo ao excluir um ponto de interrupção pendente:

## <a name="deletion-process"></a>Processo de exclusão
 O SDM (Gerenciador de depuração de sessão) chama o método [IDebugPendingBreakpoint2::D xcluir](../../extensibility/debugger/reference/idebugpendingbreakpoint2-delete.md) para remover o ponto de interrupção pendente e todos os pontos de interrupção associados a ele.

> [!NOTE]
> Um ponto de interrupção de associação simples também pode ser excluído por uma chamada para [IDebugBoundBreakpoint2::D xcluir](../../extensibility/debugger/reference/idebugboundbreakpoint2-delete.md).

## <a name="see-also"></a>Confira também
- [Chamar eventos do depurador](../../extensibility/debugger/calling-debugger-events.md)
