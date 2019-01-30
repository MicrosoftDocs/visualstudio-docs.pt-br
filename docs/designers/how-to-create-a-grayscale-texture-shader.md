---
title: 'Como: Criar um sombreador de textura em escala de cinza'
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.topic: conceptual
ms.assetid: 79181d81-44af-445e-9a18-03483dd70260
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 58f6ca03a7bad27ad3c2cb4f7dae662e14292e95
ms.sourcegitcommit: 2193323efc608118e0ce6f6b2ff532f158245d56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55015495"
---
# <a name="how-to-create-a-grayscale-texture-shader"></a>Como: Criar um sombreador de textura em escala de cinza

Este artigo demonstra como usar o Designer de Sombreador e a DGSL (Directed Graph Shader Language) para criar um sombreador de textura em escala de cinza. Esse sombreador modifica o valor de cor RGB da amostra de textura e, em seguida, usa-o junto com o valor alfa inalterado para definir a cor final.

## <a name="create-a-grayscale-texture-shader"></a>Criar um sombreador de textura em escala de cinza

Você pode implementar um sombreador de textura em escala de cinza, modificando o valor de cor de uma amostra de textura antes de gravá-lo na cor de saída final.

Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.

1.  Crie um sombreador de textura básica, conforme descrito em [Como: Criar um sombreador de textura básica](../designers/how-to-create-a-basic-texture-shader.md).

2.  Desconecte o terminal **RGB** do nó **Amostra de Textura** do terminal **RGB** do nó **Cor Final**. No modo de **Seleção**, escolha o terminal **RGB** do nó **Amostra de Textura** e, em seguida, escolha **Quebrar Links**. Isso abre o espaço para o nó que será adicionado na próxima etapa.

3.  Adicione um nó **Remover Saturação** ao grafo. Na **Caixa de Ferramentas**, em **Filtros**, selecione **Remover Saturação** e mova-o para a superfície de design.

4.  Calcule o valor de escala de cinza usando o nó **Remover Saturação**. No modo de **Seleção**, mova o terminal **RGB** do nó **Amostra de Textura** para o terminal **RGB** do nó **Remover Saturação**.

    > [!NOTE]
    > Por padrão, o nó **Remover Saturação** remove totalmente a saturação da cor de entrada e usa os pesos de luminância padrão para a conversão em escala de cinza. Você pode alterar como o nó **Remover Saturação** se comporta, alterando o valor da propriedade **Luminância** ou removendo apenas parcialmente a saturação da cor de entrada. Para remover parcialmente a saturação da cor de entrada, forneça um valor escalar no intervalo [0,1) para o terminal **Porcentagem** do nó **Remover Saturação**.

5.  Conecte o valor de cor em escala de cinza à cor final. Mova o terminal de **Saída** do nó **Remover Saturação** para o terminal **RGB** do nó **Cor Final**.

A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a um cubo.

> [!NOTE]
> Nesta ilustração foi usado um plano como a forma de visualização e foi especificada uma textura para demonstrar melhor o efeito do sombreador.

![Grafo de sombreador e uma versão prévia de seu efeito](../designers/media/digit-grayscale-effect.png)

Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter mais informações sobre a visualização de sombreadores no Designer de Sombreador, consulte [Designer de Sombreador](../designers/shader-designer.md)

## <a name="see-also"></a>Consulte também

- [Como: Aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)
- [Como: Exportar um sombreador](../designers/how-to-export-a-shader.md)
- [Editor de Imagens](../designers/image-editor.md)
- [Designer de Sombreador](../designers/shader-designer.md)
- [Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)