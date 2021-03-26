---
title: Habilitando um programa a ser depurado | Microsoft Docs
description: Saiba mais sobre como iniciar o mecanismo de depuração ou anexe o mecanismo de depuração a um programa existente para depurar um programa.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], enabling for programs
ms.assetid: 61d24820-0cd9-48b6-8674-6813f7493237
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4ed7ce97e6ff7e8801953877ed80afa7ca262f20
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105097221"
---
# <a name="enable-a-program-to-be-debugged"></a>Habilitar um programa a ser depurado
Antes que o mecanismo DE depuração (DE) possa depurar um programa, você deve primeiro iniciar o ou anexá-lo a um programa existente.

## <a name="in-this-section"></a>Nesta seção
 [Obter uma porta](../../extensibility/debugger/getting-a-port.md) Discute como obter uma porta como a primeira etapa para habilitar um programa a ser depurado.

 [Registrar o programa](../../extensibility/debugger/registering-the-program.md) Explica a próxima etapa para habilitar um programa a ser depurado: registrá-lo com a porta. Depois de registrado, o programa pode ser depurado pelo processo de anexação ou depuração JIT (just-in-time).

 [Anexar ao programa](../../extensibility/debugger/attaching-to-the-program.md) Explica a próxima etapa: anexar o depurador ao programa.

 [Anexação baseada em inicialização](../../extensibility/debugger/launch-based-attachment.md) Descreve o anexo baseado em inicialização para um programa, que é automático após a inicialização pelo SDM.

 [Enviar os eventos necessários](../../extensibility/debugger/sending-the-required-events.md) Percorre os eventos necessários ao criar um mecanismo DE depuração (DE) e anexá-lo a um programa.

## <a name="related-sections"></a>Seções relacionadas
 [Criando um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md) Define um mecanismo DE depuração (DE) e descreve os serviços implementados por meio das interfaces e como eles podem fazer com que o depurador faça a transição entre diferentes modos operacionais.
