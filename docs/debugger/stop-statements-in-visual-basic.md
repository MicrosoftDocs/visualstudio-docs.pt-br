---
title: Instruções Stop no Visual Basic | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- End statements
- breakpoints, Stop statements
- debugging managed code, Stop statements vs breakpoints
- Stop statements, about Stop statements
- debugging [Visual Basic], Stop statements vs. breakpoints
ms.assetid: 4ad3fe5c-3dfb-4913-b2eb-a0b635751c18
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 74be447f523713cdef9ee5c52876ee0acf4c25b2
ms.sourcegitcommit: 0bf2aff6abe485e3fe940f5344a62a885ad7f44e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2018
ms.locfileid: "37056137"
---
# <a name="stop-statements-in-visual-basic"></a>Instruções Stop no Visual Basic
A instrução Stop do Visual Basic fornece uma alternativa programática ao definir um ponto de interrupção. Quando o depurador encontrar uma instrução Stop, ele interromperá a execução do programa (entra em modo de interrupção). Os programadores de C# podem obter o mesmo efeito usando uma chamada ao System.Diagnostics.Debugger.Break.  
  
 Você define ou remove uma instrução Stop editando o código-fonte. Você não pode definir ou limpar instruções Stop usando os comandos do depurador, como se fosse um ponto de interrupção.  
  
 Ao contrário de uma instrução End, a instrução Stop não redefine variáveis ou retorna você ao modo de design. Você pode escolher Continuar no menu Depurar para continuar a execução do aplicativo.  
  
 Quando executar um aplicativo do Visual Basic fora do depurador, uma instrução Stop iniciará o depurador se a depuração Just-In-Time estiver habilitada. Se a depuração Just-In-Time não estiver habilitada, a instrução Stop se comportará como se fosse uma instrução End, finalizando a execução. Nenhum evento do QueryUnload ou Unload ocorrerá, por isso, você deverá remover todas as instruções Stop da versão de lançamento do aplicativo do Visual Basic. Para obter mais informações, consulte [depuração Just-in-](../debugger/just-in-time-debugging-in-visual-studio.md).  
  
 Para evitar ter que remover as instruções Stop, você pode usar a compilação condicional:  
  
```cpp
#If DEBUG Then  
   Stop  
#Else  
   ' Don't stop  
#End If  
```  
  
 Outra alternativa é usar uma instrução Assert em vez da instrução Stop. Uma instrução Debug.Assert interromperá a execução somente quando uma condição especificada não for atendida e for removida automaticamente ao criar uma versão de lançamento. Para obter mais informações, consulte [asserções em código gerenciado](../debugger/assertions-in-managed-code.md). Se você quiser uma instrução Assert que sempre interrompa a execução na versão de Depuração, você poderá fazer isso:  
  
```csharp
Debug.Assert(false)  
```  
  
 No entanto, outra alternativa é usar o método Debug.Fail:  
  
```csharp
Debug.Fail("a clever output string goes here")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Tipos de projeto do C#, F# e Visual Basic](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)   
 [Depurando código gerenciado](../debugger/debugging-managed-code.md)
