---
title: Como modificar o ponto dinâmico de um modelo 3D | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c20b4ec8-29f5-4ca5-bc39-d4548ca6f573
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: beba04bab85b3fd09aafb195039ad6e34106e293
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49850523"
---
# <a name="how-to-modify-the-pivot-point-of-a-3-d-model"></a>Como modificar o ponto dinâmico de um modelo 3D
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento demonstra como usar o Editor de Modelo para modificar o *ponto dinâmico* de um modelo 3D. O ponto dinâmico é o ponto no espaço que define o centro matemático do objeto para rotação e colocação em escala.  
  
 Este documento demonstra esta atividade:  
  
-   Modificar o ponto dinâmico de um objeto  
  
## <a name="modifying-the-pivot-point-of-a-3-d-model"></a>Modificar o ponto dinâmico de um modelo 3D  
 Você pode redefinir a origem de um modelo 3D ao modificar seu ponto dinâmico.  
  
 Verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.  
  
#### <a name="to-modify-the-pivot-point-of-a-3-d-model"></a>Para modificar o ponto dinâmico de um modelo 3D  
  
1. Comece com um modelo 3D existente, como o que é descrito em [Como criar um modelo 3D básico](../designers/how-to-create-a-basic-3-d-model.md).  
  
2. Entre no modo dinâmico. Na barra de ferramentas do **Modo do Editor de Modelo**, escolha o **Modo Dinâmico** para ativar o modo dinâmico. Será exibida uma caixa ao redor do botão **Modo Dinâmico** para indicar que o Editor de Modelo agora está em modo dinâmico. No modo dinâmico, operações como a movimentação afetam o ponto dinâmico do objeto em vez da estrutura do objeto no espaço de mundo.  
  
3. Modificar o ponto dinâmico do objeto. No modo de **Seleção**, selecione o objeto e, em seguida, na barra de ferramentas do **Visualizador de Modelo**, escolha a ferramenta **Mover**. Uma caixa, que representa o ponto dinâmico, aparece na superfície de design. Mova a caixa para modificar o ponto dinâmico do objeto.  
  
    Ao mover a caixa, você pode mover o ponto dinâmico em todas as três dimensões. Para mover o ponto dinâmico em um eixo, mova a seta que corresponde ao eixo. A caixa e as setas alteram para uma cor amarela para indicar o eixo que é afetado pela translação.  
  
    Você também pode especificar o ponto dinâmico usando a propriedade **Translação do Pivô** na janela **Propriedades**.  
  
   > [!TIP]
   >  Você pode exibir o efeito do novo ponto dinâmico, girando o objeto. Para girá-lo, use a ferramenta **Girar** ou modifique a propriedade **Rotação**.  
  
   Aqui está um modelo que tem um ponto dinâmico modificado:  
  
   ![Um modelo de uma casa com um ponto dinâmico modificado](../designers/media/digit-modified-model.png "Digit-Modified-Model")  
  
## <a name="see-also"></a>Consulte também  
 [Como criar um modelo 3D básico](../designers/how-to-create-a-basic-3-d-model.md)   
 [Editor de modelo](../designers/model-editor.md)



