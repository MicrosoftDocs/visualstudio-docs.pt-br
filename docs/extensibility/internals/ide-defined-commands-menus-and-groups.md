---
title: Comandos, menus e grupos definidos pelo IDE | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, environment-defined
- .vsct files, environment-defined constants
- command groups, environment-defined
ms.assetid: 86b3af13-7163-48c6-986b-7beeedbc26cc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6557f49b019a6793698dabe852919ec2e9f28cfd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80707723"
---
# <a name="ide-defined-commands-menus-and-groups"></a>Grupos, menus e comandos definidos pelo IDE
Muitos menus, comandos e grupos de comandos já estão definidos para uso pelo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] IDE. Esses comandos também estão disponíveis para seu uso quando você estende [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] .

## <a name="finding-environment-defined-commands"></a>Localizando comandos definidos pelo ambiente
 Os comandos de ambiente são definidos em um conjunto de quatro arquivos. vsct:

- SharedCmdDef. vsct

- SharedCmdPlace. vsct

- ShellCmdDef. vsct

- ShellCmdPlace. vsct

  Esses arquivos estão localizados em *\<Visual Studio SDK installation path>* \VisualStudioIntegration\Common\Inc \\ . Esses arquivos fornecem as definições e os GUIDs dos menus e grupos que você pode usar no arquivo de configuração de tabela de comando (. vsct) do seu VSPackage como contêineres para seus próprios menus, grupos e comandos.

## <a name="in-this-section"></a>Nesta seção
- [GUIDs e IDs de menus do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-menus.md)

 Fornece os valores de GUID e ID de menus na barra de menus do Visual Studio e dos grupos que eles contêm.

- [GUIDs e IDs de barras de ferramentas do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-toolbars.md)

 Fornece os valores de GUID e ID de barras de ferramentas no IDE do Visual Studio e dos grupos que eles contêm.

- [GUIDs e IDs de comandos do Visual Studio](../../extensibility/internals/guids-and-ids-of-visual-studio-commands.md)

 Fornece os valores de GUID e ID de comandos definidos pelo IDE do Visual Studio.

## <a name="see-also"></a>Confira também
- [Arquivos .Vsct (Visual Studio Command Table)](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [Comandos definidos pelo IDE para estender sistemas de projeto](../../extensibility/internals/ide-defined-commands-for-extending-project-systems.md)
- [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
