---
title: Recursos de Designer de Fluxo de Trabalho Shell
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- WFDShellFeatures.UI
ms.assetid: 14bfe312-9592-408e-92ce-e98585ad16e7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5a6b192eae3340c6a3d84bb3ccbcce7cbf8d65b3
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85816378"
---
# <a name="workflow-designer-shell-features"></a>Recursos de Designer de Fluxo de Trabalho Shell

Designer de Fluxo de Trabalho é composta de três áreas principais da interface do usuário: a superfície do designer, a barra de navegação estrutural acima dela e o Shell abaixo dela. A barra de rastreamento, posicionado na parte superior da tela, é usada para exibir a lista de ancestrais de atividade da raiz atual. Para obter mais informações, consulte [como: usar a navegação por trilha](../workflow-designer/how-to-use-breadcrumb-navigation.md). A superfície de designer, posicionado no centro da tela, é usada para compondo fluxos de trabalho. O shell, localizado na parte inferior da tela, contém um número de botões para gerenciar o modo de exibição atual.

## <a name="shell-features"></a>Recursos de Shell
 O shell tem botões no lado direito da barra que você pode usar para ampliar ou do fluxo de trabalho, para caber o conteúdo do fluxo de trabalho o tamanho da tela, e de apresentação ou para ocultar o mapa da revisão. Você também pode ampliar ou fora de um fluxo de trabalho usando os atalhos de teclado CTRL++ e CTRL+-.

## <a name="overview-map"></a>Visão geral de mapa
 O mapa da visão geral exibe uma pequena versão da atividade inteira na raiz atual de rastreamento, incluindo todos seus filhos e todos os seus filhos expandidos. Há um viewport, um retângulo com uma borda laranja, que realça a parte da atividade exibida atualmente dentro do editor. Arraste o retângulo em torno do mapa da visão geral rola o designer de fluxo de trabalho e altera a exibição do editor.

> [!NOTE]
> A interface do usuário Designer de Fluxo de Trabalho é virtualizada. Os designers de atividade são processados somente se necessário. Se uma parte do fluxo de trabalho foi desenhada nunca na superfície do designer, essa parte aparece como o branco no mapa da revisão. Rolagem em torno do mapa da visão geral desenha completamente o fluxo de trabalho.

## <a name="copying-or-saving-workflows-as-images"></a>Copiando ou salvando fluxos de trabalho como imagens
 Fluxos de trabalho podem ser copiados no formato de bitmap ou ser salvos no formato de bitmap ou vetorial. Copiar ou salvar uma imagem fornecem uma maneira para exportar um modo de exibição da atividade inteira na raiz atual de rastreamento, incluindo todos seus filhos e todos os seus filhos expandidos a outros programa.

 Para copiar como imagem, clique com o botão direito do mouse em qualquer lugar no designer e selecione **Copiar como imagem**. Para salvar como imagem, clique com o botão direito do mouse em qualquer lugar no designer e selecione **salvar como imagem**. Fluxos de trabalho podem ser salvos no formato de JPG, PNG, GIF, ou XPS. O formato é selecionado na caixa de diálogo **salvar como** na caixa de listagem suspensa **salvar como tipo:** na parte inferior da janela.

## <a name="fonts-and-colors"></a>Fontes e cores

As fontes usadas em Designer de Fluxo de Trabalho dentro do Visual Studio são controladas pela fonte do ambiente. As cores exibidas em Designer de Fluxo de Trabalho mudam se você estiver usando um esquema de cores de alto contraste para o tema do sistema operacional. Você deve reiniciar o Visual Studio depois de fazer uma alteração nas configurações de fonte ou cor antes que as alterações entrem em vigor no Designer de Fluxo de Trabalho.