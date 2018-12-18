---
title: Como criar um modelo 3D básico | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a0d97966-2df8-449b-a8cf-5a19684dc773
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 83d4069135adf37156457321b8ce15a254c9c27b
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49825485"
---
# <a name="how-to-create-a-basic-3-d-model"></a>Como criar um modelo 3D básico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento demonstra como usar o Editor de Modelo para criar um modelo 3D básico.  
  
 Este documento demonstra essas atividades:  
  
-   Adicionar objetos a uma cena  
  
-   Selecionar faces e bordas  
  
-   Converter seleções  
  
-   Uso das ferramentas **Subdivide a face** e **Extrudar face**  
  
-   Uso do comando **Triangular**  
  
## <a name="creating-a-basic-3-d-model"></a>Criando um modelo 3D básico  
 Você pode usar o Editor de Modelo para criar e modificar modelos e cenas 3D para seu jogo ou aplicativo. As etapas a seguir mostram como usar o Editor de Modelo para criar um modelo 3D simplificado de uma casa. Um modelo simplificado pode ser usado como um substituto para ativos de arte final que ainda estão sendo criados, como uma malha para detecção de colisão ou como um modelo de nível baixo de detalhes a ser usado quando o objeto que ele representa está muito longe tirar proveito de uma renderização mais detalhada.  
  
 Ao terminar, o modelo deve ter esta aparência:  
  
 ![O modelo concluído da casa simplificada](../designers/media/gfx-model-demo-house-final.png "gfx_model_demo_house_final")  
  
 Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.  
  
#### <a name="to-create-a-simplified-3-d-model-of-a-house"></a>Para criar um modelo 3D simplificado de uma casa  
  
1. Crie um modelo 3D com o qual trabalhar. Para obter informações sobre como adicionar um modelo ao seu projeto, consulte a seção de Introdução em [Editor de Modelo](../designers/model-editor.md).  
  
2. Adicione um cubo para a cena. Na janela **Caixa de Ferramentas**, em **Formas**, selecione **Cubo** e mova-o para a superfície de design.  
  
3. Mude para seleção de face. Na barra de ferramentas do Editor de Modelo, escolha **Selecionar Face**.  
  
4. Subdivida a parte superior do cubo. No modo de seleção de face, escolha o cubo uma vez para ativá-lo para a seleção e, em seguida, escolha a parte superior do cubo para selecionar a face superior. Na barra de ferramentas do Editor de Modelo, escolha **Subdivide a face**. Isso adiciona novos vértices na parte superior do cubo que o dividem em quatro partições de tamanhos iguais.  
  
    ![A parte superior do cubo foi subdividida](../designers/media/gfx-model-demo-house-subdiv.png "gfx_model_demo_house_subdiv")  
  
5. Faça a extrusão de dois lados adjacentes do cubo, por exemplo, a frente e o lado direito do cubo. No modo de seleção de face, escolha uma vez o cubo para ativá-lo para a seleção e, em seguida, escolha um lado do cubo. Pressione e mantenha a tecla Control pressionada, escolha outro lado do cubo que seja adjacente ao lado que foi selecionado primeiro e, em seguida, na barra de ferramentas do Editor de Modelo, escolha **Extrudar face**.  
  
    ![Os lados do cubo foram extrudados](../designers/media/gfx-model-demo-house-extrude.png "gfx_model_demo_house_extrude")  
  
6. Estenda uma das extrusões. Escolha uma as faces que você acabou de extrudar e, na barra de ferramentas do Editor de Modelo, escolha a ferramenta **Mover** e mova o manipulador de movimento na mesma direção da extrusão.  
  
    ![Um lado do cubo foi ainda mais extrudado.](../designers/media/gfx-model-demo-house-extend.png "gfx_model_demo_house_extend")  
  
7. Triangular o modelo. Na barra de ferramentas do Editor de Modelo, escolha **Avançado**, **Ferramentas** e **Triangular**.  
  
8. Crie o teto da casa. Mude para o modo de seleção de borda escolhendo **Selecionar Borda** na barra de ferramentas do Editor de Modelo e, em seguida, escolha o cubo para ativá-lo. Pressione e mantenha a tecla Control pressionada enquanto seleciona as bordas que são mostradas aqui:  
  
    ![As bordas que formarão o cume do telhado](../designers/media/gfx-model-demo-house-edges.png "gfx_model_demo_house_edges")  
  
    Com as bordas selecionadas, na barra de ferramentas do Editor de Modelo, escolha a ferramenta **Mover** e, em seguida, mova o manipulador de movimento para cima a fim de criar o telhado da casa.  
  
   O modelo de casa simplificada está concluído. Aqui está o modelo final novamente, com sombreamento simples aplicado:  
  
   ![O modelo concluído da casa simplificada](../designers/media/gfx-model-demo-house-final.png "gfx_model_demo_house_final")  
  
   Como uma próxima etapa, você pode aplicar um sombreador a esse modelo 3D. Para obter mais informações, consulte [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como modelar terreno 3D](../designers/how-to-model-3-d-terrain.md)   
 [Editor de Modelo](../designers/model-editor.md)   
 [Designer de Sombreador](../designers/shader-designer.md)



