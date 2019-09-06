---
title: Implantar um contêiner do Docker ASP.NET Core no Hub do Docker | Microsoft Docs
description: Saiba como usar as ferramentas de contêiner do Visual Studio para implantar um aplicativo Web ASP.NET Core no Hub do Docker
author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.devlang: dotnet
ms.topic: article
ms.date: 07/23/2019
ms.author: ghogen
ms.openlocfilehash: 267e0c1ed1ac3911aad2161f186bf4a482f069b6
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "70312192"
---
# <a name="deploy-to-docker-hub"></a>Implantar no Docker Hub

O Hub do Docker fornece um serviço de hospedagem conveniente para seus repositórios de imagens. Você pode facilmente implantar no Hub do Docker manualmente a partir do Visual Studio.

## <a name="create-a-docker-account-and-docker-hub-repository"></a>Criar uma conta do Docker e um repositório do Hub do Docker

[Inscreva-](https://hub.docker.com/signup) se para uma conta do Docker, se você ainda não tiver uma.

Se você não tiver um repositório do Hub do Docker, crie um no [Hub do Docker](https://hub.docker.com/).

## <a name="publish-the-image-for-a-single-project-to-docker-hub"></a>Publicar a imagem de um único projeto no Hub do Docker

1. Clique com o botão direito do mouse no nó do projeto e escolha **publicar...** . É exibida uma tela mostrando as opções de implantação.

   ![](media/deploy-docker-hub/container-tools-docker-hub-deploy.png)

1. Em **escolher um destino de publicação**, escolha **registro de contêiner**e, em seguida, selecione **Hub do Docker**. A caixa de diálogo **Hub do Docker** é exibida.

   ![](media/deploy-docker-hub/container-tools-docker-hub-credentials.png)

1. Se você estiver se conectando ao seu próprio repositório (não faz parte de uma organização), deixe a caixa de seleção **publicar em um repositório pessoal** verificada. Se o repositório for de propriedade de uma organização, desmarque a caixa de seleção e insira o nome da organização. Insira o nome de usuário e a senha do Docker para sua conta do Docker que tenha permissões para acessar o repositório ao qual você está se conectando e, em seguida, selecione **salvar**.  

   O Visual Studio tenta implantar a imagem no Hub do Docker.  Se for bem-sucedida, a tela de **publicação** aparecerá com a URL da imagem do repositório, a marca de imagem, o repositório e a configuração de compilação * * (por exemplo, **versão**).

   ![](media/deploy-docker-hub/container-tools-docker-hub-finished.png)

1. Você pode atualizar a imagem a qualquer momento clicando no botão **publicar** nesta página.  Ou, você pode modificar ou remover o perfil usando os links abaixo da URL.

## <a name="next-steps"></a>Próximas etapas

Publique no [registro de contêiner do Azure](/azure/container-registry/) seguindo as etapas em [implantar no registro de contêiner do Azure](vs-azure-tools-docker-hosting-web-apps-in-docker.md).

Configure a integração e a entrega contínuas (CI/CD) com [Azure pipelines](/azure/devops/pipelines/?view=azure-devops).

## <a name="see-also"></a>Consulte também

[Implantar](deploy-app-service.md)
nas ferramentas de contêiner do serviço Azure app do[Visual Studio](/visualstudio/containers/).