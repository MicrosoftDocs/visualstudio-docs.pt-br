---
title: Como modificar o ponto dinâmico de um modelo 3D
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: c20b4ec8-29f5-4ca5-bc39-d4548ca6f573
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 352685e6b31aa688ff51f9564f141fa800c348d8
ms.sourcegitcommit: e5a382de633156b85b292f35e3d740f817715d47
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38977806"
---
# <a name="how-to-modify-the-pivot-point-of-a-3d-model"></a>Como modificar o ponto dinâmico de um modelo 3D

Este artigo demonstra como usar o Editor de Modelo para modificar o *ponto dinâmico* de um modelo 3D. O ponto dinâmico é o ponto no espaço que define o centro matemático do objeto para rotação e colocação em escala.

## <a name="modify-the-pivot-point-of-a-3d-model"></a>Modificar o ponto dinâmico de um modelo 3D

Você pode redefinir a origem de um modelo 3D ao modificar seu ponto dinâmico.

Verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.

1.  Comece com um modelo 3D existente, como aquele descrito em [Como criar um modelo 3D básico](../designers/how-to-create-a-basic-3-d-model.md).

2.  Entre no modo dinâmico. Na barra de ferramentas do **Modo do Editor de Modelo**, escolha o **Modo Dinâmico** para ativar o modo dinâmico. Será exibida uma caixa ao redor do botão **Modo Dinâmico** para indicar que o Editor de Modelo agora está em modo dinâmico. No modo dinâmico, operações como a movimentação afetam o ponto dinâmico do objeto em vez da estrutura do objeto no espaço de mundo.

3.  Modificar o ponto dinâmico do objeto. No modo de **Seleção**, selecione o objeto e, em seguida, na barra de ferramentas do **Visualizador de Modelo**, escolha a ferramenta **Mover**. Uma caixa, que representa o ponto dinâmico, aparece na superfície de design. Mova a caixa para modificar o ponto dinâmico do objeto.

     Ao mover a caixa, você pode mover o ponto dinâmico em todas as três dimensões. Para mover o ponto dinâmico em um eixo, mova a seta que corresponde ao eixo. A caixa e as setas alteram para uma cor amarela para indicar o eixo que é afetado pela translação.

     Você também pode especificar o ponto dinâmico usando a propriedade **Translação do Pivô** na janela **Propriedades**.

    > [!TIP]
    > Você pode exibir o efeito do novo ponto dinâmico, girando o objeto. Para girá-lo, use a ferramenta **Girar** ou modifique a propriedade **Rotação**.

Aqui está um modelo que tem um ponto dinâmico modificado:

![Um modelo de uma casa com um ponto dinâmico modificado](../designers/media/digit-modified-model.png)

## <a name="see-also"></a>Consulte também

- [Como criar um modelo 3D básico](../designers/how-to-create-a-basic-3-d-model.md)
- [Editor de modelos](../designers/model-editor.md)