---
title: Inspecionar seu aplicativo com o histórico de depuração | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 629b5d93-39b2-430a-b8ba-d2a47fdf2584
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 2309a3213344607fa0f5b2f626fc67af2eff8f79
ms.sourcegitcommit: a749c287ec7d54148505978e8ca55ccd406b71ee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/21/2018
ms.locfileid: "46542332"
---
# <a name="inspect-your-app-with-intellitrace-historical-debugging-in-visual-studio"></a>Inspecionar seu aplicativo com o IntelliTrace histórico de depuração no Visual Studio
Você pode usar [depuração histórica](../debugger/historical-debugging.md) para retroceder e encaminhe por meio da execução do seu aplicativo e inspecionar seu estado.  
  
Você pode usar o IntelliTrace no Visual Studio Enterprise edition, mas não as edições Professional ou Community.  
  
## <a name="navigate-your-code-with-historical-debugging"></a>Navegar pelo código com o histórico de depuração  
 Vamos começar com um programa simples que tem um bug. Em um aplicativo de console em C#, adicione o seguinte código:  
  
```csharp  
static void Main(string[] args)  
{  
    int testInt = 0;  
    int resultInt = AddAll(testInt);  
    Console.WriteLine(resultInt);  
}  
private static int AddAll(int j)  
{  
    for (int i = 0; i < 20; i++)  
    {  
        j = AddInt(j);  
    }  
    return j;  
}  
  
private static int AddInt(int add)  
{  
    if (add == 10)  
    {  
        return add += 25;  
    }  
    return ++add;  
}  
```  
  
 Vamos supor que o valor esperado `resultInt` depois de chamar `AddAll()` é 20 (o resultado de incrementar `testInt` 20 vezes). (Vamos também supor que você não consegue ver o bug no `AddInt()`). Mas o resultado é, na verdade, 44. Como pode localizar o bug sem percorrendo `AddAll()` 10 vezes? Podemos usar depuração histórica para encontrar bugs mais rápido e mais facilmente. Veja como:  
  
1.  Na **Ferramentas > Opções > IntelliTrace > geral**, certifique-se de que o IntelliTrace está habilitado e selecione **eventos do IntelliTrace e informações de chamada**. Se você não selecionar essa opção, você não poderá ver a medianiz de navegação (conforme explicado abaixo).  
  
2.  Defina um ponto de interrupção a `Console.WriteLine(resultInt);` linha.  
  
3.  Inicie a depuração. O código é executado no ponto de interrupção. No **Locals** janela, você pode ver que o valor de `resultInt` é 44.  
  
4.  Abra o **ferramentas de diagnóstico** janela (**Depurar > Mostrar ferramentas de diagnóstico**). A janela de código deve ter esta aparência:  
  
     ![Janela de código no ponto de interrupção](../debugger/media/historicaldebuggingbreakpoint.png "HistoricalDebuggingBreakpoint")  
  
5.  Você deve ver uma seta dupla na margem esquerda, logo acima do ponto de interrupção. Essa área é chamada a medianiz de navegação e é usada para depuração de histórico. Clique na seta.  
  
     Na janela de código, você deverá ver que a linha de código anterior (`int resultInt = AddIterative(testInt);`) é colorido em rosa. Acima da janela, você deve ver uma mensagem que você está agora na depuração histórica.  
  
     A janela de código agora fica assim:  
  
     ![janela de código no modo de depuração histórica](../debugger/media/historicaldebuggingback.png "HistoricalDebuggingBack")  
  
6.  Agora você pode intervir a `AddAll()` método (**F11**, ou o **intervir** botão na medianiz de navegação. Vá para frente (**F10**, ou **ir para próxima chamada** na medianiz de navegação. A linha rosa agora, é o `j = AddInt(j);` linha. **F10** nesse caso, não a etapa para a próxima linha de código. Em vez disso, ele etapas para a próxima chamada de função. Depuração histórica navega de uma chamada e, em seguida, ele ignora as linhas de código que não incluem uma chamada de função.  
  
7.  Entrar agora o `AddInt()` método. Você deve ver o bug nesse código imediatamente.  

## <a name="next-steps"></a>Próximas etapas

Este procedimento apenas uma pequena amostra do que você pode fazer com a depuração histórica.

- Para exibir instantâneos durante a depuração, consulte [inspecionar estados anteriores do aplicativo usando o IntelliTrace](../debugger/view-historical-application-state.md).
- Para obter mais informações sobre as diferentes configurações e os efeitos dos botões diferentes na medianiz de navegação, consulte [recursos do IntelliTrace](../debugger/intellitrace-features.md).