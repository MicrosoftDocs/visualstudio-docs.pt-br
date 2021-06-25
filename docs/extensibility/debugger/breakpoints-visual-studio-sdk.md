---
title: Pontos de interrupção (Visual Studio SDK) | Microsoft Docs
description: 'Saiba mais sobre os três tipos de pontos de interrupção: pendente, limitado e erro. Este artigo lista as interfaces usadas para implementar os tipos.'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- breakpoints
ms.assetid: acfcabed-9f2f-436c-ad18-7ca2f45d631b
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1fce472faf95aa77f87ab02d78a3da640b6bd3bf
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901481"
---
# <a name="breakpoints-visual-studio-sdk"></a>Pontos de interrupção (SDK do Visual Studio)
Há três tipos de pontos de interrupção: pendente, limitado e erro.

 **Um ponto de interrupção pendente:**

- É uma abstração que contém todas as informações necessárias para vincular um ponto de interrupção a um ou mais contextos de código em um ou mais programas. Sempre que um programa que está sendo depurado faz com que o código seja carregado, o mecanismo de depuração verifica todos os pontos de interrupção pendentes para ver se eles podem ser vinculados.

   Um ponto de interrupção pendente nunca se vincula ao código, mas, em vez disso, coleta e é dito que contém todos os pontos de interrupção vinculados que ele gera.

- É representado por uma interface [IDebugPendingBreakpoint2.](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)

  **Um ponto de interrupção vinculado:**

- É uma abstração para um ponto de interrupção associado a ou associado a um único contexto de código. Cada ponto de interrupção vinculado é gerado em resposta a um ponto de interrupção pendente. No entanto, um ponto de interrupção pendente pode gerar mais de um ponto de interrupção vinculado.

   Quando o código é descarregado, um ponto de interrupção vinculado pode ser desaconsudido e descartado.

- É representado por uma interface [IDebugBoundBreakpoint2.](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)

  **Um ponto de interrupção de erro:**

- É uma abstração para descrever um erro ao tentar vincular um ponto de interrupção pendente a um contexto de código. Um ponto de interrupção de erro descreve um erro no local ou na própria expressão de ponto de interrupção. Para obter mais informações, consulte [Pontos de interrupção de associação](../../extensibility/debugger/binding-breakpoints.md).

   O erro de ponto de interrupção pode ser um erro ou um aviso.

- É representado por uma interface [IDebugErrorBreakpoint2.](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)

## <a name="see-also"></a>Confira também
- [Programas](../../extensibility/debugger/programs.md)
- [Conceitos do depurador](../../extensibility/debugger/debugger-concepts.md)
- [Contexto de código](../../extensibility/debugger/code-context.md)
- [IDebugBoundBreakpoint2](../../extensibility/debugger/reference/idebugboundbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugErrorBreakpoint2](../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
