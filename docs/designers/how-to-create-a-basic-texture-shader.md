---
title: Como criar um sombreador de textura básica
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 5af113fb-6415-4be0-8b23-10fddb10e80a
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: 211da971bc7e4e275ef43b88531fe46a7fc0b4eb
ms.sourcegitcommit: db680e8fa8066f905e7f9240342ece7ab9259308
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2018
ms.locfileid: "37924060"
---
# <a name="how-to-create-a-basic-texture-shader"></a>Como criar um sombreador de textura básico

Este artigo demonstra como usar o Designer de Sombreador e a DGSL (Directed Graph Shader Language) para criar um sombreador de textura única. Esse sombreador define a cor final diretamente para os valores RGB e alfa, cujas amostras são obtidas da textura.

## <a name="create-a-basic-texture-shader"></a>Criar um sombreador de textura básica

Você pode implementar um sombreador de textura única básico ao gravar os valores de cor e valores alfa de uma amostra de textura diretamente na cor de saída final.

Antes de começar, verifique se a janela **Propriedades** e a **Caixa de Ferramentas** estão sendo exibidas.

1.  Crie um sombreador DGSL com o qual trabalhar. Para obter informações sobre como adicionar um sombreador DGSL ao seu projeto, consulte a seção de Introdução em [Designer de Sombreador](../designers/shader-designer.md).

2.  Exclua o nó **Ponto de Cor**. No modo de **Seleção**, selecione o nó **Cor do Ponto** e, em seguida, na barra de menus, escolha **Editar** > **Excluir**. Isso abre o espaço para o nó que será adicionado na próxima etapa.

3.  Adicione um nó **Amostra de Textura** ao grafo. Na **Caixa de Ferramentas**, em **Textura**, selecione **Amostra de Textura** e mova-a para a superfície de design.

4.  Adicione um nó **Coordenada de Textura** ao grafo. Na **Caixa de Ferramentas**, em **Textura**, selecione **Coordenada de Textura** e mova-a para a superfície de design.

5.  Escolha uma textura para aplicar. No modo de **Seleção**, selecione o nó **Amostra de Textura** e, em seguida, na janela **Propriedades**, especifique a textura que você deseja usar através da propriedade **Filename**.

6.  Torne a textura publicamente acessível. Selecione o nó **Amostra de Textura** e, em seguida, na janela **Propriedades**, defina a propriedade **Acesso** como **Público**. Agora é possível definir a textura de outra ferramenta, como o **Editor de Modelo**.

7.  Conecte as coordenadas de textura à amostra de textura. No modo de **Seleção**, mova o terminal de **Saída** do nó **Coordenada de Textura** para o terminal **UV** do nó **Amostra de Textura**. Essa conexão retira uma amostra de textura nas coordenadas especificadas.

8.  Conecte a amostra de textura à cor final. Mova o terminal **RGB** do nó **Amostra de Textura** para o terminal **RGB** do nó **Cor Final** e, em seguida, mova o terminal **Alfa** do nó **Amostra de Textura** para o terminal **Alfa** do nó **Cor Final**.

A ilustração a seguir mostra o grafo de sombreador concluído e uma visualização do sombreador aplicado a um cubo.

> [!NOTE]
> Nesta ilustração foi usado um plano como a forma de visualização e foi especificada uma textura para demonstrar melhor o efeito do sombreador.

![Grafo de sombreador e uma versão prévia de seu efeito](../designers/media/digit-texture-effect.png)

Determinadas formas podem fornecer melhores visualizações para alguns sombreadores. Para obter mais informações sobre como visualizar sombreadores no Designer de Sombreador, consulte [Designer de Sombreador](../designers/shader-designer.md)

## <a name="see-also"></a>Consulte também

- [Como aplicar um sombreador a um modelo 3D](../designers/how-to-apply-a-shader-to-a-3-d-model.md)
- [Editor de Imagens](../designers/image-editor.md)
- [Designer de Sombreador](../designers/shader-designer.md)
- [Nós do Designer de Sombreador](../designers/shader-designer-nodes.md)