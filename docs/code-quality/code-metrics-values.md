---
title: Calcular métricas de código
ms.date: 11/02/2018
ms.topic: conceptual
helpviewer_keywords:
- code metrics [Visual Studio]
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8b1a9d109b833d17783beb39c5f34cf6b9ed3274
ms.sourcegitcommit: 60315ba949aca1ff06fe431dbcbcfb0fedc1e8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85292887"
---
# <a name="code-metrics-values"></a>Valores de métricas de código

A maior complexidade dos aplicativos de software modernos também aumenta a dificuldade de tornar o código confiável e passível de manutenção. As métricas de código são um conjunto de medidas de software que fornecem aos desenvolvedores uma visão melhor do código que estão desenvolvendo. Aproveitando as métricas de código, os desenvolvedores podem entender quais tipos e/ou métodos devem ser retrabalhados ou testados com mais detalhes. As equipes de desenvolvimento podem identificar possíveis riscos, compreender o estado atual de um projeto e acompanhar o progresso durante o desenvolvimento de software.

Os desenvolvedores podem usar o Visual Studio para gerar dados de métricas de código que medem a complexidade e a manutenção de seu código gerenciado. Os dados de métricas de código podem ser gerados para uma solução inteira ou um único projeto.

Para obter informações sobre como gerar dados de métricas de código no Visual Studio, consulte [como gerar dados de métricas de código](../code-quality/how-to-generate-code-metrics-data.md).

## <a name="software-measurements"></a>Medições de software

A lista a seguir mostra os resultados de métricas de código que o Visual Studio calcula:

- **Índice de facilidade de manutenção** – calcula um valor de índice entre 0 e 100 que representa a facilidade relativa de manter o código. Um valor alto significa melhor facilidade de manutenção. As Classificações codificadas por cor podem ser usadas para identificar rapidamente os pontos problemáticos em seu código. Uma classificação verde é entre 20 e 100 e indica que o código tem boa facilidade de manutenção. Uma classificação amarela é entre 10 e 19 e indica que o código é de manutenção moderada. Uma classificação vermelha é uma classificação entre 0 e 9 e indica baixa facilidade de manutenção. Para obter mais informações, consulte o [intervalo de índice de manutenção e](https://blogs.msdn.microsoft.com/codeanalysis/2007/11/20/maintainability-index-range-and-meaning/) o que significa a postagem no blog.

- **Complexidade ciclomática** – mede a complexidade estrutural do código. Ele é criado calculando o número de caminhos de código diferentes no fluxo do programa. Um programa que tem um fluxo de controle complexo requer mais testes para obter uma boa cobertura de código e é menos passível de manutenção. Para obter mais informações, consulte a [entrada da Wikipédia para complexidade ciclomática](https://wikipedia.org/wiki/Cyclomatic_complexity).

- **Profundidade de herança** – indica o número de classes diferentes que herdam uma da outra, de volta para a classe base. A profundidade da herança é semelhante ao acoplamento de classes, pois uma alteração em uma classe base pode afetar qualquer uma de suas classes herdadas. Quanto maior esse número, mais profunda a herança e maior o potencial para modificações na classe base resultam em uma alteração significativa. Para uma profundidade de herança, um valor baixo é bom e um valor alto é ruim.

- **Acoplamento de classe** – mede o acoplamento para classes exclusivas por meio de parâmetros, variáveis locais, tipos de retorno, chamadas de método, instanciações genéricas ou de modelo, classes base, implementações de interface, campos definidos em tipos externos e decoração de atributo. Um bom design de software determina que os tipos e métodos devem ter alta coesão e acoplamento baixo. O acoplamento alto indica um design que é difícil de reutilizar e manter devido a muitas interdependências em outros tipos. Para obter mais informações, consulte a postagem do blog de [acoplamento de classes](https://blogs.msdn.microsoft.com/zainnab/2011/05/25/code-metrics-class-coupling/) .

::: moniker range=">=vs-2019"

- **Linhas de código-fonte** – indica o número exato de linhas de código-fonte que estão presentes no arquivo de origem, incluindo linhas em branco. Essa métrica está disponível a partir do Visual Studio 2019 versão 16,4 e Microsoft. CodeAnalysis. Metrics (2.9.5).

- **Linhas de código executável** – indica o número aproximado de linhas ou operações de código executável. Esta é uma contagem do número de operações no código executável. Essa métrica está disponível a partir do Visual Studio 2019 versão 16,4 e Microsoft. CodeAnalysis. Metrics (2.9.5). O valor normalmente é uma correspondência próxima à métrica anterior, **linhas de código**, que é a métrica baseada em instrução MSIL usada no modo herdado.
::: moniker-end
::: moniker range="vs-2017"

- **Linhas de código** – indica o número aproximado de linhas no código. A contagem é baseada no código IL e, portanto, não é o número exato de linhas no arquivo de código-fonte. Uma contagem alta pode indicar que um tipo ou método está tentando fazer muito trabalho e deve ser dividido. Ele também pode indicar que o tipo ou o método pode ser difícil de manter.

   > [!NOTE]
   > A [versão de linha de comando](../code-quality/how-to-generate-code-metrics-data.md#command-line-code-metrics) da ferramenta de métricas de código conta as linhas reais de código, pois ele analisa o código-fonte em vez de Il.
::: moniker-end

## <a name="anonymous-methods"></a>Métodos anônimos

Um *método anônimo* é apenas um método que não tem nome. Os métodos anônimos são usados com mais frequência para passar um bloco de código como um parâmetro delegado. Os resultados de métricas de código para um método anônimo declarado em um membro, como um método ou acessador, são associados ao membro que declara o método. Eles não estão associados ao membro que chama o método.

## <a name="generated-code"></a>Código gerado

Algumas ferramentas de software e compiladores geram código que é adicionado a um projeto e que o desenvolvedor do projeto não vê ou não deve ser alterado. Principalmente, as métricas de código ignoram o código gerado quando calcula os valores de métricas. Isso permite que os valores de métrica reflitam o que o desenvolvedor pode ver e alterar.

O código gerado para Windows Forms não é ignorado, pois é um código que o desenvolvedor pode ver e alterar.

## <a name="next-steps"></a>Próximas etapas

- [Como gerar dados de métricas de código](../code-quality/how-to-generate-code-metrics-data.md)
- [Usar a janela de resultados de métricas de código](../code-quality/working-with-code-metrics-data.md)
