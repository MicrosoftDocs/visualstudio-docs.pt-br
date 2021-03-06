---
title: Depuração remota do ASP.NET em um computador com IIS
description: Saiba como configurar e configurar um aplicativo do Visual Studio ASP.NET MVC 4.5.2, implantá-lo no IIS e anexar o depurador remoto do Visual Studio.
ms.custom:
- remotedebugging
- seodec18
ms.date: 05/06/2020
ms.topic: conceptual
ms.assetid: 9cb339b5-3caf-4755-aad1-4a5da54b2a23
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- aspnet
ms.openlocfilehash: 104927d42f7ec68e43686278042c0712bb3c875e
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250083"
---
# <a name="remote-debug-aspnet-on-a-remote-iis-computer"></a>Depuração remota do ASP.NET em um computador remoto IIS

Para depurar um aplicativo ASP.NET que foi implantado no IIS, instale e execute as ferramentas remotas no computador em que você implantou seu aplicativo e, em seguida, anexe ao seu aplicativo em execução no Visual Studio.

![Componentes do depurador remoto](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

Este guia explica como configurar e configurar um aplicativo do Visual Studio ASP.NET MVC 4.5.2, implantá-lo no IIS e anexar o depurador remoto do Visual Studio.

> [!NOTE]
> Para a depuração remota ASP.NET Core em vez disso, consulte [ASP.NET Core de depuração remota em um computador IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md). Para Azure App serviço, você pode facilmente implantar e depurar em uma instância pré-configurada do IIS usando o [depurador de instantâneos](../debugger/debug-live-azure-applications.md) (.NET 4.6.1 necessário) ou [anexando o depurador de Gerenciador de servidores](../debugger/remote-debugging-azure.md).

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=vs-2019"
O Visual Studio 2019 é necessário para seguir as etapas mostradas neste artigo.
::: moniker-end
::: moniker range="vs-2017"
O Visual Studio 2017 é necessário para seguir as etapas mostradas neste artigo.
::: moniker-end

Esses procedimentos foram testados nessas configurações de servidor:

* Windows Server 2012 R2 e IIS 8 (para Windows Server 2008 R2, as etapas do servidor são diferentes)

## <a name="network-requirements"></a>Requisitos de rede

O depurador remoto tem suporte no Windows Server a partir do Windows Server 2008 Service Pack 2. Para obter uma lista completa dos requisitos, consulte [requisitos](../debugger/remote-debugging.md#requirements_msvsmon).

> [!NOTE]
> Não há suporte para a depuração entre dois computadores conectados por meio de um proxy. A depuração em uma conexão de alta latência ou de baixa largura de banda, como a Internet dial-up ou pela Internet entre países, não é recomendada e pode falhar ou ser lenta de forma inaceitável.

## <a name="app-already-running-in-iis"></a>O aplicativo já está em execução no IIS?

Este artigo inclui etapas sobre como configurar uma configuração básica do IIS no Windows Server e implantar o aplicativo do Visual Studio. Essas etapas estão incluídas para verificar se o servidor tem os componentes necessários instalados, se o aplicativo pode ser executado corretamente e se você está pronto para depuração remota.

* Se seu aplicativo estiver em execução no IIS e você quiser apenas baixar o depurador remoto e iniciar a depuração, acesse [baixar e instalar as ferramentas remotas no Windows Server](#BKMK_msvsmon).

* Se você quiser obter ajuda para certificar-se de que seu aplicativo está configurado, implantado e em execução corretamente no IIS para que você possa depurar, siga todas as etapas neste tópico.

## <a name="create-the-aspnet-452-application-on-the-visual-studio-computer"></a>Criar o aplicativo ASP.NET 4.5.2 no computador do Visual Studio

1. Crie um novo aplicativo MVC ASP.NET.

    ::: moniker range=">=vs-2019"
    No Visual Studio 2019, digite **Ctrl + Q** para abrir a caixa de pesquisa, digite **ASP.net**, escolha **modelos** e, em seguida, escolha **criar novo aplicativo Web ASP.net (.NET Framework)**. Na caixa de diálogo que aparece, nomeie o projeto **MyASPApp** e, em seguida, escolha **criar**. Selecione **MVC** e escolha **criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    Para fazer isso no Visual Studio 2017, escolha **arquivo > novo > projeto** e, em seguida, selecione **Visual C# > Web > ASP.NET aplicativo Web**. Na seção modelos do **ASP.NET 4.5.2** , selecione **MVC**. Verifique se a **caixa de seleção Habilitar suporte do Docker** não está selecionada e se a **autenticação** está definida como **sem autenticação**. Nomeie o projeto **MyASPApp**.)
    ::: moniker-end

2. Abra o arquivo  *HomeController.cs* e defina um ponto de interrupção no `About()` método.

## <a name="install-and-configure-iis-on-windows-server"></a><a name="bkmk_configureIIS"></a> Instalar e configurar o IIS no Windows Server

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>Atualizar as configurações de segurança do navegador no Windows Server

Se a configuração de segurança aprimorada estiver habilitada no Internet Explorer (habilitada por padrão), talvez seja necessário adicionar alguns domínios como sites confiáveis para que você possa baixar alguns dos componentes do servidor Web. Adicione os sites confiáveis acessando **Opções da Internet > segurança > sites confiáveis > sites**. Adicione os domínios a seguir.

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

Ao baixar o software, você pode obter solicitações para conceder permissão para carregar vários recursos e scripts de site. Alguns desses recursos não são necessários, mas para simplificar o processo, clique em **Adicionar** quando solicitado.

## <a name="install-aspnet-45-on-windows-server"></a><a name="BKMK_deploy_asp_net"></a> Instalar o ASP.NET 4,5 no Windows Server

Se você quiser informações mais detalhadas para instalar o ASP.NET no IIS, consulte [iis 8,0 usando ASP.NET 3,5 e ASP.NET 4,5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45).

1. No painel esquerdo de Gerenciador do Servidor, selecione **IIS**. Clique com o botão direito do mouse no servidor e selecione **Gerenciador de serviços de informações da Internet (IIS)**.

1. Use o Web Platform Installer (WebPI) para instalar o ASP.NET 4,5 (do nó do servidor no Windows Server 2012 R2, escolha **obter novos componentes da Web Platform** e, em seguida, pesquise por ASP.net)

    ![Captura de tela do Web Platform Installer 5,0 mostrando os resultados da pesquisa para asp.net com o componente de plataforma da Web IIS: ASP.NET 4,5 circulado em vermelho.](../debugger/media/remotedbg_iis_aspnet_45.png)

    > [!NOTE]
    > Se você estiver usando o Windows Server 2008 R2, instale o ASP.NET 4, em vez disso, usando este comando:

     **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe -ir**

2. Reinicie o sistema (ou execute **net stop foi/y** seguido por **net start W3SVC** em um prompt de comando para selecionar uma alteração no caminho do sistema).

## <a name="choose-a-deployment-option"></a>Escolha uma opção de implantação

Se precisar de ajuda para implantar o aplicativo no IIS, considere estas opções:

* Implante criando um arquivo de configurações de publicação no IIS e importando as configurações no Visual Studio. Em alguns cenários, essa é uma maneira rápida de implantar seu aplicativo. Quando você cria o arquivo de configurações de publicação, as permissões são configuradas automaticamente no IIS.

* Implante por meio da publicação em uma pasta local e copiando a saída por um método preferencial para uma pasta de aplicativo preparada no IIS.

## <a name="optional-deploy-using-a-publish-settings-file"></a>Adicional Implantar usando um arquivo de configurações de publicação

Você pode usar essa opção para criar um arquivo de configurações de publicação e importá-lo para o Visual Studio.

> [!NOTE]
> Esse método de implantação usa Implantação da Web, que deve ser instalado no servidor. Se desejar configurar Implantação da Web manualmente em vez de importar as configurações, você poderá instalar o Implantação da Web 3,6 em vez de Implantação da Web 3,6 para servidores de hospedagem. No entanto, se você configurar Implantação da Web manualmente, será necessário certificar-se de que uma pasta de aplicativo no servidor esteja configurada com os valores e permissões corretos (consulte [configurar site da ASP.net](#BKMK_deploy_asp_net)).

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>Instalar e configurar Implantação da Web para servidores de hospedagem no Windows Server

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>Criar o arquivo de configurações de publicação no IIS no Windows Server

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>Importar as configurações de publicação no Visual Studio e implantar

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

Depois que o aplicativo for implantado com êxito, ele deverá ser iniciado automaticamente. Se o aplicativo não iniciar no Visual Studio, inicie o aplicativo no IIS.

1. Alterne para uma configuração de depuração.

   ::: moniker range=">=vs-2019"
   Escolha **Editar** para editar o perfil e, em seguida, escolha **configurações**. Escolha uma configuração de **depuração** e escolha **remover arquivos adicionais no destino** nas opções de **publicação de arquivo** .
   ::: moniker-end
   ::: moniker range="vs-2017"
   Na caixa de diálogo **configurações** , habilite a depuração clicando em **Avançar**, escolha uma configuração de **depuração** e, em seguida, escolha **remover arquivos adicionais no destino** nas opções de **publicação de arquivo** .
   ::: moniker-end

   > [!IMPORTANT]
   > Se você escolher uma configuração de versão, desabilite a depuração no arquivo de *web.config* quando publicar.

1. Clique em **salvar** e Republique o aplicativo.

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>Adicional Implantar por publicação em uma pasta local

Você pode usar essa opção para implantar seu aplicativo se quiser copiar o aplicativo para o IIS usando o PowerShell, o RoboCopy ou desejar copiar manualmente os arquivos.

### <a name="configure-the-aspnet-web-site-on-the-windows-server-computer"></a><a name="BKMK_deploy_asp_net"></a> Configurar o site do ASP.NET no computador do Windows Server

1. Abra o Windows Explorer e crie uma nova pasta, **C:\Publish**, em que você implantará posteriormente o projeto ASP.net.

2. Se ainda não estiver aberto, abra o **Gerenciador do serviços de informações da Internet (IIS)**. (No painel esquerdo de Gerenciador do Servidor, selecione **IIS**. Clique com o botão direito do mouse e selecione **Gerenciador do IIS (Serviços de Informações da Internet)**).

3. Em **conexões** no painel esquerdo, vá para **sites**.

4. Selecione o **site da Web padrão**, escolha **configurações básicas** e defina o **caminho físico** como **C:\Publish**.

5. Clique com o botão direito do mouse no nó do **site da Web padrão** e selecione **Adicionar aplicativo**.

6. Defina o campo **alias** como **MyASPApp**, aceite o pool de aplicativos padrão (**DefaultAppPool**) e defina o **caminho físico** como **C:\Publish**.

7. Em **conexões**, selecione **pools de aplicativos**. Abra **DefaultAppPool** e defina o campo pool de aplicativos como **ASP.NET v 4.0** (ASP.NET 4,5 não é uma opção para o pool de aplicativos).

8. Com o site selecionado no Gerenciador do IIS, escolha **Editar permissões** e verifique se IUSR, IIS_IUSRS ou o usuário configurado para o pool de aplicativos é um usuário autorizado com direitos de execução de leitura &. Se nenhum desses usuários estiver presente, adicione IUSR como um usuário com direitos de execução de leitura &.

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>Publicar e implantar o aplicativo publicando em uma pasta local do Visual Studio

Você também pode publicar e implantar o aplicativo usando o sistema de arquivos ou outras ferramentas.

1. (ASP.NET 4.5.2) Certifique-se de que o arquivo web.config liste a versão correta do .NET.  Por exemplo, se você estiver direcionando ASP.NET 4.5.2, verifique se essa versão está listada em web.config.

    ```xml
    <system.web>
      <compilation debug="true" targetFramework="4.5.2" />
      <httpRuntime targetFramework="4.5.2" />
      <httpModules>
        <add name="ApplicationInsightsWebTracking" type="Microsoft.ApplicationInsights.Web.ApplicationInsightsHttpModule, Microsoft.AI.Web" />
      </httpModules>
    </system.web>

    ```

    Por exemplo, a versão deve ser 4,0 se você instalar ASP.NET 4 em vez de 4.5.2.

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

## <a name="download-and-install-the-remote-tools-on-windows-server"></a><a name="BKMK_msvsmon"></a> Baixar e instalar as ferramentas remotas no Windows Server

Baixe a versão das ferramentas remotas que corresponde à sua versão do Visual Studio.

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]

## <a name="set-up-the-remote-debugger-on-windows-server"></a><a name="BKMK_setup"></a> Configurar o depurador remoto no Windows Server

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> Se você precisar adicionar permissões para usuários adicionais, altere o modo de autenticação ou o número da porta para o depurador remoto, consulte [Configurar o depurador remoto](../debugger/remote-debugging.md#configure_msvsmon).

Para obter informações sobre como executar o depurador remoto como um serviço, consulte [executar o depurador remoto como um serviço](../debugger/remote-debugging.md#bkmk_configureService).

## <a name="attach-to-the-aspnet-application-from-the-visual-studio-computer"></a><a name="BKMK_attach"></a> Anexar ao aplicativo ASP.NET do computador do Visual Studio

1. No computador do Visual Studio, abra a solução que você está tentando depurar (**MyASPApp** se estiver seguindo as etapas neste artigo).
2. No Visual Studio, clique em **depurar > anexar ao processo** (CTRL + ALT + P).

    > [!TIP]
    > No Visual Studio 2017 e versões posteriores, você pode reanexar ao mesmo processo ao qual você anexou anteriormente usando **Debug > reanexar para processar...** (Shift + Alt + P).

3. Defina o campo qualificador como **\<remote computer name>** e pressione **Enter**.

    Verifique se o Visual Studio adiciona a porta necessária ao nome do computador, que aparece no formato: **\<remote computer name> :p classificar**

    ::: moniker range=">=vs-2019"
    No Visual Studio 2019, você deve ver **\<remote computer name> : 4024**
    ::: moniker-end
    ::: moniker range="vs-2017"
    No Visual Studio 2017, você deve ver **\<remote computer name> : 4022**
    ::: moniker-end
    A porta é necessária. Se você não vir o número da porta, adicione-o manualmente.

4. Clique em **Atualizar**.
    Você verá alguns processos exibidos na janela **processos disponíveis** .

    Se você não vir nenhum processo, tente usar o endereço IP em vez do nome do computador remoto (a porta é necessária). Você pode usar `ipconfig` o em uma linha de comando para obter o endereço IPv4.

5. Marque  **Mostrar processos de todos os usuários**.

6. Digite a primeira letra de um nome de processo para localizar rapidamente **w3wp.exe** para ASP.NET 4,5.

    Se você tiver vários processos mostrando **w3wp.exe**, verifique a coluna **nome de usuário** . Em alguns cenários, a coluna **nome de usuário** mostra o nome do pool de aplicativos, como o **IIS APPPOOL\DefaultAppPool**. Se você vir o pool de aplicativos, uma maneira fácil de identificar o processo correto é criar um novo pool de aplicativos nomeados para a instância do aplicativo que você deseja depurar e, em seguida, encontrá-lo facilmente na coluna **nome de usuário** .

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. Clique em **anexar**

8. Abra o site do computador remoto. Em um navegador, acesse **http:// \<remote computer name>**.

    Você deve ver a página da Web do ASP.NET.
9. No aplicativo ASP.NET em execução, clique no link para a página **sobre** .

    O ponto de interrupção deve ser atingido no Visual Studio.

## <a name="troubleshooting-open-required-ports-on-windows-server"></a><a name="bkmk_openports"></a>Solução de problemas Abra as portas necessárias no Windows Server

Na maioria das configurações, as portas necessárias são abertas pela instalação do ASP.NET e do depurador remoto. No entanto, talvez seja necessário verificar se as portas estão abertas.

> [!NOTE]
> Em uma VM do Azure, você deve abrir portas por meio do [grupo de segurança de rede](/azure/virtual-machines/windows/nsg-quickstart-portal).

Portas obrigatórias:

* 80-necessário para o IIS
::: moniker range=">=vs-2019"
* 4024-necessário para a depuração remota do Visual Studio 2019 (consulte [atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md) para obter mais informações).
::: moniker-end
::: moniker range="vs-2017"
* 4022-necessário para a depuração remota do Visual Studio 2017 (consulte [atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md) para obter mais informações).
::: moniker-end
* UDP 3702-a porta de descoberta (opcional) permite que você localize o botão **Localizar** ao anexar ao depurador remoto no Visual Studio.

1. Para abrir uma porta no Windows Server, abra o menu **Iniciar** , procure por **Firewall do Windows com segurança avançada**.

2. Em seguida, escolha **regras de entrada > nova regra > porta**. Escolha **Avançar** e, em **portas locais específicas**, insira o número da porta, clique em **Avançar** e, em seguida, **permitir a conexão**, clique em avançar e adicione o nome (**IIS**, **implantação da Web** ou **msvsmon**) para a regra de entrada.

    Se você quiser obter mais detalhes sobre como configurar o Firewall do Windows, consulte [Configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md).

3. Crie regras adicionais para as outras portas necessárias.