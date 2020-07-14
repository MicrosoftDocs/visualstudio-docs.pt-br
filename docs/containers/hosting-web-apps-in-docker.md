---
title: Implantar o contêiner do Docker ASP.NET no registro ACR
description: Saiba como usar as ferramentas de contêiner do Visual Studio para implantar um aplicativo Web ASP.NET ou ASP.NET Core em um registro de contêiner
author: ghogen
manager: jillfra
ms.assetid: e5e81c5e-dd18-4d5a-a24d-a932036e78b9
ms.devlang: dotnet
ms.topic: how-to
ms.technology: vs-azure
ms.date: 03/14/2019
ms.author: ghogen
ms.openlocfilehash: 9778590d804a72ff896b190a743fc08293f5b9ca
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283132"
---
# <a name="deploy-an-aspnet-container-to-a-container-registry-using-visual-studio"></a>Implantar um contêiner do ASP.NET em um registro de contêiner usando o Visual Studio

## <a name="overview"></a>Visão geral

O Docker é um mecanismo de contêiner leve, semelhante em alguns pontos a uma máquina virtual, que você pode usar para hospedar aplicativos e serviços.
Este tutorial orienta sobre o uso do Visual Studio para publicar o aplicativo em contêiner em um [Registro de Contêiner do Azure](https://azure.microsoft.com/services/container-registry).

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/dotnet/?utm_source=acr-publish-doc&utm_medium=docs&utm_campaign=docs) antes de começar.

## <a name="prerequisites"></a>Pré-requisitos

Para concluir este tutorial:

::: moniker range="vs-2017"
* Instale a versão mais recente do [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download)com a carga de trabalho "ASP.net e Web Development"
::: moniker-end
::: moniker range=">=vs-2019"
* Instale a versão mais recente do [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) com a carga de trabalho "ASP.net e Web Development"
::: moniker-end
* Instalar [Docker for Windows](https://docs.docker.com/docker-for-windows/install/)

## <a name="create-an-aspnet-core-web-app"></a>Criar um aplicativo Web ASP.NET Core
As etapas a seguir guiam você na criação de um aplicativo básico ASP.NET Core que será usado neste tutorial. Se você já tiver um projeto, poderá ignorar esta seção.

::: moniker range="vs-2017"
[!INCLUDE [create-aspnet5-app](../azure/includes/create-aspnet5-app.md)]
::: moniker-end
::: moniker range=">=vs-2019"
[!INCLUDE [create-aspnet5-app](../azure/includes/vs-2019/create-aspnet5-app-2019.md)]
::: moniker-end

## <a name="publish-your-container-to-azure-container-registry"></a>Publicar o contêiner no Registro de Contêiner do Azure
1. Clique com o botão direito no projeto em **Gerenciador de Soluções** e escolha **Publicar**.
2. Na caixa de diálogo de destino de publicação, selecione a guia **Registro de Contêiner**.
3. Escolha **Novo Registro de Contêiner do Azure** e clique em **Publicar**.
4. Preencha os valores desejados em **Criar um novo Registro de Contêiner do Azure**.

    | Configuração      | Valor sugerido  | Descrição                                |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Prefixo DNS** | Nome globalmente exclusivo | Nome que identifica exclusivamente o registro de contêiner. |
    | **Assinatura** | Escolha sua assinatura | A assinatura do Azure a utilizar. |
    | **[Grupo de Recursos](/azure/azure-resource-manager/resource-group-overview)** | myResourceGroup |  Nome do grupo de recursos no qual criar o registro de contêiner. Escolha **Novo** para criar um novo grupo de recursos.|
    | **[SKU](/azure/container-registry/container-registry-skus)** | Standard | Camada de serviço do registro de contêiner  |
    | **Localização do Registro** | Um local próximo | Escolha um Local em uma [região](https://azure.microsoft.com/regions/) próxima a você ou perto de outros serviços que usarão o registro de contêiner. |

    ![Caixa de diálogo Criar um Registro de Contêiner do Azure do Visual Studio](media/hosting-web-apps-in-docker/vs-acr-provisioning-dialog.png)

5. Clique em **Criar**

Agora, é possível extrair o contêiner do registro para qualquer host capaz de executar imagens do Docker, por exemplo [Instâncias de Contêiner do Azure](/azure/container-instances/container-instances-tutorial-deploy-app).

## <a name="see-also"></a>Veja também

[Início rápido: implantar uma instância de contêiner no Azure usando o CLI do Azure](/azure/container-instances/container-instances-quickstart)
