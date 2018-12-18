---
title: Implantar aplicativos da Windows Store pelo Visual Studio | Microsoft Docs
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
ms.assetid: ef3a0f36-bfc9-4ca0-aa61-18261f619bff
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 1b6d94eb5541ea79fdc7ba2d1d3ebe5ef02df2d6
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51806042"
---
# <a name="deploy-windows-store-apps-from-visual-studio"></a>Implantar aplicativos da Windows Store pelo Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Aplica-se ao Windows apenas] (... /Image/windows_only_content.png "windows_only_content")  
  
 A funcionalidade de implantação do Visual Studio compila e registra aplicativos na Windows Store que são criados com o Visual Studio em um dispositivo de destino. Exatamente como o aplicativo é registrado depende de o dispositivo de destino ser local ou remoto:  
  
- Quando o destino é o computador local com o Visual Studio, ele registra o aplicativo de sua pasta de build.  
  
- Quando o destino é um dispositivo remoto, o Visual Studio copia os arquivos necessários ao computador remoto e registra o aplicativo nesse dispositivo.  
  
  Implantação é automática quando você depura seu aplicativo do Visual Studio usando o **iniciar depuração** opção (teclado: F5) ou o **Start Without Debugging** opção (teclado: CTRL + F5). Você também pode implantar seu aplicativo manualmente. A implantação manual é útil nos seguintes cenários:  
  
- Teste ad-hoc em um computador local ou remoto.  
  
- Implantação de um aplicativo que iniciará outro aplicativo que você quer depurar.  
  
- Implantação de um aplicativo que será depurado quando é iniciado por outro aplicativo ou método.  
  
##  <a name="BKMK_In_this_topic"></a> Neste tópico  
 Neste tópico, você pode aprender:  
  
 [Como implantar um aplicativo da Windows Store](#BKMK_How_to_deploy_a_Windows_Store_app)  
  
 [Como especificar um dispositivo remoto](#BKMK_How_to_specify_a_remote_device)  
  
 [Opções de implantação](#BKMK_Deployment_options)  
  
##  <a name="BKMK_How_to_deploy_a_Windows_Store_app"></a> Como implantar um aplicativo da Windows Store  
 Implantar manualmente um aplicativo é simples:  
  
1.  Se você está implantando para um dispositivo remoto, especifique o nome ou o endereço IP do dispositivo na página de propriedade do projeto de inicialização do aplicativo. (As etapas para fazer isso são listadas a seguir neste tópico.)  
  
2.  Na barra de ferramentas do depurador Visual Studio, escolha o destino de implantação na lista suspensa ao lado de **iniciar depuração** botão.  
  
     ![Executar no computador Local](../debugger/media/vsrun-f5-local.png "VSRUN_F5_Local")  
  
3.  Sobre o **construir** menu, escolha **implantar**  
  
##  <a name="BKMK_How_to_specify_a_remote_device"></a> Como especificar um dispositivo remoto  
 **Pré-requisitos**  
  
 Para implantar um aplicativo em um dispositivo remoto:  
  
-   Uma licença de desenvolvedor deve estar instalada no dispositivo remoto.  
  
-   As Ferramentas Remotas do Visual Studio devem estar instaladas no dispositivo remoto e o Monitor de Depuração Remota deve estar em execução.  
  
     A implantação usa o canal de rede do depurador remoto para enviar os arquivos do aplicativo ao dispositivo remoto.  
  
#### <a name="to-specify-a-remote-device"></a>Para especificar um dispositivo remoto  
  
1. Na página de propriedade de depuração do projeto de inicialização, especifique o nome ou o endereço IP de um destino de implantação remoto.  
  
2. Para abrir a página de propriedades de depuração, escolha o projeto no Gerenciador de soluções e, em seguida, escolha **propriedades** no menu de atalho.  
  
3. Em seguida, escolha o **depurar** nó na janela de páginas de propriedade.  
  
4. Você pode digitar o nome ou endereço IP do dispositivo remoto, ou você pode escolher o dispositivo a partir de **Selecionar Conexão de depurador remoto** caixa de diálogo.  
  
    ![Marque a caixa de diálogo Conexão de depurador remoto](../debugger/media/vsrun-selectremotedebuggerdlg.png "VSRUN_SelectRemoteDebuggerDlg")  
  
    O **Selecionar Conexão de depurador remoto** caixa de diálogo exibe os dispositivos na sub-rede local e em qualquer dispositivo que está conectado diretamente ao computador do Visual Studio por um cabo Ethernet.  
  
   **Especificar o dispositivo remoto em uma página de projeto do Visual C++ ou JavaScript**  
  
   ![C&#43; &#43; propriedades para depuração remota do projeto](../debugger/media/vsrun-cpp-projprop-remote.png "VSRUN_CPP_ProjProp_Remote")  
  
5. Escolher **depurador remoto** da **depurador a iniciar** lista.  
  
6. Insira o nome de rede do dispositivo remoto na **nome da máquina** caixa. Ou então, você pode escolher a seta para baixo na caixa para selecionar o dispositivo da caixa de diálogo Selecionar Conexão de Depurador Remoto.  
  
   **Especificar o dispositivo remoto em uma página de projeto do Visual c# e Visual Basic**  
  
   ![Gerenciado propriedades do projeto para depuração remota](../debugger/media/vsrun-managed-projprop-remote.png "VSRUN_Managed_ProjProp_Remote")  
  
7. Escolher **computador remoto** da **dispositivo de destino** lista.  
  
8. Insira o nome de rede do dispositivo remoto na **computador remoto** caixa ou clique em **localizar** para escolher o dispositivo dos **Selecionar Conexão de depurador remoto** caixa de diálogo.  
  
##  <a name="BKMK_Deployment_options"></a> Opções de implantação  
 Você pode definir as opções de implantação a seguir na página de propriedade de depuração do projeto de inicialização.  
  
 **Permitir Loopback de rede**  
 Por motivos de segurança, um aplicativo [!INCLUDE[win8_appname_long](../includes/win8-appname-long-md.md)] instalado de maneira padrão não pode efetuar chamadas de rede para o dispositivo em que está instalado. Por padrão, a implantação do Visual Studio cria uma isenção dessa regra para o aplicativo implantado. Essa isenção permite que você teste procedimentos de comunicação em um único computador. Antes de enviar seu aplicativo para [!INCLUDE[win8_appstore_long](../includes/win8-appstore-long-md.md)], você deve testá-lo sem a isenção.  
  
 Para remover a isenção de loopback de rede do aplicativo:  
  
- Na página de propriedade de depuração c# e VB, desmarque a **permitir Loopback de rede** caixa de seleção.  
  
- Na página de propriedade de JavaScript e depuração, defina as **permitir Loopback de rede** valor para **não**.  
  
  **Não iniciar, mas depurar meu código quando ele iniciar (c# e VB) / Iniciar aplicativo (JavaScript e C++)**  
  Para configurar a implantação para iniciar automaticamente uma sessão de depuração quando o aplicativo é iniciado:  
  
- Na página de propriedade de depuração c# e VB, marque a **não iniciar, mas depurar meu código quando iniciar** caixa de seleção.  
  
- Na página de propriedade de JavaScript e depuração, defina as **aplicativo&lt;3}.&lt;1** valor para **Sim**.  
  
## <a name="see-also"></a>Consulte também  
 [Executar aplicativos usando o Visual Studio](../debugger/run-store-apps-from-visual-studio.md)



