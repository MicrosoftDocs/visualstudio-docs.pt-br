---
title: 'Como: depurar exceções do ASP.NET | Microsoft Docs'
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
helpviewer_keywords:
- debugging [Visual Studio], ASP.NET exceptions
- ASP.NET, exceptions
- exceptions, ASP.NET
ms.assetid: 1810096e-de8c-435e-be3d-f365d0cd0a6a
caps.latest.revision: 26
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3d505e67018c24f659e88401b565011a4c7bea96
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51789207"
---
# <a name="how-to-debug-aspnet-exceptions"></a>Como depurar exceções do ASP.NET
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Depuração de exceções é uma parte importante do desenvolvimento de um robusto [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] aplicativo. Informações gerais sobre como depurar exceções estão na [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md).  
  
 Para depurar sem tratamento [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] exceções, certifique-se de que o depurador é interrompido para elas. O tempo de execução do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] tem um manipulador de exceção de nível superior. Portanto, por padrão, o depurador nunca é interrompido em exceções não tratadas. Para interromper o depurador quando uma exceção é lançada, você deve selecionar **interromper quando uma exceção for: lançada** definindo para essa exceção específica na **exceções** caixa de diálogo.  
  
 Se você tiver habilitado apenas meu código **interromper quando uma exceção for: lançada** não faz com que o depurador para interromper imediatamente se uma exceção é gerada em um método do .NET Framework ou outro código do sistema. Em vez disso, a execução continua até que o depurador atinja código que não seja do sistema, e então é interrompida. Como resultado, você não precisa depurar o código do sistema quando ocorre uma exceção.  
  
 Apenas meu código oferece outra opção que pode ser ainda mais útil: **interromper quando uma exceção for: User-unhandled**. Se você escolher essa configuração para uma exceção, o depurador interromperá a execução no código do usuário, mas apenas se a exceção não for detectada e não for tratada pelo código do usuário. Essa configuração anula o efeito do manipulador de exceção de nível superior do [!INCLUDE[vstecasp](../includes/vstecasp-md.md)], porque esse manipulador está em código de não usuário.  
  
### <a name="to-enable-debugging-of-aspnet-exceptions-with-just-my-code"></a>Para ativar a depuração de exceções do ASP.NET com Apenas Meu Código  
  
1.  Sobre o **Debug** menu, clique em **exceções**.  
  
     O **exceções** caixa de diálogo é exibida.  
  
2.  Sobre o **exceções do Common Language Runtime** linha, selecione **lançada** ou **User-unhandled**.  
  
     Para usar o **User-unhandled** definir, **Just My Code** deve estar habilitado...  
  
### <a name="to-use-best-practices-for-aspnet-exception-handling"></a>Para usar as práticas recomendadas para o tratamento de exceção do ASP.NET  
  
-   Coloque blocos de `try … catch` em torno do código que pode lançar exceções que você pode prever e sabe como manipular. Por exemplo, se o aplicativo está fazendo chamadas para um serviço Web XML ou diretamente em um SQL Server, esse código deve estar em **try... catch** bloqueia porque há várias exceções que podem ocorrer.



