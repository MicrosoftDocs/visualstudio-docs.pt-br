---
title: GUIDs e IDs das barras de ferramentas do Visual Studio | Microsoft Docs
description: Exiba uma lista de valores GUID e ID para as barras de ferramentas e os grupos que eles contêm, que estão incluídos no IDE (ambiente de desenvolvimento integrado) do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- visual studio groups
- toolbars
- visual studio toolbar
- id
- toolgar group
- tool window toolbar
- guid
ms.assetid: c9cacd57-9225-450f-a9ac-cbf3168ea844
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 3d2ba6c92a2913ec63a59751a4181454aa67fa67
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898104"
---
# <a name="guids-and-ids-of-visual-studio-toolbars"></a>GUIDs e IDs das barras de ferramentas do Visual Studio
Este tópico enumera os valores de GUID e ID das barras de ferramentas que estão incluídas no IDE (ambiente de desenvolvimento integrado) do Visual Studio e nos grupos que eles contêm. Esses valores são definidos em arquivos *. vsct* que são instalados como parte do SDK do Visual Studio. Para obter mais informações, consulte [comandos, menus e grupos definidos pelo IDE](../../extensibility/internals/ide-defined-commands-menus-and-groups.md).

> [!NOTE]
> Muitas das barras de ferramentas disponíveis para o Visual Studio não são definidas pelo Visual Studio, e seus valores GUID e ID não são públicos. Este tópico lista somente as barras de ferramentas definidas nos arquivos SDK *. vsct* do Visual Studio.

 Para obter mais informações sobre como trabalhar com objetos IDE definidos em arquivos *. vsct* , consulte [estender menus e comandos](../../extensibility/extending-menus-and-commands.md).

 As barras de ferramentas padrão fornecidas pelo IDE do Visual Studio usam o GUID `guidSHLMainMenu` , exceto onde especificado de outra forma usando a `GUID:ID` sintaxe.

## <a name="ide-toolbars"></a>Barras de ferramentas do IDE
 As barras de ferramentas a seguir são fornecidas pelo IDE do Visual Studio. As barras de ferramentas podem ser exibidas selecionando-as no submenu **barras de ferramentas** do menu **ferramentas** . As barras de ferramentas nas janelas de ferramentas não estão incluídas nesta seção.

 Somente os grupos podem ser decrescentes diretamente das barras de ferramentas. Para adicionar um grupo, defina seu pai como o GUID e a ID da barra de ferramentas. Para adicionar um botão a uma barra de ferramentas, defina seu pai como um grupo na barra de ferramentas.

|Barra de ferramentas|ID|
|-------------|--------|
|Standard|IDM_VS_TOOL_STANDARD|
|Build|IDM_VS_TOOL_BUILD|
|Editor de texto|IDM_VS_TOOL_TEXTEDITOR|
|Depurar|guidVSDebugGroup: IDM_DEBUG_TOOLBAR|
|Local de depuração|guidVSDebugGroup: IDM_DEBUG_CONTEXT_TOOLBAR|

### <a name="special-toolbars"></a>Barras de ferramentas especiais
 Essas barras de ferramentas são definidas pelo IDE do Visual Studio, mas servem para funções especializadas e não hospedam grupos de comandos.

|Barra de ferramentas|ID|
|-------------|--------|
|Adicionar comando|IDM_VS_TOOL_ADDCOMMAND|
|Indefinido|IDM_VS_TOOL_UNDEFINED|
|esquema XML|IDM_VS_TOOL_SCHEMA|
|dados XML|IDM_VS_TOOL_DATA|

## <a name="groups-on-the-ide-toolbars"></a>Grupos nas barras de ferramentas do IDE
 Para adicionar um botão a uma barra de ferramentas padrão, defina um dos grupos a seguir como seu pai. Os grupos são classificados por barra de ferramentas pai.

### <a name="standard-toolbar-groups"></a>Grupos de barras de ferramentas padrão

|Nome|ID|
|----------|--------|
|Salvar/abrir|IDG_VS_TOOLSB_SAVEOPEN|
|Recortar/copiar|IDG_VS_TOOLSB_CUTCOPY|
|Desfazer/refazer|IDG_VS_TOOLSB_UNDOREDO|
|Executar/compilar|IDG_VS_TOOLSB_RUNBUILD|
|Search|IDG_VS_TOOLSB_SEARCH|
|Windows|IDG_VS_TOOLSB_WINDOWS|
|Novas janelas|IDG_VS_TOOLSB_NEWWINDOWS|
|Carregar/salvar|IDG_VS_WINDOWUI_LOADSAVE|
|Medidor|IDG_VS_TOOLSB_GAUGE|

### <a name="build-toolbar-groups"></a>Criar grupos da barra de ferramentas

|Nome|ID|
|----------|--------|
|Barra de Build|IDG_VS_BUILDBAR|
|Cancelar|IDG_VS_BUILD_CANCEL|

### <a name="text-editor-toolbar-groups"></a>Grupos de barras de ferramentas do editor de texto

|Nome|ID|
|----------|--------|
|Completion|IDM_VS_TOOL_TEXTEDITOR|
|Recuar|IDG_VS_EDITTOOLBAR_INDENT|
|Comentário|IDG_VS_EDITTOOLBAR_COMMENT|
|Indicadores|IDG_VS_EDITTOOLBAR_TEMPBOOKMARKS|

### <a name="debug-toolbar-groups"></a>Depurar grupos da barra de ferramentas

|Nome|ID|
|----------|--------|
|Execução|IDM_DEBUG_TOOLBAR|
|Depuração|IDG_DEBUG_TOOLBAR_STEPPING|
|Assistir|IDG_DEBUG_TOOLBAR_WATCH|
|Windows|IDG_DEBUG_TOOLBAR_WINDOWS|

### <a name="debug-location-toolbar-groups"></a>Grupos da barra de ferramentas do local de depuração

|Nome|ID|
|----------|--------|
|Local de depuração|IDG_DEBUG_CONTEXT_TOOLBAR|

## <a name="tool-window-toolbars"></a>Barras de ferramentas da janela de ferramentas
 As barras de ferramentas podem aparecer diretamente no IDE ou nas janelas de ferramentas, **como** Gerenciador de Soluções . Como as janelas de ferramentas não são definidas *em arquivos .vsct,* as barras de ferramentas da janela de ferramentas não têm pais definidos. Em vez disso, eles são colocados no código. A tabela a seguir mostra as barras de ferramentas que aparecem nas janelas de ferramentas no IDE e os grupos de comandos que elas contêm.

> [!NOTE]
> Barras de ferramentas e grupos usam o GUID , exceto quando especificado de outra `guidSHLMainMenu` forma usando a sintaxe GUID:ID. Quando um GUID é especificado para uma barra de ferramentas, ele também se aplica aos grupos descendentes dessa barra de ferramentas.

|Janela de ferramentas|Barra de ferramentas|Grupos|
|-----------------|-------------|------------|
|Gerenciador de Soluções|IDM_VS_TOOL_PROJWIN|IDG_VS_PROJ_TOOLBAR1.. 5|
|Gerenciador de Servidores|guid_SE_MenuGroup:IDM_SE_TOOLBAR_SERVEREXPLORER|IDG_SE_TOOLBAR_REFRESH|
|Propriedades|IDM_VS_TOOL_PROPERTIES|IDG_VS_PROPERTIES_SORT<br /><br /> IDG_VS_PROPERTIES_PAGES|
|Exibição de Classe|IDM_VS_TOOL_CLASSVIEW|IDG_VS_CLASSVIEW_FOLDERS<br /><br /> IDG_VS_CLASSVIEW_SEARCH<br /><br /> IDG_VS_CLASSVIEW_SETTINGS|
|Exibição de Classe|IDM_VS_TOOL_CLASSVIEW_GO|IDG_VS_CLASSVIEW_SEARCH2|
|Pesquisador de Objetos|IDM_VS_TOOL_OBJBROWSER|IDG_VS_OBJBROWSER_SUBSETS<br /><br /> IDG_VS_OBJBROWSER_SEARCH<br /><br /> IDG_VS_OBJBROWSER_ADDREFERENCE<br /><br /> IDG_VS_OBJBROWSER_BROWSERSETTINGS|
|Pesquisador de Objetos|IDM_VS_TOOL_OBJECT_BROWSER_GO|IDG_VS_OBJBROWSER_SEARCH2|
|Saída|IDM_VS_TOOL_OUTPUTWINDOW|IDG_VS_OUTPUTWINDOW_SELECT<br /><br /> IDG_VS_OUTPUTWINDOW_GOTO<br /><br /> IDG_VS_OUTPUTWINDOW_NEXTPREV<br /><br /> IDG_VS_OUTPUTWINDOW_CLEAR<br /><br /> IDG_VS_OUTPUTWINDOW_WORDWRAP|
|Localizar e Substituir|IDM_VS_TOOL_UNIFIEDFIND|IDG_VS_FINDTAB<br /><br /> IDG_VS_REPLACETAB|
|Encontrar Resultados 1|IDM_VS_TOOL_FINDRESULTS1|IDG_VS_FINDRESULTS1_GOTO<br /><br /> IDG_VS_FINDRESULTS1_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS1_CLEAR<br /><br /> IDG_VS_FINDRESULTS1_STOPFIND|
|Encontrar Resultados 2|IDM_VS_TOOL_FINDRESULTS2|IDG_VS_FINDRESULTS2_GOTO<br /><br /> IDG_VS_FINDRESULTS2_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS2_CLEAR<br /><br /> IDG_VS_FINDRESULTS2_STOPFIND|
|Snippet|IDM_VS_TOOL_SNIPPETMENUS|IDG_VS_SNIPPET_REPL<br /><br /> IDG_VS_SNIPPET_REF<br /><br /> IDG_VS_SNIPPET_PROP|
|Indicadores|IDM_VS_TOOL_BOOKMARKWIND|IDG_VS_BWNEWFOLDER<br /><br /> IDG_VS_BWNEXTBM<br /><br /> IDG_VS_BWNEXTBMF<br /><br /> IDG_VS_BWENABLE<br /><br /> IDG_VS_BWDELETE|
|Lista de Tarefas|IDM_VS_TOOL_TASKLIST|IDG_VS_TASKLIST_PROVIDERLIST|
|Tarefas do usuário|IDM_VS_TOOL_USERTASKS|IDG_VS_TASKLIST_PROVIDERLIST<br /><br /> IDG_VS_USERTASKS_EDIT|
|Lista de Erros|IDM_VS_TOOL_ERRORLIST|IDG_VS_ERRORLIST_ERRORGROUP<br /><br /> IDG_VS_ERRORLIST_WARNINGGROUP<br /><br /> IDG_VS_ERRORLIST_MESSAGEGROUP|
|Pesquisador de Chamadas|IDM_VS_TOOL_CALLBROWSER1.. 16|IDG_VS_TOOLBAR_CALLBROWSER1_ACTIONS<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_TYPE<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_CBSETTINGS|
|Pontos de interrupção|guidVSDebugGroup:IDM_BREAKPOINTS_WINDOW_TOOLBAR|IDG_BREAKPOINTS_WINDOW_NEW<br /><br /> IDG_BREAKPOINTS_WINDOW_DELETE<br /><br /> IDG_BREAKPOINTS_WINDOW_ALL<br /><br /> IDG_BREAKPOINTS_WINDOW_VIEW<br /><br /> IDG_BREAKPOINTS_WINDOW_EDIT<br /><br /> IDG_BREAKPOINTS_WINDOW_COLUMNS|
|Desmontagem|guidVSDebugGroup:IDM_DISASM_WINDOW_TOOLBAR|IDG_DISASM_WINDOW_TOOLBAR|
|Memória de 1 a 4|guidVSDebugGroup: IDM_MEMORY_WINDOW_TOOLBAR1... quatro|IDG_MEMORY_EXPRESSION1.. quatro<br /><br /> IDG_MEMORY_COLUMNS1.. quatro|
|Processos|guidVSDebugGroup: IDM_ATTACHED_PROCS_TOOLBAR|IDG_ATTACHED_PROCS_EXECCNTRL IDG_ATTACHED_PROCS_STEPPING<br /><br /> IDG_ATTACHED_PROCS_EXECCNTRL2<br /><br /> IDG_ATTACHED_PROCS_ATTACH<br /><br /> IDG_ATTACHED_PROCS_COLUMNS|

## <a name="see-also"></a>Confira também
- [Adicionar um controlador de menu a uma barra de ferramentas](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)
- [Adicionar uma barra de ferramentas a uma janela de ferramentas](../../extensibility/adding-a-toolbar-to-a-tool-window.md)
- [GUIDs e IDs dos menus do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)
