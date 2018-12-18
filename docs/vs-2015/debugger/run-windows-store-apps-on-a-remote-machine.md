---
title: Aplicativos de execução Windows Store em um computador remoto | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-debug
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: 0f6814d6-cd0d-49f3-b501-dea8c094b8ef
caps.latest.revision: 47
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3a3be715f58d3ed80122dfdd3aaf879c7db8aebd
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51784540"
---
# <a name="run-windows-store-apps-on-a-remote-machine"></a>Executar aplicativos da Windows Store em um computador remoto
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows apenas] (... /Image/windows_only_content.png "windows_only_content")  
  
 O aplicativo Ferramentas Remotas do Visual Studio permite executar, depurar, analisar e testar um aplicativo da Windows Store sendo executado em um dispositivo de um segundo computador que esteja executando o Visual Studio. A execução em um dispositivo remoto pode ser especialmente eficaz quando o computador do Visual Studio não oferece suporte à funcionalidade específica dos aplicativos da Windows Store, como toque, localização geográfica e orientação física. Este tópico descreve os procedimentos para configurar e iniciar uma sessão remota.  
  
##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 Você aprende sobre:  
  
 [Pré-requisitos](#BKMK_Prerequisites)  
  
 [Segurança](#BKMK_Security)  
  
 [Como se conectar diretamente a um dispositivo remoto](#BKMK_DirectConnect)  
  
 [Instalando as ferramentas remotas](#BKMK_Installing_the_Remote_Tools)  
  
 [Iniciando o Monitor de depuração remota](#BKMK_Starting_the_Remote_Debugger_Monitor)  
  
 [Configurando o depurador remoto](#BKMK_ConfigureRemoteDebugger)  
  
 [Configurando o projeto do Visual Studio para depuração remota](#BKMK_ConnectVS)  
  
- [Escolhendo o dispositivo remoto para projetos c# e Visual Basic](#BKMK_Choosing_the_remote_device_for_C__and_Visual_Basic_projects)  
  
- [Escolhendo o dispositivo remoto para projetos em JavaScript e C++](#BKMK_Choosing_the_remote_device_for_JavaScript_and_C___projects)  
  
  [Execução de uma sessão de depuração remota](#BKMK_RunRemoteDebug)  
  
##  <a name="BKMK_Prerequisites"></a> Pré-requisitos  
 Para depurar em um dispositivo remoto:  
  
-   O dispositivo remoto e o computador com o Visual Studio devem estar conectados por uma rede ou diretamente por um cabo Ethernet. Não há suporte à depuração pela Internet.  
  
-   Uma licença de desenvolvedor deve estar instalada no dispositivo remoto.  
  
-   O dispositivo remoto deve estar executando os componentes de depuração remota.  
  
-   Você deve ser um administrador do dispositivo remoto para configurar o firewall durante a instalação. Você deve ter acesso de usuário ao dispositivo remoto para executar o depurador remoto ou conectar-se a ele.  
  
##  <a name="BKMK_Security"></a> Segurança  
 Por padrão, o depurador remoto usa a Autenticação do Windows.  
  
> [!WARNING]
>  Você também pode optar por executar o depurador remoto no Modo Sem Autenticação, mas isso é altamente desaconselhável. Nesse modo não há nenhuma segurança de rede. Escolha o Modo Sem Autenticação somente se você tiver certeza de que a rede não corre risco de tráfego mal-intencionado ou hostil.  
  
##  <a name="BKMK_DirectConnect"></a> Como se conectar diretamente a um dispositivo remoto  
 Para se conectar diretamente a um dispositivo remoto, conecte o computador com o Visual Studio ao dispositivo usando um cabo Ethernet padrão. Se o dispositivo não tiver uma porta Ethernet, você poderá usar um adaptador USB-Ethernet para se conectar ao cabo.  
  
##  <a name="BKMK_Installing_the_Remote_Tools"></a> Instalando as ferramentas remotas  
  
> [!NOTE]
>  **Versões e atualizações**  
>   
>  O **as ferramentas remotas para Visual Studio 2015** não têm suporte para versões anteriores do Visual Studio.  
>   
>  É recomendável que você instale a versão de atualização das ferramentas remotas para Visual Studio 2015 que corresponde à versão de atualização da instalação do Visual Studio.  
>   
>  O depurador do VS é compatível com qualquer combinação de versões do VS 2015 e as ferramentas remotas para VS 2015. No entanto, o recurso mais recente do Visual Studio exige que o Visual Studio e as Ferramentas Remotas estejam na versão mais atualizada.  
>   
>  Outras ferramentas de diagnóstico podem exigir as mesmas versões das ferramentas remotas e do Visual Studio.  
  
 **Instalando os componentes de depuração remota em um dispositivo remoto**  
  
 Para executar ou salvar o programa de instalação para as ferramentas remotas, escolha um dos links nesta tabela que corresponde à sua versão do Visual Studio:  
  
|Versão|Link|Observações|
|-|-|-|
|Visual Studio 2015 Atualização 3|[Ferramentas remotas](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Se solicitado, ingressar no grupo do Visual Studio Dev Essentials gratuito, ou você pode apenas entrar com uma assinatura válida do Visual Studio. Em seguida, reabra o link se necessário. Sempre Baixe a versão correspondente do seu sistema operacional do dispositivo (x x86, x64 ou versão ARM)|
|Visual Studio 2015 (antiga)|[Ferramentas remotas](https://my.visualstudio.com/Downloads?q=remote%20tools%20visual%20studio%202015)|Se solicitado, ingressar no grupo do Visual Studio Dev Essentials gratuito, ou você pode apenas entrar com uma assinatura válida do Visual Studio. Em seguida, reabra o link se necessário. Sempre Baixe a versão correspondente do seu sistema operacional do dispositivo (x x86, x64 ou versão ARM)|
|Visual Studio 2013|[Ferramentas remotas](https://msdn.microsoft.com/library/bt727f1t(v=vs.120).aspx#BKMK_Installing_the_Remote_Tools)|Baixar a página na documentação do Visual Studio 2013|
  
 É possível optar por baixar o programa de instalação ou executá-lo imediatamente. Quando você executa o programa de instalação, aceite o contrato de usuário e, em seguida, escolha **instalar**.  
  
 Por padrão, os componentes de depuração remotos são instalados na **C:\Program Files\Microsoft Visual Studio 14.0\Common7\IDE\Remote depurador** pasta.  
  
##  <a name="BKMK_Starting_the_Remote_Debugger_Monitor"></a> Iniciando o Monitor de depuração remota  
  
> [!NOTE]
>  Como o depurador remoto configura o firewall para permitir a comunicação com o host do Visual Studio, você deve ser um administrador no dispositivo remoto ao iniciar o depurador remoto pela primeira vez.  
  
 Depois de ter instalado as ferramentas remotas, escolha **depurador remoto** sobre o **iniciar** tela. O **configuração de depuração remota** aparece na primeira vez que você iniciar o depurador remoto.  
  
 Sobre o **configuração de depuração remota** caixa de diálogo:  
  
1.  Se a API de serviços de Web do Windows não estiver instalada, escolha **instalar**  
  
2.  No **configurar o Firewall do Windows** de grupo, escolha as que você deseja permitir conexões com redes. Somente as redes às quais o dispositivo está conectado no momento estão habilitadas. Você deve escolher pelo menos uma rede.  
  
3.  Escolher **configurar a depuração remota** para definir as opções de firewall e iniciar o depurador remoto.  Abra o **Visual Studio Remote Debugging Monitor** avançada de caixa de diálogo para fornecer aos usuários permissões para as ferramentas remotas e definir outras opções.  
  
4.  O **Visual Studio Remote Debugging Monitor** caixa de diálogo é exibida. Você pode fornecer aos usuários permissões para as ferramentas remotas e definir outras opções avançadas nessa caixa de diálogo.  
  
##  <a name="BKMK_ConfigureRemoteDebugger"></a> Configurando o depurador remoto  
 São usadas duas ferramentas para modificar a configuração do depurador remoto.  
  
1. Sobre o **ferramentas** menu da **Visual Studio Remote Debugging Monitor**:  
  
   1.  Escolher **opções** para alterar o número da porta, o modo de autenticação ou o intervalo de tempo limite do depurador remoto.  
  
   2.  Escolher **permissões** para adicionar ou remover usuários que têm permissão para depuração remota.  
  
       > [!NOTE]
       >  As permissões devem ser concedidas a cada conta de usuário que depurar remotamente.  
  
   Você usa o **Assistente de configuração do depurador remoto** para definir opções avançadas para o depurador remoto. Para abrir o assistente, escolha **Assistente de configuração do depurador remoto** na tela inicial.  
  
2. Sobre o **configurar o depurador remoto do Visual Studio** página, que você pode optar por executar o depurador remoto como um serviço. Na maioria dos casos, não é obrigatória a execução como um serviço.  
  
3. Sobre o **configurar o Firewall do Windows para depuração** página, você pode adicionar ou remover o tipo de rede que você deseja que o depurador remoto para se conectar ao. Somente as redes às quais o dispositivo está conectado no momento estão habilitadas. Você deve escolher pelo menos uma rede.  
  
##  <a name="BKMK_ConnectVS"></a> Configurando o projeto do Visual Studio para depuração remota  
 Você especifica o dispositivo remoto ao qual deseja se conectar nas propriedades do projeto. O procedimento varia dependendo da linguagem de programação. Você pode digitar o nome da rede do dispositivo remoto ou pode selecioná-lo na caixa de diálogo Selecionar Conexão de Depurador Remoto.  
  
 ![Marque a caixa de diálogo Conexão de depurador remoto](../debugger/media/vsrun-selectremotedebuggerdlg.png "VSRUN_SelectRemoteDebuggerDlg")  
  
 A caixa de diálogo lista somente os dispositivos que estão na sub-rede local do computador com o Visual Studio e que estão executando o depurador remoto.  
  
> [!TIP]
>  Se você tiver problemas para se conectar a um dispositivo remoto, tente inserir o endereço IP do dispositivo. Para determinar o endereço IP de um dispositivo, abra uma janela de comando e digite **ipconfig**. O endereço IP é listado como **endereço IPv4**.  
  
###  <a name="BKMK_Choosing_the_remote_device_for_C__and_Visual_Basic_projects"></a> Escolhendo o dispositivo remoto para projetos c# e Visual Basic  
 ![Gerenciado propriedades do projeto para depuração remota](../debugger/media/vsrun-managed-projprop-remote.png "VSRUN_Managed_ProjProp_Remote")  
  
1.  Selecione o nome do projeto no Gerenciador de soluções e escolha **propriedades** no menu de atalho.  
  
2.  Selecione **depurar**.  
  
3.  Escolher **computador remoto** da **dispositivo de destino** lista.  
  
4.  Insira o nome de rede do dispositivo remoto na **computador remoto** caixa ou escolha **localizar** para escolher o dispositivo dos **Selecionar Conexão de depurador remoto** caixa de diálogo.  
  
###  <a name="BKMK_Choosing_the_remote_device_for_JavaScript_and_C___projects"></a> Escolhendo o dispositivo remoto para projetos em JavaScript e C++  
 ![C&#43; &#43; propriedades para depuração remota do projeto](../debugger/media/vsrun-cpp-projprop-remote.png "VSRUN_CPP_ProjProp_Remote")  
  
1.  Selecione o nome do projeto no Gerenciador de soluções e escolha **propriedades** no menu de atalho.  
  
2.  Expanda o **propriedades de configuração** nó e, em seguida, selecione **depuração**.  
  
3.  Escolher **depurador remoto** da **depurador a iniciar** lista.  
  
4.  Insira o nome de rede do dispositivo remoto na **nome da máquina** caixa ou clique na seta para baixo na caixa para escolher o dispositivo da **Selecionar Conexão de depurador remoto** caixa de diálogo.  
  
##  <a name="BKMK_RunRemoteDebug"></a> Execução de uma sessão de depuração remota  
 Você inicia e interrompe uma sessão de depuração remota e navega por ela da mesma maneira que faz em uma sessão local. Antes de iniciar a depuração, verifique se o Monitor de Depuração Remota está em execução no dispositivo remoto.  
  
 Em seguida, escolha **iniciar depuração** sobre o **depurar** menu (teclado: F5). O projeto é recompilado, depois é implantado e iniciado no dispositivo remoto. O depurador suspende a execução em pontos de interrupção, e você pode fazer step-into, step-over e step-out do seu código. Escolher **parar depuração** para encerrar a sessão de depuração e fechar o aplicativo remoto. Para obter mais informações, consulte [depurar aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também  
 [Testar aplicativos da Store com o Visual Studio](../test/testing-store-apps-with-visual-studio.md)   
 [Depurar aplicativos no Visual Studio](../debugger/debug-store-apps-in-visual-studio.md)



