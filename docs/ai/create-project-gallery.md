---
title: Criar um projeto
description: Criar um projeto usando um exemplo da galeria do Azure Machine Learning
keywords: ia, visual studio, azure machine learning
author: jillre
ms.author: jillfra
manager: jillfra
monikerRange: vs-2017
ms.date: 11/13/2017
ms.topic: how-to
ms.workload:
- multiple
ms.openlocfilehash: 4bcc1932bad5b34d9695257feb163654f6b99514
ms.sourcegitcommit: 48e93538f1e352fc1f972b642bb5fcce2f6834a2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85371619"
---
# <a name="create-an-ai-project-from-the-azure-machine-learning-gallery-in-visual-studio"></a>Criar um projeto de IA da galeria do Azure Machine Learning no Visual Studio

O Azure Machine Learning está integrado com as Ferramentas do Visual Studio para IA. É possível usá-lo para enviar trabalhos de aprendizado de máquina a destinos de computação remotos, como as máquinas virtuais do Azure, clusters Spark e muito mais. 

Depois de [instalar as Ferramentas do Visual Studio para IA](installation.md), é fácil criar um novo projeto Python usando receitas predefinidas na galeria de exemplos do Azure Machine Learning.

> [!NOTE]
> O Azure Machine Learning Workbench deve estar instalado. 

1. Inicie o Visual Studio. Abra o **Gerenciador de Servidores** abrindo o menu **Ferramentas de IA** e escolhendo **Selecionar Cluster**

    ![Seletor de cluster](media/create-project-gallery/select-cluster.png)

2. Entre na sua assinatura do Azure Machine Learning clicando com o botão direito do mouse no nó do **Azure Machine Learning** no Gerenciador de Servidores e, em seguida, selecione **Logon** e siga as instruções.

    ![login](media/create-project-gallery/azureml-login.png)

3. Selecione **Ferramentas de IA > Galeria de exemplos do Azure Machine Learning**.

    ![Galeria de exemplos](media/create-project-gallery/gallery.png)

4. Para este início rápido, selecione o exemplo "**MNIST usando TensorFlow**" e clique em **Instalar**. Forneça o seguinte:

   - **Grupo de Recursos**: grupo de recursos do Azure em que os metadados serão armazenados
   - **Conta**: conta de experimentação do Azure Machine Learning
   - **Workspace**: Workspace do Azure Machine Learning
   - **Tipo de Projeto**: a estrutura de aprendizado de máquina. Nesse caso, escolha o **TensorFlow**
   - **Adicionar à Solução**: determina se é necessário adicionar à sua solução do Visual Studio atual ou uma criar e abrir uma nova solução
   - **Caminho do Projeto**: local em que o código será salvo
   - **Nome do Projeto**: tipo **TensorFlowMNIST**

   ![Projeto resultante ao usar o modelo de aplicativo do Python](media/create-project-gallery/new-AzureSampleProject.png)

5. O Visual Studio cria o arquivo de projeto (um arquivo `.pyproj` no disco) junto com outros arquivos definidos no exemplo. Como o modelo "MNIST", o projeto contém vários arquivos.

    ![mnist](media/create-project-gallery/azml-mnist.png)

6. Envie o trabalho ao Azure Machine Learning.

    ![mnist](media/create-project-gallery/submit-azml.png)

7. Execute em um contêiner do Docker ou no seu computador local

    ![mnist](media/create-project-gallery/azml-local.png)
