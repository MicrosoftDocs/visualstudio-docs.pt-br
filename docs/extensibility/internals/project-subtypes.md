---
title: Subtipos de projeto | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], subtypes
- project subtypes [Visual Studio SDK]
ms.assetid: d235b47b-cf11-4d47-a63f-e33d9d16105d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 71dab4767c806b44cbd1f9638738b4a13d6b2bcb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2020
ms.locfileid: "80706407"
---
# <a name="project-subtypes"></a>Subtipos de projeto
Os subtipos de projeto permitem que você personalize ou represente o comportamento dos sistemas de projeto do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . As personalizações incluem salvar dados adicionais no arquivo de projeto, adicionar ou filtrar itens na caixa de diálogo **Adicionar novo item** , controlar como os assemblies são depurados e implantados e estender a caixa de diálogo **páginas de propriedades** do projeto. VSPackages implementar subtipos de projeto usando agregação COM.

> [!NOTE]
> O sistema de projeto Visual C++ não oferece suporte a subtipos de projeto. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Ele usa subtipos de projeto para implementar SQL Server e projetos de dispositivo inteligente.

## <a name="in-this-section"></a>Nesta seção
- [Design de subtipos de projeto](../../extensibility/internals/project-subtypes-design.md)

 Descreve o conceito de subtipos de projeto.

- [Sequência de inicialização de subtipos de projeto](../../extensibility/internals/initialization-sequence-of-project-subtypes.md)

 Descreve a sequência de inicialização de subtipo de projeto programático por [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente.

- [Propriedades e métodos estendidos por subtipos de projeto](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)

 Fornece descrições detalhadas dos recursos e métodos mais frequentemente estendidos usando subtipos de projeto.

- [Mantendo os dados no arquivo de projeto do MSBuild](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)

 Descreve como manter dados em um arquivo de projeto e como usar <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> o para manter os dados no arquivo de projeto nos níveis de agregação de subtipo de projeto.

- [Interface do usuário de propriedades do projeto](../../extensibility/internals/project-property-user-interface.md)

 Descreve como os subtipos de projeto podem modificar a caixa de diálogo **páginas de propriedades** do projeto.

- [Estendendo o modelo de objeto do projeto base](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)

 Fornece informações sobre como os subtipos de projeto podem usar extensores de automação para estender o modelo de objeto de automação.

- [Contribuindo com a caixa de diálogo Adicionar Novo Item](../../extensibility/internals/contributing-to-the-add-new-item-dialog-box.md)

 Descreve como adicionar itens à caixa de diálogo **Adicionar novo item** .

- [Salvar dados em arquivos de projeto](../../extensibility/saving-data-in-project-files.md)

 Explica como um subtipo de projeto pode salvar e recuperar dados específicos de subtipo no arquivo de projeto usando o MPF (estrutura de pacote gerenciada).

- [Manipulação de implantação especializada](../../extensibility/internals/handling-specialized-deployment.md)

 Explica como os subtipos de projeto podem fornecer um comportamento de implantação especializado implementando a <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> interface.

- [Adicionar e remover páginas de propriedade](../../extensibility/adding-and-removing-property-pages.md)

 Descreve como adicionar e remover páginas de propriedades no designer de projeto.

## <a name="related-sections"></a>Seções relacionadas
- [Tipos de Projeto](../../extensibility/internals/project-types.md)

 Fornece links para tópicos que detalham [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projetos.
