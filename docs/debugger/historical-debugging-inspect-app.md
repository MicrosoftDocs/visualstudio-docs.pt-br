---
title: Inspecione seu aplicativo com a depuração histórica | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 629b5d93-39b2-430a-b8ba-d2a47fdf2584
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: efabc8cd185daed4f018e3e4209e391b5bc39f44
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350440"
---
# <a name="inspect-your-app-with-intellitrace-historical-debugging-in-visual-studio-c-visual-basic-c"></a>Inspecione seu aplicativo com a depuração histórica do IntelliTrace no Visual Studio (C#, Visual Basic, C++)

Você pode usar a [depuração histórica](../debugger/historical-debugging.md) para retroceder e avançar pela execução do seu aplicativo e inspecionar seu estado.

Você pode usar o IntelliTrace no Visual Studio Enterprise Edition, mas não as edições Professional ou Community.

## <a name="navigate-your-code-with-historical-debugging"></a>Navegar pelo seu código com a depuração histórica

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

Vamos pressupor que o valor esperado de `resultInt` após a chamada `AddAll()` seja 20 (o resultado de incrementos `testInt` 20 vezes). (Também vamos supor que você não consiga ver o bug no `AddInt()` ). Mas o resultado é, na verdade, 44. Como podemos encontrar o bug sem passar por `AddAll()` 10 vezes? Podemos usar a depuração histórica para encontrar o bug com mais rapidez e facilidade. Veja como:

1. Em **ferramentas > opções > intellitrace > geral**, verifique se o IntelliTrace está habilitado e selecione **eventos do IntelliTrace e informações de chamada**. Se você não selecionar essa opção, não será possível ver a medianiz de navegação (conforme explicado abaixo).

2. Defina um ponto de interrupção na linha `Console.WriteLine(resultInt);`.

3. Inicie a depuração. O código é executado para o ponto de interrupção. Na janela **locais** , você pode ver que o valor de `resultInt` é 44.

4. Abra a janela de **ferramentas de diagnóstico** (**depurar > mostrar ferramentas de diagnóstico**). A janela de código deve ter a seguinte aparência:

    ![Janela de código no ponto de interrupção](../debugger/media/historicaldebuggingbreakpoint.png "HistoricalDebuggingBreakpoint")

5. Você deve ver uma seta dupla ao lado da margem esquerda, logo acima do ponto de interrupção. Essa área é chamada de medianiz de navegação e é usada para depuração histórica. Clique na seta.

    Na janela de código, você verá que a linha de código anterior ( `int resultInt = AddIterative(testInt);` ) é cor rosa. Acima da janela, você verá uma mensagem informando que agora está na depuração histórica.

    A janela de código agora tem esta aparência:

    ![janela de código no modo de depuração histórica](../debugger/media/historicaldebuggingback.png "HistoricalDebuggingBack")

6. Agora você pode entrar no `AddAll()` método (**F11**ou no botão entrar **Step Into** na medianiz de navegação. Avançar (**F10**ou **ir para próxima chamada** na medianiz de navegação. A linha rosa está agora na `j = AddInt(j);` linha. O **F10** , nesse caso, não faz a etapa para a próxima linha de código. Em vez disso, ele percorre a próxima chamada de função. A depuração histórica navega da chamada para chamada e ignora as linhas de código que não incluem uma chamada de função.

7. Agora, percorra o `AddInt()` método. Você deve ver o bug neste código imediatamente.

## <a name="next-steps"></a>Próximas etapas

Esse procedimento apenas arranha a superfície do que você pode fazer com a depuração histórica.

- Para exibir instantâneos durante a depuração, consulte [inspecionar os Estados de aplicativos anteriores usando o IntelliTrace](../debugger/view-historical-application-state.md).
- Para saber mais sobre as diferentes configurações e os efeitos dos diferentes botões na medianiz de navegação, consulte recursos do [IntelliTrace](../debugger/intellitrace-features.md).
