---
title: 'Como: Criar um sombreador Phong básico'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c7c69da8-142b-4d3b-9be9-4be0d5970b25
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 131afbaf4fcbdf5456a6276a36c551a47b663eec
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55926132"
---
# <a name="how-to-create-a-basic-phong-shader"></a>Como: Criar um sombreador Phong básico

Este artigo demonstra como usar o Designer de Sombreador e o DGSL (Directed Graph Shader Language) para criar um sombreador de iluminação que implementa o modelo de iluminação de Phong clássico.

## <a name="the-phong-lighting-model"></a>O modelo de iluminação de Phong

O modelo de iluminação de Phong amplia o modelo de iluminação de Lambert para incluir o realce especular, que simula as propriedades de reflexão de uma superfície. O componente especular fornece iluminação adicional das mesmas fontes de luz direcionais que são usadas no modelo de iluminação Lambert, mas sua contribuição para a cor final é processada de forma diferente. O realce especular afeta cada superfície na cena de forma diferente, com base na relação entre a direção da exibição, a direção das fontes de luz e a orientação da superfície. É um produto da cor especular, do potencial de reflexão e da orientação da superfície e a cor, intensidade e direção das fontes de luz. As superfícies que refletem a fonte de luz diretamente no visualizador recebem a contribuição especular máxima e as superfícies que refletem a fonte de luz distante do visualizador não recebem nenhuma contribuição. No modelo de iluminação de Phong, um ou mais componentes especulares são combinados para determinar a cor e a intensidade do realce especular para cada ponto no objeto e, em seguida, são adicionados ao resultado do modelo de iluminação de Lambert para produzir a cor final do pixel.

Para obter mais informações sobre o modelo de iluminação de Lambert, confira [Como: Criar um sombreador Lambert básico](../designers/how-to-create-a-basic-lambert-shader.md).

Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.

1. Crie um sombreador Lambert básico, conforme descrito em [Como: Criar um sombreador Lambert básico](../designers/how-to-create-a-basic-lambert-shader.md).

2. Desconecte o nó **Lambert** do nó **Cor Final**. Escolha o terminal **RGB** do nó **Lambert** e, em seguida, escolha **Quebrar Links**. Isso abre o espaço para o nó que será adicionado na próxima etapa.

3. Adicione um nó **Adicionar** ao grafo. Na **Caixa de Ferramentas**, em **Matemática**, selecione **Adicionar** e mova-a para a superfície de design.

4. Adicione um nó **Especular** ao gráfico. Na **Caixa de Ferramentas**, em **Utilitário**, selecione **Especular** e mova-o para a superfície de design.

5. Adicione a contribuição especular. Mova o terminal de **Saída** do nó **Especular** para o terminal **X** do nó **Adicionar** e, em seguida, mova o terminal de **Saída** do nó **Lambert** para o terminal **Y** do nó **Adicionar**. Essas conexões combinam as contribuições de cor difusa e especular totais para o pixel.

6. Conecte o valor de cor calculado à cor final. Mova o terminal de **Saída** do nó **Adicionar** para o terminal **RGB** do nó **Cor Final**.

   A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a um modelo de bule.

> [!NOTE]
> Para demonstrar melhor o efeito do sombreador nesta ilustração, foi especificada uma cor laranja usando o parâmetro **MaterialDiffuse** do sombreador e foi especificado um acabamento de aparência metálica usando os parâmetros **MaterialSpecular** e **MaterialSpecularPower**. Para obter informações sobre parâmetros de material, consulte a seção Visualização de Sombreadores em [Designer de Sombreador](../designers/shader-designer.md).

 ![Grafo de sombreador e uma versão prévia de seu efeito](../designers/media/digit-lighting-graph.png)

 Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter mais informações sobre como visualizar sombreadores no Designer de Sombreador, consulte a seção Visualização de Sombreadores em [Designer de Sombreador](../designers/shader-designer.md)

 A ilustração a seguir mostra o sombreador que é descrito neste documento, aplicado a um modelo 3D. A propriedade **MaterialSpecular** foi definida como (1,00, 0,50, 0,20, 0,00) e sua propriedade **MaterialSpecularPower** foi definida como 16.

> [!NOTE]
> A propriedade **MaterialSpecular** determina o acabamento aparente do material da superfície. Uma superfície brilhante como vidro ou plástico tende a apresentar uma cor especular com uma tonalidade clara de branco. Uma superfície metálica tende a apresentar uma cor especular próxima de sua cor difusa. Uma superfície de acabamento acetinado tende a apresentar uma cor especular com um tom de cinza escuro.
>
> A propriedade **MaterialSpecularPower** determina a intensidade dos realces especulares. Alta potência especular simula realces mais opacos e localizados. A potência especular muito baixa simula realces intensos e abrangentes que podem saturar e ocultar a cor da superfície inteira.

 ![Iluminação Phong aplicada a um modelo](../designers/media/digit-lighting-model.png)

 Para obter mais informações sobre como aplicar um sombreador a um modelo 3D, confira [Como: Aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md).

## <a name="see-also"></a>Consulte também

- [Como: Aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)
- [Como: Exportar um sombreador](../designers/how-to-export-a-shader.md)
- [Como: Criar um sombreador Lambert básico](../designers/how-to-create-a-basic-lambert-shader.md)
- [Designer de Sombreador](../designers/shader-designer.md)
- [Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)