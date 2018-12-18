---
title: Depurar aplicativos UWP em computadores remotos | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 0f6814d6-cd0d-49f3-b501-dea8c094b8ef
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: 0350358c2225851619a84216c929b8d7435dc4e3
ms.sourcegitcommit: 1df0ae74af03bcf0244129a29fd6bd605efc9f61
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/01/2018
ms.locfileid: "50750700"
---
# <a name="debug-uwp-apps-on-remote-machines-from-visual-studio"></a>Depurar aplicativos UWP em máquinas remotas do Visual Studio
  
Você pode usar o Visual Studio para executar, depurar, analisar e testar um aplicativo da plataforma Universal do Windows (UWP) em outro computador ou dispositivo. Executar o aplicativo UWP em um computador remoto é especialmente útil quando o computador do Visual Studio não dá suporte a funcionalidade específica de UWP, como toque, localização geográfica ou orientação física. 

##  <a name="BKMK_Prerequisites"></a> Pré-requisitos  

Para depurar um aplicativo UWP em um dispositivo remoto do Visual Studio:  
  
- O projeto do Visual Studio deve ser configurado para depuração remota.
- O computador remoto e o computador do Visual Studio devem ser conectados via rede ou conectados diretamente por meio de um cabo Ethernet ou USB. Não há suporte à depuração pela Internet.  
- Você deve [ativar o modo de desenvolvedor](/windows/uwp/get-started/enable-your-device-for-development) no computador do Visual Studio e o computador remoto. 
- Computadores remotos devem estar executando as ferramentas remotas para Visual Studio. 
  - Algumas versões do Windows 10 iniciarem e executar as ferramentas remotas automaticamente. Caso contrário, [instalar e executar as ferramentas remotas para Visual Studio](#BKMK_download).
  - Dispositivos Windows Mobile 10 não exigem ou dar suporte a ferramentas remotas. 

##  <a name="BKMK_ConnectVS"></a> Configurar um projeto do Visual Studio para depuração remota
<a name="BKMK_DirectConnect"></a> Usar o projeto **propriedades** para especificar o dispositivo remoto para se conectar ao. As configurações são diferentes dependendo da linguagem de programação. 

> [!CAUTION]
> Por padrão, a página de propriedade define **Universal (protocolo não criptografado)** como o **tipo de autenticação** para conexões remotas do Windows 10. Você talvez precise definir **sem autenticação** para se conectar ao depurador remoto. **Universal (protocolo não criptografado)** e **sem autenticação** protocolos não têm nenhuma segurança de rede, para que os dados passados entre o desenvolvimento e máquinas remotas estão vulneráveis. Escolha esses tipos de autenticação apenas para redes confiáveis que você está claro que não estão em risco de tráfego mal-intencionado ou hostil. 
>
>Se você escolher **autenticação do Windows** para o **tipo de autenticação**, você precisará entrar no computador remoto durante a depuração. O depurador remoto também deve ser executado sob **autenticação do Windows** modo, com a mesma conta de usuário como no computador do Visual Studio.

###  <a name="BKMK_Choosing_the_remote_device_for_C__and_Visual_Basic_projects"></a> Configurar um C# ou o projeto do Visual Basic para depuração remota  

1. Selecione o C# ou o projeto do Visual Basic no Visual Studio **Gerenciador de soluções** e selecione o **propriedades** ícone, pressione **Alt** +  **Insira**, ou clique com botão direito e escolha **propriedades**.
  
1.  Selecione a guia **Depurar**.  
  
1.  Sob **dispositivo de destino**, selecione **máquina remota** para um computador remoto, ou **dispositivo** para um dispositivo do Windows Mobile 10 diretamente conectados.  
  
1.  Para um computador remoto, insira o nome de rede ou o endereço IP na **computador remoto** campo, ou selecione **localizar** para pesquisar o dispositivo na [caixa de diálogo conexões remotas](#remote-connections). 
    
    ![Gerenciado propriedades do projeto para depuração remota](../debugger/media/vsrun_managed_projprop_remote.png "propriedades do projeto de depuração gerenciados")  
    
###  <a name="BKMK_Choosing_the_remote_device_for_JavaScript_and_C___projects"></a> Configurar um projeto de JavaScript ou C++ para depuração remota   
  
1.  Selecione o projeto C++ ou JavaScript no Visual Studio **Gerenciador de soluções** e selecione o **Properties** ícone, pressione **Alt**+**Enter** , ou clique com botão direito e escolha **propriedades**.
  
1.  Selecione o **depuração** guia.  
  
3.  Sob **depurador a iniciar**, selecione **máquina remota** para um computador remoto, ou **dispositivo** para um dispositivo do Windows Mobile 10 diretamente conectados. 
  
1.  Para uma máquina remota, insira ou selecione o nome de rede ou o endereço IP na **nome da máquina** campo ou soltar para baixo e selecione **localizar** para pesquisar o dispositivo na [caixa de diálogo conexões remotas ](#remote-connections). 

    ![Propriedades de projeto do C++ para depuração remota](../debugger/media/vsrun_cpp_projprop_remote.png "propriedades do projeto de depuração de C++")
    
### <a name="remote-connections"></a> Use a caixa de diálogo conexões remotas

No **conexões remotas** caixa de diálogo, você pode procurar por um nome de computador remoto específico ou endereço IP ou detectar automaticamente as conexões, selecionando o ícone de seta arredondado para atualização. A caixa de diálogo pesquisa somente os dispositivos na sub-rede local que esteja executando o depurador remoto. Nem todos os dispositivos podem ser detectados na **conexões remotas** caixa de diálogo. 

 ![Caixa de diálogo de Conexão remota](../debugger/media/vsrun_selectremotedebuggerdlg.png "caixa de diálogo conexões remotas")  

>[!TIP]
>Se você não pode se conectar a um dispositivo remoto por nome, tente usar seu endereço IP. Para determinar o endereço IP, no dispositivo remoto, digite **ipconfig** em uma janela de comando. O endereço IP é exibido como **endereço IPv4**.  
    
## <a name="BKMK_download"></a> Baixe e instale as ferramentas remotas para Visual Studio

Para o Visual Studio depurar aplicativos em um computador remoto, o computador remoto deve estar executando as ferramentas remotas para Visual Studio. 

- Dispositivos Windows Mobile 10 não exigem nem dão suporte as ferramentas remotas. 
- Computadores com Windows 10 em execução do criador atualizar (versão 1703) e posterior, dispositivos Windows 10 Xbox, HoloLens e IoT instalam as ferramentas remotas automaticamente quando você implanta o aplicativo. 
- Em computadores do Windows 10 do pré-Creators Update, você deve manualmente baixar, instalar e estar executando as ferramentas remotas no computador remoto antes de iniciar a depuração.

**Para baixar e instalar as ferramentas remotas:**

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]
  
### <a name="BKMK_setup"></a> Configurar as ferramentas remotas

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]  
  
##  <a name="BKMK_RunRemoteDebug"></a> Depurar aplicativos UWP remotamente 

Depuração remota funciona da mesma forma depuração local. 

1. Em versões de atualização do pre-criador do Windows 10, certifique-se o Monitor de depuração remota (*msvsmon.exe*) está em execução no dispositivo remoto.  
   
1. No computador do Visual Studio, certifique-se o destino de depuração correto (**computador remoto** ou **dispositivo**) é exibido ao lado da seta verde na barra de ferramentas. 
   
1. Iniciar a depuração, selecionando **Debug** > **iniciar depuração**, pressionando **F5**, ou selecionando a seta verde na barra de ferramentas. 
   
   O projeto recompilações, implanta e é iniciado no dispositivo remoto. O depurador suspende a execução nos pontos de interrupção, e você pode entrar, failover e fora do código. 
   
1. Se necessário, selecione **Debug** > **parar depuração** ou pressione **Shift**+**F5** para parar a depuração e Feche o aplicativo remoto.
  
## <a name="see-also"></a>Consulte também  
 [Opções de implantação remota avançadas](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)  
 [Testando aplicativos UWP com o Visual Studio](../test/testing-store-apps-with-visual-studio.md)   
 [Depurar aplicativos UWP no Visual Studio](debugging-windows-store-and-windows-universal-apps.md)
