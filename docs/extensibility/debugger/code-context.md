---
title: Contexto de código | Microsoft Docs
description: Saiba mais sobre o contexto de código na depuração do Visual Studio, que descreve uma posição no código que existe quando um programa é interrompido em um ponto de interrupção.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 65e4d37a-086b-426e-9394-a3534967fd59
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c668cd1fa80efe24fa596cc4e9f311e2db519246
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105055031"
---
# <a name="code-context"></a>Contexto de código
Na [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuração, um **contexto de código**:

- Fornece uma abstração de uma posição no código, como conhecido pelo mecanismo DE depuração (DE). Para a maioria das arquiteturas de tempo de execução hoje, um contexto de código pode ser considerado como um endereço no fluxo de instruções de um programa. Para linguagens não tradicionais, em que o código não pode ser representado por instruções, um contexto de código pode ser representado por outros meios.

- Descreve a posição atual no fluxo de execução do programa que você está depurando.

- Existe somente quando um programa é interrompido em um ponto de interrupção.

- Tem um contexto de documento associado.

- É implementado por uma interface [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md) .

## <a name="see-also"></a>Confira também
- [Contexto do documento](../../extensibility/debugger/document-context.md)
- [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)
