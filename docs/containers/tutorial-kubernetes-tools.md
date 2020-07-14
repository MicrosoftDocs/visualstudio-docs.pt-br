---
title: Tutorial de ferramentas de kubernetes | Microsoft Docs
ms.date: 06/08/2018
ms.topic: tutorial
author: ghogen
ms.author: ghogen
manager: jillfra
ms.technology: vs-azure
ms.workload:
- azure
ms.openlocfilehash: 02a672321a11889d88a8af3305e64a66fe779080
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283184"
---
# <a name="get-started-with-visual-studio-kubernetes-tools"></a>Introdução às ferramentas de kubernetes do Visual Studio

As ferramentas de kubernetes do Visual Studio ajudam a simplificar o desenvolvimento de aplicativos em contêineres direcionados a kubernetes. O Visual Studio pode criar automaticamente os arquivos de configuração como código necessários para dar suporte à implantação do kubernetes, como gráficos Dockerfiles e Helm. Você pode depurar seu código em um cluster do AKS (serviço de kubernetes do Azure) usando Azure Dev Spaces ou publicar diretamente em um cluster do AKS de dentro do Visual Studio.

Este tutorial aborda o uso do Visual Studio para adicionar suporte a kubernetes a um projeto e publicar no AKS. Se você estiver interessado principalmente em usar [Azure dev Spaces](/azure/dev-spaces/) para depurar e testar seu projeto em execução no AKs, poderá ir para o [tutorial de Azure dev Spaces](/azure/dev-spaces/get-started-netcore-visualstudio) em vez disso.

## <a name="prerequisites"></a>Pré-requisitos

Para aproveitar essa nova funcionalidade, você precisará de:

::: moniker range="vs-2017"
- A versão mais recente do [Visual Studio 2017](https://visualstudio.microsoft.com/vs/older-downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=vs+2017+download) com a ASP.net e a carga de trabalho de *desenvolvimento Web* .
- O [kubernetes Tools for Visual Studio](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vs-tools-for-kubernetes), disponível como um download separado.
::: moniker-end
::: moniker range="vs-2019"
- [Visual Studio 2019](https://visualstudio.microsoft.com/downloads) com a carga de trabalho de *desenvolvimento Web e do ASP.NET*.
::: moniker-end
- [Docker desktop](https://store.docker.com/editions/community/docker-ce-desktop-windows) instalado em sua estação de trabalho de desenvolvimento (ou seja, onde você executa o Visual Studio), se você quiser criar imagens do Docker, depure os contêineres do Docker em execução localmente ou publique em AKs. (O Docker *não* é necessário para criar e depurar contêineres do Docker no AKS usando Azure dev Spaces.)
::: moniker range="vs-2017"
- Se você quiser publicar no AKS do Visual Studio (*não* é necessário para a depuração no AKS usando Azure dev Spaces):

    1. As [ferramentas de publicação do AKS](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vs-tools-for-kubernetes), disponíveis como um download separado.

    1. Um cluster do Serviço de Kubernetes do Azure. Para obter mais informações, consulte [criando um cluster AKs](/azure/aks/kubernetes-walkthrough-portal#create-an-aks-cluster). Certifique [-se de conectar-se ao cluster](/azure/aks/kubernetes-walkthrough#connect-to-the-cluster) de sua estação de trabalho de desenvolvimento.

    1. Helm CLI instalada em sua estação de trabalho de desenvolvimento. Para obter mais informações, consulte [instalando o Helm](https://github.com/helm/helm-www/blob/master/content/en/docs/helm/helm_install.md).

    1. Helm configurado em seu cluster AKS usando o `helm init` comando. Para obter mais informações sobre como fazer isso, consulte [como configurar o Helm](/azure/aks/kubernetes-helm#configure-helm).
::: moniker-end

## <a name="create-a-new-kubernetes-project"></a>Criar um novo projeto kubernetes

::: moniker range="vs-2017"

Depois de instalar as ferramentas apropriadas, inicie o Visual Studio e crie um novo projeto. Em **nuvem**, escolha o **aplicativo de contêiner para** o tipo de projeto kubernetes. Selecione este tipo de projeto e escolha **OK**.

![Captura de tela da criação de um novo projeto de aplicativo kubernetes](media/tutorial-kubernetes-tools/k8s-tools-new-k8s-app.png)

::: moniker-end
::: moniker range=">= vs-2019"

Na janela iniciar do Visual Studio, procure *kubernetes*e escolha o **aplicativo de contêiner para kubernetes**.

![Captura de tela da criação de um novo projeto de aplicativo kubernetes](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-new-k8s-app1.png)

Forneça o nome do projeto.

![Captura de tela da criação de um novo projeto de aplicativo kubernetes](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-new-k8s-app2.png)

::: moniker-end

Em seguida, você pode escolher qual tipo de aplicativo Web ASP.NET Core criar. Escolha **Aplicativo Web**. A opção **habilitar suporte do Docker** não aparecerá nesta caixa de diálogo.  O suporte ao Docker é habilitado por padrão para um aplicativo de contêiner para kubernetes.

::: moniker range="vs-2017"

![Captura de tela da seleção do aplicativo Web](media/tutorial-kubernetes-tools/k8s-tools-web-app-selection-screen.png)

::: moniker-end
::: moniker range=">=vs-2019"

![Captura de tela da seleção do aplicativo Web](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-web-app-selection-screen-2019.png)

::: moniker-end

## <a name="add-kubernetes-support-to-an-existing-project"></a>Adicionar suporte a kubernetes a um projeto existente

Como alternativa, você pode adicionar suporte a kubernetes a um projeto de aplicativo Web ASP.NET Core existente. Para fazer isso, clique com o botão direito do mouse no projeto e escolha **Adicionar**  >  **suporte ao orquestrador de contêiner**.

::: moniker range="vs-2017"

![Captura de tela do item de menu Adicionar orquestrador de contêiner](media/tutorial-kubernetes-tools/k8s-tools-add-container-orchestrator.png)

::: moniker-end
::: moniker range=">=vs-2019"

![Captura de tela do item de menu Adicionar orquestrador de contêiner](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-add-container-orchestrator-2019.png)

::: moniker-end

Na caixa de diálogo, selecione **kubernetes/Helm** e escolha **OK**.

![Captura de tela da caixa de diálogo Adicionar orquestrador de contêineres](media/tutorial-kubernetes-tools/k8s-tools-add-container-orchestrator-dialog-box.PNG)

## <a name="what-visual-studio-creates-for-you"></a>O que o Visual Studio cria para você

Depois de criar um novo **aplicativo de contêiner para** o projeto kubernetes ou adicionar suporte de orquestrador de contêiner kubernetes a um projeto existente, você verá alguns arquivos adicionais em seu projeto que facilitam a implantação no kubernetes.

::: moniker range="vs-2017"

![Captura de tela de Gerenciador de Soluções depois de adicionar suporte ao orquestrador de contêiner](media/tutorial-kubernetes-tools/k8s-tools-solution-explorer.png)

::: moniker-end
::: moniker range="vs-2019"

![Captura de tela de Gerenciador de Soluções depois de adicionar suporte ao orquestrador de contêiner](media/tutorial-kubernetes-tools/vs-2019/k8s-tools-solution-explorer-2019.png)

::: moniker-end

Os arquivos adicionados são:

- um Dockerfile, que permite que você gere uma imagem de contêiner do Docker que hospeda esse aplicativo Web. Como você verá, as ferramentas do Visual Studio aproveitam esse Dockerfile ao depurar e implantar no kubernetes. Se você preferir trabalhar diretamente com a imagem do Docker, clique com o botão direito do mouse no Dockerfile e escolha **criar imagem do Docker**.

   ![Captura de tela da opção criar imagem do Docker](media/tutorial-kubernetes-tools/k8s-tools-build-docker-image.png)

- um gráfico do Helm e uma pasta de *gráficos* . Esses arquivos YAML compõem o gráfico do Helm para o aplicativo, que pode ser usado para implantá-lo no kubernetes. Para obter mais informações sobre o Helm, consulte [https://www.helm.sh](https://www.helm.sh) .

- *azds.yaml*. Isso contém configurações para Azure Dev Spaces, que fornece uma experiência de depuração rápida e iterativa no serviço kubernetes do Azure. Para obter mais informações, consulte [a documentação do Azure dev Spaces](/azure/dev-spaces/azure-dev-spaces).

::: moniker range="vs-2017"

## <a name="publish-to-azure-kubernetes-service-aks"></a>Publicar no serviço kubernetes do Azure (AKS)

Com todos esses arquivos em vigor, você pode usar o IDE do Visual Studio para escrever e depurar o código do aplicativo, exatamente como sempre tem. Você também pode usar [Azure dev Spaces](/azure/dev-spaces/) para executar rapidamente e depurar seu código em execução em um cluster AKs. Para obter mais informações, consulte o [tutorial de Azure dev Spaces](/azure/dev-spaces/get-started-netcore-visualstudio)

Depois que o código estiver sendo executado da maneira desejada, você poderá publicar diretamente do Visual Studio em um cluster AKS.

Para fazer isso, primeiro você precisa verificar se instalou tudo conforme descrito na seção [pré-requisitos](#prerequisites) sob o item para publicar no AKs e executar todas as etapas de linha de comando fornecidas nos links. Em seguida, configure um perfil de publicação que publique sua imagem de contêiner no ACR (registro de contêiner do Azure). Em seguida, AKS pode extrair a imagem de contêiner do ACR e implantá-la no cluster.

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em seu *projeto* e escolha **publicar**.

   ![Captura de tela do item de menu publicar](media/tutorial-kubernetes-tools/k8s-tools-publish-project.png)

2. Na tela **publicar** , escolha **registro de contêiner** como o destino de publicação e siga os prompts para selecionar o registro de contêiner. Se você ainda não tiver um registro de contêiner, escolha **criar novo registro de contêiner do Azure** para criar um do Visual Studio. Para obter mais informações, consulte [publicar seu contêiner no registro de contêiner do Azure](hosting-web-apps-in-docker.md).

   ![Captura de tela de escolher um destino de publicação](media/tutorial-kubernetes-tools/k8s-tools-publish-to-acr.png)

3. De volta ao Gerenciador de Soluções, clique com o botão direito do mouse em sua *solução* e clique em **publicar no Azure AKs**.

   ![Captura de tela do item de menu publicar no Azure AKS](media/tutorial-kubernetes-tools/k8s-tools-publish-solution.png)

4. Escolha sua assinatura e o cluster AKS, juntamente com o perfil de publicação ACR que você acabou de criar. Em seguida, clique em **OK**.

   ![Captura de tela de publicar no AKS Screen](media/tutorial-kubernetes-tools/k8s-tools-publish-to-aks.png)

   Isso levará você à tela **publicar no Azure AKs** .

5. Escolha o link **Configurar Helm** para atualizar a linha de comando usada para instalar os gráficos do Helm no servidor.

   ![Captura de tela do link configurar Helm](media/tutorial-kubernetes-tools/k8s-tools-configure-helm.png)

   A atualização da linha de comando será útil se houver argumentos de linha de comando personalizados que você deseja especificar, como um contexto kubernetes diferente ou um nome de gráfico.

   ![Captura de tela de configuração do Helm](media/tutorial-kubernetes-tools/k8s-tools-helm-configure-screen.png)

6. Quando você estiver pronto para implantar, clique no botão **publicar** para publicar seu aplicativo no AKs.

   ![Captura de tela de publicar no Azure AKS](media/tutorial-kubernetes-tools/k8s-tools-publish-screen.png)

::: moniker-end

Parabéns! Agora você pode usar todo o potencial do Visual Studio para todo o desenvolvimento de aplicativos kubernetes.

## <a name="next-steps"></a>Próximas etapas

Saiba mais sobre o desenvolvimento do kubernetes no Azure lendo a [documentação do AKS](/azure/aks).

Saiba mais sobre Azure Dev Spaces lendo a [documentação do Azure dev Spaces](/azure/dev-spaces/)
