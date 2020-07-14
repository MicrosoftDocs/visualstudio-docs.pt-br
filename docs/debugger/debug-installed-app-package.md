---
title: Depurar um pacote de aplicativo UWP instalado | Microsoft Docs
ms.custom: ''
ms.date: 11/07/2018
ms.topic: how-to
f1_keywords:
- vs.debug.installedapppackagelauncher
- vs.debug.remote.connection
dev_langs:
- C++
- FSharp
- CSharp
- JScript
- VB
helpviewer_keywords:
- app package, debug
ms.assetid: 5a94ad64-100d-43ca-9779-16cb5af86f97
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: eabc694665bede7d193a360a01c42366568e33c5
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350726"
---
# <a name="debug-an-installed-uwp-app-package-in-visual-studio"></a>Depurar um pacote de aplicativo UWP instalado no Visual Studio

O Visual Studio pode depurar pacotes de aplicativos UWP (Plataforma Universal do Windows instalados) em computadores com Windows 10 e dispositivos Xbox, HoloLens e IoT.

>[!NOTE]
>A depuração do Visual Studio para aplicativos UWP instalados não tem suporte em telefones.

Para obter mais informações sobre como depurar aplicativos UWP, consulte as postagens no blog sobre [depuração de pacotes de aplicativos instalados](https://devblogs.microsoft.com/devops/updates-for-debugging-installed-app-packages-in-visual-studio-2015-update-2/) e [criação de aplicativos universais do Windows (UWP)](https://devblogs.microsoft.com/visualstudio/universal-windows-apps-targeting-windows-10-anniversary-sdk/).

## <a name="debug-an-installed-uwp-app-on-a-local-machine"></a>Depurar um aplicativo UWP instalado em um computador local

1. No Visual Studio, selecione **depurar**  >  **outros destinos de depuração**  >  **depurar pacote do aplicativo instalado**.

1. Na caixa de diálogo **depurar pacote do aplicativo instalado** , em **tipo de conexão**, selecione **computador local**.

1. Em **pacotes de aplicativos instalados**, selecione o aplicativo que você deseja depurar ou digite seu nome na caixa de pesquisa. Os pacotes de aplicativos instalados sem execução aparecem em **não em execução**e os aplicativos em execução estão em **execução**.

   ![DebugInstalledAppPackage](../debugger/media/debug-installed-app-pkg.png "DebugInstalledAppPackage")

1. Se necessário, altere o tipo de código em **depurar este tipo de código**e selecione outras opções.
   - Selecione não **Iniciar, mas depurar meu código quando começar** a iniciar a depuração quando o aplicativo for iniciado. Iniciar a depuração quando o aplicativo é iniciado é uma maneira eficaz de depurar caminhos de controle de [diferentes métodos de inicialização](/windows/uwp/xbox-apps/automate-launching-uwp-apps), como a ativação de protocolo com parâmetros personalizados.

1. Selecione **Iniciar**ou, se o aplicativo estiver em execução, selecione **anexar**.

> [!NOTE]
> Você também pode se conectar a qualquer UWP em execução ou a outro processo de aplicativo selecionando a **depuração**  >  **anexar para processar** no Visual Studio. Você não precisa do projeto original do Visual Studio para anexar a um processo em execução, mas carregar os símbolos do aplicativo ajudará significativamente ao depurar um processo para o qual você não tenha o código original. Consulte [especificar o símbolo e os arquivos de origem no depurador](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

## <a name="debug-an-installed-uwp-app-on-a-remote-computer-or-device"></a><a name="remote"></a>Depurar um aplicativo UWP instalado em um computador ou dispositivo remoto

Na primeira vez que o Visual Studio decorre bugs em um aplicativo UWP instalado em um dispositivo Windows 10 ou em um computador com o Windows 10 do post-Creator remoto, ele instala as ferramentas de depuração remota no dispositivo de destino.

1. [Habilite o modo de desenvolvedor](/windows/uwp/get-started/enable-your-device-for-development) no computador do Visual Studio e no computador ou dispositivo remoto.

1. Se você estiver se conectando a um computador remoto executando o Windows 10 do pre-Creator, [Instale e inicie manualmente o depurador remoto](../debugger/remote-debugging.md) no computador remoto.

1. No computador do Visual Studio, selecione **depurar**  >  **outros destinos de depuração**  >  **depurar pacote do aplicativo instalado**.

1. Na caixa de diálogo **depurar pacote do aplicativo instalado** , em **tipo de conexão**, selecione **computador remoto** ou **dispositivo**.

   Se você selecionar **dispositivo**, seu computador deverá estar fisicamente conectado a um dispositivo Windows 10.

   Para um computador remoto, se o endereço do computador não aparecer ao lado de **endereço**, selecione **alterar**.

   1. Na caixa de diálogo **conexão remota** , ao lado de **endereço**, digite o nome ou o endereço IP do computador ao qual você deseja se conectar.

      ![ChooseRemoteComputer](../debugger/media/debug-remote-app-pkg.png "ChooseRemoteComputer")

      Se o depurador não puder se conectar a um computador remoto usando o nome do computador, use o endereço IP em vez disso. Use o endereço IP para dispositivos Xbox, HoloLens ou IoT.
   1. Selecione uma opção de autenticação ao lado do **modo de autenticação**.

      Para a maioria dos aplicativos, mantenha o valor padrão, **Universal (protocolo não criptografado)**.
   1. Selecione **Selecionar**.

1. Em **pacotes de aplicativos instalados**, selecione o aplicativo que você deseja depurar ou digite seu nome na caixa de pesquisa. Os pacotes de aplicativos instalados sem execução aparecem em **não em execução**e os aplicativos em execução estão em **execução**.

1. Se necessário, altere o tipo de código em **depurar este tipo de código**e selecione outras opções.
   - Selecione não **Iniciar, mas depurar meu código quando começar** a iniciar a depuração quando o aplicativo for iniciado. Iniciar a depuração quando o aplicativo é iniciado é uma maneira eficaz de depurar caminhos de controle de [diferentes métodos de inicialização](/windows/uwp/xbox-apps/automate-launching-uwp-apps), como a ativação de protocolo com parâmetros personalizados.

1. Selecione **Iniciar**ou, se o aplicativo estiver em execução, selecione **anexar**.

Quando você inicia a depuração de um pacote do aplicativo instalado em um dispositivo Xbox, HoloLens ou IoT conectado pela primeira vez, o Visual Studio instala a versão correta do depurador remoto para seu dispositivo de destino. A instalação do depurador remoto pode levar algum tempo e a mensagem **iniciando o depurador remoto** é exibida enquanto ele está acontecendo.

>[!NOTE]
>Atualmente, um dispositivo Xbox ou HoloLens reinicia o aplicativo com o depurador anexado se ele já estava em execução.

Para obter mais informações sobre a implantação remota de aplicativos UWP, consulte [implantar e depurar aplicativos UWP](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options) e [depurar aplicativos UWP em computadores remotos](run-windows-store-apps-on-a-remote-machine.md).

## <a name="see-also"></a>Veja também

- [Depurando no Visual Studio](../debugger/index.yml)
- [Introdução ao depurador](../debugger/debugger-feature-tour.md)
- [Depuração remota](../debugger/remote-debugging.md)
- [Configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md)
- [Atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md)
- [Erros de depuração remota e solução de problemas](../debugger/remote-debugging-errors-and-troubleshooting.md)