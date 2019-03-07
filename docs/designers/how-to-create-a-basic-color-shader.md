---
title: 'Como: Criar um sombreador de cores básico'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c301328a-079a-49e8-b688-4749c01657c0
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 858ea12709b187204cd1662d41b82266c99efc01
ms.sourcegitcommit: 21d667104199c2493accec20c2388cf674b195c3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2019
ms.locfileid: "55953471"
---
# <a name="how-to-create-a-basic-color-shader"></a>Como: Criar um sombreador de cores básico

Este artigo demonstra como usar o Designer de Sombreador e a DGSL (Directed Graph Shader Language) para criar um sombreador de cor simples. Esse sombreador define a cor final em um valor de cor RGB constante.

## <a name="create-a-flat-color-shader"></a>Criar um sombreador de cor simples

Você pode implementar um sombreador de cor simples gravando o valor de cor de uma constante de cor RGB na cor de saída final.

Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.

1.  Crie um sombreador DGSL com o qual trabalhar. Para obter informações sobre como adicionar um sombreador DGSL ao seu projeto, consulte a seção de Introdução em [Designer de Sombreador](../designers/shader-designer.md).

2.  Exclua o nó **Ponto de Cor**. Use a ferramenta **Selecionar** para selecionar o nó **Cor do Ponto** e, em seguida, na barra de menus, escolha **Editar** > **Excluir**.

3.  Adicione um nó **Constante de Cor** ao grafo. Na **Caixa de Ferramentas**, em **Constantes**, selecione **Constante de Cor** e mova para a superfície de design.

4.  Especifique um valor de cor para o nó **Constante de Cor**. Use a ferramenta **Selecionar** para selecionar o nó **Constante de Cor** e, em seguida, na janela **Propriedades**, na propriedade **Saída**, especifique um valor de cor. Para laranja, especifique um valor de (1,0, 0,5, 0,2, 1,0).

5.  Conecte a constante de cor à cor final. Para criar as conexões, mova o terminal **RGB** do nó **Constante de Cor** para o terminal **RGB** do nó **Cor Final** e, em seguida, mova o terminal **Alfa** do nó **Constante de Cor** para o terminal **Alfa** do nó **Cor Final**. Essas conexões definem a cor final para a constante de cor definida na etapa anterior.

A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a um cubo.

> [!NOTE]
> Na ilustração foi especificada uma cor laranja para demonstrar melhor o efeito do sombreador.

![Grafo de sombreador e seu resultado em um modelo 3D](../designers/media/digit-flat-color-effect.png)

Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter mais informações sobre como visualizar sombreadores no Designer de Sombreador, consulte [Designer de Sombreador](../designers/shader-designer.md).

## <a name="see-also"></a>Consulte também

- [Como: Aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)
- [Como: Exportar um sombreador](../designers/how-to-export-a-shader.md)
- [Designer de Sombreador](../designers/shader-designer.md)
- [Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)