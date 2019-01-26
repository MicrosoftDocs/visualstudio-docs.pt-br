---
title: Extensibilidade do depurador do Visual Studio | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Visual Studio], Debugging SDK
- Debugging SDK
ms.assetid: c088b6a2-c3ad-446b-830d-9c6f41b2934b
author: gregvanl
ms.author: gregvanl
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 04031c2307d5d91a4854678f810f87b5afde0627
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "54952152"
---
# <a name="visual-studio-debugger-extensibility"></a>Extensibilidade do depurador do Visual Studio
O Visual Studio inclui um depurador de código fonte totalmente interativas, fornecendo uma ferramenta poderosa e fácil de usar para rastrear bugs em seu programa. O depurador tem suporte completo ao Visual Basic, c#, C/C++ e JavaScript. No entanto, com o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)], que é disponível do [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=214453), outras linguagens de programação podem ter suporte no depurador com os mesmos recursos avançados.  
  
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador é o front-end comum (ou seja, a interface do usuário) para os componentes de depuração que são, por sua vez, específicas da linguagem que está sendo depurada. Para novas linguagens, tudo o que é necessário para dar suporte ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depurador é criar os componentes de back-end necessários, como um mecanismo de depuração (DES). Esse ponto é onde o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] chega.  
  
 O [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)] inclui uma referência completa a todos os [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] elementos necessários para criar DE um novo. Além disso, há exemplos e tutoriais que ajudarão você a começar.  
  
 Para obter um exemplo completo de um sistema de projeto de linguagem com suporte à depuração, consulte o [exemplo de IronPython](https://www.microsoft.com/download/details.aspx?id=55984).  
  
 As seções a seguir descrevem como estender o depurador usando o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Introdução](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)  
 Descreve o que [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ofertas e como instalar o SDK de depuração.  
  
 [Criar um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
 Documenta o processo DE personalizado, de preparação de seu programa para a DE para desanexar o DE.  
  
 [Escrever um avaliador de expressão de CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)  
 Explica como se você deve escrever um avaliador de expressão.  
  
 [Escolha uma estratégia de implementação do mecanismo de depuração](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md)  
 Discute como implementar seu DE.  
  
 [Referência](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md)  
 Documentos de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] API de depuração.  
  
 [Amostras](../../extensibility/debugger/visual-studio-debugging-samples.md)  
 Contém links para uma amostra do avaliador de expressão comum language runtime e um exemplo de mecanismo de depuração.
