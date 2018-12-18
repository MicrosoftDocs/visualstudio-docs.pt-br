---
title: Trabalhar com ativos 3D para jogos e aplicativos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- vs.graphics
ms.assetid: 910d673b-c884-4eeb-9928-0e89f3d38cb6
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: bdf19958ec7b3cfe72ee00ea84e0e23724a51458
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49265221"
---
# <a name="working-with-3-d-assets-for-games-and-apps"></a>Trabalhando com ativos 3D para jogos e aplicativos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento descreve as ferramentas [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que você pode usar para criar ou modificar modelos 3D, texturas e sombreadores para aplicativos e jogos do DirectX.  
  
## <a name="directx-app-development-in-visual-studio"></a>Desenvolvimento de aplicativos em DirectX no Visual Studio  
 Normalmente, um aplicativo DirectX combina lógica de programação, a API do DirectX e programas HLSL (High Level Shading Language), junto com ativos visuais 3D e de áudio para apresentar uma experiência multimídia avançada e interativa.[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Inclui ferramentas que você pode usar para trabalhar com imagens e texturas, modelos 3D e sombreadores sem sair do IDE para usar outra ferramenta. As ferramentas do Visual Studio são especialmente adequadas para a criação de ativos de *espaço reservado*, os quais você pode usar para testar o código ou compilar protótipos antes de comissão de ativos prontos para produção e para inspecionar e modificar ativos prontos para produção quando você estiver depurando seu aplicativo.  
  
 Confira aqui mais informações sobre os tipos de ativos com os quais você pode trabalhar [!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
### <a name="images-and-textures"></a>Imagens e texturas  
 Imagens e texturas fornecem cor e detalhes visuais em jogos e aplicativos. Em gráficos 3D, as texturas vêm em diversos formatos, tipos e geometrias para dar suporte a diferentes usos. Por exemplo, mapas normais fornecem superfície por pixel normal para uma iluminação mais detalhada dos modelos 3D, e mapas de cubo fornecem textura em todas as direções para utilizações como conversão boxing do céu, reflexos e mapeamento da textura esférica. As texturas podem fornecer minimapas para dar suporte à renderização eficiente em níveis diferentes de detalhe e podem oferecer suporte a canais de cores diferentes e ordenações de cor. As texturas podem ser armazenadas em vários formatos compactados que ocupam menos memória gráfica dedicada e ajudam os GPUs a acessar texturas com mais eficiência.  
  
 Use o Editor de Imagens do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com imagens e texturas em muitos tipos e formatos comuns.  
  
### <a name="3-d-models"></a>Modelos 3 D  
 Os modelos 3D criam espaço e forma em jogos e aplicativos. No mínimo, os modelos codificam a posição de pontos no espaço 3D — que são conhecidos como *vértices*— junto com os dados de indexação para definir linhas ou triângulos que representam a forma do modelo. É possível associar dados adicionais a esses vértices — por exemplo, informações de cores, vetores normais ou atributos específicos ao aplicativo. Cada modelo também pode definir atributos de todo o objeto — por exemplo, qual sombreador é usado para calcular a aparência da superfície do objeto ou qual textura é aplicada a ele.  
  
 Use o Editor de Modelo do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com modelos 3D em vários formatos comuns.  
  
### <a name="shaders"></a>Sombreadores  
 Sombreadores são programas pequenos específicos ao domínio executados em uma GPU (unidade de processamento gráfico). Os sombreadores determinam como os modelos 3D são transformados em formas na tela e como cada pixel nessas formas é colorido. Ao criar um sombreador e aplicá-lo a um objeto em seu jogo ou aplicativo, você pode dar ao objeto uma aparência exclusiva.  
  
 Use o Designer de Sombreador do [!INCLUDE[vsprvs](../includes/vsprvs-md.md)], que é uma ferramenta de design de sombreador baseada em grafo, para criar efeitos visuais personalizados sem conhecer programação em HLSL.  
  
> [!NOTE]
>  Para saber mais sobre como iniciar a programação em DirectX, consulte [DirectX](http://go.microsoft.com/fwlink/p/?LinkId=224633). Para saber mais sobre como depurar um aplicativo baseado no DirectX, consulte [Diagnóstico de gráficos (Depuração de gráficos DirectX)](../debugger/visual-studio-graphics-diagnostics.md).  
  
## <a name="directx-version-compatibility"></a>Compatibilidade de versão do DirectX  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] usa o DirectX para renderizar ativos 2D e 3D. Selecione o renderizador do DirectX 11, ou o renderizador de software WARP (Windows Advanced Rasterization Platform). O renderizador do DirectX 11 fornece renderização acelerada por hardware de alto desempenho em GPUs do DirectX 11 e do DirectX 10. O renderizador WARP ajuda a garantir que seus ativos funcionem muitos computadores — incluindo computadores que não possuem hardware de gráfico moderno e computadores com hardware de gráfico integrado. Para saber mais sobre WARP, consulte [Guia do WARP (Windows Advanced Rasterization Platform)](http://go.microsoft.com/fwlink/p/?LinkId=224634).  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
|Título|Descrição|  
|-----------|-----------------|  
|[Trabalhando com texturas e imagens](../designers/working-with-textures-and-images.md)|Descreve como usar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com imagens e texturas.|  
|[Trabalhando com modelos 3D](../designers/working-with-3-d-models.md)|Descreve como usar o [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para trabalhar com modelos 3D.|  
|[Trabalhando com sombreadores](../designers/working-with-shaders.md)|Descreve como usar o Designer de sombrador [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] para criar e modificar efeitos de sombreamento personalizado.|  
|[Usando ativos 3D no jogo ou no aplicativo](../designers/using-3-d-assets-in-your-game-or-app.md)|Descreve como usar ativos, que você criou usando o Editor de Imagens, o Editor de Modelo ou o Designer de Sombreador, em seu jogo ou aplicativo.|



