---
title: R e contêineres do Docker
description: Como configurar contêineres do Docker para R e conectá-los ao Visual Studio.
ms.date: 12/04/2017
ms.topic: conceptual
author: kraigb
ms.author: kraigb
ms.reviewer: karthiknadig
manager: jmartens
ms.workload:
- data-science
ms.openlocfilehash: 3aefba3880443269dbdb1c933e2c12b2f8001469
ms.sourcegitcommit: fc05a763b59e212c86350d117a1900a1f2686ec8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2021
ms.locfileid: "111551274"
---
# <a name="use-docker-containers-with-r-tools-for-visual-studio"></a>Use contêineres do Docker com as Ferramentas do R para Visual Studio

As RTVS (Ferramentas do R para Visual Studio) versão 1.3+, juntamente com uma instalação do [Docker para Windows](https://www.docker.com/docker-windows), dão suporte ao trabalho com os contêineres do Docker.

## <a name="create-a-container"></a>Criar um contêiner

1. Selecione o botão **Contêineres** no canto superior direito da janela **Workspaces** (**Ferramentas do R** > **Windows** > **Workspaces**). A janela informará se você não tiver instalado o Docker para Windows e fornecerá um link para o download. A instalação do Docker pode exigir uma reinicialização do computador.

    ![Janela Workspaces nas Ferramentas do R para Visual Studio (VS2017) com o comando Contêineres](media/container-workspaces-window.png)

1. Na janela **Contêineres**, selecione **Criar**:

    ![Criar comando na janela Contêineres](media/containers-window-create.png)

1. Preencha as informações obrigatórias na caixa de diálogo e selecione **Criar**. As credenciais inseridas também são usadas para criar uma conta no Linux, com a qual você entrará mais tarde.

    ![Inserindo um nome e credenciais de contêiner ao criar um contêiner](media/containers-window-create-fill.png)

1. Talvez demore um pouco para as RTVS montarem a imagem. A janela **Saída** no Visual Studio mostra o andamento, mas talvez pareça que ela não esteja fazendo muita coisa durante os downloads demorados de imagem; seja paciente. Depois que a imagem for montada, as RTVS iniciam o contêiner e ele é exibido na janela **Contêiner**. Os controles à direita interrompem, removem ou reiniciam o contêiner.

    ![Janela Contêineres mostrando um contêiner concluído](media/containers-window-created.png)

## <a name="connect-to-a-container"></a>Conectar-se a um contêiner

1. A seção **Contêineres Locais em Execução** da janela **Workspaces** exibe os contêineres que estão executando o daemon das RTVS na porta 5444. (Consulte [Remote R Server for Linux](setting-up-remote-r-service-on-linux.md) (R Server Remoto para Linux) para obter detalhes sobre como o daemon está configurado.)

    ![Janela Workspaces mostrando contêineres disponíveis](media/workspaces-window-running-containers.png)

1. Para conectar-se a um contêiner, clique duas vezes no nome do contêiner ou selecione o botão de seta para frente à sua direita. Quando conectado, você verá uma janela **R Interativo** (consulte [Trabalhar com a janela R Interativo](interactive-repl-for-r-in-visual-studio.md)):

    ![Janelas Workspaces e janela REPL aberta para um contêiner](media/workspaces-window-container-connected.png)

## <a name="use-custom-built-images"></a>Usar imagens personalizadas

As RTVS detectam e permitem o gerenciamento de contêineres criados usando imagens personalizadas, como a imagem microsoft/rtvs descrita no arquivo do docker abaixo. A imagem base usada aqui tem rtvs-daemon, R 3.4.2 e os pacotes R comuns pré-instalados. **Observação**: altere o nome de usuário e a senha mostrados aqui, conforme necessário.

```docker
FROM mcr.microsoft.com/rtvs:1.3-ub1604-r3.4.2
RUN useradd --create-home ruser1
RUN echo "ruser1:foobar" | chpasswd

#Install additional R packages. You may have to install OS dependencies, see package info or error messages during build.
#RUN Rscript --vanilla -e "install.packages(c('AzureML','wordcloud'), repos = 'http://cran.us.r-project.org');"
```

Use o seguinte comando para montar a imagem, alterando o nome do contêiner (o argumento `--name`) conforme desejado:

```bash
docker build -t my-rtvs-image:latest .
docker run -p 6056:5444 --name my-rtvs-container my-rtvs-image:latest rtvsd
```

O argumento `-p 6056:5444` mapeia a porta 6056 para a porta 5444 interna, que as RTVS usam para detectar o rtvs-daemon. Qualquer contêiner que expõe a porta de contêiner 5444 está listado na janela **Workspaces**. É possível usar a janela **Workspaces** para se conectar a um contêiner usando `<<unix>>\ruser1` como o nome de usuário e "foobar" como a senha, a menos que você tenha especificado credenciais diferentes no arquivo do docker.
