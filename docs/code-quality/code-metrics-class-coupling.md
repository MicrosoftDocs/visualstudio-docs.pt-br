---
title: Métricas de código – Acoplamento de classe
ms.date: 1/8/2021
description: Saiba mais sobre a métrica de acoplamento de classe para métricas de código Visual Studio.
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 0853b807d3287eb584e76d9640ac98f930edb1a7
ms.sourcegitcommit: cc66c898ce82f9f1159bd505647f315792cac9fc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2021
ms.locfileid: "109666803"
---
# <a name="code-metrics---class-coupling"></a>Métricas de código – Acoplamento de classe

O acoplamento de classe também é chamado de Acoplamento entre Objetos (CBO), conforme definido originalmente por [CK94.](#ck94) Basicamente, o acoplamento de classe é uma medida de quantas classes uma única classe usa. Um número alto é ruim e um número baixo geralmente é bom com essa métrica. O acoplamento de classe foi mostrado como um preditor preciso de falha de software e estudos recentes mostraram que um valor de limite superior de 9 é o [S2010 mais eficiente.](#s2010)

De acordo com a documentação da Microsoft, o acoplamento de classe "mede o acoplamento a classes exclusivas por meio de parâmetros, variáveis locais, tipos de retorno, chamadas de método, instações genéricas ou de modelo, classes base, implementações de interface, campos definidos em tipos externos e decoração de atributo. Um bom design de software determina que tipos e métodos devem ter alta coesão e acoplamento baixo. O acoplamento alto indica um design difícil de reutilizar e manter devido a suas muitas interdependências em outros tipos."

Os conceitos de acoplamento e coesão estão claramente relacionados. Para manter essa discussão sobre o tópico, não entraremos em detalhes com a coesão além de dar uma breve definição de [KKLS2000:](#kkls2000)

"A coesão do módulo foi introduzida por Yourdon e Ltda como "quão fortemente vinculados ou relacionados os elementos internos de um módulo estão entre si" [YC79](#yc79). Um módulo terá uma coesão forte se representar exatamente uma tarefa [...], e todos os seus elementos contribuem para essa única tarefa. Eles descrevem a coesão como um atributo de design, em vez de código, e um atributo que pode ser usado para prever a reutilização, a capacidade de manutenção e a capacidade de alteração."

## <a name="class-coupling-example"></a>Exemplo de acoplamento de classe

Vamos ver o acoplamento de classe em ação. Primeiro, crie um novo aplicativo de console e crie uma nova classe chamada Person com algumas propriedades nele e calcule imediatamente as métricas de código:

![Exemplo de acoplamento de classe 1](media/class-coupling-example-1.png)

Observe que o acoplamento de classe é 0, pois essa classe não usa outras classes. Agora, crie outra classe chamada PersonStuff com um método que cria uma instância de Person e define os valores de propriedade. Calcule novamente as métricas de código:

![Exemplo de acoplamento de classe 2](media/class-coupling-example-2.png)

Veja como o valor de acoplamento de classe aumenta? Observe também que, não importa quantas Propriedades você definiu, o valor de acoplamento de classe acaba em 1 e não em outro valor. O acoplamento de classe mede cada classe apenas uma vez para essa métrica, não importa quanto ela é usada. Além disso, você pode ver que `DoSomething()` tem um 1, mas o construtor, `PersonStuff()` tem um 0 para seu valor? Atualmente, não há nenhum código no construtor que esteja usando outra classe.

E se você colocar o código no construtor que usou outra classe? Aqui está o que você obtém:

![Exemplo de acoplamento de classe 3](media/class-coupling-example-3.png)

Agora, o construtor tem claramente o código que usa outra classe e a métrica de acoplamento de classe mostra esse fato. Novamente, você pode ver que o acoplamento de classe geral para `PersonStuff()` é 1 e `DoSomething()` também é 1 para mostrar que apenas uma classe externa está sendo usada, não importa a quantidade de código interno que ela usa.

Em seguida, crie outra classe nova. Dê um nome a essa classe e crie algumas propriedades dentro dela:

![Exemplo de acoplamento de classe – Adicionar nova classe](media/class-coupling-example-add-new-class.png)

Agora, consuma a classe em nosso `DoSomething()` método dentro da `PersonStuff` classe e calcule novamente as métricas de código:

![Exemplo de acoplamento de classe 4](media/class-coupling-example-4.png)

Como você pode ver, o acoplamento de classe para a classe PersonStuff vai até 2 e, se você detalhar a classe, poderá ver que o `DoSomething()` método tem o maior acoplamento nele, mas o Construtor ainda consome apenas uma classe.  Usando essas métricas, você pode ver o número máximo geral de uma determinada classe e fazer uma busca nos detalhes por membro.

## <a name="the-magic-number"></a>O número mágico

Assim como com a complexidade massática, não há nenhum limite que se ajuste a todas as organizações. No entanto, [S2010](#s2010) indica que um limite de 9 é ideal:

"Portanto, consideramos os valores de limite [...] como o mais eficaz. Esses valores de limite (para um único membro) são CBO = 9[...]." (ênfase adicionada)

## <a name="code-analysis"></a>Análise de Código

A análise de código inclui uma categoria de regras de manutenção. Para obter mais informações, consulte [Regras de manutenção](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings). Ao usar a análise de código herdada, o conjunto de regras de Diretriz de Design Estendido contém uma área de capacidade de manutenção:

![Regras de diretrizes de design estendido de acoplamento de classe](media/class-coupling-extended-design-guideline-rules.png)

Dentro da área de manutenção, há uma regra para o acoplamento de classe:

![Regra de acoplamento de classe](media/class-coupling-maintainability-area-rules.png)

Essa regra emite um aviso quando o acoplamento de classe é excessivo. Para obter mais informações, consulte [CA1506: Evitar acoplamento de classe excessivo.](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)

## <a name="citations"></a>Citações

### <a name="ck94"></a>CK94

Chidamber, S. R. & Kemerer, C. F. (1994). Um conjunto de métricas para design orientado a objeto (transações IEEE na engenharia de software, Vol. 20, não. 6). Recuperado em 14 de maio de 2011, da Universidade do site da Pittsburgh: [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="kkls2000"></a>KKLS2000

Kabaili, H., Keller, R., Lustman, F., e Saint-Denis, G. (2000). Coesão de classe revisitada: um estudo empírica nos sistemas industriais (procedimentos do workshop sobre abordagens quantitativas em Object-Oriented engenharia de software). Recuperado de 20 de maio de 2011, do site da Web do Université de Montréal [http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf](http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf)

### <a name="sk2003"></a>SK2003

Subramanyam, R. & Krishnan, M. S. (2003). Empírica análise de métricas de CK para Object-Oriented complexidade de design: implicações para defeitos de software (transações IEEE na engenharia de software, Vol. 29, não. 4). Recuperado 14 de maio de 2011, do site da Universidade de Massachusetts Dartmouth [http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf](http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf)

### <a name="s2010"></a>S2010

Shatnawi, R. (2010). Uma investigação quantitativa dos níveis de risco aceitáveis de Object-Oriented métricas em sistemas Open-Source (transações IEEE na engenharia de software, Vol. 36, não. 2).

### <a name="yc79"></a>YC79

Edward Yourdon e Larry L. Constantine. Design estruturado. Prentice Hall, Englewood beira, N.J., 1979.