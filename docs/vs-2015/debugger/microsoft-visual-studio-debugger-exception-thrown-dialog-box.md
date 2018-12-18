---
title: Microsoft Visual Studio (exceção lançada) caixa de diálogo do depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.debug.exceptions.thrown
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- Microsoft Visual Studio Debugger (Exception Thrown) dialog box
- exception handling, during debugging
- debugger, exceptions
- throwing exceptions, during debugging
ms.assetid: 1fe98d10-c8f9-4b39-a920-99169bfd542e
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 851a48bc4573aadfbb89b4e5891a482a29b69e00
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51737834"
---
# <a name="microsoft-visual-studio-debugger-exception-thrown-dialog-box"></a>Caixa de diálogo Depurador do Microsoft Visual Studio (exceção gerada)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Ocorreu uma exceção no seu programa. Esta caixa de diálogo relata o tipo de exceção lançada. Seu código precisa tratar essa exceção. Você pode escolher entre as seguintes opções para tratar a exceção:  
  
 **quebra**  
 Permite que a execução seja interrompida no depurador. O manipulador de exceção não será invocado antes da interrupção. Se você continuar a partir da interrupção, o manipulador de exceção será invocado.  
  
 **Continue**  
 Permite que a execução continue, dando ao manipulador de exceção a possibilidade de tratar a exceção. Essa opção não está disponível para determinados tipos de exceções. **Continuar** permitirá que o aplicativo continuar. Em um aplicativo nativo, ela fará com que a exceção seja relançada. Em um aplicativo gerenciado, ela fará com que o programa seja encerrado ou a exceção seja tratada por um aplicativo de hospedagem.  
  
> [!NOTE]
>  Você não pode continuar depois de uma exceção sem tratamento em código gerenciado. Escolhendo **continuar** depois que uma exceção sem tratamento em código gerenciado faz com que a depuração a parar.  
  
 **Ignorar**  
 Permite que a execução continue sem invocar o manipulador de exceção. Como o manipulador de exceção não é invocado, isso poderá resultar em outras consequências, incluindo erros e exceções adicionais. Essa opção não está disponível para determinados tipos de exceções.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md)   
 [Práticas recomendadas para exceções](http://msdn.microsoft.com/library/f06da765-235b-427a-bfb6-47cd219af539)   
 [Tratamento de Exceção](http://msdn.microsoft.com/library/ccb11fe8-6938-41ac-b477-a183e85865b9)



