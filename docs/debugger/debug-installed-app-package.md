---
title: Depurar um pacote de aplicativo UWP instalado | Microsoft Docs
ms.custom: H1Hack27Feb2017
ms.date: 11/07/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
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
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 331fd642001f1e6217736185d4b3bbbd7f56923e
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51784410"
---
# <a name="debug-an-installed-uwp-app-package-in-visual-studio"></a>Depurar um pacote de aplicativo UWP instalado no Visual Studio

O Visual Studio pode depurar pacotes de aplicativo de plataforma Universal do Windows (UWP) instalados em computadores com Windows 10 e dispositivos Xbox, HoloLens e IoT. 

>[!NOTE]
>Não há suporte para a depuração para aplicativos instalados da UWP do Visual Studio em telefones.
   
Para obter mais informações sobre como depurar aplicativos UWP, consulte as postagens de blog sobre [depuração instalado pacotes de aplicativos](https://blogs.msdn.microsoft.com/devops/2016/03/30/updates-for-debugging-installed-app-packages-in-visual-studio-2015-update-2/) e [criação de aplicativos Universal do Windows (UWP)](https://blogs.msdn.microsoft.com/visualstudio/2016/08/02/universal-windows-apps-targeting-windows-10-anniversary-sdk/).

## <a name="debug-an-installed-uwp-app-on-a-local-machine"></a>Depurar um aplicativo UWP instalado em um computador local

1. No Visual Studio, selecione **Debug** > **outros destinos de depuração** > **depurar pacote do aplicativo instalado**.
   
1. No **depurar pacote do aplicativo instalado** caixa de diálogo, em **tipo de Conexão**, selecione **Máquina Local**.
   
1. Sob **pacotes de aplicativos instalado**, selecione o aplicativo que você deseja depurar, ou digite seu nome na caixa de pesquisa. Pacotes de aplicativos instalados de execução não aparecem sob **não está em execução**, e a execução de aplicativos está sob **executando**. 
   
   ![DebugInstalledAppPackage](../debugger/media/debug-installed-app-pkg.png "DebugInstalledAppPackage")
   
1. Se necessário, altere o tipo de código sob **depurar esse tipo de código**e selecione outras opções. 
   - Selecione **não iniciar, mas depurar meu código quando iniciar** para iniciar a depuração quando o aplicativo é iniciado. Iniciar a depuração quando o aplicativo for iniciado é uma maneira eficiente para depurar os caminhos de controle de [métodos de inicialização diferente de](/windows/uwp/xbox-apps/automate-launching-uwp-apps), como a ativação de protocolo com parâmetros personalizados.
   
1. Selecione **inicie**, ou se o aplicativo estiver em execução, selecione **Attach**.

> [!NOTE]
> Você também pode anexar a qualquer UWP em execução ou outro processo do aplicativo, selecionando **Debug** > **anexar ao processo** no Visual Studio. Não é necessário o projeto original do Visual Studio para anexar a um processo em execução, mas o carregamento de símbolos do aplicativo ajudará significativamente durante a depuração de um processo que você não tiver o código original para. Ver [especificar arquivos de símbolo e de origem no depurador](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).
  
## <a name="remote"></a> Depurar um aplicativo UWP instalado em um dispositivo ou computador remoto

Na primeira vez em que o Visual Studio depura um aplicativo UWP instalado em um dispositivo Windows 10 ou computador de atualização Windows 10 de um remoto post-do criador, ele instala as ferramentas de depuração remotas no dispositivo de destino. 

1. [Habilitar o modo de desenvolvedor](/windows/uwp/get-started/enable-your-device-for-development) no computador do Visual Studio e o dispositivo ou computador remoto.
   
1. Se você estiver se conectando a um computador remoto executando o Windows 10 do pré-Creators Update, [instalar e iniciar o depurador remoto manualmente](../debugger/remote-debugging.md) no computador remoto.
   
1. No computador do Visual Studio, selecione **Debug** > **outros destinos de depuração** > **depurar pacote do aplicativo instalado**.
   
1. No **depurar pacote do aplicativo instalado** caixa de diálogo, em **tipo de Conexão**, selecione **máquina remota** ou **dispositivo**.
   
   Se você selecionar **dispositivo**, seu computador deve estar fisicamente conectado a um dispositivo Windows 10.
   
   Para um computador remoto, se o endereço do computador não for exibido ao lado **endereço**, selecione **alteração**. 
      
   1. No **Conexão remota** caixa de diálogo, em seguida **endereço**, digite o nome ou endereço IP do computador que você deseja se conectar.
      
      ![ChooseRemoteComputer](../debugger/media/debug-remote-app-pkg.png "ChooseRemoteComputer")
      
      Se o depurador não pode se conectar a um computador remoto usando o nome do computador, use o endereço IP. Use o endereço IP para os dispositivos de IoT, HoloLens ou Xbox.
   1. Selecione uma opção de autenticação lado **modo de autenticação**.
      
      Para a maioria dos aplicativos, mantenha o valor padrão, **Universal (protocolo não criptografado)**.
   1. Selecione **selecionar**. 

1. Sob **pacotes de aplicativos instalado**, selecione o aplicativo que você deseja depurar, ou digite seu nome na caixa de pesquisa. Pacotes de aplicativos instalados de execução não aparecem sob **não está em execução**, e a execução de aplicativos está sob **executando**. 
   
1. Se necessário, altere o tipo de código sob **depurar esse tipo de código**e selecione outras opções. 
   - Selecione **não iniciar, mas depurar meu código quando iniciar** para iniciar a depuração quando o aplicativo é iniciado. Iniciar a depuração quando o aplicativo for iniciado é uma maneira eficiente para depurar os caminhos de controle de [métodos de inicialização diferente de](/windows/uwp/xbox-apps/automate-launching-uwp-apps), como a ativação de protocolo com parâmetros personalizados.
   
1. Selecione **inicie**, ou se o aplicativo estiver em execução, selecione **Attach**.

Quando você inicia a depuração de um pacote de aplicativos instalados em um dispositivo do Xbox, HoloLens ou IoT conectado pela primeira vez, o Visual Studio instala a versão correta do depurador remoto para seu dispositivo de destino. Instalando o depurador remoto pode levar algum tempo e a mensagem **iniciando o depurador remoto** exibe enquanto ele está acontecendo.

>[!NOTE]
>Atualmente, um dispositivo Xbox ou HoloLens reinicia o aplicativo com o depurador anexado se ele já estava em execução.

Para obter mais informações sobre a implantação remota de aplicativos UWP, consulte [implantar e depurar aplicativos da UWP](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options) e [UWP depurar aplicativos em máquinas remotas](run-windows-store-apps-on-a-remote-machine.md). 
  
## <a name="see-also"></a>Consulte também  
 [Depurando no Visual Studio](../debugger/index.md)  
 [Tour dos recursos do depurador](../debugger/debugger-feature-tour.md)  
 [Depuração remota](../debugger/remote-debugging.md)  
 [Configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md)  
 [Atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md)  
 [Erros e solução de problemas de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)