---
title: Executar aplicativos UWP no simulador | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 81b69bf8-ec87-4bb6-9ad4-1fa7b7802d16
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: f8d1ae730947a70cac253866d0257aa4e0216626
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49882763"
---
# <a name="run-uwp-apps-in-the-simulator"></a>Executar aplicativos UWP no simulador
O simulador do Visual Studio para aplicativos UWP é um aplicativo da área de trabalho que simula um aplicativo UWP. Normalmente, convém depurar no computador local, um dispositivo conectado ou um computador remoto. No entanto, em alguns cenários, você talvez queira usar o simulador do Visual Studio para emular um tamanho da tela física diferente e resolução. Você também pode simular eventos comuns de toque e rotação e simular propriedades de conexão de rede.
  
 O simulador fornece um ambiente no qual você pode criar, desenvolver, depurar e testar aplicativos UWP. No entanto, antes de publicar seu aplicativo Microsoft Store, você deve testar seu aplicativo em um dispositivo real.  
  
 O simulador do Visual Studio para aplicativos UWP não é executado em um ambiente isolado em seu computador local. Portanto, os erros que ocorrem no simulador, como um erro não recuperável geral do sistema, também podem afetar o computador inteiro.  
  
> [!IMPORTANT]
>  O simulador do Visual Studio 2015 não inclui o botão de localização geográfica. Isso ocorre porque o simulador do Windows 10 não inclui a simulação de localização geográfica.
  
##  <a name="BKMK_Set_the_simulator_as_the_target"></a> Definir o simulador como o destino  
 Para executar seu aplicativo UWP no simulador, selecione **simulador** na lista suspensa lista ao lado de **iniciar depuração** botão no depurador **padrão** barra de ferramentas. Essa opção só estará disponível se seu aplicativo **mínima da plataforma de destino. Versão** é menor que ou igual ao sistema operacional no computador de desenvolvimento. 
  
 ![Em execução no simulador](../debugger/media/vsrun_f5_simulator.png "VSRUN_F5_Simulator")  
  
##  <a name="BKMK_Choose_an_interaction_mode"></a> Escolher um modo de interação  
 Você pode escolher os seguintes modos de interação  
  
-   ![Botão de modo do mouse](../debugger/media/simulator_mousemodebtn.png "SIMULATOR_MouseModeBtn") modo do Mouse: define o modo de interação para gestos do mouse. Esses gestos incluem cliques, cliques duplos e arrastos.  
  
-   ![Botão de emulação de toque iniciar](../debugger/media/simulator_starttouchemulationbtn.png "SIMULATOR_StartTouchEmulationBtn") iniciar emulação de toque: define o modo de interação para gestos de um único dedo com. Os eventos desse tipo incluem tocar, arrastar e passar o dedo.  
  
     ![Destino de um dedo Simulator](../debugger/media/simulator_onefinger.png "SIMULATOR_OneFinger") o ícone de alvo único indica o local dos eventos no simulador. Use o mouse para posicionar o ponteiro.  
  
     ![Destino de toque de um dedo](../debugger/media/simulator_onefingerengaged.png "SIMULATOR_OneFingerEngaged") pressione o botão esquerdo do mouse para ativar o modo de toque. Por exemplo, clique no botão para simular um gesto de tocar, ou pressione e segure o botão enquanto você arrasta ou passa o dedo.  
  
## <a name="pinch-and-zoom"></a>Aperto e zoom  
 Defina o modo de interação como sendo gestos de aperto e zoom com dois dedos.  
  
-   ![Destino de dedo Siimulator duas](../debugger/media/simulator_twofinger.png "SIMULATOR_TwoFinger")  
  
     O ícone de alvo duplo indica o local de dois dedos na tela do dispositivo.  
  
    -   Mova o mouse para posicionar os ícones sobre o objeto na tela do dispositivo.  
  
    -   Gire a roda do mouse para trás ou para a frente a fim de alterar a distância simulada dos dois dedos antes de apertar ou aplicar zoom.  
  
-   -   ![Aperto, zoom e girar destinos](../debugger/media/simulator_twofingerengaged.png "SIMULATOR_TwoFingerEngaged")  
  
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
>  Você pode salvar versões dimensionadas de imagens de bitmap em seu aplicativo, e o Windows carregará a imagem correta para a escala atual. Para obter mais informações, consulte [introdução de Design e da interface do usuário](/windows/uwp/layout/design-and-ui-intro). No entanto, se você alterar a resolução do simulador de modo que o Windows selecione uma imagem diferente para ajustar à resolução, será preciso parar e reiniciar a sessão de depuração para exibir a nova imagem.  
  
##  <a name="BKMK_Capture_a_screenshot_of_your_app_for_submission_to_the_Microsoft_Store"></a> Uma captura de tela de seu aplicativo para enviar à Microsoft Store  
 Quando você envia um aplicativo à Microsoft Store, você deve incluir capturas de tela do aplicativo.  
  
> [!NOTE]
>  A captura de tela é salva na resolução atual do simulador. Para alterar a resolução, escolha o **alterar resolução** botão.  
  
-   Para criar capturas de tela de seu aplicativo de simulador, escolha o **captura de tela na área de transferência** botão.  
  
-   Para definir o local onde se encontram as capturas de tela, escolha o **configurações de captura de tela** botão e escolha o local no menu de atalho.  
  
     ![Menu de contexto de configurações de captura de tela](../debugger/media/simulator_screenshotsettingscntxmnu.png "SIMULATOR_ScreenShotSettingsCntxMnu")  
  
##  <a name="BKMK_Simulate_network_connection_properties"></a> Simular propriedades de conexão de rede  
 Você pode ajudar os usuários do seu aplicativo a gerenciar o custo de conexões de rede limitadas mantendo o reconhecimento de rede conexão custo ou dados plano das alterações de status e habilitando o aplicativo para usar essas informações para evitar incorrer em custos adicionais para roaming ou exceder um limite de transferência de dados especificado. O [Windows.Networking.Connectivity](/uwp/api/windows.networking.connectivity) APIs permitem que você responda aos [NetworkStatusChanged](/uwp/api/windows.networking.connectivity.networkinformation) e [TriggerType](/uwp/api/windows.applicationmodel.background.systemtrigger) eventos que assinar. Ver [guia de início rápido: restrições de custo de gerenciamento de rede limitada](https://msdn.microsoft.com/library/windows/apps/Hh750310.aspx).  
  
 Para depurar ou testar seu código com reconhecimento de custo de rede, o simulador pode imitar as propriedades de uma rede que são expostas por meio de [ConnectionProfile](/uwp/api/windows.networking.connectivity.connectionprofile) objeto retornado por [GetInternetConnectionProfile](/uwp/api/windows.networking.connectivity.networkinformation).
  
 Para simular propriedades de rede:  
  
1. Na barra de ferramentas do simulador, escolha o **alterar propriedades da rede** botão.  
  
2. Sobre o **definir propriedades de rede** caixa de diálogo, selecione **uso simulado propriedades de rede**.  
  
    Desmarque a caixa de seleção para remover a simulação e retornar às propriedades de rede da interface atualmente conectada.  
  
3. Insira um **nome do perfil** para a rede simulada. É recomendável usar um nome exclusivo que você pode usar para identificar a simulação na [ProfileName](/uwp/api/windows.networking.connectivity.connectionprofile) propriedade da [ConnectionProfile](/uwp/api/windows.networking.connectivity.connectionprofile) objeto.  
  
4. Selecione o [NetworkCostType](/uwp/api/windows.networking.connectivity.networkcosttype) valor para o perfil da **tipo de custo de rede** lista.  
  
5. Dos **sinalizador de Status de limite de dados** lista, você pode definir o [ApproachingDataLimit](/uwp/api/windows.networking.connectivity.connectioncost) propriedade ou o [OverDataLimit](/uwp/api/windows.networking.connectivity.connectioncost) propriedade como true, ou você pode escolher  **Abaixo do limite de dados** para definir os dois valores como false.  
  
6. Dos **estado de Roaming** lista, defina as [Roaming](/uwp/api/windows.networking.connectivity.connectioncost) propriedade.  
  
7. Escolher **propriedades do conjunto** para simular as propriedades de rede Disparando um primeiro plano [NetworkStatusChanged](/uwp/api/windows.networking.connectivity.networkinformation) eventos e um plano de fundo [SystemTrigger](/uwp/api/windows.applicationmodel.background.systemtrigger) do tipo  **NetworkStateChange**.  
  
   **Para obter mais informações sobre como gerenciar conexões de rede**  
  
   [Guia de início rápido: Gerenciando monitorados restrições de custo de rede](https://msdn.microsoft.com/library/windows/apps/Hh750310.aspx)  
  
   [Exemplo de informações de rede](https://code.msdn.microsoft.com/windowsapps/Network-Information-Sample-63aaa201)  
  
   [Analisar o uso de energia](../profiling/analyze-energy-use-in-store-apps.md)  
  
   [Windows.Networking.Connectivity](/uwp/api/windows.networking.connectivity)  
  
   [Como responder a eventos do sistema com tarefas em segundo plano](/previous-versions/windows/apps/hh977058(v=win.10))  
  
   [Como disparar eventos para suspender, retomar e em segundo plano em aplicativos UWP](/visualstudio/debugger/how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio)  
  
##  <a name="BKMK_Navigate_the_simulator_with_the_keyboard"></a> Navegar no simulador com o teclado  
 Você pode navegar a barra de ferramentas do simulador pressionando **CTRL + ALT + seta para cima** para alternar o foco da janela do simulador na barra de ferramentas do simulador. Use o **seta para cima** e o **seta para baixo** para mover entre os botões da barra de ferramentas.  
  
 Você pode desligar o simulador pressionando **CTRL + ALT + F4**.  
  
## <a name="see-also"></a>Consulte também  
 [Executar aplicativos usando o Visual Studio](../debugger/run-store-apps-from-visual-studio.md)