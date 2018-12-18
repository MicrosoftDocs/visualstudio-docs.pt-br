---
title: GUIDs e IDs de Menus do Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- visual studio menus
- visual studio groups
- id
- existing menus
- guid
- menus
ms.assetid: 84639d86-dd21-4b35-9988-6bb654162488
caps.latest.revision: 13
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 72ba04f5f33b3b9ef5030326fddb69d83e0a8f9d
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51762689"
---
# <a name="guids-and-ids-of-visual-studio-menus"></a>GUIDs e IDs de menus do Visual Studio
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Este tópico enumera os valores GUID e ID de menus e grupos na barra de menus do Visual Studio. Esses valores são definidos em arquivos. VSCT que são instalados como parte do SDK do Visual Studio. Para obter mais informações, consulte [IDE-Defined comandos, Menus e grupos](../../extensibility/internals/ide-defined-commands-menus-and-groups.md).  
  
 Para obter mais informações sobre como trabalhar com objetos de (IDE) do ambiente de desenvolvimento integrado que são definidos em arquivos. VSCT, consulte [estendendo Menus e comandos](../../extensibility/extending-menus-and-commands.md).  
  
 Os menus e grupos na barra de menus do Visual Studio usam o GUID `guidSHLMainMenu`. No menu da barra em si tem uma ID de `IDM_VS_TOOL_MAINMENU`.  
  
## <a name="groups-on-the-visual-studio-menu-bar"></a>Grupos na barra de menus do Visual Studio  
 Para adicionar um menu a barra de menus, defina um desses grupos como seu pai.  
  
|Grupo|ID|  
|-----------|--------|  
|Arquivo/Editar/exibir|IDG_VS_MM_FILEEDITVIEW|  
|Refatoração|IDG_VS_MM_REFACTORING:|  
|Projeto|IDG_VS_MM_PROJECT|  
|Build|IDG_VS_MM_BUILDDEBUGRUN|  
|Formato/Tools|IDG_VS_MM_TOOLSADDINS|  
|Janela/Ajuda/Community|IDG_VS_MM_WINDOWHELP|  
|Suplementos|IDG_VS_MM_MACROS|  
|FullScreenBar|IDG_VS_MM_FULLSCREENBAR|  
  
## <a name="menus-on-the-visual-studio-menu-bar"></a>Menus na barra de menus do Visual Studio  
 Para adicionar um grupo a um menu existente do Visual Studio, defina um dos seguintes menus como seu pai. Submenus não estão incluídos nessa lista.  
  
|Menu|ID|  
|----------|--------|  
|Arquivo|IDM_VS_MENU_FILE|  
|Editar|IDM_VS_MENU_EDIT|  
|Exibir|IDM_VS_MENU_VIEW|  
|Refatoração|IDM_VS_MENU_REFACTORING|  
|Projeto|IDM_VS_MENU_PROJECT|  
|Build|IDM_VS_MENU_BUILD|  
|Formatar|IDM_VS_MENU_FORMAT|  
|Ferramentas|IDM_VS_MENU_TOOLS|  
|Janela|IDM_VS_MENU_WINDOW|  
|Suplementos|IDM_VS_MENU_ADDINS|  
|Comunidade|IDM_VS_MENU_COMMUNITY|  
|Ajuda|IDM_VS_MENU_HELP|  
  
## <a name="groups-on-visual-studio-menus"></a>Grupos de Menus do Visual Studio  
 As listas a seguir mostram os grupos que descendem diretamente dos menus na barra de menus do Visual Studio. A maneira mais rápida para adicionar um comando ao menu Visual Studio é definir um desses grupos como o pai. Grupos que descendem dos seus submenus não aparecem nesta seção.  
  
### <a name="file-menu-groups"></a>Grupos de menus do arquivo  
  
|Grupo|ID|  
|-----------|--------|  
|Novo/abrir|IDG_VS_FILE_FILE|  
|Adicionar|IDG_VS_FILE_ADD|  
|Solução|IDG_VS_FILE_SOLUTION|  
|Diversos|IDG_VS_FILE_MISC|  
|Salvar|IDG_VS_FILE_SAVE|  
|Renomear|IDG_VS_FILE_RENAME|  
|Navegador|IDG_VS_FILE_BROWSER|  
|Imprimir|IDG_VS_FILE_PRINT|  
|Usado mais recentemente|IDG_VS_FILE_MRU|  
|Mover|IDG_VS_FILE_MOVE|  
|Sair|IDG_VS_FILE_EXIT|  
  
### <a name="edit-menu-groups"></a>Editar grupos de menus  
  
|Grupo|ID|  
|-----------|--------|  
|Desfazer/refazer|IDG_VS_EDIT_UNDOREDO|  
|Recortar/copiar/colar|IDG_VS_EDIT_CUTCOPY|  
|Selecionar|IDG_VS_EDIT_SELECT|  
|Ir para|IDG_VS_EDIT_GOTO|  
|Localizar|IDG_VS_EDIT_FIND|  
|Objetos|IDG_VS_EDIT_OBJECTS|  
|Verbos OLE|IDG_VS_EDIT_OLEVERBS|  
|Comando bem|IDG_VS_EDIT_COMMANDWELL|  
  
### <a name="refactor-menu-groups"></a>Refatorar os grupos de menus  
  
|Grupo|ID|  
|-----------|--------|  
|Comuns|IDG_REFACTORING_COMMON|  
|Avançado|IDG_REFACTORING_ADVANCED|  
  
### <a name="view-menu-groups"></a>Exibir grupos de Menu  
  
|Grupo|ID|  
|-----------|--------|  
|Código de formulário|IDG_VS_VIEW_FORMCODE|  
|Navegador|IDG_VS_VIEW_BROWSER|  
|Definir modos de exibição|IDG_VS_VIEW_DEFINEVIEWS|  
|Windows|IDG_VS_VIEW_WINDOWS|  
|Arquiteto Windows|IDG_VS_VIEW_ARCH_WINDOWS|  
|Windows da organização|IDG_VS_VIEW_ORG_WINDOWS|  
|Navegador de código|IDG_VS_VIEW_CODEBROWSENAV_WINDOWS|  
|Desenvolvimento Windows|IDG_VS_VIEW_DEV_WINDOWS|  
|Barras de ferramentas|IDG_VS_VIEW_TOOLBARS|  
|Símbolos|IDG_VS_VIEW_SYMBOLNAVIGATE|  
|Navegar|IDG_VS_VIEW_NAVIGATE|  
|Navegue pequenos|IDG_VS_VIEW_SMALLNAVIGATE|  
|Pesquisador de Objetos|IDG_VS_VIEW_OBJBRWSR|  
|Comando bem|IDG_VS_VIEW_COMMANDWELL|  
|Páginas de propriedade|IDG_VS_VIEW_PROPPAGES|  
|Atualizar|IDG_VS_VIEW_REFRESH|  
  
### <a name="project-menu-groups"></a>Grupos de menus do projeto  
  
|Grupo|ID|  
|-----------|--------|  
|Diversos adicionar|IDG_VS_PROJ_MISCADD|  
|Adicionar|IDG_VS_PROJ_ADD|  
|Pasta|IDG_VS_PROJ_FOLDER|  
|Descarregamento/recarregamento|IDG_VS_PROJ_UNLOADRELOAD|  
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
|Trechos de código|IDG_VS_TOOLS_SNIPPETS|  
|Subconjunto do objeto|IDG_VS_TOOLS_OBJSUBSET|  
|Opções|IDG_VS_TOOLS_OPTIONS|  
|Outras 2|IDG_VS_TOOLS_OTHER2|  
|Ferramentas externas|IDG_VS_TOOLS_EXT_TOOLS|  
|Personalizações externas|IDG_VS_TOOLS_EXT_CUST|  
  
### <a name="window-menu-groups"></a>Grupos de menus da janela  
  
|Grupo|ID|  
|-----------|--------|  
|Novo|IDG_VS_WINDOW_NEW|  
|Encaixe/de fechamento|IDG_VS_DOCKCLOSE|  
|Encaixe/ocultar|IDG_VS_DOCKHIDE|  
|Organizar|IDG_VS_WINDOW_ARRANGE|  
|Navegação|IDG_VS_WINDOW_NAVIGATION|  
|Lista|IDG_VS_WINDOW_LIST|  
  
### <a name="help-menu-groups"></a>Grupos de menus ajuda  
  
|Grupo|ID|  
|-----------|--------|  
|Exemplos|IDG_VS_HELP_SAMPLES|  
|Suporte|IDG_VS_HELP_SUPPORT|  
|Sobre o|IDG_VS_HELP_ABOUT|  
  
## <a name="submenus-of-visual-studio-menus"></a>Submenus de Menus do Visual Studio  
 A hierarquia a seguir mostra os submenus que estão associados com os menus na barra de menus do Visual Studio. Como apenas um grupo pode ter um menu como seu pai, cada submenu deve descender de um grupo em um menu, em vez de diretamente do menu. Para obter mais informações sobre a relação entre os submenus de menus e grupos, consulte [adicionando um Submenu a um Menu](../../extensibility/adding-a-submenu-to-a-menu.md).  
  
> [!NOTE]
>  Os nomes dos menus na barra de menus do Visual Studio não são mostrados separadamente nesta hierarquia porque eles podem ser inferidos de convenção de nomenclatura para grupos no IDE, da seguinte maneira: IDG_VS_*nome do Menu*_*nomedegrupo*.  
  
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
|||IDG_VS_WNDO_OTRWNDWS1... 6|  
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
  
## <a name="see-also"></a>Consulte também  
 [GUIDs e IDs de barras de ferramentas do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)   
 [GUIDs e IDs de comandos do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)   
 [Arquivos da tabela de comandos do Visual Studio (.Vsct)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)

