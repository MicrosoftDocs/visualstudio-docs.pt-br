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
ms.openlocfilehash: b6ceee76d8c24ccddb41e47c0865d96c79e6fc32
ms.sourcegitcommit: 79a6be815244f1cfc7b4123afff29983fce0555c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249880"
---
1. Na **Gerenciador de soluções**, clique com o botão direito do mouse no nó do projeto e selecione **publicar** (para Web Forms, **publicar aplicativo Web**).

    Se você já tiver configurado anteriormente quaisquer perfis de publicação, o painel **Publicar** será exibido. Clique em **novo perfil**.

1. Na caixa de diálogo **publicar** , selecione **pasta**, clique em **procurar** e crie uma nova pasta, **C:\Publish**.

   ::: moniker range=">=vs-2019"

   :::image type="content" source="../media/vs-2019/remotedbg-publish-local.png" alt-text="Captura de tela da caixa de diálogo escolher um destino de publicação no Visual Studio com a pasta ' C:\Publish ' selecionada como o destino de publicação.":::

   Clique em **concluir** para salvar o perfil de publicação.
   ::: moniker-end
   ::: moniker range="vs-2017"
   ![Captura de tela da caixa de diálogo escolher um destino de publicação no Visual Studio com a pasta ' bin\Release\Publish ' selecionada como o destino de publicação.](../media/remotedbg_publish_local.png)
   Para um aplicativo Web Forms, escolha **personalizado** na caixa de diálogo publicar, insira um nome de perfil e escolha **OK**.

   Clique em **Criar perfil** na lista suspensa (**publicar** é o valor padrão).
   ::: moniker-end

1. Alterne para uma configuração de depuração.

   ::: moniker range=">=vs-2019"
   Escolha **Editar** para editar o perfil e, em seguida, escolha **configurações**. Escolha uma configuração de **depuração** e escolha **remover arquivos adicionais no destino** nas opções de **publicação de arquivo** .
   ::: moniker-end
   ::: moniker range="vs-2017"
   Na caixa de diálogo **configurações** , habilite a depuração clicando em **Avançar**, escolha uma configuração de **depuração** e, em seguida, escolha **remover arquivos adicionais no destino** nas opções de **publicação de arquivo** .
   ::: moniker-end

   > [!NOTE]
   > Se você usar uma compilação de versão, desabilite a depuração no arquivo de *web.config* quando publicar.

1. Clique em **Publicar**.

    ![Captura de tela da guia configurações na caixa de diálogo publicar. A configuração está definida como depurar e o botão Publicar está selecionado.](../media/remotedbg_publish_debug_config.png)

    O aplicativo publica uma configuração de **depuração** do projeto na pasta local. O progresso é mostrado na janela saída.

1. Copie o diretório do projeto ASP.NET do computador do Visual Studio para o diretório local configurado para o aplicativo ASP.NET (neste exemplo, **C:\Publish**) no computador do Windows Server. Neste tutorial, supomos que você está copiando manualmente, mas pode usar outras ferramentas como PowerShell, xcopy ou Robocopy.

    > [!CAUTION]
    > Se precisar fazer alterações no código ou recompilar, você deverá republicar e repetir essa etapa. O executável que você copiou para o computador remoto deve corresponder exatamente à fonte local e aos símbolos. Se você não fizer isso, receberá um `cannot find or open the PDB file` aviso no Visual Studio ao tentar depurar o processo.

1. No Windows Server, verifique se você pode executar o aplicativo corretamente abrindo o aplicativo em seu navegador.

    Se o aplicativo não for executado corretamente, poderá haver uma incompatibilidade entre a versão do ASP.NET instalada no servidor e o computador do Visual Studio, ou talvez você tenha um problema com a configuração do IIS ou do site. Verifique novamente as etapas anteriores.
