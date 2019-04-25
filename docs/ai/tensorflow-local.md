---
title: Treinar um modelo do TensorFlow no local
description: Executar um modelo TensorFlow localmente nas Ferramentas de IA para Visual Studio
keywords: ia, visual studio, tensorflow, local
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: quickstart
ms.devlang: python
ms.workload:
- multiple
ms.openlocfilehash: 26668247bf993da3eb3f2803abaf9288e566ffee
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62555447"
---
# <a name="train-a-tensorflow-model-locally"></a>Treinar um modelo do TensorFlow no local

Neste guia de início rápido, treinaremos um modelo do TensorFlow com o conjunto de dados [MNIST](http://yann.lecun.com/exdb/mnist/) localmente nas Ferramentas do Visual Studio para IA.

O banco de dados MNIST tem um conjunto de treinamento de 60 mil exemplos e um conjunto de testes de 10 mil exemplos de dígitos manuscritos.

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar, confira se os itens a seguir estão instalados:

### <a name="google-tensorflow"></a>Google TensorFlow

Em um terminal, execute o seguinte comando:

```cmd
C:\>pip.exe install tensorflow
```

### <a name="numpy-and-scipy"></a>NumPy e SciPy
Instale o [NumPy](https://www.lfd.uci.edu/~gohlke/pythonlibs/#numpy) e o [SciPy](https://www.lfd.uci.edu/~gohlke/pythonlibs/#scipy).

### <a name="download-sample-code"></a>Baixar o código de exemplo
Baixe este [Repositório GitHub](https://github.com/Microsoft/samples-for-ai) que contém exemplos de como começar a trabalhar com aprendizagem profunda no TensorFlow, CNTK, Theano e muito mais.

## <a name="open-solution-and-train-model"></a>Abrir a solução e treinar o modelo

- Inicie o Visual Studio e selecione **Arquivo > Abrir > Projeto/Solução**.

- Selecione a pasta **Exemplos do TensorFlow** no repositório de exemplos baixada e abra o arquivo **TensorflowExamples.sln**.

   ![Abrir o projeto](media/tensorflow-local/open-project.png)

   ![Abrir a solução](media/tensorflow-local/open-solution.png)

- Localize o projeto MNIST no **Gerenciador de Soluções**, clique nele com o botão direito do mouse e selecione **Definir como Projeto de Inicialização**.

- Clique em **Iniciar**.

- A saída é impressa no console.

   ![Exemplo de saída do console](media/tensorflow-local/console-output.png)

> [!div class="nextstepaction"]
> [Treinar um modelo do TensorFlow na nuvem](tensorflow-vm.md)