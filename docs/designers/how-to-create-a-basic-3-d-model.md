---
title: Como criar um modelo 3D básico
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: a0d97966-2df8-449b-a8cf-5a19684dc773
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 6242b80c1dcefe0e1a3a35561337a75e6098d25d
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49913436"
---
# <a name="how-to-create-a-basic-3d-model"></a>Como criar um modelo 3D básico

Este artigo demonstra como usar o Editor de Modelo para criar um modelo 3D básico. As seguintes atividades são abordadas:

-   Adicionar objetos a uma cena

-   Selecionar faces e bordas

-   Converter seleções

-   Uso das ferramentas **Subdivide a face** e **Extrudar face**

-   Uso do comando **Triangular**

## <a name="create-a-basic-3d-model"></a>Criar um modelo 3D básico
 Você pode usar o Editor de Modelo para criar e modificar modelos e cenas 3D para seu jogo ou aplicativo. As etapas a seguir mostram como usar o Editor de Modelos para criar um modelo 3D simplificado de uma casa. Um modelo simplificado pode ser usado como um substituto para ativos de arte final que ainda estão sendo criados, como uma malha para detecção de colisão ou como um modelo de nível baixo de detalhes a ser usado quando o objeto que ele representa está muito longe tirar proveito de uma renderização mais detalhada.

 Ao terminar, o modelo deve ter esta aparência:

 ![O modelo concluído da casa simplificada](../designers/media/gfx_model_demo_house_final.png)

 Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.

### <a name="to-create-a-simplified-3d-model-of-a-house"></a>Para criar um modelo 3D simplificado de uma casa

1. Crie um modelo 3D com o qual trabalhar. Para obter informações sobre como adicionar um modelo ao seu projeto, consulte a seção de Introdução em [Editor de Modelo](../designers/model-editor.md).

2. Adicione um cubo para a cena. Na janela **Caixa de Ferramentas**, em **Formas**, selecione **Cubo** e mova-o para a superfície de design.

3. Mude para seleção de face. Na barra de ferramentas do Editor de Modelo, escolha **Selecionar Face**.

4. Subdivida a parte superior do cubo. No modo de seleção de face, escolha o cubo uma vez para ativá-lo para a seleção e, em seguida, escolha a parte superior do cubo para selecionar a face superior. Na barra de ferramentas do Editor de Modelo, escolha **Subdivide a face**. Isso adiciona novos vértices na parte superior do cubo que o dividem em quatro partições de tamanhos iguais.

    ![A parte superior do cubo foi subdividida](../designers/media/gfx_model_demo_house_subdiv.png)

5. Faça a extrusão de dois lados adjacentes do cubo, por exemplo, a frente e o lado direito do cubo. No modo de seleção de face, escolha uma vez o cubo para ativá-lo para a seleção e, em seguida, escolha um lado do cubo. Pressione e segure a tecla **Ctrl**, escolha outro lado do cubo que seja adjacente ao lado que foi selecionado primeiro e na barra de ferramentas do Editor de Modelo, clique em **Extrudar face**.

    ![Os lados do cubo tiveram sido extrudados](../designers/media/gfx_model_demo_house_extrude.png)

6. Estenda uma das extrusões. Escolha uma as faces que você acabou de extrudar e, na barra de ferramentas do Editor de Modelo, escolha a ferramenta **Mover** e mova o manipulador de movimento na mesma direção da extrusão.

    ![Um lado do cubo foi extrudado mais ainda.](../designers/media/gfx_model_demo_house_extend.png)

7. Triangular o modelo. Na barra de ferramentas do Editor de Modelo, escolha **Avançado** > **Ferramentas** > **Triangular**.

8. Crie o teto da casa. Mude para o modo de seleção de borda escolhendo **Selecionar Borda** na barra de ferramentas do Editor de Modelo e, em seguida, escolha o cubo para ativá-lo. Pressione e segure a tecla **Ctrl** enquanto você seleciona as bordas que são mostradas aqui:

    ![As bordas que formarão o cume do telhado](../designers/media/gfx_model_demo_house_edges.png)

    Com as bordas selecionadas, na barra de ferramentas do Editor de Modelo, escolha a ferramenta **Mover** e, em seguida, mova o manipulador de movimento para cima a fim de criar o telhado da casa.

   O modelo de casa simplificada está concluído. Aqui está o modelo final novamente, com sombreamento simples aplicado:

   ![O modelo concluído da casa simplificada](../designers/media/gfx_model_demo_house_final.png)

   Como uma próxima etapa, você pode aplicar um sombreador a esse modelo 3D. Para obter informações, confira [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md).

## <a name="see-also"></a>Consulte também

- [Como modelar um terreno 3D](../designers/how-to-model-3-d-terrain.md)
- [Editor de modelos](../designers/model-editor.md)
- [Designer de sombreador](../designers/shader-designer.md)
