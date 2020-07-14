---
title: Tour de recursos do Blend para Visual Studio
titleSuffix: ''
ms.date: 07/31/2019
ms.topic: overview
f1_keywords:
- Blend.Start.Dev12
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8348ba38849b76a745a56f941850d6b61a8f433f
ms.sourcegitcommit: 57d96de120e0574e506dfd80bb7adfbac73f96be
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/24/2020
ms.locfileid: "85332092"
---
# <a name="blend-for-visual-studio-overview"></a>Visão geral do Blend para Visual Studio

O Blend for Visual Studio ajuda você a projetar aplicativos Web e Windows baseados em XAML. Ele fornece a mesma experiência básica de design XAML que o Visual Studio e adiciona designers visuais para tarefas avançadas, como animações e comportamentos. Para obter uma comparação entre o Blend e o Visual Studio, confira [Criar XAML no Visual Studio e no Blend para Visual Studio](../xaml-tools/designing-xaml-in-visual-studio.md).

Blend para Visual Studio é um componente do Visual Studio. Para instalar o Blend, no **Instalador do Visual Studio** escolha a carga de trabalho **desenvolvimento de Plataforma Universal do Windows** ou **desenvolvimento de área de trabalho do .NET**. As duas cargas de trabalho incluem o componente Blend para Visual Studio.

![Componentes da carga de trabalho UWP](media/installer-uwp.png)&nbsp;&nbsp;&nbsp;&nbsp;![Componentes da carga de trabalho de desenvolvimento de área de trabalho do .NET](media/installer-dotnet-desktop.png)

Se você estiver começando a usar o Blend for Visual Studio, reserve um tempo para familiarizar-se com os recursos exclusivos do workspace. Este tópico apresenta um tour rápido.

## <a name="tools-panel"></a>Painel Ferramentas

É possível usar o painel **Ferramentas** no Blend for Visual Studio para criar e modificar objetos no aplicativo. O painel **Ferramentas** aparece no lado esquerdo do Designer XAML quando você tem um arquivo *.xaml* aberto.

Você cria os objetos selecionando uma ferramenta e desenhando na prancheta com o mouse.

![Painel Ferramentas no Blend para Visual Studio](media/blend-tools-panel.png)

> [!TIP]
> Algumas das ferramentas no painel **Ferramentas** têm variações, por exemplo, em vez de um retângulo, você pode escolher uma elipse ou uma linha. Para acessar essas variações, clique com o botão direito do mouse na ferramenta ou clique nela e mantenha o botão do mouse pressionado.
>
> ![Variações de ferramenta Forma no Blend para Visual Studio](media/blend-rectangle-tool-variations.png)

### <a name="selection-tools"></a>Ferramentas de seleção

Selecione objetos e caminhos. Use a ferramenta **Seleção Direta** para selecionar objetos aninhados e segmentos de caminho.

### <a name="view-tools"></a>Ferramentas de exibição

Ajuste a prancheta, como para zoom e movimento panorâmico.

### <a name="brush-tools"></a>Ferramentas de pincel

Trabalhe com os atributos visuais de um objeto, como transformar um pincel ou aplicar um gradiente.

### <a name="object-tools"></a>Ferramentas de objeto

Desenhe os objetos mais comuns na prancheta, como demarcadores, formas, painéis de layout, texto e controles.

### <a name="asset-tools"></a>Ferramentas de ativo

Acesse o painel Ativos e mostre o ativo usado mais recentemente na biblioteca.

## <a name="assets-window"></a>Janela Ativos

A janela **Ativos** contém todos os controles disponíveis e é semelhante à **Caixa de ferramentas** no Visual Studio. Além dos controles, você encontrará tudo o que pode adicionar à sua prancheta na janela **Ativos**, incluindo estilos, mídias, comportamentos e efeitos. Para abrir a janela **Ativos**, escolha **Exibir** > **Janela Ativos** ou pressione **Ctrl**+**Alt**+**X**.

![Janela Ativos no Blend para Visual Studio](media/blend-assets-window.png)

- Insira texto na caixa **Pesquisar ativos** para filtrar a lista de ativos.
- Alterne a exibição dos ativos entre o Modo de grade e o Modo de lista usando os botões no canto superior direito.

## <a name="objects-and-timeline-window"></a>Janela Objetos e Linha do Tempo

Use essa janela para organizar os objetos na prancheta e, se quiser, para animá-los. Para abrir a janela **Objetos e Linha do Tempo**, escolha **Exibir** > **Estrutura de Tópicos do Documento**. Além da funcionalidade fornecida na [janela Estrutura de Tópicos do Documento](creating-a-ui-by-using-xaml-designer-in-visual-studio.md#document-outline-window) no Visual Studio, a janela Objetos e Linha do Tempo no Blend para Visual Studio posiciona a área de composição da linha do tempo à direita. Use a linha do tempo quando estiver criando e editando animações.

![Janela Objetos e Linha do Tempo no modo de animação](media/storyboard-timeline.png)

Usar os botões relacionados ao storyboard ![Botões do storyboard no Blend para Visual Studio](media/storyboard-buttons.png) para criar, excluir, fechar ou selecionar um storyboard. Use a área de composição da linha do tempo à direita para exibir a linha do tempo e mover os quadros-chave.

Passe o mouse sobre cada botão na janela para saber mais sobre a funcionalidade disponível.

## <a name="see-also"></a>Veja também

- [Animar objetos](../xaml-tools/animate-objects-in-xaml-designer.md)
- [Desenhar formas e caminhos](../xaml-tools/draw-shapes-and-paths.md)
- [Criando o XAML no Visual Studio e no Blend for Visual Studio](../xaml-tools/designing-xaml-in-visual-studio.md)
