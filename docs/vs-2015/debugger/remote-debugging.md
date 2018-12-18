---
title: Depuração remota | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- vs.debug.remote.overview
dev_langs:
- C++
- CSharp
- FSharp
- JScript
- VB
helpviewer_keywords:
- remote debugging, setup
ms.assetid: 5a94ad64-100d-43ca-9779-16cb5af86f97
caps.latest.revision: 81
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 0ac1bbe2cc1832d0b34706f88b4df583d117149c
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51799269"
---
# <a name="remote-debugging"></a>Depuração remota
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode depurar um aplicativo do Visual Studio que tenha sido implantado em um computador diferente.  Para fazer isso, você deve usar o depurador remoto do Visual Studio.  
  
 As informações aqui se aplica a aplicativos da área de trabalho do Windows e aplicativos ASP.NET.  Para obter informações sobre os aplicativos Windows Store depuração remotos e os aplicativos do Azure, consulte [depuração remota em aplicativos da Windows Store e Azure](#bkmk_winstoreAzure).  
  
## <a name="get-the-remote-tools"></a>Obtenha as ferramentas remotas  
Você pode baixar as ferramentas remotas diretamente no dispositivo ou no servidor que você deseja depurar, ou você podem obter as ferramentas remotas do seu computador host com o Visual Studio instalado.

### <a name="to-download-and-install-the-remote-tools"></a>Para baixar e instalar as ferramentas remotas
  
1.  No dispositivo ou servidor máquina que você deseja depurar (em vez do computador que executa o Visual Studio), obtenha a versão correta das ferramentas remotas.

    |Versão|Link|Observações|
    |-|-|-|
    |Visual Studio 2015 Atualização 3|[Ferramentas remotas](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Se solicitado, ingressar no grupo do Visual Studio Dev Essentials gratuito, ou você pode apenas entrar com uma assinatura válida do Visual Studio. Em seguida, reabra o link se necessário. Sempre Baixe a versão correspondente do seu sistema operacional do dispositivo (x x86, x64 ou versão ARM)|
    |Visual Studio 2015 (antiga)|[Ferramentas remotas](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Se solicitado, ingressar no grupo do Visual Studio Dev Essentials gratuito, ou você pode apenas entrar com uma assinatura válida do Visual Studio. Em seguida, reabra o link se necessário.|
    |Visual Studio 2013|[Ferramentas remotas](https://msdn.microsoft.com/library/bt727f1t(v=vs.120).aspx#BKMK_Installing_the_Remote_Tools)|Baixar a página na documentação do Visual Studio 2013|
    |Visual Studio 2012|[Ferramentas remotas](https://msdn.microsoft.com/library/bt727f1t(v=vs.110).aspx#BKMK_Installing_the_Remote_Tools)|Baixar a página na documentação do Visual Studio 2012|
  
2.  Na página de download, escolha a versão das ferramentas que corresponde ao seu sistema operacional (x x86, x64 ou versão ARM) e baixar as ferramentas remotas.
  
    > [!IMPORTANT]
    >  Recomendamos que você instale a versão mais recente das ferramentas remotas que corresponde à sua versão do Visual Studio. Versões incompatíveis não são recomendadas.  
    >   
    >  Além disso, você deve instalar as ferramentas remotas que têm a mesma arquitetura de sistema operacional no qual você deseja instalá-lo. Em outras palavras, se você quiser depurar um aplicativo de 32 bits em um computador remoto executando um sistema operacional de 64 bits, você deve instalar a versão de 64 bits das ferramentas remotas no computador remoto.  
  
3.  Quando você terminar de baixar o arquivo executável, siga as instruções para instalar o aplicativo no computador remoto. Consulte [instruções de instalação](#bkmk_setup)

Se você tentar copiar o depurador remoto (msvsmon.exe) para o computador remoto e executá-lo, esteja ciente de que o **Assistente de configuração do depurador remoto** (**rdbgwiz.exe**) é instalado apenas quando você baixar o ferramentas e você talvez precise usar o Assistente para configuração mais tarde, especialmente se você deseja que o depurador remoto para ser executado como um serviço. Para obter mais informações, consulte [(opcional) configurar o depurador remoto como um serviço](#bkmk_configureService) abaixo.

### <a name="to-run-the-remote-debugger-from-a-file-share"></a>Para executar o depurador remoto de um compartilhamento de arquivos

Você pode encontrar o depurador remoto (**msvsmon.exe**) em um computador com Visual Studio 2015 Community, Professional ou Enterprise já está instalado. Para muitos cenários, a maneira mais fácil de configurar a depuração remota é executar o depurador remoto (msvsmon.exe) de um compartilhamento de arquivos. Para limitações de uso, consulte a página de Ajuda do depurador remoto (**ajuda / uso** no depurador remoto).

1. Encontre **msvsmon.exe** no diretório correspondente à versão do Visual Studio. Para Visual Studio 2015:

      **Programa de Programas\Microsoft Visual Studio 14.0\Common7\IDE\Remote Debugger\x86\msvsmon.exe**
      
      **Programa de Programas\Microsoft Visual Studio 14.0\Common7\IDE\Remote Debugger\x64\msvsmon.exe**

2. Compartilhamento de **depurador remoto** pasta no computador do Visual Studio.

3. No computador remoto, execute **msvsmon.exe**. Siga as [instruções de instalação](#bkmk_setup).

> [!TIP] 
> Para instalação de linha de comando e referência de linha de comando, consulte a página de Ajuda **msvsmon.exe** digitando ``msvsmon.exe /?`` na linha de comando no computador com o Visual Studio instalado (ou acesse **ajuda / uso**no depurador remoto).

  
## <a name="supported-operating-systems"></a>Supported Operating Systems  
 O computador remoto deve estar executando um dos seguintes sistemas operacionais:  
  
-   Windows 10  
  
-   Windows 8 ou 8.1  
  
-   Windows 7 Service Pack 1  
  
-   Windows Server 2012 ou Windows Server 2012 R2  
  
-   Windows Server 2008 Service Pack 2, Windows Server 2008 R2 Service Pack 1  
  
## <a name="supported-hardware-configurations"></a>Configurações de Hardware com suporte  
  
-   Processador de 1,6 GHz ou mais rápido  
  
-   1 GB de RAM (1,5 GB se executado em uma máquina virtual)  
  
-   1 GB de espaço em disco disponível  
  
-   Disco rígido de 5400 RPM  
  
-   Placa de vídeo compatível com DirectX 9 com execução na resolução de tela 1024 x 768 ou superior  
  
## <a name="network-configuration"></a>Configuração de rede  
 O computador remoto e o computador do Visual Studio devem ser conectados por uma rede, um grupo de trabalho ou um grupo doméstico, senão conectados diretamente por meio de um cabo Ethernet. Não há suporte à depuração pela Internet.  
  
## <a name="bkmk_setup"></a>Configurar o depurador remoto  
 Você deve ter permissões administrativas no computador remoto  
  
1. Localize o aplicativo depurador remoto. (Abra o menu Iniciar e pesquise **depurador remoto**.)
  
    Se você estiver executando o depurador remoto em um servidor remoto, você pode o aplicativo depurador remoto com o botão direito e escolha **executar como administrador** (ou, você pode executar o depurador remoto como um serviço). Se você não estiver executando-lo em um servidor remoto, apenas iniciá-lo normalmente.
  
2. Ao iniciar as ferramentas remotas pela primeira vez (ou antes que você tenha configurado para isso), o **configuração de depuração remota** dalog caixa é exibida.  
  
    ![RemoteDebuggerConfWizardPage](../debugger/media/remotedebuggerconfwizardpage.png "RemoteDebuggerConfWizardPage")  
  
3. Se a API de serviço do Windows não está instalada (o que ocorre apenas no Windows Server 2008 R2), escolha o **instalar** botão.  
  
4. Selecione os tipos de rede que você deseja usar as ferramentas remotas no. Pelo menos um tipo de rede deve ser selecionado. Se os computadores estiverem conectados por meio de um domínio, você deve escolher o primeiro item. Se os computadores estiverem conectados por meio de um grupo de trabalho ou um grupo doméstico, você precisa escolher o item de segundo ou terceiro conforme apropriado.  
  
5. Escolher **configurar a depuração remota** para configurar o firewall e iniciar a ferramenta.  
  
6. Quando a configuração estiver concluída, a janela do depurador remoto é exibida.
  
    ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")
  
    O depurador remoto agora está aguardando uma conexão. Anote o nome do servidor e o número da porta que é exibido, pois você precisará dele mais tarde para a configuração no Visual Studio.  
  
   Quando você terminar a depuração e a necessidade de parar o depurador remoto, clique em **arquivo / sair** na janela. Você pode reiniciá-lo partir o **iniciar** menu ou da linha de comando:  
  
   **\<Diretório de instalação do Visual Studio > \Common7\IDE\Remote depurador\\< x86, x64 ou Appx\msvsmon.exe**.  
  
## <a name="configure-the-remote-debugger"></a>Configurar o depurador remoto  
 Você pode alterar alguns aspectos da configuração do depurador remoto depois que tiver iniciado pela primeira vez.
  
- Para permitir que outros usuários para se conectar ao depurador remoto, escolha **ferramentas / permissões**. Você deve ter privilégios de administrador para conceder ou negar permissões.

  > [!IMPORTANT]
  > Você pode executar o depurador remoto em uma conta de usuário é diferente da conta de usuário que você está usando no computador do Visual Studio, mas você deve adicionar a conta de usuário diferente para permissões de usuário do depurador remoto. 

   Como alternativa, você pode iniciar o depurador remoto na linha de comando com o **/Allow \<nome de usuário >** parâmetro: **msvsmon / permitir \< username@computer>**.
  
- Para alterar o modo de autenticação ou o número da porta ou especificar um valor de tempo limite para as ferramentas remotas: escolha **Ferramentas / opções**.  
  
   Para obter uma lista dos números de porta usados por padrão, consulte [as atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md).  
  
   > [!WARNING]
  >  Você também pode optar por executar as ferramentas remotas no Modo Sem Autenticação, mas isso é altamente desaconselhável. Nesse modo não há nenhuma segurança de rede. Escolha o modo sem autenticação somente se você tiver certeza de que a rede não está em risco de tráfego mal-intencionado ou hostil.

##  <a name="bkmk_configureService"></a> (Opcional) Configurar o depurador remoto como um serviço
 Para depuração no ASP.NET e outros ambientes de servidor, você deve executar o depurador remoto como um administrador ou, se você quiser que ele sempre em execução, executar o depurador remoto como um serviço.
  
 Se você quiser configurar o depurador remoto como um serviço, siga estas etapas.  
  
1. Localizar o **Assistente de configuração do depurador remoto** (rdbgwiz.exe). (Isso é um aplicativo separado do depurador remoto.) Ele está disponível apenas quando você instala as ferramentas remotas. Ele não é instalado com o Visual Studio.  
  
2. Começar a executar o Assistente de configuração. Quando a primeira página é exibida, clique em **próxima**.  
  
3. Verifique as **executar o depurador remoto do Visual Studio 2015, como um serviço** caixa de seleção.  
  
4. Adicione o nome da conta de usuário e senha.  
  
    Talvez você precise adicionar o **fazer logon como um serviço** direito de usuário desta conta. (Encontre **política de segurança Local** (secpol. msc) na **iniciar** página ou janela (ou tipo **secpol** em um prompt de comando). Quando a janela é exibida, clique duas vezes **atribuição de direitos de usuário**, em seguida, localize **fazer logon como um serviço** no painel direito. Clique duas vezes nesse item. Adicione a conta de usuário para o **propriedades** janela e clique em **Okey**.) Clique em **Avançar**.  
  
5. Selecione o tipo de rede que você deseja que as ferramentas remotas para se comunicar com. Pelo menos um tipo de rede deve ser selecionado. Se os computadores estiverem conectados por meio de um domínio, você deve escolher o primeiro item. Se os computadores estiverem conectados por meio de um grupo de trabalho ou um grupo doméstico, você deve escolher os itens de segundo ou terceiro. Clique em **Avançar**.  
  
6. Se o serviço pode ser iniciado, você verá **concluiu com êxito o Assistente de configuração de depurador Visual remoto Studio**. Se o serviço não pode ser iniciado, você verá **Falha ao concluir o Assistente de configuração de depurador Visual remoto Studio**. A página também fornece algumas dicas a seguir para restaurar o serviço para iniciar.  
  
7. Clique em **Finalizar**.  
  
   Neste ponto, o depurador remoto está em execução como um serviço. Você pode verificar isso acessando **painel de controle / serviços** e procurando **depurador remoto do Visual Studio 2015**.  
  
   Você pode parar e iniciar o serviço de depurador remoto do **painel de controle / serviços**.  

## <a name="remote-debug-an-aspnet-application"></a>Depuração remota de um aplicativo ASP.NET  
 Implantar um aplicativo ASP.NET em um computador remoto executando o IIS tem etapas diferentes, dependendo do sistema operacional e versão do IIS. Para computadores remotos que executam o Windows Server 2008 ou Windows Server 2012 que tem o IIS 7.5 ou posterior instalado, consulte [ASP.NET de depuração remota em um computador remoto do IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md).
 
 Se você estiver depurando um aplicativo ASP.NET Core, consulte [publicar no IIS](https://docs.asp.net/en/latest/publishing/iis.html). São necessárias etapas diferentes para publicar um ASP.NET Core no IIS. Depois de publicar um aplicativo ASP.NET Core com êxito, você pode acessar remotamente depurá-lo [assim como outros aplicativos ASP.NET](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md), exceto que o processo que você precisa anexar ao é dnx.exe em vez de w3wp.exe.

## <a name="remote-debug-a-visual-c-project"></a>Depuração remota de um projeto do Visual C++  
 No procedimento a seguir, o nome e caminho do projeto é C:\remotetemp\MyMfc e é o nome do computador remoto **MJO DL**.  
  
1. Criar um aplicativo MFC chamado **mymfc.**  
  
2. Defina um ponto de interrupção em algum lugar no aplicativo que é atingido com facilidade, por exemplo, no **MainFrm.cpp**, no início de `CMainFrame::OnCreate`.  
  
3. No Gerenciador de soluções, clique com botão direito no projeto e selecione **propriedades**. Abra o **depuração** guia.  
  
4. Defina as **depurador a iniciar** à **depurador remoto do Windows**.  
  
    ![RemoteDebuggingCPlus](../debugger/media/remotedebuggingcplus.png "RemoteDebuggingCPlus")  
  
5. Faça as seguintes alterações nas propriedades:  
  
   |Configuração|Valor|
   |-|-|  
   |Comando remoto|C:\remotetemp\mymfc.exe|  
   |Diretório de trabalho|C:\remotetemp|  
   |Nome do servidor remoto|MJO-DL:*portnumber*|  
   |Conexão|Remoto sem Autenticação do Windows|  
   |Tipo de Depurador|Somente Nativo|  
   |Diretório de implantação|C:\remotetemp.|  
   |Arquivos adicionais a implantar|C:\data\mymfcdata.txt.|  
  
    Se você implantar arquivos adicionais (opcionais), a pasta deve existir nos dois computadores.  
  
6. No Gerenciador de soluções, clique com botão direito a solução e escolha **Configuration Manager**.  
  
7. Para o **Debug** configuração, selecione o **implantar** caixa de seleção.  
  
    ![RemoteDebugCplusDeploy](../debugger/media/remotedebugcplusdeploy.png "RemoteDebugCplusDeploy")  
  
8. Iniciar a depuração (**depurar / iniciar depuração**, ou **F5**).  
  
9. O executável é implantado automaticamente para o computador remoto.  
  
10. Se solicitado, insira as credenciais de rede para se conectar ao computador remoto.  
  
     As credenciais necessárias são específicas para a configuração de segurança da sua rede. Por exemplo, em um computador de domínio, você pode escolher um certificado de segurança ou insira seu nome de domínio e senha. Em um computador fora do domínio, você pode inserir o nome do computador e um nome de conta de usuário válido, como <strong>MJO-DL\name@something.com</strong>, junto com a senha correta.  
  
11. No computador do Visual Studio, você deve ver que a execução é interrompida no ponto de interrupção.  
  
    > [!TIP]
    >  Como alternativa, você pode implantar os arquivos como uma etapa separada. No **Gerenciador de soluções,** com o botão direito do **mymfc** nó e, em seguida, escolha **implantar**.  
  
    Se você tiver arquivos sem código que precisam ser usados pelo aplicativo, você precisará incluí-los no projeto do Visual Studio. Crie uma pasta de projeto para os arquivos adicionais (na **Gerenciador de soluções**, clique em **adicionar / nova pasta**.) Em seguida, adicione os arquivos na pasta (na **Gerenciador de soluções**, clique em **adicionar / existente Item**, em seguida, selecione os arquivos.). Sobre o **propriedades** para cada arquivo, defina **Copy to Output Directory** para **copiar sempre**.  
  
## <a name="remote-debug-a-visual-c-or-visual-basic-project"></a>Depuração remota de um projeto Visual c# ou Visual Basic  
 O depurador não é possível implantar aplicativos de desktop em Visual C# ou Visual Basic para um computador remoto, mas você ainda pode depurá-los remotamente da seguinte maneira. O procedimento a seguir pressupõe que você deseja para depurá-lo em um computador denominado **MJO DL**, conforme mostrado na ilustração anterior.
  
1. Crie um projeto WPF chamado **MyWpf**.  
  
2. Defina um ponto de interrupção em algum lugar no código que é alcançado com facilidade.  
  
    Por exemplo, você pode definir um ponto de interrupção em um manipulador de botão. Para fazer isso, abra o MainWindow. XAML e adicionar um controle de botão da caixa de ferramentas, clique duas vezes no botão para abrir o manipulador de TI.
  
3. No Gerenciador de soluções, clique com botão direito no projeto e escolha **propriedades**.  
  
4. Sobre o **propriedades** , escolha o **depurar** guia.  
  
    ![RemoteDebuggerCSharp](../debugger/media/remotedebuggercsharp.png "RemoteDebuggerCSharp")  
  
5. Verifique se o **diretório de trabalho** caixa de texto está vazia.  
  
6. Escolher **usar computador remoto**e digite **MJO-DL:4020** na caixa de texto. (4020 é o número da porta mostrado na janela do depurador remoto).  
  
7. Certifique-se de que **habilitar a depuração de código nativo** não estiver selecionada.  
  
8. Compile o projeto.  
  
9. Crie uma pasta no computador remoto que é o mesmo caminho que o **Debug** pasta em seu computador do Visual Studio:  **\<caminho de origem > \MyWPF\MyWPF\bin\Debug**.  
  
10. Copie o arquivo executável que você acabou de criar do seu computador do Visual Studio para a pasta recém-criada no computador remoto.
  
    > [!CAUTION]
    >  Não faça alterações no código ou recriação (ou você deve repetir esta etapa). O executável que você copiou para o computador remoto deve corresponder exatamente, seu local de origem e símbolos.

    Você pode copiar o projeto manualmente, use Xcopy, Robocopy, Powershell ou outras opções.
  
11. Verifique se que o depurador remoto está em execução no computador de destino. (Se não for, pesquise **depurador remoto** na **iniciar** menu. ) A janela do depurador remoto se parece com isso.  
  
     ![RemoteDebuggerWindow](../debugger/media/remotedebuggerwindow.png "RemoteDebuggerWindow")  
  
12. No Visual Studio, inicie a depuração (**depurar / iniciar depuração**, ou **F5**).  
  
13. Se solicitado, insira as credenciais de rede para se conectar ao computador remoto.  
  
     As credenciais necessárias variam dependendo da configuração de segurança da sua rede. Por exemplo, em um computador de domínio, você pode inserir seu nome de domínio e senha. Em um computador fora do domínio, você pode inserir o nome do computador e um nome de conta de usuário válido, como <strong>MJO-DL\name@something.com</strong>, junto com a senha correta.

     Você deve ver que a janela principal do aplicativo do WPF está aberta no computador remoto.
  
14. Se necessário, execute a ação para o ponto de interrupção. Você deve ver que o ponto de interrupção está ativo. Caso contrário, os símbolos para o aplicativo ainda não carregado. Tente novamente e se isso não funcionar, obter informações sobre o carregamento de símbolos e como solucioná-los no [configurações de símbolo de Noções básicas sobre arquivos de símbolo e o Visual Studio](http://blogs.msdn.com/b/visualstudioalm/archive/2015/01/05/understanding-symbol-files-and-visual-studio-s-symbol-settings.aspx).
  
15. No computador do Visual Studio, você deve ver que a execução foi interrompido no ponto de interrupção.
  
    Se você tiver arquivos sem código que precisam ser usados pelo aplicativo, você precisará incluí-los no projeto do Visual Studio. Crie uma pasta de projeto para os arquivos adicionais (na **Gerenciador de soluções**, clique em **adicionar / nova pasta**.) Em seguida, adicione os arquivos na pasta (na **Gerenciador de soluções**, clique em **adicionar / existente Item**, em seguida, selecione os arquivos.). Sobre o **propriedades** para cada arquivo, defina **Copy to Output Directory** para **copiar sempre**.
  
## <a name="set-up-debugging-with-remote-symbols"></a>Configurar a depuração com símbolos remotos  
 Você deve ser capaz de depurar seu código com os símbolos que você gerar no computador do Visual Studio. O desempenho do depurador remoto é muito melhor quando você usa símbolos locais.  Se você precisar usar símbolos remotos, você precisa informar o monitor de depuração remota para procurar por símbolos no computador remoto.  
  
 A partir do Visual Studio 2013 atualização 2, você pode usar a seguinte opção de linha de comando do msvsmon para usar símbolos remotos para código gerenciado: `Msvsmon / /FallbackLoadRemoteManagedPdbs`  
  
 Para obter mais informações, consulte a Ajuda de depuração remota (pressione **F1** na janela do depurador remoto, ou clique em **ajuda / uso**). Você pode encontrar mais informações em [.NET Remote Symbol alterações de carregamento no Visual Studio 2012 e 2013](http://blogs.msdn.com/b/visualstudioalm/archive/2013/10/16/net-remote-symbol-loading-changes-in-visual-studio-2012-and-2013.aspx)  
  
##  <a name="bkmk_winstoreAzure"></a> Depuração remota em aplicativos da Windows Store e Azure  
 Para obter informações sobre a depuração remota com os aplicativos da Windows Store, consulte [depurar e testar aplicativos da Windows Store em um dispositivo remoto do Visual Studio](http://msdn.microsoft.com/library/windows/apps/hh441469.aspx).  
  
 Para obter informações sobre a depuração no Azure, consulte um destes tópicos:  
  
-   [Depurando um serviço de nuvem ou máquina Virtual no Visual Studio](http://msdn.microsoft.com/library/azure/ff683670.aspx)  
  
-   [Depuração de back-end do .NET no Visual Studio](http://blogs.msdn.com/b/azuremobile/archive/2014/03/14/debugging-net-backend-in-visual-studio.aspx)  
  
-   Introdução à depuração remota em Sites do Azure ([parte 1](http://azure.microsoft.com/blog/2014/05/06/introduction-to-remote-debugging-on-azure-web-sites/), [parte 2](http://azure.microsoft.com/blog/2014/05/07/introduction-to-remote-debugging-azure-web-sites-part-2-inside-remote-debugging/), [parte 3](http://azure.microsoft.com/blog/2014/05/08/introduction-to-remote-debugging-on-azure-web-sites-part-3-multi-instance-environment-and-git/)).  
  
## <a name="see-also"></a>Consulte também  
 [Depurando no Visual Studio](../debugger/debugging-in-visual-studio.md)   
 [Configurar o Firewall do Windows para depuração remota](../debugger/configure-the-windows-firewall-for-remote-debugging.md)   
 [Atribuições de porta do depurador remoto](../debugger/remote-debugger-port-assignments.md)   
 [Depuração Remota de ASP.NET em um computador remoto IIS](../debugger/remote-debugging-aspnet-on-a-remote-iis-7-5-computer.md)  
 [Erros e solução de problemas de depuração remota](../debugger/remote-debugging-errors-and-troubleshooting.md)



