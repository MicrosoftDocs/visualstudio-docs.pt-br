---
title: Instalar e configurar ferramentas para compilar usando iOS | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tgt-pltfrm-cross-plat
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- C++
ms.assetid: d0c311c9-9eb9-42c5-ba07-25604362cd28
caps.latest.revision: 13
author: corob-msft
ms.author: corob
manager: ghogen
ms.openlocfilehash: 6a5d5543ace2087db4ed5349e72fcaf53228d8ec
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787803"
---
# <a name="install-and-configure-tools-to-build-using-ios"></a>Instalar e configurar ferramentas para criação usando iOS
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

  
É possível usar o Visual C++ para Desenvolvimento Móvel de Multiplataforma para editar, depurar e implantar código do iOS no Simulador de IOS ou em um dispositivo iOS, mas devido a restrições de licenciamento, o código deve ser compilado e executado remotamente em um Mac. Para compilar e executar aplicativos iOS usando o Visual Studio, é necessário instalar e configurar o agente remoto, [vcremote](http://go.microsoft.com/fwlink/p/?LinkId=534988), no Mac. O agente remoto trata de solicitações de build do Visual Studio e executa o aplicativo em um dispositivo iOS conectado ao Mac, ou no Simulator de iOS no Mac.  
  
> [!NOTE]
>  Para obter informações sobre como usar serviços Mac hospedados na nuvem em vez de um Mac, consulte [Compilar e simular o iOS na nuvem](https://taco.visualstudio.com/en-us/docs/build_ios_cloud/). As instruções são para compilação usando as Ferramentas do Visual Studio para Apache Cordova. Para usar as instruções para compilar usando o Visual C++ para Desenvolvimento Móvel de Multiplataforma, substitua vcremote por vs-mda-remote.  
  
 Após ter instalado as ferramentas para compilar usando o iOS, consulte neste tópico as maneiras de configurar e atualizar rapidamente o agente remoto para desenvolvimento de iOS no Visual Studio e no Mac.  
  
 [Pré-requisitos](#Prerequisites)  
  
 [Instalar o agente remoto para iOS](#Install)  
  
 [Iniciar o agente remoto](#Start)  
  
 [Configurar o agente remoto no Visual Studio](#ConfigureVS)  
  
 [Gerar um novo PIN de segurança](#GeneratePIN)  
  
 [Gerar um novo certificado do servidor](#GenerateCert)  
  
 [Configurar o agente remoto no Mac](#ConfigureMac)  
  
##  <a name="Prerequisites"></a> Pré-requisitos  
 Para instalar e usar o agente remoto para desenvolver código para iOS, é necessário primeiro ter estes pré-requisitos:  
  
-   Um computador Mac executando OS X Mavericks ou posterior  
  
-   Uma [Apple ID](https://appleid.apple.com/)  
  
-   Uma conta do [Programa de Desenvolvedores de iOS](https://developer.apple.com/programs/ios/) ativa com a Apple  
  
-   [Xcode 6](https://developer.apple.com/xcode/downloads/)  
  
     O Xcode 6 pode ser baixados da App Store.  
  
-   Ferramentas de linha de comando do Xcode  
  
     Para instalar as ferramentas de linha de comando do Xcode, abra o aplicativo Terminal no Mac e digite o seguinte comando:  
  
     `xcode-select --install`  
  
-   Um identidade de assinatura do iOS configurada no Xcode  
  
     Para obter informações detalhadas de como obter uma identidade de assinatura do iOS, consulte [Maintaining Your Signing Identities and Certificates](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingCertificates/MaintainingCertificates.html) (Mantendo seus certificados e identidades de assinatura) na Biblioteca do Desenvolvedor de iOS. Para ver ou definir a identidade de assinatura no Xcode, abra o menu do **Xcode** e escolha **Preferences** (Preferências). Selecione **Accounts** (Contas) e escolha sua Apple ID e, em seguida, escolha o botão **View Details** (Exibir Detalhes).  
  
-   Se você estiver usando um dispositivo iOS para desenvolvimento, um perfil de provisionamento será configurado no Xcode para seu dispositivo  
  
     Para obter informações detalhadas sobre a criação de perfis de provisionamento, consulte [Creating Provisioning Profiles Using Member Center](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW24) (Criando perfis de provisionamento usando a central de membros) na Biblioteca do Desenvolvedor de iOS.  
  
-   [Node.js](http://nodejs.org/)  
  
-   Uma versão atualizada do npm  
  
     A versão do npm que vem com o Node.js pode não ser suficientemente recente para instalar o vcremote. Para atualizar o npm, abra o aplicativo Terminal no Mac e digite o seguinte comando:  
  
     `sudo npm install -g npm@latest`  
  
##  <a name="Install"></a> Instalar o agente remoto para iOS  
 Quando você instala o Visual C++ para Desenvolvimento Móvel de Multiplataforma, o Visual Studio pode se comunicar com [vcremote](http://go.microsoft.com/fwlink/p/?LinkId=534988), um agente remoto em execução no seu Mac, para transferir arquivos, compilar e executar seu aplicativo iOS e enviar comandos de depuração.  
  
 Antes de instalar o agente remoto, verifique se os [Pré-requisitos](#Prerequisites) foram satisfeitos e se você instalou o [Visual C++ para Desenvolvimento Móvel de Multiplataforma](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md#InstallTheTools).  
  
###  <a name="DownloadInstall"></a> Para baixar e instalar o agente remoto  
  
- No aplicativo Terminal no seu Mac, insira:  
  
   `sudo npm install -g --unsafe-perm vcremote`  
  
   O comutador da instalação global (**-g**) é recomendado, mas não é obrigatório.  
  
   Durante a instalação, vcremote é instalado e o modo de desenvolvedor é ativado em seu Mac. [Homebrew](http://brew.sh/) e dois pacotes npm, vcremote-lib e vcremote-utils, também são instalados.  
  
  > [!NOTE]
  >  Para instalar o Homebrew, você deve ter acesso sudo (administrador). Se precisar instalar o vcremote sem sudo, você poderá instalar o Homebrew manualmente em um local usr/local e adicionar sua pasta de compartimento ao seu caminho. Para obter mais informações, consulte a [Documentação do Homebrew](https://github.com/Homebrew/homebrew/wiki/Installation). Para habilitar manualmente o modo de desenvolvedor, digite este comando no aplicativo Terminal: `DevToolsSecurity –enable`  
  
  Se atualizar para uma nova versão do Visual Studio, você também deverá atualizar para a versão atual do agente remoto. Para atualizar o agente remoto, repita as etapas para baixar e instalá-lo.  
  
##  <a name="Start"></a> Iniciar o agente remoto  
 O agente remoto deve estar em execução para o Visual Studio compilar e executar seu código do iOS. O Visual Studio deve ser emparelhado ao agente remoto antes que possa se comunicar. Por padrão, o agente remoto é executado no modo de conexão segura, o que requer um PIN para emparelhar ao Visual Studio.  
  
###  <a name="RemoteAgentStartServer"></a> Para iniciar o agente remoto  
  
- No aplicativo Terminal no seu Mac, insira:  
  
   `vcremote`  
  
   Isso inicia o agente remoto com um diretório de build padrão de ~/ vcremote. Para ver opções de configuração adicionais, consulte [Configurar o agente remoto no Mac](#ConfigureMac).  
  
  Na primeira vez em que você iniciar o agente e sempre que criar um novo certificado de cliente, serão fornecidas as informações necessárias para configurar o agente no Visual Studio, incluindo o nome do host, a porta e o PIN.  
  
  ![Usar o vcremote para gerar um PIN seguro](../cross-platform/media/cppmdd-vcremote-generateclientcert.png "CPPMDD_vcremote_generateClientCert")  
  
  Se você pretende configurar o agente remoto no Visual Studio usando o nome do host, execute o ping para o Mac do Windows usando o nome de host para verificar se ele está acessível. Caso contrário, poderá ser necessário usar o endereço IP em vez disso.  
  
  O PIN gerado é de uso único e só é válido por um período limitado. Se você não emparelhar o Visual Studio ao agente remoto antes desse período expirar, será necessário gerar um novo PIN. Para obter mais informações, consulte [Gerar um novo PIN de segurança](#GeneratePIN).  
  
  É possível usar o agente remoto no modo desprotegido. No modo desprotegido, o agente remoto pode ser emparelhado ao Visual Studio sem um PIN.  
  
#### <a name="to-disable-secured-connection-mode"></a>Para desabilitar o modo de conexão segura  
  
-   Para desabilitar o modo de conexão segura no vcremote, digite este comando no aplicativo Terminal no seu Mac:  
  
     `vcremote --secure false`  
  
#### <a name="to-enable-secured-connection-mode"></a>Para habilitar o modo de conexão segura  
  
- Para habilitar o modo de conexão segura, digite este comando:  
  
   `vcremote --secure true`  
  
  Depois de iniciar o agente remoto, você pode usá-lo no Visual Studio até pará-lo.  
  
#### <a name="to-stop-the-remote-agent"></a>Para parar o agente remoto  
  
-   Na janela do Terminal em que o vcremote está em execução, digite `Control+C`.  
  
##  <a name="ConfigureVS"></a> Configurar o agente remoto no Visual Studio  
 Para se conectar ao agente remoto do Visual Studio, você deve especificar a configuração remota nas opções do Visual Studio.  
  
#### <a name="to-configure-the-remote-agent-from-visual-studio"></a>Para configurar o agente remoto do Visual Studio  
  
1. Se o agente não estiver sendo executado no Mac, siga as etapas em [Iniciar o agente remoto](#Start). O Mac deve estar executando o vcremote para Visual Studio para emparelhar com êxito, conectar e compilar seu projeto.  
  
2. No Mac, obtenha o nome do host ou o endereço IP do seu Mac.  
  
    É possível obter o endereço IP usando o comando **ifconfig** em uma janela do Terminal. Use o endereço inet listado no adaptador de rede ativo.  
  
3. Na barra de menus do Visual Studio, escolha **Ferramentas**, **Opções**.  
  
4. Na caixa de diálogo **Opções**, expanda **Multiplataforma**, **C++**, **iOS**.  
  
5. Nos campos **Nome do Host** e **Porta**, insira os valores especificados pelo agente remoto quando você o iniciou. O nome do host pode ser o nome DNS ou o endereço IP do seu Mac. A porta padrão é a 3030.  
  
   > [!NOTE]
   >  Se não puder executar ping do Mac usando o nome do host, você precisará usar o endereço IP.  
  
6. Se você usar o agente remoto no modo de conexão segura padrão, marque a caixa de seleção **Seguro** e insira o valor do PIN especificado pelo agente remoto no campo **Pin**. Se você usar o agente remoto no modo de conexão não segura, desmarque a caixa de seleção **Seguro** e deixe o campo **Pin** em branco.  
  
7. Escolha **Emparelhamento** para habilitar o emparelhamento.  
  
    ![Configurar a conexão de vcremote para compilações do iOS](../cross-platform/media/cppmdd-options-ios.PNG "CPPMDD_Options_iOS")  
  
    O emparelhamento persiste até que você altere o nome do host ou a porta. Se você alterar o nome do host ou a porta na caixa de diálogo **Opções**, para desfazer a alteração, escolha o botão **Reverter** para reverter o emparelhamento anterior.  
  
    Se o emparelhamento não for bem-sucedido, verifique se o agente remoto está em execução seguindo as etapas em [Iniciar o agente remoto](#Start). Se muito tempo tiver decorrido desde que o PIN do agente remoto foi gerado, siga as etapas em [Gerar um novo PIN de segurança](#GeneratePIN) no Mac e tente novamente. Se você estiver usando o nome de host do seu Mac, tente usar o endereço IP no campo **Nome do Host** em vez disso.  
  
8. Atualize o nome da pasta no campo **Raiz Remota** para especificar a pasta usada pelo agente remoto em seu diretório inicial (~) no Mac. Por padrão, o agente remoto usa /Users/`username`/vcremote como a raiz remota.  
  
9. Escolha **OK** para salvar as configurações de conexão de emparelhamento remoto.  
  
   O Visual Studio usa as mesmas informações para se conectar ao agente remoto no seu Mac sempre que você usá-lo. Você não precisa emparelhar o Visual Studio ao agente remoto novamente a menos que gere um novo certificado de segurança no Mac ou que seu nome de host ou endereço IP seja alterado.  
  
##  <a name="GeneratePIN"></a> Gerar um novo PIN de segurança  
 Quando você inicia o agente remoto pela primeira vez, o PIN gerado é válido por um período limitado — por padrão, 10 minutos. Se você não emparelhar o Visual Studio ao agente remoto antes desse período expirar, será necessário gerar um novo PIN.  
  
#### <a name="to-generate-a-new-pin"></a>Para gerar um novo PIN  
  
1.  Pare o agente ou abra uma segunda janela do aplicativo Terminal no Mac e use-a para inserir o comando.  
  
2.  Digite este comando no aplicativo Terminal:  
  
     `vcremote generateClientCert`  
  
     O agente remoto gera um novo PIN temporário. Para emparelhar o Visual Studio usando o novo PIN, repita as etapas em [Configurar o agente remoto no Visual Studio](#ConfigureVS).  
  
##  <a name="GenerateCert"></a> Gerar um novo certificado do servidor  
 Por motivos de segurança, os certificados de servidor que emparelham o Visual Studio ao agente remoto estão vinculados ao nome de host ou ao endereço IP do seu Mac. Se esses valores forem alterados, você precisará gerar um novo certificado do servidor e reconfigurar o Visual Studio com os novos valores.  
  
#### <a name="to-generate-a-new-server-certificate"></a>Para gerar um novo certificado do servidor  
  
1.  Pare o agente remoto.  
  
2.  Digite este comando no aplicativo Terminal:  
  
     `vcremote resetServerCert`  
  
3.  Quando for solicitado a confirmar, digite `Y`.  
  
4.  Digite este comando no aplicativo Terminal:  
  
     `vcremote generateClientCert`  
  
     Isso gera um novo PIN temporário.  
  
5.  Para emparelhar o Visual Studio usando o novo PIN, repita as etapas em [Configurar o agente remoto no Visual Studio](#ConfigureVS).  
  
##  <a name="ConfigureMac"></a> Configurar o agente remoto no Mac  
 É possível configurar o agente remoto usando várias opções de linha de comando. Por exemplo, você pode especificar a porta para escutar solicitações de compilação e especificar o número máximo de compilações a serem mantidas no sistema de arquivos. Por padrão, o limite é de 10 compilações. O agente remoto removerá as compilações que ultrapassarem o máximo no desligamento.  
  
#### <a name="to-configure-the-remote-agent"></a>Para atualizar o agente remoto  
  
-   Para ver uma lista completa dos comandos do agente remoto, no aplicativo Terminal, digite:  
  
     `vcremote --help`  
  
-   Para desabilitar o modo seguro e habilitar conexões simples baseadas em HTTP, digite:  
  
     `vcremote --secure false`  
  
     Quando usar essa opção, desmarque a caixa de segurança **Seguro** e deixe o campo **Pin** em branco ao configurar o agente no Visual Studio.  
  
-   Para especificar um local para arquivos de agente remoto, digite:  
  
     `vcremote --serverDir directory_path`  
  
     em que *directory_path* é o local no seu Mac para colocar os arquivos de log, compilações e certificados de servidor. Por padrão, esse local é /Users/*nome do usuário*/vcremote. As compilações são organizadas por número de build nesse local.  
  
-   Para usar um processo em segundo plano para capturar `stdout` e `stderr` para um arquivo chamado server.log, digite:  
  
     `vcremote > server.log 2>&1 &`  
  
     O arquivo server.log pode ajudar na solução de problemas de build.  
  
-   Para executar o agente usando um arquivo de configuração em vez de parâmetros de linha de comando, digite:  
  
     `vcremote --config config_file_path`  
  
     em que *config_file_path* é o caminho para um arquivo de configuração no formato JSON. As opções de inicialização e seus valores não devem incluir traços.  
  
## <a name="see-also"></a>Consulte também  
 [Instalar o Visual C++ para Desenvolvimento Móvel Multiplataforma](../cross-platform/install-visual-cpp-for-cross-platform-mobile-development.md)

