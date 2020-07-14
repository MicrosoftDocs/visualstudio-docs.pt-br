---
title: Introdução ao Docker
description: Saiba como adicionar o Docker aos seus projetos no Visual Studio para Mac
author: heiligerdankgesang
ms.author: dominicn
ms.date: 06/17/2019
ms.topic: how-to
ms.openlocfilehash: 5f21d55568328a9aeb9b7982e5978500f7ef715b
ms.sourcegitcommit: 2ce59c2ffeba5ba7f628c2e6c75cba4731deef8a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85939057"
---
# <a name="get-started-with-docker-in-visual-studio-for-mac"></a>Introdução ao Docker no Visual Studio para Mac

Com o Visual Studio para Mac, você pode facilmente criar, depurar e executar aplicativos ASP.NET Core em contêineres e publicá-los no Azure.

## <a name="prerequisites"></a>Pré-requisitos

* [Docker Desktop](https://hub.docker.com/editions/community/docker-ce-desktop-mac)
* [Visual Studio para Mac 2019](https://visualstudio.microsoft.com/vs/mac)

## <a name="installation-and-setup"></a>Instalação e configuração

Para a instalação do Docker, revise e siga as informações em [Instalar Docker Desktop para Mac](https://docs.docker.com/docker-for-mac/install/).

## <a name="creating-an-aspnet-core-web-application-and-adding-docker-support"></a>Como criar um aplicativo Web ASP.NET Core e adicionando suporte ao Docker

1. Crie uma nova solução acessando **Arquivo > Nova Solução**.
1. Em **.NET Core > aplicativo** , escolha o modelo de **aplicativo Web** : ![ criar um novo aplicativo ASP.net](media/docker-quickstart-1.png)
1. Selecione a estrutura de destino. Neste exemplo, usaremos o .NET Core 2,2: ![ definir estrutura de destino](media/docker-quickstart-2.png)
1. Insira os detalhes do projeto, como o nome (_DockerDemo_ neste exemplo). O projeto criado contém todos os princípios necessários para compilar e executar um site do ASP.NET Core.
1. Na Painel de Soluções, clique com o botão direito do mouse no projeto DockerDemo e selecione **adicionar > adicionar suporte ao Docker**: ![ Adicionar suporte ao Docker](media/docker-quickstart-3.png)

O Visual Studio para Mac vai adicionar automaticamente um novo projeto à sua solução denominado **docker-compose** e um **Dockerfile** ao seu projeto existente.

![Arquivos de suporte ao docker gerados](media/docker-quickstart-4.png)

## <a name="dockerfile-overview"></a>Visão geral do Dockerfile

Um Dockerfile é a receita para criar uma imagem final do Docker. Consulte a [referência do Dockerfile](https://docs.docker.com/engine/reference/builder/) para obter uma compreensão dos comandos dentro dele.

```
FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY DockerDemo/DockerDemo.csproj DockerDemo/
RUN dotnet restore DockerDemo/DockerDemo.csproj
COPY . .
WORKDIR /src/DockerDemo
RUN dotnet build DockerDemo.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish DockerDemo.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "DockerDemo.dll"]
```

O *Dockerfile* anterior baseia-se na imagem [microsoft/aspnetcore](https://hub.docker.com/r/microsoft/aspnetcore/) e inclui instruções para modificar a imagem base criando o projeto e adicionando-o ao contêiner.

> [!NOTE]
> O Dockerfile padrão criado pelo Visual Studio para Mac expõe a porta 80 para tráfego HTTP. Para habilitar o tráfego HTTPS, adicione `Expose 443` ao Dockerfile.

## <a name="debugging"></a>Depuração

Defina o projeto `docker-compose` como o Projeto de Inicialização e inicie a depuração (**Executar > Iniciar Depuração**). Isso compila, implanta e inicia o projeto ASP.NET em um contêiner.

> [!TIP]
> Na primeira execução após a instalação do Docker Desktop, você pode receber o seguinte erro ao tentar depurar: `Cannot start service dockerdemo: Mounts denied`
>
> Adicione `/usr/local/share/dotnet/sdk/NuGetFallbackFolder` à guia Compartilhamento de Arquivos no Docker Desktop:
>
> ![Como adicionar a pasta de NuGetFallbackFolder ao Compartilhamento de Arquivos](media/docker-quickstart-5.png)

Quando a compilação estiver concluída, o aplicativo será iniciado no Safari:

![Projeto padrão do Docker em execução no Safari](media/docker-quickstart-6.png)

Observe que o contêiner estará escutando em um porta, `http://localhost:32768` por exemplo, e essa porta pode variar.

Para ver a lista de contêineres em execução, use o comando `docker ps` no Terminal.

Observe a retransmissão de porta na captura de tela abaixo (em **PORTS**). Isso mostra que o contêiner está escutando na porta que vimos no Safari acima e retransmitindo solicitações para o servidor Web interno na porta 80 (conforme definido no Dockerfile). Da perspectiva do aplicativo, ele está escutando na porta 80:

![Lista de contêineres do Docker](media/docker-quickstart-7.png)
