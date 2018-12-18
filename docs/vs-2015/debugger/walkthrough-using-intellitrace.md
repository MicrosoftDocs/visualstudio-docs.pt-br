---
title: 'Passo a passo: Usando o IntelliTrace | Microsoft Docs'
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e1c9c91a-0009-4c4e-9b4f-c9ab3a6022a7
caps.latest.revision: 10
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: cc1e2b40e16a14da505243aeb11542df3adfb18d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51781303"
---
# <a name="walkthrough-using-intellitrace"></a>Passo a passo: usando o IntelliTrace
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o IntelliTrace para coletar informações sobre categorias de eventos ou eventos específicos, ou sobre chamadas de função individuais Além disso, a eventos. Os procedimentos a seguir mostram como fazer isso.  
  
 Você pode usar o IntelliTrace no Visual Studio Enterprise edition (mas não as edições Professional ou Community).  
  
##  <a name="GettingStarted"></a> Usando o IntelliTrace somente com eventos  
 Você pode tentar depurar com apenas eventos do IntelliTrace. Os eventos do IntelliTrace são eventos do depurador, exceções, eventos do .NET Framework e outros eventos do sistema. Você deve ativar ou desativar eventos específicos para controlar os eventos que o IntelliTrace registra antes de iniciar a depuração. Para obter mais informações, consulte [recursos do IntelliTrace](../debugger/intellitrace-features.md).  
  
 As etapas a seguir mostram como depurar com somente eventos do IntelliTrace:  
  
1.  Ative o evento do IntelliTrace para acesso a arquivos. Vá para o **Ferramentas / opções / IntelliTrace / eventos do IntelliTrace** página e, em seguida, expanda o **arquivo** categoria. Verifique as **arquivo** categoria de evento. Isso faz com que todos os arquivos eventos (acessar, fechar, excluir) a ser verificado.  
  
2.  Crie um aplicativo de console C#. No arquivo Program.cs, adicione o seguinte `using` instrução:  
  
    ```csharp  
    using System.IO;  
    ```  
  
3.  Criar um <xref:System.IO.FileStream> no método Main, lê-lo, feche-o e exclua o arquivo. Adicione outra linha apenas para ter um local para definir um ponto de interrupção:  
  
    ```csharp  
    static void Main(string[] args)  
    {  
        FileStream fs = File.Create("WordSearchInputs.txt");  
        fs.ReadByte();  
        fs.Close();  
        File.Delete("WordSearchInputs.txt");  
  
        Console.WriteLine("done");  
    }  
    ```  
  
4.  Definir um ponto de interrupção em `Console.WriteLine("done");`  
  
5.  Inicie a depuração como de costume. (Pressione **F5** ou clique em **depurar / iniciar depuração**.  
  
    > [!TIP]
    >  Manter o **Locals** e **Autos** janelas abertas enquanto você estiver depurando para consultar e registrar os valores nessas janelas.  
  
6.  Interrompe a execução no ponto de interrupção. Se você não vir as **ferramentas de diagnóstico** janela, clique em **depurar / Windows / eventos do IntelliTrace**.  
  
     No **ferramentas de diagnóstico** janela, localizar o **eventos** guia (você deve ver 3 guias, **eventos**, **uso de memória**, e **CPU Uso**). O **eventos** guia mostra uma lista cronológica de eventos, terminando com o último evento antes que o depurador interromper a execução. Você deve ver um evento chamado **WordSearchInputs.txt acesso**.  
  
     Captura de tela a seguir é do Visual Studio 2015 atualização 1.  
  
     ![IntelliTrace&#45;Update1](../debugger/media/intellitrace-update1.png "IntelliTrace-Update1")  
  
7.  Selecione o evento para expandir seus detalhes.  
  
     Captura de tela a seguir é do Visual Studio 2015 atualização 1.  
  
     ![IntelliTraceUpdate1&#45;SingleEvent](../debugger/media/intellitraceupdate1-singleevent.png "IntelliTraceUpdate1 SingleEvent")  
  
     Você pode escolher o link do nome do caminho para abrir o arquivo. Se o nome do caminho completo não estiver disponível, o **abrir arquivo** caixa de diálogo é exibida.  
  
     Clique em **Ativar depuração histórica**, que define contexto do depurador para a hora em que o evento selecionado foi coletado, mostrando os dados históricos na **pilha de chamadas**, **locais** e os outros participantes janelas do depurador. Se o código-fonte estiver disponível, o Visual Studio moverá o ponteiro para o código correspondente na janela de origem para que você possa examiná-lo.  
  
     Captura de tela a seguir é do Visual Studio 2015 atualização 1.  
  
     ![HistoricalDebugging&#45;Update1](../debugger/media/historicaldebugging-update1.png "HistoricalDebugging Update1")  
  
8.  Se você não encontrou o bug, tente examinar outros eventos que levam ao bug. Você também pode ter informações de chamada de registro do IntelliTrace para que você possa passar por chamadas de função.  
  
## <a name="using-intellitrace-with-events-and-function-calls"></a>Usando o IntelliTrace com eventos e chamadas de função  
 O IntelliTrace poderá registrar chamadas de função juntamente com os eventos. Isso permite que você consulte o histórico da pilha de chamadas e retroceda e avance por meio de chamadas em seu código. O IntelliTrace registra dados como nomes de função, pontos de entrada e saída da função e determinados valores de parâmetros e valores de retorno. Ver [recursos do IntelliTrace](../debugger/intellitrace-features.md).  
  
1.  Ative a coleta de chamadas. (No **Ferramentas / opções / IntelliTrace / contabilidade**, selecione **eventos do IntelliTrace e informações de chamada**. IntelliTrace iniciará a coleta dessas informações quando o próxima sessão de depuração é iniciada.  
  
    > [!TIP]
    >  Isso pode reduzir a velocidade de seu aplicativo e aumentar o tamanho de qualquer arquivo de log do IntelliTrace (arquivos. itrace) que você está salvando em disco. Para obter a maioria dos dados de chamada, mas minimizar os efeitos, registrar dados somente dos módulos que lhe interessam. Para alterar o tamanho máximo dos seus arquivos. itrace, vá para **Ferramentas / opções / IntelliTrace / avançados**e especifique a quantidade máxima de espaço em disco. O padrão é 250 MB.  
  
2.  Inicie a depuração do aplicativo de console c# criado na seção anterior. Interrompe a execução no ponto de interrupção. Se você não vir as **ferramentas de diagnóstico** janela, clique em **depurar / Windows / eventos do IntelliTrace**.  
  
3.  Alterne para o **chamadas** guia.  
  
     Agora você vê chamadas de função do seu aplicativo, começando com a chamada de raiz (na solução atual, o ponto de entrada principal) e terminando com o local em que a execução interrompida.  
  
     Selecione uma das chamadas de função e clique duas vezes nele. Você deve ver os pontos de entrada e saída de função, bem como as chamadas que a chamada atual feitas para outras funções e os eventos de IntelliTrace gerados pela chamada. Se você não tiver ativado depuração histórica, essa ação ativa. Para obter mais informações sobre o histórico de depuração, consulte [depuração histórica](../debugger/historical-debugging.md).  
  
    > [!NOTE]
    >  Você pode ver que algumas chamadas estão esmaecidas. Isso ocorre porque o IntelliTrace não registra dados dos módulos correspondentes. Para ver esses dados, com o IntelliTrace colete dados desses módulos. Para obter informações sobre como especificar módulos, consulte [recursos do IntelliTrace](../debugger/intellitrace-features.md).  
  
## <a name="next-steps"></a>Próximas etapas






