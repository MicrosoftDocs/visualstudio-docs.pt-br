---
title: Opções, Editor de Texto, Todas as Linguagens, Barras de Rolagem
ms.date: 10/25/2018
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.All_Languages.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.Basic.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.CSharp.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.C%2FC%2B%2B.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.CoffeeScript.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.CSS.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.Dockerfile.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.F%2523.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.HQL.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.HTML.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.HTMLX.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.JavaScript.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.TypeScript.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.JSON.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.LESS.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.Plain_Text.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.ResJSON.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.SCSS.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.SQL_Server_Tools.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.StreamAnalytics.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.T-SQL90.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.U-SQL.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.XAML.ScrollBars
- VS.ToolsOptionsPages.Text_Editor.XML.ScrollBars
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 54ce07537adc436f719de8596657d1367afcb87d
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/01/2020
ms.locfileid: "75588792"
---
# <a name="options-text-editor-all-languages-scroll-bars"></a>Opções, Editor de Texto, Todas as Linguagens, Barras de Rolagem
Essa caixa de diálogo permite alterar o comportamento padrão da barra de rolagem do editor de código. Para exibir essas opções, selecione **Opções** do menu **Ferramentas**. Na pasta **Editor de Texto**, expanda a subpasta **Todas as Linguagens** e, em seguida, escolha **Barras de Rolagem**.

> [!CAUTION]
> Essa página define opções padrão para todas as linguagens de desenvolvimento. A redefinição de uma opção nessa caixa de diálogo redefinirá as opções das Barras de Rolagem em todas as linguagens em relação às opções selecionadas aqui. Para alterar as opções do Editor de Texto para apenas uma linguagem, expanda a subpasta para aquela linguagem e selecione suas páginas de opções.

## <a name="show-horizontal-scroll-bar"></a>Mostrar barra de rolagem horizontal

Quando selecionada, exibe uma barra de rolagem horizontal, que permite rolar de um lado para o outro para exibir os elementos que estão fora da área de exibição do Editor. Se barras de rolagem horizontais não estiverem disponíveis, você poderá usar as teclas de cursor para rolar.

## <a name="show-vertical-scroll-bar"></a>Mostrar barra de rolagem vertical

Quando selecionada, exibe uma barra de rolagem vertical que permite rolar para cima e para baixo para exibir os elementos que estão fora da área de exibição do Editor. Se barras de rolagem verticais não estiverem disponíveis, você poderá usar Page Up, Page Down e teclas do cursor para rolar.

## <a name="display"></a>{1&gt;Vídeo&lt;1}

### <a name="show-annotations-over-vertical-scroll-bar"></a>Mostrar anotações sobre a barra de rolagem vertical

Selecione se a barra de rolagem vertical mostra as anotações a seguir:

- alterações
- marcas
- erros
- posição do cursor

> [!TIP]
> A opção **Exibir marcas** inclui pontos de interrupção e indicadores.

Experimente abrir um arquivo de código grande e substituir algumas partes do texto que ocorrem em vários locais no arquivo. A barra de rolagem mostra o efeito das substituições, de modo que você pode desfazer suas alterações se tiver substituído algo que não deveria.

Veja a postagem no blog da [Barra de rolagem avançada](https://blogs.msdn.microsoft.com/cdnstudents/2014/01/21/visual-studio-tips-and-tricks-enhanced-scroll-bar/) sobre o que as várias cores e símbolos significam ao editar código.

## <a name="behavior"></a>Comportamento

A barra de rolagem tem dois modos: o modo de barra e o modo de mapa.

### <a name="use-bar-mode-for-vertical-scroll-bar"></a>Use o modo de barra para barra de rolagem vertical

O *modo de barra* exibe indicadores de anotação na barra de rolagem. Clicando na barra de rolagem é possível rolar a página para cima ou para baixo, mas não ir para aquele local no arquivo.

### <a name="use-map-mode-for-vertical-scroll-bar"></a>Use o modo de mapa para barra de rolagem vertical

No *modo de mapa*, quando você clica em um local na barra de rolagem, o cursor vai para aquele local no arquivo em vez de simplesmente rolar para cima ou para baixo em uma página. As linhas de código são mostradas em miniatura na barra de rolagem. É possível escolher a largura da coluna do mapa selecionando um valor em **Visão geral do Código-fonte**. Para habilitar uma visualização maior do código quando você parar o ponteiro no mapa, selecione a opção **Mostrar Dica de Ferramenta de Visualização**. As regiões recolhidas ficam sombreadas de forma diferente e são expandidas quando você clica duas vezes nelas.

> [!TIP]
> Você pode desabilitar a exibição de código em miniatura no modo de mapa definindo a opção **Visão geral do código-fonte** como **Desabilitada**. Se a opção **Mostrar Dica de Ferramenta de Visualização** estiver selecionada, você ainda verá uma visualização do código nesse local ao passar o ponteiro do mouse sobre a barra de rolagem e, o cursor ainda o levará para esse local no arquivo quando você clicar.

## <a name="see-also"></a>Veja também

- [Como personalizar a barra de rolagem](../how-to-track-your-code-by-customizing-the-scrollbar.md)
