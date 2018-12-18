---
title: Aplicativos de execução Windows Store no simulador | Microsoft Docs
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
ms.assetid: 81b69bf8-ec87-4bb6-9ad4-1fa7b7802d16
caps.latest.revision: 45
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 504a63d0f99a1a96d1192a1666d45dafde037253
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51775102"
---
# <a name="run-windows-store-apps-in-the-simulator"></a>Executar aplicativos da Windows Store no simulador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O simulador do Visual Studio para aplicativos da Windows Store é um aplicativo da área de trabalho que simula um aplicativo da Windows Store. Você pode executar aplicativos e simule eventos comuns de toque e rotação em seu computador de desenvolvimento. Você também pode escolher o tamanho da tela física e a resolução que você deseja emular e simular propriedades de conexão de rede.  
  
 O simulador fornece um ambiente no qual você pode criar, desenvolver, depurar e testar aplicativos da Windows Store. No entanto, antes de publicar um aplicativo na Windows Store, convém testá-lo em um dispositivo real.  
  
 O simulador do Visual Studio para aplicativos da Windows Store não é executado em um ambiente isolado na máquina local. Portanto, os erros que ocorrem no simulador, como um erro não recuperável geral do sistema, também podem afetar o computador inteiro.  
  
 Ver [aplicativos de execução do Windows Phone no emulador](../debugger/run-windows-phone-apps-in-the-emulator.md) para obter informações do Windows Phone.  
  
> [!IMPORTANT]
>  O simulador do Visual Studio 2015 não inclui o botão de localização geográfica. Isso ocorre porque o simulador do Windows 10 não inclui a simulação de localização geográfica. Se você precisar fazer esse tipo de simulação, você pode usar o simulador do Visual Studio 2013 no Windows 8.1 ou sistemas operacionais anteriores.  
  
##  <a name="BKMK_Set_the_simulator_as_the_target"></a> Definir o simulador como o destino  
 Para executar seu aplicativo da Windows Store no simulador, selecione **simulador** na lista suspensa lista ao lado de **iniciar depuração** botão no depurador **padrão** barra de ferramentas.  
  
 ![Em execução no simulador](../debugger/media/vsrun-f5-simulator.png "VSRUN_F5_Simulator")  
  
##  <a name="BKMK_Choose_an_interaction_mode"></a> Escolher um modo de interação  
 Você pode escolher os seguintes modos de interação  
  
-   ![Botão de modo do mouse](../debugger/media/simulator-mousemodebtn.png "SIMULATOR_MouseModeBtn") modo do Mouse: define o modo de interação para gestos do mouse. Esses gestos incluem cliques, cliques duplos e arrastos.  
  
-   ![Botão de emulação de toque iniciar](../debugger/media/simulator-starttouchemulationbtn.png "SIMULATOR_StartTouchEmulationBtn") iniciar emulação de toque: define o modo de interação para gestos de um único dedo com. Os eventos desse tipo incluem tocar, arrastar e passar o dedo.  
  
     ![Destino de um dedo Simulator](../debugger/media/simulator-onefinger.png "SIMULATOR_OneFinger") o ícone de alvo único indica o local dos eventos no simulador. Use o mouse para posicionar o ponteiro.  
  
     ![Destino de toque de um dedo](../debugger/media/simulator-onefingerengaged.png "SIMULATOR_OneFingerEngaged") pressione o botão esquerdo do mouse para ativar o modo de toque. Por exemplo, clique no botão para simular um gesto de tocar, ou pressione e segure o botão enquanto você arrasta ou passa o dedo.  
  
## <a name="pinch-and-zoom"></a>Aperto e zoom  
 Defina o modo de interação como sendo gestos de aperto e zoom com dois dedos.  
  
-   ![Destino de dedo Siimulator duas](../debugger/media/simulator-twofinger.png "SIMULATOR_TwoFinger")  
  
     O ícone de alvo duplo indica o local de dois dedos na tela do dispositivo.  
  
    -   Mova o mouse para posicionar os ícones sobre o objeto na tela do dispositivo.  
  
    -   Gire a roda do mouse para trás ou para a frente a fim de alterar a distância simulada dos dois dedos antes de apertar ou aplicar zoom.  
  
-   -   ![Aperto, zoom e girar destinos](../debugger/media/simulator-twofingerengaged.png "SIMULATOR_TwoFingerEngaged")  
  
         Pressione o botão esquerdo e gire a roda para trás (na sua direção) a fim de ampliar a exibição (aperto).  
  
    -   Pressione o botão esquerdo e gire a roda do mouse para a frente (afastada de você) a fim de reduzir a exibição (zoom).  
  
## <a name="object-rotation"></a>Rotação de objeto  
 O **rotação da emulação de toque** botão define o modo de interação para gestos de rotação usando dois dedos.  
  
-   -   Mova o mouse para posicionar os ícones sobre o objeto na tela do dispositivo.  
  
    -   Gire a roda do mouse para trás ou para frente para alterar a orientação simulada dos dois dedos antes de girar o objeto.  
  
-   -   Pressione o botão esquerdo e gire a roda para trás (na sua direção) a fim de girar o objeto no sentido anti-horário. Conforme você gira a roda do mouse, um dos dois ícones de alvo gira em torno do outro para indicar o tamanho relativo da rotação.  
  
    -   Pressione o botão esquerdo e gire a roda do mouse para a frente (afastada de você) a fim de girar o objeto no sentido horário.  
  
##  <a name="BKMK_Enable_or_disable_Always_on_top_mode"></a> Habilitar ou desabilitar o AlwaysOn modo superior  
 Você pode configurar a janela do simulador para ficar sempre por cima das outras janelas. O **alternar janela superior** botão habilita ou desabilita a **sempre visível** modo da janela do simulador.  
  
##  <a name="BKMK_Change_the_device_orientation"></a> Alterar a orientação do dispositivo  
 Você pode alternar a orientação do dispositivo entre retrato e paisagem girando o simulador 90 graus em qualquer direção.  
  
> [!NOTE]
>  O simulador não respeita [Displayproperties](http://go.microsoft.com/fwlink/?LinkId=249460) propriedade de um projeto. Por exemplo, se o projeto define a orientação como `Landscape` e você gira o simulador até a orientação retrato, a imagem de exibição do simulador também é girada e redimensionada. Teste essas configurações em um dispositivo real.  
  
> [!NOTE]
>  Se você gira o simulador de modo que uma borda dele fica maior do que a tela em que ele é exibido, o simulador é automaticamente redimensionado para caber na tela. O simulador não é redimensionado para o tamanho original se você o gira novamente.  
  
##  <a name="BKMK_Change_the_simulated_screen_size_and_resolution"></a> Alterar o tamanho de tela simulados e a resolução  
 Para alterar o tamanho de tela simulados e a resolução, escolha o **alterar resolução** botão na paleta e escolha um novo tamanho e resolução na lista.  
  
 O tamanho da tela e a resolução são listados como *polegadas de largura de tela, a altura de pixel de largura X do pixel*. Observe que tanto o tamanho como a resolução da tela são simulados. As coordenadas de local no simulador são convertidas nas coordenadas do tamanho e da resolução do dispositivo selecionado.  
  
> [!NOTE]
>  Você pode salvar versões dimensionadas de imagens de bitmap em seu aplicativo, e o Windows carregará a imagem correta para a escala atual. Para obter mais informações, consulte [101 de Design responsivo](https://msdn.microsoft.com/library/windows/apps/dn958435.aspx). No entanto, se você alterar a resolução do simulador de modo que o Windows selecione uma imagem diferente para ajustar à resolução, será preciso parar e reiniciar a sessão de depuração para exibir a nova imagem.  
  
##  <a name="BKMK_Capture_a_screenshot_of_your_app_for_submission_to_the_Microsoft_Store"></a> Uma captura de tela do seu aplicativo para envio para a Windows Store  
 Quando você envia um aplicativo na app Store do Windows, você deve incluir capturas de tela do aplicativo.  
  
> [!NOTE]
>  A captura de tela é salva na resolução atual do simulador. Para alterar a resolução, escolha o **alterar resolução** botão.  
  
-   Para criar capturas de tela de seu aplicativo de simulador, escolha o **captura de tela na área de transferência** botão.  
  
-   Para definir o local onde se encontram as capturas de tela, escolha o **configurações de captura de tela** botão e escolha o local no menu de atalho.  
  
     ![Menu de contexto de configurações de captura de tela](../debugger/media/simulator-screenshotsettingscntxmnu.png "SIMULATOR_ScreenShotSettingsCntxMnu")  
  
##  <a name="BKMK_Simulate_network_connection_properties"></a> Simular propriedades de conexão de rede  
 Você pode ajudar os usuários de seu aplicativo a gerenciar o custo de conexões de rede limitadas mantendo a percepção do custo da conexão de rede ou as alterações de status do plano de dados e habilitando o aplicativo para usar essas informações para evitar a cobrança de custos adicionais para roaming ou exceder um limite especificado de transferência de dados. O [Windows.Networking.Connectivity](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.aspx) APIs permitem que você responda aos [NetworkStatusChanged](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.networkinformation.networkstatuschanged.aspx) e [TriggerType](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.background.systemtrigger.triggertype.aspx) eventos que assinar. Ver [guia de início rápido: restrições de custo de gerenciamento de rede limitada](http://msdn.microsoft.com/library/windows/apps/Hh750310.aspx).  
  
 Para depurar ou testar seu código com reconhecimento de custo de rede, o simulador pode imitar as propriedades de uma rede que são expostas por meio de [ConnectionProfile](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectionprofile.aspx) objeto retornado por [GetInternetConnectionProfile](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.networkinformation.getinternetconnectionprofile.aspx)...  
  
 Para simular propriedades de rede:  
  
1. Na barra de ferramentas do simulador, escolha o **alterar propriedades da rede** botão.  
  
2. Sobre o **definir propriedades de rede** caixa de diálogo, selecione **uso simulado propriedades de rede**.  
  
    Desmarque a caixa de seleção para remover a simulação e retornar às propriedades de rede da interface atualmente conectada.  
  
3. Insira um **nome do perfil** para a rede simulada. É recomendável usar um nome exclusivo que você pode usar para identificar a simulação na [ProfileName](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectionprofile.profilename.aspx) propriedade da [ConnectionProfile](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectionprofile.aspx) objeto.  
  
4. Selecione o [NetworkCostType](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.networkcosttype.aspx) valor para o perfil da **tipo de custo de rede** lista.  
  
5. Dos **sinalizador de Status de limite de dados** lista, você pode definir o [ApproachingDataLimit](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectioncost.approachingdatalimit.aspx) propriedade ou o [OverDataLimit](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectioncost.overdatalimit.aspx)propriedade como true, ou você pode escolher  **Abaixo do limite de dados** para definir os dois valores como false.  
  
6. Dos **estado de Roaming** lista, defina as [Roaming](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.connectioncost.roaming.aspx) propriedade.  
  
7. Escolher **propriedades do conjunto** para simular as propriedades de rede Disparando um primeiro plano [NetworkStatusChanged](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.networkinformation.networkstatuschanged.aspx) eventos e um plano de fundo [SystemTrigger](https://msdn.microsoft.com/library/windows/apps/windows.applicationmodel.background.systemtrigger.aspx) do tipo  **NetworkStateChange**.  
  
   **Para obter mais informações sobre como gerenciar conexões de rede**  
  
   [Guia de início rápido: Gerenciando monitorados restrições de custo de rede](http://msdn.microsoft.com/library/windows/apps/Hh750310.aspx)  
  
   [Exemplo de informações de rede](http://code.msdn.microsoft.com/windowsapps/Network-Information-Sample-63aaa201)  
  
   [Analisar o uso de energia](../profiling/analyze-energy-use-in-store-apps.md)  
  
   [Windows.Networking.Connectivity](https://msdn.microsoft.com/library/windows/apps/windows.networking.connectivity.aspx)  
  
   [Como responder a eventos do sistema com tarefas em segundo plano](http://msdn.microsoft.com/en-us/f7c86e86-a7ae-4abb-a923-76b03337a80a)  
  
   [Como disparar suspender, continuar e eventos em aplicativos da Windows Store em segundo plano](http://msdn.microsoft.com/library/windows/apps/hh974425.aspx)  
  
##  <a name="BKMK_Navigate_the_simulator_with_the_keyboard"></a> Navegar no simulador com o teclado  
 Você pode navegar a barra de ferramentas do simulador pressionando **CTRL + ALT + seta acima** para alternar o foco da janela do simulador na barra de ferramentas do simulador. Use o **seta para cima** e o **seta para baixo** para mover entre os botões da barra de ferramentas.  
  
 Você pode desligar o simulador pressionando **CTRL + ALT + F4**.  
  
## <a name="see-also"></a>Consulte também  
 [Executar aplicativos usando o Visual Studio](../debugger/run-store-apps-from-visual-studio.md)



