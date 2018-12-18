---
title: Executar um modelo do TensorFlow na nuvem
description: executar um modelo do tensorflow em uma vm de aprendizagem profunda do azure
keywords: ia, visual studio, máquina virtual de aprendizagem profunda
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: tutorial
ms.devlang: python
ms.service: multiple
ms.technology: vs-ai-tools
ms.workload:
- multiple
ms.openlocfilehash: 8c84fbb3001bffb93d6c06f383551c073461419b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49911326"
---
# <a name="train-a-tensorflow-model-in-the-cloud"></a>Treinar um modelo do TensorFlow na nuvem

Neste tutorial, treinaremos um modelo do TensorFlow usando um [conjunto de dados MNIST](http://yann.lecun.com/exdb/mnist/) em uma máquina virtual de [aprendizagem profunda](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview) do Azure.

O banco de dados MNIST tem um conjunto de treinamento de 60 mil exemplos e um conjunto de testes de 10 mil exemplos de dígitos manuscritos.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar, confira se os itens a seguir estão instalados e configurados:

### <a name="setup-azure-deep-learning-virtual-machine"></a>Configurar uma máquina virtual de aprendizagem profunda do Azure

> [!NOTE]
> Definir **tipo do sistema operacional** como Linux.

As instruções para configurar a máquina virtual de aprendizagem profunda podem ser encontradas [aqui](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/provision-deep-learning-dsvm).

### <a name="remove-comment-in-parens"></a>Remover o comentário entre parênteses

```bash
echo -e ". /etc/profile\n$(cat ~/.bashrc)" > ~/.bashrc
```

### <a name="download-sample-code"></a>Baixar o código de exemplo

Baixe este [Repositório GitHub](https://github.com/Microsoft/samples-for-ai) que contém exemplos de como começar a trabalhar com aprendizagem profunda no TensorFlow, CNTK, Theano e muito mais.

## <a name="open-project"></a>Abrir o projeto

- Inicie o Visual Studio e selecione **Arquivo > Abrir > Projeto/Solução**.

- Selecione a pasta **Exemplos do TensorFlow** no repositório de exemplos baixada e abra o arquivo **TensorflowExamples.sln**.

   ![Abrir o projeto](media/tensorflow-local/open-project.png)

   ![Abrir a solução](media/tensorflow-local/open-solution.png)

## <a name="add-azure-remote-vm"></a>Adicionar a VM remota do Azure

No Gerenciador de Servidores, clique com o botão direito do mouse no nó **Computadores Remotos** no nó Ferramentas de IA e selecione "Adicionar...". Insira o nome de exibição do computador remoto, o IP host, a porta SSH, o nome de usuário e a senha/arquivo de chave.

![Adicionar um novo computador remoto](media/tensorflow-vm/add-remote-vm.png)

## <a name="submit-job-to-azure-vm"></a>Enviar o trabalho para a VM do Azure
Clique com o botão direito do mouse no projeto MNIST no **Gerenciador de Soluções** e selecione **Enviar Trabalho**.

![Envio de trabalho para um computador remoto](media/tensorflow-vm/job-submission.png)

Na janela de envio:

- Na lista **Cluster a ser usado**, selecione o computador remoto (com o prefixo "rm:") ao qual enviar o trabalho.

- Insira um **Nome do trabalho**.

- Clique em **Enviar**.

## <a name="check-status-of-job"></a>Verificar o status do trabalho
Para ver o status e detalhes dos trabalhos, expanda a máquina virtual a que o trabalho foi enviado no **Gerenciador de Servidores**. Clique duas vezes em **Trabalhos**.

![Navegador do trabalho](media/tensorflow-vm/job-browser.png)

## <a name="clean-up-resources"></a>Limpar recursos

Interrompa a VM caso planeje usá-lo no futuro próximo. Se tiver terminado este tutorial, execute o seguinte comando para limpar seus recursos:

```azurecli-interactive
az group delete --name myResourceGroup
```
