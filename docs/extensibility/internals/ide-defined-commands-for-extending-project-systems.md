---
title: Comandos definidos pelo IDE para a extensão de sistemas de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
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
ms.openlocfilehash: 4941f5d842f311f078594ee9a9deef02219ea05d
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31132009"
---
# <a name="ide-defined-commands-for-extending-project-systems"></a>Comandos definidos pelo IDE para a extensão de sistemas de projeto
Quando você deseja estender sistemas de projeto, você pode usar os comandos e comando grupos fornecidos pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.  
  
 As seções a seguir listam os itens de comando que são especialmente úteis para estender a sistemas de projeto.  
  
## <a name="command-menus"></a>Menus de comandos  
 A tabela a seguir mostra os menus de comando que são úteis locais para colocar os comandos de alto nível que invocam um extensor de projeto.  
  
|Menu comando|Descrição|  
|------------------|-----------------|  
|IDM_VS_MENU_PROJECT|O **projeto** menus de nível superior.|  
|IDM_VS_TOOL_PROJWIN|O **Solution Explorer** barra de ferramentas.|  
  
## <a name="shortcut-menus"></a>Menus de atalho  
 A tabela a seguir mostra os menus de atalho que se aplicam quando um único nó é selecionado no **Solution Explorer**, ou quando há várias seleções homogêneos no **Solution Explorer**, que é quando todos os nós selecionados são do mesmo tipo.  
  
|Menu de atalho|Descrição|  
|-------------------|-----------------|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>|Aplica-se quando o nó do projeto está selecionado.|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_ITEMNODE>|Aplica-se quando um arquivo é selecionado.|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_FOLDERNODE>|Aplica-se quando uma pasta está selecionada.|  
|IDM_VS_CTXT_WEBREFFOLDER|Aplica-se quando a pasta de referência da Web está selecionada.|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCEROOT>|Aplica-se quando o nó raiz de referências chamado "Referências" está selecionado.|  
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCE>|Aplica-se quando nós de referência são selecionados; Isso inclui assembly, COM e somente as referências do projeto. Não inclui referências da Web.|  
  
 A tabela a seguir mostra os menus de atalho que se aplicam quando a seleção no **Solution Explorer** abrange várias hierarquias  
  
|Menu de atalho|Descrição|  
|-------------------|-----------------|  
|IDM_VS_CTXT_XPROJ_SLNPROJ|Aplica-se quando a seleção atual contém o nó da solução e nós do projeto raiz.|  
|IDM_VS_CTXT_XPROJ_SLNITEM|Aplica-se quando a seleção atual contém os itens de projeto e o nó de solução.|  
|IDM_VS_CTXT_XPROJ_MULTIPROJ|Aplica-se quando a seleção atual consiste em vários projetos nós raiz apenas.|  
|IDM_VS_CTXT_XPROJ_PROJITEM|Aplica-se quando a seleção atual contiver uma mistura de nós de raiz do projeto e itens de projeto. Além disso, a seleção pode conter o nó da solução.|  
|IDM_VS_CTXT_XPROJ_MULTIITEM|Aplica-se quando a seleção atual contém itens de projeto de vários projetos na solução, ou itens de tipos diferentes são selecionados no mesmo projeto.|  
  
## <a name="command-groups"></a>Grupos de comando  
 A tabela a seguir mostra os grupos de comando que você pode usar ao estender projetos e que você pode acessar por meio de <xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE> menu de atalho.  
  
|Grupo de comandos|Descrição|  
|-------------------|-----------------|  
|IDG_VS_CTXT_PROJECT_BUILD|Comandos para criar, recriar e implantar o projeto.|  
|IDG_VS_CTXT_COMPILELINK|Comandos para compilar e vincular o projeto.|  
|IDG_VS_CTXT_PROJECT_CONFIG|Comandos que definir a configuração de projeto e ordem de compilação.|  
|IDG_VS_CTXT_PROJECT_ADD|Comandos que adicionar itens ao projeto.|  
|IDG_VS_CTXT_PROJECT_START|Comandos que definem o projeto de inicialização associado com a tecla F5.|  
|IDG_VS_CTXT_PROJECT_SAVE|Comandos para salvar itens de projeto.|  
|IDG_VS_CTXT_PROJECT_DEBUG|Comandos de depuração.|  
|IDG_VS_CTXT_PROJECT_SCC|Comandos de controle de origem.|  
|IDG_VS_CTXT_PROJECT_TRANSFER|Comandos para recortar, copiar e colar operações.|  
|IDG_VS_CTXT_PROJECT_PROPERTIES|Comandos que fornecem acesso ao **propriedades do projeto** caixa de diálogo.|  
  
## <a name="see-also"></a>Consulte também  
 [Como VSPackages adicionar elementos da Interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [MenuCommands Vs. OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md)   
 [Criar grupos reutilizáveis de botões](../../extensibility/creating-reusable-groups-of-buttons.md)