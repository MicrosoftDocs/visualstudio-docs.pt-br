---
title: 'Como: depurar exceções ASP.NET | Microsoft Docs'
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
- debugging [Visual Studio], ASP.NET exceptions
- ASP.NET, exceptions
- exceptions, ASP.NET
ms.assetid: 1810096e-de8c-435e-be3d-f365d0cd0a6a
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 5923818e93170ded1f857ac20d42cd6134aed5d3
ms.sourcegitcommit: 3d10b93eb5b326639f3e5c19b9e6a8d1ba078de1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
ms.locfileid: "31476150"
---
# <a name="how-to-debug-aspnet-exceptions"></a>Como depurar exceções do ASP.NET
Exceções de depuração é uma parte importante do desenvolvimento de um robusto [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] aplicativo. Informações gerais sobre como depurar exceções estão no [Gerenciando exceções com o depurador](../debugger/managing-exceptions-with-the-debugger.md).  
  
 Para depurar sem tratamento [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] exceções, você deve ter certeza de que o depurador interrompe para eles. O tempo de execução do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] tem um manipulador de exceção de nível superior. Portanto, por padrão, o depurador nunca é interrompido em exceções não tratadas. Para interromper o depurador quando uma exceção é gerada, você deve selecionar **interromper quando uma exceção é: gerada** definindo esta exceção específica no **exceções** caixa de diálogo.  
  
 Se você tiver habilitado apenas meu código **interromper quando uma exceção é: gerada** não faz com que o depurador para interromper imediatamente se uma exceção será lançada em um método do .NET Framework ou outro código do sistema. Em vez disso, a execução continua até que o depurador atinja código que não seja do sistema, e então é interrompida. Como resultado, você não precisa depurar o código do sistema quando ocorre uma exceção.  
  
 Apenas meu código oferece outra opção que pode ser ainda mais útil: **interromper quando uma exceção é: sem tratamento do usuário**. Se você escolher essa configuração para uma exceção, o depurador interromperá a execução no código do usuário, mas apenas se a exceção não for detectada e não for tratada pelo código do usuário. Essa configuração anula o efeito do manipulador de exceção de nível superior do [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)], porque esse manipulador está em código de não usuário.  
  
### <a name="to-enable-debugging-of-aspnet-exceptions-with-just-my-code"></a>Para ativar a depuração de exceções do ASP.NET com Apenas Meu Código  
  
1.  Sobre o **depurar** menu, clique em **exceções**.  
  
     O **exceções** caixa de diálogo é exibida.  
  
2.  Sobre o **exceções do Common Language Runtime** linha, selecione **Thrown** ou **manipulado pelo usuário**.  
  
     Para usar o **manipulado pelo usuário** configuração, **Just My Code** deve ser habilitado.  
  
### <a name="to-use-best-practices-for-aspnet-exception-handling"></a>Para usar as práticas recomendadas para o tratamento de exceção do ASP.NET  
  
-   Coloque blocos de `try ... catch` em torno do código que pode lançar exceções que você pode prever e sabe como manipular. Por exemplo, se o aplicativo está fazendo chamadas para um serviço Web XML ou diretamente em um SQL Server, esse código deve estar em **try... catch** bloqueia porque há várias exceções que podem ocorrer.

## <a name="see-also"></a>Consulte também
[Depurar aplicativos ASP.NET](../debugger/how-to-enable-debugging-for-aspnet-applications.md)