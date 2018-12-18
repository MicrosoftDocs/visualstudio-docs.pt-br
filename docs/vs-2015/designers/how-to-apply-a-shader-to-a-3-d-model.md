---
title: Como aplicar um sombreador a um modelo 3D | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a3877bd6-abd8-4a9d-842c-6848b6c2f335
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 804e7c0a2e7a9a710071cc6050249bf408bc8230
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49862836"
---
# <a name="how-to-apply-a-shader-to-a-3-d-model"></a>Como aplicar um sombreador a um modelo 3-D
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento demonstra como usar o Editor de Modelos para aplicar um sombreador DGSL (Directed Graph Shader Language) a um modelo 3D.  
  
 Este documento demonstra esta atividade:  
  
-   Aplicar um sombreador a um modelo 3D  
  
## <a name="applying-a-shader-to-a-3-d-model"></a>Aplicar um sombreador a um modelo 3D  
 Você pode aplicar um efeito de sombreador a um modelo 3D para dar a ele uma aparência interessante.  
  
 Antes de começar, verifique se a janela **Propriedades** está sendo exibida.  
  
#### <a name="to-apply-a-shader-to-a-3-d-model"></a>Para aplicar um sombreador a um modelo 3D  
  
1. Comece com uma cena 3D que contém um ou mais modelos. Se você não tiver uma cena 3D adequada, crie uma conforme descrito em [Como criar um modelo 3D básico](../designers/how-to-create-a-basic-3-d-model.md). Você também precisa ter um sombreador DGSL que possa aplicar ao modelo. Se não tiver um sombreador adequado, crie um conforme descrito em [Como criar um sombreador de cor básico](../designers/how-to-create-a-basic-color-shader.md) e salve-o em um arquivo antes de continuar.  
  
2. No modo **Selecionar**, selecione o modelo ao qual deseja aplicar o sombreador e, na janela **Propriedades**, na propriedade **Nome do Arquivo** do grupo de propriedades **Efeito**, especifique o sombreador DGSL que deseja aplicar ao modelo.  
  
   Este é um modelo ao qual o efeito de cor básico foi aplicado:  
  
   ![Cena 3D que mostra o efeito de cor básico](../designers/media/digit-3d-model-effect.png "Digit-3D-Model-Effect")  
  
   Depois de aplicar um sombreador a um modelo, você pode abri-lo no Designer de Sombreador selecionando o modelo e, em seguida, na janela **Propriedades**, na propriedade **(Avançado)** do grupo de propriedades **Efeito**, escolha o botão de reticências (**...** ).  
  
## <a name="see-also"></a>Consulte também  
 [Como criar um modelo 3D básico](../designers/how-to-create-a-basic-3-d-model.md)   
 [Como criar um sombreador de cor básico](../designers/how-to-create-a-basic-color-shader.md)   
 [Editor de Modelo](../designers/model-editor.md)   
 [Designer de Sombreador](../designers/shader-designer.md)



