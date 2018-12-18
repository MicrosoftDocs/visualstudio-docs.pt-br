---
title: Introdução ao depurador | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: c763d706-3213-494f-b4d2-990b6e1ec456
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 755c4a0b66c91aa37f96d3d6f06972878ee856b8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51771616"
---
# <a name="getting-started-with-the-debugger"></a>Introdução ao depurador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O depurador do Visual Studio é fácil de usar em qualquer idioma. Aqui, mostraremos como depurar um programa c# simples, mas você pode aplicar as mesmas etapas para o código em outras linguagens como C++ e JavaScript.  
  
##  <a name="BKMK_Start_debugging_a_VS_project"></a> Depurar um projeto c# básico  
 Vamos começar com um simple aplicativo de console em c# (**arquivo / novo / projeto**, em seguida, selecione **Visual c#** e, em seguida, selecione **aplicativo de Console**). Se você nunca trabalhou com o Visual Studio antes, consulte [instruções passo a passo: criar um aplicativo simples](../ide/walkthrough-create-a-simple-application-with-visual-csharp-or-visual-basic.md). O **Main** método apenas adiciona 1 a uma variável de inteiro 10 vezes e imprime o resultado no console:  
  
```csharp  
static void Main(string[] args)  
{  
    int testInt = 0;  
    for (int i = 1; i <= 10; i++)  
    {  
        testInt += 1;  
    }  
    Console.WriteLine(testInt);  
}  
```  
  
 Compilar esse código na **depurar** configuração. Essa configuração é definida por padrão. Para obter mais informações sobre as configurações, consulte [Noções básicas sobre configurações de Build](../ide/understanding-build-configurations.md).  
  
 Execute esse código no depurador clicando **depurar / iniciar depuração** (ou **inicie** na barra de ferramentas, ou **F5**). O aplicativo deve sair quase imediatamente, portanto, você não pode informar se nada foi impresso na janela do Console.  
  
 Você pode interromper a execução de tempo suficiente para ver a janela do Console, definindo um ponto de interrupção e, em seguida, passo a passo à frente. Para definir um ponto de interrupção, coloque o cursor a `Console.WriteLine` de linha e clique em **depurar / novo ponto de interrupção / ponto de interrupção de função**, ou simplesmente clique na margem esquerda na mesma linha. O ponto de interrupção deve ter esta aparência:  
  
 ![Defina um ponto de interrupção](../debugger/media/getstartedbreakpoint.png "GetStartedBreakpoint")  
  
 Para obter mais informações sobre pontos de interrupção, consulte [usando pontos de interrupção](../debugger/using-breakpoints.md).  
  
##  <a name="BKMK_Inspect_Variables"></a> Inspecionar variáveis  
 A depuração geralmente envolve encontrar as variáveis que não contêm os valores esperados em um ponto específico. Mostraremos algumas das maneiras que você pode inspecionar variáveis.  
  
 Inicie a depuração novamente. Interrompe a execução antes do `Console.WriteLine` código é executado. Você pode fazer com que ele execute passo à frente (clique em **Debug / etapa Over** ou **F10**). Nesse caso, você poderia escolher **intervir** (**F11**) e obter o mesmo resultado; vamos explicar a diferença mais tarde. A linha com a última chave de abertura do método deve ter desativado amarela. Examine a janela do Console. Você deve ver **10**.  
  
 É possível focalizar o **testInt** variável para exibir o valor atual em uma dica de dados.  
  
 ![DBG&#95;Basics&#95;Data&#95;Tips](../debugger/media/dbg-basics-data-tips.png "DBG_Basics_Data_Tips")  
  
 A janela de código abaixo, você deverá ver a **Autos**, **Locals**, e **inspeção** windows. Essas janelas mostram os valores atuais das variáveis no momento da execução. Os dois o **Autos** e o **Locals** windows Mostrar **testInt** com um valor de **10**.  
  
 ![Janela Autos durante a depuração](../debugger/media/getstartedwindows.png "GetStartedWindows")  
  
 Para obter mais informações sobre essas janelas, consulte [Autos e locais Windows](../debugger/autos-and-locals-windows.md).  
  
 Vamos ver como o valor da variável é alterado enquanto nós o orientamos por meio do programa. Defina um ponto de interrupção a `testInt += 1;` de linha e reinicie a depuração. Você deve ver que **testInt** no **locais** e **Autos** for windows **0**, e **i** é **1**. Quando você continua a depuração (**depurar / continuam**, ou **continuar** na barra de ferramentas, ou **F5**), você pode ver que o valor de **testInt** muda para **1**, em seguida, **2**e assim por diante. Quando você se cansar de examinar essas alterações, remova o ponto de interrupção (**depurar / ativar/desativar ponto de interrupção**, ou clique na margem) e continuar a depuração. Se você quiser remover todos os pontos de interrupção, clique em **depurar / excluir todos os pontos de interrupção**, ou **CTRL + SHIFT + F9**e clique em **Sim** na caixa de diálogo que pergunta **você deseja remover todos os pontos de interrupção?** .  
  
## <a name="stepping-into-and-over-function-calls"></a>A intervenção em chamadas de função  
 Você pode executar código em que o depurador instrução pela instrução (**intervir**) ou você pode executar o código enquanto o depurador ignora funções (**Step Over**) para obter rapidamente o código que você está mais interessado no ( código de função ainda é executado). Você pode alternar entre os dois métodos na mesma sessão de depuração.  
  
 Para ver a diferença entre **intervir** e **Step Over**, precisamos adicionar um método que é chamado por outro método. Adicione um método para o aplicativo em C# e chamá-la no método Main. O código deve ter esta aparência:  
  
```csharp  
static void Main(string[] args)  
{  
    Method1();  
    Console.WriteLine("end");  
}  
  
private static void Method1()  
{  
    Console.WriteLine("in Method1");  
}  
```  
  
 Defina um ponto de interrupção a `Method1();` chamar o método Main e iniciar a depuração. Quando a execução é interrompida, clique em **depurar / intervir** (ou **intervir** na barra de ferramentas, ou **F11**). Quebras de execução novamente na primeira chave de abertura em Method1:  
  
 ![Depuração em código](../debugger/media/getstartedstepinto.png "GetStartedStepInto")  
  
 Parar a depuração e iniciar novamente e, quando a execução é interrompida no ponto de interrupção, clique em **Debug / etapa Over** (ou **Step Over** na barra de ferramentas, ou **F10**). Novamente, a execução quebra na `Console.WriteLine("end");`.  
  
 Se você quiser saber mais sobre a navegação de código com o depurador, consulte [navegar pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md).





