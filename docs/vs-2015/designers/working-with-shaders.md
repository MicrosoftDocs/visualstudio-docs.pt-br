---
title: Trabalho com sombreadores | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6b2ea1ed-b995-4e75-af19-c68fd37a3bc5
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 72325522886ed1bc6ab262152c84fc3660231d86
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49226831"
---
# <a name="working-with-shaders"></a>Trabalhando com sombreadores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o Designer de Sombreadores baseado em gráfico em [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para efeitos de sombreamento personalizado de design. Você pode usar esses sombreadores em seu jogo ou aplicativo baseado no DirectX.  
  
## <a name="shaders"></a>Sombreadores  
 A *sombreador* é um programa de computador que executa cálculos de gráficos — por exemplo, transformações de vértice ou cor do pixel — e normalmente é executado em uma unidade de processamento gráfico (GPU) em vez da CPU. Porque a maioria dos estágios de pipeline gráfica tradicional, função fixa agora são executados por programas de sombreador, você pode usá-los para criar um pipeline é específico para as necessidades de seu aplicativo.  
  
 Os tipos mais comuns de sombreadores são *sombreadores de vértices*, que executam cálculos por vértice e substituir a transformação de função fixa e circuitos de iluminação no hardware de gráficos não programável, e *sombreadores de pixel*, que executam cálculos por pixel que determinam a cor de um pixel e substitua os circuitos de combinador de cores de função fixa em hardware de gráficos não programáveis. O hardware de gráficos moderno tornou ainda mais tipos de sombreadores possíveis —*sombreadores convexos*, *sombreadores de domínio* e *sombreadores de geometria* para cálculos de gráficos e *sombreadores de computação* para cálculos não gráficos. Nenhum desses estágios está disponível no hardware de gráficos não programável. Sombreadores foram criados usando uma linguagem semelhante ao assembly fornecido paralela de dados (SIMD) e instruções centrados em gráficos (produto de ponto). Agora, sombreadores normalmente são criados usando linguagens de alto nível, como C como HLSL (linguagem de sombreador de alto nível).  
  
 Você pode usar o Designer de Sombreadores criar sombreadores de pixel interativamente em vez de inserir e compilar o código. No Designer de Sombreadores, um sombreador é definido por um número de nós que representam conexões entre nós que representam o fluxo de valores de dados e os resultados intermediários por meio do sombreador e operações e dados. Usando essa abordagem e a visualização em tempo real no Designer de Sombreadores, você pode visualizar a execução do sombreador mais facilmente e variações de sombreador interessante por meio de experimentação "descobrir".  
  
## <a name="dgsl-documents"></a>Documentos DGSL  
 O Designer de Sombreadores salva sombreadores no formato de linguagem de sombreador gráfico direcionado (DGSL), que é um formato XML que se baseia em direcionadas gráfico Markup Language (DGML). Você pode aplicar os sombreadores DGSL diretamente em modelos 3D no Editor de Modelos. No entanto, antes de usar um sombreador DGSL em seu aplicativo, você deve exportá-lo em um formato que compreende DirectX — por exemplo, HLSL.  
  
 Como DGSL é compatível com DGML, você pode usar ferramentas projetadas para analisar documentos DGML para analisar seus sombreadores DGSL. Para saber mais sobre DGML, veja [Noções básicas sobre DGML (Directed Graph Markup Language)](http://msdn.microsoft.com/library/ee842619.aspx).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Designer de Sombreador](../designers/shader-designer.md)|Descreve como usar o Designer de Sombreador do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com sombreadores.|  
|[Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)|Discute os tipos de nós de Designer de Sombreadores que você pode usar para obter efeitos gráficos.|  
|[Exemplos do Designer de Sombreador](../designers/shader-designer-examples.md)|Fornece links para tópicos que demonstram como usar o Designer do sombreador para atingir efeitos gráficos comuns.|



