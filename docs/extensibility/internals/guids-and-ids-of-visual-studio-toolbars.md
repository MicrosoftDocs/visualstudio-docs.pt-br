---
title: GUIDs e IDs de barras de ferramentas do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- visual studio groups
- toolbars
- visual studio toolbar
- id
- toolgar group
- tool window toolbar
- guid
ms.assetid: c9cacd57-9225-450f-a9ac-cbf3168ea844
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 6982835b9d3b6259a47439dbe7b1b9252edc3dbe
ms.sourcegitcommit: 1c2ed640512ba613b3bbbc9ce348e28be6ca3e45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2018
ms.locfileid: "39499000"
---
# <a name="guids-and-ids-of-visual-studio-toolbars"></a>Barras de ferramentas GUIDs e IDs do Visual Studio
Este tópico enumera os valores GUID e ID das barras de ferramentas que estão incluídos no ambiente de desenvolvimento integrado (IDE) do Visual Studio e dos grupos que eles contêm. Esses valores são definidos no *VSCT* arquivos que são instalados como parte do SDK do Visual Studio. Para obter mais informações, consulte [definidos pelo IDE comandos, menus e grupos](../../extensibility/internals/ide-defined-commands-menus-and-groups.md).  
  
> [!NOTE]
>  Muitas das barras de ferramentas disponíveis para o Visual Studio não são definidas pelo Visual Studio e sua GUID e valores de ID não são públicos. Este tópico lista somente as barras de ferramentas que são definidas no SDK do Visual Studio *VSCT* arquivos.  
  
 Para obter mais informações sobre como trabalhar com objetos IDE que são definidos no *VSCT* arquivos, consulte [estendem os menus e comandos](../../extensibility/extending-menus-and-commands.md).  
  
 Barras de ferramentas padrão fornecidas pelo IDE do Visual Studio usam o GUID `guidSHLMainMenu`, exceto quando especificado de outra forma usando `GUID:ID` sintaxe.  
  
## <a name="ide-toolbars"></a>Barras de ferramentas do IDE  
 As barras de ferramentas a seguir são fornecidas pelo IDE do Visual Studio. Barras de ferramentas podem ser exibidas selecionando-as na **barras de ferramentas** submenu a **ferramentas** menu. Barras de ferramentas em janelas de ferramentas não estão incluídas nesta seção.  
  
 Somente os grupos podem descendem diretamente de barras de ferramentas. Para adicionar um grupo, defina seu pai para o GUID e a ID da barra de ferramentas. Para adicionar um botão à barra de ferramentas, defina seu pai a um grupo na barra de ferramentas.  
  
|Barra de ferramentas|ID|  
|-------------|--------|  
|Padrão|IDM_VS_TOOL_STANDARD|  
|Build|IDM_VS_TOOL_BUILD|  
|Editor de texto|IDM_VS_TOOL_TEXTEDITOR|  
|Depurar|guidVSDebugGroup:IDM_DEBUG_TOOLBAR|  
|Local de depuração|guidVSDebugGroup:IDM_DEBUG_CONTEXT_TOOLBAR|  
  
### <a name="special-toolbars"></a>Barras de ferramentas especiais  
 Essas barras de ferramentas são definidas pelo IDE do Visual Studio, mas eles servem funções especializadas e não hospedam os grupos de comando.  
  
|Barra de ferramentas|ID|  
|-------------|--------|  
|Adicionar comando|IDM_VS_TOOL_ADDCOMMAND|  
|Indefinido|IDM_VS_TOOL_UNDEFINED|  
|Esquema XML|IDM_VS_TOOL_SCHEMA|  
|dados XML|IDM_VS_TOOL_DATA|  
  
## <a name="groups-on-the-ide-toolbars"></a>Grupos nas barras de ferramentas IDE  
 Para adicionar um botão à barra de ferramentas padrão, defina um dos seguintes grupos como seu pai. Os grupos são classificados pela barra de ferramentas pai.  
  
### <a name="standard-toolbar-groups"></a>Grupos de barra de ferramentas padrão  
  
|Nome|ID|  
|----------|--------|  
|Salvar/abrir|IDG_VS_TOOLSB_SAVEOPEN|  
|Recortar/copiar|IDG_VS_TOOLSB_CUTCOPY|  
|Desfazer/refazer|IDG_VS_TOOLSB_UNDOREDO|  
|Execução/Build.|IDG_VS_TOOLSB_RUNBUILD|  
|Pesquisar|IDG_VS_TOOLSB_SEARCH|  
|Windows|IDG_VS_TOOLSB_WINDOWS|  
|Novas janelas|IDG_VS_TOOLSB_NEWWINDOWS|  
|Carregar/salvar|IDG_VS_WINDOWUI_LOADSAVE|  
|Medidor|IDG_VS_TOOLSB_GAUGE|  
  
### <a name="build-toolbar-groups"></a>Criar grupos de barra de ferramentas  
  
|Nome|ID|  
|----------|--------|  
|Barra de compilação|IDG_VS_BUILDBAR|  
|Cancelar|IDG_VS_BUILD_CANCEL|  
  
### <a name="text-editor-toolbar-groups"></a>Grupos de barra de ferramentas do editor de texto  
  
|Nome|ID|  
|----------|--------|  
|Conclusão|IDM_VS_TOOL_TEXTEDITOR|  
|Recuar|IDG_VS_EDITTOOLBAR_INDENT|  
|Comentário|IDG_VS_EDITTOOLBAR_COMMENT|  
|Indicadores|IDG_VS_EDITTOOLBAR_TEMPBOOKMARKS|  
  
### <a name="debug-toolbar-groups"></a>Grupos de barra de ferramentas de depuração  
  
|Nome|ID|  
|----------|--------|  
|Execução|IDM_DEBUG_TOOLBAR|  
|Depuração|IDG_DEBUG_TOOLBAR_STEPPING|  
|Inspeção|IDG_DEBUG_TOOLBAR_WATCH|  
|Windows|IDG_DEBUG_TOOLBAR_WINDOWS|  
  
### <a name="debug-location-toolbar-groups"></a>Grupos de barra de ferramentas do local de depuração  
  
|Nome|ID|  
|----------|--------|  
|Local de depuração|IDG_DEBUG_CONTEXT_TOOLBAR|  
  
## <a name="tool-window-toolbars"></a>Barras de ferramentas da janela de ferramentas  
 Barras de ferramentas podem aparecer diretamente no IDE ou nas janelas de ferramentas, como **Gerenciador de soluções**. Como as janelas de ferramentas não estão definidas na *VSCT* arquivos, barras de ferramentas de janela de ferramenta não definiu os pais. Em vez disso, eles são colocados no código. A tabela a seguir mostra as barras de ferramentas que aparecem nas janelas de ferramentas no IDE e os grupos de comando que eles contêm.  
  
> [!NOTE]
>  Barras de ferramentas e grupos de usam o GUID `guidSHLMainMenu`, exceto quando especificado de outra forma, usando a sintaxe GUID:ID. Quando um GUID for especificado para uma barra de ferramentas, ele também se aplica aos grupos que descendem daquela barra de ferramentas.  
  
|Janela de ferramentas|Barra de ferramentas|Grupos|  
|-----------------|-------------|------------|  
|Gerenciador de Soluções|IDM_VS_TOOL_PROJWIN|IDG_VS_PROJ_TOOLBAR1... 5|  
|conexões de servidor|guid_SE_MenuGroup:IDM_SE_TOOLBAR_SERVEREXPLORER|IDG_SE_TOOLBAR_REFRESH|  
|Propriedades|IDM_VS_TOOL_PROPERTIES|IDG_VS_PROPERTIES_SORT<br /><br /> IDG_VS_PROPERTIES_PAGES|  
|Exibição de Classe|IDM_VS_TOOL_CLASSVIEW|IDG_VS_CLASSVIEW_FOLDERS<br /><br /> IDG_VS_CLASSVIEW_SEARCH<br /><br /> IDG_VS_CLASSVIEW_SETTINGS|  
|Exibição de Classe|IDM_VS_TOOL_CLASSVIEW_GO|IDG_VS_CLASSVIEW_SEARCH2|  
|Pesquisador de Objetos|IDM_VS_TOOL_OBJBROWSER|IDG_VS_OBJBROWSER_SUBSETS<br /><br /> IDG_VS_OBJBROWSER_SEARCH<br /><br /> IDG_VS_OBJBROWSER_ADDREFERENCE<br /><br /> IDG_VS_OBJBROWSER_BROWSERSETTINGS|  
|Pesquisador de Objetos|IDM_VS_TOOL_OBJECT_BROWSER_GO|IDG_VS_OBJBROWSER_SEARCH2|  
|Saída|IDM_VS_TOOL_OUTPUTWINDOW|IDG_VS_OUTPUTWINDOW_SELECT<br /><br /> IDG_VS_OUTPUTWINDOW_GOTO<br /><br /> IDG_VS_OUTPUTWINDOW_NEXTPREV<br /><br /> IDG_VS_OUTPUTWINDOW_CLEAR<br /><br /> IDG_VS_OUTPUTWINDOW_WORDWRAP|  
|Localizar e Substituir|IDM_VS_TOOL_UNIFIEDFIND|IDG_VS_FINDTAB<br /><br /> IDG_VS_REPLACETAB|  
|Localizar resultados 1|IDM_VS_TOOL_FINDRESULTS1|IDG_VS_FINDRESULTS1_GOTO<br /><br /> IDG_VS_FINDRESULTS1_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS1_CLEAR<br /><br /> IDG_VS_FINDRESULTS1_STOPFIND|  
|Localizar resultados 2|IDM_VS_TOOL_FINDRESULTS2|IDG_VS_FINDRESULTS2_GOTO<br /><br /> IDG_VS_FINDRESULTS2_NEXTPREV<br /><br /> IDG_VS_FINDRESULTS2_CLEAR<br /><br /> IDG_VS_FINDRESULTS2_STOPFIND|  
|Trecho de código|IDM_VS_TOOL_SNIPPETMENUS|IDG_VS_SNIPPET_REPL<br /><br /> IDG_VS_SNIPPET_REF<br /><br /> IDG_VS_SNIPPET_PROP|  
|Indicadores|IDM_VS_TOOL_BOOKMARKWIND|IDG_VS_BWNEWFOLDER<br /><br /> IDG_VS_BWNEXTBM<br /><br /> IDG_VS_BWNEXTBMF<br /><br /> IDG_VS_BWENABLE<br /><br /> IDG_VS_BWDELETE|  
|Lista de Tarefas|IDM_VS_TOOL_TASKLIST|IDG_VS_TASKLIST_PROVIDERLIST|  
|Tarefas do usuário|IDM_VS_TOOL_USERTASKS|IDG_VS_TASKLIST_PROVIDERLIST<br /><br /> IDG_VS_USERTASKS_EDIT|  
|Lista de Erros|IDM_VS_TOOL_ERRORLIST|IDG_VS_ERRORLIST_ERRORGROUP<br /><br /> IDG_VS_ERRORLIST_WARNINGGROUP<br /><br /> IDG_VS_ERRORLIST_MESSAGEGROUP|  
|Pesquisador de chamadas|IDM_VS_TOOL_CALLBROWSER1... 16|IDG_VS_TOOLBAR_CALLBROWSER1_ACTIONS<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_TYPE<br /><br /> IDG_VS_TOOLBAR_CALLBROWSER1_CBSETTINGS|  
|Pontos de interrupção|guidVSDebugGroup:IDM_BREAKPOINTS_WINDOW_TOOLBAR|IDG_BREAKPOINTS_WINDOW_NEW<br /><br /> IDG_BREAKPOINTS_WINDOW_DELETE<br /><br /> IDG_BREAKPOINTS_WINDOW_ALL<br /><br /> IDG_BREAKPOINTS_WINDOW_VIEW<br /><br /> IDG_BREAKPOINTS_WINDOW_EDIT<br /><br /> IDG_BREAKPOINTS_WINDOW_COLUMNS|  
|Desmontagem|guidVSDebugGroup:IDM_DISASM_WINDOW_TOOLBAR|IDG_DISASM_WINDOW_TOOLBAR|  
|Memória de 1 a 4|guidVSDebugGroup:IDM_MEMORY_WINDOW_TOOLBAR1... 4|IDG_MEMORY_EXPRESSION1... 4<br /><br /> IDG_MEMORY_COLUMNS1... 4|  
|Processos|guidVSDebugGroup:IDM_ATTACHED_PROCS_TOOLBAR|IDG_ATTACHED_PROCS_EXECCNTRL IDG_ATTACHED_PROCS_STEPPING<br /><br /> IDG_ATTACHED_PROCS_EXECCNTRL2<br /><br /> IDG_ATTACHED_PROCS_ATTACH<br /><br /> IDG_ATTACHED_PROCS_COLUMNS|  
  
## <a name="see-also"></a>Consulte também  
 [Adicionar um controlador de menu a uma barra de ferramentas](../../extensibility/adding-a-menu-controller-to-a-toolbar.md)   
 [Adicionar uma barra de ferramentas para uma janela de ferramentas](../../extensibility/adding-a-toolbar-to-a-tool-window.md)   
 [Menus de GUIDs e IDs do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)