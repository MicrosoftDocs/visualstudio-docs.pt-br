---
title: IDE-Defined comandos para estender os sistemas de projeto | Microsoft Docs
description: Saiba mais sobre os comandos e grupos de comandos definidos no IDE (ambiente de desenvolvimento integrado) do Visual Studio que são usados para estender sistemas de projetos.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, project systems
- project systems, environment-defined commands
ms.assetid: 0e33b8e9-16fa-4400-a941-e92d56120e7e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6fedca7081c531fef257e20e64426f8b35e88e87
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085995"
---
# <a name="ide-defined-commands-for-extending-project-systems"></a>Comandos definidos pelo IDE para estender sistemas de projeto
Quando você deseja estender sistemas de projeto, você pode usar comandos e grupos de comandos fornecidos pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE.

 As seções a seguir listam os itens de comando que são especialmente úteis para estender sistemas de projeto.

## <a name="command-menus"></a>Menus de comando
 A tabela a seguir mostra os menus de comando que são locais úteis para que você coloque comandos de alto nível que invocam um extensor de projeto.

|Menu de comando|Descrição|
|------------------|-----------------|
|IDM_VS_MENU_PROJECT|O menu de nível superior do **projeto** .|
|IDM_VS_TOOL_PROJWIN|A barra de ferramentas **Gerenciador de soluções** .|

## <a name="shortcut-menus"></a>Menus de atalho
 A tabela a seguir mostra os menus de atalho que se aplicam quando um único nó é selecionado na **Gerenciador de soluções**, ou quando há várias seleções homogêneas no **Gerenciador de soluções**, que é quando todos os nós selecionados são do mesmo tipo.

|Menu de atalho|Descrição|
|-------------------|-----------------|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE>|Aplica-se quando o nó do projeto é selecionado.|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_ITEMNODE>|Aplica-se quando um arquivo é selecionado.|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_FOLDERNODE>|Aplica-se quando uma pasta é selecionada.|
|IDM_VS_CTXT_WEBREFFOLDER|Aplica-se quando a pasta de referência Web é selecionada.|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCEROOT>|Aplica-se quando o nó raiz de referências chamado "referências" é selecionado.|
|<xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_REFERENCE>|Aplica-se quando nós de referência são selecionados; Isso inclui somente referências de assembly, COM e projeto. Não inclui referências Web.|

 A tabela a seguir mostra os menus de atalho que se aplicam quando a seleção no **Gerenciador de soluções** abrange várias hierarquias,

|Menu de atalho|Descrição|
|-------------------|-----------------|
|IDM_VS_CTXT_XPROJ_SLNPROJ|Aplica-se quando a seleção atual contém o nó da solução e os nós do projeto raiz.|
|IDM_VS_CTXT_XPROJ_SLNITEM|Aplica-se quando a seleção atual contém o nó da solução e os itens do projeto.|
|IDM_VS_CTXT_XPROJ_MULTIPROJ|Aplica-se quando a seleção atual consiste somente em vários nós de projeto raiz.|
|IDM_VS_CTXT_XPROJ_PROJITEM|Aplica-se quando a seleção atual contém uma combinação de nós de projeto raiz e itens de projeto. Além disso, a seleção pode conter o nó da solução.|
|IDM_VS_CTXT_XPROJ_MULTIITEM|Aplica-se quando a seleção atual contém itens de projeto de vários projetos na solução ou quando itens de tipos diferentes são selecionados no mesmo projeto.|

## <a name="command-groups"></a>Grupos de comandos
 A tabela a seguir mostra os grupos de comandos que você pode usar ao estender projetos e que você pode acessar por meio do <xref:Microsoft.VisualStudio.Shell.VsMenus.IDM_VS_CTXT_PROJNODE> menu de atalho.

|Grupo de comandos|Descrição|
|-------------------|-----------------|
|IDG_VS_CTXT_PROJECT_BUILD|Comandos para compilar, recompilar e implantar o projeto.|
|IDG_VS_CTXT_COMPILELINK|Comandos para compilar e vincular o projeto.|
|IDG_VS_CTXT_PROJECT_CONFIG|Comandos que definem a ordem de compilação e a configuração do projeto.|
|IDG_VS_CTXT_PROJECT_ADD|Comandos que adicionam itens ao projeto.|
|IDG_VS_CTXT_PROJECT_START|Comandos que definem o projeto de inicialização associado à tecla F5.|
|IDG_VS_CTXT_PROJECT_SAVE|Comandos para salvar itens de projeto.|
|IDG_VS_CTXT_PROJECT_DEBUG|Comandos para depuração.|
|IDG_VS_CTXT_PROJECT_SCC|Comandos para controle do código-fonte.|
|IDG_VS_CTXT_PROJECT_TRANSFER|Comandos para operações de recortar, copiar e colar.|
|IDG_VS_CTXT_PROJECT_PROPERTIES|Comandos que fornecem acesso à caixa de diálogo **Propriedades do projeto** .|

## <a name="see-also"></a>Confira também

- [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Criar grupos reutilizáveis de botões](../../extensibility/creating-reusable-groups-of-buttons.md)
