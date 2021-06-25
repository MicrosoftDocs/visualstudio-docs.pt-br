---
title: GUIDs e IDs dos menus do Visual Studio | Microsoft Docs
description: Exiba uma lista de valores de GUID e ID para os menus e grupos na barra de menus do Visual Studio incluída no IDE (ambiente de desenvolvimento integrado) do Visual Studio.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- visual studio menus
- visual studio groups
- id
- existing menus
- guid
- menus
ms.assetid: 84639d86-dd21-4b35-9988-6bb654162488
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bceee5fce8a77ad5169020bd3d21896bdbc71443
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112898065"
---
# <a name="guids-and-ids-of-visual-studio-menus"></a>GUIDs e IDs dos menus do Visual Studio
Este artigo enumera os valores de GUID e ID dos menus e grupos na barra de menus do Visual Studio. Esses valores são definidos em arquivos *. vsct* que são instalados como parte do SDK do Visual Studio. Para obter mais informações, consulte [comandos, menus e grupos definidos pelo IDE](../../extensibility/internals/ide-defined-commands-menus-and-groups.md).

 Para obter mais informações sobre como trabalhar com objetos IDE (ambiente de desenvolvimento integrado) definidos em arquivos *. vsct* , consulte [estender menus e comandos](../../extensibility/extending-menus-and-commands.md).

 Os menus e grupos na barra de menus do Visual Studio usam o GUID `guidSHLMainMenu` . A própria barra de menus tem uma ID de `IDM_VS_TOOL_MAINMENU` .

## <a name="groups-on-the-visual-studio-menu-bar"></a>Grupos na barra de menus do Visual Studio
 Para adicionar um menu à barra de menus, defina um desses grupos como seu pai.

|Grupo|ID|
|-----------|--------|
|Arquivo/Editar/Exibir|IDG_VS_MM_FILEEDITVIEW|
|Refatoração|IDG_VS_MM_REFACTORING:|
|Project|IDG_VS_MM_PROJECT|
|Build|IDG_VS_MM_BUILDDEBUGRUN|
|Formato/ferramentas|IDG_VS_MM_TOOLSADDINS|
|Janela/ajuda/Comunidade|IDG_VS_MM_WINDOWHELP|
|Suplementos|IDG_VS_MM_MACROS|
|FullScreenBar|IDG_VS_MM_FULLSCREENBAR|

## <a name="menus-on-the-visual-studio-menu-bar"></a>Menus na barra de menus do Visual Studio
 Para adicionar um grupo a um menu existente do Visual Studio, defina um dos seguintes menus como seu pai. Os submenus não são incluídos nesta lista.

|Menu|ID|
|----------|--------|
|Arquivo|IDM_VS_MENU_FILE|
|Editar|IDM_VS_MENU_EDIT|
|Visualizar|IDM_VS_MENU_VIEW|
|Refatoração|IDM_VS_MENU_REFACTORING|
|Project|IDM_VS_MENU_PROJECT|
|Build|IDM_VS_MENU_BUILD|
|Formatar|IDM_VS_MENU_FORMAT|
|Ferramentas|IDM_VS_MENU_TOOLS|
|Extensões|IDM_VS_MENU_EXTENSIONS|
|Janela|IDM_VS_MENU_WINDOW|
|Suplementos|IDM_VS_MENU_ADDINS|
|Comunidade|IDM_VS_MENU_COMMUNITY|
|Ajuda|IDM_VS_MENU_HELP|

## <a name="groups-on-visual-studio-menus"></a>Grupos nos menus do Visual Studio
 As listas a seguir mostram os grupos que descendem diretamente dos menus na barra de menus do Visual Studio. A maneira mais rápida de adicionar um comando a um menu do Visual Studio é definir um desses grupos como o pai. Os grupos que descendem de submenus não aparecem nesta seção.

### <a name="file-menu-groups"></a>Grupos de menus de arquivo

|Grupo|ID|
|-----------|--------|
|Novo/abrir|IDG_VS_FILE_FILE|
|Adicionar|IDG_VS_FILE_ADD|
|Solução|IDG_VS_FILE_SOLUTION|
|Diversos|IDG_VS_FILE_MISC|
|Salvar|IDG_VS_FILE_SAVE|
|Renomear|IDG_VS_FILE_RENAME|
|Navegador|IDG_VS_FILE_BROWSER|
|Impressão|IDG_VS_FILE_PRINT|
|Usado mais recentemente|IDG_VS_FILE_MRU|
|Mover|IDG_VS_FILE_MOVE|
|Fechar|IDG_VS_FILE_EXIT|

### <a name="edit-menu-groups"></a>Editar grupos de menus

|Grupo|ID|
|-----------|--------|
|Desfazer/refazer|IDG_VS_EDIT_UNDOREDO|
|Recortar/copiar/colar|IDG_VS_EDIT_CUTCOPY|
|Selecionar|IDG_VS_EDIT_SELECT|
|Fim|IDG_VS_EDIT_GOTO|
|Localizar|IDG_VS_EDIT_FIND|
|Objetos|IDG_VS_EDIT_OBJECTS|
|Verbos OLE|IDG_VS_EDIT_OLEVERBS|
|Caixa de comando|IDG_VS_EDIT_COMMANDWELL|

### <a name="refactor-menu-groups"></a>Refatorar grupos de menus

|Grupo|ID|
|-----------|--------|
|Comum|IDG_REFACTORING_COMMON|
|Avançado|IDG_REFACTORING_ADVANCED|

### <a name="view-menu-groups"></a>Exibir grupos de menus

|Grupo|ID|
|-----------|--------|
|Código de formulário|IDG_VS_VIEW_FORMCODE|
|Navegador|IDG_VS_VIEW_BROWSER|
|Definir exibições|IDG_VS_VIEW_DEFINEVIEWS|
|Windows|IDG_VS_VIEW_WINDOWS|
|Arquitetar janelas|IDG_VS_VIEW_ARCH_WINDOWS|
|Janelas da organização|IDG_VS_VIEW_ORG_WINDOWS|
|Navegador de código|IDG_VS_VIEW_CODEBROWSENAV_WINDOWS|
|Janelas de desenvolvimento|IDG_VS_VIEW_DEV_WINDOWS|
|Barras de ferramentas|IDG_VS_VIEW_TOOLBARS|
|Símbolos|IDG_VS_VIEW_SYMBOLNAVIGATE|
|Navegar|IDG_VS_VIEW_NAVIGATE|
|Navegação pequena|IDG_VS_VIEW_SMALLNAVIGATE|
|Pesquisador de Objetos|IDG_VS_VIEW_OBJBRWSR|
|Caixa de comando|IDG_VS_VIEW_COMMANDWELL|
|Páginas de propriedade|IDG_VS_VIEW_PROPPAGES|
|Atualizar|IDG_VS_VIEW_REFRESH|

### <a name="project-menu-groups"></a>Grupos de menus do projeto

|Grupo|ID|
|-----------|--------|
|Adição de diversos|IDG_VS_PROJ_MISCADD|
|Adicionar|IDG_VS_PROJ_ADD|
|Pasta|IDG_VS_PROJ_FOLDER|
|Descarregar/recarregar|IDG_VS_PROJ_UNLOADRELOAD|
|Referência|IDG_VS_PROJ_REFERENCE|
|Opções|IDG_VS_PROJ_OPTIONS|
|Configurações|IDG_VS_PROJ_SETTINGS|

### <a name="build-menu-groups"></a>Criar grupos de menus

|Grupo|ID|
|-----------|--------|
|Solução|IDG_VS_BUILD_SOLUTION|
|Seleção|IDG_VS_BUILD_SELECTION|
|Otimização Guiada por Perfil|IDG_VS_PGO_SELECTION|
|Diversos|IDG_VS_BUILD_MISC|
|Cancelar|IDG_VS_BUILD_CANCEL|

### <a name="tools-menu-groups"></a>Grupos de menus de ferramentas

|Grupo|ID|
|-----------|--------|
|Linha de Comando|IDG_VS_TOOLS_CMDLINE|
|Snippets|IDG_VS_TOOLS_SNIPPETS|
|Subconjunto de objetos|IDG_VS_TOOLS_OBJSUBSET|
|Opções|IDG_VS_TOOLS_OPTIONS|
|Outros 2|IDG_VS_TOOLS_OTHER2|
|Ferramentas Externas|IDG_VS_TOOLS_EXT_TOOLS|
|Personalizações externas|IDG_VS_TOOLS_EXT_CUST|

### <a name="window-menu-groups"></a>Grupos de menus de janela

|Grupo|ID|
|-----------|--------|
|Novo|IDG_VS_WINDOW_NEW|
|Encaixar/fechar|IDG_VS_DOCKCLOSE|
|Encaixar/ocultar|IDG_VS_DOCKHIDE|
|Organizar|IDG_VS_WINDOW_ARRANGE|
|Navegação|IDG_VS_WINDOW_NAVIGATION|
|Lista|IDG_VS_WINDOW_LIST|

### <a name="help-menu-groups"></a>Grupos de menus de ajuda

|Grupo|ID|
|-----------|--------|
|Exemplos|IDG_VS_HELP_SAMPLES|
|Suporte|IDG_VS_HELP_SUPPORT|
|Sobre|IDG_VS_HELP_ABOUT|

## <a name="submenus-of-visual-studio-menus"></a>Submenus dos menus do Visual Studio
 A hierarquia a seguir mostra os submenus associados aos menus na barra de menus do Visual Studio. Como apenas um grupo pode ter um menu como seu pai, cada submenu deve ser decrescente de um grupo em um menu, em vez de diretamente do menu. Para obter mais informações sobre a relação entre menus, grupos e submenus, consulte [Adicionar um submenu a um menu](../../extensibility/adding-a-submenu-to-a-menu.md).

> [!NOTE]
> Os nomes dos menus na barra de menus do Visual Studio não são mostrados separadamente nesta hierarquia porque podem ser inferidos da Convenção de nomenclatura para grupos no IDE, da seguinte maneira: *IDG_VS_ \<Menu Name\> _ \<Group Name\>*.

|Grupo pai|Submenu|Grupos filho|
|------------------|-------------|------------------|
|IDG_VS_FILE_FILE|IDM_VS_CSCD_NEW|IDG_VS_FILE_NEW_CASCADE|
||IDM_VS_CSCD_OPEN|IDG_VS_FILE_OPENP_CASCADE|
|||IDG_VS_FILE_OPENF_CASCADE|
|IDG_VS_FILE_ADD|IDM_VS_CSCD_ADD|IDG_VS_FILE_ADD_PROJECT_NEW|
|||IDG_VS_FILE_ADD_PROJECT_EXI|
|IDG_VS_FILE_MRU|IDM_VS_CSCD_FILEMRU|IDG_VS_FILE_FMRU_CASCADE|
||IDM_VS_CSCD_PROJMRU|IDG_VS_FILE_PMRU_CASCADE|
|IDG_VS_FILE_MOVE|IDM_VS_CSCD_MOVETOPRJ|IDG_VS_FILE_MOVE_CASCADE|
|||IDG_VS_FILE_MOVE_PICKER|
|IDG_VS_VIEW_DEV_WINDOWS|IDM_VS_CSCD_FINDRESULTS|IDG_VS_WNDO_FINDRESULTS|
||IDM_VS_CSCD_WINDOWS|IDG_VS_VIEW_CALLBROWSER|
|||IDG_VS_WNDO_OTRWNDWS1... 152|
|||IDG_VS_WNDO_WINDOWS2|
|IDG_VS_VIEW_TOOLBARS|IDM_VS_CSCD_COMMANDBARS||
|IDG_VS_EDIT_GOTO|IDM_VS_EDITOR_FIND_MENU||
|IDG_VS_EDIT_OBJECTS|IDM_VS_CSCD_MNUDES|IDG_VS_MNUDES_INSERT|
|||IDG_VS_MNUDES_EDITNAMES|
||IDM_VS_CSCD_OLEVERBS|IDG_VS_EDIT_OLEVERBS|
|IDG_VS_BUILD_SELECTION|IDM_VS_CSCD_BUILD|IDG_VS_BUILD_CASCADE|
|||IDG_VS_BUILD_PROJPICKER|
||IDM_VS_CSCD_REBUILD|IDG_VS_REBUILD_CASCADE|
|||IDG_VS_REBUILD_PROJPICKER|
||IDM_VS_CSCD_PROJONLY|IDG_VS_PROJONLY_CASCADE|
||IDM_VS_CSCD_CLEAN|IDG_VS_CLEAN_CASCADE|
|||IDG_VS_CLEAN_PROJPICKER|
||IDM_VS_CSCD_DEPLOY|IDG_VS_DEPLOY_CASCADE|
|||IDG_VS_DEPLOY_PROJPICKER|
|IDG_VS_PGO_SELECTION|IDM_VS_CSCD_PGO_BUILD|IDG_VS_PGO_BUILD_CASCADE_BUILD|
|||IDG_VS_PGO_BUILD_CASCADE_RUN|

## <a name="see-also"></a>Confira também
- [GUIDs e IDs das barras de ferramentas do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)
- [GUIDs e IDs de comandos do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)
- [Arquivos de tabela de comando do Visual Studio (. vsct)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
