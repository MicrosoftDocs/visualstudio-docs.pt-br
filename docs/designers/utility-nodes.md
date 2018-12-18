---
title: Nós de utilitário
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: reference
ms.assetid: ff732221-b731-424c-ad5b-82ef5f21dff5
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: b4d3371001c3df3b5233562ce7b30e711ed12d4c
ms.sourcegitcommit: e13e61ddea6032a8282abe16131d9e136a927984
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
ms.locfileid: "31918199"
---
# <a name="utility-nodes"></a>Nós de utilitário

No Designer de Sombreador, nós de utilitário representam cálculos comuns e úteis de sombreador que não se enquadram em outras categorias. Alguns nós de utilitário realizam operações simples como acrescentar vetores ou escolher resultados condicionalmente; outros executam operações complexas, como calcular contribuições de iluminação de acordo com modelos populares de iluminação.

## <a name="utility-node-reference"></a>Referência do nó de utilitário

|Nó|Detalhes|Propriedades|
|----------|-------------|----------------|
|**Vetor de Acréscimo**|Cria um vetor acrescentando as entradas especificadas.<br /><br /> **Entrada:**<br /><br /> `Vector`: `float`, `float2` ou `float3`<br /> Os valores a se acrescentar.<br /><br /> `Value to Append`: `float`<br /> O valor a ser acrescentado.<br /><br /> **Saída:**<br /><br /> `Output`: `float2`, `float3` ou `float4` dependendo do tipo de entrada `Vector`<br /> O novo vetor.|Nenhum|
|**Fresnel**|Calcula a queda de Fresnel com base no vetor perpendicular à superfície especificado.<br /><br /> O valor da queda de Fresnel expressa a proximidade do vetor perpendicular à superfície do pixel atual ao vetor de exibição. Quando os vetores estão alinhados, o resultado da função é 0; o resultado aumenta à medida que os vetores se tornam menos semelhantes e atingem o máximo quando os vetores são ortogonais. Você pode usar esses vetores para tornar um efeito mais ou menos aparente com base na relação entre a orientação do pixel atual e da câmera.<br /><br /> **Entrada:**<br /><br /> `Surface Normal`: `float3`<br /> O vetor perpendicular à superfície do pixel atual, definido no espaço tangente do pixel atual. É possível usar isso para perturbar vetor perpendicular à superfície aparente, como no mapeamento normal.<br /><br /> **Saída:**<br /><br /> `Output`: `float`<br /> A reflexibilidade do pixel atual.|**Expoente**<br /> O expoente usado para calcular a queda do Fresnel.|
|**Se**|De forma condicional, escolhe um dos três resultados possíveis por componente. A condição é definida pela relação entre duas outras entradas especificadas.<br /><br /> Para cada componente do resultado, o componente correspondente de um dos três resultados possível é escolhido, com base na relação entre os componentes correspondentes das duas primeiras entradas.<br /><br /> **Entrada:**<br /><br /> `X`: `float`, `float2`, `float3` ou `float4`<br /> O valor do lado esquerdo a se comparar.<br /><br /> `Y`: mesmo tipo como entrada `X`<br /> O valor do lado direito a se comparar.<br /><br /> `X > Y`: mesmo tipo como entrada `X`<br /> Os valores escolhidos quando `X` é maior do que `Y`.<br /><br /> `X = Y`: mesmo tipo como entrada `X`<br /> Os valores escolhidos quando `X` é igual a `Y`.<br /><br /> `X < Y`: mesmo tipo como entrada `X`<br /> Os valores escolhidos quando `X` é menor que `Y`.<br /><br /> **Saída:**<br /><br /> `Output`: `float3`<br /> O resultado escolhido, por componente.|Nenhum|
|**Lambert**|Calcula a cor do pixel atual de acordo com o modelo de iluminação de Lambert, usando o vetor perpendicular à superfície especificado.<br /><br /> Essa cor é a soma da cor ambiente e contribuições de iluminação difusa em luminosidade direta. A cor ambiente aproxima a contribuição total da luminosidade indireta, mas parece simples e fosca sem a ajuda de iluminação adicional. A iluminação difusa ajuda a adicionar forma e a profundidade a um objeto.<br /><br /> **Entrada:**<br /><br /> `Surface Normal`: `float3`<br /> O vetor perpendicular à superfície do pixel atual, definido no espaço tangente do pixel atual. É possível usar isso para perturbar vetor perpendicular à superfície aparente, como no mapeamento normal.<br /><br /> `Diffuse Color`: `float3`<br /> A cor difusa do pixel atual, normalmente o **Ponto de Cor**. Se nenhuma entrada for fornecida, o valor padrão será branco.<br /><br /> **Saída:**<br /><br /> `Output`: `float3`<br /> A cor difusa do pixel atual.|Nenhum|
|**Vetor de Máscara**|Componentes de máscaras de vetor especificado.<br /><br /> É possível usá-lo para remover canais de cores específicos de um valor de cor ou para impedir que componentes específicos tenham um efeito em cálculos subsequentes.<br /><br /> **Entrada:**<br /><br /> `Vector`: `float4`<br /> O vetor a ser mascarado.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> O vetor mascarado.|**Vermelho / X**<br /> **False** para mascarar o componente vermelho (x); caso contrário, **True**.<br /><br /> **Verde / Y**<br /> **False** para mascarar o componente verde (y); caso contrário, **True**.<br /><br /> **Azul / Z**<br /> **False** para mascarar o componente azul (z); caso contrário, **True**.<br /><br /> **Alfa / W**<br /> **False** para mascarar o componente alfa (w); caso contrário, **True**.|
|**Vetor de Reflexão**|Calcula o vetor de reflexão do pixel atual no espaço tangente, com base na posição da câmera.<br /><br /> Pode ser usado para calcular reflexões, coordenadas de cubemap e contribuições de iluminação especular<br /><br /> **Entrada:**<br /><br /> `Tangent Space Surface Normal`: `float3`<br /> O vetor perpendicular à superfície do pixel atual, definido no espaço tangente do pixel atual. É possível usar isso para perturbar vetor perpendicular à superfície aparente, como no mapeamento normal.<br /><br /> **Saída:**<br /><br /> `Output`: `float3`<br /> O vetor de reflexão.|Nenhum|
|**Especular**|Calcula a contribuição de iluminação especular acordo com o modelo de iluminação de Phong, usando o vetor perpendicular à superfície especificado.<br /><br /> A iluminação especular dá uma aparência brilhante e refletora a um objeto, por exemplo, água, plástico ou metais.<br /><br /> **Entrada:**<br /><br /> `Surface Normal`: `float3`<br /> O vetor perpendicular à superfície do pixel atual, definido no espaço tangente do pixel atual. É possível usar isso para perturbar vetor perpendicular à superfície aparente, como no mapeamento normal.<br /><br /> **Saída:**<br /><br /> `Output`: `float3`<br /> A contribuição de cor de realces especulares.|Nenhum|