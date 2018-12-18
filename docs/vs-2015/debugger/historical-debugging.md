---
title: Histórico de depuração | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7cc5ddf2-2f7c-4f83-b7ca-58e92e9bfdd2
caps.latest.revision: 9
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: d43e48b67cdbfabcb38703469f8570f78336dcab
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51794589"
---
# <a name="historical-debugging"></a>Depuração de histórico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Depuração de histórico é um modo de depuração que depende das informações coletadas pelo IntelliTrace. Ele permite que você voltar para encaminhar por meio da execução do seu aplicativo e inspecionar seu estado.  
  
 Você pode usar o IntelliTrace no Visual Studio Enterprise edition (mas não as edições Professional ou Community).  
  
## <a name="why-use-historical-debugging"></a>Por que usar o histórico de depuração?  
 Definir pontos de interrupção para encontrar bugs pode ser uma questão em vez disso, tanto inexata. Você define um ponto de interrupção perto o lugar em seu código onde você suspeitar que o bug seja e executar o aplicativo no depurador e esperança de que seu ponto de interrupção obtém ocorrências e que o local em que a execução quebra pode revelar a origem do erro. Caso contrário, você terá que tente definir um ponto de interrupção em outro lugar no código e execute novamente o depurador, executando as etapas de teste repetidamente até encontrar o problema.  
  
 ![definindo um ponto de interrupção](../debugger/media/breakpointprocesa.png "BreakpointProcesa")  
  
 Você pode usar o IntelliTrace e a depuração histórica circulem por em seu aplicativo e inspecionar o estado (pilha de chamadas e variáveis locais) sem precisar definir pontos de interrupção, reinicie a depuração e repita as etapas de teste. Isso pode economizar muito tempo, especialmente quando o bug estiver localizado profundo em um cenário de teste que leva muito tempo para ser executado.  
  
## <a name="how-do-i-start-using-historical-debugging"></a>Como posso começar a usar a depuração de histórico?  
 IntelliTrace está ativado por padrão. Tudo o que você precisa fazer é decidir quais eventos e chamadas de função são de interesse para você. Para obter mais informações sobre como definir o que você deseja procurar, consulte [recursos do IntelliTrace](../debugger/intellitrace-features.md). Para uma conta de passo a passo de depuração com o IntelliTrace, consulte [instruções passo a passo: usando o IntelliTrace](../debugger/walkthrough-using-intellitrace.md).  
  
## <a name="navigating-your-code-with-historical-debugging"></a>Navegando pelo código com o histórico de depuração  
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
  
1. Em Ferramentas / opções / IntelliTrace / geral, certifique-se de que IntelliTrace estiver habilitado e selecione os eventos do IntelliTrace e informações de opção de chamada. Se você não selecionar essa opção, você não poderá ver a medianiz de navegação (conforme explicado abaixo).  
  
2. Defina um ponto de interrupção a `Console.WriteLine(resultInt);` linha.  
  
3. Inicie a depuração. O código é executado no ponto de interrupção. No **Locals** janela, você pode ver que o valor de `resultInt` é 44.  
  
4. Abra o **ferramentas de diagnóstico** janela (**depurar / Mostrar ferramentas de diagnóstico**). A janela de código deve ter esta aparência:  
  
    ![Janela de código no ponto de interrupção](../debugger/media/historicaldebuggingbreakpoint.png "HistoricalDebuggingBreakpoint")  
  
5. Você deve ver uma seta dupla na margem esquerda, logo acima do ponto de interrupção. Essa área é chamada a medianiz de navegação e é usada para depuração de histórico. Clique na seta.  
  
    Na janela de código, você deverá ver que a linha de código anterior (`int resultInt = AddIterative(testInt);`) é colorido em rosa. Acima da janela, você deve ver uma mensagem que você está agora na depuração histórica.  
  
    A janela de código agora fica assim:  
  
    ![janela de código no modo de depuração histórica](../debugger/media/historicaldebuggingback.png "HistoricalDebuggingBack")  
  
6. Agora você pode intervir a `AddAll()` método (**F11**, ou o **intervir** botão na medianiz de navegação. Vá para frente (**F10**, ou **ir para próxima chamada** na medianiz de navegação. A linha rosa agora, é o `j = AddInt(j);` linha. **F10** nesse caso, não a etapa para a próxima linha de código. Em vez disso, ele etapas para a próxima chamada de função. Depuração histórica navega de uma chamada e, em seguida, ele ignora as linhas de código que não incluem uma chamada de função.  
  
7. Entrar agora o `AddInt()` método. Você deve ver o bug nesse código imediatamente.  
  
   Este procedimento apenas uma pequena amostra do que você pode fazer com a depuração histórica. Para obter mais informações sobre as diferentes configurações e os efeitos dos botões diferentes na medianiz de navegação, consulte [recursos do IntelliTrace](../debugger/intellitrace-features.md).





