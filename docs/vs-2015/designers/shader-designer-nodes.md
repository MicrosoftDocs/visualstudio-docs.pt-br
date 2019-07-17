---
title: Nós do Designer de Sombreador | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: f5192fbd-c78f-40a8-a4d4-443209610268
caps.latest.revision: 8
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: cde6b6a44649f3a9e100a0ff10e3dda21f2d6f3c
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187739"
---
# <a name="shader-designer-nodes"></a>Nós do Designer de Sombreador
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Os artigos nesta seção da documentação contêm informações sobre os vários nós do Designer de Sombreador que você pode usar para criar efeitos gráficos.  
  
## <a name="nodes-and-node-types"></a>Nós e tipos de nó  
 O Designer de Sombreador representa os efeitos visuais, como um grafo. Esses grafos são criados de nós que são especificamente escolhidos e conectados de modo a obter o efeito desejado. Cada nó representa uma parte das informações ou de uma função matemática e as conexões entre eles representam como as informações fluem através do grafo para produzir o resultado. O Designer de Sombreador fornece seis tipos de nós diferentes — filtros, nós de textura, parâmetros, constantes, nós de utilitário e nós de matemática — e vários nós individuais pertencem a cada tipo. Esses nós e tipos de nó são descritos em outros artigos nesta seção. Consulte os links no final deste documento.  
  
## <a name="node-structure"></a>Estrutura de nó  
 Todos os nós são compostos de uma combinação de elementos comuns. Cada nó tem pelo menos um terminal de saída no seu lado direito (exceto o nó de cor final, que representa a saída do sombreador). Nós que representam cálculos ou amostras de textura têm terminais de entrada do lado esquerdo, mas nós que representam informações não têm terminais de entrada. Terminais de saída estão conectados a terminais de entrada para mover informações de um nó para outro.  
  
### <a name="promotion-of-inputs"></a>Promoção de entradas  
 Como o Designer de Sombreador, em última análise, deve gerar código-fonte HLSL para que o efeito possa ser usado em um jogo ou aplicativo, os nós do Designer de Sombreador são sujeito às regras da promoção de tipos que o HLSL usa. Como o hardware gráfico opera principalmente em valores de ponto flutuante, a promoção de tipos entre tipos diferentes — por exemplo, de `int` para `float` ou de `float` para `double` — é incomum. Em vez disso, como o hardware gráfico usa a mesma operação em várias partes de informações ao mesmo tempo, um tipo diferente de promoção pode ocorrer, no qual o mais curto de um número de entradas é aumentado para corresponder ao tamanho da entrada maior. A forma como o aumento é feito depende do tipo de entrada e também da própria operação:  
  
- **Se o menor tipo for um valor escalar, então:**  
  
     O valor escalar será replicado em um vetor que é igual à entrada maior. Por exemplo, a entrada escalar 5.0 se torna o vetor (5.0, 5.0, 5.0) quando a entrada maior da operação for um vetor de três elementos, independentemente de qual é a operação.  
  
- **Se o menor tipo for um vetor e a operação for de multiplicação (\*, /, % e assim por diante), então:**  
  
     O valor do vetor será copiado nos elementos à esquerda de um vetor que é igual à entrada maior e os elementos à direita serão definidos como 1.0. Por exemplo, a entrada de vetor (5.0, 5.0) se torna o vetor (5.0, 5.0, 1.0, 1.0) quando ele é multiplicado por um vetor de quatro elementos. Isso preserva o terceiro e o quarto elemento da saída usando a identidade de multiplicação, 1.0.  
  
- **Se o menor tipo for um vetor e a operação for aditiva (+,- e assim por diante), então:**  
  
     O valor do vetor será copiado nos elementos à esquerda de um vetor que é igual à entrada maior e os elementos à direita serão definidos como 0.0. Por exemplo, a entrada de vetor (5.0, 5.0) se torna o vetor (5.0, 5.0, 0.0, 0.0) quando ele é adicionado a um vetor de quatro elementos. Isso preserva o terceiro e o quarto elemento da saída usando a identidade de adição, 0.0.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Nós de constante](../designers/constant-nodes.md)|Descreve nós que você pode usar para representar valores literais e informações de estado de vértice interpoladas em cálculos do sombreador. Como o estado do vértice é interpolado — e, portanto, é diferente para cada pixel — cada instância de sombreador de pixel recebe uma versão diferente da constante.|  
|[Nós de parâmetro](../designers/parameter-nodes.md)|Descreve nós que você pode usar para representar a posição da câmera, as propriedades de material, os parâmetros de iluminação, a hora e outras informações de estado do aplicativo em cálculos do sombreador.|  
|[Nós de textura](../designers/texture-nodes.md)|Descreve os nós que você pode usar para amostragem de vários tipos de texturas e geometrias, e para produzir ou transformar as coordenadas de textura de maneiras comuns.|  
|[Nós de matemática](../designers/math-nodes.md)|Descreve os nós que você pode usar para executar operações algébricas, lógicas, trigonométricas e outras operações matemáticas que mapeiam diretamente até as instruções do HLSL.|  
|[Nós de utilitário](../designers/utility-nodes.md)|Descreve os nós que você pode usar para executar cálculos de iluminação comuns e outras operações comuns que não mapeiam diretamente até as instruções do HLSL.|  
|[Nós de filtro](../designers/filter-nodes.md)|Descreve os nós que você pode usar para executar a filtragem de textura e de cor.|
