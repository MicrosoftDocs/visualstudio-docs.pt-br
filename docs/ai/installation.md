---
title: Instalar ferramentas de inteligência artificial
description: Descreve como instalar ferramentas de inteligência artificial do Visual Studio
keywords: ia, visual studio
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 11/13/2017
ms.topic: conceptual
ms.devlang: multiple
ms.service: multiple
ms.technology: vs-ai-tools
ms.workload:
- multiple
ms.openlocfilehash: 465443211d1a3f1aff8bfa63fa6cb8068b55980b
ms.sourcegitcommit: 551f13774e8bb0eb47cbd973745628a956e866aa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2018
ms.locfileid: "49459758"
---
# <a name="installation"></a>Instalação

As Ferramentas do Visual Studio para IA podem ser instaladas nos sistemas operacionais Windows de 64 bits.

## <a name="install-visual-studio-tools-for-ai"></a>Instalar o Visual Studio Tools for AI

Essa extensão funciona com o Visual Studio 2015 e o Visual Studio 2017, Community Edition ou versões posteriores.

Você pode fazer o download das ferramentas do [Visual Studio Marketplace](http://aka.ms/vstoolsforai) ou do Visual Studio:

1. Escolha **Ferramentas** > **Extensões e Atualizações**.

   ![Menu Extensões e Atualizações do Visual Studio](media/installation/extensions.png)

2. Na caixa de diálogo **Extensões e Atualizações**, selecione **Online** no lado esquerdo.
3. Na caixa de pesquisa no canto superior direito, digite ou insira "tools for ai".
4. Selecione **Visual Studio Tools for AI** nos resultados.
5. Clique em **Baixar**.

## <a name="prepare-your-local-machine"></a>Preparar seu computador local

Antes de começar a treinar os modelos de aprendizagem profunda em seu computador local, verifique se você tem os pré-requisitos aplicáveis instalados. Isso inclui garantir que você tenha os drivers e as bibliotecas mais recentes para sua GPU NVIDIA (se tiver uma). Verifique também se tem o Python e suas bibliotecas instalados, como NumPy e SciPy, bem como as estruturas de aprendizagem profunda corretas, como o CNTK (Microsoft Cognitive Toolkit), TensorFlow, Caffe2, MXNet, Keras, Theano, PyTorch e Chainer, que você planeja usar em seu projeto.

> [!NOTE]
> Nas subseções a seguir, a introdução aos software foi extraída de suas páginas iniciais.

### <a name="nvidia-gpu-driver"></a>Driver da GPU NVIDIA

As estruturas de aprendizagem profunda aproveitam-se da GPU NVIDIA para permitir que computadores aprendam com velocidade, precisão e escala, em direção à verdadeira inteligência artificial. Se o computador tem cartões GPU NVIDIA, clique [aqui](http://www.nvidia.com/Download/index.aspx) ou tente atualizar o sistema operacional para instalar o driver mais recente.

### <a name="cuda"></a>CUDA

A [CUDA](https://developer.nvidia.com/cuda-zone) é uma plataforma de computação paralela e um modelo de programação inventado pela NVIDIA. Ela aumenta drasticamente o desempenho de computação aproveitando a potência da GPU. Atualmente, o CUDA Toolkit 8.0 é exigido por estruturas de aprendizagem profunda.

Para instalar a CUDA

- Acesse este [site](https://developer.nvidia.com/cuda-80-ga2-download-archive), baixe a CUDA e instale-a.
- Não se esqueça de instalar as bibliotecas de tempo de execução CUDA e, em seguida, adicionar o caminho binário CUDA à variável de ambiente %PATH% ou $Path.
- No Windows, esse caminho é "C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\bin" por padrão.

![Instalar a CUDA no Windows](media/installation/install_cuda_win.png)

### <a name="cudnn"></a>cuDNN

A [cuDNN](https://developer.nvidia.com/cudnn) (CUDA Deep Neural Network) é a biblioteca de primitivos acelerada por GPU para redes neurais profundas da NVIDIA. A cuDNN v6 é exigida pelas estruturas de aprendizagem profunda mais recentes.

Para instalar a cuDNN:

- Visite [NVIDIA Developer](https://developer.nvidia.com/rdp/cudnn-download) (Desenvolvedor para NVIDIA) para baixar e instalar o pacote mais recente.
- Não se esqueça de adicionar o diretório que contém o binário cuDNN para a variável de ambiente %PATH% ou $Path.
- No Windows, copie cudnn64_6.dll para "C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v8.0\bin".

> [!NOTE]
> Estruturas de aprendizagem profunda mais antigas, como o CNTK 2.0 e o TensorFlow 1.2.1 precisam da cuDNN v5.1. No entanto, é possível instalar várias versões da cuDNN juntas.

### <a name="python"></a>Python

O Python tem sido a principal linguagem de programação para aplicativos de aprendizagem profunda. A versão de **64 bits** do Python é obrigatória e o [Python 3.5.4](https://www.python.org/downloads/release/python-354/) é recomendado para uma compatibilidade melhor.

### <a name="to-install-python-on-windows"></a>Para instalar o Python no Windows

- Sugerimos a instalação do inicializador de Python só para você, bem como a adição do Python à variável de ambiente %PATH%.
- Lembre-se de instalar o pip, que é o sistema de gerenciamento de pacotes para instalar e gerencial pacotes de software escritos em Python.

As estruturas de aprendizagem profunda dependem do pip para sua própria instalação.

![Instalar o Python no Windows](media/installation/install_python_win.png)

Em seguida, precisamos verificar se o Python 3.5 está instalado corretamente e atualizar o pip para a versão mais recente, executando os seguintes comandos em um terminal:

- **Windows**
    ```cmd
    C:\Users\test>python -V
    Python 3.5.4

    C:\Users\test>pip3.5 -V
    pip 9.0.1 from c:\users\test\appdata\local\programs\python\python35\lib\site-packages (python 3.5)

    C:\Users\test>python -m pip install -U pip
    ```

- **macOS**
    ```bash
    MyMac:~ test$ python3.5 -V
    Python 3.5.4

    MyMac:~ test$ pip3.5 -V
    pip 9.0.1 from /Library/Frameworks/Python.framework/Versions/3.5/lib/python3.5/site-packages (python 3.5)

    MyMac:~ test$ python3.5 -m pip install -U pip
    ```

### <a name="python-on-visual-studio"></a>Python no Visual Studio

O Python tem suporte completo no Visual Studio por meio de extensões.
Saiba mais sobre a instalação do [Python para Ferramentas do Visual Studio](../python/installing-python-support-in-visual-studio.md) para obter mais detalhes.

### <a name="numpy-and-scipy"></a>NumPy e SciPy

- O **NumPy** é um pacote de processamento de matriz de uso geral projetado para manipular de forma eficiente grandes matrizes multidimensionais de registros arbitrários, sem prejudicar demais a velocidade de matrizes multidimensionais pequenas.

- O **SciPy** (pronuncia-se "Sigh Pie" em inglês) é um software livre para matemática, ciências e engenharia, dependente do NumPy. Agora, a partir da versão 1.0.0, o SciPy tem um pacote predefinido oficial no formato wheel para o Windows.

Para instalar o NumPy e o SciPy, execute o seguinte comando em um terminal:

```bash
pip3.5 install -U numpy scipy
```

> [!NOTE]
> Esse comando atualiza o NumPy e o SciPy antigos ou não oficiais (por exemplo, pacotes de terceiros de http://www.lfd.uci.edu/~gohlke/pythonlibs/ para Windows) para as versões mais recentes.

### <a name="microsoft-cognitive-toolkit-cntk"></a>Microsoft Cognitive Toolkit (CNTK)

O [Microsoft Cognitive Toolkit](https://cntk.ai) é um kit de ferramentas unificado de aprendizagem profunda que descreve redes neurais como uma série de passos computacionais por meio de um gráfico direcionado. O CNTK tem suporte para as linguagens de programação Python e BrainScript.

> [!NOTE]
> Atualmente, não há suporte para macOS no CNTK.

Para instalar o pacote em Python no CNTK, veja [como instalar o CNTK](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="tensorflow"></a>TensorFlow

O [TensorFlow](https://www.tensorflow.org/) é uma biblioteca de software livre para computação numérica que usa grafos de fluxo de dados. Para saber mais detalhes sobre a instalação, clique [aqui](https://www.tensorflow.org/install/).

> [!NOTE]
> A partir da versão 1.2, o TensorFlow não terá mais suporte de GPU para macOS.

### <a name="caffe2"></a>Caffe2

O [Caffe2](https://caffe2.ai/) é uma estrutura de aprendizagem profunda leve, modular e escalonável. Baseado no Caffe original, o Caffe2 é projetado com expressão, velocidade e modularidade em mente.

Atualmente, não há um pacote wheel de Python predefinido para o Caffe2.

Clique [aqui](https://caffe2.ai/docs/getting-started.html) para compilar no código-fonte.

### <a name="mxnet"></a>MXNet

O [Apache MXNet (em encubação)](https://mxnet.incubator.apache.org/) é uma estrutura de aprendizagem profunda projetada para ser eficiente e flexível. Ele permite **misturar** [programação imperativa e simbólica](http://mxnet.io/architecture/index.html#deep-learning-system-design-concepts) a fim de maximizar a eficiência e a produtividade.

Para instalar o MXNet, execute o seguinte comando em um terminal:

- Com a GPU
    ```bash
    pip3.5 install mxnet-cu80==0.12.0
    ```
- Sem a GPU
    ```bash
    pip3.5 install mxnet==0.12.0
    ```

### <a name="keras"></a>Keras

A [Keras](https://keras.io/) é uma API de redes neurais de alto nível escrita em Python, que pode ser executada sobre o CNTK, o TensorFlow ou o Theano. Ela foi desenvolvida com foco em habilitar uma experimentação rápida. Conseguir passar da ideia para o resultado com o mínimo de atraso é fundamental para uma boa pesquisa.

Para instalar a Keras, execute o seguinte comando em um terminal:

```bash
pip3.5 install Keras==2.0.9
```

### <a name="theano"></a>Theano

O [Theano](http://deeplearning.net/software/theano/) é uma biblioteca em Python que permite definir, otimizar e avaliar de forma eficiente expressões matemáticas que envolvem matrizes multidimensionais.

Para instalar o Theano, execute o seguinte comando em um terminal:

```bash
pip3.5 install Theano==0.9.0
```

### <a name="pytorch"></a>PyTorch

O [PyTorch](http://pytorch.org/) é um pacote em Python que oferece dois recursos de alto nível:

- Computação por tensores (como o NumPy) com forte aceleração de GPU
- Redes Neurais Profundas criadas em um sistema autograd baseado em fita

Para instalar o PyTorch, execute o seguinte comando em um terminal:

- **Windows**
    - Ainda não há nenhum pacote indicador oficial. Você pode baixar um [pacote Anaconda PyTorch](https://anaconda.org/pytorch/repo?type=all) de terceiros.
    - Descompacte-o no diretório base, por exemplo, "C:\Users\test\pytorch".
    - Adicione "C:\Users\test\pytorch\Lib\site-packages" à variável de ambiente %PYTHONPATH%.

- **macOS**
    ```bash
    pip3.5 install http://download.pytorch.org/whl/torch-0.2.0.post3-cp35-cp35m-macosx_10_7_x86_64.whl
    ```
    > [!NOTE]
    > Os binários macOS não tem suporte para CUDA, instale da fonte se o CUDA for necessário

- **Linux**
    ```bash
    pip3.5 install http://download.pytorch.org/whl/cu80/torch-0.2.0.post3-cp35-cp35m-manylinux1_x86_64.whl
    ```
    > [!NOTE]
    > Este pacote único é compatível com GPU e CPU.

Por fim, instale o torchvision em não Windows:

```bash
pip3.5 install torchvision
```

### <a name="chainer"></a>Chainer

O [Chainer](https://chainer.org/) é uma estrutura de aprendizagem profunda baseada em Python que tem como foco a flexibilidade. Ele oferece APIs de diferenciação automática baseadas na **abordagem definida pela execução** (conhecida também como grafos computacionais dinâmicos), bem como as APIs de alto nível orientadas a objeto para criar e treinar redes neurais.

Para habilitar o suporte para CUDA, instale o [CuPy](https://github.com/cupy/cupy):

```bash
pip3.5 install cupy
```

> [!NOTE]
> No Windows, você precisa da versão 2015 do [Visual Studio](https://visualstudio.microsoft.com/) ou das [Ferramentas de Build do Microsoft Visual C++](https://visualstudio.microsoft.com/visual-cpp-build-tools/) para compilar o CuPy com o CUDA 8.0.

Para instalar o Chainer, execute o seguinte comando em um terminal:

```bash
pip3.5 install chainer==3.0.0
```