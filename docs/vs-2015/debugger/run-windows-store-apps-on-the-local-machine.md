---
title: Aplicativos de execução Windows Store no computador local | Microsoft Docs
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
ms.assetid: e42a21a8-6423-4caf-b4dc-72b263e76019
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 40fafcbdacac8a63a4aba70526a473d091b35de8
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51766835"
---
# <a name="run-windows-store-apps-on-the-local-machine"></a>Executar aplicativos da Windows Store na máquina local
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows apenas] (... /Image/windows_only_content.png "windows_only_content")  
  
 Para depurar, testar ou executar análise de desempenho em um aplicativo da Windows Store, você pode executar o aplicativo no mesmo computador host do Visual Studio. Se a tela do dispositivo for habilitada para toque, você poderá ativar a funcionalidade completa do aplicativo; do contrário, você estará limitado aos gestos do mouse e do teclado.  
  
##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 Você aprende sobre:  
  
 [Como executar em um computador local](#BKMK_How_to_run_on_a_local_machine)  
  
 [Como alternar entre um aplicativo da Windows Store e o Visual Studio em um único monitor](#BKMK_How_to_switch_between_a_Windows_Store_app_and_Visual_Studio_on_a_single_monitor)  
  
##  <a name="BKMK_How_to_run_on_a_local_machine"></a> Como executar em um computador local  
 Para executar o aplicativo no computador local, selecione **computador Local** na lista suspensa ao lado do botão Iniciar depuração no depurador **Standard** barra de ferramentas.  
  
 ![Executar no computador Local](../debugger/media/vsrun-f5-local.png "VSRUN_F5_Local")  
  
 Se você não conseguir ver a **Standard** barra de ferramentas, clique no **exibição** , aponte para **barras de ferramentas**e, em seguida, clique em **padrão**.  
  
 A escolha que você faz na lista suspensa persiste no arquivo de propriedades do projeto e se torna o destino de execução padrão.  
  
 Você também pode definir o destino de execução diretamente no arquivo de propriedades do projeto. Clique com botão direito no nome do projeto no **Gerenciador de soluções** e, em seguida, escolha **propriedades**. Siga um destes procedimentos:  
  
-   Em projetos c# e Visual Basic, clique em **Debug** e, em seguida, selecione **Máquina Local** do **dispositivo de destino** lista suspensa.  
  
     ![C&#35; e a página de propriedades de projeto do Visual Basic](../debugger/media/vsrun-cs-vb-projprop-local.png "VSRUN_CS_VB_ProjProp_Local")  
  
-   Em projetos do C++ e JavaScript, expanda o **propriedades de configuração** nó, clique em **depuração**e, em seguida, selecione **depurador Local** do **depurador para iniciar** lista.  
  
     ![C&#43; &#43; e a página de propriedades do projeto de JavaScript](../debugger/media/vsrun-cpp-js-projprop-local.png "VSRUN_CPP_JS_ProjProp_Local")  
  
##  <a name="BKMK_How_to_switch_between_a_Windows_Store_app_and_Visual_Studio_on_a_single_monitor"></a> Como alternar entre um aplicativo da Windows Store e o Visual Studio em um único monitor  
 **Para alternar de uma instância em execução de um aplicativo da Windows Store para Visual Studio**  
  
 Quando você executa um aplicativo da Windows Store em um computador local e usa apenas um único monitor, você pode querer alternar para o Visual Studio enquanto deixa o aplicativo em execução. Por exemplo, o aplicativo pode estar em um estado que não pode ser alcançado por um ponto de interrupção, como esperar por um evento ou estar preso em um loop extenso ou sem fim. Para retornar ao Visual Studio, pressione ALT+TAB.



