---
title: Nós de textura | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b7df5ef3-dd4f-4964-9d96-34e0e180515e
caps.latest.revision: 14
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: bda107323b24940ed8cab18a61f9e491f8392f53
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49252350"
---
# <a name="texture-nodes"></a>Nós de textura
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Designer de Sombreador, os nós de textura coletam amostram de vários tipos de textura e geometrias e produzem ou transformam as coordenadas de textura. As texturas fornecem detalhes de cor e iluminação dos objetos.  
  
## <a name="texture-node-reference"></a>Referência do nó de textura  
  
|Nó|Detalhes|Propriedades|  
|----------|-------------|----------------|  
|**Amostra de Cubemap**|Usa uma amostra de cor de um cubemap nas coordenadas especificadas.<br /><br /> É possível usar um cubemap para fornecer detalhes de cor para efeitos de reflexão ou para aplicar a um objeto esférico uma textura que tem menos distorção do que uma textura 2D.<br /><br /> **Entrada:**<br /><br /> `UVW`: `float3`<br /> Um vetor que especifica o local no cubo de textura em que a amostra é coletada. A amostra é coletada no ponto em que esse vetor intersecciona o cubo.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> A amostra de cor.|**Textura**<br /> O registro de textura associado à amostra.|  
|**Amostra de mapa normal**|Usa uma amostra normal de um mapa normal 2D nas coordenadas especificadas<br /><br /> É possível usar um mapa normal para simular a aparência de detalhes geométricos adicionais na superfície de um objeto. Mapas normais contêm dados compactados que representam um vetor de unidade em vez de dados de cor<br /><br /> **Entrada:**<br /><br /> `UV`: `float2`<br /> As coordenadas nas quais a amostra é coletada.<br /><br /> **Saída:**<br /><br /> `Output`: `float3`<br /> A amostra normal.|**Ajuste de eixo**<br /> O fator usado para ajustar a direção da amostra do mapa normal.<br /><br /> **Textura**<br /> O registro de textura associado à amostra.|  
|**Pan UV**|Aplica a panorâmica às coordenadas de textura especificadas como uma função de tempo.<br /><br /> É possível usar essa opção para mover uma textura ou um mapa normal na superfície de um objeto.<br /><br /> **Entrada:**<br /><br /> `UV`: `float2`<br /> As coordenadas às quais aplicar a panorâmica.<br /><br /> `Time`: `float`<br /> O tempo durante o qual será aplicada uma panorâmica, em segundos.<br /><br /> **Saída:**<br /><br /> `Output`: `float2`<br /> As coordenadas com panorâmica aplicada.|**Velocidade X**<br /> O número de texels estendidos ao longo do eixo x, por segundo.<br /><br /> **Velocidade Y**<br /> O número de texels estendido ao longo do eixo y, por segundo.|  
|**Parallax UV**|Desloca as coordenadas de textura especificadas como uma função de altura e um ângulo de visão.<br /><br /> O efeito que isso cria é conhecido como *mapeamento parallax* ou mapeamento de deslocamento virtual. É possível usá-lo para criar a ilusão de profundidade em uma superfície plana.<br /><br /> **Entrada:**<br /><br /> `UV`: `float2`<br /> As coordenadas a serem deslocadas.<br /><br /> `Height`: `float`<br /> O valor de heightmap associado às coordenadas `UV`.<br /><br /> **Saída:**<br /><br /> `Output`: `float2`<br /> As coordenadas deslocadas.|**Plano de profundidade**<br /> A profundidade de referência do efeito parallax. Por padrão, o valor é 0,5. Valores menores elevam a textura; valores maiores a afundam na superfície.<br /><br /> **Escala de profundidade**<br /> A escala do efeito parallax. Isso torna a profundidade aparente mais ou menos acentuada. Os valores típicos variam de 0,02 a 0,1.|  
|**Girar UV**|Gira as coordenadas de textura especificadas em torno de um ponto central como uma função de tempo.<br /><br /> É possível usar essa opção para girar uma textura ou um mapa normal na superfície de um objeto.<br /><br /> **Entrada:**<br /><br /> `UV`: `float2`<br /> As coordenadas a serem giradas.<br /><br /> `Time`: `float`<br /> O tempo durante o qual será aplicada uma panorâmica, em segundos.<br /><br /> **Saída:**<br /><br /> `Output`: `float2`<br /> As coordenadas giradas.|**X central**<br /> A coordenada x que define o centro de rotação.<br /><br /> **Y central**<br /> A coordenada y que define o centro de rotação.<br /><br /> **Velocidade**<br /> O ângulo em radianos, pelo qual a textura gira por segundo.|  
|**Coordenada de textura**|As coordenadas de textura do pixel atual.<br /><br /> As coordenadas de textura são determinadas pela interpolação entre os atributos de coordenadas de textura de vértices próximos. É possível considerar isso como a posição do pixel atual no espaço de textura.<br /><br /> **Saída:**<br /><br /> `Output`: `float2`<br /> As coordenadas de textura.|Nenhum|  
|**Dimensões de textura**|Gera a largura e a altura de um mapa de textura 2D.<br /><br /> É possível usar as dimensões de textura para considerar a largura e a altura da textura em um sombreador.<br /><br /> **Saída:**<br /><br /> `Output`: `float2`<br /> A largura e a altura da textura, expressas como um vetor. A largura é armazenada no primeiro elemento do vetor. A altura é armazenada no segundo elemento.|**Textura**<br /> O registro de textura associado às dimensões de textura.|  
|**Texel Delta**|Gera o delta (distância) entre os texels de um mapa de textura 2D.<br /><br /> É possível usar o texel delta para coletar amostras de valores de texel vizinhos em um sombreador.<br /><br /> **Saída:**<br /><br /> `Output`: `float2`<br /> O delta (distância) de um texel até o próximo texel (movendo diagonalmente na direção positiva), expresso como um vetor no espaço de textura normalizado. É possível derivar as posições de todos os texels vizinhos ignorando ou negando seletivamente as coordenadas U ou V do delta.|**Textura**<br /> O registro de textura associado ao textel delta.|  
|**Amostra de textura**|Usa uma amostra de cor de um mapa de textura 2D nas coordenadas especificadas.<br /><br /> É possível usar um mapa de textura para fornecer detalhes de cor na superfície de um objeto.<br /><br /> **Entrada:**<br /><br /> `UV`: `float2`<br /> As coordenadas nas quais a amostra é coletada.<br /><br /> **Saída:**<br /><br /> `Output`: `float4`<br /> A amostra de cor.|**Textura**<br /> O registro de textura associado à amostra.|



