---
title: Métricas de código-complexidade ciclomática
ms.date: 5/7/2021
description: Saiba mais sobre a métrica de complexidade ciclomática para métricas de código no Visual Studio.
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 1798b0faa1b0cf44ae490f5b27571e5466b82ca9
ms.sourcegitcommit: cc66c898ce82f9f1159bd505647f315792cac9fc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2021
ms.locfileid: "109682623"
---
# <a name="code-metrics---cyclomatic-complexity"></a>Métricas de código-complexidade ciclomática

Ao trabalhar com métricas de código, um dos itens menos compreendidos parece ser uma complexidade ciclomática. Essencialmente, com a complexidade de ciclomática, os números mais altos são ruins e os números mais baixos são bons. Você pode usar a complexidade do ciclomática para ter uma noção de como um determinado código pode ser testado, mantido ou solucionado, bem como uma indicação de quão provável que o código será para produzir erros. Em um alto nível, determinamos o valor da complexidade ciclomática contando o número de decisões feitas em seu código-fonte. Neste artigo, você começa com um exemplo simples de complexidade ciclomática para entender o conceito rapidamente e, em seguida, examina algumas informações adicionais sobre o uso real e os limites sugeridos. Por fim, há uma seção de citações que podem ser usadas para se aprofundar nesse assunto.

## <a name="example"></a>Exemplo

A complexidade de ciclomática é definida como medindo "a quantidade de lógica de decisão em uma função de código-fonte" [NIST235](#nist235). Em síntese, quanto mais decisões tiverem de ser feitas no código, mais complexa será.

Vamos vê-lo em ação. Crie um novo aplicativo de console e calcule imediatamente suas métricas de código indo para **analisar > calcular métricas de código para solução**.

![Exemplo de complexidade ciclomática 1](media/cyclomatic-complexity-example-1.png)

Observe que a complexidade do ciclomática é a 2 (o menor valor possível). Se você adicionar um código de não decisão, observe que a complexidade não é alterada:

![Exemplo de complexidade ciclomática 2](media/cyclomatic-complexity-example-2.png)

Se você adicionar uma decisão, o valor de complexidade ciclomática subirá em 1:

![Exemplo de complexidade ciclomática 3](media/cyclomatic-complexity-example-3.png)

Quando você altera a instrução If para uma instrução switch com quatro decisões a serem feitas, ela vai do original de 2 a 6:

![Exemplo 4 de complexidade 4](media/cyclomatic-complexity-example-4.png)

Vamos dar uma olhada em uma base de código (hipotética) maior.

![Exemplo 5 de complexidade 5](media/cyclomatic-complexity-example-5.png)

Observe que a maioria dos itens, conforme você faz drill down na classe Products_Related, tem um valor de 1, mas alguns deles têm uma complexidade de 5. Por si só, isso pode não ser um grande problema, mas considerando que a maioria dos outros membros tem um 1 na mesma classe, você deve definitivamente olhar mais de perto esses dois itens e ver o que está neles. Você pode fazer isso clicando com o botão direito do mouse no item e escolhendo **Ir para Código-Fonte** no menu de contexto. Dê uma olhada mais de perto `Product.set(Product)` em :

![Exemplo 6 de complexidade 6](media/cyclomatic-complexity-example-6.png)

Considerando todas as instruções if, você pode ver por que a complexidadematica está em 5. Neste ponto, você pode decidir que esse é um nível aceitável de complexidade ou você pode refactorar para reduzir a complexidade.

## <a name="the-magic-number"></a>O número mágico

Assim como com muitas métricas nesse setor, não há nenhum limite exato de complexidade estemática que se ajuste a todas as organizações. No entanto, [NIST235](#nist235) indica que um limite de 10 é um bom ponto de partida:

"O número preciso a ser usado como um limite, no entanto, permanece um pouco confuso. O limite original de 10, conforme proposto por McCabe, tem evidências de suporte significativas, mas os limites até 15 também foram usados com êxito. Limites acima de 10 devem ser reservados para projetos que têm várias vantagens operacionais em relação a projetos típicos, por exemplo, equipe experiente, design formal, uma linguagem de programação moderna, programação estruturada, passo a passo de código e um plano de teste abrangente. Em outras palavras, uma organização pode escolher um limite de complexidade maior que 10, mas somente se tiver certeza de que sabe o que está fazendo e está disposto a dedicar o esforço de teste adicional exigido por módulos mais complexos." [NIST235](#nist235)

## <a name="cyclomatic-complexity-and-line-numbers"></a>Complexidade e números de linha metamáticos

Apenas observando o número de linhas de código por si só é, na melhor das coisas, um preditor muito amplo de qualidade de código. Há alguma verdade básica para a ideia de que quanto mais linhas de código em uma função, mais provável é ter erros. No entanto, quando você combina a complexidade ciclomática com linhas de código, você tem uma imagem muito mais clara do potencial para erros.

Conforme descrito pelo Software Assurance Technology Center (SATC) na NASA:

"O SATC encontrou a avaliação mais eficaz é uma combinação de tamanho e complexidade (ciclomática). Os módulos com uma alta complexidade e um grande porte tendem a ter a menor confiabilidade. Os módulos com baixo tamanho e alta complexidade também são um risco de confiabilidade, pois tendem a ser um código muito conciso, que é difícil de alterar ou modificar. " [SATC](#satc)

## <a name="code-analysis"></a>Análise de Código

A análise de código inclui uma categoria de regras de manutenção. Para obter mais informações, consulte [regras de manutenção](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings). Ao usar a análise de código herdado, o conjunto de regras de diretriz de design estendido contém uma área de manutenção:

![Conjuntos de regras de diretrizes de design de complexidade ciclomática](media/cyclomatic-complexity-design-guidelines.png)

Dentro da área de manutenção, há uma regra de complexidade:

![Regra de manutenção de complexidade ciclomática](media/cyclomatic-complexity-maintainability-rule.png)

Essa regra emite um aviso quando a complexidade do ciclomática atinge 25, para que possa ajudá-lo a evitar complexidade excessiva. Para saber mais sobre a regra, consulte [CA1502](/dotnet/fundamentals/code-analysis/quality-rules/ca1502)

## <a name="putting-it-all-together"></a>Juntando tudo

O resultado final é que um número de alta complexidade significa maior probabilidade de erros com o aumento de tempo para manter e solucionar problemas. Examine com mais detalhes todas as funções que têm alta complexidade e decida se elas devem ser refatoras para torná-las menos complexas.

## <a name="citations"></a>Citações

### <a name="mccabe5"></a>MCCABE5

McCabe, T. e A. Watson (1994), Complexidade de software (CrossTalk: The Journal of Defense Software Engineering).

### <a name="nist235"></a>NIST235

Watson, A. H., & McCabe, T. J. (1996). Testes estruturados: uma metodologia de teste usando a métrica de complexidade moscossomática (Publicação especial NIST 500-235). Recuperado em 14 de maio de 2011, do site mcCabe Software: [http://www.mccabe.com/pdf/mccabe-nist235r.pdf](http://www.mccabe.com/pdf/mccabe-nist235r.pdf)

### <a name="satc"></a>Satc

Rose, L., Hammer, T., Marshall, J. (1998). Métricas e confiabilidade de software (Procedimentos do International International Symposium on Software Reliability Engineering). Recuperado em 14 de maio de 2011, do site da Universidade State De York: [http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.104.4041&rep=rep1&type=pdf)