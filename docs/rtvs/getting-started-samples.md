---
title: Projetos de exemplo em R
description: Um índice de uma coleção de exemplos para começar a usar R e Visual Studio.
ms.date: 01/24/2018
ms.prod: visual-studio-dev15
ms.technology: vs-rtvs
ms.topic: conceptual
author: kraigb
ms.author: kraigb
manager: douge
ms.workload:
- data-science
ms.openlocfilehash: adb26b3cf6097d830c899ef4ef251d2066b81a38
ms.sourcegitcommit: f685fa5e2df9dc307bf1230dd9dc3288aaa408b5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36235180"
---
# <a name="r-tools-for-visual-studio-sample-projects"></a>Projetos de exemplo das Ferramentas do R para Visual Studio

Essa coleção de exemplos ajuda você a começar a usar o R, as RTVS (Ferramentas do R para Visual Studio) e o Microsoft Machine Learning Server:

1. Baixe o [arquivo zip de exemplo](https://github.com/Microsoft/RTVS-docs/archive/master.zip) e extraia em uma pasta da sua escolha.
1. Abra `examples/Examples.sln` para ver duas pastas do projeto:

    - *A First Look at R* (Uma introdução ao R) fornece uma introdução fácil para principiantes em R.
    - *MRS and Machine Learning* fornece exemplos de como usar o R e o Microsoft Machine Learning Server para aprendizado de máquina.

## <a name="a-first-look-at-r"></a>A First Look at R (Uma introdução ao R)

Este exemplo fornece uma introdução detalhada ao R por meio de comentários extensos nos dois arquivos de origem. Para a melhor experiência, posicione o cursor na parte superior do arquivo e pressione Ctrl+Enter para enviar o código linha-por-linha para a janela **R Interativo**. (As linhas que instalam pacotes devem levar um ou dois minutos para serem concluídas.)

- `1-Getting Started with R.R` aborda vários conceitos básicos do R incluindo o uso de pacotes, carregamento e análise de dados e criação de gráficos.

    ![Exemplo de saída de 1-Getting Started with R.R (1 – Introdução ao R.R)](media/samples-getting-started-output.png)

- `2-Introduction to ggplot2.R` apresenta o pacote gráfico ggplot2 conhecido por seus gráficos atraentes e sua sintaxe simples. Este exemplo visualiza dados de terremoto de Fiji.

    ![Exemplo de saída de 2-Introduction to ggplot2.R (2 – Introdução ao ggplot2.R)](media/samples-ggplot-output.png)

## <a name="microsoft-machine-learning-server-and-machine-learning"></a>Microsoft Machine Learning Server e aprendizado de máquina

Esta coleção de exemplos mostra como usar R para criar modelos de aprendizado de máquina e aproveitar o [Microsoft Machine Learning Server](/machine-learning-server/what-is-machine-learning-server).

Como em todos os exemplos, abra o arquivo, coloque o cursor na parte superior e, em seguida, percorra o código, linha por linha, com **Ctrl**+**Enter**. Os arquivos markdown em cada pasta também contêm detalhes adicionais.

- `Benchmarks` executa diversos cálculos de álgebra linear intensos paralelos para mostrar os ganhos de desempenho possíveis pelo uso do Microsoft R Open e da Intel MKL (Math Kernel Library). Com os dados simulados, os parâmetros de comparação comparam especificamente os cálculos de matriz em um thread versus dois.

    ![Gráfico de parâmetro de comparação de exemplo](media/samples-mro-benchmark-plot.png)

- `Bike_Rental_Estimation_with_MRS` cria um modelo de previsão de demanda para locações de bicicletas com base em um conjunto de dados histórico, usando o Microsoft ML Server. 

- `Data_Exploration` contém três scripts:

  - `Import Data from URL.R` mostra como carregar um arquivo de dados identificado por URL no R.
  - `Import Data from URL to xdf.R` mostra como carregar um arquivo de dados identificado por URL no Microsoft ML Server como um xdf.
  - `Using ggplot2.R` é uma extensão do exemplo `A First Look at R/2-Introduction to ggplot2.R`, fazendo um tour mais amplo da funcionalidade do ggplot2, incluindo a criação de gráficos 3D interativos.

      ![Exemplo de saída usando o ggplot2.R](media/samples-3d-interactive.png)

- `Datasets` contém três arquivos *.csv* usados por outros exemplos
- `Flight_Delays_Prediction_with_R` e `Flight_Delays_Prediction_with_MRS` mostram como prever atrasos de voo usando R, aprendizado de máquina e desempenho e dados meteorológicos pontuais históricos. 
- `Machine learning` contém três exemplos de aprendizado para prever os atrasos de voo, preços de habitação e locações de bicicleta. Juntos, esses exemplos demonstram a aplicação do R e do Microsoft ML Server a problemas reais. Eles também mostram como usar vários modelos de aprendizado de máquina populares e implantá-los como um serviço Web do Azure usando um espaço de trabalho do [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/).

- `R_MRO_MRS_Comparison` é uma comparação de seis partes que mostra as semelhanças e as diferenças entre R, Microsoft R Open e Microsoft ML Server em relação a comandos, sintaxe, constructos e desempenho.

## <a name="whats-special-about-microsoft-r-open-and-microsoft-ml-server"></a>O que o Microsoft R Open e o Microsoft ML Server têm de especial?

O [Microsoft R Open](http://aka.ms/rtvs-r-open), a distribuição do R da Microsoft, é diferente do [CRAN R](https://cran.r-project.org/) de duas maneiras importantes:

1. [Melhor desempenho de computação](https://mran.revolutionanalytics.com/rro/#intelmkl1) quando usado com as [Intel Math Kernel Libraries](https://software.intel.com/intel-mkl). As bibliotecas estão disponíveis como um download gratuito da Microsoft para uso com o Microsoft R Open.

1. O [Kit de ferramentas do R reproduzível](https://mran.revolutionanalytics.com/rro/#reproducibility) garante que as bibliotecas usadas para criar o programa R estejam sempre disponíveis para outras pessoas que deseja reproduzir seu trabalho.

O [Microsoft ML Server (MLS)](/machine-learning-server/what-is-machine-learning-server) é uma extensão do R que permite lidar com mais dados e com mais rapidez. Ele oferece ao R dois recursos avançados:

1. Conjuntos de dados maiores sem limitações de RAM. O ML Server pode processar dados fora da memória de uma variedade de fontes incluindo clusters, bancos de dados e data warehouses Hadoop.

1. Processamento paralelo, de vários núcleos. O MLS consegue distribuir a computação com eficiência entre todos os recursos computacionais que ele tem disponíveis. Em sua estação de trabalho pessoal ou em um cluster remoto, o MLS obtém respostas com mais rapidez.

A comparação a seguir mostra que o MLS e MRO com MKL têm um desempenho de computação significativamente melhor em relação a certos cálculos de matriz do que o R e o MRO sem MKL. São usados dados simulados no cálculo:

![Comparando MLS e MRO com MKL ao R e o MRO sem MKL](media/samples-speed-comparison.png)

Para obter uma comparação técnica do R com o MRO e MLS, confira a [discussão detalhada de Lixun Zhang](http://htmlpreview.github.io/?https://github.com/lixzhang/R-MRO-MRS/blob/master/Introduction_to_MRO_and_MRS.html) sobre o assunto.

A figura a seguir compara o tempo decorrido em segundos usado na criação de modelos de regressão logística para prever atrasos de voos maiores de 15 minutos.  O tempo decorrido usado em CRAN R aumenta drasticamente quando um pequeno número de linhas é aumentado, enquanto o MRS aumenta apenas cerca de duas vezes. Para obter detalhes sobre esse parâmetro de comparação, confira o exemplo *Benchmarks/rxGlm_benchmark.R*.

![Parâmetro de comparação rxGlm](media/samples-rxGLM-benchmark.png)
