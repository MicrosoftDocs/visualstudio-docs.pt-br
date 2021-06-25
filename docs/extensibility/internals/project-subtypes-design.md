---
title: Design de subtipos de projeto | Microsoft Docs
description: Saiba como os subtipos de projeto permitem que o VSPackages estenda projetos com base no Microsoft Build Engine (MSBuild).
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- project subtypes, design
ms.assetid: 405488bb-1362-40ed-b0f1-04a57fc98c56
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c04c8e681646aed6816c645defe7ffd87ac7033c
ms.sourcegitcommit: bab002936a9a642e45af407d652345c113a9c467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2021
ms.locfileid: "112899687"
---
# <a name="project-subtypes-design"></a>Design de subtipos de projeto

Os subtipos de projeto permitem que o VSPackages estenda projetos com base no Microsoft Build Engine (MSBuild). O uso da agregação permite reutilizar a maior parte do sistema de projeto gerenciado principal implementado no e ainda personalizar o comportamento [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] para um cenário específico.

 Os tópicos a seguir detalham o design básico e a implementação de subtipos de projeto:

- Design de subtipo de projeto.

- Agregação de vários níveis.

- Interfaces de suporte.

## <a name="project-subtype-design"></a>Design de subtipo de projeto

A inicialização de um subtipo de projeto é alcançada agregando os objetos principal <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> e . Essa agregação permite que um subtipo de projeto substitua ou aprimora a maioria dos recursos do projeto base. Subtipos de projeto tem a primeira chance de lidar com propriedades usando , comandos usando e <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> e gerenciamento de item de projeto usando <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> . Os subtipos de projeto também podem estender:

- Objetos de configuração do projeto.

- Objetos dependentes de configuração.

- Objetos de navegação independentes de configuração.

- Objetos de automação de projeto.

- Coleções de propriedades de automação de projeto.

Para obter mais informações sobre extensibilidade por subtipos de projeto, consulte Propriedades e métodos [estendidos por subtipos de projeto.](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md)

### <a name="policy-files"></a>Arquivos de Política

O ambiente fornece um exemplo de extensão do sistema de projeto base com um subtipo de projeto [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] em sua implementação de arquivos de política. Um arquivo de política permite a formatação do ambiente gerenciando recursos que incluem o Gerenciador de Soluções, a caixa de diálogo Adicionar Projeto, a caixa de diálogo Adicionar Novo Item e a caixa de diálogo [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] Propriedades.    O subtipo de política substitui e aprimora esses recursos por <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> meio de `IOleCommandTarget` <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> implementações e .

### <a name="aggregation-mechanism"></a>Mecanismo de agregação

O mecanismo de agregação de subtipo de projeto do ambiente dá suporte a vários níveis de agregação, permitindo que um subtipo avançado seja implementado por meio de um projeto mais saboroso. Além disso, os objetos de suporte de um subtipo de projeto, como , são <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> projetados para permitir vários níveis de camadas. Para manter as restrições das regras de agregação COM e COM, subtipos de projeto e projetos base precisam ser programados de forma cooperativo para permitir que o subtipo interno ou o projeto base participe corretamente da delegação de chamadas de método e do gerenciamento de contagens de referência. Ou seja, o projeto prestes a ser agregado deve ser programado para dar suporte à agregação.

A ilustração a seguir mostra uma representação esquematização de uma agregação de subtipo de projeto de vários níveis.

![Gráfico de projectflavor de vários níveis do Visual Studio](../../extensibility/internals/media/vs_multilevelprojectflavor.gif)

Uma agregação de subtipo de projeto de vários níveis consiste em três níveis, um projeto base, que é agregado por um subtipo de projeto e, em seguida, agregado por um subtipo de projeto avançado. A figura se concentra em algumas das interfaces de suporte fornecidas como parte da arquitetura [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] de subtipo de projeto.

### <a name="deployment-mechanisms"></a>Mecanismos de implantação

Entre muitas das funcionalidades do sistema de projeto base aprimoradas por um subtipo de projeto estão os mecanismos de implantação. Um subtipo de projeto influencia os mecanismos de implantação implementando interfaces de configuração (como e ) que são recuperadas chamando <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> QueryInterface em <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> . Em um cenário em que o subtipo de projeto e o subtipo de projeto avançado adicionam implementações de configuração diferentes, o projeto base chama no subtipo `QueryInterface` avançado do projeto `IUnknown` . Se o subtipo de projeto interno contiver a implementação de configuração que o projeto base está solicitando, o subtipo de projeto avançado delega à implementação fornecida pelo subtipo de projeto interno. Como um mecanismo para persistir o estado de um nível de agregação para outro, todos os níveis de subtipos de projeto implementam para persistir dados XML não relacionados ao build nos arquivos <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> de projeto. Para obter mais informações, [consulte Persistindo dados no arquivo de projeto do MSBuild.](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md) <xref:EnvDTE80.IInternalExtenderProvider> é implementado como um mecanismo para recuperar os extenders de automação dos subtipos de projeto.

A ilustração a seguir se concentra na implementação do extensor de automação, a configuração do projeto procurar o objeto em particular, usado por subtipos de projeto para estender o sistema de projeto base.

![Gráfico do Extensor Automático do Vs Project Flavor](../../extensibility/internals/media/vs_projectflavorautoextender.gif)

Subtipos de projeto podem estender ainda mais o sistema de projeto base estendendo o modelo de objeto de automação. Eles são definidos como parte do objeto de automação de DTE e são usados para estender o objeto Project, o `ProjectItem` objeto e o objeto `Configuration` . Para obter mais informações, [consulte Estendendo o modelo de objeto do projeto base](../../extensibility/internals/extending-the-object-model-of-the-base-project.md).

## <a name="multi-level-aggregation"></a>Agregação de vários níveis

Uma implementação de subtipo de projeto que envolve um subtipo de projeto de nível inferior precisa ser programada de forma cooperativa para permitir que o subtipo de projeto interno funcione corretamente. Uma lista de responsabilidades de programação inclui:

- A implementação do subtipo de projeto que está envolvendo o subtipo interno deve delegar à implementação do subtipo de projeto interno <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> para os métodos e <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> .

- A <xref:EnvDTE80.IInternalExtenderProvider> implementação do subtipo de projeto wrapper deve delegar à de seu subtipo de projeto interno. Em particular, a implementação de precisa obter a cadeia de caracteres de nomes do subtipo de projeto interno e concatenar as cadeias de caracteres que deseja adicionar como <xref:EnvDTE80.IInternalExtenderProvider.GetExtenderNames%2A> estendedores.

- A implementação de um subtipo de projeto wrapper deve insinuar o objeto de seu subtipo de projeto interno e mantê-lo como um delegado privado, já que apenas o objeto de configuração do projeto base sabe diretamente que o objeto de configuração de subtipo de projeto <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> wrapper existe. O subtipo de projeto externo pode inicialmente escolher interfaces de configuração que deseja manipular diretamente e, em seguida, delegar o restante à implementação do subtipo de projeto interno de <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg.get_CfgType%2A> .

## <a name="supporting-interfaces"></a>Interfaces de suporte

O projeto base delega chamadas para interfaces de suporte adicionadas por um subtipo de projeto, para estender vários aspectos de sua implementação. Isso inclui a extensão de objetos de configuração de projeto e vários objetos de navegador de propriedade. Essas interfaces são recuperadas chamando em (um ponteiro para o ) do agregador de subtipo de projeto mais `QueryInterface` `punkOuter` `IUnknown` externo.

|Interface|Subtipo do projeto|
|---------------|---------------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>|Permite que o subtipo de projeto:<br /><br /> - Forneça uma implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> .<br />– Controlar o lançamento do depurador permitindo que o subtipo de projeto forneça sua própria implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> .<br />– Desabilite a avaliação da expressão em tempo de design manipulando adequadamente `DBGLAUNCH_DesignTimeExprEval` o caso em sua implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.QueryDebugLaunch%2A> .|
|<xref:EnvDTE80.IInternalExtenderProvider>|Permite que o subtipo de projeto:<br /><br /> – Estenda <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject> o do projeto para adicionar ou remover propriedades independentes de configuração do projeto.<br />– Estenda o objeto de automação de projeto ( <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtObject> ) do projeto.<br /><br /> Os valores de propriedade acima são retirados <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> da enumeração .|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>|Permite que o subtipo de projeto mapeie de volta para o objeto, considerando o objeto de navegação <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> da configuração do projeto.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBrowseObject>|Permite que o subtipo de projeto mapeie de volta para o objeto ou , considerando o objeto de navegação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> `VSITEMID` configuração do projeto.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>|Permite que o subtipo de projeto persista dados estruturados XML arbitrários para o arquivo de projeto (.vbproj ou .csproj). Esses dados não são visíveis para o MSBuild.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>|Permite que o subtipo de projeto:<br /><br /> - Adicione novas propriedades do MSBuild a serem persistentes.<br />– Remover propriedades desnecessárias do MSBuild.<br />– Consultar um valor atual de uma propriedade do MSBuild.<br />- Altere o valor atual de uma propriedade do MSBuild.|

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>
