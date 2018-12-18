---
title: ASP.NET Core em um computador remoto IIS de depuração remota | Microsoft Docs
ms.custom: remotedebugging
ms.date: 05/21/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 573a3fc5-6901-41f1-bc87-557aa45d8858
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- aspnet
- dotnetcore
ms.openlocfilehash: bcb0db3a6eab91c517ce731ddf6e201d5a73f1f8
ms.sourcegitcommit: 40b6438b5acd7e59337a382c39ec711b9e99cc8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2018
ms.locfileid: "49101063"
---
# <a name="remote-debug-aspnet-core-on-a-remote-iis-computer-in-visual-studio-2017"></a>Depuração remota do ASP.NET Core em um computador remoto IIS no Visual Studio 2017
Para depurar um aplicativo ASP.NET que tenha sido implantado no IIS, instalar e executar as ferramentas remotas no computador onde você implantou seu aplicativo e, em seguida, anexar a seu aplicativo em execução do Visual Studio.

![Componentes do depurador remoto](../debugger/media/remote-debugger-aspnet.png "Remote_debugger_components")

Este guia explica como configurar e configurar um núcleo de ASP.NET do Visual Studio 2017, implantá-lo no IIS e anexar o depurador remoto do Visual Studio. A depuração remota ASP.NET 4.5.2, consulte [depuração remota ASP.NET em um computador com IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md). Você também pode implantar e depurar no IIS usando o Azure. Para o serviço de aplicativo do Azure, você pode facilmente implantar e depurar em uma instância pré-configurada do IIS e o depurador remoto usando o [depurador de instantâneo](../debugger/debug-live-azure-applications.md) ou pelo [anexando o depurador do Gerenciador de servidores](../debugger/remote-debugging-azure.md).

Esses procedimentos foram testados nessas configurações de servidor:
* Windows Server 2012 R2 e IIS 8
* Windows Server 2016 e o IIS 10

## <a name="requirements"></a>Requisitos

Não há suporte para depuração entre dois computadores conectados por meio de um proxy. Depuração em uma alta latência ou a conexão de baixa largura de banda, como dial-up da Internet, ou pela Internet entre países não é recomendado e pode falhar ou ser muito lento. Para obter uma lista completa dos requisitos, consulte [requisitos de](../debugger/remote-debugging.md#requirements_msvsmon).

## <a name="app-already-running-in-iis"></a>Aplicativo já em execução no IIS?

Este artigo inclui etapas sobre como configurar uma configuração básica do IIS no Windows server e implantar o aplicativo do Visual Studio. Essas etapas são incluídas para certificar-se de que o servidor tem necessário componentes instalados, que o aplicativo pode ser executado corretamente e que você está pronto para depuração remota.

* Se o aplicativo é executado no IIS e quiser apenas baixar o depurador remoto e iniciar a depuração, vá para [Baixe e instale as ferramentas remotas no Windows Server](#BKMK_msvsmon).

* Se você deseja obter ajuda para certificar-se de que seu aplicativo é configurado, implantado e executando corretamente no IIS para que você possa depurar, siga as etapas neste tópico.

## <a name="create-the-aspnet-core-application-on-the-visual-studio-2017-computer"></a>Criar o aplicativo ASP.NET Core no computador do Visual Studio 2017 

1. Crie um novo aplicativo ASP.NET Core. (**Arquivo > Novo > projeto**, em seguida, selecione **Visual c# > Web > aplicativo Web ASP.NET Core**).

    No **ASP.NET Core** seção de modelos, selecione **aplicativo Web**.

2. Certifique-se de que **ASP.NET Core 2.0** está selecionado, que **Habilitar suporte ao Docker** é **não** selecionado e que **autenticação** é definido como **Nenhuma autenticação**.

3. Nomeie o projeto **MyASPApp** e clique em **Okey** para criar a nova solução.

4. Abra o arquivo About.cshtml.cs e defina um ponto de interrupção na `OnGet` método (em modelos mais antigos, abra HomeController.cs em vez disso e defina o ponto de interrupção `About()` método).

## <a name="bkmk_configureIIS"></a> Instalar e configurar o IIS no Windows Server

[!INCLUDE [remote-debugger-install-iis-role](../debugger/includes/remote-debugger-install-iis-role.md)]

## <a name="update-browser-security-settings-on-windows-server"></a>Atualizar configurações de segurança do navegador no Windows Server

Se a configuração de segurança aprimorada estiver habilitada no Internet Explorer (ela é habilitada por padrão), em seguida, você precisa adicionar alguns domínios como sites confiáveis para que você possa baixar alguns dos componentes do servidor web. Adicione os sites confiáveis acessando **opções da Internet > Segurança > Sites confiáveis > Sites**. Adicione os domínios a seguir.

- microsoft.com
- go.microsoft.com
- download.microsoft.com
- IIS.NET

Quando você baixar o software, você pode receber solicitações para conceder permissão para carregar vários scripts do site da web e recursos. Alguns desses recursos não são necessárias, mas para simplificar o processo, clique em **adicionar** quando solicitado.

## <a name="install-aspnet-core-on-windows-server"></a>Instalar o ASP.NET Core no Windows Server

1. Instalar o [hospedagem do .NET Core Windows Server](https://aka.ms/dotnetcore-2-windowshosting) pacote no sistema de hospedagem. O pacote instala o Runtime do .NET Core, biblioteca do .NET Core e o módulo do ASP.NET Core. Para obter mais instruções detalhadas, consulte [publicar no IIS](/aspnet/core/publishing/iis?tabs=aspnetcore2x#iis-configuration).

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

1. Abra o Windows Explorer e crie uma nova pasta, **C:\Publish**, onde você irá implantar posteriormente o projeto do ASP.NET.

2. Se não ainda estiver aberto, abra o **serviços de informações da Internet (IIS) Manager**. (No painel esquerdo do Gerenciador do servidor, selecione **IIS**. O servidor com o botão direito e selecione **serviços de informações da Internet (IIS) Manager**.)

3. Sob **conexões** no painel esquerdo, vá até **Sites**.

4. Selecione o **Site padrão**, escolha **configurações básicas**e defina o **caminho físico** para **C:\Publish**.

4. Clique com botão direito do **Site padrão** nó e selecione **Adicionar aplicativo**.

5. Defina a **Alias** campo **MyASPApp**, aceite o padrão do Pool de aplicativos (**DefaultAppPool**) e defina o **caminho físico** para  **C:\Publish**.

6. Sob **conexões**, selecione **Pools de aplicativos**. Abra **DefaultAppPool** e defina o campo de pool de aplicativos como **sem código gerenciado**.

7. O novo site no Gerenciador do IIS com o botão direito, escolha **editar permissões**e certifique-se de que IUSR, IIS_IUSRS ou o usuário configurado para acesso ao aplicativo web é um usuário autorizado com direitos de leitura e execução.

    Se você não vir um desses usuários com acesso, percorra as etapas para adicionar IUSR como um usuário com direitos de leitura e execução.

### <a name="publish-and-deploy-the-app-by-publishing-to-a-local-folder-from-visual-studio"></a>Publicar e implantar o aplicativo pela publicação em uma pasta local do Visual Studio

Você também pode publicar e implantar o aplicativo usando o sistema de arquivos ou outras ferramentas.

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

1. No computador do Visual Studio, abra a solução que você está tentando depurar (**MyASPApp** se você estiver seguindo todas as etapas neste artigo).
2. No Visual Studio, clique em **Depurar > Anexar ao processo** (Ctrl + Alt + P).

    > [!TIP]
    > No Visual Studio 2017, você pode anexar novamente o mesmo processo que você anexado anteriormente usando **Depurar > anexar novamente ao processo...** (Shift + Alt + P). 

3. Definir o qualificador de campo para  **\<nome do computador remoto >: 4022**.
4. Clique em **Refresh**.
    Você deve ver alguns processos que aparecem na **processos disponíveis** janela.

    Se você não vir todos os processos, tente usar o endereço IP em vez do nome do computador remoto (a porta é necessária). Você pode usar `ipconfig` em uma linha de comando para obter o endereço IPv4.

    Se você quiser usar o **encontrar** botão, talvez você precise [abra a porta UDP 3702](#bkmk_openports) no servidor.

5. Verifique **Mostrar processos de todos os usuários**.
6. Digite a primeira letra do nome de um processo para localizar rapidamente **dotnet.exe** (para o ASP.NET Core).

    ![RemoteDBG_AttachToProcess](../debugger/media/remotedbg_attachtoprocess_aspnetcore.png "RemoteDBG_AttachToProcess")

7. Clique em **Anexar**.

8. Abra o site do computador remoto. Em um navegador, vá para **http://\<nome do computador remoto >**.
    
    Você deve ver a página da web ASP.NET.

9. No aplicativo ASP.NET em execução, clique no link para o **sobre** página.

    O ponto de interrupção deve ser atingido no Visual Studio.

## <a name="bkmk_openports"></a> Solução de problemas: Abrir as portas necessárias no Windows Server

Na maioria das configurações, as portas necessárias estão abertas pela instalação do ASP.NET e o depurador remoto. No entanto, talvez você precise verificar se as portas estão abertas.

> [!NOTE]
> Em uma VM do Azure, você deve abrir as portas por meio de [grupo de segurança de rede](/azure/virtual-machines/virtual-machines-windows-hero-role#open-port-80-for-web-traffic).

Portas necessárias:

- 80 - obrigatórias para IIS
- 4022 - necessários para a depuração remota do Visual Studio 2017 (consulte [as atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md) para obter informações detalhadas.
- 8172 - (opcional) necessária para a implantação da Web para implantar o aplicativo do Visual Studio.
- UDP 3702 - porta (opcional) descoberta permite que você os **localizar** botão ao anexar ao depurador remoto no Visual Studio.

1. Para abrir uma porta no Windows Server, abra o **inicie** menu, procure **Firewall do Windows com segurança avançada**.

2. Em seguida, escolha **regras de entrada > nova regra > porta**e, em seguida, clique em **próxima**. (Para UDP 3702, escolha **regras de saída** em vez disso.)

3. Sob **portas locais específicas**, insira o número da porta, clique em **próxima**.

4. Clique em **permitir a Conexão**, clique em **próxima**.

5. Selecione um ou mais tipos de rede para habilitar para a porta e clique em **próxima**.

    O tipo selecionado deve incluir a rede à qual o computador remoto está conectado.
6. Adicione o nome (por exemplo, **IIS**, **implantação da Web**, ou **msvsmon**) para a regra de entrada e clique em **concluir**.

    Você deve ver a nova regra na lista de regras de entrada ou regras de saída.

    Se você quiser obter mais detalhes sobre como configurar o Firewall do Windows, consulte [configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md).

3. Crie regras adicionais para as outras portas necessárias.
