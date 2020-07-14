---
title: Logs de contêiner do Docker, variáveis de ambiente e acesso ao sistema de arquivos
description: Descreve como melhorar sua capacidade de depurar e diagnosticar seus aplicativos baseados em contêiner no Visual Studio usando uma janela de ferramentas para ver o que está acontecendo dentro dos contêineres que hospedam seu aplicativo.
author: ghogen
ms.author: ghogen
ms.topic: how-to
ms.date: 01/20/2020
ms.technology: vs-azure
monikerRange: vs-2019
ms.openlocfilehash: c870378cf277a6008f17ec42d960e07e18a53e86
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283119"
---
# <a name="how-to-view-and-diagnose-containers-and-images-in-visual-studio"></a>Como exibir e diagnosticar contêineres e imagens no Visual Studio

Você pode exibir o que está acontecendo dentro dos contêineres que hospedam seu aplicativo usando a janela **contêineres** . Se você estiver acostumado a usar o prompt de comando para executar comandos do Docker para exibir e diagnosticar o que está acontecendo com seus contêineres, essa janela fornece uma maneira mais conveniente de monitorar seus contêineres sem sair do IDE do Visual Studio.

## <a name="prerequisites"></a>Pré-requisitos

- [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-windows)
- [Visual studio 2019 versão 16,4 Preview 2](https://visualstudio.microsoft.com/downloads) ou posterior, ou se você estiver usando uma versão anterior do Visual Studio 2019, instale a [extensão da janela contêineres](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vs-containers-tools-extensions).

## <a name="view-information-about-your-containers"></a>Exibir informações sobre seus contêineres

A janela **contêineres** é aberta automaticamente quando você inicia um projeto .net em contêiner. Para exibir seus contêineres no Visual Studio a qualquer momento, use **Ctrl** + **Q** para ativar a caixa de pesquisa do Visual Studio e digite `Containers` e escolha o primeiro item. Você também pode abrir a janela **contêineres** no menu principal. Use o menu caminho **Exibir**  >  **outros**  >  **contêineres**do Windows.  

![Captura de tela da guia ambiente na janela contêineres](media/view-and-diagnose-containers/container-window.png)

No lado esquerdo, você verá a lista de contêineres em seu computador local. Os contêineres associados à sua solução são mostrados em **contêineres de solução**. À direita, você vê um painel com guias de **ambiente**, **portas**, **logs**e **arquivos**.

> [!TIP]
> Você pode personalizar facilmente onde a janela de ferramenta **contêineres** está encaixada no Visual Studio. Consulte [Personalizando layouts de janela no Visual Studio](../ide/customizing-window-layouts-in-visual-studio.md). Por padrão, a janela **contêineres** é encaixada com a janela **Watch** quando o depurador está em execução.

## <a name="view-environment-variables"></a>Exibir variáveis de ambiente

A guia **ambiente** mostra as variáveis de ambiente no contêiner. Para o contêiner do seu aplicativo, você pode definir essas variáveis de várias maneiras, por exemplo, no Dockerfile, em um arquivo. env ou usando a opção-e quando você inicia um contêiner usando um comando do Docker.

![Captura de tela da guia ambiente na janela contêineres](media/view-and-diagnose-containers/containers-environment-vars.png)

> [!NOTE]
> As alterações nas variáveis de ambiente não são refletidas em tempo real. Além disso, as variáveis de ambiente nessa guia são as variáveis de ambiente do sistema no contêiner e não refletem as variáveis de ambiente do usuário locais para o aplicativo.

## <a name="view-port-mappings"></a>Exibir mapeamentos de porta

Na guia **portas** , você pode verificar os mapeamentos de porta que estão em vigor para o contêiner.

![Captura de tela da guia portas na janela contêineres](media/view-and-diagnose-containers/containers-ports.png)

As portas conhecidas são vinculadas, portanto, se houver conteúdo disponível em uma porta, você poderá clicar no link para abrir o navegador.

## <a name="view-logs"></a>Exibir logs

A guia **logs** mostra os resultados do `docker logs` comando. Por padrão, a guia mostra fluxos stdout e stderr em um contêiner, mas você pode configurar a saída. Para obter detalhes, consulte [registro em log do Docker](https://docs.docker.com/config/containers/logging/).  Por padrão, a guia **logs** transmite os logs, mas você pode desabilitá-lo escolhendo o botão **parar** na guia.

![Captura de tela da guia logs na janela contêineres](media/view-and-diagnose-containers/containers-logs.png)

Para limpar os logs, use o botão **limpar** na guia **logs** .  Para obter todos os logs, use o botão **Atualizar** .

> [!NOTE]
> O Visual Studio redireciona automaticamente stdout e stderr para a janela de **saída** quando você executa sem depuração com contêineres do Windows, de modo que contêineres do Windows iniciados a partir do Visual Studio usando **Ctrl** + **F5** não exibirão logs nesta guia; em vez disso, use a janela **saída** .

## <a name="view-the-filesystem"></a>Exibir o sistema de arquivos

Na guia **arquivos** , você pode exibir o sistema de arquivos do contêiner, incluindo a pasta do aplicativo que contém o projeto.

![Captura de tela da guia arquivos na janela contêineres](media/view-and-diagnose-containers/container-filesystem.png)

Para abrir arquivos no Visual Studio, navegue até o arquivo e clique duas vezes nele, ou clique com o botão direito do mouse e escolha **abrir**. O Visual Studio abre os arquivos no modo somente leitura.

![Captura de tela de arquivo aberto para exibição no Visual Studio](media/view-and-diagnose-containers/container-file-open.png)

Usando a guia **arquivos** , você pode exibir logs de aplicativos, como logs do IIS, arquivos de configuração e outros arquivos de conteúdo no sistema de arquivos do contêiner.

## <a name="start-stop-and-remove-containers"></a>Iniciar, parar e remover contêineres

Por padrão, a janela **contêineres** mostra todos os contêineres no computador que o Docker gerencia. Você pode usar os botões da barra de ferramentas para iniciar, parar ou remover (excluir) um contêiner que não deseja mais.  Essa lista é atualizada dinamicamente à medida que contêineres são criados ou removidos.

## <a name="open-a-terminal-window-in-a-running-container"></a>Abrir uma janela de terminal em um contêiner em execução

Você pode abrir uma janela do terminal (prompt de comando ou shell interativo) no contêiner usando o botão **Abrir janela do terminal** na janela **contêiner** .

![Captura de tela da janela abrir terminal na janela contêineres](media/view-and-diagnose-containers/containers-open-terminal-window.png)

Para contêineres do Windows, o prompt de comando do Windows é aberto. Para contêineres do Linux, ele abre uma janela usando o shell bash.

![Captura de tela da janela bash](media/view-and-diagnose-containers/container-bash-window.png)

Normalmente, a janela do terminal é aberta fora do Visual Studio como uma janela separada. Se você quiser um ambiente de linha de comando integrado ao IDE do Visual Studio como uma janela de ferramentas do encaixáveis, poderá instalar o [terminal do partilhe partilhe](https://marketplace.visualstudio.com/items?itemName=DanielGriffen.WhackWhackTerminal).

## <a name="attach-the-debugger-to-a-process"></a>Anexar o depurador a um processo

Você pode anexar o depurador a um processo que está sendo executado no contêiner usando o botão **anexar ao processo** na barra de ferramentas da janela contêineres. Quando você usar esse botão, a caixa de diálogo **anexar ao processo** será exibida e mostrará os processos disponíveis em execução no contêiner.  

![Captura de tela da caixa de diálogo anexar ao processo](media/view-and-diagnose-containers/containers-attach-to-process.jpg)

Você pode anexar a processos gerenciados no contêiner. Para procurar um processo em outro contêiner, use o botão **Localizar** e selecione outro contêiner na caixa de diálogo **selecionar contêiner do Docker** .

## <a name="viewing-images"></a>Exibindo imagens

Você também pode exibir imagens no computador local usando a guia **imagens** na janela **contêineres** . As imagens extraídas de repositórios externos são agrupadas em um TreeView. Selecione uma imagem para inspecionar os detalhes da imagem.

Para remover uma imagem, clique com o botão direito do mouse na imagem no modo de exibição de árvore e escolha **remover**ou selecione a imagem e use o botão **remover** na barra de ferramentas.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre as ferramentas de contêiner disponíveis no Visual Studio lendo a [visão geral das ferramentas de contêiner](overview.md).

## <a name="see-also"></a>Veja também

[Desenvolvimento de contêiner no Visual Studio](/visualstudio/containers)

[Marketplace de extensões para Visual Studio](https://marketplace.visualstudio.com/)
