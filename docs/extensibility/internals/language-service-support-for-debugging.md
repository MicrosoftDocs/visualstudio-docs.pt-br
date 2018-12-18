---
title: Suporte ao serviço de linguagem para depuração | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugger, language support
- language services, debugging support
ms.assetid: 7a44067f-a410-4a6a-84d2-bda5184140bc
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 59c044f6ffc3f2cdf0749f0192f4b8fa458b00cc
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31128644"
---
# <a name="language-service-support-for-debugging"></a>Suporte ao serviço de linguagem para depuração
Um serviço de idioma pode fornecer recursos que oferecem suporte a um depurador a <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo> interface. Esses recursos incluem validar os pontos de interrupção e fornecer uma lista de expressões para o **Autos** janela.  
  
 No entanto, você precisa ter um avaliador de expressão para depurar seu idioma. O avaliador de expressão é responsável por avaliar expressões para gerar valores de durante a depuração. Para obter informações sobre como implementar avaliadores de expressão do CLR, consulte:  
  
-   [Avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)  
  
-   [Amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)  
  
## <a name="compiler-output"></a>Saída do compilador  
 O tipo de compilador determina o que você precisa fazer para implementar a depuração para o seu idioma. Se o compilador tem como alvo o sistema operacional Windows e grava um arquivo. PDB, você pode depurar programas com o código nativo que é integrado ao Visual Studio do mecanismo de depuração. Se o compilador gera Microsoft intermediate language (MSIL), você pode depurar programas com o código gerenciado depuração engine, que também é integrado no Visual Studio. Se o compilador tem como alvo um sistema operacional proprietário ou em um ambiente de tempo de execução diferente, você precisa gravar seu próprio mecanismo de depuração.  
  
 Para obter mais informações sobre a implementação de depuração para o seu idioma, consulte [Introdução](../../extensibility/debugger/getting-started-with-debugger-extensibility.md) no SDK do Visual Studio de depuração.