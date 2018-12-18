---
title: Desenhe as formas e caminhos | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d5378c59-e2e5-49f0-91f1-aa82d984a33c
caps.latest.revision: 12
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 0f59ecbdf9e69093d5c445cdb6d4780eb3b6f86e
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49188168"
---
# <a name="draw-shapes-and-paths"></a>Desenhe as formas e demarcadores
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

No Designer XAML, uma *forma* é exatamente o que você espera. Por exemplo: um retângulo, um círculo ou uma elipse. Um *caminho* é uma versão mais flexível de uma forma. É possível reformatar ou combiná-los para obter novas formas.  
  
 Formas e caminhos usam gráficos vetoriais, portanto, eles se adaptam bem a exibições de alta resolução. Caso queira saber mais sobre gráficos vetoriais, consulte [O que são Gráficos Vetoriais](https://www.youtube.com/watch?v=MoCSwF0n-io) ou [gráficos vetoriais](http://www.webopedia.com/TERM/V/vector_graphics.html).  
  
 **Neste tópico:**  
  
-   [Desenhar uma forma](#Shape)  
  
-   [Desenhar um caminho](#Path)  
  
-   [Converter uma forma em um caminho](#Convert)  
  
-   [Combinar caminhos](#Combine)  
  
-   [Criar um caminho composto](#Compound)  
  
-   [Criar um caminho de recorte](#Clipping)  
  
##  <a name="Shape"></a> Desenhar uma forma  
 É possível encontrar formas no painel **Ativos**.  
  
 ![Categoria Formas no painel Ativos](../designers/media/b4-shapes-assetspanel.png "b4_Shapes_AssetsPanel")  
  
 Arraste a forma desejada para a prancheta. Então, será possível usar identificadores na forma para ajustar a escala, girar, mover ou distorcer a forma.  
  
 ![](../designers/media/84261e83-3091-4490-ab58-4218b188439e.png "84261e83-3091-4490-ab58-4218b188439e")  
  
##  <a name="Path"></a> Desenhar um caminho  
 Um caminho é uma série de linhas e curvas conectadas. Use um caminho para criar formas interessantes que não estão disponíveis no painel **Ativos**.  
  
 É possível desenhar um caminho usando uma linha, caneta ou lápis. Essas ferramentas podem ser encontradas no painel **Ferramentas**.  
  
 ![](../designers/media/717956a8-b6a5-4e37-8af3-70bcfc78c82a.png "717956a8-b6a5-4e37-8af3-70bcfc78c82a") ![](../designers/media/8fbbbb21-be83-4cf6-903b-3a49f00c9860.png "8fbbbb21-be83-4cf6-903b-3a49f00c9860")  
  
### <a name="draw-a-straight-line"></a>Desenhar uma linha reta  
 Use a ferramenta **Caneta** ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54") ou a ferramenta **Linha** ![](../designers/media/eb618397-5283-48be-8396-3449be7b6fbf.png "eb618397-5283-48be-8396-3449be7b6fbf").  
  
 **Usando a ferramenta Caneta** ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54")  
  
 Na prancheta, clique uma vez para definir o ponto inicial e, em seguida, clique novamente para definir o final da linha.  
  
 **Usando a ferramenta Linha** ![](../designers/media/eb618397-5283-48be-8396-3449be7b6fbf.png "eb618397-5283-48be-8396-3449be7b6fbf")  
  
 Na prancheta, arraste do ponto em que deseja que a linha se inicie e libere no ponto em que deseja que a linha termine.  
  
### <a name="draw-a-curve"></a>Desenhar uma curva  
 Use a ferramenta **Caneta** ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54").  
  
 Na prancheta, clique uma vez para definir o ponto inicial de uma linha e, em seguida, clique e arraste o ponteiro para criar a curva desejada.  
  
 Se desejar fechar o caminho, clique no primeiro ponto da linha.  
  
### <a name="change-the-shape-of-a-curve"></a>Alterar a forma de uma curva  
 Use a ferramenta **Seleção direta** ![](../designers/media/6dd6571f-c116-451d-8dd2-1f88b8406362.png "6dd6571f-c116-451d-8dd2-1f88b8406362").  
  
 Clique na forma e, em seguida, arraste qualquer ponto na forma de alterar formas curvadas.  
  
### <a name="draw-a-free-form-path"></a>Desenhar um demarcador de forma livre  
 Use a ferramenta **Lápis** ![](../designers/media/509dc167-734f-46c9-b012-987ee63450cd.png "509dc167-734f-46c9-b012-987ee63450cd").  
  
 Na prancheta, desenhe um caminho de forma livre, assim como com um lápis real.  
  
### <a name="remove-part-of-a-path"></a>Remover parte de um caminho  
 Use a ferramenta **Seleção direta** ![](../designers/media/6dd6571f-c116-451d-8dd2-1f88b8406362.png "6dd6571f-c116-451d-8dd2-1f88b8406362").  
  
 Selecione o caminho que contém o segmento que deseja excluir e, em seguida, clique no botão **Excluir**.  
  
### <a name="remove-a-point-in-a-path"></a>Remover um ponto em um caminho  
 Use a ferramenta **Seleção** ![](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png "2ff91340-477e-4efa-a0f7-af20851e4daa") e a ferramenta **Caneta** ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54").  
  
 Use a ferramenta **Seleção** ![](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png "2ff91340-477e-4efa-a0f7-af20851e4daa") para selecionar o caminho. Em seguida, use a ferramenta **Caneta** ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54") para clicar no ponto que você deseja remover.  
  
### <a name="add-a-point-to-a-path"></a>Adicionar um ponto a um caminho  
 Use a ferramenta **Seleção** ![](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png "2ff91340-477e-4efa-a0f7-af20851e4daa") e a ferramenta **Caneta** ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54").  
  
 Use a ferramenta **Seleção** ![](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png "2ff91340-477e-4efa-a0f7-af20851e4daa") para selecionar o caminho. Use a ferramenta **Caneta** ![](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png "894f8612-e0ed-4e00-84cf-a9bc8f38fc54") para clicar em qualquer local do caminho em que você deseja adicionar o ponto.  
  
##  <a name="Convert"></a> Converter uma forma em um caminho  
 Para modificar uma forma da mesma maneira que um caminho, converta a forma em um caminho.  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Trabalhando com caminhos: converter uma forma em um caminho](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=147).  
  
##  <a name="Combine"></a> Combinar caminhos  
 É possível combinar caminhos e formas em um único caminho.  
  
 ![](../designers/media/2df17a5d-a338-4ef4-96c5-dae51cc1ca8a.png "2df17a5d-a338-4ef4-96c5-dae51cc1ca8a")  
  
|||||  
|-|-|-|-|  
|![](../designers/media/b1-1.png "B1_1")|Duas formas antes da combinação|![](../designers/media/b1-4.png "B1_4")|Interseção|  
|![](../designers/media/b1-2.png "B1_2")|União|![](../designers/media/b1-5.png "B1_5")|Excluir Sobreposição|  
|![](../designers/media/b1-3.png "B1_3")|Divisão|![](../designers/media/b1-6.png "B1_6")|Subtração|  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Trabalhando com caminhos: combinar caminhos](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=195).  
  
##  <a name="Compound"></a> Criar um caminho composto  
 Quando você cria um caminho composto, todas as partes de interseção dos caminhos são subtraídas do resultado e o caminho resultante assume as propriedades visuais do caminho mais baixo.  
  
 É possível separar um caminho composto a qualquer momento após sua criação.  
  
 ![](../designers/media/2157a8aa-d9a7-4de4-8de5-b10d28f08a84.png "2157a8aa-d9a7-4de4-8de5-b10d28f08a84")  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Trabalhando com caminhos: criar um caminho composto](https://www.youtube.com/watch?v=Io5bC0-nH6Q).  
  
##  <a name="Clipping"></a> Criar um caminho de recorte  
 Um caminho de recorte é um caminho ou uma forma que é aplicada a outro objeto, o que oculta as partes do objeto mascarado que fica fora do caminho de recorte.  
  
 ![](../designers/media/22471e98-a841-4f39-a3ef-36090cf5a625.png "22471e98-a841-4f39-a3ef-36090cf5a625")  
  
 **Assista a um breve vídeo:** ![Configurar Recursos Instalados](../designers/media/bldadminconsoleinitialconfigicon.PNG "BldAdminConsoleInitialConfigIcon") [Trabalhando com caminhos: criar um caminho de recorte](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=232).  
  
## <a name="see-also"></a>Consulte também  
 [Criando uma interface do usuário usando o Blend for Visual Studio](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)



