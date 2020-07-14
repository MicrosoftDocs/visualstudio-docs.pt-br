---
title: Desenhe as formas e demarcadores
titleSuffix: Blend for Visual Studio
ms.date: 07/31/2019
ms.topic: conceptual
ms.assetid: d5378c59-e2e5-49f0-91f1-aa82d984a33c
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b87ed03c8f513f6a9a750186d8763e56061bed98
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85350817"
---
# <a name="draw-shapes-and-paths"></a>Desenhe as formas e demarcadores

No Designer XAML, uma *forma* é exatamente o que se espera que seja. Por exemplo: um retângulo, um círculo ou uma elipse. Um *caminho* é uma versão mais flexível de uma forma. É possível reformatar ou combiná-los para obter novas formas.

Formas e caminhos usam gráficos vetoriais, portanto, eles se adaptam bem a exibições de alta resolução.

## <a name="draw-a-shape"></a>Desenhar uma forma

Encontre formas na janela **Ativos**.

![Categoria Formas na janela Ativos](media/blend-shapes.png)

Arraste a forma desejada para a prancheta. Em seguida, use as alças da forma para ajustar a escala, girar, mover ou distorcer a forma.

![Alças](../designers/media/84261e83-3091-4490-ab58-4218b188439e.png)

## <a name="draw-a-path"></a>Desenhar um caminho

Um caminho é uma série de linhas e curvas conectadas. Use um caminho para criar formas interessantes que não estejam disponíveis na janela **Ativos**.

É possível desenhar um caminho usando uma linha, caneta ou lápis. Essas ferramentas podem ser encontradas na janela **Ferramentas**.

### <a name="draw-a-straight-line"></a>Desenhar uma linha reta

Use a ferramenta **Caneta** ou a ferramenta **Linha**.

**Usar a ferramenta Caneta**

Na prancheta, clique uma vez para definir o ponto inicial e, em seguida, clique novamente para definir o final da linha.

**Usar a ferramenta Linha**

Na prancheta, arraste do ponto em que deseja que a linha se inicie e libere no ponto em que deseja que a linha termine.

### <a name="draw-a-curve"></a>Desenhar uma curva

Use a ferramenta **Caneta**.

Na prancheta, clique uma vez para definir o ponto inicial de uma linha e, em seguida, clique e arraste o ponteiro para criar a curva desejada.

Se desejar fechar o caminho, clique no primeiro ponto da linha.

### <a name="change-the-shape-of-a-curve"></a>Alterar a forma de uma curva

Use a ferramenta **Seleção Direta**.

Clique na forma e, em seguida, arraste qualquer ponto na forma de alterar formas curvadas.

### <a name="draw-a-free-form-path"></a>Desenhar um demarcador de forma livre

Use a ferramenta **Lápis**.

Na prancheta, desenhe um caminho de forma livre, assim como com um lápis real.

### <a name="remove-part-of-a-path"></a>Remover parte de um caminho

Use a ferramenta **Seleção Direta**.

Selecione o caminho que contém o segmento que deseja excluir e, em seguida, clique no botão **Excluir**.

### <a name="remove-a-point-in-a-path"></a>Remover um ponto em um caminho

Use a ferramenta **Seleção** para selecionar o caminho. Em seguida, use a ferramenta **Caneta** para clicar no ponto a ser removido.

### <a name="add-a-point-to-a-path"></a>Adicionar um ponto a um caminho

Use a ferramenta **Seleção** para selecionar o caminho. Use a ferramenta **Caneta** para clicar em qualquer local do caminho em que deseja adicionar o ponto.

## <a name="convert-a-shape-to-a-path"></a>Converter uma forma em um caminho

Para modificar uma forma da mesma maneira que um caminho, converta a forma em um caminho. Selecione a forma e, em seguida, selecione **Formatar**  >  **caminho**  >  **converter em demarcador**.

**Assista a um vídeo curto:** ![Configure installed features](../designers/media/bldadminconsoleinitialconfigicon.png) [Working with paths: Convert a shape to a path](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=147) (Configurar recursos instalados, Trabalhando com demarcadores: converter uma forma em um demarcador).

> [!NOTE]
> Atualmente, a opção **Converter em Caminho** não está disponível para aplicativos UWP que tenham no mínimo a `TargetPlatformVersion` 10.0.16299.0 ou posterior.

## <a name="combine-paths"></a>Combinar demarcadores

É possível combinar caminhos e formas em um único caminho.

![Combinar demarcadores](../designers/media/2df17a5d-a338-4ef4-96c5-dae51cc1ca8a.png)

|Número|Ação|
|-|-|
|![Duas formas antes da combinação](../designers/media/b1_1.png)|Duas formas antes da combinação|
|![União](../designers/media/b1_2.png)|União|
|![Dividir](../designers/media/b1_3.png)|Dividir|
|![Intersect](../designers/media/b1_4.png)|Intersect|
|![Excluir sobreposição](../designers/media/b1_5.png)|Excluir Sobreposição|
|![Subtrair](../designers/media/b1_6.png)|Subtrair|

**Assista a um vídeo curto:** ![Configure installed features](../designers/media/bldadminconsoleinitialconfigicon.png) [Working with paths: Combine paths](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=195) (Configurar recursos instalados, Trabalhando com caminhos: combinar caminhos).

## <a name="create-a-compound-path"></a>Criar um demarcador composto

Quando você cria um caminho composto, todas as partes de interseção dos caminhos são subtraídas do resultado e o caminho resultante assume as propriedades visuais do caminho mais baixo.

É possível separar um caminho composto a qualquer momento após sua criação.

![Interromper um demarcador composto](../designers/media/2157a8aa-d9a7-4de4-8de5-b10d28f08a84.png)

**Assista a um vídeo curto:** ![Configure installed features](../designers/media/bldadminconsoleinitialconfigicon.png) [Working with paths: Create a compound path](https://www.youtube.com/watch?v=Io5bC0-nH6Q) (Configurar recursos instalados, Trabalhando com caminhos: criar um demarcador composto).

## <a name="create-a-clipping-path"></a>Criar um demarcador de recorte

Um caminho de recorte é um caminho ou uma forma que é aplicada a outro objeto, o que oculta as partes do objeto mascarado que fica fora do caminho de recorte.

![Demarcador de recorte](../designers/media/22471e98-a841-4f39-a3ef-36090cf5a625.png)

**Assista a um vídeo curto:** ![Configure installed features](../designers/media/bldadminconsoleinitialconfigicon.png) [Working with paths: Create a clipping path](https://www.youtube.com/watch?v=Io5bC0-nH6Q#t=232) (Configurar recursos instalados, Trabalhando com demarcadores: criar um demarcador de recorte).
