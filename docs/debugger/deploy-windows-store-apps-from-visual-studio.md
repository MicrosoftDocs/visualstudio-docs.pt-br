---
title: Implantar aplicativos UWP | Microsoft Docs
ms.custom: seodec18
ms.date: 01/16/2018
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: d8006fb0ddcab4ab3eeee1616632d2dc513428ba
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53056805"
---
# <a name="deploy-uwp-apps-from-visual-studio"></a>Implantar aplicativos UWP usando o Visual Studio

A funcionalidade de implantação do Visual Studio cria e registra aplicativos UWP que são criados com o Visual Studio em um dispositivo de destino. Exatamente como o aplicativo é registrado depende de o dispositivo de destino ser local ou remoto:

- Quando o destino é o computador local com o Visual Studio, ele registra o aplicativo de sua pasta de build.

- Quando o destino é um dispositivo remoto, o Visual Studio copia os arquivos necessários ao computador remoto e registra o aplicativo nesse dispositivo.

A implantação é automática quando você depura seu aplicativo do Visual Studio usando a opção Iniciar depuração** (Teclado: F5) ou o **Start Without Debugging** opção (teclado: CTRL + F5 Você também pode implantar seu aplicativo manualmente. A implantação manual é útil nos seguintes cenários:

- Teste ad-hoc em um computador local ou remoto.

- Implantação de um aplicativo que iniciará outro aplicativo que você quer depurar.

- Implantação de um aplicativo que será depurado quando é iniciado por outro aplicativo ou método.

##  <a name="BKMK_How_to_deploy_a_Windows_Store_app"></a> Como implantar um aplicativo UWP
 Implantar manualmente um aplicativo é simples:

1.  Se você está implantando para um dispositivo remoto, especifique o nome ou o endereço IP do dispositivo na página de propriedade do projeto de inicialização do aplicativo. (As etapas para fazer isso são listadas a seguir neste tópico.)

2.  Na barra de ferramentas Visual Studio do depurador, escolha o destino da implantação na lista suspensa ao lado do botão **Iniciar Depuração**.

     ![Executar no computador Local](../debugger/media/vsrun_f5_local.png "VSRUN_F5_Local")

3.  No menu **Compilar**, escolha **Implantar**

##  <a name="BKMK_How_to_specify_a_remote_device"></a> Como especificar um dispositivo remoto

**Pré-requisitos**

Em um dispositivo remoto do Windows 10, você deve habilitar [modo de desenvolvedor](/windows/uwp/get-started/enable-your-device-for-development). Em dispositivos Windows 10 que executam a atualização do criador ou posterior, as ferramentas remotas são instaladas automaticamente quando você implanta seu aplicativo. Para obter mais informações, consulte [depurar pacote de aplicativo instalado](../debugger/debug-installed-app-package.md).

> [!NOTE]
> Em versões de atualização do pre-criador do Windows 10, as ferramentas remotas para Visual Studio deve ser instaladas no dispositivo remoto e o depurador remoto deve estar em execução.

A implantação usa o canal de rede do depurador remoto para enviar os arquivos do aplicativo ao dispositivo remoto.

#### <a name="to-specify-a-remote-device"></a>Para especificar um dispositivo remoto

1. Na página de propriedade de depuração do projeto de inicialização, especifique o nome ou o endereço IP de um destino de implantação remoto.

2. Para abrir a página de propriedades de depuração, escolha o projeto no Gerenciador de Soluções e **Propriedades** no menu de atalho.

3. Em seguida, escolha o nó **Depurar** na janela de páginas de propriedades.

4. Para **dispositivo de destino**, selecione **máquina remota**.

5. Sob **computador remoto**, clique em **localizar**.

6. Você pode digitar o nome ou endereço IP do dispositivo remoto, ou você pode escolher o dispositivo a partir de **Conexão remota** caixa de diálogo.

    ![Marque a caixa de diálogo Conexão de depurador remoto](../debugger/media/vsrun_selectremotedebuggerdlg.png "VSRUN_SelectRemoteDebuggerDlg")

    O **Conexão remota** caixa de diálogo exibe os dispositivos na sub-rede local e em qualquer dispositivo que está conectado diretamente ao computador do Visual Studio por um cabo Ethernet.

   **Especificando o dispositivo remoto na página de projetos em JavaScript ou Visual C++**

   ![C&#43; &#43; propriedades para depuração remota do projeto](../debugger/media/vsrun_cpp_projprop_remote.png "VSRUN_CPP_ProjProp_Remote")

7. Escolha **Depurador Remoto** na lista **Depurador a ser iniciado**.

8. Insira o nome de rede do dispositivo remoto na caixa **Nome do Computador**. Ou então, você pode escolher a seta para baixo na caixa para selecionar o dispositivo da caixa de diálogo Selecionar Conexão de Depurador Remoto.

   **Especificando o dispositivo remoto em uma página de projetos em Visual C# e Visual Basic**

   ![Gerenciado propriedades do projeto para depuração remota](../debugger/media/vsrun_managed_projprop_remote.png "VSRUN_Managed_ProjProp_Remote")

9. Escolha **Computador Remoto** na lista **Dispositivo de Destino**.

10. Insira o nome de rede do dispositivo remoto na caixa **Computador Remoto** ou clique em **Localizar** para escolher o dispositivo na caixa de diálogo **Selecionar conexão de depurador remoto**.

##  <a name="BKMK_Deployment_options"></a> Opções de implantação

Você pode definir as opções de implantação a seguir na página de propriedade de depuração do projeto de inicialização.

**Permitir loopback de rede**

Por motivos de segurança, um UWP ou [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] aplicativo instalado da maneira padrão não tem permissão para fazer chamadas de rede para o dispositivo está instalado. Por padrão, a implantação do Visual Studio cria uma isenção dessa regra para o aplicativo implantado. Essa isenção permite que você teste procedimentos de comunicação em um único computador. Antes de enviar seu aplicativo para [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)], você deve testá-lo sem a isenção.

Para remover a isenção de loopback de rede do aplicativo:

- Sobre o C# e Visual Basic Depurar página de propriedades, desmarque a **permitir Loopback de rede** caixa de seleção.

- Na página de propriedades JavaScript e depuração, defina o valor de **Permitir loopback de rede** como **Não**.

**Não iniciar, mas depurar meu código quando ele é iniciado (C# e Visual Basic) / Iniciar aplicativo (JavaScript e C++)**

Para configurar a implantação para iniciar automaticamente uma sessão de depuração quando o aplicativo é iniciado:

- Sobre o C# e a página de propriedades de depuração do Visual Basic, verifique o **não iniciar, mas depurar meu código quando ele é iniciado** caixa de seleção.

- Na página de propriedades JavaScript e depuração, defina o valor de **Iniciar Aplicativo** como **Sim**.

## <a name="see-also"></a>Consulte também

- [Opções avançadas de implantação remota](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)
- [Depurar pacote de aplicativo instalado](../debugger/debug-installed-app-package.md)
- [Executar aplicativos usando o Visual Studio](../debugger/run-store-apps-from-visual-studio.md)
