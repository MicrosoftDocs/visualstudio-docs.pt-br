---
title: Comandos definidos pelo IDE para estender sistemas de projeto | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, project systems
- project systems, environment-defined commands
ms.assetid: 0e33b8e9-16fa-4400-a941-e92d56120e7e
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 0e3dc6a30dedebd8a5bc25c53e86aff4d3315ff8
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53990864"
---
# <a name="ide-defined-commands-for-extending-project-systems"></a>Comandos definidos pelo IDE para estender sistemas de projeto
Quando você deseja estender sistemas de projeto, você pode usar os comandos e comando grupos fornecidos pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.  
  
 As seções a seguir listam os itens de comando que são especialmente úteis para estender sistemas de projeto.  
  
## <a name="command-menus"></a>Menus de comandos  
 A tabela a seguir mostra os menus de comando que são locais úteis para você colocar os comandos de alto nível que invocam um extensor de projeto.  
  
|Menu de comando|Descrição|  
|------------------|-----------------|  
|IDM_VS_MENU_PROJECT|O **projeto** menu de nível superior.|  
|IDM_VS_TOOL_PROJWIN|O **Gerenciador de soluções** barra de ferramentas.|  
  
## <a name="shortcut-menus"></a>Menus de atalho  
 A tabela a seguir mostra os menus de atalho que se aplicam quando um único nó é selecionado na **Gerenciador de soluções**, ou quando há várias seleções homogêneos na **Gerenciador de soluções**, que é quando todos os nós selecionados são do mesmo tipo.  
  
|Menu de atalho|Descrição|  
|-------------------|-----------------|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>|Aplica-se ao nó do projeto está selecionado.|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_ITEMNODE>|Aplica-se quando um arquivo é selecionado.|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_FOLDERNODE>|Se aplica quando uma pasta está selecionada.|  
|IDM_VS_CTXT_WEBREFFOLDER|Aplica-se quando a pasta de referência da Web está selecionada.|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCEROOT>|Aplica-se quando o nó raiz de referências chamado "Referências" está selecionado.|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCE>|Aplica-se ao nó de referência estiver selecionado; Isso inclui o assembly, COM e apenas referências do projeto. Não inclui referências da Web.|  
  
 A tabela a seguir mostra os menus de atalho que se aplicam quando a seleção na **Gerenciador de soluções** abrange várias hierarquias,  
  
|Menu de atalho|Descrição|  
|-------------------|-----------------|  
|IDM_VS_CTXT_XPROJ_SLNPROJ|Aplica-se quando a seleção atual contém o nó da solução e nós do projeto raiz.|  
|IDM_VS_CTXT_XPROJ_SLNITEM|Aplica-se quando a seleção atual contém os itens de projeto e o nó da solução.|  
|IDM_VS_CTXT_XPROJ_MULTIPROJ|Aplica-se quando a seleção atual consiste em vários projeto nós raiz apenas.|  
|IDM_VS_CTXT_XPROJ_PROJITEM|Aplica-se quando a seleção atual contiver uma mistura de nós de raiz do projeto e itens de projeto. Além disso, a seleção pode conter o nó da solução.|  
|IDM_VS_CTXT_XPROJ_MULTIITEM|Aplica-se quando a seleção atual contém itens de projeto de vários projetos na solução, ou itens de tipos diferentes são selecionados no mesmo projeto.|  
  
## <a name="command-groups"></a>Grupos de comando  
 A tabela a seguir mostra os grupos de comando que você pode usar ao estender projetos e que você pode acessar por meio de <xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE> menu de atalho.  
  
|Grupo de comandos|Descrição|  
|-------------------|-----------------|  
|IDG_VS_CTXT_PROJECT_BUILD|Comandos para compilar, recompilar e implantar o projeto.|  
|IDG_VS_CTXT_COMPILELINK|Comandos para compilar e vincular o projeto.|  
|IDG_VS_CTXT_PROJECT_CONFIG|Comandos que definir a configuração de projeto e a ordem de compilação.|  
|IDG_VS_CTXT_PROJECT_ADD|Comandos que adicionar itens ao projeto.|  
|IDG_VS_CTXT_PROJECT_START|Comandos que defina o projeto de inicialização associado com a tecla F5.|  
|IDG_VS_CTXT_PROJECT_SAVE|Comandos para salvar itens de projeto.|  
|IDG_VS_CTXT_PROJECT_DEBUG|Comandos de depuração.|  
|IDG_VS_CTXT_PROJECT_SCC|Comandos de controle de origem.|  
|IDG_VS_CTXT_PROJECT_TRANSFER|Comandos para recortar, copiar e colar operações.|  
|IDG_VS_CTXT_PROJECT_PROPERTIES|Comandos que fornecem acesso para o **propriedades do projeto** caixa de diálogo.|  
  
## <a name="see-also"></a>Consulte também  
 [Como os VSPackages adicionam elementos da Interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [MenuCommands Vs. OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md)   
 [Criar grupos reutilizáveis de botões](../../extensibility/creating-reusable-groups-of-buttons.md)