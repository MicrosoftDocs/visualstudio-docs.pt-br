---
title: Analisar o uso de memória para objetos .NET | Microsoft Docs
ms.date: 12/9/2019
ms.topic: how-to
helpviewer_keywords:
- memory allocation, memory usage
author: Sagar-S-S
ms.author: sashe
manager: AndSter
ms.workload:
- multiple
ms.openlocfilehash: f7ec98f8d17465e95369eb6e2ecd88051f8daa59
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85330456"
---
# <a name="analyze-memory-usage-by-using-the-net-object-allocation-tool"></a>Analisar o uso de memória usando a ferramenta de alocação de objeto .NET

Você pode ver quanto memória seu aplicativo usa e quais caminhos de código alocam mais memória usando a ferramenta de alocação de objeto .NET.

Depois de executar a ferramenta, você pode ver os caminhos de execução da função em que os objetos estão sendo alocados. Em seguida, você pode rastrear de volta para a raiz da árvore de chamada que está ocupando a maior parte da memória.

## <a name="setup"></a>Instalação

1. Selecione **ALT + F2** para abrir o criador de perfil de desempenho no Visual Studio.

1. Marque a caixa de seleção **controle de alocação de objeto .net** .

   ![A ferramenta de acompanhamento de alocação de objeto dotnet selecionada](../profiling/media/dotnetalloctoolselected.png "A ferramenta de acompanhamento de alocação de objeto dotnet selecionada")

1. Selecione o botão **Iniciar** para executar a ferramenta.

1. Depois que a ferramenta começar a ser executada, percorra o cenário no qual você deseja criar o perfil em seu aplicativo. Em seguida, selecione **parar coleta** ou feche seu aplicativo para ver seus dados.

   ![Uma janela mostrando A coleção de parada](../profiling/media/stopcollectionlighttheme.png "Uma janela mostrando A coleção de parada")

1. Selecione a guia **alocação** . o conteúdo da janela semelhante à captura de tela a seguir é exibido.

   ![A guia alocação](../profiling/media/allocationview.png "A guia alocação")

Agora você pode analisar a alocação de memória dos objetos.

Durante a coleta, a ferramenta de rastreamento pode retardar o aplicativo de perfil. Se o desempenho da ferramenta de rastreamento ou do aplicativo for lento e se você não precisar controlar todos os objetos, poderá ajustar a taxa de amostragem. Para fazer isso, selecione o símbolo de engrenagem ao lado da ferramenta de rastreamento na página Resumo do criador de perfil.

![Configurações para a ferramenta de alocação dotnet](../profiling/media/dotnetallocsettings.png "Configurações para a ferramenta de alocação dotnet")

Ajuste a taxa de amostragem para a taxa desejada. Essa alteração ajuda a acelerar o desempenho do seu aplicativo durante a coleta e a análise.

![Uma taxa de amostragem ajustada](../profiling/media/adjustedsamplingratedotnetalloctool.png "Uma taxa de amostragem ajustada")

Para obter mais informações sobre como tornar a ferramenta mais eficiente, consulte [otimizando as configurações do criador de perfil](../profiling/optimize-profiler-settings.md).

## <a name="understand-your-data"></a>Entenda seus dados

![Um grafo para a ferramenta de alocação dotnet](../profiling/media/graphdotnetalloc.png "Um grafo para a ferramenta de alocação dotnet")

Na exibição gráfica anterior, o grafo superior mostra o número de objetos ao vivo em seu aplicativo. O gráfico **Delta do objeto** inferior mostra a alteração percentual de objetos de aplicativo. As barras vermelhas indicam quando houve a coleta de lixo.

![Um grafo filtrado do tempo de alocação dotnet](../profiling/media/graphdotnetalloctimefiltered.png "Um grafo filtrado do tempo de alocação dotnet")

Você pode filtrar os dados tabulares para exibir a atividade apenas para um intervalo de tempo especificado. Você também pode ampliar ou reduzir o grafo.

### <a name="allocation"></a>Alocação

![A exibição de alocação expandida](../profiling/media/allocationexpandedlight.png "A exibição de alocação expandida")

A exibição de **alocação** mostra o local dos objetos que estão Alocando memória e a quantidade de memória que esses objetos estão alocando.

- A coluna **tipo**   é uma lista de classes e estruturas que ocupam memória. Clique duas vezes em um tipo para exibir seu backtrace como uma árvore de chamada invertida. Somente na exibição de **alocação** , você pode ver os itens dentro da categoria selecionada que ocupam memória.

- A coluna **alocações**   mostra o número de objetos que ocupam memória dentro de um tipo ou função de alocação específico. Essa coluna aparece apenas nas exibições de **alocação**, **árvore de chamadas**e **funções**   .

- Os **bytes**   e as colunas de **tamanho médio (bytes)**   não aparecem por padrão. Para mostrá-los, clique com o botão direito do mouse na coluna **tipo**   ou **alocações**e   selecione as opções **bytes**   e **tamanho médio (bytes)**   para adicioná-los ao gráfico. 

   As duas colunas são semelhantes ao **total (alocações)** e à **própria (alocações)**, exceto pelo fato de que elas mostram a quantidade de memória ocupada em vez do número de objetos que ocupam memória. Essas colunas aparecem apenas na exibição de **alocação** .

- A coluna **nome do módulo**   mostra o módulo que contém a função ou o processo que está chamando.

Todas essas colunas são classificável. Para as colunas do **nome do módulo** e do **tipo** , você pode classificar itens em ordem alfabética nas ordens crescente ou decrescente. Para **alocações**, **bytes**   e **tamanho médio (bytes)**, você pode classificar itens aumentando ou diminuindo o valor numérico.

#### <a name="symbols"></a>Símbolos

Os seguintes símbolos aparecem nas guias **alocação**, **árvore de chamadas**e **funções** :

- ![O tipo de valor Symbol](../profiling/media/valuetypeicon.png "O símbolo de tipo de valor") -um tipo de valor como inteiro

- ![O símbolo de coleção de tipo de valor](../profiling/media/valuetypecollectionicon.png "O símbolo de coleção de tipo de valor") -uma coleção de tipo de valor como matriz de inteiros

- ![O tipo de referência Symbol](../profiling/media/referencetypeicon.png "O símbolo de tipo de referência") -um tipo de referência como cadeia de caracteres

- ![O símbolo de coleção de tipo de referência](../profiling/media/referencetypecollectionicon.png "O símbolo de coleção de tipo de referência") – uma coleção de tipo de referência como matriz de cadeias de caracteres

### <a name="call-tree"></a>Árvore de chamadas

![O modo de exibição de árvore de chamada](../profiling/media/calltreelight.png "O modo de exibição de árvore de chamada")

O modo de exibição de **árvore de chamadas**   mostra os caminhos de execução de função que contêm objetos que alocam muita memória.

- A coluna **nome da função**   mostra o processo ou o nome da função que contém objetos que alocam memória. A exibição é baseada no nível do nó que você está inspecionando.
- As colunas **total (alocações)** e **Tamanho total (bytes)**   mostram o número de objetos alocados e a quantidade de memória usada por uma função e todas as outras funções que ele chama.
- As colunas **auto (alocações)** e **autotamanho (bytes)** mostram o número de objetos alocados e a quantidade de memória usada por uma única função ou tipo de alocação selecionado.
- A coluna **tamanho médio (bytes)** mostra as mesmas informações que no modo de exibição **alocações** .
- A coluna **nome do módulo**   mostra o módulo que contém a função ou o processo que está chamando.

   ![Um Hot Path expandido](../profiling/media/hotpathlight.png "Um Hot Path expandido")

- O botão **expandir caminho quente** realça um caminho de execução de função que contém muitos objetos que estão Alocando memória. O algoritmo começa em um nó que você seleciona e realça o caminho da maioria das alocações, orientando você em sua investigação.
- O botão **Mostrar caminho quente** mostra ou oculta os símbolos de chama que indicam quais nós fazem parte do Hot Path.

### <a name="functions"></a>Funções

![A exibição de funções](../profiling/media/functionslight.png "A exibição de funções")

O modo de exibição de **funções** mostra processos, módulos e funções que estão Alocando memória.

- A coluna **nome** mostra processos como os nós de nível mais alto. Os processos abaixo são módulos e os módulos abaixo são funções.
- Essas colunas mostram as mesmas informações que fazem nas exibições de árvore de **alocação** e de **chamada** :

   - **Total (alocações)**
   - **Auto (alocações)**
   - **Tamanho total (bytes)**
   - **Autotamanho (bytes)**
   - **Tamanho médio (bytes)**

### <a name="collection"></a>Coleção

![O modo de exibição de coleção](../profiling/media/collectionlight.png "O modo de exibição de coleção")

O modo de exibição de **coleção** mostra quantos objetos foram coletados ou retidos durante a coleta de lixo. Essa exibição também mostra gráficos de pizza para visualizar objetos coletados e sobreviveram por tipo.

- A coluna **coletada** mostra o número de objetos coletados pelo coletor de lixo.
- A coluna **sobreviveram** mostra o número de objetos que sobreviveram após a execução do coletor de lixo.

### <a name="filtering-tools"></a>Ferramentas de filtragem

As exibições de **alocações**, **árvore de chamadas**e **funções** contêm as opções **Mostrar apenas meu código** e **Mostrar código nativo** e uma caixa de filtro.

- **Mostrar apenas meu código** recolhe sistemas, estruturas e outros códigos que não são de usuário em quadros **[código externo]** para que você possa se concentrar apenas em seu código. Para obter mais informações, consulte [depurar código do usuário com apenas meu código](../debugger/just-my-code.md).
- **Mostrar código nativo** mostra o código nativo dentro do destino da análise e pode incluir código não-usuário.
- Com a caixa de filtro, você pode filtrar a coluna **nome** ou **nome da função** com base no valor fornecido. Insira um valor de cadeia de caracteres na caixa. Em seguida, a tabela mostra apenas os tipos que contêm essa cadeia de caracteres.
