---
title: Extensibilidade do depurador do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- debugging [Visual Studio], Debugging SDK
- Debugging SDK
ms.assetid: c088b6a2-c3ad-446b-830d-9c6f41b2934b
caps.latest.revision: 33
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 8b5e9e7a3db38b5138f6392ff89f3a3bb4a13303
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51743487"
---
# <a name="visual-studio-debugger-extensibility"></a>Extensibilidade do depurador do Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

O Visual Studio inclui um depurador de código fonte totalmente interativas, fornecendo uma ferramenta poderosa e fácil de usar para rastrear bugs em seu programa. O depurador tem suporte completo ao Visual Basic, c#, C/C++ e JavaScript. No entanto, com o [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)], que é disponível do [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=214453), outras linguagens de programação podem ter suporte no depurador com os mesmos recursos avançados.  
  
 O [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depurador é o front-end comum (ou seja, a interface do usuário) para os componentes de depuração que são, por sua vez, específicas da linguagem que está sendo depurada. Para novas linguagens, tudo o que é necessário para dar suporte ao [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depurador é criar os componentes de back-end necessários, como um mecanismo de depuração (DES). É aí que o [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] chega.  
  
 O [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)] inclui uma referência completa a todos os [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] elementos necessários para criar DE um novo. Além disso, há exemplos e tutoriais que ajudarão você a começar.  
  
 Para um exemplo de ponta a ponta de um sistema de projeto de linguagem com suporte à depuração, consulte o [exemplo de IronPython](http://msdn.microsoft.com/en-us/4c41695c-12c1-4670-b43b-d8d84c9e4089).  
  
 As seções a seguir descrevem como estender o depurador usando o [!INCLUDE[vsipsdk](../../includes/vsipsdk-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Introdução](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)  
 Descreve o que [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ofertas e como instalar o SDK de depuração.  
  
 [Criar um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
 Documenta o processo DE personalizado, de preparação de seu programa para a DE para desanexar o DE.  
  
 [Escrevendo um avaliador de expressão do CLR](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)  
 Explica como se você deve escrever um avaliador de expressão.  
  
 [Escolher uma estratégia de implementação do mecanismo de depuração](../../extensibility/debugger/choosing-a-debug-engine-implementation-strategy.md)  
 Discute como implementar seu DE.  
  
 [Referência](../../extensibility/debugger/reference/reference-visual-studio-debugging-apis.md)  
 Documentos de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] API de depuração.  
  
 [Amostras](../../extensibility/debugger/visual-studio-debugging-samples.md)  
 Contém links para uma amostra do avaliador de expressão comum language runtime e um exemplo de mecanismo de depuração.

