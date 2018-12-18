---
title: Desenhe as formas e demarcadores
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: d5378c59-e2e5-49f0-91f1-aa82d984a33c
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 97172253a088be86f20fae77fe62d01330a3b801
ms.sourcegitcommit: 206e738fc45ff8ec4ddac2dd484e5be37192cfbd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39513085"
---
# <a name="draw-shapes-and-paths"></a>Desenhe as formas e demarcadores

No Designer XAML, uma *forma* é exatamente o que se espera que seja. Por exemplo: um retângulo, um círculo ou uma elipse. Um *caminho* é uma versão mais flexível de uma forma. É possível reformatar ou combiná-los para obter novas formas.

Formas e caminhos usam gráficos vetoriais, portanto, eles se adaptam bem a exibições de alta resolução. Caso queira saber mais sobre gráficos vetoriais, consulte [O que são Gráficos Vetoriais](https://www.youtube.com/watch?v=MoCSwF0n-io) ou [gráficos vetoriais](http://www.webopedia.com/TERM/V/vector_graphics.html).

##  <a name="Shape"></a> Desenhar uma forma
 É possível encontrar formas no painel **Ativos**.

 ![Categoria Formas no painel Ativos](../designers/media/b4_shapes_assetspanel.png)

 Arraste a forma desejada para a prancheta. Então, será possível usar identificadores na forma para ajustar a escala, girar, mover ou distorcer a forma.

 ![Alças](../designers/media/84261e83-3091-4490-ab58-4218b188439e.png)

##  <a name="Path"></a> Desenhar um caminho
 Um caminho é uma série de linhas e curvas conectadas. Use um caminho para criar formas interessantes que não estão disponíveis no painel **Ativos**.

 É possível desenhar um caminho usando uma linha, caneta ou lápis. Essas ferramentas podem ser encontradas no painel **Ferramentas**.

 ![Ferramenta Caneta](../designers/media/717956a8-b6a5-4e37-8af3-70bcfc78c82a.png) ![Opções da ferramenta Caneta](../designers/media/8fbbbb21-be83-4cf6-903b-3a49f00c9860.png)

### <a name="draw-a-straight-line"></a>Desenhar uma linha reta
 Use a ferramenta **Caneta** ![ferramenta Caneta](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png) ou a ferramenta **Linha** ![ferramenta Linha](../designers/media/eb618397-5283-48be-8396-3449be7b6fbf.png).

 **Usando a ferramenta Caneta** ![ferramenta Caneta](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png)

 Na prancheta, clique uma vez para definir o ponto inicial e, em seguida, clique novamente para definir o final da linha.

 **Usando a ferramenta Linha** ![ferramenta Linha](../designers/media/eb618397-5283-48be-8396-3449be7b6fbf.png)

 Na prancheta, arraste do ponto em que deseja que a linha se inicie e libere no ponto em que deseja que a linha termine.

### <a name="draw-a-curve"></a>Desenhar uma curva
 Use a ferramenta **Caneta** ![ferramenta Caneta](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png).

 Na prancheta, clique uma vez para definir o ponto inicial de uma linha e, em seguida, clique e arraste o ponteiro para criar a curva desejada.

 Se desejar fechar o caminho, clique no primeiro ponto da linha.

### <a name="change-the-shape-of-a-curve"></a>Alterar a forma de uma curva
 Use a ferramenta **Seleção direta** ![ferramenta Seleção direta](../designers/media/6dd6571f-c116-451d-8dd2-1f88b8406362.png).

 Clique na forma e, em seguida, arraste qualquer ponto na forma de alterar formas curvadas.

### <a name="draw-a-free-form-path"></a>Desenhar um demarcador de forma livre
 Use a ferramenta **Lápis** ![ferramenta Lápis](../designers/media/509dc167-734f-46c9-b012-987ee63450cd.png).

 Na prancheta, desenhe um caminho de forma livre, assim como com um lápis real.

### <a name="remove-part-of-a-path"></a>Remover parte de um caminho
 Use a ferramenta **Seleção direta** ![ferramenta Seleção direta](../designers/media/6dd6571f-c116-451d-8dd2-1f88b8406362.png).

 Selecione o caminho que contém o segmento que deseja excluir e, em seguida, clique no botão **Excluir**.

### <a name="remove-a-point-in-a-path"></a>Remover um ponto em um caminho
 Use a ferramenta **Seleção** ![ferramenta Seleção](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png) e a ferramenta **Caneta** ![ferramenta Caneta](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png).

 Use a ferramenta **Seleção** ![Ferramenta Seleção](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png) para selecionar o caminho. Em seguida, use a ferramenta **Caneta** ![ferramenta Caneta](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png) para clicar no ponto em que você deseja remover.

### <a name="add-a-point-to-a-path"></a>Adicionar um ponto a um caminho
 Use a ferramenta **Seleção** ![ferramenta Seleção](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png) e a ferramenta **Caneta** ![ferramenta Caneta](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png).

 Use a ferramenta **Seleção** ![Ferramenta Seleção](../designers/media/2ff91340-477e-4efa-a0f7-af20851e4daa.png) para selecionar o caminho. Use a ferramenta **Caneta** ![ferramenta Caneta](../designers/media/894f8612-e0ed-4e00-84cf-a9bc8f38fc54.png) para clicar em qualquer local do caminho em que deseja adicionar o ponto.

##  <a name="Convert"></a> Converter uma forma em um caminho
 Para modificar uma forma da mesma maneira que um caminho, converta a forma em um caminho.

 **Assista a um vídeo curto:** ![Configure installed features](../designers/media/bldadminconsoleinitialconfigicon.png) [Working with paths: Convert a shape to a path](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=147) (Configurar recursos instalados, Trabalhando com demarcadores: converter uma forma em um demarcador).

##  <a name="Combine"></a> Combinar caminhos
 É possível combinar caminhos e formas em um único caminho.

 ![Combinar caminhos](../designers/media/2df17a5d-a338-4ef4-96c5-dae51cc1ca8a.png)

|||||
|-|-|-|-|
|![Duas formas antes da combinação](../designers/media/b1_1.png)|Duas formas antes da combinação|![Interseção](../designers/media/b1_4.png)|Interseção|
|![Excluir sobreposição](../designers/media/b1_2.png)|União|![](../designers/media/b1_5.png)|Excluir Sobreposição|
|![Subtração](../designers/media/b1_3.png)|Divisão|![](../designers/media/b1_6.png)|Subtração|

 **Assista a um vídeo curto:** ![Configure installed features](../designers/media/bldadminconsoleinitialconfigicon.png) [Working with paths: Combine paths](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=195) (Configurar recursos instalados, Trabalhando com caminhos: combinar caminhos).

##  <a name="Compound"></a> Criar um caminho composto
 Quando você cria um caminho composto, todas as partes de interseção dos caminhos são subtraídas do resultado e o caminho resultante assume as propriedades visuais do caminho mais baixo.

 É possível separar um caminho composto a qualquer momento após sua criação.

 ![Interromper um demarcador composto](../designers/media/2157a8aa-d9a7-4de4-8de5-b10d28f08a84.png)

 **Assista a um vídeo curto:** ![Configure installed features](../designers/media/bldadminconsoleinitialconfigicon.png) [Working with paths: Create a compound path](https://www.youtube.com/watch?v=Io5bC0-nH6Q) (Configurar recursos instalados, Trabalhando com caminhos: criar um demarcador composto).

##  <a name="Clipping"></a> Criar um caminho de recorte
 Um caminho de recorte é um caminho ou uma forma que é aplicada a outro objeto, o que oculta as partes do objeto mascarado que fica fora do caminho de recorte.

 ![Demarcador de recorte](../designers/media/22471e98-a841-4f39-a3ef-36090cf5a625.png)

 **Assista a um vídeo curto:** ![Configure installed features](../designers/media/bldadminconsoleinitialconfigicon.png) [Working with paths: Create a clipping path](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=232) (Configurar recursos instalados, Trabalhando com demarcadores: criar um demarcador de recorte).

## <a name="see-also"></a>Consulte também

- [Criando uma interface do usuário usando o Blend for Visual Studio](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)