---
title: Nós de filtro
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: f7cae2dc-e9a7-49d4-8be5-58b79868624e
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bfc74287706976f96a5e565bef3da1493cd44866
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769279"
---
# <a name="filter-nodes"></a>Nós de filtro

No Designer de Sombreador, nós de filtro transformam uma entrada — por exemplo, uma amostra de cor ou textura — em um valor de cor figurativo. Esses valores de cor figurativos normalmente são usados na renderização não fotorrealista ou como componentes de outros efeitos visuais.

## <a name="filter-node-reference"></a>Referência do nó de filtro

|Nó|Detalhes|Propriedades|
|----------|-------------|----------------|
|**Desfoque**|Desfoca os pixels em uma textura usando uma função gaussiana.<br /><br /> É possível usá-lo para reduzir o ruído ou os detalhes de cor em uma textura.<br /><br /> **Entrada:**<br /><br /> `UV`: `float2`<br /> As coordenadas o texel a ser testado.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> O valor da cor desfocada.|**Textura**<br /> O registro de textura associado à amostra usada durante o desfoque.|
|**Remover Saturação**|Reduz a quantidade de cor na cor especificada.<br /><br /> Conforme a cor é removida, o valor da cor se aproxima de seu equivalente na escala de cinza.<br /><br /> **Entrada:**<br /><br /> `RGB`: `float3`<br /> A cor cuja saturação será removida.<br /><br /> `Percent`: `float`<br /> A porcentagem de cor a ser removida, expressa como um valor normalizado no intervalo [0, 1].<br /><br /> **Saída:**<br /><br /> `Output`: `float3`<br /> A cor cuja saturação foi removida.|**Luminância**<br /> Os pesos dados aos componentes de cor vermelho, verde e azul.|
|**Detecção de Borda**|Detecta bordas em uma textura usando um detector de bordas de Canny. Os pixels da borda são transformados em branco e os pixels que não são da borda são transformados em preto.<br /><br /> É possível usá-lo para identificar bordas em uma textura para que você possa usar efeitos adicionais para tratar os pixels da borda.<br /><br /> **Entrada:**<br /><br /> `UV`: `float2`<br /> As coordenadas o texel a ser testado.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> Branco se o texel estiver em uma borda; caso contrário, preto.|**Textura**<br /> O registro de textura que está associado à amostra usada durante a detecção de borda.|
|**Ajustar Nitidez**|Ajusta a nitidez de uma textura.<br /><br /> É possível usá-lo para destacar os detalhes de uma textura.<br /><br /> **Entrada:**<br /><br /> `UV`: `float2`<br /> As coordenadas o texel a ser testado.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> O valor da cor desfocada.|**Textura**<br /> O registro de textura associado à amostra usada durante o ajuste de nitidez.|