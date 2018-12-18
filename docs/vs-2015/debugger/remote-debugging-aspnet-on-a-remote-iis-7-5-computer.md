---
title: Depuração remota de ASP.NET em um remoto IIS 7.5 computador | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 573a3fc5-6901-41f1-bc87-557aa45d8858
caps.latest.revision: 13
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 71d249571830ac608bef12c4a47d0243de1859a5
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51764063"
---
# <a name="remote-debugging-aspnet-on-a-remote-iis-computer"></a>Depuração remota de ASP.NET em um computador remoto IIS
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode implantar um aplicativo Web ASP.NET em um computador Windows Server com o IIS e configurá-lo para depuração remota. Este guia explica como configurar e configurar um aplicativo do Visual Studio 2015 MVC 4.5.2, implantá-lo no IIS e anexar o depurador remoto do Visual Studio.

Esses procedimentos foram testados nessas configurações de servidor:
* Windows Server 2012 R2 e IIS 10
* Windows Server 2008 R2 e IIS 7.5

A maioria das informações neste artigo também se aplica à depuração remota um aplicativo ASP.NET Core, exceto que a implantação de aplicativos ASP.NET core é diferente e requer etapas adicionais. Para implantar um aplicativo ASP.NET Core no IIS, você precisará concluir todas as seções do [deste artigo](https://docs.asp.net/en/latest/publishing/iis.html).

## <a name="prerequisites-install-the-remote-debugger-on-the-windows-server-computer"></a>Pré-requisitos: instalar o depurador remoto no computador do Windows Server

Para obter instruções sobre como baixar o depurador remoto no computador do Windows Server, consulte [depuração remota](../debugger/remote-debugging.md).

Para fazer a depuração remota de aplicativos ASP.NET, você pode executar o aplicativo depurador remoto como um administrador ou iniciar o depurador remoto como um serviço. Obter detalhes sobre como executar o depurador remoto como um serviço pode ser encontrado na [depuração remota](../debugger/remote-debugging.md).

Depois de instalado, verifique se que o depurador remoto está em execução no computador de destino. (Se não for, pesquise **depurador remoto** na **iniciar** menu. ) A janela do depurador remoto se parece com isso. (4020 é o número da porta padrão)

![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")
  
## <a name="create-the-application-on-the-visual-studio-computer"></a>Criar o aplicativo no computador do Visual Studio  
  
1. Crie um novo aplicativo ASP.NET MVC. (**Arquivo / novo / projeto**, em seguida, selecione **Visual c# / Web / aplicativo Web ASP.NET** . No **ASP.NET 4.5.2** seção de modelos, selecione **MVC**. Certifique-se de que **Host na nuvem** não estiver selecionada na seção do Azure. Nomeie o projeto **MyMVC**.)
1. Abra o arquivo HomeController.cs e defina um ponto de interrupção `About()` método.
1. No **Gerenciador de soluções**, clique com botão direito no nó do projeto e selecione **publicar**.
1. Para **selecione um destino de publicação**, selecione **personalizado** e nomeie o perfil **MyMVC**. Clique em **Avançar**.
1. No **Conexão** guia, defina o **método de publicação** campo **sistema de arquivos** e o **local de destino** campo para um diretório local. Clique em **Avançar**.

    ![RemoteDBG_Publish_Local](../debugger/media/remotedbg-publish-local.png "RemoteDBG_Publish_Local")
1. Definir a configuração para **depurar**. Clique em **Publicar**.

    ![RemoteDBG_Publish_Debug_Config](../debugger/media/remotedbg-publish-debug-config.png "RemoteDBG_Publish_Debug_Config")
    
    O aplicativo deve ser publicado para o diretório local.

## <a name="BKMK_deploy_asp_net"></a> Implantar o aplicativo ASP.NET no computador remoto do Windows Server

 Esta seção pressupõe que o computador com Windows Server já tem habilitados para IIS. No Windows Server 2012 R2, consulte [configuração do IIS](https://docs.asp.net/en/latest/publishing/iis.html#iis-configuration) para habilitar o IIS. (Você pode ignorar outras seções deste artigo, a menos que você está tentando implantar um aplicativo ASP.NET Core. Para o ASP.NET Core, siga as etapas no artigo para implantar o aplicativo em vez das etapas descritas aqui.)
1. Instalar o ASP.NET usam os componentes de plataforma da Web para instalar o ASP.NET 4.5 (no nó do servidor no Windows Server 2012 R2, escolha **obter novos componentes do Web Platform** e, em seguida, pesquise por ASP.NET)

    ![RemoteDBG_IIS_AspNet_45](../debugger/media/remotedbg-iis-aspnet-45.png "RemoteDBG_IIS_AspNet_45")

    No Windows Server 2008 R2, instale o ASP.NET 4, em vez de usar esse comando: **\v4.0.30319\aspnet_regiis.exe - ir C:\Windows\Microsoft.NET\Framework (64)**
1. Copiar o diretório de projeto do ASP.NET do computador do Visual Studio para um diretório local (que chamaremos **C:\Publish**) no computador do Windows Server. Você pode copiar o projeto manualmente, use Xcopy, implantação da Web, Robocopy, Powershell ou outras opções.

    > [!CAUTION]
    >  Se você precisar fazer alterações no código ou recompilação, você deve republicar e repita esta etapa. O executável que você copiou para o computador remoto deve corresponder exatamente, seu local de origem e símbolos.
1. Certifique-se de que o arquivo Web. config lista a versão correta do .NET Framework.  Por exemplo, a versão do .NET Framework instalada por padrão no Windows Server 2008 R2 é 4.0.30319, mas criamos um ASP.NET 4.5.2 versão. Se um aplicativo ASP.NET 4.0 está em execução no computador do Windows Server, você precisa alterar a versão:
  
    ```xml
    <system.web>
        <authentication mode="None" />  
        <compilation debug="true" targetFramework="4.0.30319" />
        <httpRuntime targetFramework="4.0.30319" />
      </system.web>
  
    ```
1. Abra o **Gerenciador de serviços de informações da Internet (IIS)** e vá para **Sites**.
1. Clique com botão direito do **Site padrão** nó e selecione **Adicionar aplicativo**.
1. Defina as **Alias** campo **MyMVC** e o campo de pool de aplicativos para **ASP.NET v4.0** (ASP.NET 4.5 não é uma opção para o pool de aplicativos). Defina as **caminho físico** ao **C:\Publish** (onde você copiou o diretório de projeto do ASP.NET).

    >[!NOTE] 
    > Para aplicativos ASP.NET Core, defina o campo de pool de aplicativo como **sem código gerenciado**.
1. Testar a implantação clicando **Site padrão** e selecione **procurar**.
    Se você implantou com êxito o aplicativo, você verá a página da web.

## <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a>Anexar ao aplicativo ASP.NET de computador do Visual Studio

1. No computador do Visual Studio, abra o **MyMVC** solução.
1. No Visual Studio, clique em **depurar / anexar ao processo** (**Ctrl + Alt + P**).
1. Definir o qualificador de campo para  **\<nome do computador remoto >: 4020**.
1. Clique em **Refresh**.
    Você deve ver alguns processos que aparecem na **processos disponíveis** janela.

    Se você não vir todos os processos, tente usar o endereço IP em vez do nome do computador remoto (a porta é necessária). Use `ipconfig` em uma linha de comando para obter o endereço IPv4.
1. Verifique **Mostrar processos de todos os usuários**.
1. Procure **w3wp.exe** e clique em **Attach**.

     Para localizar rapidamente o nome do processo, digite a primeira letra do processo.
     
    >[!NOTE]
    > Para um aplicativo ASP.NET Core, escolha o processo de dnx.exe em vez de w3wp.exe. (Esse nome de processo pode mudar em uma versão futura).

    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess.png "RemoteDBG_AttachToProcess")

1. Abra o site do computador remoto. Em um navegador, vá para **http://\<nome do computador remoto >**.
    
    Você deve ver a página da web ASP.NET.
1. Na página da web ASP.NET, clique no link para o **sobre** página.

    O ponto de interrupção deve ser atingido no Visual Studio.



