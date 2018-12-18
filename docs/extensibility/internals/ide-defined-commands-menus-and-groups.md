---
title: Comandos definidos pelo IDE, Menus e grupos | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, environment-defined
- .vsct files, environment-defined constants
- command groups, environment-defined
ms.assetid: 86b3af13-7163-48c6-986b-7beeedbc26cc
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 34c41608a90b15538e190be093ed2791a90824f9
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49857270"
---
# <a name="ide-defined-commands-menus-and-groups"></a>Grupos, menus e comandos definidos pelo IDE
Muitos menus, comandos e grupos de comando já estão definidos para uso pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE. Esses comandos também estão disponíveis para uso quando você estende [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)].  
  
## <a name="finding-environment-defined-commands"></a>Encontrando comandos definidos pelo ambiente  
 Os comandos de ambiente são definidos em um conjunto de quatro arquivos. VSCT:  
  
- SharedCmdDef.vsct  
  
- SharedCmdPlace.vsct  
  
- ShellCmdDef.vsct  
  
- ShellCmdPlace.vsct  
  
  Esses arquivos estão localizados no  *\<caminho de instalação do SDK do Visual Studio >* \visualstudiointegration\common\inc\\. Esses arquivos fornecem as definições e os GUIDs dos menus e grupos que você pode usar no arquivo de configuração (. VSCT) de tabela de comando de seu VSPackage como contêineres para seus próprios menus, grupos e comandos.  
  
## <a name="in-this-section"></a>Nesta seção  
 [GUIDs e IDs de menus do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)  
 Fornece os valores GUID e ID de menus na barra de menus do Visual Studio e dos grupos que eles contêm.  
  
 [GUIDs e IDs de barras de ferramentas do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)  
 Fornece os valores GUID e ID das barras de ferramentas no IDE do Visual Studio e dos grupos que eles contêm.  
  
 [GUIDs e IDs de comandos do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)  
 Fornece os valores GUID e ID de comandos definidos pelo IDE do Visual Studio.  
  
## <a name="see-also"></a>Consulte também  
 [Tabela de comando do Visual Studio (. Arquivos de VSCT)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [Comandos definidos pelo IDE para estender sistemas de projeto](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)   
 [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)