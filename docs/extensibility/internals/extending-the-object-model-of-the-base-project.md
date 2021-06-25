---
title: Estendendo o modelo de objeto do projeto base | Microsoft Docs
description: Saiba como estender o modelo de objeto de automação do projeto base Visual Studio usando um subtipo de projeto.
ms.custom: SEO-VS-2020
ms.date: 03/22/2018
ms.topic: reference
helpviewer_keywords:
- automation object model, extending
- project subtypes, extending automation object model
- automation object model
ms.assetid: 2f95cc53-dff6-476c-bacd-500fb0ff7725
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 175571b374c6a54999b212b316301f3f775891ff
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899336"
---
# <a name="extend-the-object-model-of-the-base-project"></a>Estender o modelo de objeto do projeto base

Um subtipo de projeto pode estender o modelo de objeto de automação do projeto base nos seguintes locais:

- Project.Extender(" "): isso permite que um subtipo de projeto ofereça um objeto com métodos \<ProjectSubtypeName> personalizados do <xref:EnvDTE.Project> objeto . Um subtipo de projeto pode usar os Extenders de Automação para expor o `Project` objeto. A interface implementada no agregador de subtipo de projeto principal deve oferecer seu objeto para o de (correspondente a um <xref:EnvDTE80.IInternalExtenderProvider> valor `VSHPROPID_ExtObjectCATID` de <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> `itemid` [VSITEMID. Raiz](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID.

- ProjectItem.Extender(" "): isso permite que um subtipo de projeto ofereça um objeto com métodos personalizados de um \<ProjectSubtypeName> objeto específico dentro do <xref:EnvDTE.ProjectItem> projeto. Um subtipo de projeto pode usar os estendedores de automação para expor esse objeto. A interface implementada no agregador de subtipo de projeto principal precisa oferecer seu objeto para o <xref:EnvDTE80.IInternalExtenderProvider> `VSHPROPID_ExtObjectCATID` de <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> (correspondente a um ) <xref:Microsoft.VisualStudio.VSConstants.VSITEMID> CATID desejado.

- Project.Properties: essa coleção expõe as propriedades independentes de configuração do `Project` objeto. Para obter mais informações sobre `Project` propriedades, consulte <xref:EnvDTE.Project.Properties%2A> . Um subtipo de projeto pode usar os Extenders de Automação para adicionar suas propriedades a essa coleção. A interface implementada no agregador de subtipo de projeto principal precisa oferecer seu objeto para o de (correspondente a um valor <xref:EnvDTE80.IInternalExtenderProvider> `VSHPROPID_BrowseObjectCATID` de <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> `itemid` [VSITEMID. Raiz](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)) CATID.

- Configuration.Properties: essa coleção expõe as propriedades dependentes de configuração do projeto para uma configuração específica (por exemplo, Depurar). Para obter mais informações, consulte <xref:EnvDTE.Configuration>. Um subtipo de projeto pode usar os Extenders de Automação para adicionar suas propriedades a essa coleção. A interface implementada no agregador de subtipo de projeto principal oferece seu objeto para <xref:EnvDTE80.IInternalExtenderProvider> CATID (correspondente a um `VSHPROPID_CfgBrowseObjectCATID` valor de `itemid` [VSITEMID. Raiz](<xref:Microsoft.VisualStudio.VSConstants.VSITEMID.Root>)). A <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject> interface é usada para distinguir um objeto de navegação de configuração de outro.

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
