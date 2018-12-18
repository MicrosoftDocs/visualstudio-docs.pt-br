---
title: Depurar em tempo de design | Microsoft Docs
ms.custom: seodec18
ms.date: 11/21/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- debugging [Visual Studio], design-time
- breakpoints, design-time debugging
- Immediate window, design-time debugging
- design-time debugging
ms.assetid: 35bfdd2c-6f60-4be1-ba9d-55fce70ee4d8
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: d9c4b0996faf26279ff8018e0e072fd25a33d783
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53063416"
---
# <a name="debug-at-design-time-in-visual-studio-c-c-visual-basic-f"></a>Depurar em tempo de design no Visual Studio (C#, C++, Visual Basic, F#)

Para depurar o código em tempo de design em vez de enquanto um aplicativo está em execução, você pode usar o **imediato** janela. 

Para depurar o código XAML por trás de um aplicativo no designer XAML, como o código de associação de dados, você pode usar **Debug** > **anexar ao processo**.
  
## <a name="use-the-immediate-window"></a>Usar a janela imediata  

Você pode usar o Visual Studio **imediato** janela para executar uma função ou sub-rotina sem executar seu aplicativo. Se a função ou sub-rotina contiver um ponto de interrupção, o Visual Studio interromperá no ponto de interrupção. Então, você poderá usar o depurador do Windows para examinar o estado do programa. Esse recurso é chamado de *depuração em tempo de design*.  

O exemplo a seguir está em Visual Basic. Você também pode usar o **Immediate** em tempo de design na janela de C#, F#e aplicativos em C++.

1. Cole o código a seguir em um aplicativo de console em branco do Visual Basic:  
   
   ```vb  
   Module Module1
   
       Sub Main()
           MySub()
       End Sub
   
       Function MyFunction() As Decimal
           Static i As Integer
           i = i + 1
           Return i
       End Function
   
       Sub MySub()
           MyFunction()
   
       End Sub
   End Module
   ```  
   
1. Defina um ponto de interrupção na linha **End Function**.  
   
1. Abra o **imediato** janela selecionando **Debug** > **Windows** > **imediato**. Tipo de `?MyFunction` na janela e, em seguida, pressione **Enter**.   
   
   O ponto de interrupção é o impacto e o valor de **MyFunction** na **Locals** janela está **1**. Você pode examinar a pilha de chamadas e outras janelas de depuração enquanto o aplicativo estiver no modo de interrupção. 
   
1. Selecione **continuar** na barra de ferramentas do Visual Studio. O aplicativo termina, e **1** é retornado na **imediato** janela. Verifique se que você ainda estiver no modo de design.  
   
1. Tipo de `?MyFunction` no **imediato** janela novamente e pressione **Enter**. O ponto de interrupção é o impacto e o valor de **MyFunction** na **Locals** janela está **2**. 
   
1. Sem selecionar **continuar**, digite `?MySub()` no **imediato** janela e, em seguida, pressione **Enter**. O ponto de interrupção é o impacto e o valor de **MyFunction** na **Locals** janela está **3**. Você pode examinar o estado do aplicativo enquanto o aplicativo estiver no modo de interrupção. 
   
1. Selecione **continuar**. O ponto de interrupção é ocorrências novamente e o valor de **MyFunction** na **Locals** janela agora está **2**. O **Immediate** janela retorna **expressão foi avaliada e não tem nenhum valor**.
   
1. Selecione **continuar** novamente. O aplicativo termina, e **2** é retornado na **imediato** janela. Certifique-se de que você ainda estiver no modo de design.
   
1. Para limpar o conteúdo do **Immediate** janela, o botão direito do mouse na janela e selecione **Limpar tudo**. 

## <a name="attach-to-an-app-from-the-xaml-designer"></a>Anexar a um aplicativo do designer XAML

Em alguns cenários de associação de dados declarativa, ele pode ajudar a depurar o code-behind no designer XAML.

1. No projeto do Visual Studio, adicione uma nova página XAML, como *temp.xaml*. Deixe a nova página XAML vazia. 
   
1. Compile a solução.
   
1. Abra *temp.xaml*, que carrega o designer de XAML *XDesProc.exe*, ou *UwpSurface.exe* em um aplicativo UWP. 
   
1. Abra uma nova instância do Visual Studio. Na nova instância, selecione **Debug** > **anexar ao processo**. 
   
1. No **anexar ao processo** caixa de diálogo, selecione o designer processe do **processos disponíveis** lista.
   
   Para a UWP projetos direcionados ao Windows build 16299 ou acima, é o processo do designer *UwpSurface.exe*. Para WPF ou UWP versões anteriores ao 16299, é o processo do designer *XDesProc.exe*.
   
1. Certifique-se a **anexar** campo é definido como o tipo de código correto para sua versão do .NET, como **código gerenciado (CoreCLR)**. 
   
1. Selecione **anexar**.
   
1. Enquanto conectado ao processo, alterne para a instância do Visual Studio e defina pontos de interrupção em que você deseja depurar o código por trás de seu aplicativo.
   
   Por exemplo, você pode definir um ponto de interrupção no código de conversor de tipo para o XAML a seguir, que associa um TextBlock em tempo de design.
   
    ```xaml
    <TextBlock Text="{Binding title, ConverterParameter=lower, Converter={StaticResource StringFormatConverter}, Mode=TwoWay}"  />
    ```
   Quando a página for carregada, o ponto de interrupção é atingido.
  
## <a name="see-also"></a>Consulte também  
 [Segurança do depurador](../debugger/debugger-security.md)   
 [Noções básicas do depurador](../debugger/getting-started-with-the-debugger.md)
