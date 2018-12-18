---
title: Usando o MSBuild | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- VSPackages, compiling with MSBuild
- MSBuild, extensibility
- packages, compiling with MSBuild
ms.assetid: 9d38c388-1f64-430e-8f6c-e88bc99a4260
caps.latest.revision: 21
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: dba9feb50ddab868d81eb61565c34a8c694c2a69
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51768181"
---
# <a name="using-msbuild"></a>Usando o MSBuild
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

MSBuild fornece um formato XML bem definido e extensível para a criação de arquivos de projeto que descrevem totalmente os itens de projeto para ser compilado, as tarefas de compilação e configurações de build.  
  
 Para um exemplo de ponta a ponta de um sistema de projeto de linguagem baseado no MSBuild, consulte o exemplo de IronPython Deep Dive na[exemplos de VSSDK](../../misc/vssdk-samples.md).  
  
## <a name="general-msbuild-considerations"></a>Considerações gerais MSBuild  
 Arquivos de projeto MSBuild, por exemplo, [!INCLUDE[csprcs](../../includes/csprcs-md.md)] . csproj e [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] arquivos. vbproj, contêm dados que são usados no momento da compilação, mas também podem conter dados que são usados em tempo de design. Dados de tempo de compilação são armazenados usando o MSBuild primitivos, incluindo [elemento Item (MSBuild)](../../msbuild/item-element-msbuild.md) e [elemento Property (MSBuild)](../../msbuild/property-element-msbuild.md). Dados de tempo de design, que são específico para o tipo de projeto e quaisquer subtipos do projeto relacionado a dados, são armazenados no XML de forma livre, reservada para ela.  
  
 MSBuild não tem suporte nativo para objetos de configuração, mas fornecer atributos condicionais para especificar dados de configuração específicos. Por exemplo:  
  
```  
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>  
```  
  
 Para obter mais informações sobre atributos condicionais, consulte [constructos condicionais](../../msbuild/msbuild-conditional-constructs.md).  
  
### <a name="extending-msbuild-for-your-project-type"></a>Estendendo o MSBuild para o tipo de projeto  
 APIs e interfaces do MSBuild estão sujeitos a alterações em versões futuras do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Portanto, é aconselhável usar as classes de estrutura (MPF) de pacote gerenciado porque eles fornecem a blindagem de alterações.  
  
 A estrutura de pacote gerenciado para projetos (MPFProj) fornece classes auxiliares para criar e gerenciar o novo sistema de projeto. Você pode encontrar a fonte de instruções de código e compilação em [MPF de projetos – Visual Studio 2013](http://mpfproj12.codeplex.com/).  
  
 As classes MPF de específicos do projeto são da seguinte maneira:  
  
|Classe|Implementação|  
|-----------|--------------------|  
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|  
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|  
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|  
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|  
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|  
  
 `Microsoft.VisualStudio.Package.ProjectElement` classe é um wrapper para itens do MSBuild.  
  
#### <a name="single-file-generators-vs-msbuild-tasks"></a>Geradores de arquivo único vs. Tarefas do MSBuild  
 Arquivo único geradores são acessíveis em tempo de design somente, mas as tarefas do MSBuild podem ser usadas no tempo de design e tempo de compilação. Para máxima flexibilidade, portanto, use tarefas do MSBuild para transformar e gerar código. Para obter mais informações, consulte [ferramentas personalizados](../../extensibility/internals/custom-tools.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência do MSBuild](../../msbuild/msbuild-reference.md)   
 [MSBuild](http://msdn.microsoft.com/en-us/7c49aba1-ee6c-47d8-9de1-6f29a906e20b)   
 [Ferramentas personalizadas](../../extensibility/internals/custom-tools.md)

