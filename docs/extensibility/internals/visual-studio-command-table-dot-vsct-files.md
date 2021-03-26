---
title: Tabela de comandos do Visual Studio (. Arquivos de vsct) | Microsoft Docs
description: Saiba mais sobre os arquivos de configuração de tabela de comando, que são arquivos de texto que descrevem o conjunto de comandos que um VSPackage contém.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT files, overview
- Visual Studio command table configuration files (VSCT), overview
ms.assetid: 1313adb4-add4-4e74-90e2-f4be522f5259
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 305bf0e5463fd4e030f2ce3e9f7fa6eca99bfe20
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085735"
---
# <a name="visual-studio-command-table-vsct-files"></a>Arquivos .Vsct (Visual Studio Command Table)
Um arquivo de configuração de tabela de comando é um arquivo de texto que descreve o conjunto de comandos que um VSPackage contém. O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] compilador de tabela de comando (vsct) compila arquivos de configuração baseados em XML (arquivos. vsct) em arquivos binários de saída de tabela de comando (. CTO). Os arquivos. CTO resultantes são os mesmos que os que são criados usando o compilador de tabela de comando (CTC) para compilar arquivos de configuração. CTC. No entanto, os arquivos. vsct baseados em XML têm algumas vantagens, como um editor de XML e o XML IntelliSense.

 Para saber mais sobre a sintaxe e a semântica de arquivos. vsct, consulte [criando tabela de comandos XML (. Arquivos de vsct)](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

## <a name="in-this-section"></a>Nesta seção
 [Projetar arquivos da tabela de comandos XML (.Vsct)](../../extensibility/internals/designing-xml-command-table-dot-vsct-files.md)

 Descreve como projetar arquivos. vsct.

 [Como criar um arquivo .Vsct](../../extensibility/internals/how-to-create-a-dot-vsct-file.md)

 Compara os métodos para criar um arquivo. vsct. Descreve o processo para criar manualmente um novo arquivo. vsct.

## <a name="related-sections"></a>Seções relacionadas
 [Referência do esquema XML do VSCT](../../extensibility/vsct-xml-schema-reference.md)

 Fornece detalhes sobre cada seção do arquivo de configuração XML da tabela de comandos.

 [Configuração de tabela de comando (. CTC)](/previous-versions/bb165153(v=vs.100)) apresenta uma visão geral do formato de arquivo. CTC preterido.

 [Como os VSPackages adicionam elementos da interface do usuário](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)

 Descreve a especificação de formato de tabela de comando.

 [Recursos em VSPackages](../../extensibility/internals/resources-in-vspackages.md)

 Descreve como usar recursos gerenciados e não gerenciados em VSPackages gerenciados.

 [Comandos, menus e barras de ferramentas](../../extensibility/internals/commands-menus-and-toolbars.md)

 Explica como criar uma interface do usuário que inclui menus, barras de ferramentas e caixas de combinação de comandos.