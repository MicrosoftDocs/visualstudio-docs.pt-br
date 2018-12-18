---
title: Continuando a execução após uma exceção | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- managed exceptions, continuing execution after
- exceptions, continuing execution after
- debugger, exceptions
- managed code, exception handling
- exception handling, continuing execution after
- execution, continuing after an exception
- program execution
- threading [Visual Studio], continuing execution after exceptions
- Exceptions dialog box
- programs, executing
ms.assetid: 6fe97aac-2131-4615-bd92-d3afee741558
caps.latest.revision: 30
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 947a17993fe0e8366149d1cef79c26c68b11d22a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51730025"
---
# <a name="continuing-execution-after-an-exception"></a>Continuando a execução depois de uma exceção
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando o depurador interrompe a execução devido a uma exceção, uma caixa de diálogo é exibida. Para o Visual Basic ou c#, você verá a [Assistente de exceção](http://msdn.microsoft.com/library/992892ac-9d52-44cc-bf09-b44bfc5befeb) caixa de diálogo, por padrão. Para C++, você verá o mais antigo **exceção** caixa de diálogo. Se você estiver usando o Visual Basic ou c#, mas tiver desabilitado as **Assistente de exceção** na **opções** caixa de diálogo, você verá o **exceção** caixa de diálogo.  
  
 Quando o **Assistente de exceção** ou **exceção** caixa de diálogo for exibida, você pode tentar corrigir o problema que causou a exceção.  
  
## <a name="managed-code"></a>Código gerenciado  
 No código gerenciado, você poderá continuar a execução no mesmo thread após uma exceção não tratada. O **Assistente de exceção** desenrola a pilha de chamadas para o ponto em que a exceção foi lançada.  
  
## <a name="native-code"></a>Código nativo  
 No modo nativo C/C++, você tem duas opções:  
  
-   Você pode clicar em **quebrar** e tentar corrigir o problema. Enquanto você estiver no modo de interrupção, você poderá desenrolar a pilha de chamadas clicando em um quadro na **pilha de chamadas** janela e selecionando **desenrolar para este quadro** no menu de atalho. Quando você continuar a depuração, o **exceção** caixa de diálogo será exibida novamente se você não tiver corrigido o problema. Caso contrário, o **exceção** caixa de diálogo não reaparecerá.  
  
-   Você pode clicar em **continuar** para continuar a execução sem tentar corrigir o problema. O **exceção** caixa de diálogo será exibida novamente.  
  
## <a name="mixed-code"></a>Código misto  
 Se você atinge uma exceção não tratada ao depurar um código nativo misto e gerenciado, as restrições do sistema operacional impedem o desenrolar da pilha de chamadas. Se você tentar voltar a pilha de chamadas usando o menu de atalho, uma mensagem de erro explicará que o depurador não pode desenrolar de uma exceção não tratada exceto durante a depuração de código misto.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md)





