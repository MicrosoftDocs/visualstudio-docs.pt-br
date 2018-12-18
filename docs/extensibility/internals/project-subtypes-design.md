---
title: Design os subtipos de projeto | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- project subtypes, design
ms.assetid: 405488bb-1362-40ed-b0f1-04a57fc98c56
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: b9032da4a8884c940973865016bf0bbec955ebb5
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49876588"
---
# <a name="project-subtypes-design"></a>Design de subtipos de projeto
Subtipos do projeto permitem que os VSPackages estender projetos com base no Microsoft Build Engine (MSBuild). O uso de agregação lhe permite reutilizar a maior parte do sistema de projeto core gerenciado implementado em [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ainda ainda personalizar o comportamento para um cenário específico.  
  
 Os tópicos a seguir detalham o design básico e a implementação de subtipos de projeto:  
  
-   Design de subtipo de projeto.  
  
-   Agregação de vários nível.  
  
-   Interfaces de suporte.  
  
## <a name="project-subtype-design"></a>Design de subtipo de projeto  
 A inicialização de um subtipo de projeto é obtida ao agregar principal <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject> objetos. Essa agregação permite que um subtipo de projeto substituir ou aumentar a maioria dos recursos do projeto base. Subtipos de projeto obtém a primeira oportunidade para lidar com as propriedades usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy>, comandos usando <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy>e o gerenciamento de item de projeto usando <xref:Microsoft.VisualStudio.Shell.Interop.IVsProject3>. Também podem estender os subtipos de projeto:  
  
- Objetos de configuração do projeto.  
  
- Objetos dependentes de configuração.  
  
- Objetos de configuração independente procurar.  
  
- Objetos de automação do projeto.  
  
- Coleções de propriedade de automação de projeto.  
  
  Para obter mais informações sobre extensibilidade por subtipos do projeto, consulte [as propriedades e métodos estendidos por subtipos do projeto](../../extensibility/internals/properties-and-methods-extended-by-project-subtypes.md).  
  
##### <a name="policy-files"></a>Arquivos de política  
 O [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente fornece um exemplo de estender o sistema de projeto base com um subtipo de projeto em sua implementação de arquivos de política. Um arquivo de política permite que a modelagem do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ambiente por meio do gerenciamento de recursos que incluem o Gerenciador de soluções, **Add Project** caixa de diálogo **Adicionar Novo Item** caixa de diálogo e o  **Propriedades** caixa de diálogo. O subtipo de política substitui e aprimora esses recursos por meio <xref:Microsoft.VisualStudio.Shell.Interop.IVsFilterAddProjectItemDlg>, `IOleCommandTarget` e <xref:Microsoft.VisualStudio.Shell.Interop.IVsUIHierarchy> implementações.  
  
##### <a name="aggregation-mechanism"></a>Mecanismo de agregação  
 Mecanismo de agregação de subtipo de projeto do ambiente dá suporte a vários níveis de agregação, permitindo assim que um subtipo avançado ser implementada por mais de um projeto flavored flavoring. Além disso, os objetos de suporte de um projeto de subtipo, como <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>, são projetados para permitir que vários níveis de disposição em camadas. Para manter as restrições de COM e COM regras de agregação, subtipos do projeto e projetos base precisam ser programados de forma cooperativa para permitir que o subtipo interno ou projeto base participem adequadamente em chamadas de método de delegação e gerenciar contagens de referência . Ou seja, o projeto prestes a ser agregada tem de ser programado para dar suporte à agregação.  
  
 A ilustração a seguir mostra uma representação esquemática de uma agregação de subtipo de projeto de vários níveis.  
  
 ![Gráfico de projectflavor de vários níveis do Visual Studio](../../extensibility/internals/media/vs_multilevelprojectflavor.gif "VS_MultilevelProjectFlavor")  
Subtipo de projeto em vários níveis  
  
 Uma agregação de subtipo de vários níveis de projeto consiste em três níveis, um projeto de base, que é agregado por um subtipo de projeto, em seguida, ainda mais agregados por um subtipo de projeto avançadas. A Figura enfatiza algumas das interfaces de suporte que são fornecidas como parte do [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] subtipo de arquitetura do projeto.  
  
##### <a name="deployment-mechanisms"></a>Mecanismos de implantação  
 Entre muitos do sistema de projeto base as funcionalidades aprimoradas por um subtipo de projeto são os mecanismos de implantação. Um subtipo de projeto influencia os mecanismos de implantação com a implementação de interfaces de configuração (como <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg> e <xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildableProjectCfg>) que são recuperadas chamando QueryInterface no <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider>. Em um cenário onde o subtipo de projeto e o subtipo de projeto avançado adicionam implementações de configuração diferentes, o projeto base chama `QueryInterface` sobre o subtipo de projeto avançado `IUnknown`. Se o subtipo de projeto interno contém a implementação de configuração que o projeto base está pedindo para os delegados de subtipo de projeto avançado para a implementação fornecida pelo subtipo de projeto interno. Como um mecanismo para manter o estado do nível de uma agregação para outro, todos os níveis de subtipos de projeto implementam <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> persistir não-build relacionados a dados XML em arquivos de projeto. Para obter mais informações, consulte [persistência de dados no arquivo de projeto MSBuild](../../extensibility/internals/persisting-data-in-the-msbuild-project-file.md). <xref:EnvDTE80.IInternalExtenderProvider> é implementado como um mecanismo para recuperar os extensores de automação de subtipos de projeto.  
  
 A ilustração a seguir se concentra na implementação de extensor de automação, o objeto de procura de configuração de projeto em particular, usado por subtipos do projeto para estender o sistema de projeto base.  
  
 ![Gráfico de extensor de automático de tipo de projeto do VS](../../extensibility/internals/media/vs_projectflavorautoextender.gif "VS_ProjectFlavorAutoExtender")  
Extensor de automação do subtipo de projeto.  
  
 Subtipos de projeto podem estender ainda mais o sistema de projeto base, estendendo o modelo de objeto de automação. Esses são definidos como parte do objeto de automação de DTE e são usados para estender o objeto de projeto, o `ProjectItem` objeto e o `Configuration` objeto. Para obter mais informações, consulte [estendendo o modelo de objeto do projeto Base](../../extensibility/internals/extending-the-object-model-of-the-base-project.md).  
  
## <a name="multi-level-aggregation"></a>Agregação de vários nível  
 Uma implementação de subtipo de projeto que encapsula um subtipo de projeto de nível inferior deve ser programado cooperativamente para permitir que o subtipo de projeto interno funcionar corretamente. Inclui uma lista de responsabilidades de programação:  
  
-   O <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> implementação do subtipo de projeto que está encapsulando o subtipo interno deve delegar para o <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment> implementação do subtipo de projeto interno para ambos <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Load%2A> e <xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment.Save%2A> métodos.  
  
-   O <xref:EnvDTE80.IInternalExtenderProvider> implementação do subtipo de projeto de wrapper deverá delegar ao de seu subtipo de projeto interno. Em particular, a implementação de <xref:EnvDTE80.IInternalExtenderProvider.GetExtenderNames%2A> precisa obter a cadeia de caracteres de nomes do subtipo de projeto interno e, em seguida, concatenar as cadeias de caracteres que deseja adicionar como extensores.  
  
-   O <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectCfgProvider> implementação de um subtipo de projeto de wrapper deve instanciar a <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg> objeto do seu interna subtipo de projeto e mantê-la como um delegado particular, já que somente o objeto de configuração de projeto do projeto base diretamente sabe que o wrapper objeto de configuração do subtipo de projeto existe. O subtipo de projeto externa pode inicialmente escolher interfaces de configuração que ele deseja tratar diretamente e, em seguida, delegue o resto para implementação do subtipo de projeto interno da <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg.get_CfgType%2A>.  
  
## <a name="supporting-interfaces"></a>Interfaces de suporte  
 Projeto base delega chamadas ao suporte a interfaces adicionadas por um subtipo de projeto, para estender a vários aspectos da sua implementação. Isso inclui estender objetos de configuração de projeto e de vários objetos de navegador de propriedade. Essas interfaces são recuperadas chamando `QueryInterface` na `punkOuter` (um ponteiro para o `IUnknown`) do agregador de subtipo de projeto mais externo.  
  
|Interface|Subtipo de projeto|  
|---------------|---------------------|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFlavorCfg>|Permite que o subtipo de projeto para:<br /><br /> -Fornecer uma implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsDeployableProjectCfg>.<br />-Controlam o lançamento do depurador, permitindo que o subtipo de projeto fornecer sua própria implementação do <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg>.<br />-Desabilitar a avaliação da expressão de tempo de design por lidar adequadamente com o `DBGLAUNCH_DesignTimeExprEval` maiusculas em sua implementação de <xref:Microsoft.VisualStudio.Shell.Interop.IVsDebuggableProjectCfg.QueryDebugLaunch%2A>.|  
|<xref:EnvDTE80.IInternalExtenderProvider>|Permite que o subtipo de projeto para:<br /><br /> -Estender o <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID> do projeto para adicionar ou remover propriedades de configuração independente do projeto.<br />-Estender o objeto de automação de projeto (<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>) do projeto.<br /><br /> Valores de propriedade acima são obtidos do <xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID2> enumeração.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsCfgBrowseObject>|Permite que o subtipo de projeto mapear para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsCfg> objeto dado o objeto de procura de configuração do projeto.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBrowseObject>|Permite que o subtipo de projeto mapear para o <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy> ou o `VSITEMID` objeto, dado o objeto de procura de configuração do projeto.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IPersistXMLFragment>|Permite que o subtipo de projeto manter os dados XML estruturado arbitrários para o arquivo de projeto (. vbproj ou. csproj). Esses dados não são visíveis para o MSBuild.|  
|<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildPropertyStorage>|Permite que o subtipo de projeto para:<br /><br /> -Adicione novas propriedades do MSBuild a ser mantido.<br />-Remova propriedades desnecessárias do MSBuild.<br />-Consulta para um valor atual de uma propriedade do MSBuild.<br />-Altere o valor atual de uma propriedade do MSBuild.|  
  
## <a name="see-also"></a>Consulte também  
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__VSPROPID2>