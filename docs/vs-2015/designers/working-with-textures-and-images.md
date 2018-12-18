---
title: Trabalhando com texturas e imagens | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b9fbc8fa-66d1-4055-8460-24d8b8fbe43e
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ff5125ce46abe993f35551a0ce46a0d211af99bb
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49250491"
---
# <a name="working-with-textures-and-images"></a>Trabalhando com texturas e imagens
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Você pode usar o Editor de Imagens no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para criar e modificar imagens e texturas. O Editor de Imagens dá suporte aos formatos avançados de textura e imagens como aqueles que são usados no desenvolvimento de aplicativos do DirectX.  
  
> [!NOTE]
>  O Editor de Imagens não dá suporte a imagens com poucas cores como ícones ou cursores. Para criar ou modificar esses tipos de imagens, use o [Editor de imagens para ícones](http://msdn.microsoft.com/library/586d2b8b-0348-4883-a85d-1ff0ddbf14dd).  
  
## <a name="textures-and-images"></a>Texturas e imagens  
 Texturas e imagens são, em um nível básico, apenas tabelas de dados que são usadas para fornecer detalhes visuais em aplicativos de gráficos. O tipo de detalhe que uma imagem ou textura fornece depende de como ela é usada, mas amostras de cores, valores de alfa (transparência), normais da superfície e valores de altura são exemplos comuns. A principal diferença entre uma textura e uma imagem é que uma textura deve ser usada junto com uma representação de forma — normalmente um modelo 3D — para expressar um objeto completo ou cena, mas uma imagem é normalmente uma representação independente do objeto ou cena.  
  
 Os tipos comuns de texturas incluem:  
  
 Mapas de textura  
 Os mapas de textura contêm valores de cor que são organizados como matrizes uni, bi e tridimensionais. Eles são usados para fornecer detalhes de cor no objeto afetado. Cores normalmente são codificadas usando os canais de cor RGB (vermelho, verde, azul) e podem incluir um quarto canal, alfa, que representa a transparência. As cores podem ser codificadas em outro esquema de cores, o que é menos comum ou o quarto canal pode conter dados que não são alfa — por exemplo, a altura.  
  
 Mapas normais  
 Os mapas normais contêm normais da superfície. Eles são usados para fornecer detalhes de iluminação no objeto afetado. Os normais são usualmente codificados usando os componentes de cor vermelho, verde e azul para armazenar as dimensões x, y e z do vetor. No entanto, existem outras codificações — por exemplo, codificações baseadas em coordenadas polares.  
  
 Mapas de altura  
 Os mapas de altura contêm dados de campo de altura. Eles são usados para fornecer um formulário de detalhe geométrico no objeto afetado — usando o código do sombreador para calcular o efeito desejado — ou para fornecer pontos de dados para fins como geração de terreno. Os valores de altura normalmente são codificados usando um canal em uma textura.  
  
 Mapas de cubo  
 Os mapas de cubo podem conter diferentes tipos de dados — por exemplo, cores ou normais — mas são organizados como seis texturas nas faces de um cubo. Por causa disso, os mapas de cubo não são amostrados fornecendo as coordenadas de textura, mas fornecendo um vetor cuja origem é o centro do cubo. O exemplo é capturado no ponto em que o vetor cruza o cubo. Os mapas de cubo são usados para fornecer uma aproximação do ambiente que pode ser usado para calcular os reflexos — isso é conhecido como *mapeamento de ambiente* — ou para fornecer textura a objetos esféricos com menos distorção do que as texturas básicas e bidimensionais podem fornecer.  
  
 Qualquer textura pode ser codificada e compactada em várias maneiras ortogonais para o tipo de dados que contém uma textura ou para a dimensionalidade ou "forma" da textura. No entanto, os diferentes métodos de compactação e codificação produzem resultados melhores para diferentes tipos de dados.  
  
 Você pode usar o Editor de Imagens para criar e modificar texturas e imagens de maneiras semelhantes a outros editores de imagem. O Editor de Imagens também fornece mapeamento mip e outros recursos para uso com elementos gráficos 3D e dá suporte a muitos dos formatos de textura altamente compactados e acelerados por hardware que dão suporte ao DirectX.  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Editor de Imagens](../designers/image-editor.md)|Descreve como usar o Editor de Imagens para trabalhar com texturas e imagens.|  
|[Exemplos do Editor de Imagens](../designers/image-editor-examples.md)|Fornece links para tópicos que demonstram como usar o Editor de Imagens para executar tarefas de processamento de imagens comuns.|



