---
title: Como modelar terreno 3D | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f779b1fd-82a9-4a11-8ab7-c1c9caabc883
caps.latest.revision: 19
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: fae94fe5e7474580f8867f531fc41d0ce6781cf8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49940509"
---
# <a name="how-to-model-3-d-terrain"></a>Como modelar terreno 3D
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento demonstra como usar o Editor de Modelo para criar um modelo de terreno 3D.  
  
 Este documento demonstra essas atividades:  
  
-   Adicionar objetos a uma cena  
  
-   Selecionar faces e pontos  
  
-   Converter seleções  
  
-   Usando a ferramenta **Subdivide a face**  
  
-   Enquadrar um objeto na superfície de design  
  
## <a name="creating-a-3-d-terrain-model"></a>Criar um modelo de terreno 3D  
 Você pode criar um terreno 3D subdividindo um plano para fazer faces adicionais e, em seguida, manipular seus vértices para criar características de terreno interessantes.  
  
 Ao terminar, o modelo deve ter esta aparência:  
  
 ![Cena 3D que mostra um modelo de terreno](../designers/media/digit-terrain-model.png "Digit-Terrain-Model")  
  
 Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.  
  
#### <a name="to-create-a-3-d-terrain-model"></a>Para criar um modelo de terreno 3D  
  
1. Crie um modelo 3D com o qual trabalhar. Para obter informações sobre como adicionar um modelo ao seu projeto, consulte a seção de Introdução em [Editor de Modelo](../designers/model-editor.md).  
  
2. Adicione um plano para a cena. Na **Caixa de Ferramentas**, em **Formas**, selecione **Plano** e mova-o para a superfície de design.  
  
   > [!TIP]
   >  Para facilitar o trabalho com o objeto de plano, você pode enquadrá-lo na superfície de design. No modo de **Seleção**, selecione o objeto de plano e, em seguida, na barra de ferramentas do Editor de Modelo, escolha o botão **Enquadrar Objeto**.  
  
3. Entre no modo de seleção de face. Na barra de ferramentas do Editor de Modelo, escolha **Selecionar Face**.  
  
4. Subdivida o plano. No modo de seleção de face, escolha o plano uma vez para ativá-lo para a seleção e, em seguida, escolha-o novamente para selecionar a sua única face. Na barra de ferramentas do Editor de Modelo, escolha **Subdivide a face**. Isso adiciona novos vértices ao plano dividindo-o em quatro partições de tamanhos iguais.  
  
5. Crie mais subdivisões. Com as novas faces ainda selecionadas, escolha **Subdivide a face** mais duas vezes. Isso cria um total de 64 faces. Ao criar mais subdivisões, você pode dar mais detalhes ao terreno.  
  
6. Entre no modo de seleção de ponto. Na barra de ferramentas do Editor de Modelo, escolha **Selecionar Ponto**.  
  
7. Modifique um ponto para criar um recurso de terreno. No modo de seleção de ponto, selecione um dos pontos e, em seguida, na barra de ferramentas do Editor de Modelo, escolha a ferramenta **Mover**. Uma caixa que representa o ponto aparece na superfície de design. Use a seta verde para mover a caixa e, assim, modificar a altura do ponto. Repita essa etapa para diferentes pontos a fim de criar características interessantes de terreno.  
  
   > [!TIP]
   >  Você pode selecionar vários pontos de uma vez para modificá-los de maneira uniforme.  
  
   O modelo de terreno está concluído. Aqui está o modelo final novamente, com sombreamento Phong aplicado:  
  
   ![Cena 3D que mostra um modelo de terreno](../designers/media/digit-terrain-model.png "Digit-Terrain-Model")  
  
   Você pode usar esse modelo de terreno para demonstrar o efeito do sombreador de gradiente descrito em [Como criar um sombreador de gradiente com base na geometria](../designers/how-to-create-a-geometry-based-gradient-shader.md).  
  
## <a name="see-also"></a>Consulte também  
 [Editor de modelo](../designers/model-editor.md)



