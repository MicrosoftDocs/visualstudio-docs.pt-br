---
title: Misto de código e informações ausentes na janela pilha de chamadas | Microsoft Docs
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
- SQL
- VB
- CSharp
- C++
helpviewer_keywords:
- managed code, stepping
- Call Stack window, mixed-mode debugging
- Call Stack window, troubleshooting
- native frames
- managed call stacks
- mixed-mode debugging, call stack
- stepping, out of managed code
ms.assetid: dd628427-e8d6-4fc2-b524-9d6393ea5376
caps.latest.revision: 23
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 6f4ae8e527e5f6ce04680c444baad58802bfad48
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51788916"
---
# <a name="mixed-code-and-missing-information-in-the-call-stack-window"></a>Código misto e informações ausentes na janela Pilha de Chamadas
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Devido às diferenças entre as pilhas de chamadas para código gerenciado e nativo, o depurador nem sempre pode mostrar a pilha de chamadas completa quando os tipos de código são misturados. Ao código nativo chama código gerenciado, você pode perceber as seguintes discrepâncias na **pilha de chamadas** janela:  
  
- O quadro nativo imediatamente acima do código gerenciado pode estar ausente dos **pilha de chamadas** janela. Para obter mais informações, consulte [como: sair do código gerenciado quando quadros nativos estiverem ausentes da janela pilha de chamadas](../debugger/how-to-step-out-of-managed-code-when-native-frames-are-missing-from-the-call-stack-window.md).  
  
- Para aplicativos de modo misto iniciados fora do depurador, o **pilha de chamadas** janela pode exibir somente o código gerenciado e nenhum dos quadros nativos estará visível.  
  
  Ambos os casos são razoavelmente incomuns. Na maioria das chamadas nativas para o código gerenciado, as pilhas de chamadas são exibidas corretamente.  
  
## <a name="see-also"></a>Consulte também  
 [Como usar a janela Pilha de Chamadas](../debugger/how-to-use-the-call-stack-window.md)





