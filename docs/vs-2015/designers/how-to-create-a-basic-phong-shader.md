---
title: Como criar um sombreador Phong básico | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c7c69da8-142b-4d3b-9be9-4be0d5970b25
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: ddb8f32cbf23184da140c3426e88c1f622dea1b7
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49832674"
---
# <a name="how-to-create-a-basic-phong-shader"></a>Como criar um sombreador Phong básico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento demonstra como usar o Designer de Sombreador e o DGSL (Directed Graph Shader Language) para criar um sombreador de iluminação que implementa o modelo de iluminação de Phong clássico.  
  
 Este documento demonstra essas atividades:  
  
-   Adicionar nós a um grafo de sombreador  
  
-   Desconectar nós  
  
-   Conectar nós  
  
## <a name="the-phong-lighting-model"></a>O modelo de iluminação de Phong  
 O modelo de iluminação de Phong amplia o modelo de iluminação de Lambert para incluir o realce especular, que simula as propriedades de reflexão de uma superfície. O componente especular fornece iluminação adicional das mesmas fontes de luz direcionais que são usadas no modelo de iluminação Lambert, mas sua contribuição para a cor final é processada de forma diferente. O realce especular afeta cada superfície na cena de forma diferente, com base na relação entre a direção da exibição, a direção das fontes de luz e a orientação da superfície. É um produto da cor especular, do potencial de reflexão e da orientação da superfície e a cor, intensidade e direção das fontes de luz. As superfícies que refletem a fonte de luz diretamente no visualizador recebem a contribuição especular máxima e as superfícies que refletem a fonte de luz distante do visualizador não recebem nenhuma contribuição. No modelo de iluminação de Phong, um ou mais componentes especulares são combinados para determinar a cor e a intensidade do realce especular para cada ponto no objeto e, em seguida, são adicionados ao resultado do modelo de iluminação de Lambert para produzir a cor final do pixel.  
  
 Para obter mais informações sobre o modelo de iluminação de Lambert, consulte [Como criar um sombreador Lambert básico](../designers/how-to-create-a-basic-lambert-shader.md).  
  
 Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.  
  
#### <a name="to-create-a-phong-shader"></a>Para criar um sombreador Phong  
  
1. Crie um sombreador Lambert, conforme descrito em [Como criar um sombreador Lambert básico](../designers/how-to-create-a-basic-lambert-shader.md).  
  
2. Desconecte o nó **Lambert** do nó **Cor Final**. Escolha o terminal **RGB** do nó **Lambert** e, em seguida, escolha **Quebrar Links**. Isso abre o espaço para o nó que será adicionado na próxima etapa.  
  
3. Adicione um nó **Adicionar** ao grafo. Na **Caixa de Ferramentas**, em **Matemática**, selecione **Adicionar** e mova-a para a superfície de design.  
  
4. Adicione um nó **Especular** ao gráfico. Na **Caixa de Ferramentas**, em **Utilitário**, selecione **Especular** e mova-o para a superfície de design.  
  
5. Adicione a contribuição especular. Mova o terminal de **Saída** do nó **Especular** para o terminal **X** do nó **Adicionar** e, em seguida, mova o terminal de **Saída** do nó **Lambert** para o terminal **Y** do nó **Adicionar**. Essas conexões combinam as contribuições de cor difusa e especular totais para o pixel.  
  
6. Conecte o valor de cor calculado à cor final. Mova o terminal de **Saída** do nó **Adicionar** para o terminal **RGB** do nó **Cor Final**.  
  
   A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a um modelo de bule.  
  
> [!NOTE]
>  Para demonstrar melhor o efeito do sombreador nesta ilustração, foi especificada uma cor laranja usando o parâmetro **MaterialDiffuse** do sombreador e foi especificado um acabamento de aparência metálica usando os parâmetros **MaterialSpecular** e **MaterialSpecularPower**. Para obter informações sobre parâmetros de material, consulte a seção Visualização de Sombreadores em [Designer de Sombreador](../designers/shader-designer.md).  
  
 ![Grafo de sombreador e uma visualização de seu efeito](../designers/media/digit-lighting-graph.png "Digit-Lighting-Graph")  
  
 Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter mais informações sobre como visualizar sombreadores no Designer de Sombreador, consulte a seção Visualização de Sombreadores em [Designer de Sombreador](../designers/shader-designer.md)  
  
 A ilustração a seguir mostra o sombreador que é descrito neste documento, aplicado a um modelo 3D. A propriedade **MaterialSpecular** foi definida como (1,00, 0,50, 0,20, 0,00) e sua propriedade **MaterialSpecularPower** foi definida como 16.  
  
> [!NOTE]
>  A propriedade **MaterialSpecular** determina o acabamento aparente do material da superfície. Uma superfície brilhante como vidro ou plástico tende a apresentar uma cor especular com uma tonalidade clara de branco. Uma superfície metálica tende a apresentar uma cor especular próxima de sua cor difusa. Uma superfície de acabamento acetinado tende a apresentar uma cor especular com um tom de cinza escuro.  
>   
>  A propriedade **MaterialSpecularPower** determina a intensidade dos realces especulares. Alta potência especular simula realces mais opacos e localizados. A potência especular muito baixa simula realces intensos e abrangentes que podem saturar e ocultar a cor da superfície inteira.  
  
 ![Iluminação de Phong aplicada a um modelo](../designers/media/digit-lighting-model.png "Digit-Lighting-Model")  
  
 Para obter mais informações sobre como aplicar um sombreador a um modelo 3D, consulte [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)   
 [Como exportar um sombreador](../designers/how-to-export-a-shader.md)   
 [Como criar um sombreador Lambert básico](../designers/how-to-create-a-basic-lambert-shader.md)   
 [Designer de Sombreador](../designers/shader-designer.md)   
 [Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)



