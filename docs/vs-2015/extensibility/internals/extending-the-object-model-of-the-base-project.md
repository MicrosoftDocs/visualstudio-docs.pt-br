---
title: Estendendo o modelo de objeto do projeto Base | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- automation object model, extending
- project subtypes, extending automation object model
- automation object model
ms.assetid: 2f95cc53-dff6-476c-bacd-500fb0ff7725
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7723881bce81824b66a936793175077a0ec67666
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "68187161"
---
# <a name="extending-the-object-model-of-the-base-project"></a>Estendendo o modelo de objeto do projeto base
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Um subtipo de projeto pode estender o modelo de objeto de automação do projeto base nos seguintes locais:  
  
- Project.Extender ("\<ProjectSubtypeName >") – isso permite que um subtipo de projeto oferece um objeto com métodos personalizados do <xref:EnvDTE.Project>. Um subtipo de projeto pode usar extensores de automação para expor o `Project` objeto. O <xref:EnvDTE80.IInternalExtenderProvider>interface implementada do agregador de subtipo de projeto principal deve oferecer seu objeto para o `VSHPROPID_ExtObjectCATID` de <xref:Microsoft.VisualStudio.Shell.Interop.__VSSPROPID2> (correspondente a um `itemid` valor de VSITEMID_ROOT, de `VSITEMID`) CATID.  
  
- ProjectItem.Extender ("\<ProjectSubtypeName >") – isso permite que um subtipo de projeto oferece um objeto com métodos personalizados de um determinado <xref:EnvDTE.ProjectItem> objeto dentro do projeto. Um subtipo de projeto pode usar extensores de automação para expor esse objeto. O <xref:EnvDTE80.IInternalExtenderProvider> interface implementada do agregador de subtipo de projeto principal precisa oferecer seu objeto para o `VSHPROPID_ExtObjectCATID` de <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> (correspondente a um desejado `VSITEMID`) CATID.  
  
- Properties – essa coleção expõe as propriedades de configuração independente do `Project` objeto. Para obter mais informações sobre as propriedades do projeto, consulte <xref:EnvDTE.Project.Properties%2A>. Um subtipo de projeto pode usar extensores de automação para adicionar suas propriedades para esta coleção. O <xref:EnvDTE80.IInternalExtenderProvider> interface implementada do agregador de subtipo de projeto principal precisa oferecer seu objeto para o `VSHPROPID_BrowseObjectCATID` de VSHPROPID2 (correspondente a um `itemid` valor de VSITEMID_ROOT, de <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2>) CATID.  
  
- Configuration.Properties – esta coleção expõe as propriedades dependentes de configuração do projeto para uma configuração específica (por exemplo, Debug). Para obter mais informações, consulte <xref:EnvDTE.Configuration>. Um subtipo de projeto pode usar extensores de automação para adicionar suas propriedades para esta coleção. O <xref:EnvDTE80.IInternalExtenderProvider> interface implementada do agregador de subtipo de projeto principal oferece seu objeto para o CATID `VSHPROPID_CfgBrowseObjectCATID` (correspondente a um `itemid` valor de <xref:Microsoft.VisualStudio.VSConstants.VSITEMID>). O <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>interface é usada para diferenciar um objeto de configuração de navegação do outro.  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSFPROPID>
