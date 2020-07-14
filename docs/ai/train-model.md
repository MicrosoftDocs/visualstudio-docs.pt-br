---
title: Enviar um trabalho para treinamento de modelo na IA do Lote do Azure
description: treinar nuvem modelo
keywords: ia, visual studio, modelo de treinamento, nuvem
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- azure
ms.openlocfilehash: 4d705cbff1ce4e25892dfc5df896418e6d58b632
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371645"
---
# <a name="train-ai-models-in-azure-batch-ai"></a>Treinar modelos de IA no Lote do Azure AI

A IA do Lote é um serviço gerenciado que permite que os pesquisadores de IA e cientistas de dados treinem IA e outros modelos de aprendizado de máquina em clusters de máquinas virtuais do Azure, incluindo VMs com suporte de GPU. Descreva os requisitos do seu trabalho, onde encontrar as entradas e armazenar as saídas, e a IA do Lote cuida do resto. [Saiba mais sobre a IA do Lote do Azure](/azure/batch-ai/overview)

Ela está integrada às Ferramentas do Visual Studio para IA, assim, é possível aumentar de forma dinâmica modelos de treinamento no Azure.  Depois de [instalar as Ferramentas do Visual Studio para IA](installation.md), é fácil criar um novo projeto Python usando receitas predefinidas na galeria de exemplos do Azure Machine Learning.

1. Inicie o Visual Studio. Abra o **Gerenciador de Servidores** abrindo o menu **Ferramentas de IA** e escolhendo **Selecionar Cluster**

    ![Seletor de cluster](media/train-model/select-cluster.png)

2. Expanda **Ferramentas de IA**. Todos os recursos do IA do Lote serão detectados automaticamente e exibidos no Gerenciador de Servidores.

    ![Galeria de exemplos](media/train-model/batchai.png)

3. Selecione **Exibir > Team Explorer...** para abrir a janela do **Team Explorer**, em que é possível se conectar ao GitHub ou ao Azure DevOps ou clonar um repositório.

    ![Janela do Team Explorer mostrando o Azure DevOps, o GitHub e a clonagem de um repositório](media/train-model/team-explorer-devops.png)

4. No campo de URL em **Repositórios Git Locais**, insira `https://github.com/Microsoft/samples-for-ai`, insira uma pasta para os arquivos clonados e selecione **Clonar**.

    > [!Tip]
    > A pasta especificada no Team Explorer é a pasta específica para receber os arquivos clonados. Ao contrário do comando `git clone`, criar um clone no Team Explorer não cria automaticamente uma subpasta com o nome do repositório.

5. Quando a clonagem for concluída, clique em **Arquivo > Abrir Solução > Projeto/Solução**

    ![Galeria de exemplos](media/train-model/open-solution.png)

6. Abra **samples-for-ai\TensorFlowExamples\TensorFlowExamples.sln** no diretório em que o repositório foi clonado

    ![Galeria de exemplos](media/train-model/tensorflowexamples.png)

7. Defina o projeto do MNIST como o **Projeto de Inicialização**

    ![Galeria de exemplos](media/train-model/mnist-startup.png)

8. <strong>Clique com o botão direito do mouse no **projeto do MNIST e clique em** **Enviar Trabalho**</strong>

    ![Galeria de exemplos](media/train-model/submit-job.png)
9. Selecione o cluster da **IA do Lote do Azure** e, depois, clique em **Importar**. Selecione o arquivo `AzureBatchAI_TF_MNIST.json` para preencher rapidamente alguns valores padrão, como qual imagem do Docker usar. Então clique em **Enviar**

    ![Galeria de exemplos](media/train-model/submit-batch.png)
