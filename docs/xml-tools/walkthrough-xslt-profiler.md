---
title: 'Passo a passo: Profiler XSLT'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 87387c9a-2e89-4801-ad51-83740cd6ea25
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 14abf52e65a796325d4af8bd95f5434c105c3fa3
ms.sourcegitcommit: 0aafcfa08ef74f162af2e5079be77061d7885cac
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34693793"
---
# <a name="walkthrough-xslt-profiler"></a>Passo a passo: Profiler XSLT

O profiler XSLT criar relatórios de desempenho detalhados XSLT que a medida da ajuda, avalia, e problemas de desempenho relacionados de destino no código XSLT. O profiler XSLT inclui dicas úteis para XSL e otimizações de folha de estilos XSLT. Para aplicativos que requerem XSLT máximo desempenho, essa ferramenta pode ser essencial.

## <a name="prerequisites"></a>Pré-requisitos

Os procedimentos a instrução a seguir exigem que o Visual Studio e .NET Framework versão 4.0 ou posterior.

### <a name="create-the-performance-report"></a>Crie o relatório de desempenho

1.  Abrir um documento XSLT no Visual Studio.

2.  Clique no **perfil XSLT** opção está disponível no menu de XML.

3.  Fornecer um documento XML de entrada. Se um documento XML ele já não estiver aberto, você será solicitado para o arquivo.

4.  Inicia a análise, e uma barra de progresso exibem o progresso no editor.

5.  A saída XSLT são visíveis no painel de saída.

6.  Após extremidades de uma sessão de desempenho, verifique o relatório de desempenho. Os dados salvos em um relatório de desempenho permitem que você exiba e analisar o desempenho XSLT.

### <a name="get-all-the-available-views"></a>Obter todos os modos disponíveis

1.  Clique no **exibição atual** lista suspensa para obter todos os modos de exibição disponíveis.

2.  Selecione o **exibição de resumo** opção o **exibição atual** lista suspensa. Por padrão, um relatório de desempenho é exibido no **exibição de resumo**. Esta exibição é um ponto de partida para determinar problemas de desempenho com documentos XSLT. O **exibição de resumo** lista os pontos de dados a seguir:

    -   A maioria chamaram funções

    -   Funções com a maioria de trabalho individual

    -   Funções que usam o tempo os mais longa de executar

3.  Por padrão, há três colunas para cada ponto de dados: o nome da função, o número de chamadas o valor absoluto, e um valor percentual de função chamado para chamadas de função total. De cada dados point-in a **exibição de resumo**, você pode navegar para modos de exibição mais detalhados clicando nos pontos de dados de função.

4.  Selecione o **exibir função** opção o **exibição atual** lista suspensa. O **exibir função** lista funções chamadas durante a criação de perfil. Você pode classificar os dados em um nome de coluna. As colunas exibidas por padrão são:

    -   **Nome da Função**

    -   **Tempo Inclusivo Decorrido**

    -   **Tempo Exclusivo Decorrido**

    -   **Tempo Inclusivo do Aplicativo**

    -   **Tempo Exclusivo do Aplicativo**

    -   **Número de Chamadas**

5.  Todas as colunas de tempo são exibidas em valores absolutos e em porcentagens. O termo **exclusivo** refere-se ao tempo total de uma função de execução gasto exclusivos de tempo gasto por outras funções de chamada durante a execução dessa função.

6.  O termo **inclusiva** refere-se o tempo total gasto em execução, incluindo o tempo de execução de todas as funções de chamada e se qualquer uma dessas funções de chamada chamado outras funções.

### <a name="select-callercallee-view"></a>O modo de seleção do chamador/receptor

1.  Selecione **chamador/receptor** exibir no **exibição atual** lista suspensa.

2.  O **chamador/receptor** exibição tem três partes distintas:

    -   **Funções que chamaram**: todas as funções que chamaram uma função específica são listadas na parte superior do modo de exibição.

    -   **Função atual**: A função específica que foi chamada está listada na parte do meio da exibição.

    -   **Funções que foram chamadas pela** : todas as funções que foram chamadas pela função específica são listadas na parte inferior do modo de exibição.

3.  Se uma função chamada `SyncToNavigator` aparece na parte média de exibição, todas as funções que chamaram a função de `SyncToNavigator` aparecem na parte superior de exibição, e em todas as funções que foram chamados por `SyncToNavigator` aparecem na parte de fundo de exibição.

4.  Você pode alterar a função na parte média de exibição clicando duas vezes em algumas das funções listadas em duas outras partes de exibição. A exibição é atualizado para refletir automaticamente as alterações.

5.  Você também pode classificar os dados clicando em nomes de coluna.

### <a name="select-call-tree-view"></a>Selecione o modo de exibição de árvore de chamadas

1.  Selecione **exibição de árvore de chamadas** no **exibição atual** lista suspensa. Esta exibição é um modo de exibição de árvore de execução do programa.

2.  O **exibição de árvore de chamadas** mostra a raiz da árvore, como o nome do processo. As funções são os nós de árvore. Esta exibição permite que você fure em rastreamentos específicos de chamada e analise que os rastreamentos têm o maior impacto de desempenho. A exibição é semelhante a **exibição de pilha de chamadas** disponível durante a depuração. Além das colunas no **exibir função**, no **exibição de árvore de chamadas**, há uma coluna adicional para exibir o **nome do módulo**.

3.  Selecione **marcas** no **exibição atual** lista suspensa.

4.  Com o profiler de SLT, há marcas que aparece no fluxo da coleção de dados com um comentário associado. As marcas são locais no código que têm contadores. Quando você indica que o profiler XSLT para coletar contadores de desempenho XSLT, os contadores obtém como cada vez que uma dessas marcas é executado. Os dados são exibidos em uma tabela que contém o **ID de marca**, **nome da marca** (**Iniciar programa**, **programa final**) e o  **Carimbo de hora**. As marcas não são agregadas e aparecem em ordem cronológica no **exibição de marcas** do relatório de desempenho.

### <a name="select-modules-in-the-current-view"></a>Módulos selecionados na exibição atual

1.  Selecione **módulos** no **exibição atual** lista suspensa.

2.  Exibição de módulos é uma lista plana das funções agregadas para o nível de módulo. Expandir ou recolher o nome do módulo para exibir ou fechar a exibição de dados de desempenho do módulo. Você pode classificar os dados em um nome de coluna. Por padrão, há valores absolutos e números de porcentagem para **tempo inclusivo decorrido**, **tempo exclusivo decorrido**, **tempo inclusivo do aplicativo**, **Tempo exclusivo do aplicativo**, e **número de chamadas**.

3.  Selecione **processo** no **exibição atual** lista suspensa.

4.  O modo de exibição de processo exibe uma tabela que inclui o **ID do processo**, **nome do processo**, **hora de início**e o **hora de término**. Os dados podem ser classificados clicando em nomes de coluna.

## <a name="see-also"></a>Consulte também

- [Passo a passo: Usando a hierarquia XSLT](../xml-tools/walkthrough-using-xslt-hierarchy.md)