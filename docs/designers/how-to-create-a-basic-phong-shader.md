---
title: Como criar um sombreador Phong básico
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: c7c69da8-142b-4d3b-9be9-4be0d5970b25
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 718607d74be1a74a799f8de9f4883e1df9fb7ef5
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769181"
---
# <a name="how-to-create-a-basic-phong-shader"></a>Como criar um sombreador Phong básico

Este artigo demonstra como usar o Designer de Sombreador e o DGSL (Directed Graph Shader Language) para criar um sombreador de iluminação que implementa o modelo de iluminação de Phong clássico.

## <a name="the-phong-lighting-model"></a>O modelo de iluminação de Phong

O modelo de iluminação de Phong amplia o modelo de iluminação de Lambert para incluir o realce especular, que simula as propriedades de reflexão de uma superfície. O componente especular fornece iluminação adicional das mesmas fontes de luz direcionais que são usadas no modelo de iluminação Lambert, mas sua contribuição para a cor final é processada de forma diferente. O realce especular afeta cada superfície na cena de forma diferente, com base na relação entre a direção da exibição, a direção das fontes de luz e a orientação da superfície. É um produto da cor especular, do potencial de reflexão e da orientação da superfície e a cor, intensidade e direção das fontes de luz. As superfícies que refletem a fonte de luz diretamente no visualizador recebem a contribuição especular máxima e as superfícies que refletem a fonte de luz distante do visualizador não recebem nenhuma contribuição. No modelo de iluminação de Phong, um ou mais componentes especulares são combinados para determinar a cor e a intensidade do realce especular para cada ponto no objeto e, em seguida, são adicionados ao resultado do modelo de iluminação de Lambert para produzir a cor final do pixel.

Para obter mais informações sobre o modelo de iluminação de Lambert, confira [Como criar um sombreador Lambert básico](../designers/how-to-create-a-basic-lambert-shader.md).

Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.

1. Criar um sombreador Lambert, conforme descrito em [Como criar um sombreador Lambert básico](../designers/how-to-create-a-basic-lambert-shader.md).

2. Desconecte o nó **Lambert** do nó **Cor Final**. Escolha o terminal **RGB** do nó **Lambert** e, em seguida, escolha **Quebrar Links**. Isso abre o espaço para o nó que será adicionado na próxima etapa.

3. Adicione um nó **Adicionar** ao grafo. Na **Caixa de Ferramentas**, em **Matemática**, selecione **Adicionar** e mova-a para a superfície de design.

4. Adicione um nó **Especular** ao gráfico. Na **Caixa de Ferramentas**, em **Utilitário**, selecione **Especular** e mova-o para a superfície de design.

5. Adicione a contribuição especular. Mova o terminal de **Saída** do nó **Especular** para o terminal **X** do nó **Adicionar** e, em seguida, mova o terminal de **Saída** do nó **Lambert** para o terminal **Y** do nó **Adicionar**. Essas conexões combinam as contribuições de cor difusa e especular totais para o pixel.

6. Conecte o valor de cor calculado à cor final. Mova o terminal de **Saída** do nó **Adicionar** para o terminal **RGB** do nó **Cor Final**.

   A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a um modelo de bule.

> [!NOTE]
> Para demonstrar melhor o efeito do sombreador nesta ilustração, foi especificada uma cor laranja usando o parâmetro **MaterialDiffuse** do sombreador e foi especificado um acabamento de aparência metálica usando os parâmetros **MaterialSpecular** e **MaterialSpecularPower**. Para obter informações sobre parâmetros de material, consulte a seção Visualização de Sombreadores em [Designer de Sombreador](../designers/shader-designer.md).

![Grafo de sombreador e uma versão prévia de seu efeito](../designers/media/digit-lighting-graph.png)

Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter mais informações sobre como Visualizar sombreadores no designer do sombreador, consulte a seção visualizações de sombreadores no [Designer de sombreador](../designers/shader-designer.md)

A ilustração a seguir mostra o sombreador que é descrito neste documento, aplicado a um modelo 3D. A propriedade **MaterialSpecular** foi definida como (1,00, 0,50, 0,20, 0,00) e sua propriedade **MaterialSpecularPower** foi definida como 16.

> [!NOTE]
> A propriedade **MaterialSpecular** determina o acabamento aparente do material da superfície. Uma superfície brilhante como vidro ou plástico tende a apresentar uma cor especular com uma tonalidade clara de branco. Uma superfície metálica tende a apresentar uma cor especular próxima de sua cor difusa. Uma superfície de acabamento acetinado tende a apresentar uma cor especular com um tom de cinza escuro.
>
> A propriedade **MaterialSpecularPower** determina a intensidade dos realces especulares. Alta potência especular simula realces mais opacos e localizados. A potência especular muito baixa simula realces intensos e abrangentes que podem saturar e ocultar a cor da superfície inteira.

![Iluminação Phong aplicada a um modelo](../designers/media/digit-lighting-model.png)

Para obter mais informações de como aplicar um sombreador a um modelo 3D, confira [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md).

## <a name="see-also"></a>Confira também

- [Como: aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)
- [Como: exportar um sombreador](../designers/how-to-export-a-shader.md)
- [Como criar um sombreador Lambert básico](../designers/how-to-create-a-basic-lambert-shader.md)
- [Designer de sombreador](../designers/shader-designer.md)
- [Nós do designer do sombreador](../designers/shader-designer-nodes.md)
