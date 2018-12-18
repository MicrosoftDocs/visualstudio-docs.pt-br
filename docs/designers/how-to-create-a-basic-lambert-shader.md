---
title: Como criar um sombreador Lambert básico
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: ec5c10fb-9600-4240-8280-d59451ea1d68
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 7d71a59e0173be60779675f838fad20943eabc85
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49913248"
---
# <a name="how-to-create-a-basic-lambert-shader"></a>Como criar um sombreador Lambert básico

Este artigo demonstra como usar o Designer de Sombreador e o DGSL (Directed Graph Shader Language) para criar um sombreador de iluminação que implementa o modelo de iluminação de Lambert clássico.

## <a name="the-lambert-lighting-model"></a>O modelo de iluminação de Lambert

O modelo de iluminação de Lambert incorpora iluminação ambiente e direcional para sombrear objetos em uma cena 3D. Os componentes do ambiente fornecem um nível básico de iluminação na cena 3D. Os componentes direcionais fornecem iluminação adicional de fontes de luz direcionais (distantes). A iluminação ambiente afeta todas as superfícies da cena igualmente, independentemente da orientação. Para uma determinada superfície, é um produto da cor ambiente da superfície e a cor e a intensidade da luz ambiente na cena. A iluminação direcional afeta cada superfície na cena de maneira diferente, com base na orientação da superfície em relação a direção da fonte de luz. É um produto da cor difusa e a orientação da superfície e a cor, intensidade e direção das fontes de luz. As superfícies que estão voltadas diretamente para a fonte de luz recebem a contribuição máxima e superfícies que estão diretamente voltadas para o lado oposto, não recebem nenhuma contribuição. No modelo de iluminação de Lambert, o componente ambiente e um ou mais componentes direcionais são combinados para determinar a contribuição de cor difusa total para cada ponto no objeto.

Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.

1. Crie um sombreador DGSL com o qual trabalhar. Para obter informações sobre como adicionar um sombreador DGSL ao seu projeto, consulte a seção de Introdução em [Designer de Sombreador](../designers/shader-designer.md).

2. Desconectar o nó **Ponto de Cor** do nó **Cor Final**. Escolha o terminal **RGB** do nó **Ponto de Cor** e, em seguida, escolha **Quebrar Links**. Deixe o terminal **Alfa** conectado.

3. Adicione um nó **Lambert** ao grafo. Na **Caixa de Ferramentas**, em **Utilitário**, selecione **Lambert** e mova-o para a superfície de design. O nó Lambert calcula a contribuição de cor difusa total do pixel, com base em parâmetros de iluminação difusa e ambiente.

4. Conecte o nó **Ponto de Cor** ao nó **Lambert**. No modo de **Seleção**, mova o terminal **RGB** do nó **Ponto de Cor** para o terminal **Cor Difusa** do nó **Lambert**. Essa conexão fornece o nó Lambert com a cor difusa interpolada do pixel.

5. Conecte o valor de cor calculado à cor final. Mova o terminal de **Saída** do nó **Lambert** para o terminal **RGB** do nó **Cor Final**.

   A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a um modelo de bule.

> [!NOTE]
> Para demonstrar melhor o efeito do sombreador nesta ilustração, foi especificada uma cor laranja usando o parâmetro **MaterialDiffuse** do sombreador. Um jogo ou um aplicativo pode usar esse parâmetro para fornecer um valor de cor exclusivo para cada objeto. Para obter informações sobre parâmetros de material, consulte a seção Visualização de Sombreadores em [Designer de Sombreador](../designers/shader-designer.md).

 ![O grafo de sombreador e uma versão prévia de seu efeito.](../designers/media/digit-lambert-effect-graph.png)

 Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter mais informações sobre como visualizar sombreadores no Designer de Sombreador, consulte a seção Visualização de Sombreadores em [Designer de Sombreador](../designers/shader-designer.md).

 A ilustração a seguir mostra o sombreador que é descrito neste documento, aplicado a um modelo 3D.

 ![Iluminação Lambert aplicada a um modelo.](../designers/media/digit-lambert-effect-result.png)

 Para obter mais informações sobre como aplicar um sombreador a um modelo 3D, consulte [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md).

## <a name="see-also"></a>Consulte também

- [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)
- [Como exportar um sombreador](../designers/how-to-export-a-shader.md)
- [Como criar um sombreador Phong básico](../designers/how-to-create-a-basic-phong-shader.md)
- [Designer de Sombreador](../designers/shader-designer.md)
- [Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)