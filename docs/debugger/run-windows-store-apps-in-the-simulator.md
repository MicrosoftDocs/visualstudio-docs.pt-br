---
title: Executar aplicativos UWP no simulador | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 81b69bf8-ec87-4bb6-9ad4-1fa7b7802d16
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 1c208e435e63891c71fe47ebd64c5fe1307e0c82
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348135"
---
# <a name="run-uwp-apps-in-the-simulator"></a>Executar aplicativos UWP no simulador

O simulador do Visual Studio para aplicativos UWP é um aplicativo de área de trabalho que simula um aplicativo UWP. Normalmente, você desejará depurar no computador local, em um dispositivo conectado ou em um computador remoto. No entanto, em alguns cenários, talvez você queira usar o simulador do Visual Studio para emular um tamanho de tela física e uma resolução diferentes. Você também pode simular eventos comuns de toque e rotação e simular Propriedades de conexão de rede.

O simulador fornece um ambiente no qual você pode criar, desenvolver, depurar e testar aplicativos UWP. No entanto, antes de publicar seu aplicativo no Microsoft Store, você deve testar seu aplicativo em um dispositivo real.

O simulador do Visual Studio para aplicativos UWP não é executado em um ambiente isolado em seu computador local. Portanto, os erros que ocorrem no simulador, como um erro não recuperável geral do sistema, também podem afetar o computador inteiro.

> [!IMPORTANT]
> O simulador do Visual Studio 2015 não inclui o botão de localização geográfica. Isso ocorre porque o simulador do Windows 10 não inclui a simulação de geolocalização.

## <a name="set-the-simulator-as-the-target"></a><a name="BKMK_Set_the_simulator_as_the_target"></a> Definir o simulador como o destino

Para executar seu aplicativo UWP no simulador, selecione **simulador** na lista suspensa ao lado do botão **Iniciar Depuração** na barra de ferramentas **padrão** do depurador. Essa opção estará disponível apenas se a **Versão Mínima da Plataforma de Destino** de seu aplicativo for menor ou igual ao sistema operacional no computador de desenvolvimento.

![Executando no simulador](../debugger/media/vsrun_f5_simulator.png "VSRUN_F5_Simulator")

## <a name="choose-an-interaction-mode"></a><a name="BKMK_Choose_an_interaction_mode"></a> Escolher um modo de interação

Você pode escolher os seguintes modos de interação:

- ![Botão de modo do mouse](../debugger/media/simulator_mousemodebtn.png "SIMULATOR_MouseModeBtn") Modo de mouse: define o modo de interação com gestos do mouse. Esses gestos incluem cliques, cliques duplos e arrastos.

- ![Botão iniciar emulação de toque](../debugger/media/simulator_starttouchemulationbtn.png "SIMULATOR_StartTouchEmulationBtn") Iniciar emulação de toque: define o modo de interação para gestos de toque de um único dedo. Os eventos desse tipo incluem tocar, arrastar e passar o dedo.

   ![Destino de um dedo de simulador](../debugger/media/simulator_onefinger.png "SIMULATOR_OneFinger")
   
   O ícone de alvo único indica o local dos eventos no simulador. Use o mouse para posicionar o ponteiro.

   ![Destino de toque de um dedo](../debugger/media/simulator_onefingerengaged.png "SIMULATOR_OneFingerEngaged")
   
   Pressione o botão esquerdo do mouse para ativar o modo de toque. Por exemplo, clique no botão para simular um gesto de tocar, ou pressione e segure o botão enquanto você arrasta ou passa o dedo.

## <a name="pinch-and-zoom"></a>Aperto e zoom

Defina o modo de interação como sendo gestos de aperto e zoom com dois dedos.

![Destino de dois dedos de simulador](../debugger/media/simulator_twofinger.png)

O ícone de alvo duplo indica o local de dois dedos na tela do dispositivo.

- Mova o mouse para posicionar os ícones sobre o objeto na tela do dispositivo.

- Gire a roda do mouse para trás ou para a frente a fim de alterar a distância simulada dos dois dedos antes de apertar ou aplicar zoom.

![Pinçar, aplicar zoom e girar destinos](../debugger/media/simulator_twofingerengaged.png)

- Pressione o botão esquerdo e gire a roda para trás (na sua direção) a fim de ampliar a exibição (aperto).

- Pressione o botão esquerdo e gire a roda do mouse para a frente (afastada de você) a fim de reduzir a exibição (zoom).

## <a name="object-rotation"></a>Rotação de objeto

O botão **girar emulação de toque** define o modo de interação com gestos de rotação usando dois dedos.

- Mova o mouse para posicionar os ícones sobre o objeto na tela do dispositivo. Gire a roda do mouse para trás ou para frente para alterar a orientação simulada dos dois dedos antes de girar o objeto.

- Pressione o botão esquerdo e gire a roda para trás (na sua direção) a fim de girar o objeto no sentido anti-horário. Conforme você gira a roda do mouse, um dos dois ícones de alvo gira em torno do outro para indicar o tamanho relativo da rotação.

- Pressione o botão esquerdo e gire a roda do mouse para a frente (afastada de você) a fim de girar o objeto no sentido horário.

## <a name="enable-or-disable-always-on-top-mode"></a><a name="BKMK_Enable_or_disable_Always_on_top_mode"></a> Habilitar ou desabilitar o modo Sempre visível
 Você pode configurar a janela do simulador para ficar sempre por cima das outras janelas. O botão **alternar janela superior** habilita ou desabilita o modo **superior do Always on** na janela do simulador.

## <a name="change-the-device-orientation"></a><a name="BKMK_Change_the_device_orientation"></a> Alterar a orientação do dispositivo
 Você pode alternar a orientação do dispositivo entre retrato e paisagem girando o simulador 90 graus em qualquer direção.

> [!NOTE]
> O simulador não respeita a propriedade [DisplayProperties.AutoRotationPreferences](/uwp/api/windows.graphics.display.displayproperties.autorotationpreferences) de um projeto. Por exemplo, se o projeto define a orientação como `Landscape` e você gira o simulador até a orientação retrato, a imagem de exibição do simulador também é girada e redimensionada. Teste essas configurações em um dispositivo real.

> [!NOTE]
> Se você gira o simulador de modo que uma borda dele fica maior do que a tela em que ele é exibido, o simulador é automaticamente redimensionado para caber na tela. O simulador não é redimensionado para o tamanho original se você o gira novamente.

## <a name="change-the-simulated-screen-size-and-resolution"></a><a name="BKMK_Change_the_simulated_screen_size_and_resolution"></a> Alterar o tamanho e a resolução de tela simulados
 Para alterar o tamanho e a resolução de tela simulados, escolha o botão **Alterar Resolução** na paleta e escolha um novo tamanho e uma nova resolução na lista.

 O tamanho e a resolução da tela são listados como *Largura da tela em polegadas, largura em pixel X altura em pixel*. Observe que tanto o tamanho como a resolução da tela são simulados. As coestações de local no simulador são convertidas para o tamanho e a resolução do dispositivo selecionado.

> [!NOTE]
> Você pode salvar versões dimensionadas de imagens de bitmap em seu aplicativo, e o Windows carregará a imagem correta para a escala atual. Para obter mais informações, consulte [introdução à interface do usuário e design](/windows/uwp/layout/design-and-ui-intro). No entanto, se você alterar a resolução do simulador de modo que o Windows selecione uma imagem diferente para ajustar à resolução, será preciso parar e reiniciar a sessão de depuração para exibir a nova imagem.

## <a name="capture-a-screenshot-of-your-app-for-submission-to-microsoft-store"></a><a name="BKMK_Capture_a_screenshot_of_your_app_for_submission_to_the_Microsoft_Store"></a>Capture uma captura de tela de seu aplicativo para envio para Microsoft Store
 Ao enviar um aplicativo para Microsoft Store, você deve incluir capturas de tela do aplicativo.

> [!NOTE]
> A captura de tela é salva na resolução atual do simulador. Para alterar a resolução, escolha o botão **Alterar Resolução**.

- Para criar capturas de tela do aplicativo por meio do simulador, escolha o botão **Capturar tela na área de transferência**.

- Para definir o local em que as capturas de tela estão localizadas, escolha o botão **configurações de captura de tela** e escolha o local no menu de atalho.

   ![Menu de contexto de configurações de captura de tela](../debugger/media/simulator_screenshotsettingscntxmnu.png)

## <a name="simulate-network-connection-properties"></a><a name="BKMK_Simulate_network_connection_properties"></a> Simular propriedades de conexão de rede

Você pode ajudar os usuários de seu aplicativo a gerenciar os custos de conexões de rede limitadas mantendo a percepção desses custos da conexão de rede ou das alterações de status do plano de dados e habilitando o seu aplicativo para usar essas informações a fim de evitar a cobrança de custos adicionais por roaming ou exceder um limite especificado de transferência de dados. As APIs [Windows. Networking. Connectivity](/uwp/api/windows.networking.connectivity) permitem responder a eventos [NetworkStatusChanged](/uwp/api/windows.networking.connectivity.networkinformation) e [TriggerType](/uwp/api/windows.applicationmodel.background.systemtrigger) que assinam. Consulte [início rápido: Gerenciando restrições de custo de rede limitada](https://msdn.microsoft.com/library/windows/apps/Hh750310.aspx).

Para depurar ou testar seu código de reconhecimento de custos de rede, o simulador pode imitar as propriedades de uma rede que são expostas por meio do objeto [ConnectionProfile](/uwp/api/windows.networking.connectivity.connectionprofile) retornado por [GetInternetConnectionProfile](/uwp/api/windows.networking.connectivity.networkinformation).

Para simular propriedades de rede:

1. Na barra de ferramentas do simulador, escolha o botão **alterar propriedades da rede** .

2. Na caixa de diálogo **Definir Propriedades de Rede**, selecione **Usar propriedades de rede simulada**.

    Desmarque a caixa de seleção para remover a simulação e retornar às propriedades de rede da interface atualmente conectada.

3. Digite um **Nome de Perfil** para a rede simulada. É recomendável usar um nome exclusivo que você pode usar para identificar a simulação na propriedade [ProfileName](/uwp/api/windows.networking.connectivity.connectionprofile) do objeto [ConnectionProfile](/uwp/api/windows.networking.connectivity.connectionprofile) .

4. Selecione o valor [NetworkCostType](/uwp/api/windows.networking.connectivity.networkcosttype) para o perfil na lista **tipo de custo de rede** .

5. Na lista **sinalizador de status do limite de dados** , você pode definir a propriedade [ApproachingDataLimit](/uwp/api/windows.networking.connectivity.connectioncost) ou a propriedade [OverDataLimit](/uwp/api/windows.networking.connectivity.connectioncost) como true ou pode escolher **em limite de dados** para definir os dois valores como false.

6. Na lista **estado de roaming** , defina a propriedade [roaming](/uwp/api/windows.networking.connectivity.connectioncost) .

7. Escolha **definir propriedades** para simular as propriedades de rede disparando um evento [NetworkStatusChanged](/uwp/api/windows.networking.connectivity.networkinformation) em primeiro plano e um [SystemTrigger](/uwp/api/windows.applicationmodel.background.systemtrigger) em segundo plano do tipo **NetworkStateChange**.

Para obter mais informações sobre como gerenciar conexões de rede, consulte:

[Início rápido: Gerenciando restrições de custo de rede limitada](https://msdn.microsoft.com/library/windows/apps/Hh750310.aspx)

[Exemplo de informações de rede](https://code.msdn.microsoft.com/windowsapps/Network-Information-Sample-63aaa201)

::: moniker range="vs-2017"
[Analisar o uso de energia](../profiling/analyze-energy-use-in-store-apps.md)
::: moniker-end

[Windows.Networking.Connectivity](/uwp/api/windows.networking.connectivity)

[Como responder a eventos do sistema com tarefas em segundo plano](/previous-versions/windows/apps/hh977058(v=win.10))

[Como disparar eventos para suspender, retomar e em segundo plano em aplicativos UWP](how-to-trigger-suspend-resume-and-background-events-for-windows-store-apps-in-visual-studio.md)

## <a name="navigate-the-simulator-with-the-keyboard"></a><a name="BKMK_Navigate_the_simulator_with_the_keyboard"></a> Navegar no simulador com o teclado

Você pode navegar na barra de ferramentas do simulador pressionando **Ctrl + Alt + seta para cima** para alternar o foco da janela simular para a barra de ferramentas do simulador. Use a **seta para cima** e a **seta para baixo** para navegar entre os botões da barra de ferramentas.

Você pode desligar o simulador pressionando **Ctrl + Alt + F4**.

## <a name="see-also"></a>Veja também

- [Executar aplicativos do Visual Studio](debugging-windows-store-and-windows-universal-apps.md)
