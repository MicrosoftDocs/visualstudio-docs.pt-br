---
title: ASP.NET Core no IIS e o Azure de depuração remota | Microsoft Docs
ms.custom: remotedebugging
ms.date: 05/21/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: a6c04b53-d1b9-4552-a8fd-3ed6f4902ce6
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
- dotnetcore
- azure
ms.openlocfilehash: 821da7c5d131acea62e944055ec6c450e4bc5154
ms.sourcegitcommit: 40b6438b5acd7e59337a382c39ec711b9e99cc8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49101102"
---
# <a name="remote-debug-aspnet-core-on-iis-in-azure-in-visual-studio-2017"></a>Depuração remota do ASP.NET Core no IIS no Azure no Visual Studio 2017

Este guia explica como configurar e configurar um aplicativo ASP.NET Core do Visual Studio 2017, implantá-lo no IIS usando o Azure e anexar o depurador remoto do Visual Studio.

A maneira recomendada para depuração remota no Azure depende de seu cenário:

* Para depurar o ASP.NET Core no serviço de aplicativo do Azure, consulte [depurar aplicativos do Azure usando o depurador de instantâneo](../debugger/debug-live-azure-applications.md). Esse é o método recomendado.
* Para depurar o ASP.NET Core no serviço de aplicativo do Azure usando os recursos de depuração mais tradicionais, siga as etapas neste tópico (consulte a seção [depuração remota no serviço de aplicativo do Azure](#remote_debug_azure_app_service)).

    Nesse cenário, você deve implantar seu aplicativo do Visual Studio para o Azure, mas não é necessário instalar manualmente ou configurar o IIS ou o depurador remoto (esses componentes são representados com linhas pontilhadas), conforme mostrado na ilustração a seguir.

    ![Componentes do depurador remoto](../debugger/media/remote-debugger-azure-app-service.png "Remote_debugger_components")

* Para depurar o IIS em uma VM do Azure, siga as etapas neste tópico (consulte a seção [depuração remota em uma VM do Azure](#remote_debug_azure_vm)). Isso permite que você use uma configuração personalizada do IIS, mas as etapas de instalação e implantação são mais complicadas.

    Para uma VM do Azure, você deve implantar seu aplicativo do Visual Studio para o Azure e você também precisará instalar manualmente a função do IIS e o depurador remoto, conforme mostrado na ilustração a seguir.

    ![Componentes do depurador remoto](../debugger/media/remote-debugger-azure-vm.png "Remote_debugger_components")

* Para depurar o ASP.NET Core no Azure Service Fabric, consulte [depurar um aplicativo do Service Fabric remoto](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application).

> [!WARNING]
> Certifique-se de excluir os recursos do Azure que você cria quando você tiver concluído as etapas neste tutorial. Dessa forma, que você pode evitar incorrer em encargos desnecessários.


### <a name="requirements"></a>Requisitos

Não há suporte para depuração entre dois computadores conectados por meio de um proxy. Depuração em uma alta latência ou a conexão de baixa largura de banda, como dial-up da Internet, ou pela Internet entre países não é recomendado e pode falhar ou ser muito lento. Para obter uma lista completa dos requisitos, consulte [requisitos de](../debugger/remote-debugging.md#requirements_msvsmon).

## <a name="create-the-aspnet-core-application-on-the-visual-studio-2017-computer"></a>Criar o aplicativo ASP.NET Core no computador do Visual Studio 2017 

1. Crie um novo aplicativo ASP.NET Core. (Escolha **arquivo > Novo > projeto**, em seguida, selecione **Visual c# > Web > aplicativo Web ASP.NET Core**).

    No **ASP.NET Core** seção de modelos, selecione **aplicativo Web**.

2. Certifique-se de que **ASP.NET Core 2.0** está selecionado, que **Habilitar suporte ao Docker** é **não** selecionado e que **autenticação** é definido como **Nenhuma autenticação**.

3. Nomeie o projeto **MyASPApp** e clique em **Okey** para criar a nova solução.

4. Abra o arquivo About.cshtml.cs e defina um ponto de interrupção na `OnGet` método (em modelos mais antigos, abra HomeController.cs em vez disso e defina o ponto de interrupção `About()` método).

## <a name="remote_debug_azure_app_service"></a> Depuração remota do ASP.NET Core em um serviço de aplicativo do Azure

No Visual Studio, você pode publicar e depurar seu aplicativo a uma instância totalmente provisionado do IIS rapidamente. No entanto, a configuração do IIS é predefinida e não é possível personalizá-lo. Para obter instruções mais detalhadas, consulte [implantar um aplicativo web ASP.NET Core no Azure usando o Visual Studio](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs). (Se você precisar de capacidade de personalizar o IIS, experimente a depuração um [Azure VM](#remote_debug_azure_vm).) 

#### <a name="to-deploy-the-app-and-remote-debug-using-server-explorer"></a>Para implantar o aplicativo e a depuração remota usando o Gerenciador de servidores

1. No Visual Studio, clique com botão direito no nó do projeto e escolha **publicar**.

    Se você já tiver configurado qualquer perfil de publicação, o **publicar** painel será exibido. Clique em **novo perfil**.

1. Escolher **serviço de aplicativo do Azure** da **Publish** caixa de diálogo, selecione **criar novo**e siga os prompts para publicar.

    Para obter instruções detalhadas, consulte [implantar um aplicativo web ASP.NET Core no Azure usando o Visual Studio](/aspnet/core/tutorials/publish-to-azure-webapp-using-vs).

    ![Publicar no Serviço de Aplicativo do Azure](../debugger/media/remotedbg_azure_app_service_profile.png)

1. Abra **Gerenciador de servidores** (**exibição** > **Server Explorer**), clique com botão direito na instância do serviço de aplicativo e escolha **Anexar depurador**.

1. No aplicativo ASP.NET em execução, clique no link para o **sobre** página.

    O ponto de interrupção deve ser atingido no Visual Studio.

    É só isso! O restante das etapas neste tópico se aplicam a depuração remota em uma VM do Azure.

## <a name="remote_debug_azure_vm"></a> Depuração remota do ASP.NET Core em uma VM do Azure

Você pode criar uma VM do Azure para o Windows Server e, em seguida, instalar e configurar o IIS e os outros componentes de software necessárias. Isso leva mais tempo do que a implantação em um serviço de aplicativo do Azure e requer que você siga as etapas restantes neste tutorial.

Primeiro, siga as etapas descritas em [instalar e executar o IIS](/azure/virtual-machines/windows/quick-create-portal).

Quando você abre a porta 80 no grupo de segurança de rede, também abra a porta 4022 para o depurador remoto. Dessa forma, você não precisará abri-lo mais tarde.

### <a name="app-already-running-in-iis-on-the-azure-vm"></a>Aplicativo já em execução no IIS na VM do Azure?

Este artigo inclui etapas sobre como configurar uma configuração básica do IIS no Windows server e implantar o aplicativo do Visual Studio. Essas etapas são incluídas para certificar-se de que o servidor tem os componentes necessários instalados, que o aplicativo pode ser executado corretamente e que você está pronto para depuração remota.

* Se o aplicativo é executado no IIS e quiser apenas baixar o depurador remoto e iniciar a depuração, vá para [Baixe e instale as ferramentas remotas no Windows Server](#BKMK_msvsmon).

* Se você deseja obter ajuda para certificar-se de que seu aplicativo é configurado, implantado e executando corretamente no IIS para que você possa depurar, siga as etapas neste tópico.

### <a name="update-browser-security-settings-on-windows-server"></a>Atualizar configurações de segurança do navegador no Windows Server

Se a configuração de segurança aprimorada estiver habilitada no Internet Explorer (ela é habilitada por padrão), em seguida, você precisa adicionar alguns domínios como sites confiáveis para que você possa baixar alguns dos componentes do servidor web. Adicione os sites confiáveis acessando **opções da Internet > Segurança > Sites confiáveis > Sites**. Adicione os domínios a seguir.

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- IIS.NET

Quando você baixar o software, você pode receber solicitações para conceder permissão para carregar vários scripts do site da web e recursos. Alguns desses recursos não são necessárias, mas para simplificar o processo, clique em **adicionar** quando solicitado.

### <a name="install-aspnet-core-on-windows-server"></a>Instalar o ASP.NET Core no Windows Server

1. Instalar o [hospedagem do .NET Core Windows Server](https://aka.ms/dotnetcore-2-windowshosting) pacote no sistema de hospedagem. O pacote instalará o módulo do ASP.NET Core, biblioteca do .NET Core e o tempo de execução do .NET Core. Para obter mais instruções detalhadas, consulte [publicar no IIS](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration).

    > [!NOTE]
    > Se o sistema não tiver uma conexão de Internet, obtenha e instale o *[Microsoft Visual C++ 2015 redistribuível](https://www.microsoft.com/download/details.aspx?id=53840)* antes de instalar o pacote de hospedagem do .NET Core Windows Server.

3. Reinicie o sistema (ou execute **net stop was /y** seguido **net start w3svc-** em um prompt de comando para acompanhar uma alteração no caminho do sistema).

## <a name="choose-a-deployment-option"></a>Escolha uma opção de implantação

Se você precisar de ajuda para implantar o aplicativo no IIS, considere estas opções:

* Implante criando um arquivo de configurações de publicação no IIS e importar as configurações no Visual Studio. Em alguns cenários, isso é uma maneira rápida de implantar seu aplicativo. Quando você cria o arquivo de configurações de publicação, permissões são automaticamente definidas no IIS.

* Implante, publicando em uma pasta local e copiar a saída por um método preferencial para uma pasta de aplicativo preparado no IIS.

## <a name="optional-deploy-using-a-publish-settings-file"></a>(Opcional) Implantar usando um arquivo de configurações de publicação

Você pode usar essa opção de criar um arquivo de configurações de publicação e importe-o para o Visual Studio.

> [!NOTE]
> Esse método de implantação usa a implantação da Web. Se você quiser configurar a implantação da Web manualmente no Visual Studio em vez de importar as configurações, você pode instalar o Web implantar 3.6, em vez de Web implantar 3.6 para servidores de hospedagem. No entanto, se você configurar a implantação da Web manualmente, você precisará certificar-se de que uma pasta do aplicativo no servidor é configurada com os valores corretos e as permissões (consulte [configurar o site da Web ASP.NET](#BKMK_deploy_asp_net)).

### <a name="install-and-configure-web-deploy-for-hosting-servers-on-windows-server"></a>Instalar e configurar a implantação da Web para hospedar servidores no Windows Server

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/install-web-deploy-with-hosting-server.md)]

### <a name="create-the-publish-settings-file-in-iis-on-windows-server"></a>Criar o arquivo de configurações de publicação no IIS no Windows Server

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/create-publish-settings-iis.md)]

### <a name="import-the-publish-settings-in-visual-studio-and-deploy"></a>Importar as configurações de publicação no Visual Studio e implantar

[!INCLUDE [install-web-deploy-with-hosting-server](../deployment/includes/import-publish-settings-vs.md)]

Depois que o aplicativo é implantado com êxito, ele deve ser iniciado automaticamente. Se o aplicativo não for iniciado do Visual Studio, inicie o aplicativo no IIS. Para o ASP.NET Core, você precisará certificar-se de que o pool de aplicativos de campo para o **DefaultAppPool** é definido como **sem código gerenciado**.

1. No **as configurações** caixa de diálogo, ative a depuração clicando **próxima**, escolha um **depurar** configuração e, em seguida, escolha **remover arquivos adicionais no destino** sob o **Publicar arquivo** opções.

    > [!NOTE]
    > Se você escolher uma configuração de versão, você desabilitar a depuração na *Web. config* arquivo quando você publicar.

1. Clique em **salvar** e, em seguida, republicar o aplicativo.

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>(Opcional) Implantar pela publicação em uma pasta local

Você pode usar essa opção para implantar seu aplicativo se você deseja copiar o aplicativo para o IIS usando o Powershell, RoboCopy, ou você deseja copiar os arquivos manualmente.

### <a name="BKMK_deploy_asp_net"></a> Configurar o site da Web ASP.NET no computador com Windows Server

Se você estiver importando as configurações de publicação, você poderá ignorar esta seção.

1. Abra o **Gerenciador de serviços de informações da Internet (IIS)** e vá para **Sites**.

2. Clique com botão direito do **Site padrão** nó e selecione **Adicionar aplicativo**.

3. Defina as **Alias** campo **MyASPApp** e o campo de pool de aplicativos para **sem código gerenciado**. Defina as **caminho físico** ao **C:\Publish** (onde você irá implantar posteriormente o projeto do ASP.NET).

4. Com o site selecionado no Gerenciador do IIS, escolha **editar permissões**e certifique-se de que IUSR, IIS_IUSRS ou o usuário configurado para o Pool de aplicativos é um usuário autorizado com direitos de leitura e execução.

    Se você não vir um desses usuários com acesso, percorra as etapas para adicionar IUSR como um usuário com direitos de leitura e execução.

### <a name="optional-publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>(Opcional) Publicar e implantar o aplicativo pela publicação em uma pasta local do Visual Studio

Se você não estiver usando a implantação da Web, você deve publicar e implantar o aplicativo usando o sistema de arquivos ou outras ferramentas. Você pode começar criando um pacote usando o sistema de arquivos e, em seguida, implantar o pacote manualmente ou usar outras ferramentas, como XCopy, RoboCopy ou PowerShell. Nesta seção, presumimos que você estiver copiando o pacote manualmente se você não estiver usando a implantação da Web.

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

### <a name="BKMK_msvsmon"></a> Baixe e instale as ferramentas remotas no Windows Server

Neste tutorial, estamos usando o Visual Studio 2017.

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]
  
### <a name="BKMK_setup"></a> Configurar o depurador remoto no Windows Server

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> Se você precisar adicionar permissões para usuários adicionais, alterar o modo de autenticação ou número da porta para o depurador remoto, consulte [configurar o depurador remoto](../debugger/remote-debugging.md#configure_msvsmon).

### <a name="BKMK_attach"></a> Anexar ao aplicativo ASP.NET de computador do Visual Studio

1. No computador do Visual Studio, abra a solução que você está tentando depurar (**MyASPApp** se você estiver seguindo as etapas neste artigo).
2. No Visual Studio, clique em **Depurar > Anexar ao processo** (Ctrl + Alt + P).

    > [!TIP]
    > No Visual Studio 2017, você pode anexar novamente para o mesmo processo anteriormente anexado ao usando **Depurar > anexar novamente ao processo...** (Shift + Alt + P). 

3. Definir o qualificador de campo para  **\<nome do computador remoto >: 4022**.
4. Clique em **Refresh**.
    Você deve ver alguns processos que aparecem na **processos disponíveis** janela.

    Se você não vir todos os processos, tente usar o endereço IP em vez do nome do computador remoto (a porta é necessária). Você pode usar `ipconfig` em uma linha de comando para obter o endereço IPv4.

    Se você quiser usar o **encontrar** botão, talvez você precise [abra a porta UDP 3702](#bkmk_openports) no servidor.

5. Verifique **Mostrar processos de todos os usuários**.

6. Digite a primeira letra do nome de um processo para localizar rapidamente *dotnet.exe* (para o ASP.NET Core).
   
   Para um aplicativo ASP.NET Core, o nome do processo anterior foi *dnx.exe*.

    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg_attachtoprocess_aspnetcore.png "RemoteDBG_AttachToProcess")

7. Clique em **Anexar**.

8. Abra o site do computador remoto. Em um navegador, vá para **http://\<nome do computador remoto >**.
    
    Você deve ver a página da web ASP.NET.
9. No aplicativo ASP.NET em execução, clique no link para o **sobre** página.

    O ponto de interrupção deve ser atingido no Visual Studio.

### <a name="bkmk_openports"></a> Solução de problemas: Abrir as portas necessárias no Windows Server

Na maioria das configurações, as portas necessárias estão abertas pela instalação do ASP.NET e o depurador remoto. No entanto, se você estiver solucionando problemas de implantação e o aplicativo é hospedado atrás de um firewall, você precisa verificar se as portas corretas estão abertas.

Em uma VM do Azure, você deve abrir as portas por meio de [grupo de segurança de rede](/azure/virtual-machines/virtual-machines-windows-hero-role#open-port-80-for-web-traffic). 

Portas necessárias:

- 80 - obrigatórias para IIS
- 4022 - necessários para a depuração remota do Visual Studio 2017 (consulte [as atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md) para obter mais informações).
- UDP 3702 - porta (opcional) descoberta permite que você os **localizar** botão ao anexar ao depurador remoto no Visual Studio.

Além disso, essas portas já devem ser abertas pela instalação do ASP.NET:
- 8172 - (opcional) necessária para a implantação da Web para implantar o aplicativo do Visual Studio

