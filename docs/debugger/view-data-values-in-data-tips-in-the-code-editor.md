---
title: Exibir valores de variáveis em DataTips | Microsoft Docs
description: Use DataTips para exibir de forma conveniente informações sobre variáveis, incluindo matrizes e estruturas, durante a depuração. Você também pode modificar valores.
ms.custom: SEO-VS-2020
ms.date: 11/21/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], DataTips
- DataTips tool
ms.assetid: ffa7bd18-439b-4685-a9b3-c7884b5de41f
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: a84c3379c04799aa1faea5b0e62afe0ef1aa11e9
ms.sourcegitcommit: e3a364c014ccdada0860cc4930d428808e20d667
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112386469"
---
# <a name="view-data-values-in-datatips-in-the-code-editor"></a>Exibir valores de dados em DataTips no editor de código

Os DataTips fornecem um modo conveniente de exibir informações sobre variáveis em seu programa durante a depuração. Os DataTips funcionam apenas no modo de interrupção e apenas com variáveis que estejam no escopo de execução atual. Se esta for a primeira vez que você tentou depurar o código, talvez você queira ler [depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) e [ferramentas e técnicas de depuração antes de](../debugger/write-better-code-with-visual-studio.md) passar por este artigo.

## <a name="work-with-datatips"></a>Trabalhar com DataTips

DataTips aparecem apenas no modo de interrupção e somente em variáveis que estão no escopo atual de execução.

### <a name="display-a-datatip"></a>Exibir um DataTip

1. Defina um ponto de interrupção em seu código e inicie a depuração pressionando **F5** ou selecionando **depurar**  >  **Iniciar Depuração**.

1. Quando em pausa no ponto de interrupção, passe o mouse sobre qualquer variável no escopo atual. Um DataTip é exibido, mostrando o nome e o valor atual da variável.

### <a name="make-a-datatip-transparent"></a>Tornar um DataTip transparente

Para tornar um DataTip transparente para ver o código que está abaixo dele, no DataTip, pressione **Ctrl**. O DataTip permanece transparente, desde que você mantenha pressionada a tecla **Ctrl** . Isso não funciona para DataTips fixados ou flutuantes.
### <a name="pin-a-datatip"></a>Fixar um DataTip

Para fixar um DataTip para que ele permaneça aberto, selecione o ícone **fixar na fonte** .

![Fixar um DataTip](../debugger/media/dbg-tips-data-tips-pinned.png "Fixar um DataTip")

Você pode mover um DataTip fixado arrastando-o para a janela de código. Um ícone de pino aparece na medianiz ao lado da linha à qual o DataTip está fixado.

>[!NOTE]
>DataTips sempre são avaliados no contexto em que a execução é suspensa, não o cursor atual ou o local DataTip. Se você passar o mouse sobre uma variável em outra função que tenha o mesmo nome de uma variável no contexto atual, o valor da variável no contexto atual será exibido.

### <a name="unpin-a-datatip-from-source"></a>Desafixar um DataTip da origem

Para flutuar um DataTip fixado, passe o mouse sobre o DataTip e selecione o ícone de pino no menu de contexto.

O ícone de pino muda para a posição desafixada e o DataTip agora flutua ou pode ser arrastado para cima de todas as janelas abertas. As dicas de datafloats são fechadas quando a sessão de depuração termina.

### <a name="repin-a-datatip"></a>Fixá DataTip

Para fixá um DataTip flutuante à origem, focalize-o no editor de código e selecione o ícone de pino. O ícone de pino muda para a posição fixada e o DataTip é fixado novamente somente na janela de código.

Se um DataTip estiver flutuando em uma janela de código não-fonte, o ícone de pino ficará indisponível e o DataTip não poderá ser reafixado. Para acessar o ícone de pino, retorne o DataTip para a janela do editor de código arrastando-o ou dando o foco da janela de código.

### <a name="close-a-datatip"></a>Fechar um DataTip

Para fechar um DataTip, passe o mouse sobre o DataTip e selecione o ícone fechar (**x**) no menu de contexto.

### <a name="close-all-datatips"></a>Fechar todas as dicas de DataTips

Para fechar todas as dicas de DataTips, no menu **depurar** , selecione **limpar todas as dicas** de data.

### <a name="close-all-datatips-for-a-specific-file"></a>Fechar todas as dicas de um arquivo específico

Para fechar todas as dicas de seleção de um arquivo específico, no menu **depurar** , selecione **limpar todos os DataTips \<Filename> fixados para**.

## <a name="expand-and-edit-information"></a>Expandir e editar informações
Você pode usar os DataTips para expandir uma matriz, uma estrutura ou um objeto para exibir seus membros. Você também pode editar o valor de uma variável de um DataTip.

### <a name="expand-a-variable"></a>Expandir uma variável

Para expandir um objeto em um DataTip para ver seus elementos, passe o mouse sobre as setas de expansão antes dos nomes dos itens para exibir os elementos no formulário de árvore. Para um DataTip fixado, selecione o **+** antes do nome da variável e expanda a árvore.

![Expandir um DataTip](../debugger/media/dbg-tour-data-tips.png "Expandir um DataTip")

Você pode usar o mouse ou as teclas de direção no teclado para mover para cima e para baixo na exibição expandida.

Você também pode fixar itens expandidos no DataTip fixado passando o mouse sobre eles e selecionando seus ícones de pino. Os elementos são exibidos no DataTip fixado depois que a árvore é recolhida.

### <a name="edit-the-value-of-a-variable"></a>Editar o valor de uma variável

Para editar o valor de uma variável ou elemento em um DataTip, selecione o valor, digite um novo valor e pressione **Enter**. A seleção está desabilitada para valores somente leitura.

::: moniker range=">= vs-2019"

## <a name="pin-properties-in-datatips"></a>Propriedades do PIN em DataTips

> [!NOTE]
> Esse recurso tem suporte para o .NET Core 3,0 ou superior.

Você pode inspecionar objetos rapidamente por suas propriedades em DataTips com a ferramenta **fixas Properties** .  Para usar essa ferramenta, focalize uma propriedade e selecione o ícone de pino que aparece ou clique com o botão direito do mouse e selecione a opção **fixar membro como favorito** no menu de contexto resultante.  Isso faz com que essa propriedade apareça na parte superior da lista de propriedades do objeto, e o nome e o valor da propriedade são exibidos na coluna à direita do DataTip.  Para Desafixar uma propriedade, selecione o ícone de fixação novamente ou selecione a opção **Desafixar membro como favorito** no menu de contexto.

![Fixando uma propriedade em um DataTip](../debugger/media/basic-pin-datatip.gif "Fixando uma propriedade em um DataTip")

Você também pode alternar nomes de propriedade e filtrar Propriedades não fixas ao exibir a lista de propriedades do objeto em um DataTip.  Você pode acessar qualquer uma das opções clicando com o botão direito do mouse em uma linha que contém uma propriedade e selecionando as opções **Mostrar somente membros fixados** ou **ocultar nomes de membros fixados em valores** no menu de contexto.

::: moniker-end

## <a name="visualize-complex-data-types"></a>Visualizar tipos de dados complexos

Um ícone de lupa ao lado de uma variável ou elemento em um DataTip significa que um ou mais [visualizadores](../debugger/create-custom-visualizers-of-data.md), como o [Visualizador de texto](../debugger/string-visualizer-dialog-box.md), estão disponíveis para a variável. Os visualizadores exibem informações em uma maneira mais significativa, às vezes, gráfica.

Para exibir o elemento usando o visualizador padrão para o tipo de dados, selecione o ícone do ![Visualizador](../debugger/media/dbg-tips-visualizer-icon.png "Ícone do Visualizador")de ícones de lupa. Selecione a seta ao lado do ícone de lupa para selecionar em uma lista de visualizadores para o tipo de dados.

## <a name="add-a-variable-to-a-watch-window"></a>Adicionar uma variável a um janela Inspeção

Se você quiser continuar a assistir a uma variável, poderá adicioná-la a uma janela de **inspeção** de um DataTip. Clique com o botão direito do mouse na variável no DataTip e selecione **Adicionar inspeção**.

A variável aparece na janela **Watch** . Se sua edição do Visual Studio der suporte a mais de uma janela **Watch** , a variável aparecerá no **Watch 1**.

## <a name="import-and-export-datatips"></a>Importar e exportar DataTips

Você pode exportar DataTips para um arquivo XML, que pode ser compartilhado ou editado usando um editor de texto. Você também pode importar um arquivo XML DataTip que você recebeu ou editou.

**Para exportar DataTips:**

1. Selecione **depurar**  >  **Exportar DataTips**.

1. Na caixa de diálogo **Exportar DataTips** , navegue até o local para salvar o arquivo XML, digite um nome para o arquivo e, em seguida, selecione **salvar**.

**Para importar DataTips:**

1. Selecione **depurar**  >  **importar DataTips**.

1. Na caixa de diálogo **importar DataTips** , selecione o arquivo XML DataTips que você deseja abrir e, em seguida, selecione **abrir**.

## <a name="see-also"></a>Confira também
- [O que é depuração?](../debugger/what-is-debugging.md)
- [Técnicas e ferramentas de depuração](../debugger/write-better-code-with-visual-studio.md)
- [Primeira olhada na depuração](../debugger/debugger-feature-tour.md)
- [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)
- [Janelas de Inspeção e QuickWatch](../debugger/watch-and-quickwatch-windows.md)
- [Criar visualizadores personalizados](../debugger/create-custom-visualizers-of-data.md)
