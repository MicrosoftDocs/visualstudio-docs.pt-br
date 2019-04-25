---
title: Opções, Editor de Texto, Geral
ms.date: 01/18/2019
ms.topic: reference
f1_keywords:
- VS.ToolsOptionsPages.Text_Editor.RDL_Expression.General
- VS.ToolsOptionsPages.Text_Editor.SQL.General
- vs.toolsoptionspages.text_editor
- VS.ToolsOptionsPages.Text_Editor.T-SQL80.General
- VS.ToolsOptionsPages.Text_Editor.SQL_Script.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL7.General
- VS.ToolsOptionsPages.Text_Editor.T-SQL.General
- VS.ToolsOptionsPages.Text_Editor.PL/SQL.General
- VS.ToolsOptionsPages.Text_Editor
- VS.ToolsOptionsPages.Text_Editor.XOML.General
- VS.ToolsOptionsPages.Text_Editor.SQL
- VS.ToolsOptionsPages.Text_Editor.SQL_Script
- VS.ToolsOptionsPages.Text_Editor.General
- VS.ToolsOptionsPages.Text_Editor.Python
- VS.ToolsOptionsPages.Text_Editor.R
helpviewer_keywords:
- Text Editor Options dialog box
- Code Editor
- Text Editor [Visual Studio]
- editors, global settings
ms.assetid: 4ac21e48-3243-4141-9058-7eaf12b3cde7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9a7bcf7b57c6cdc7e0ff4ff5a851397b7c96b345
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62778641"
---
# <a name="options-text-editor-general"></a>Opções, Editor de Texto, Geral

Essa caixa de diálogo permite alterar as configurações globais do editor de texto e código do Visual Studio. Para exibir essa caixa de diálogo, selecione **Opções** no menu **Ferramentas**, expanda a pasta **Editor de Texto** e selecione **Geral**.

## <a name="settings"></a>Configurações

### <a name="drag-and-drop-text-editing"></a>Recurso de edição arrastar-e-soltar

Quando selecionado, permite mover texto selecionando-o e arrastando-o com o mouse para outro local no documento atual ou em qualquer outro documento aberto.

### <a name="automatic-delimiter-highlighting"></a>Realce automático de delimitadores

Quando selecionado, os caracteres delimitadores que separam parâmetros ou pares de valor do item, bem como as chaves correspondentes, são realçados.

### <a name="track-changes"></a>Controlar alterações

Quando o editor de códigos é selecionado, uma linha amarela vertical aparece na margem de seleção para marcar o código que foi alterado desde que o arquivo foi salvo mais recentemente. Quando você salva as alterações, as linhas verticais ficam verdes.

### <a name="auto-detect-utf-8-encoding-without-signature"></a>Detecção automática de codificação UTF-8 sem assinatura

Por padrão, o editor detecta a codificação procurando por marcas de ordem de byte ou marcas de conjunto de caracteres. Se nenhuma for encontrada no documento atual, o editor de códigos tentará detectar automaticamente a codificação UTF-8 examinando sequências de bytes. Para desabilitar a detecção automática da codificação, desmarque essa opção.

### <a name="follow-project-coding-conventions"></a>Seguir as convenções de codificação do projeto

Quando selecionada, as convenções de codificação especificada do projeto substituem qualquer convenções de codificação usadas em seus projetos pessoais.

### <a name="enable-mouse-click-to-perform-go-to-definition"></a>Habilitar clique do mouse para executar Ir para Definição

Com essa opção estiver selecionada, você poderá pressionar **Ctrl** e passar o mouse sobre um elemento ao clicar com o mouse. Isso leva você até a definição do elemento selecionado. Você também pode escolher **Alt** ou **Ctrl** + **Alt** no menu suspenso **Usar tecla modificadora**.

Marque a caixa de seleção **Abrir definição na exibição de inspeção** para exibir a definição do elemento selecionado em uma janela sem sair do local atual no editor de código.

## <a name="display"></a>Monitor

### <a name="selection-margin"></a>Margem de seleção

Quando selecionado, exibe uma margem vertical ao longo da borda esquerda da área de texto do editor. Você pode clicar nessa margem para selecionar uma linha de texto inteira ou clicar e arrastar para selecionar linhas consecutivas de texto.

|Margem de seleção ativada|Margem de seleção desativada|
| - | - |
|![Captura de tela de HTMLpageSelectionMarginOn](../../ide/reference/media/vxselmaron.gif)|![Captura de tela de HTMLpageSelectionMarginOff](../../ide/reference/media/vxselmaroff.gif)|

### <a name="indicator-margin"></a>Margem de indicadores

Quando selecionado, exibe uma margem vertical fora da borda esquerda da área de texto do editor. Quando você clica nesta margem, um ícone e uma dica de ferramenta relacionados ao texto aparecem. Por exemplo, atalhos da lista de tarefas ou de pontos de interrupção aparecem na margem de indicadores. Informações da Margem de Indicadores não são impressas.

### <a name="highlight-current-line"></a>Realçar linha atual

Quando selecionado, exibe uma caixa cinza ao redor da linha de código na qual o cursor está localizado.

### <a name="show-structure-guide-lines"></a>Mostrar diretrizes de estrutura

Quando essa opção estiver selecionada, as linhas verticais serão exibidas no editor, alinhadas aos blocos de código estruturado, o que permite que você identifique facilmente os blocos individuais de código.

## <a name="see-also"></a>Consulte também

- [Opções, Editor de Texto, Todas as Linguagens](../../ide/reference/options-text-editor-all-languages.md)
- [Opções, Editor de Texto, Todas as Linguagens, Guias](../../ide/reference/options-text-editor-all-languages-tabs.md)
- [Opções, Editor de Texto, Extensão de Arquivo](../../ide/reference/options-text-editor-file-extension.md)
- [Identificando e personalizando atalhos de teclado](../../ide/identifying-and-customizing-keyboard-shortcuts-in-visual-studio.md)
- [Personalizando o editor](../../ide/customizing-the-editor.md)
- [Usando o IntelliSense](../../ide/using-intellisense.md)