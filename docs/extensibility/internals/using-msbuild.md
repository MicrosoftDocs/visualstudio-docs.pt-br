---
title: Usando o MSBuild | Microsoft Docs
description: O MSBuild fornece um formato XML extensível para a criação de arquivos de projeto que descrevem totalmente os itens de projeto a serem criados, as tarefas de compilação e as configurações de compilação.
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, compiling with MSBuild
- MSBuild, extensibility
- packages, compiling with MSBuild
ms.assetid: 9d38c388-1f64-430e-8f6c-e88bc99a4260
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8891d9674a952f0272855c8b9203109ad2e22468
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105090688"
---
# <a name="using-msbuild"></a>Usando o MSBuild
O MSBuild fornece um formato XML extensível e bem definido para a criação de arquivos de projeto que descrevem totalmente os itens de projeto a serem criados, as tarefas de compilação e as configurações de compilação.

## <a name="general-msbuild-considerations"></a>Considerações gerais do MSBuild
 Arquivos de projeto MSBuild, por exemplo, [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] arquivos. csproj e [!INCLUDE[vbprvb](../../code-quality/includes/vbprvb_md.md)] . vbproj, contêm dados que são usados no momento da compilação, mas também podem conter dados que são usados em tempo de design. Os dados de tempo de compilação são armazenados usando primitivos do MSBuild, incluindo o [elemento de item (MSBuild)](../../msbuild/item-element-msbuild.md) e o [elemento de propriedade (MSBuild)](../../msbuild/property-element-msbuild.md). Os dados de tempo de design, que são dados específicos para o tipo de projeto e todos os subtipos de projeto relacionados, são armazenados em XML de forma livre reservado para ele.

 O MSBuild não tem suporte nativo para objetos de configuração, mas fornece atributos condicionais para especificar dados específicos da configuração. Por exemplo:

```xml
<OutputDir Condition="'$(Configuration)'=="release'">Bin\MyReleaseConfig</OutputDir>
```

 Para obter mais informações sobre atributos condicionais, consulte [constructos condicionais](../../msbuild/msbuild-conditional-constructs.md).

### <a name="extending-msbuild-for-your-project-type"></a>Estendendo o MSBuild para o tipo de projeto
 As interfaces e APIs do MSBuild estão sujeitas a alterações em versões futuras do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] . Portanto, é prudente usar as classes do MPF (estrutura de pacote gerenciada) porque elas fornecem a blindagem de alterações.

 A estrutura de pacote gerenciada para projetos (MPFProj) fornece classes auxiliares para criar e gerenciar o novo sistema de projeto. Você pode encontrar o código-fonte e as instruções de compilação em [MPF for projects-Visual Studio 2013](https://github.com/tunnelvisionlabs/MPFProj10).

 As classes do MPF específicas do projeto são as seguintes:

|Classe|Implementação|
|-----------|--------------------|
|`Microsoft.VisualStudio.Package.ProjectNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgProvider2><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistFileFormat><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents>|
|`Microsoft.VisualStudio.Package.ProjectFactory`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>|
|`Microsoft.VisualStudio.Package.HierarchyNode`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>|
|`Microsoft.VisualStudio.Package.ProjectConfig`|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg><br /><br /> <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>|
|`Microsoft.VisualStudio.Package.SettingsPage`|<xref:Microsoft.VisualStudio.OLE.Interop.IPropertyPageSite>|

 `Microsoft.VisualStudio.Package.ProjectElement` a classe é um wrapper para itens do MSBuild.

#### <a name="single-file-generators-vs-msbuild-tasks"></a>Geradores de arquivo único versus tarefas do MSBuild
 Os geradores de arquivo único são acessíveis em tempo de design apenas, mas as tarefas do MSBuild podem ser usadas em tempo de design e em tempo de compilação. Para obter máxima flexibilidade, portanto, use tarefas do MSBuild para transformar e gerar código. Para obter mais informações, consulte [ferramentas personalizadas](../../extensibility/internals/custom-tools.md).

## <a name="see-also"></a>Confira também
- [Referência do MSBuild](../../msbuild/msbuild-reference.md)
- [MSBuild](../../msbuild/msbuild.md)
- [Ferramentas personalizadas](../../extensibility/internals/custom-tools.md)
