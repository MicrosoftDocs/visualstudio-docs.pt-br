---
title: Chamar eventos do depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], events
ms.assetid: b3440ac3-80af-40c6-bef4-cbf00fa67885
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 3ae37a6f6ed180d13623a04afd357efcc109039f
ms.sourcegitcommit: 0e5289414d90a314ca0d560c0c3fe9c88cb2217c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2018
ms.locfileid: "39153027"
---
# <a name="call-debugger-events"></a>Chamar eventos do depurador
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
 [Criando um mecanismo de depuração personalizado](../../extensibility/debugger/creating-a-custom-debug-engine.md)