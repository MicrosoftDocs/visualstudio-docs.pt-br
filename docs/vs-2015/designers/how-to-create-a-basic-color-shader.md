---
title: 'Como: Criar um sombreador de cor básico | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: c301328a-079a-49e8-b688-4749c01657c0
caps.latest.revision: 26
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: b1e202f84fb3b4e0e865e2cebb96b6728289ff6b
ms.sourcegitcommit: 8b538eea125241e9d6d8b7297b72a66faa9a4a47
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54774108"
---
# <a name="how-to-create-a-basic-color-shader"></a>Como criar um sombreador de cor básico
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento demonstra como usar o Designer de Sombreador e a DGSL (Directed Graph Shader Language) para criar um sombreador de cor simples. Esse sombreador define a cor final em um valor de cor RGB constante.  
  
 Este documento demonstra essas atividades:  
  
-   Remover nós de um grafo  
  
-   Adicionar nós a um grafo  
  
-   Configurar propriedades de nó  
  
-   Conectar nós  
  
## <a name="creating-a-flat-color-shader"></a>Criar um sombreador de cor simples  
 Você pode implementar um sombreador de cor simples gravando o valor de cor de uma constante de cor RGB na cor de saída final.  
  
 Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.  
  
#### <a name="to-create-a-flat-color-shader"></a>Para criar um sombreador de cor simples  
  
1. Crie um sombreador DGSL com o qual trabalhar. Para obter informações sobre como adicionar um sombreador DGSL ao seu projeto, consulte a seção de Introdução em [Designer de Sombreador](../designers/shader-designer.md).  
  
2. Exclua o nó **Ponto de Cor**. Use a ferramenta **Selecionar** para selecionar o nó **Ponto de Cor** e, em seguida, na barra de menus, escolha **Editar** e **Excluir**.  
  
3. Adicione um nó **Constante de Cor** ao grafo. Na **Caixa de Ferramentas**, em **Constantes**, selecione **Constante de Cor** e mova para a superfície de design.  
  
4. Especifique um valor de cor para o nó **Constante de Cor**. Use a ferramenta **Selecionar** para selecionar o nó **Constante de Cor** e, em seguida, na janela **Propriedades**, na propriedade **Saída**, especifique um valor de cor. Para laranja, especifique um valor de (1,0, 0,5, 0,2, 1,0).  
  
5. Conecte a constante de cor à cor final. Para criar as conexões, mova o terminal **RGB** do nó **Constante de Cor** para o terminal **RGB** do nó **Cor Final** e, em seguida, mova o terminal **Alfa** do nó **Constante de Cor** para o terminal **Alfa** do nó **Cor Final**. Essas conexões definem a cor final para a constante de cor definida na etapa anterior.  
  
   A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a um cubo.  
  
> [!NOTE]
>  Na ilustração foi especificada uma cor laranja para demonstrar melhor o efeito do sombreador.  
  
 ![Grafo de sombreador e seu resultado em um modelo 3D](../designers/media/digit-flat-color-effect.png "Digit-Flat-Color-Effect")  
  
 Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter mais informações sobre como visualizar sombreadores no Designer de Sombreador, consulte [Designer de Sombreador](../designers/shader-designer.md).  
  
## <a name="see-also"></a>Consulte também  
 [Como: Aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)   
 [Como exportar um sombreador](../designers/how-to-export-a-shader.md)   
 [Designer de Sombreador](../designers/shader-designer.md)   
 [Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)
