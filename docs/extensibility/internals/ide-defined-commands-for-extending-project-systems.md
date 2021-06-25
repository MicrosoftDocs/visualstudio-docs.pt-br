---
title: IDE-Defined comandos para estender sistemas de projeto | Microsoft Docs
description: Saiba mais sobre os comandos e grupos de comandos definidos no Visual Studio IDE (ambiente de desenvolvimento integrado) que são usados para estender sistemas de projeto.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- commands, project systems
- project systems, environment-defined commands
ms.assetid: 0e33b8e9-16fa-4400-a941-e92d56120e7e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 4525802bf308d740ea5c468fac171e74bff2b34e
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112901156"
---
# <a name="ide-defined-commands-for-extending-project-systems"></a>Comandos definidos pelo IDE para estender sistemas de projeto
Quando você deseja estender sistemas de projeto, pode usar comandos e grupos de comandos fornecidos pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.

 As seções a seguir listam itens de comando que são especialmente úteis para estender sistemas de projeto.

## <a name="command-menus"></a>Menus de comando
 A tabela a seguir mostra os menus de comando que são locais úteis para você colocar comandos de alto nível que invocam um extensor de projeto.

|Menu De comando|Descrição|
|------------------|-----------------|
|IDM_VS_MENU_PROJECT|O menu **De** nível superior do projeto.|
|IDM_VS_TOOL_PROJWIN|A **barra Gerenciador de Soluções** de ferramentas.|

## <a name="shortcut-menus"></a>Menus de atalho
 A tabela a seguir mostra os menus de atalho que se aplicam quando um único nó é selecionado no **Gerenciador de Soluções** ou quando há várias seleções homogêneas no **Gerenciador de Soluções**, que é quando todos os nós selecionados são do mesmo tipo.

|Menu de atalho|Descrição|
|-------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>|Aplica-se quando o nó do projeto é selecionado.|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_ITEMNODE>|Aplica-se quando um arquivo é selecionado.|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_FOLDERNODE>|Aplica-se quando uma pasta é selecionada.|
|IDM_VS_CTXT_WEBREFFOLDER|Aplica-se quando a pasta Referência da Web é selecionada.|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCEROOT>|Aplica-se quando o nó raiz de referência chamado "Referências" é selecionado.|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCE>|Aplica-se quando os nós de referência são selecionados; elas incluem apenas referências de assembly, COM e projeto. Não inclui referências da Web.|

 A tabela a seguir mostra os menus de atalho que se aplicam quando a seleção no **Gerenciador de Soluções** abrange várias hierarquias,

|Menu de atalho|Descrição|
|-------------------|-----------------|
|IDM_VS_CTXT_XPROJ_SLNPROJ|Aplica-se quando a seleção atual contém o nó da solução e os nós de projeto raiz.|
|IDM_VS_CTXT_XPROJ_SLNITEM|Aplica-se quando a seleção atual contém o nó da solução e os itens de projeto.|
|IDM_VS_CTXT_XPROJ_MULTIPROJ|Aplica-se quando a seleção atual consiste apenas em vários nós de projeto raiz.|
|IDM_VS_CTXT_XPROJ_PROJITEM|Aplica-se quando a seleção atual contém uma combinação de nós de projeto raiz e itens de projeto. Além disso, a seleção pode conter o nó da solução.|
|IDM_VS_CTXT_XPROJ_MULTIITEM|Aplica-se quando a seleção atual contém itens de projeto de vários projetos na solução ou quando itens de tipos diferentes são selecionados no mesmo projeto.|

## <a name="command-groups"></a>Grupos de comandos
 A tabela a seguir mostra os grupos de comandos que você pode usar ao estender projetos e que você pode acessar por meio do <xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE> menu de atalho.

|Grupo de comandos|Descrição|
|-------------------|-----------------|
|IDG_VS_CTXT_PROJECT_BUILD|Comandos para criar, recriar e implantar o projeto.|
|IDG_VS_CTXT_COMPILELINK|Comandos para compilar e vincular o projeto.|
|IDG_VS_CTXT_PROJECT_CONFIG|Comandos que configuram o projeto e a ordem de build.|
|IDG_VS_CTXT_PROJECT_ADD|Comandos que adicionam itens ao projeto.|
|IDG_VS_CTXT_PROJECT_START|Comandos que configuram o projeto de inicialização associado à chave F5.|
|IDG_VS_CTXT_PROJECT_SAVE|Comandos para salvar itens de projeto.|
|IDG_VS_CTXT_PROJECT_DEBUG|Comandos para depuração.|
|IDG_VS_CTXT_PROJECT_SCC|Comandos para controle do código-fonte.|
|IDG_VS_CTXT_PROJECT_TRANSFER|Comandos para operações de recortar, copiar e colar.|
|IDG_VS_CTXT_PROJECT_PROPERTIES|Comandos que fornecem acesso à caixa **de diálogo Propriedades do** Projeto .|

## <a name="see-also"></a>Confira também

- [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Criar grupos reutilizáveis de botões](../../extensibility/creating-reusable-groups-of-buttons.md)
