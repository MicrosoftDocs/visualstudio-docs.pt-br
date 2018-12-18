---
title: Suporte do serviço de linguagem para depuração | Microsoft Docs
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
- debugger, language support
- language services, debugging support
ms.assetid: 7a44067f-a410-4a6a-84d2-bda5184140bc
caps.latest.revision: 16
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 7141c7a6b3845edda6888e1ed33abfbf8af37988
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51809682"
---
# <a name="language-service-support-for-debugging"></a>Suporte do serviço de linguagem para depuração
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um serviço de linguagem pode fornecer recursos que dão suporte a um depurador por meio de <xref:Microsoft.VisualStudio.TextManager.Interop.IVsLanguageDebugInfo> interface. Esses recursos incluem a validação de pontos de interrupção e fornecendo uma lista de expressões para o **automóveis** janela.  
  
 No entanto, você precisa ter um avaliador de expressão para depurar seu idioma. O avaliador de expressão é responsável por avaliar expressões para produzir valores durante a depuração. Para obter informações sobre como implementar os avaliadores de expressão de CLR, consulte:  
  
-   [Avaliadores de expressão de CLR](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)  
  
-   [Amostra do avaliador de expressão gerenciado](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)  
  
## <a name="compiler-output"></a>Saída do compilador  
 O tipo do compilador determina o que você precisa fazer para implementar a depuração para seu idioma. Se o compilador direciona o sistema operacional Windows e grava um arquivo. PDB, você pode depurar programas com o mecanismo que é integrado ao Visual Studio de depuração de código nativo. Se o compilador produz Microsoft intermediate language (MSIL), você pode depurar programas com o código gerenciado, depuração engine, que também é integrado ao Visual Studio. Se seu compilador se destina a um sistema operacional proprietário ou um ambiente de tempo de execução diferente, você precisa escrever seu próprio mecanismo de depuração.  
  
 Para obter mais informações sobre a implementação de depuração para seu idioma, consulte [guia de Introdução](../../extensibility/debugger/getting-started-with-debugger-extensibility.md) no SDK do Visual Studio de depuração.

