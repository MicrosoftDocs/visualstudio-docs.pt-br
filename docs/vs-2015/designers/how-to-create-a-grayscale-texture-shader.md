---
title: Como criar um sombreador de textura em escala de cinza | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 79181d81-44af-445e-9a18-03483dd70260
caps.latest.revision: 20
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 046ae16670edaebb44986dee34ea086b4129a0a3
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49922335"
---
# <a name="how-to-create-a-grayscale-texture-shader"></a>Como criar um sombreador de textura em escala de cinza
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento demonstra como usar o Designer de Sombreador e a DGSL (Directed Graph Shader Language) para criar um sombreador de textura em escala de cinza. Esse sombreador modifica o valor de cor RGB da amostra de textura e, em seguida, usa-o junto com o valor alfa inalterado para definir a cor final.  
  
## <a name="creating-a-grayscale-texture-shader"></a>Criar um sombreador de textura em escala de cinza  
 Você pode implementar um sombreador de textura em escala de cinza, modificando o valor de cor de uma amostra de textura antes de gravá-lo na cor de saída final.  
  
 Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.  
  
#### <a name="to-create-a-grayscale-texture-shader"></a>Para criar um sombreador de textura em escala de cinza  
  
1. Crie um sombreador de textura básico, conforme descrito em [Como criar um sombreador de textura básico](../designers/how-to-create-a-basic-texture-shader.md).  
  
2. Desconecte o terminal **RGB** do nó **Amostra de Textura** do terminal **RGB** do nó **Cor Final**. No modo de **Seleção**, escolha o terminal **RGB** do nó **Amostra de Textura** e, em seguida, escolha **Quebrar Links**. Isso abre o espaço para o nó que será adicionado na próxima etapa.  
  
3. Adicione um nó **Remover Saturação** ao grafo. Na **Caixa de Ferramentas**, em **Filtros**, selecione **Remover Saturação** e mova-o para a superfície de design.  
  
4. Calcule o valor de escala de cinza usando o nó **Remover Saturação**. No modo de **Seleção**, mova o terminal **RGB** do nó **Amostra de Textura** para o terminal **RGB** do nó **Remover Saturação**.  
  
   > [!NOTE]
   >  Por padrão, o nó **Remover Saturação** remove totalmente a saturação da cor de entrada e usa os pesos de luminância padrão para a conversão em escala de cinza. Você pode alterar como o nó **Remover Saturação** se comporta, alterando o valor da propriedade **Luminância** ou removendo apenas parcialmente a saturação da cor de entrada. Para remover parcialmente a saturação da cor de entrada, forneça um valor escalar no intervalo [0,1) para o terminal **Porcentagem** do nó **Remover Saturação**.  
  
5. Conecte o valor de cor em escala de cinza à cor final. Mova o terminal de **Saída** do nó **Remover Saturação** para o terminal **RGB** do nó **Cor Final**.  
  
   A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a um cubo.  
  
> [!NOTE]
>  Nesta ilustração foi usado um plano como a forma de visualização e foi especificada uma textura para demonstrar melhor o efeito do sombreador.  
  
 ![Grafo de sombreador e uma visualização de seu efeito](../designers/media/digit-grayscale-effect.png "Digit-Grayscale-Effect")  
  
 Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter mais informações sobre a visualização de sombreadores no Designer de Sombreador, consulte [Designer de Sombreador](../designers/shader-designer.md)  
  
## <a name="see-also"></a>Consulte também  
 [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)   
 [Como exportar um sombreador](../designers/how-to-export-a-shader.md)   
 [Editor de imagens](../designers/image-editor.md)   
 [Designer de Sombreador](../designers/shader-designer.md)   
 [Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)



