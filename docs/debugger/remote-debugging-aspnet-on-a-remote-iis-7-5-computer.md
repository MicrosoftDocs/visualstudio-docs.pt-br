---
title: Depuração remota do ASP.NET em um computador com IIS
ms.custom:
- remotedebugging
- seodec18
ms.date: 05/21/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 9cb339b5-3caf-4755-aad1-4a5da54b2a23
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
ms.openlocfilehash: 336f34c1229e07eb3734f9d278070e5994957d16
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53065552"
---
# <a name="remote-debug-aspnet-on-a-remote-iis-computer"></a>Depuração remota do ASP.NET em um computador remoto IIS
Para depurar um aplicativo ASP.NET que tenha sido implantado no IIS, instalar e executar as ferramentas remotas no computador onde você implantou seu aplicativo e, em seguida, anexar a seu aplicativo em execução do Visual Studio.

![Componentes do depurador remoto](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

Este guia explica como configurar e configurar um aplicativo do Visual Studio 2017 ASP.NET MVC 4.5.2, implantá-lo no IIS e anexar o depurador remoto do Visual Studio.

> [!NOTE]
> Para remoto depurar o ASP.NET Core em vez disso, consulte [remota de depuração do ASP.NET Core em um computador IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-computer.md). Para o serviço de aplicativo do Azure, você pode facilmente implantar e depurar em uma instância pré-configurada do IIS usando o [depurador de instantâneo](../debugger/debug-live-azure-applications.md) (.NET 4.6.1 exigido) ou pelo [anexando o depurador do Gerenciador de servidores](../debugger/remote-debugging-azure.md).

Esses procedimentos foram testados nessas configurações de servidor:
* Windows Server 2012 R2 e IIS 8 (para o Windows Server 2008 R2, as etapas do servidor são diferentes)

## <a name="requirements"></a>Requisitos

O depurador remoto tem suporte no Windows Server a partir do Windows Server 2008 Service Pack 2. Para obter uma lista completa dos requisitos, consulte [requisitos de](../debugger/remote-debugging.md#requirements_msvsmon).

> [!NOTE]
> Não há suporte para depuração entre dois computadores conectados por meio de um proxy. Depuração em uma alta latência ou a conexão de baixa largura de banda, como dial-up da Internet, ou pela Internet entre países não é recomendado e pode falhar ou ser muito lento.

## <a name="app-already-running-in-iis"></a>Aplicativo já em execução no IIS?

Este artigo inclui etapas sobre como configurar uma configuração básica do IIS no Windows server e implantar o aplicativo do Visual Studio. Essas etapas são incluídas para certificar-se de que o servidor tem necessário componentes instalados, que o aplicativo pode ser executado corretamente e que você está pronto para depuração remota.

* Se o aplicativo é executado no IIS e quiser apenas baixar o depurador remoto e iniciar a depuração, vá para [Baixe e instale as ferramentas remotas no Windows Server](#BKMK_msvsmon).

* Se você deseja obter ajuda para certificar-se de que seu aplicativo é configurado, implantado e executando corretamente no IIS para que você possa depurar, siga as etapas neste tópico.

## <a name="create-the-aspnet-452-application-on-the-visual-studio-computer"></a>Criar do ASP.NET 4.5.2 aplicativo no computador do Visual Studio
  
1. Crie um novo aplicativo ASP.NET MVC. (**Arquivo > Novo > projeto**, em seguida, selecione <strong>Visual C# > Web > aplicativo Web ASP.NET. No **ASP.NET 4.5.2</strong> seção de modelos, selecione **MVC**. Certifique-se de que **Habilitar suporte ao Docker** não está selecionado e que **autenticação** está definido como **sem autenticação**. Nomeie o projeto **MyASPApp**.)

2. Abra o arquivo HomeController.cs e defina um ponto de interrupção `About()` método.

## <a name="bkmk_configureIIS"></a> Instalar e configurar o IIS no Windows Server

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>Atualizar configurações de segurança do navegador no Windows Server

Se a configuração de segurança aprimorada estiver habilitada no Internet Explorer (ela é habilitada por padrão), em seguida, você precisa adicionar alguns domínios como sites confiáveis para que você possa baixar alguns dos componentes do servidor web. Adicione os sites confiáveis acessando **opções da Internet > Segurança > Sites confiáveis > Sites**. Adicione os domínios a seguir.

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- iis.net

Quando você baixar o software, você pode receber solicitações para conceder permissão para carregar vários scripts do site da web e recursos. Alguns desses recursos não são necessárias, mas para simplificar o processo, clique em **adicionar** quando solicitado.

## <a name="BKMK_deploy_asp_net"></a> Instalar o ASP.NET 4.5 no Windows Server

Se você quiser obter informações mais detalhadas para instalar o ASP.NET no IIS, consulte [IIS 8.0 usando ASP.NET 3.5 e ASP.NET 4.5](/iis/get-started/whats-new-in-iis-8/iis-80-using-aspnet-35-and-aspnet-45).

1. No painel esquerdo do Gerenciador do servidor, selecione **IIS**. Clique com o botão direito do mouse e selecione **Gerenciador do IIS (Serviços de Informações da Internet)**.

1. Use o Web Platform Installer (WebPI) para instalar o ASP.NET 4.5 (no nó do servidor no Windows Server 2012 R2, escolha **obter novos componentes do Web Platform** e, em seguida, pesquise por ASP.NET)

    ![RemoteDBG_IIS_AspNet_45](../debugger/media/remotedbg_iis_aspnet_45.png "RemoteDBG_IIS_AspNet_45")

    > [!NOTE]
    > Se você estiver usando o Windows Server 2008 R2, instale o ASP.NET 4, em vez de usar este comando:

     **C:\Windows\Microsoft.NET\Framework64\v4.0.30319\aspnet_regiis.exe - ir**

2. Reinicie o sistema (ou execute **net stop was /y** seguido por **net start w3svc** em um prompt de comando para reconhecer uma alteração no PATH do sistema).

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

Depois que o aplicativo for implantado com êxito, ele deverá ser iniciado automaticamente. Se o aplicativo não for iniciado do Visual Studio, inicie o aplicativo no IIS.

1. No **as configurações** caixa de diálogo, ative a depuração clicando **próxima**, escolha um **depurar** configuração e, em seguida, escolha **remover arquivos adicionais no destino** sob o **Publicar arquivo** opções.

    > [!NOTE]
    > Se você escolher uma configuração de versão, você desabilitar a depuração na *Web. config* arquivo quando você publicar.

1. Clique em **salvar** e, em seguida, republicar o aplicativo.

## <a name="optional-deploy-by-publishing-to-a-local-folder"></a>(Opcional) Implantar pela publicação em uma pasta local

Você pode usar essa opção para implantar seu aplicativo se você deseja copiar o aplicativo para o IIS usando o Powershell, RoboCopy, ou você deseja copiar os arquivos manualmente.

### <a name="BKMK_deploy_asp_net"></a> Configurar o site da Web ASP.NET no computador com Windows Server

1. Abra o Windows Explorer e crie uma nova pasta, **C:\Publish**, onde você irá implantar posteriormente o projeto do ASP.NET.

2. Se não ainda estiver aberto, abra o **serviços de informações da Internet (IIS) Manager**. (No painel esquerdo do Gerenciador do servidor, selecione **IIS**. Clique com o botão direito do mouse e selecione **Gerenciador do IIS (Serviços de Informações da Internet)**).

3. Sob **conexões** no painel esquerdo, vá até **Sites**.

4. Selecione o **Site padrão**, escolha **configurações básicas**e defina o **caminho físico** para **C:\Publish**.

5. Clique com botão direito do **Site padrão** nó e selecione **Adicionar aplicativo**.

6. Defina a **Alias** campo **MyASPApp**, aceite o padrão do Pool de aplicativos (**DefaultAppPool**) e defina o **caminho físico** para  **C:\Publish**.

7. Sob **conexões**, selecione **Pools de aplicativos**. Abra **DefaultAppPool** e defina o campo de pool de aplicativos como **ASP.NET v4.0** (ASP.NET 4.5 não é uma opção para o pool de aplicativos).

8. Com o site selecionado no Gerenciador do IIS, escolha **editar permissões**e certifique-se de que IUSR, IIS_IUSRS ou o usuário configurado para o Pool de aplicativos é um usuário autorizado com direitos de leitura e execução. Se nenhum desses usuários estiver presente, adicione IUSR como um usuário com direitos de leitura e execução.

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>Publicar e implantar o aplicativo pela publicação em uma pasta local do Visual Studio

Você também pode publicar e implantar o aplicativo usando o sistema de arquivos ou outras ferramentas.

1. (ASP.NET 4.5.2) Certifique-se de que o arquivo Web. config lista a versão correta do .NET Framework.  Por exemplo, se você estiver direcionando a ASP.NET 4.5.2, verifique se que essa versão é listada no Web. config.
  
    ```xml
    <system.web>
      <compilation debug="true" targetFramework="4.5.2" />
      <httpRuntime targetFramework="4.5.2" />
      <httpModules>
        <add name="ApplicationInsightsWebTracking" type="Microsoft.ApplicationInsights.Web.ApplicationInsightsHttpModule, Microsoft.AI.Web" />
      </httpModules>
    </system.web>
  
    ```

    Por exemplo, a versão deve ser 4.0, se você instalar o ASP.NET 4, em vez de 4.5.2.

[!INCLUDE [remote-debugger-deploy-app-local](../debugger/includes/remote-debugger-deploy-app-local.md)]

## <a name="BKMK_msvsmon"></a> Baixe e instale as ferramentas remotas no Windows Server

Neste tutorial, estamos usando o Visual Studio 2017.

[!INCLUDE [remote-debugger-download](../debugger/includes/remote-debugger-download.md)]
  
## <a name="BKMK_setup"></a> Configurar o depurador remoto no Windows Server

[!INCLUDE [remote-debugger-configuration](../debugger/includes/remote-debugger-configuration.md)]

> [!NOTE]
> Se você precisar adicionar permissões para usuários adicionais, alterar o modo de autenticação ou número da porta para o depurador remoto, consulte [configurar o depurador remoto](../debugger/remote-debugging.md#configure_msvsmon).

Para obter informações sobre como executar o depurador remoto como um serviço, consulte [executar o depurador remoto como um serviço](../debugger/remote-debugging.md#bkmk_configureService).

## <a name="BKMK_attach"></a> Anexar ao aplicativo ASP.NET de computador do Visual Studio

1. No computador do Visual Studio, abra a solução que você está tentando depurar (**MyASPApp** se você estiver seguindo as etapas neste artigo).
2. No Visual Studio, clique em **Depurar > Anexar ao processo** (Ctrl + Alt + P).

    > [!TIP]
    > No Visual Studio 2017, você pode anexar novamente o mesmo processo que você anexado anteriormente usando **Depurar > anexar novamente ao processo...** Shift+Alt+P 

3. Definir o qualificador de campo para  **\<nome do computador remoto >: 4022**.
4. Cliquem em **Atualizar**.
    Você deve ver alguns processos que aparecem na **processos disponíveis** janela.

    Se você não vir todos os processos, tente usar o endereço IP em vez do nome do computador remoto (a porta é necessária). Você pode usar `ipconfig` em uma linha de comando para obter o endereço IPv4.

5. Verifique **Mostrar processos de todos os usuários**.
6. Digite a primeira letra do nome de um processo para localizar rapidamente **w3wp.exe** para ASP.NET 4.5.

    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg_attachtoprocess.png "RemoteDBG_AttachToProcess")

7. Clique em **Anexar**

8. Abra o site do computador remoto. Em um navegador, vá para **http://\<nome do computador remoto >**.
    
    Você deve ver a página da web ASP.NET.
9. No aplicativo ASP.NET em execução, clique no link para o **sobre** página.

    O ponto de interrupção deve ser atingido no Visual Studio.

## <a name="bkmk_openports">Solução de problemas</a> Abra as portas necessárias no Windows Server

Na maioria das configurações, as portas necessárias estão abertas pela instalação do ASP.NET e o depurador remoto. No entanto, talvez você precise verificar se as portas estão abertas.

> [!NOTE]
> Em uma VM do Azure, você deve abrir as portas por meio de [grupo de segurança de rede](/azure/virtual-machines/virtual-machines-windows-hero-role#open-port-80-for-web-traffic). 

Portas obrigatórias:

- 80 - obrigatórias para IIS
- 8172 - (opcional) necessária para a implantação da Web para implantar o aplicativo do Visual Studio
- 4022 - necessários para a depuração remota do Visual Studio 2017 (consulte [as atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md) para obter informações detalhadas.
- UDP 3702 - porta (opcional) descoberta permite que você os **localizar** botão ao anexar ao depurador remoto no Visual Studio.

1. Para abrir uma porta no Windows Server, abra o **inicie** menu, procure **Firewall do Windows com segurança avançada**.

2. Em seguida, escolha **regras de entrada > nova regra > porta**. Escolher **próxima** e, em **portas locais específicas**, insira o número da porta, clique em **próxima**, em seguida, **permitir a Conexão**, clique em Avançar, e Adicione o nome (**IIS**, **implantação da Web**, ou **msvsmon**) para a regra de entrada.

    Se você quiser obter mais detalhes sobre como configurar o Firewall do Windows, consulte [configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md).

3. Crie regras adicionais para as outras portas necessárias.