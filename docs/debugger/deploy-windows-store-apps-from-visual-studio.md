---
title: Implantar aplicativos UWP | Microsoft Docs
description: Implantar aplicativos Plataforma Universal do Windows (UWP) do Visual Studio. Especifique um dispositivo de destino local ou remoto para implantação. Entenda as opções de implantação.
ms.custom: SEO-VS-2020
ms.date: 01/16/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- uwp
ms.openlocfilehash: 0a1c1802d92beb436bbd2ac87bd1e7a39f6086f1
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112387860"
---
# <a name="deploy-uwp-apps-from-visual-studio"></a>Implantar aplicativos UWP usando o Visual Studio

A funcionalidade de implantação do Visual Studio cria e registra os aplicativos UWP criados com o Visual Studio em um dispositivo de destino. Exatamente como o aplicativo é registrado depende de o dispositivo de destino ser local ou remoto:

- Quando o destino é o computador local com o Visual Studio, ele registra o aplicativo de sua pasta de build.

- Quando o destino é um dispositivo remoto, o Visual Studio copia os arquivos necessários ao computador remoto e registra o aplicativo nesse dispositivo.

A implantação é automática quando você depura seu aplicativo do Visual Studio usando a opção **Iniciar Depuração** (teclado: F5) ou a opção **Iniciar sem depuração** (teclado: CTRL + F5). Você também pode implantar seu aplicativo manualmente. A implantação manual é útil nos seguintes cenários:

- Teste ad-hoc em um computador local ou remoto.

- Implantação de um aplicativo que iniciará outro aplicativo que você quer depurar.

- Implantação de um aplicativo que será depurado quando é iniciado por outro aplicativo ou método.

## <a name="how-to-deploy-a-uwp-app"></a><a name="BKMK_How_to_deploy_a_Windows_Store_app"></a> Como implantar um aplicativo UWP
 Implantar manualmente um aplicativo é simples:

1. Se você está implantando para um dispositivo remoto, especifique o nome ou o endereço IP do dispositivo na página de propriedade do projeto de inicialização do aplicativo. (As etapas para fazer isso são listadas a seguir neste tópico.)

2. Na barra de ferramentas Visual Studio do depurador, escolha o destino da implantação na lista suspensa ao lado do botão **Iniciar Depuração**.

     ![Executar no computador local](../debugger/media/vsrun_f5_local.png "VSRUN_F5_Local")

3. No menu **Compilar**, escolha **Implantar**

## <a name="how-to-specify-a-remote-device"></a><a name="BKMK_How_to_specify_a_remote_device"></a> Como especificar um dispositivo remoto

**Pré-requisitos**

Em um dispositivo remoto do Windows 10, você deve habilitar o [modo de desenvolvedor](/windows/uwp/get-started/enable-your-device-for-development). Em dispositivos Windows 10 executando a atualização do criador ou posterior, as ferramentas remotas são instaladas automaticamente quando você implanta seu aplicativo. Para obter mais informações, consulte [depurar um pacote do aplicativo instalado](../debugger/debug-installed-app-package.md).

> [!NOTE]
> Nas versões de atualização do Windows 10 do pre-Creator, o Ferramentas Remotas para Visual Studio deve ser instalado no dispositivo remoto e o depurador remoto deve estar em execução.

A implantação usa o canal de rede do depurador remoto para enviar os arquivos do aplicativo ao dispositivo remoto.

#### <a name="to-specify-a-remote-device"></a>Para especificar um dispositivo remoto

1. Na página de propriedade de depuração do projeto de inicialização, especifique o nome ou o endereço IP de um destino de implantação remoto.

2. Para abrir a página de propriedades de depuração, escolha o projeto no Gerenciador de Soluções e **Propriedades** no menu de atalho.

3. Em seguida, escolha o nó **Depurar** na janela de páginas de propriedades.

4. Para **dispositivo de destino**, selecione **computador remoto**.

5. Em **computador remoto**, clique em **Localizar**.

6. Você pode digitar o nome ou o endereço IP do dispositivo remoto, ou pode escolher o dispositivo na caixa de diálogo **conexão remota** .

    ![Caixa de diálogo Selecionar conexão do depurador remoto](../debugger/media/vsrun_selectremotedebuggerdlg.png "VSRUN_SelectRemoteDebuggerDlg")

    A caixa de diálogo **conexão remota** exibe os dispositivos na sub-rede da rede local e qualquer dispositivo conectado diretamente ao computador do Visual Studio por um cabo Ethernet.

   **Especificando o dispositivo remoto em uma página de projeto C++**

   ![C&#43;&#43; Propriedades do projeto para depuração remota](../debugger/media/vsrun_cpp_projprop_remote.png "VSRUN_CPP_ProjProp_Remote")

7. Escolha **Depurador Remoto** na lista **Depurador a ser iniciado**.

8. Insira o nome de rede do dispositivo remoto na caixa **Nome do Computador**. Ou então, você pode escolher a seta para baixo na caixa para selecionar o dispositivo da caixa de diálogo Selecionar Conexão de Depurador Remoto.

   **Especificando o dispositivo remoto em uma página de projetos em Visual C# e Visual Basic**

   ![Propriedades do projeto gerenciado para depuração remota](../debugger/media/vsrun_managed_projprop_remote.png "VSRUN_Managed_ProjProp_Remote")

9. Escolha **Computador Remoto** na lista **Dispositivo de Destino**.

10. Insira o nome de rede do dispositivo remoto na caixa **Computador Remoto** ou clique em **Localizar** para escolher o dispositivo na caixa de diálogo **Selecionar conexão de depurador remoto**.

## <a name="deployment-options"></a><a name="BKMK_Deployment_options"></a> Opções de implantação

Você pode definir as opções de implantação a seguir na página de propriedade de depuração do projeto de inicialização.

**Permitir loopback de rede**

Por motivos de segurança, um UWP ou um [!INCLUDE[win8_appname_long](../debugger/includes/win8_appname_long_md.md)] aplicativo que é instalado da maneira padrão não é permitido para fazer chamadas de rede para o dispositivo no qual ele está instalado. Por padrão, a implantação do Visual Studio cria uma isenção da regra para o aplicativo implantado. Esse isolamento permite que você teste procedimentos de comunicação em uma única máquina. Antes de enviar seu aplicativo para [!INCLUDE[win8_appstore_long](../debugger/includes/win8_appstore_long_md.md)], você deve testá-lo sem a isenção.

Para remover a isenção de loopback de rede do aplicativo:

- Na página de propriedades depurar C# e Visual Basic, desmarque a caixa de seleção **permitir loopback de rede** .

- Na página de propriedades de depuração C++, defina o valor de **loopback permitir rede** como **não**.

**Não iniciar, mas depurar meu código quando ele for iniciado (C# e Visual Basic)/iniciar aplicativo (C++)**

Para configurar a implantação para iniciar uma sessão de depuração quando o aplicativo for iniciado automaticamente:

- Na página de propriedades depurar do C# e Visual Basic, marque a caixa de seleção não **Iniciar, mas depurar meu código ao iniciar** .

- Na página de propriedades de depuração do C++, defina o valor do **aplicativo de inicialização** como **Sim**.

## <a name="see-also"></a>Confira também

- [Opções de implementação remota avançadas](/windows/uwp/debug-test-perf/deploying-and-debugging-uwp-apps#advanced-remote-deployment-options)
- [Depurar um pacote do aplicativo instalado](../debugger/debug-installed-app-package.md)
- [Executar aplicativos do Visual Studio](debugging-windows-store-and-windows-universal-apps.md)
