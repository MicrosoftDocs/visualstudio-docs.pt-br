---
title: Depurar aplicativos UWP em computadores remotos | Microsoft Docs
ms.date: 10/05/2018
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 0f6814d6-cd0d-49f3-b501-dea8c094b8ef
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- uwp
ms.openlocfilehash: 3d208c59f08ddeb5a322d174a2c6b56dd901c2c4
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348113"
---
# <a name="debug-uwp-apps-on-remote-machines-from-visual-studio"></a>Depurar aplicativos UWP em máquinas remotas a partir do Visual Studio

Você pode usar o Visual Studio para executar, depurar, criar um perfil e testar um aplicativo Plataforma Universal do Windows (UWP) em outro computador ou dispositivo. Executar o aplicativo UWP em um computador remoto é especialmente útil quando o computador do Visual Studio não oferece suporte a funcionalidades específicas de UWP, como toque, localização geográfica ou orientação física.

## <a name="prerequisites"></a><a name="BKMK_Prerequisites"></a> Pré-requisitos

Para depurar um aplicativo UWP em um dispositivo remoto do Visual Studio:

- O projeto do Visual Studio deve ser configurado para depuração remota.
- A máquina remota e o computador do Visual Studio devem estar conectados em uma rede ou conectados diretamente por meio de um cabo USB ou Ethernet. Não há suporte à depuração pela Internet.
- Você deve [ativar o modo de desenvolvedor](/windows/uwp/get-started/enable-your-device-for-development) tanto no computador do Visual Studio quanto na máquina remota.
- Os computadores remotos devem estar executando o Ferramentas Remotas para Visual Studio.
  - Algumas versões do Windows 10 iniciam e executam as ferramentas remotas automaticamente. Caso contrário, [Instale e execute o ferramentas remotas para Visual Studio](#BKMK_download).
  - Dispositivos Windows Mobile 10 não exigem ou dão suporte a ferramentas remotas.

## <a name="configure-a-visual-studio-project-for-remote-debugging"></a><a name="BKMK_ConnectVS"></a>Configurar um projeto do Visual Studio para depuração remota
<a name="BKMK_DirectConnect"></a>Você usa as **Propriedades** do projeto para especificar o dispositivo remoto ao qual se conectar. As configurações diferem dependendo da linguagem de programação.

> [!CAUTION]
> Por padrão, a página de propriedades define **Universal (protocolo não criptografado)** como o **tipo de autenticação** para conexões remotas do Windows 10. Talvez seja necessário não definir **nenhuma autenticação** para se conectar ao depurador remoto. **Universal (protocolo não criptografado)** e nenhum protocolo de **autenticação** não tem segurança de rede, portanto, os dados passados entre o desenvolvimento e as máquinas remotas são vulneráveis. Escolha esses tipos de autenticação somente para redes confiáveis que você tenha certeza de que não estão em risco de tráfego mal-intencionado ou hostil.
>
>Se você escolher **autenticação do Windows** para o **tipo de autenticação**, será necessário entrar no computador remoto durante a depuração. O depurador remoto também deve estar em execução no modo de **autenticação do Windows** , com a mesma conta de usuário do computador do Visual Studio.

### <a name="configure-a-c-or-visual-basic-project-for-remote-debugging"></a><a name="BKMK_Choosing_the_remote_device_for_C__and_Visual_Basic_projects"></a>Configurar um projeto em C# ou Visual Basic para depuração remota

1. Selecione o projeto C# ou Visual Basic no Visual Studio **Gerenciador de soluções** e selecione o ícone **Propriedades** , pressione **ALT** + **Enter**ou clique com o botão direito do mouse e escolha **Propriedades**.

1. Selecione a guia **Depurar**.

1. Em **dispositivo de destino**, selecione **computador remoto** para um computador remoto ou **dispositivo** para um dispositivo Windows Mobile 10 conectado diretamente.

1. Para um computador remoto, insira o nome da rede ou o endereço IP no campo **máquina remota** ou selecione **Localizar** para pesquisar o dispositivo na caixa de [diálogo conexões remotas](#remote-connections).

    ![Propriedades do projeto gerenciado para depuração remota](../debugger/media/vsrun_managed_projprop_remote.png "Propriedades do projeto de depuração gerenciado")

### <a name="configure-a-c-project-for-remote-debugging"></a><a name="BKMK_Choosing_the_remote_device_for_JavaScript_and_C___projects"></a>Configurar um projeto C++ para depuração remota

1. Selecione o projeto C++ no Visual Studio **Gerenciador de soluções** e selecione o ícone **Propriedades** , pressione **ALT** + **Enter**ou clique com o botão direito do mouse e escolha **Propriedades**.

1. Selecione a guia **depuração** .

3. Em **depurador para iniciar**, selecione **computador remoto** para um computador remoto ou **dispositivo** para um dispositivo Windows Mobile 10 conectado diretamente.

1. Para um computador remoto, insira ou selecione o nome da rede ou o endereço IP no campo **nome da máquina** ou lista suspensa e selecione **Localizar** para pesquisar o dispositivo na [caixa de diálogo conexões remotas](#remote-connections).

    ![Propriedades do projeto C++ para depuração remota](../debugger/media/vsrun_cpp_projprop_remote.png "Propriedades do projeto de depuração do C++")

### <a name="use-the-remote-connections-dialog-box"></a><a name="remote-connections"></a>Usar a caixa de diálogo conexões remotas

Na caixa de diálogo **conexões remotas** , você pode procurar um nome de computador remoto ou endereço IP específico ou detectar conexões automaticamente selecionando o ícone de atualização de seta arredondada. A caixa de diálogo pesquisa somente os dispositivos na sub-rede local que estão executando o depurador remoto no momento. Nem todos os dispositivos podem ser detectados na caixa de diálogo **conexões remotas** .

 ![Caixa de diálogo conexão remota](../debugger/media/vsrun_selectremotedebuggerdlg.png "Caixa de diálogo conexões remotas")

>[!TIP]
>Se você não puder se conectar a um dispositivo remoto por nome, tente usar seu endereço IP. Para determinar o endereço IP, no dispositivo remoto, insira **ipconfig** em uma janela de comando. O endereço IP aparece como **endereço IPv4**.

## <a name="download-and-install-the-remote-tools-for-visual-studio"></a><a name="BKMK_download"></a> Baixar e instalar as Ferramentas Remotas para Visual Studio

Para que o Visual Studio depure aplicativos em um computador remoto, o computador remoto deve estar executando o Ferramentas Remotas para Visual Studio.

- Dispositivos Windows Mobile 10 não exigem ou dão suporte a ferramentas remotas.
- Os computadores com Windows 10 executando a atualização do criador (versão 1703) e posteriores, dispositivos Windows 10 Xbox, IoT e HoloLens instalam as ferramentas remotas automaticamente quando você implanta o aplicativo.
- Na atualização dos PCs com Windows 10 do pre-Creator, você deve baixar, instalar e executar manualmente as ferramentas remotas no computador remoto antes de iniciar a depuração.

**Para baixar e instalar as ferramentas remotas:**

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

### <a name="configure-the-remote-tools"></a><a name="BKMK_setup"></a>Configurar as ferramentas remotas

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

## <a name="debug-uwp-apps-remotely"></a><a name="BKMK_RunRemoteDebug"></a>Depurar aplicativos UWP remotamente

A depuração remota funciona da mesma forma que a depuração local.

1. Nas versões de atualização do Windows 10 do pre-Creator, verifique se o Monitor de Depuração Remota (*msvsmon.exe*) está em execução no dispositivo remoto.

1. No computador do Visual Studio, verifique se o destino de depuração correto (computador ou **dispositivo****remoto** ) aparece ao lado da seta verde na barra de ferramentas.

1. Inicie a depuração selecionando **depurar**  >  **Iniciar Depuração**, pressionando **F5**ou selecionando a seta verde na barra de ferramentas.

   O projeto é recompilado e, em seguida, é implantado e iniciado no dispositivo remoto. O depurador suspende a execução em pontos de interrupção, e você pode percorrer, acima e fora de código.

1. Se necessário, selecione **depurar**  >  **parar depuração** ou pressione **Shift** + **F5** para parar a depuração e fechar o aplicativo remoto.

## <a name="see-also"></a>Veja também
- [Opções avançadas de implantação remota](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)
- [Testando aplicativos UWP com o Visual Studio](/visualstudio/test/create-and-run-unit-tests-for-a-store-app-in-visual-studio/)
- [Depurar aplicativos UWP no Visual Studio](debugging-windows-store-and-windows-universal-apps.md)
