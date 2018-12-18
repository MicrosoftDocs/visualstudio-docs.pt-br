---
title: Como criar um sombreador de gradiente com base na geometria | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4b204405-ba95-4c5e-bd51-ec033a3ebfb6
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 61dd80bb8d8ba4c272beff018d3ab65ffce41dc6
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49911870"
---
# <a name="how-to-create-a-geometry-based-gradient-shader"></a>Como criar um sombreador de gradiente com base na geometria
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento demonstra como usar o Designer de Sombreador e a Directed Graph Shader Language para criar um sombreador de gradiente com base na geometria. Esse sombreador ajusta a escala de um valor de cor RGB constante pela altura de cada ponto de um objeto no espaço de mundo.  
  
 Este documento demonstra essas atividades:  
  
-   Adicionar nós a um grafo de sombreador  
  
-   Configurar propriedades de nó  
  
-   Desconectar nós  
  
-   Conectar nós  
  
## <a name="creating-a-geometry-based-gradient-shader"></a>Criar um sombreador de gradiente com base na geometria  
 Você pode implementar um sombreador com base na geometria, incorporando a posição do pixel ao sombreador. Em linguagens de sombreamento, um pixel contém mais informações do que apenas a cor e o local em uma tela 2D. Um pixel, conhecido como um *fragmento* em alguns sistemas, é uma coleção de valores que descrevem a superfície que corresponde a um pixel. O sombreador descrito neste documento utiliza a altura de cada pixel de um objeto 3D no espaço de mundo para afetar a cor de saída final do fragmento.  
  
 Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.  
  
#### <a name="to-create-a-geometry-based-gradient-shader"></a>Para criar um sombreador de gradiente com base na geometria  
  
1. Crie um sombreador DGSL com o qual trabalhar. Para obter informações sobre como adicionar um sombreador DGSL ao seu projeto, consulte a seção de Introdução em [Designer de Sombreador](../designers/shader-designer.md).  
  
2. Desconectar o nó **Ponto de Cor** do nó **Cor Final**. Escolha o terminal **RGB** do nó **Ponto de Cor** e, em seguida, escolha **Quebrar Links**. Isso abre o espaço para o nó que será adicionado na próxima etapa.  
  
3. Adicione um nó **Multiplicar** ao grafo. Na **Caixa de Ferramentas**, em **Matemática**, selecione **Multiplicar** e mova-a para a superfície de design.  
  
4. Adicionar um nó **Vetor de Máscara** ao grafo. Na **Caixa de Ferramentas**, em **Utilitário**, selecione **Vetor de Máscara** e mova-o para a superfície de design.  
  
5. Especifique os valores de máscara para o nó **Vetor de Máscara**. No modo de **Seleção**, selecione o nó **Vetor de Máscara** e, em seguida, na janela **Propriedades**, defina a propriedade **Verde / Y** como **Verdadeiro** e, em seguida, defina as propriedades **Vermelho / X**, **Azul / Z** e **Alfa / W** como **Falso**. Neste exemplo, as propriedades **Vermelho / X**, **Verde / Y** e **Azul / Z** correspondem aos componentes x, y e z do nó **Posição do Mundo** e **Alfa / W** não é usada. Como somente **Verde / Y** está definido como **Verdadeiro**, apenas o componente y do vetor de entrada permanecerá depois que ele for mascarado.  
  
6. Adicione um nó **Posição do Mundo** ao grafo. Na **Caixa de Ferramentas**, em **Constantes**, selecione **Posição do Mundo** e mova para a superfície de design.  
  
7. Mascarar a posição do espaço de mundo do fragmento. No modo de **Seleção**, mova o terminal de **Saída** do nó **Posição do Mundo** para o terminal **Vetor** do nó **Vetor de Máscara**. Essa conexão mascara a posição do fragmento para ignorar os componentes x e z.  
  
8. Multiplique a constante de cor RGB pela posição de espaço de mundo mascarada. Mova o terminal **RGB** do nó **Ponto de Cor** para o terminal **Y** do nó **Multiplicar** e, em seguida, mova o terminal de **Saída** do nó **Vetor de Máscara** para o terminal **X** do nó **Multiplicar**. Essa conexão ajusta a escala do valor de cor pela altura do pixel no espaço de mundo.  
  
9. Conecte o valor de cor ajustado à cor final. Mova o terminal de **Saída** do nó **Multiplicar** para o terminal **RGB** do nó **Cor Final**.  
  
   A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a uma esfera.  
  
> [!NOTE]
>  Nesta ilustração é especificada uma cor laranja para demonstrar melhor o efeito do sombreador, mas como a forma de visualização não tem posição no espaço de mundo, o sombreador não pode ser visualizado totalmente no Designer de Sombreador. O sombreador deve ser visualizado em uma cena real para demonstrar o efeito completo.  
  
 ![Grafo de sombreador e uma visualização de seu efeito](../designers/media/digit-gradient-effect-graph.png "Digit-Gradient-Effect-Graph")  
  
 Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter informações sobre como visualizar sombreadores no Designer de Sombreador, consulte **Visualização de Sombreadores** em [Designer de Sombreador](../designers/shader-designer.md)  
  
 A ilustração a seguir mostra o sombreador que é descrito neste documento, aplicado a uma cena 3D que é demonstrada em [Como modelar terreno 3D](../designers/how-to-model-3-d-terrain.md). A intensidade da cor aumenta com a altura do ponto no mundo.  
  
 ![Efeito de gradiente aplicado a um modelo de terreno 3D](../designers/media/digit-gradient-effect-result.png "Digit-Gradient-Effect-Result")  
  
 Para obter mais informações sobre como aplicar um sombreador a um modelo 3D, consulte [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)   
 [Como exportar um sombreador](../designers/how-to-export-a-shader.md)   
 [Como modelar terreno 3D](../designers/how-to-model-3-d-terrain.md)   
 [Como criar um sombreador de textura em escala de cinza](../designers/how-to-create-a-grayscale-texture-shader.md)   
 [Designer de Sombreador](../designers/shader-designer.md)   
 [Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)



