---
title: Roteiro para estender o depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], roadmap
- Debugging SDK, roadmap
ms.assetid: 1f4096a8-f7aa-4dfa-84e1-6d59263e70bb
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 7527d142b27e5b49bcf133429dc232614bad04a2
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942667"
---
# <a name="roadmap-for-extending-the-debugger"></a>Roteiro para estender o depurador
Esta documentação fornece informações de referência e a guia para estender a [!INCLUDE[vs_current_short](../../code-quality/includes/vs_current_short_md.md)] do depurador com o [!INCLUDE[vsipsdk](../../extensibility/includes/vsipsdk_md.md)].  
  
 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] depuração da documentação inclui exemplos, uma referência abrangente e representativos vários cenários que demonstram maneiras comuns de personalizar o depurador.  
  
 O compilador e sua saída determinam o que é necessário para configurar a depuração em seu produto. Se seu compilador:  
  
- Direciona o sistema operacional nativo do Windows e grava um *. PDB* arquivo, você pode depurar programas com o mecanismo de depuração de código nativo (DES), que é integrado ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Você não precisa implementar um avaliador de expressão DE. O avaliador de expressão foi escrito para a sintaxe da linguagem de programação C++.  
  
- Produz a Microsoft intermediate language (MSIL) de saída, você pode depurar programas com o mecanismo de depuração de código gerenciado DE, que também é integrado ao [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. Portanto, você só precisa implementar um avaliador de expressão. Um avaliador de expressão de exemplo é fornecido para você. Para mais informações, consulte os seguintes tópicos:  
  
   [Avaliação de expressão](../../extensibility/debugger/expression-evaluation-visual-studio-debugging-sdk.md)  
  
   [Avaliando expressões](../../extensibility/debugger/evaluating-expressions.md)  
  
   [Contexto de avaliação de expressão](../../extensibility/debugger/expression-evaluation-context.md)  
  
   [Avaliação da expressão no modo de interrupção](../../extensibility/debugger/expression-evaluation-in-break-mode.md)  
  
   [Escrever um avaliador de expressão de tempo de execução de linguagem comum](../../extensibility/debugger/writing-a-common-language-runtime-expression-evaluator.md)  
  
- Destinos de um proprietário de sistema operacional ou outro ambiente de tempo de execução, você precisa escrever seu próprio DE. Um tutorial que cria um simples DE usando COM ATL é fornecido. Para mais informações, consulte os seguintes tópicos:  
  
   [Criar um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)  
  
   [Tutorial: Criar um mecanismo de depuração usando COM ATL](https://msdn.microsoft.com/library/9097b71e-1fe7-48f7-bc00-009e25940c24)  
  
   [Implementar um fornecedor de porta](../../extensibility/debugger/implementing-a-port-supplier.md)  
  
   [Amostras](../../extensibility/debugger/visual-studio-debugging-samples.md)  
  
## <a name="see-also"></a>Consulte também  
 [Introdução](../../extensibility/debugger/getting-started-with-debugger-extensibility.md)