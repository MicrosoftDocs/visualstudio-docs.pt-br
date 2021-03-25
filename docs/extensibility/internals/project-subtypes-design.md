---
title: Design de subtipos do projeto | Microsoft Docs
description: Saiba como os subtipos de projeto permitem que o VSPackages estenda projetos com base no Microsoft Build Engine (MSBuild).
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, design
ms.assetid: 405488bb-1362-40ed-b0f1-04a57fc98c56
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: bfc689705d4d42016f184a25b70564591aa5c04d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/25/2021
ms.locfileid: "105064495"
---
# <a name="project-subtypes-design"></a>Design de subtipos de projeto

Os subtipos de projeto permitem que o VSPackages estenda projetos com base no Microsoft Build Engine (MSBuild). O uso da agregação permite que você reutilize a grande parte do sistema de projeto gerenciado central implementado no, [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] embora ainda Personalize o comportamento de um cenário específico.

 Os tópicos a seguir detalham o design básico e a implementação de subtipos de projeto:

- Design de subtipo de projeto.

- Agregação de vários níveis.

- Suporte a interfaces.

## <a name="project-subtype-design"></a>Design de subtipo de projeto

A inicialização de um subtipo de projeto é obtida por meio da agregação dos <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> objetos Main e <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> . Essa agregação permite que um subtipo de projeto substitua ou aprimore a maioria dos recursos do projeto base. Os subtipos de projeto obtêm a primeira chance de manipular propriedades usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> , comandos usando o e o e o <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> Gerenciamento de itens de <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> projeto usando o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3> . Os subtipos de projeto também podem estender:

- Objetos de configuração do projeto.

- Objetos dependentes de configuração.

- Objetos de navegação independentes de configuração.

- Objetos de automação do projeto.

- Coleções de propriedades de automação do projeto.

Para obter mais informações sobre a extensibilidade por subtipos de projeto, consulte [Propriedades e métodos estendidos por subtipos de projeto](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md).

### <a name="policy-files"></a>Arquivos de Política

O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente fornece um exemplo de extensão do sistema de projeto base com um subtipo de projeto em sua implementação de arquivos de política. Um arquivo de política permite a formatação do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente Gerenciando recursos que incluem o Gerenciador de soluções, caixa de diálogo **Adicionar projeto** , caixa de diálogo **Adicionar novo item** e a caixa de diálogo **Propriedades** . O subtipo de política substitui e aprimora esses recursos por <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg> meio `IOleCommandTarget` de <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> implementações do e do.

### <a name="aggregation-mechanism"></a>Mecanismo de agregação

O mecanismo de agregação de subtipo de projeto do ambiente dá suporte a vários níveis de agregação, permitindo que um subtipo avançado seja implementado ao resumir um projeto resumido. Além disso, os objetos de suporte de um subtipo de projeto, como <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> , são projetados para permitir vários níveis de disposição em camadas. Ao manter as restrições das regras de agregação COM e COM, os subtipos de projeto e os projetos base precisam ser programados de forma cooperativa para habilitar o subtipo interno ou o projeto base para participar adequadamente da delegação de chamadas de método e gerenciamento de contagens de referência. Ou seja, o projeto prestes a ser agregado deve ser programado para dar suporte à agregação.

A ilustração a seguir mostra uma representação esquemático de uma agregação de subtipo de projeto de vários níveis.

![Gráfico de projectflavor de vários níveis do Visual Studio](../../extensibility/internals/media/vs_multilevelprojectflavor.gif)

Uma agregação de subtipo de projeto de várias níveis consiste em três níveis, um projeto base, que é agregado por um subtipo de projeto e agregado posteriormente por um subtipo de projeto avançado. A figura se concentra em algumas das interfaces de suporte que são fornecidas como parte da arquitetura de [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] subtipo de projeto.

### <a name="deployment-mechanisms"></a>Mecanismos de implantação

Entre muitas das funcionalidades básicas do sistema de projeto aprimoradas por um subtipo de projeto estão os mecanismos de implantação. Um subtipo de projeto influencia os mecanismos de implantação implementando interfaces de configuração (como <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg> ) que são recuperados chamando QueryInterface em <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> . Em um cenário em que tanto o subtipo do projeto quanto o subtipo projeto avançado adicionam implementações de configuração diferentes, o projeto base chama `QueryInterface` os subtipos do projeto avançado `IUnknown` . Se o subtipo de projeto interno contiver a implementação de configuração que o projeto base está solicitando, o subtipo de projeto avançado delegará para a implementação fornecida pelo subtipo de projeto interno. Como um mecanismo para persistir o estado de um nível de agregação para outro, todos os níveis de subtipos de projeto implementam <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> para persistir dados XML relacionados à não compilação nos arquivos de projeto. Para obter mais informações, consulte [Persistendo dados no arquivo de projeto do MSBuild](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md). <xref:EnvDTE80.IInternalExtenderProvider> é implementado como um mecanismo para recuperar extensores de automação dos subtipos do projeto.

A ilustração a seguir enfoca a implementação do extensor de automação, o objeto de procura de configuração do projeto em particular, usado por subtipos de projeto para estender o sistema de projeto base.

![Gráfico do extensor automático do tipo de projeto VS](../../extensibility/internals/media/vs_projectflavorautoextender.gif)

Os subtipos de projeto podem estender ainda mais o sistema de projeto base estendendo o modelo de objeto de automação. Eles são definidos como parte do objeto de automação do DTE e são usados para estender o objeto do projeto, o `ProjectItem` objeto e o `Configuration` objeto. Para obter mais informações, consulte [estendendo o modelo de objeto do projeto base](../../extensibility/internals/extending-the-object-model-of-the-base-project.md).

## <a name="multi-level-aggregation"></a>Agregação de vários níveis

Uma implementação de subtipo de projeto que encapsula um subtipo de projeto de nível inferior precisa ser programada de forma cooperativa para permitir que o subtipo de projeto interno funcione corretamente. Uma lista de responsabilidades de programação inclui:

- A <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> implementação do subtipo do projeto que está encapsulando o subtipo interno deve delegar para a <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> implementação do subtipo do projeto interno para ambos os <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> métodos e.

- A <xref:EnvDTE80.IInternalExtenderProvider> implementação do subtipo de projeto de wrapper deve delegar para o seu subtipo de projeto interno. Em particular, a implementação de <xref:EnvDTE80.IInternalExtenderProvider.GetExtenderNames%2A> precisa obter a cadeia de caracteres de nomes do subtipo projeto interno e concatenar as cadeias de caracteres que deseja adicionar como extensores.

- A <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> implementação de um subtipo de projeto de wrapper deve instanciar o <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> objeto de seu subtipo de projeto interno e mantê-lo como um delegado privado, já que apenas o objeto de configuração de projeto do projeto base sabe diretamente que o objeto de configuração de subtipo de projeto de wrapper existe. O subtipo de projeto externo pode inicialmente escolher as interfaces de configuração que deseja tratar diretamente e delegar o restante à implementação do subtipo do projeto interno de <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg.get_CfgType%2A> .

## <a name="supporting-interfaces"></a>Interfaces de suporte

O projeto base Delega chamadas para interfaces de suporte adicionadas por um subtipo de projeto, para estender vários aspectos de sua implementação. Isso inclui a extensão de objetos de configuração do projeto e vários objetos do navegador de propriedades. Essas interfaces são recuperadas chamando `QueryInterface` on `punkOuter` (um ponteiro para o `IUnknown` ) do agregador de subtipo de projeto mais externo.

|Interface|Subtipo de projeto|
|---------------|---------------------|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>|Permite que o subtipo do projeto:<br /><br /> – Forneça uma implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> .<br />-Controle a inicialização do depurador, permitindo que o subtipo de projeto forneça sua própria implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg> .<br />-Desabilite a avaliação de expressão em tempo de design, manipulando adequadamente o `DBGLAUNCH_DesignTimeExprEval` caso em sua implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.QueryDebugLaunch%2A> .|
|<xref:EnvDTE80.IInternalExtenderProvider>|Permite que o subtipo do projeto:<br /><br /> -Estenda o <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_BrowseObject> do projeto para adicionar ou remover propriedades independentes de configuração do projeto.<br />-Estenda o objeto de automação do projeto ( <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_ExtObject> ) do projeto.<br /><br /> Os valores de propriedade acima são obtidos da <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> enumeração.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>|Permite que o subtipo do projeto mapeie de volta para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> objeto de acordo com o objeto de procura de configuração do projeto.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBrowseObject>|Permite que o subtipo de projeto mapeie de volta para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> `VSITEMID` objeto ou, dado ao objeto de procura de configuração do projeto.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>|Permite que o subtipo de projeto persista dados estruturados XML arbitrários no arquivo de projeto (. vbproj ou. csproj). Esses dados não são visíveis para o MSBuild.|
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>|Permite que o subtipo do projeto:<br /><br /> -Adicionar novas propriedades do MSBuild a serem persistidas.<br />-Remova as propriedades desnecessárias do MSBuild.<br />-Consulta para obter um valor atual de uma propriedade do MSBuild.<br />-Alterar o valor atual de uma propriedade do MSBuild.|

## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>
- <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>
