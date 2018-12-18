---
title: Chamar eventos do depurador | Microsoft Docs
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
- debugging [Debugging SDK], events
ms.assetid: b3440ac3-80af-40c6-bef4-cbf00fa67885
caps.latest.revision: 8
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 9682e16c059483d44953ffbe11d8e10e6d46a435
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51767503"
---
# <a name="calling-debugger-events"></a>Chamando eventos do depurador
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Eventos em sessões de depuração ocorrerem em uma ordem específica.  
  
## <a name="discussion"></a>Discussão  
 Para entender o padrão de chamadas entre o mecanismo de depuração (DES) e o Gerenciador de sessão de depuração (SDM), o código a seguir representa a ordem de chamada dos eventos que ocorrem em uma sessão de depuração típica:  
  
1.  [Anexar e desanexar a um programa](../../extensibility/debugger/attaching-and-detaching-to-a-program.md)  
  
2.  [Iniciando o depurador](../../extensibility/debugger/launching-the-debugger.md)  
  
3.  [Encerrar um programa](../../extensibility/debugger/terminating-a-program.md)  
  
4.  [Criando um ponto de interrupção](../../extensibility/debugger/creating-a-breakpoint.md)  
  
5.  [Quando um ponto de interrupção é associado ou se tornar não associados](../../extensibility/debugger/when-a-breakpoint-binds-or-becomes-unbound.md)  
  
6.  [Erros de ponto de interrupção](../../extensibility/debugger/breakpoint-errors.md)  
  
7.  [Atingindo um ponto de interrupção](../../extensibility/debugger/hitting-a-breakpoint.md)  
  
8.  [Excluindo um ponto de interrupção](../../extensibility/debugger/deleting-a-breakpoint.md)  
  
9. [Entrar no modo de interrupção](../../extensibility/debugger/entering-break-mode.md)  
  
10. [Passo a passo no modo de interrupção](../../extensibility/debugger/stepping-in-break-mode.md)  
  
11. [Avaliação da expressão no modo de interrupção](../../extensibility/debugger/expression-evaluation-in-break-mode.md)  
  
12. [Tratamento de exceções](../../extensibility/debugger/exception-handling-visual-studio-sdk.md)  
  
## <a name="see-also"></a>Consulte também  
 [Criar um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)

