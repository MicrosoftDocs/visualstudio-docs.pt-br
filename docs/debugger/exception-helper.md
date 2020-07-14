---
title: Inspecionar uma exceção – Visual Studio | Microsoft Docs
ms.date: 1/18/2020
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JavaScript
helpviewer_keywords:
- exception helper, debugger, exception
- debugging [Visual Studio], exception helper, Examine an exception
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 75d044ed5ddaf4b7eb7a66bc09c8b3de3502a50f
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350492"
---
# <a name="inspect-an-exception-using-the-exception-helper"></a>Inspecionar uma exceção usando o auxiliar de exceção 

Lidar com exceções é um problema comum, não importa sua tecnologia ou nível de experiência. Pode ser uma experiência frustrante descobrir por que exceções estão causando problemas em seu código. Quando você estiver Depurando uma exceção no Visual Studio, queremos diminuir essa frustração fornecendo informações de exceção relevantes para ajudá-lo a depurar seu problema com mais rapidez.

![Auxiliar de exceção](media/debugger-exception-helper-default.png)

## <a name="pause-on-the-exception"></a>Pausar na exceção
Quando o depurador interrompe uma exceção, um ícone de erro de exceção é exibido à direita dessa linha de código. Um auxiliar de exceção não modal aparecerá próximo ao ícone de exceção.

![Auxiliar de exceção ao lado de uma linha de código](media/debugger-exception-helper-locerror.png)

## <a name="inspect-exception-info"></a>Inspecionar informações de exceção
Você pode ler instantaneamente o tipo de exceção e a mensagem de exceção no auxiliar de exceção e se a exceção foi gerada ou não tratada. Você pode inspecionar e exibir as propriedades do objeto de exceção clicando no link **Exibir detalhes** .

## <a name="analyze-null-references"></a>Analisar referências nulas
A partir do Visual Studio 2017, para o código .net e C/C++, quando você pressiona um `NullReferenceException` ou um `AccessViolation` , você vê informações de análise nulas no auxiliar de exceção. A análise é exibida como texto abaixo da mensagem de exceção. Na ilustração abaixo, as informações são mostradas como "**s** eram nulas.".

![Exceção de análise nula do auxiliar](media/debugger-exception-helper-default.png)


> [!NOTE]
> A análise de referência nula no código gerenciado requer o .NET versão 4.6.2. Atualmente, não há suporte para análise nula para Plataforma Universal do Windows (UWP) e outros aplicativos .NET Core. Ele só está disponível durante a depuração de código que não tem otimizações de código just-in-time (JIT).

## <a name="configure-exception-settings"></a>Definir configurações de exceção 
Você pode configurar o depurador para interromper quando uma exceção do tipo atual for gerada na seção de **configurações de exceção** do auxiliar de exceção. Se o depurador for pausado em uma exceção gerada, você poderá usar a caixa de seleção para desabilitar a interrupção desse tipo de exceção quando for lançado no futuro. Se você não quiser interromper essa exceção em particular quando for gerada neste módulo específico, marque a caixa de seleção pelo nome do módulo em **exceto quando gerada de:** na janela **configurações de exceção** . 

## <a name="inspect-inner-exceptions"></a>Inspecionar exceções internas 
Se a exceção tiver quaisquer exceções internas ([InnerException](https://docs.microsoft.com/dotnet/api/system.exception.innerexception), você poderá exibi-las no auxiliar de exceção. Se houver várias exceções presentes, você poderá navegar entre elas usando as setas para a esquerda e para a direita mostradas acima da pilha de chamadas.

![Auxiliar de exceção com exceção interna](media/debugger-exception-helper-innerexception.png)

## <a name="inspect-rethrown-exceptions"></a>Inspecionar exceções relançadas
Nos casos em que uma exceção foi `thrown` o auxiliar de exceção, mostra a pilha de chamadas desde a primeira vez em que a exceção foi lançada. Se a exceção foi lançada várias vezes, somente a pilha de chamadas da exceção original é mostrada.

![Exceção auxiliar com exceções relançadas](media/debugger-exception-helper-innerexception.png)

## <a name="share-a-debug-session-with-live-share"></a>Compartilhar uma sessão de depuração com Live Share
No auxiliar de exceção, você pode iniciar uma sessão de [Live share](https://docs.microsoft.com/visualstudio/liveshare/) usando o link **Iniciar Live share sessão...**. Qualquer pessoa que ingresse na sessão de Live Share pode ver o auxiliar de exceção junto com outras informações de depuração.
