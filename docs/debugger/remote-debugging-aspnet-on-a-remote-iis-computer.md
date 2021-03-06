---
title: ASP.NET Core de depuração remota em um computador IIS remoto | Microsoft Docs
description: Depure um aplicativo ASP.NET Core que foi implantado em um computador Serviços de Informações da Internet remoto (IIS) usando o depurador remoto do Visual Studio.
ms.custom: remotedebugging, SEO-VS-2020
ms.date: 05/06/2020
ms.topic: conceptual
ms.assetid: 573a3fc5-6901-41f1-bc87-557aa45d8858
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: a364289ded27879c74767f03e89b9ea7b9f604fc
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249902"
---
# <a name="remote-debug-aspnet-core-on-a-remote-iis-computer-in-visual-studio"></a>ASP.NET Core de depuração remota em um computador IIS remoto no Visual Studio

Para depurar um aplicativo ASP.NET Core que foi implantado no IIS, instale e execute as ferramentas remotas no computador em que você implantou seu aplicativo e, em seguida, anexe ao seu aplicativo em execução no Visual Studio.

![Componentes do depurador remoto](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

Este guia explica como configurar e configurar um ASP.NET Core do Visual Studio, implantá-lo no IIS e anexar o depurador remoto do Visual Studio. Para depuração remota ASP.NET 4.5.2, consulte [ASP.net de depuração remota em um computador IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md). Você também pode implantar e depurar no IIS usando o Azure. Para Azure App serviço, você pode facilmente implantar e depurar em uma instância pré-configurada do IIS e no depurador remoto usando o [depurador de instantâneos](../debugger/debug-live-azure-applications.md) ou [anexando o depurador de Gerenciador de servidores](../debugger/remote-debugging-azure.md).

## <a name="prerequisites"></a>Pré-requisitos

::: moniker range=">=vs-2019"
O Visual Studio 2019 é necessário para seguir as etapas mostradas neste artigo.
::: moniker-end
::: moniker range="vs-2017"
O Visual Studio 2017 é necessário para seguir as etapas mostradas neste artigo.
::: moniker-end

Esses procedimentos foram testados nessas configurações de servidor:
* Windows Server 2012 R2 e IIS 8
* Windows Server 2016 e IIS 10
* Windows Server 2019 e IIS 10

## <a name="network-requirements"></a>Requisitos de rede

Não há suporte para a depuração entre dois computadores conectados por meio de um proxy. A depuração em uma conexão de alta latência ou de baixa largura de banda, como a Internet dial-up ou pela Internet entre países, não é recomendada e pode falhar ou ser lenta de forma inaceitável. Para obter uma lista completa dos requisitos, consulte [requisitos](../debugger/remote-debugging.md#requirements_msvsmon).

## <a name="app-already-running-in-iis"></a>O aplicativo já está em execução no IIS?

Este artigo inclui etapas sobre como configurar uma configuração básica do IIS no Windows Server e implantar o aplicativo do Visual Studio. Essas etapas estão incluídas para verificar se o servidor tem os componentes necessários instalados, se o aplicativo pode ser executado corretamente e se você está pronto para depuração remota.

* Se seu aplicativo estiver em execução no IIS e você quiser apenas baixar o depurador remoto e iniciar a depuração, acesse [baixar e instalar as ferramentas remotas no Windows Server](#BKMK_msvsmon).

* Se você quiser obter ajuda para certificar-se de que seu aplicativo está configurado, implantado e em execução corretamente no IIS para que você possa depurar, siga todas as etapas neste tópico.

## <a name="create-the-aspnet-core-application-on-the-visual-studio-computer"></a>Criar o aplicativo ASP.NET Core no computador do Visual Studio

1. Crie um novo Aplicativo Web ASP.NET Core.

    ::: moniker range=">=vs-2019"
    No Visual Studio 2019, escolha **criar um novo projeto** na janela iniciar. Se a janela iniciar não estiver aberta, escolha **arquivo**  >  **Iniciar janela**. Digite **aplicativo Web**, escolha **C#** como idioma, escolha **ASP.NET Core aplicativo Web (Model-View-Controller)** e, em seguida, escolha **Avançar**. Na próxima tela, nomeie o projeto **MyASPApp** e escolha **Avançar**.

    Escolha a estrutura de destino recomendada (.NET Core 3,1) ou .NET 5 e, em seguida, escolha **criar**.
    ::: moniker-end
    ::: moniker range="vs-2017"
    No Visual Studio 2017, escolha **arquivo > novo projeto de >** e, em seguida, selecione **Visual C# > Web > ASP.NET Core aplicativo Web**. Na seção modelos de ASP.NET Core, selecione **aplicativo Web (Model-View-Controller)**. Certifique-se de que ASP.NET Core 2,1 está selecionado, que **habilitar o suporte ao Docker** não está selecionado e que a **autenticação** está definida como **sem autenticação**. Nomeie o projeto **MyASPApp**.
    ::: moniker-end

4. Abra o arquivo About.cshtml.cs e defina um ponto de interrupção no `OnGet` método (em modelos mais antigos, abra HomeController.cs em vez disso e defina o ponto de interrupção no `About()` método).

## <a name="install-and-configure-iis-on-windows-server"></a><a name="bkmk_configureIIS"></a> Instalar e configurar o IIS no Windows Server

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>Atualizar as configurações de segurança do navegador no Windows Server

Se a configuração de segurança aprimorada estiver habilitada no Internet Explorer (habilitada por padrão), talvez seja necessário adicionar alguns domínios como sites confiáveis para que você possa baixar alguns dos componentes do servidor Web. Adicione os sites confiáveis acessando **Opções da Internet > segurança > sites confiáveis > sites**. Adicione os domínios a seguir.

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

Ao baixar o software, você pode obter solicitações para conceder permissão para carregar vários recursos e scripts de site. Alguns desses recursos não são necessários, mas para simplificar o processo, clique em **Adicionar** quando solicitado.

## <a name="install-aspnet-core-on-windows-server"></a>Instalar o ASP.NET Core no Windows Server

1. Instale o pacote de hospedagem do .NET Core no sistema de hospedagem. O pacote instala o Runtime .NET Core, a Biblioteca do .NET Core e o Módulo do ASP.NET Core. Para obter instruções mais detalhadas, consulte [publicando no IIS](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration).

    Para o .NET Core 3, instale o [pacote de hospedagem do .NET Core](https://dotnet.microsoft.com/permalink/dotnetcore-current-windows-runtime-bundle-installer).
    Para o .NET Core 2, instale a [hospedagem do Windows Server do .NET Core](https://aka.ms/dotnetcore-2-windowshosting).

    > [!NOTE]
    > Se o sistema não tiver uma conexão com a Internet, obtenha e instale os *[Pacotes redistribuíveis do Microsoft Visual C++ 2015](https://www.microsoft.com/download/details.aspx?id=53840)* antes de instalar o pacote de hospedagem do Windows Server do .NET Core.

2. Reinicie o sistema (ou execute **net stop foi/y** seguido por **net start W3SVC** em um prompt de comando para selecionar uma alteração no caminho do sistema).

## <a name="choose-a-deployment-option"></a>Escolha uma opção de implantação

Se precisar de ajuda para implantar o aplicativo no IIS, considere estas opções:

* Implante criando um arquivo de configurações de publicação no IIS e importando as configurações no Visual Studio. Em alguns cenários, essa é uma maneira rápida de implantar seu aplicativo. Quando você cria o arquivo de configurações de publicação, as permissões são configuradas automaticamente no IIS.

* Implante por meio da publicação em uma pasta local e copiando a saída por um método preferencial para uma pasta de aplicativo preparada no IIS.

## <a name="optional-deploy-using-a-publish-settings-file"></a>Adicional Implantar usando um arquivo de configurações de publicação

Você pode usar essa opção para criar um arquivo de configurações de publicação e importá-lo para o Visual Studio.

> [!NOTE]
> Esse método de implantação usa Implantação da Web, que deve ser instalado no servidor. Se desejar configurar Implantação da Web manualmente em vez de importar as configurações, você poderá instalar o Implantação da Web 3,6 em vez de Implantação da Web 3,6 para servidores de hospedagem. No entanto, se você configurar Implantação da Web manualmente, será necessário certificar-se de que uma pasta de aplicativo no servidor esteja configurada com os valores e permissões corretos (consulte [configurar site da ASP.net](#BKMK_deploy_asp_net)).

### <a name="configure-the-aspnet-core-web-site"></a>Configurar o site da ASP.NET Core

1. No Gerenciador do IIS, no painel esquerdo, em **conexões**, selecione **pools de aplicativos**. Abra **DefaultAppPool** e defina a **versão .NET CLR** como **sem código gerenciado**. Isso é necessário para ASP.NET Core. O site padrão usa DefaultAppPool.

2. Pare e reinicie o DefaultAppPool.

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>Instalar e configurar Implantação da Web para servidores de hospedagem no Windows Server

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>Criar o arquivo de configurações de publicação no IIS no Windows Server

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>Importar as configurações de publicação no Visual Studio e implantar

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

Depois que o aplicativo for implantado com êxito, ele deverá ser iniciado automaticamente. Se o aplicativo não iniciar no Visual Studio, inicie o aplicativo no IIS para verificar se ele é executado corretamente. Por ASP.NET Core, você também precisa certificar-se de que o campo pool de aplicativos para **DefaultAppPool** esteja definido como **nenhum código gerenciado**.

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

### <a name="configure-the-aspnet-core-web-site-on-the-windows-server-computer"></a><a name="BKMK_deploy_asp_net"></a> Configurar o site do ASP.NET Core no computador do Windows Server

1. Abra o Windows Explorer e crie uma nova pasta, **C:\Publish**, em que você implantará posteriormente o projeto ASP.NET Core.

2. Se ainda não estiver aberto, abra o **Gerenciador do serviços de informações da Internet (IIS)**. (No painel esquerdo de Gerenciador do Servidor, selecione **IIS**. Clique com o botão direito do mouse e selecione **Gerenciador do IIS (Serviços de Informações da Internet)**).

3. Em **conexões** no painel esquerdo, vá para **sites**.

4. Selecione o **site da Web padrão**, escolha **configurações básicas** e defina o **caminho físico** como **C:\Publish**.

5. Clique com o botão direito do mouse no nó do **site da Web padrão** e selecione **Adicionar aplicativo**.

6. Defina o campo **alias** como **MyASPApp**, aceite o pool de aplicativos padrão (**DefaultAppPool**) e defina o **caminho físico** como **C:\Publish**.

7. Em **conexões**, selecione **pools de aplicativos**. Abra **DefaultAppPool** e defina o campo pool de aplicativos como **sem código gerenciado**.

8. Clique com o botão direito do mouse no novo site no Gerenciador do IIS, escolha **Editar permissões** e certifique-se de que IUSR, IIS_IUSRS ou o usuário configurado para acesso ao aplicativo Web é um usuário autorizado com direitos de execução de leitura &.

    Se você não vir um desses usuários com acesso, siga as etapas para adicionar IUSR como um usuário com direitos de execução de leitura &.

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>Publicar e implantar o aplicativo publicando em uma pasta local do Visual Studio

Você também pode publicar e implantar o aplicativo usando o sistema de arquivos ou outras ferramentas.

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

1. No computador do Visual Studio, abra a solução que você está tentando depurar (**MyASPApp** se você estiver seguindo todas as etapas neste artigo).
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

    Se você quiser usar o botão **Localizar** , talvez seja necessário abrir a [porta UDP 3702](#bkmk_openports) no servidor.

5. Marque  **Mostrar processos de todos os usuários**.

6. Digite a primeira letra do nome do processo para localizar rapidamente seu aplicativo.

    * Se você estiver usando o [modelo de hospedagem em processo](/aspnet/core/host-and-deploy/aspnet-core-module?view=aspnetcore-3.1&preserve-view=true#hosting-models) no IIS, selecione o processo de **w3wp.exe** correto. A partir do .NET Core 3, esse é o padrão.

    * Caso contrário, selecione o processo de **dotnet.exe** . (Esse é o modelo de hospedagem fora do processo.)

    Se você tiver vários processos mostrando *w3wp.exe* ou *dotnet.exe*, verifique a coluna **nome de usuário** . Em alguns cenários, a coluna **nome de usuário** mostra o nome do pool de aplicativos, como o **IIS APPPOOL\DefaultAppPool**. Se você vir o pool de aplicativos, mas ele não for exclusivo, crie um novo pool de aplicativos nomeados para a instância do aplicativo que você deseja depurar e, em seguida, você poderá encontrá-lo facilmente na coluna **nome de usuário** .

    ::: moniker range=">=vs-2019"
    ![RemoteDBG_AttachToProcess](../debugger/media/vs-2019/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end
    ::: moniker range="vs-2017"
    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg-attachtoprocess-aspnetcore.png "RemoteDBG_AttachToProcess")
    ::: moniker-end

7. Clique em **Anexar**.

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

2. Em seguida, escolha **regras de entrada > nova regra > porta** e clique em **Avançar**. (Para UDP 3702, escolha **regras de saída** em vez disso.)

3. Em **portas locais específicas**, insira o número da porta e clique em **Avançar**.

4. Clique em **permitir a conexão**, clique em **Avançar**.

5. Selecione um ou mais tipos de rede para habilitar para a porta e clique em **Avançar**.

    O tipo selecionado deve incluir a rede à qual o computador remoto está conectado.
6. Adicione o nome (por exemplo, **IIS**, **implantação da Web** ou **msvsmon**) para a regra de entrada e clique em **concluir**.

    Você deve ver sua nova regra na lista regras de entrada ou regras de saída.

    Se você quiser obter mais detalhes sobre como configurar o Firewall do Windows, consulte [Configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md).

3. Crie regras adicionais para as outras portas necessárias.
