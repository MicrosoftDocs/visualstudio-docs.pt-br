---
title: Pacote do Framework Classes gerenciadas | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- devlang-csharp
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- managed package framework, helper classes
- managed package helper classes
- Visual Studio SDK, managed package helper classes
- classes [Visual Studio SDK], managed package framework
ms.assetid: 15aedcc3-c79a-460b-b620-43223f1ae81e
caps.latest.revision: 24
manager: douge
ms.openlocfilehash: 931e73af72d2239ec04ac248b9fa426fe24f249a
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49188988"
---
# <a name="managed-package-framework-classes"></a>Pacote do Framework Classes gerenciadas
As classes do framework (MPF) de pacote gerenciado podem ser usadas para criar os VSPackages usando código gerenciado. Elas fornecem implementações padrão de várias interfaces de VSPackage. Ocultando as complexidades e detalhes de implementação MPF permite que você crie [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] produtos de integração com uma quantidade mínima de código.  
  
> [!WARNING]
>  A maioria dos assemblies que contêm classes de estrutura de pacote gerenciado é fornecida com o SDK do Visual Studio. Você pode baixar o código-fonte para o Managed empacotado Framework para projetos em [estrutura de pacote gerenciado para projetos](http://mpfproj11.codeplex.com/).  
  
## <a name="mpf-namespaces"></a>Namespaces MPF  
 A tabela a seguir lista os namespaces MPF fornecidos pelo [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)].  
  
|Espaço para nome|Conteúdo|  
|----------------|--------------|  
|<xref:Microsoft.VisualStudio>|Contém classes úteis para tratamento de erros COM, [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] windows Win32 e constantes.|  
|<xref:Microsoft.VisualStudio.Package>|Inclui os invólucros de código gerenciado para [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] projetos, editores e MSBuild.|  
|<xref:Microsoft.VisualStudio.Shell>|Inclui classes de base MPF dos quais você pode derivar uma implementação de muitos objetos comuns do Visual Studio.|  
|<xref:Microsoft.VisualStudio.Shell.Design>|Contém [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensões do designer.|  
|<xref:Microsoft.VisualStudio.Shell.Design.Serialization>|Contém [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensões do designer de serialização.|  
|<xref:Microsoft.VisualStudio.Shell.Design.Serialization.CodeDom>|Contém [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] extensões do designer de CodeDom.|  
|<xref:Microsoft.VisualStudio.Shell.Flavor>|Dá suporte a projeto subtipos (também conhecido como "tipos").|  
  
## <a name="see-also"></a>Consulte também  
 [Os VSPackages e a estrutura de pacote gerenciado](../misc/vspackages-and-the-managed-package-framework.md)   
 [Usar Assemblies de interoperabilidade do Visual Studio](../extensibility/internals/using-visual-studio-interop-assemblies.md)   
 [Os VSPackages e a estrutura de pacote gerenciado](../misc/vspackages-and-the-managed-package-framework.md)