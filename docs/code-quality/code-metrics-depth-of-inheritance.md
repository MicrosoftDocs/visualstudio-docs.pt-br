---
title: Métricas de código – Profundidade da herança
ms.date: 1/8/2021
description: Saiba mais sobre a profundidade da métrica de herança para métricas de código Visual Studio.
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1d6ac085463087fc73aac4429488ab475e91c10f
ms.sourcegitcommit: cc66c898ce82f9f1159bd505647f315792cac9fc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2021
ms.locfileid: "109682625"
---
# <a name="code-metrics---depth-of-inheritance-dit"></a>Métricas de código – DIT (profundidade de herança)

Neste artigo, você aprenderá sobre uma das métricas projetadas especificamente para análise orientada a objeto: profundidade de herança. A profundidade da herança, também chamada de profundidade da árvore de herança (DIT), é definida como "o comprimento máximo do nó até a raiz da árvore" [CK](#ck). Você pode ver isso com um exemplo simples. Crie um novo projeto de Biblioteca de Classes e, antes de escrever qualquer código, calcule as métricas de código escolhendo Analisar > Calcular Métricas de **Código para a Solução**.

![Exemplo de profundidade de herança 1](media/depth-of-inheritance-example-1.png)

Como todas as classes herdam `System.Object` de , a profundidade é 1 no momento. Se você herdar dessa classe e examinar a nova classe, poderá ver o resultado:

![Profundidade do exemplo de herança 2](media/depth-of-inheritance-example-2.png)

Observe que quanto menor o nó na árvore ( nesse caso), maior `Class2` a profundidade da herança. Você pode continuar a criar filhos e fazer com que a profundidade aumente tanto quanto quiser.

## <a name="assumptions"></a>Suposições

A profundidade da herança é baseada em três suposições [fundamentais CK:](#ck)

1. Quanto mais profunda for uma classe na hierarquia, maior será o número de métodos que ela provavelmente herdará, o que dificulta a previsão de seu comportamento.

2. Árvores mais profundas envolvem maior complexidade de design, pois mais classes e métodos estão envolvidos.

3. Classes mais profundas na árvore têm um maior potencial para reutilização de métodos herdados.

Suposições 1 e 2 dizem que ter um número mais alto para profundidade é ruim. Se esse for o local em que ele foi encerrado, você estaria em boa forma; no entanto, a suposição 3 indica que um número mais alto para profundidade é bom para a possível reutilização de código.

## <a name="analysis"></a>Análise

Veja como você lê a métrica de profundidade:

- Número baixo para profundidade

  Um número baixo de profundidade implica menos complexidade, mas também a possibilidade de menos reutilização de código por meio de herança.

- Número alto para profundidade

  Um número alto de profundidade implica mais potencial para a reutilização de código por meio de herança, mas também maior complexidade com uma probabilidade mais alta de erros no código.

## <a name="code-analysis"></a>Análise de Código

A análise de código inclui uma categoria de regras de manutenção. Para obter mais informações, consulte [regras de manutenção](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings). Ao usar a análise de código herdado, o conjunto de regras de diretriz de design estendido contém uma área de manutenção:

![Profundidade das diretrizes de design de herança conjuntos de regras](media/depth-of-inheritance-design-guidelines.png)

Dentro da área de manutenção, há uma regra para herança:

![Profundidade da regra de manutenção de herança](media/depth-of-inheritance-maintainability-rule.png)

Essa regra emite um aviso quando a profundidade de herança atinge 6 ou mais, portanto, é uma boa regra para ajudar a evitar a herança excessiva. Para saber mais sobre a regra, consulte [CA1501](/dotnet/fundamentals/code-analysis/quality-rules/ca1501).

## <a name="putting-it-all-together"></a>Juntando tudo

Valores altos para DIT significam que o potencial de erros também é alto, valores baixos reduzem o potencial de erros. Valores altos para DIT indicam um potencial maior para a reutilização de código por meio de herança, os valores baixos sugerem menos reutilização de código, embora a herança seja aproveitada. Devido à falta de dados suficientes, não há nenhum padrão aceito atualmente para valores de DIT. Até mesmo estudos feitos recentemente não encontraram dados suficientes para determinar um número viável que poderia ser usado como um número padrão para essa métrica [Shatnawi](#shatnawi). Embora não haja nenhuma evidência empírica para dar suporte a ela, vários recursos sugerem que uma DIT em cerca de 5 ou 6 deve ser um limite superior. Por exemplo, consulte [http://www.devx.com/architect/Article/45611](http://www.devx.com/architect/Article/45611) .

## <a name="citations"></a>Citações

### <a name="ck"></a>CK

Chidamber, S. R. & Kemerer, C. F. (1994). Um Metrics Suite para Design Orientado a Objeto (Transações IEEE na Engenharia de Software, Vol. 20, Não. 6). Recuperado em 14 de maio de 2011, do site da Universidade de York: [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="krishnan"></a>Krishnan

Subramanyam, R. & Ltdn, M. S. (2003). Análise empírica de métricas de CK para Object-Oriented design: implicações para defeitos de software (transações IEEE na engenharia de software, Vol. 29, Não. 4). Recuperado em 14 de maio de 2011, originalmente obtido do site da University of Massachusetts Dart ltda [https://ieeexplore.ieee.org/abstract/document/1191795](https://ieeexplore.ieee.org/abstract/document/1191795)

### <a name="shatnawi"></a>Shatnawi

Shatnawi, R. (2010). Uma investigação quantitativa dos níveis de risco aceitáveis Object-Oriented métricas em sistemas Open-Source (transações IEEE na engenharia de software, Vol. 36, Não. 2).