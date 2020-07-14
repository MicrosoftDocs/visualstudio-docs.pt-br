---
title: Nós de constante
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: 2c798a50-a2d7-459b-9879-ad4ad8290c9b
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 6868a5dc7cbace1d061c43cd507d32c271436a26
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769312"
---
# <a name="constant-nodes"></a>Nós de constante

No Designer do Sombreador, nós constantes representam valores literais e atributos de vértice interpolados em cálculos do sombreador de pixel. Como os atributos de vértice são interpolados — e, portanto, são diferentes para cada pixel — cada instância de sombreador de pixel recebe uma versão diferente da constante. Isso dá a cada pixel uma aparência única.

## <a name="vertex-attribute-interpolation"></a>Interpolação de atributo de vértice

A imagem de uma cena 3D em um jogo ou aplicativo é feita por meio da transformação matemática de inúmeros objetos — definido pelos vértices, atributos de vértice e definições de primitivas — em pixels na tela. Todas as informações necessárias para dar uma aparência exclusiva a um pixel são fornecidas por meio de atributos de vértice, combinados de acordo com a proximidade do pixel para os diferentes vértices que compõem seu *primitivo*. Um primitivo é um elemento básico de renderização; ou seja, uma forma simples como um ponto, uma linha ou um triângulo. Um pixel muito semelhante a um dos vértices recebe constantes quase idênticas a esse vértice, mas um pixel com espaçamento uniforme entre todos os vértices de um primitivo recebe constantes que são a média desses vértices. Na programação de gráficos, as constantes que os pixels recebem são consideradas *interpoladas*. Fornecer dados constantes a pixels dessa maneira produz qualidade visual muito boa e, ao mesmo tempo, reduz a superfície de memória e os requisitos de largura de banda.

Embora cada instância de sombreador de pixel receba apenas um conjunto de valores constantes e não possa alterar esses valores, instâncias diferentes de sombreador de pixel recebem diferentes conjuntos de dados constantes. Esse design permite que um programa sombreador produza uma saída de cor diferente para cada pixel no primitivo.

## <a name="constant-node-reference"></a>Referência de nó constante

|Nó|Detalhes|Propriedades|
|----------|-------------|----------------|
|**Vetor de Câmera**|O vetor que se estende do pixel atual para a câmera no espaço de mundo.<br /><br /> É possível usar isso para calcular reflexões no espaço de mundo.<br /><br /> **Saída**<br /><br /> `Output`: `float3`<br /> O vetor do pixel atual da câmera.|Nenhum|
|**Constante de Cor**|Um valor de cor constante.<br /><br /> **Saída**<br /><br /> `Output`: `float4`<br /> O valor da cor.|**Saída**<br /> O valor da cor.|
|**Amortiza**|Um valor escalar constante.<br /><br /> **Saída**<br /><br /> `Output`: `float`<br /> O valor escalar.|**Saída**<br /> O valor escalar.|
|**Constante 2D**|Uma constante de vetor de dois componentes.<br /><br /> **Saída**<br /><br /> `Output`: `float2`<br /> O valor do vetor.|**Saída**<br /> O valor do vetor.|
|**Constante 3D**|Uma constante de vetor de três componentes.<br /><br /> **Saída**<br /><br /> `Output`: `float3`<br /> O valor do vetor.|**Saída**<br /> O valor do vetor.|
|**Constante 4D**|Uma constante de vetor de quatro componentes.<br /><br /> **Saída**<br /><br /> `Output`: `float4`<br /> O valor da cor.|**Saída**<br /> O valor do vetor.|
|**Posição Normalizada**|A posição do pixel atual, expressa em coordenadas de dispositivo normalizadas.<br /><br /> A coordenada X e Y têm valores no intervalo de [-1, 1], a coordenada Z tem um valor no intervalo de [0, 1] e o componente w contém o valor de profundidade de ponto no espaço de modo de exibição; w não é normalizado.<br /><br /> **Saída**<br /><br /> `Output`: `float4`<br /> A posição do pixel atual.|Nenhum|
|**Ponto de cor**|A cor difusa do pixel atual, que é uma combinação da cor difusa do material e dos atributos de cor do vértice.<br /><br /> **Saída**<br /><br /> `Output`: `float4`<br /> A cor difusa do pixel atual.|Nenhum|
|**Profundidade do ponto**|A profundidade do pixel atual no espaço de exibição.<br /><br /> **Saída**<br /><br /> `Output`: `float`<br /> A profundidade do pixel atual.|Nenhum|
|**Profundidade do Ponto Normalizado**|A profundidade do pixel atual, expresso em coordenadas do dispositivo normalizado.<br /><br /> O resultado tem um valor no intervalo [0, 1].<br /><br /> **Saída**<br /><br /> `Output`: `float`<br /> A profundidade do pixel atual.|Nenhum|
|**Posição da Tela**|A posição do pixel atual, expresso em coordenadas de tela.<br /><br /> As coordenadas de tela se baseiam no visor atual. Os componentes X e Y contêm as coordenadas de tela, o componente Z contém a profundidade normalizada a um intervalo de [0, 1] e o componente w contém o valor de profundidade no espaço de exibição.<br /><br /> **Saída**<br /><br /> `Output`: `float4`<br /> A posição do pixel atual.|Nenhum|
|**Vetor Perpendicular à Superfície**|O vetor perpendicular à superfície do pixel atual no espaço de objeto.<br /><br /> É possível usar isso para calcular as contribuições de iluminação e os reflexos no espaço de objeto.<br /><br /> **Saída**<br /><br /> `Output`: `float3`<br /> A superfície normal do pixel atual.|Nenhum|
|**Vetor de Câmera do Espaço Tangente**|O vetor que se estende de pixel atual para a câmera no espaço tangente.<br /><br /> É possível usar isso para calcular reflexões no espaço tangente.<br /><br /> **Saída**<br /><br /> `Output`: `float3`<br /> O vetor do pixel atual da câmera.|Nenhum|
|**Direção da Luz do Espaço Tangente**|O vetor que define a direção na qual a luz é lançada de uma fonte de luz no espaço tangente do pixel atual.<br /><br /> É possível usar isso para calcular as contribuições de iluminação e especulares no espaço tangente.<br /><br /> **Saída:**<br /><br /> `Output`: `float3`<br /> O vetor do pixel atual para uma fonte de luz.|Nenhum|
|**Vetor Perpendicular ao Mundo**|O vetor perpendicular à superfície do pixel atual no espaço de mundo.<br /><br /> É possível usar isso para calcular as contribuições de iluminação e os reflexos no espaço de mundo.<br /><br /> **Saída**<br /><br /> `Output`: `float3`<br /> A superfície normal do pixel atual.|Nenhum|
|**Posição do Mundo**|A posição do pixel atual no espaço de mundo.<br /><br /> **Saída**<br /><br /> `Output`: `float4`<br /> A posição do pixel atual.|Nenhum|