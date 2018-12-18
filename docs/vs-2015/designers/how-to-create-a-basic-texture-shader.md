---
title: Como criar um sombreador de textura básico | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5af113fb-6415-4be0-8b23-10fddb10e80a
caps.latest.revision: 25
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 18bb4f1ad4dfc3428e8dc30958013438de22e13a
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49898532"
---
# <a name="how-to-create-a-basic-texture-shader"></a>Como criar um sombreador de textura básica
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este documento demonstra como usar o Designer de Sombreador e a DGSL (Directed Graph Shader Language) para criar um sombreador de textura única. Esse sombreador define a cor final diretamente para os valores RGB e alfa, cujas amostras são obtidas da textura.  
  
 Este documento demonstra essas atividades:  
  
-   Remover os nós de um grafo de sombreador  
  
-   Adicionar nós a um grafo  
  
-   Configurar parâmetros de sombreador  
  
-   Configurar visibilidade do parâmetro  
  
-   Conectar nós  
  
## <a name="creating-a-basic-texture-shader"></a>Criar um sombreador de textura básico  
 Você pode implementar um sombreador de textura única básico ao gravar os valores de cor e valores alfa de uma amostra de textura diretamente na cor de saída final.  
  
 Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.  
  
#### <a name="to-create-a-basic-texture-shader"></a>Para criar um sombreador de textura básico  
  
1. Crie um sombreador DGSL com o qual trabalhar. Para obter informações sobre como adicionar um sombreador DGSL ao seu projeto, consulte a seção de Introdução em [Designer de Sombreador](../designers/shader-designer.md).  
  
2. Exclua o nó **Ponto de Cor**. No modo de **Seleção**, selecione o nó **Ponto de Cor** e, em seguida, na barra de menus, escolha **Editar** e **Excluir**. Isso abre o espaço para o nó que será adicionado na próxima etapa.  
  
3. Adicione um nó **Amostra de Textura** ao grafo. Na **Caixa de Ferramentas**, em **Textura**, selecione **Amostra de Textura** e mova-a para a superfície de design.  
  
4. Adicione um nó **Coordenada de Textura** ao grafo. Na **Caixa de Ferramentas**, em **Textura**, selecione **Coordenada de Textura** e mova-a para a superfície de design.  
  
5. Escolha uma textura para aplicar. No modo de **Seleção**, selecione o nó **Amostra de Textura** e, em seguida, na janela **Propriedades**, especifique a textura que você deseja usar através da propriedade **Filename**.  
  
6. Torne a textura publicamente acessível. Selecione o nó **Amostra de Textura** e, em seguida, na janela **Propriedades**, defina a propriedade **Acesso** como **Público**. Agora é possível definir a textura de outra ferramenta, como o **Editor de Modelo**.  
  
7. Conecte as coordenadas de textura à amostra de textura. No modo de **Seleção**, mova o terminal de **Saída** do nó **Coordenada de Textura** para o terminal **UV** do nó **Amostra de Textura**. Essa conexão retira uma amostra de textura nas coordenadas especificadas.  
  
8. Conecte a amostra de textura à cor final. Mova o terminal **RGB** do nó **Amostra de Textura** para o terminal **RGB** do nó **Cor Final** e, em seguida, mova o terminal **Alfa** do nó **Amostra de Textura** para o terminal **Alfa** do nó **Cor Final**.  
  
   A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a um cubo.  
  
> [!NOTE]
>  Nesta ilustração foi usado um plano como a forma de visualização e foi especificada uma textura para demonstrar melhor o efeito do sombreador.  
  
 ![Grafo de sombreador e uma visualização de seu efeito](../designers/media/digit-texture-effect.png "Digit-Texture-Effect")  
  
 Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter mais informações sobre como visualizar sombreadores no Designer de Sombreador, consulte [Designer de Sombreador](../designers/shader-designer.md)  
  
## <a name="see-also"></a>Consulte também  
 [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)   
 [Editor de imagens](../designers/image-editor.md)   
 [Designer de Sombreador](../designers/shader-designer.md)   
 [Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)



