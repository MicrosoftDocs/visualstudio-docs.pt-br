---
title: Contexto de código | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], contexts
ms.assetid: 65e4d37a-086b-426e-9394-a3534967fd59
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d59a4c79cb21386fa6f6e7031404aeb0b435b3b9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68197368"
---
# <a name="code-context"></a>Contexto de código
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Na [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depuração, um **contexto de código**:  
  
- Fornece uma abstração de uma posição no código como conhecidos para o mecanismo de depuração (DES). Para a maioria das arquiteturas de tempo de execução atualmente, um contexto de código pode ser pensado como um endereço no fluxo de instruções de um programa. Para idiomas não tradicionais, onde o código não pode ser representado por instruções, um contexto de código pode ser representado por outros meios.  
  
- Descreve a posição atual no fluxo de execução do programa que está sendo depurado.  
  
- Existe apenas quando um programa foi interrompido no ponto de interrupção.  
  
- Tem um contexto de documento associado.  
  
- É implementado por uma [IDebugCodeContext2](../../extensibility/debugger/reference/idebugcodecontext2.md) interface.  
  
## <a name="see-also"></a>Consulte também  
 [Contexto de documento](../../extensibility/debugger/document-context.md)   
 [Contextos do depurador](../../extensibility/debugger/debugger-contexts.md)
