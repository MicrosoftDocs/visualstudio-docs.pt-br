---
title: Subtipos de projeto | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- projects [Visual Studio SDK], subtypes
- project subtypes [Visual Studio SDK]
ms.assetid: d235b47b-cf11-4d47-a63f-e33d9d16105d
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 9fdbc00863c7aa0d03ad94bd60966e81f7faaf81
ms.sourcegitcommit: 37fb7075b0a65d2add3b137a5230767aa3266c74
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2019
ms.locfileid: "53853445"
---
# <a name="project-subtypes"></a>Subtipos de projeto
Subtipos do projeto permitem que você personalize ou flavor o comportamento dos sistemas de projeto [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]. As personalizações incluem salvando dados adicionais no arquivo de projeto, adicionando ou filtrando itens na **Adicionar Novo Item** caixa de diálogo, controlando como os assemblies são depurados e implantados e estendendo o projeto **propriedade Páginas** caixa de diálogo. Os VSPackages implementar subtipos de projeto usando a agregação COM.  
  
> [!NOTE]
>  O sistema de projeto do Visual C++ não oferece suporte para os subtipos de projeto. [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] em si usa subtipos do projeto para implementar projetos de dispositivo inteligente e do SQL Server.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Design de subtipos de projeto](../../extensibility/internals/project-subtypes-design.md)  
 Descreve o conceito de subtipos de projeto.  
  
 [Sequência de inicialização dos subtipos do projeto](../../extensibility/internals/initialization-sequence-of-project-subtypes.md)  
 Descreve a sequência de inicialização do subtipo de projeto através de programação por [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente.  
  
 [Propriedades e métodos estendidos por subtipos do projeto](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)  
 Fornece descrições detalhadas dos recursos e métodos estendidos com mais frequência usando subtipos do projeto.  
  
 [Persistir os dados no arquivo de projeto do MSBuild](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md)  
 Descreve como manter os dados em um arquivo de projeto e como usar <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> para manter os dados no arquivo de projeto entre os níveis de agregação de subtipo de projeto.  
  
 [Interface de usuário de propriedades do projeto](../../extensibility/internals/project-property-user-interface.md)  
 Descreve como os subtipos de projeto podem modificar o projeto **páginas de propriedade** caixa de diálogo.  
  
 [Estender o modelo de objeto do projeto base](../../extensibility/internals/extending-the-object-model-of-the-base-project.md)  
 Fornece informações sobre como os subtipos de projeto podem usar extensores de automação para estender o modelo de objeto de automação.  
  
 [Contribuir com a caixa de diálogo Adicionar Novo Item](../../extensibility/internals/contributing-to-the-add-new-item-dialog-box.md)  
 Descreve como adicionar itens para o **Adicionar Novo Item** caixa de diálogo.  
  
 [Salvar dados em arquivos de projeto](../../extensibility/saving-data-in-project-files.md)  
 Explica como um subtipo de projeto pode salvar e recuperar dados específicos subtipo-no arquivo de projeto usando o Framework de pacote gerenciado (MPF).  
  
 [Manipulação da implantação especializada](../../extensibility/internals/handling-specialized-deployment.md)  
 Explica como subtipos do projeto podem fornecer o comportamento de implantação especializada, Implementando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> interface.  
  
 [Adicionar e remover páginas de propriedade](../../extensibility/adding-and-removing-property-pages.md)  
 Descreve a adição e remoção de páginas de propriedades no Designer de projeto.  
  
## <a name="related-sections"></a>Seções relacionadas  
 [Tipos de projeto](../../extensibility/internals/project-types.md)  
 Fornece links para tópicos que detalha [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] projetos.