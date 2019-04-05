---
title: Instruções Stop no Visual Basic | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
- VB
helpviewer_keywords:
- End statements
- breakpoints, Stop statements
- debugging managed code, Stop statements vs breakpoints
- Stop statements, about Stop statements
- debugging [Visual Basic], Stop statements vs. breakpoints
ms.assetid: 4ad3fe5c-3dfb-4913-b2eb-a0b635751c18
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8f2749ef9a6cfd310da5da832a283b55b6af59a6
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "58927164"
---
# <a name="stop-statements-in-visual-basic"></a>Instruções Stop no Visual Basic
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

A instrução Stop do Visual Basic fornece uma alternativa programática ao definir um ponto de interrupção. Quando o depurador encontrar uma instrução Stop, ele interromperá a execução do programa (entra em modo de interrupção). Os programadores de C# podem obter o mesmo efeito usando uma chamada ao System.Diagnostics.Debugger.Break.  
  
 Você define ou remove uma instrução Stop editando o código-fonte. Você não pode definir ou limpar instruções Stop usando os comandos do depurador, como se fosse um ponto de interrupção.  
  
 Ao contrário de uma instrução End, a instrução Stop não redefine variáveis ou retorna você ao modo de design. Você pode escolher Continuar no menu Depurar para continuar a execução do aplicativo.  
  
 Quando executar um aplicativo do Visual Basic fora do depurador, uma instrução Stop iniciará o depurador se a depuração Just-In-Time estiver habilitada. Se a depuração Just-In-Time não estiver habilitada, a instrução Stop se comportará como se fosse uma instrução End, finalizando a execução. Nenhum evento do QueryUnload ou Unload ocorrerá, por isso, você deverá remover todas as instruções Stop da versão de lançamento do aplicativo do Visual Basic. Para obter mais informações, confira [Depuração Just-In-Time](../debugger/just-in-time-debugging-in-visual-studio.md).  
  
 Para evitar ter que remover as instruções Stop, você pode usar a compilação condicional:  
  
```  
#If DEBUG Then  
   Stop  
#Else  
   ' Don't stop  
#End If  
```  
  
 Outra alternativa é usar uma instrução Assert em vez da instrução Stop. Uma instrução Debug.Assert interromperá a execução somente quando uma condição especificada não for atendida e for removida automaticamente ao criar uma versão de lançamento. Para obter mais informações, confira [Asserções em código gerenciado](../debugger/assertions-in-managed-code.md). Se você quiser uma instrução Assert que sempre interrompa a execução na versão de Depuração, você poderá fazer isso:  
  
```  
Debug.Assert(false)  
```  
  
 No entanto, outra alternativa é usar o método Debug.Fail:  
  
```  
Debug.Fail("a clever output string goes here")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Tipos de projeto do C#, F# e Visual Basic](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)
