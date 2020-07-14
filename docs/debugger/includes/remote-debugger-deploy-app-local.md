---
title: Implantar na pasta local
description: Implantar um aplicativo em uma pasta local
services: ''
author: mikejo5000
ms.service: ''
ms.topic: include
ms.date: 05/23/2018
ms.author: mikejo
ms.custom: include file
ms.openlocfilehash: 3fa0569739ee81ec4b2aa0eec8157068ffc949cd
ms.sourcegitcommit: 748d9cd7328a30f8c80ce42198a94a4b5e869f26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68149213"
---
1. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **publicar** (para Web Forms, **publicar aplicativo Web**).

    Se você já tiver configurado anteriormente quaisquer perfis de publicação, o painel **Publicar** será exibido. Clique em **novo perfil**.

1. Na caixa de diálogo **publicar** , selecione **pasta**, clique em **procurar**e crie uma nova pasta, **C:\Publish**.

    ![RemoteDBG_Publish_Local](../media/remotedbg_publish_local.png "RemoteDBG_Publish_Local")

    Para um aplicativo Web Forms, escolha **personalizado** na caixa de diálogo publicar, insira um nome de perfil e escolha **OK**.

1. Clique em **Criar perfil** na lista suspensa (**publicar** é o valor padrão).

1. Na caixa de diálogo **publicar** , clique no link **configurações** e, em seguida, selecione a guia **configurações** .

1. Defina a configuração a ser **depurada**, selecione **excluir todos os arquivos existentes antes de publicar**e clique em **salvar**.

    > [!NOTE]
    > Se você usar uma compilação de versão, desabilite a depuração no arquivo de web.config quando publicar.

1. Clique em **Publicar**.

    ![RemoteDBG_Publish_Debug_Config](../media/remotedbg_publish_debug_config.png "RemoteDBG_Publish_Debug_Config")

    O aplicativo publica uma configuração de **depuração** do projeto na pasta local. O progresso é mostrado na janela saída.

1. Copie o diretório do projeto ASP.NET do computador do Visual Studio para o diretório local configurado para o aplicativo ASP.NET (neste exemplo, **C:\Publish**) no computador do Windows Server. Neste tutorial, supomos que você está copiando manualmente, mas pode usar outras ferramentas como PowerShell, xcopy ou Robocopy.

    > [!CAUTION]
    > Se precisar fazer alterações no código ou recompilar, você deverá republicar e repetir essa etapa. O executável que você copiou para o computador remoto deve corresponder exatamente à fonte local e aos símbolos.    Se você não fizer isso, receberá um `cannot find or open the PDB file` aviso no Visual Studio ao tentar depurar o processo.

1. No Windows Server, verifique se você pode executar o aplicativo corretamente abrindo o aplicativo em seu navegador.

    Se o aplicativo não for executado corretamente, poderá haver uma incompatibilidade entre a versão do ASP.NET instalada no servidor e o computador do Visual Studio, ou talvez você tenha um problema com a configuração do IIS ou do site. Verifique novamente as etapas anteriores.
