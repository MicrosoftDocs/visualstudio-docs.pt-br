---
title: Extensões de ferramentas de visão geral do modelo de programação do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Studio, extending tools
- SharePoint development in Visual Studio, extensibility object models
- SharePoint development in Visual Studio, extending tools
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 82309d00d45ab6ac801297a55371cf9be5620440
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49829476"
---
# <a name="overview-of-the-programming-model-of-sharepoint-tools-extensions"></a>Extensões de ferramentas de visão geral do modelo de programação do SharePoint
  Quando você cria uma extensão para as ferramentas do SharePoint no Visual Studio, você começar com a implementação de uma ou mais interfaces de extensibilidade que são expostos pelas ferramentas do SharePoint. Na maioria dos casos, você também usará outros tipos fornecidos pelas ferramentas do SharePoint para implementar recursos em sua extensão. Em alguns cenários, você também pode usar tipos em outros modelos de objeto fornecidos pelo Visual Studio e do SharePoint. Você deve entender a finalidade de cada um desses modelos de objeto e souber como usá-los uns com os outros para criar extensões para as ferramentas do SharePoint.  

## <a name="extend-the-sharepoint-tools-by-implementing-extensibility-interfaces"></a>Estender as ferramentas do SharePoint com a implementação de interfaces de extensibilidade
 Visual Studio usa o MEF Managed Extensibility Framework () no .NET Framework 4 para fornecer o modelo de extensibilidade para as ferramentas do SharePoint. MEF é uma API (implementada no assembly Composition) que permite que os aplicativos para expor pontos de extensibilidade e descobrir e carregar extensões em tempo de execução. Para obter mais informações sobre o MEF, consulte [Managed Extensibility Framework &#40;MEF&#41;](/dotnet/framework/mef/index).  

 Para estender as ferramentas do SharePoint, implemente uma ou mais interfaces de extensibilidade que são expostas pelo Visual Studio. Você também deve aplicar o <xref:System.ComponentModel.Composition.ExportAttribute>, e os atributos de ferramentas específicas do SharePoint adicional conforme necessário, para sua implementação de interface. A tabela a seguir lista as interfaces que você pode implementar para estender as ferramentas do SharePoint.  

|Interface|Descrição|  
|---------------|-----------------|  
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider>|Implemente essa interface para definir um novo tipo de item de projeto do SharePoint. Por exemplo, consulte [como: definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md).|  
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension>|Implemente essa interface para estender um tipo de item de projeto do SharePoint que já está instalado no Visual Studio. Por exemplo, consulte [como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md).|  
|<xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension>|Implemente essa interface para estender projetos do SharePoint. Por exemplo, consulte [como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md).|  
|<xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep>|Implemente essa interface para definir uma nova etapa de implantação que pode ser executada quando um item de projeto do SharePoint é implantado ou cancelado. Por exemplo, consulte [instruções passo a passo: criar uma etapa de implantação para projetos do SharePoint](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md).|  
|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension>|Implementar essa interface para estender um nó existente sob o **conexões do SharePoint** nó na **Server Explorer** janela. Por exemplo, consulte [como: estender um nó SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md).|  
|<xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider>|Implementar essa interface para definir um novo tipo de nó sob o **conexões do SharePoint** nó na **Gerenciador de servidores** janela. Por exemplo, consulte [como: estender um nó SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md).|  
|<xref:Microsoft.VisualStudio.SharePoint.Validation.IFeatureValidationRule>|Implemente essa interface para definir uma regra de validação de recurso personalizado. Por exemplo, consulte [como: criar o recurso personalizado e o pacote de regras de validação para soluções do SharePoint](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md).|  
|<xref:Microsoft.VisualStudio.SharePoint.Validation.IPackageValidationRule>|Implemente essa interface para definir uma regra de validação de pacote personalizado. Por exemplo, consulte [como: criar o recurso personalizado e o pacote de regras de validação para soluções do SharePoint](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md).|  

 Depois de implementar uma extensão das ferramentas do SharePoint, você deve implantar o assembly de extensão em um pacote de extensão (VSIX) do Visual Studio para habilitar descobrir e carregar a extensão do Visual Studio. Para obter mais informações, consulte [implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).  

## <a name="understand-the-object-models-that-you-use-in-sharepoint-tools-extensions"></a>Entender os modelos de objeto que você usa nas extensões de ferramentas do SharePoint
 Há vários modelos de objeto, que você pode usar ao criar extensões para as ferramentas do SharePoint:  

-   *Modelo de objeto de ferramentas do SharePoint*. Esse modelo de objeto fornece as interfaces de extensibilidade que você pode implementar para criar extensões de ferramentas do SharePoint e outros tipos relacionados.  

-   *Modelos de objeto de automação e a integração Visual do Studio*. Use esses modelos de objeto para acessar recursos do Visual Studio que estão além do escopo do modelo de objeto de ferramentas do SharePoint.  

    > [!NOTE]  
    >  Você pode converter alguns objetos no modelo de objeto de ferramentas do SharePoint para objetos na automação do Visual Studio e modelos de objeto de integração e vice-versa, usando o serviço de projeto do SharePoint. Para obter mais informações, consulte [converter entre tipos de sistema de projeto do SharePoint e outros tipos de projeto do Visual Studio](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md).  

-   *Os modelos de objeto de cliente e servidor do SharePoint*. Use esses modelos de objeto para modificar um site do SharePoint ou para recuperar dados de um site do SharePoint a partir do contexto de uma extensão de ferramentas do SharePoint.  

### <a name="sharepoint-tools-object-model"></a>Modelo de objeto de ferramentas do SharePoint
 Cada extensão de ferramentas do SharePoint usa tipos no modelo de objeto de ferramentas do SharePoint para definir o comportamento principal e a funcionalidade da extensão. As tabelas a seguir descrevem os namespaces que estão incluídos nesse modelo de objeto, por que o assembly que os contém.

#### <a name="microsoftvisualstudiosharepointdll"></a>Microsoft.VisualStudio.SharePoint.dll    

|Namespace|Descrição|  
|-|-|  
|<xref:Microsoft.VisualStudio.SharePoint>|Contém tipos que você usa para estender e automatizar o sistema de projeto do SharePoint. Por exemplo, você pode estender a itens de projeto e projetos internos do SharePoint, ou você pode criar seus próprios itens de projeto. Para obter mais informações, consulte [estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md).|  
|<xref:Microsoft.VisualStudio.SharePoint.Deployment>|Contém tipos que você usa para estender o processo de implantação para projetos do SharePoint, como criar suas próprias etapas de implantação e configurações de implantação. Para obter mais informações, consulte [estender o SharePoint empacotamento e implantação](../sharepoint/extending-sharepoint-packaging-and-deployment.md).|  
|<xref:Microsoft.VisualStudio.SharePoint.Explorer>|Contém tipos que você usa para estender os nós sob o **conexões do SharePoint** nó na **Server Explorer** janela, ou para definir novos tipos de nós. Para obter mais informações, consulte [estender o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).|  
|<xref:Microsoft.VisualStudio.SharePoint.Features>|Contém tipos que você usa para acessar as definições de recurso em um projeto do SharePoint.|  
|<xref:Microsoft.VisualStudio.SharePoint.Packages>|Contém tipos que você usa para acessar a definição de pacote em uma solução do SharePoint.|  
|<xref:Microsoft.VisualStudio.SharePoint.Validation>|Contém tipos que você pode usar para personalizar o comportamento de validação de pacote e o recurso para projetos do SharePoint. Para obter mais informações, consulte [como: criar o recurso personalizado e o pacote de regras de validação para soluções do SharePoint](../sharepoint/how-to-create-custom-feature-and-package-validation-rules-for-sharepoint-solutions.md).| 

#### <a name="microsoftvisualstudiosharepointcommandsdll"></a>Microsoft.VisualStudio.SharePoint.Commands.dll

|Namespace|Descrição|  
|-|-|  
|<xref:Microsoft.VisualStudio.SharePoint.Commands>|Contém tipos que você pode usar para criar um personalizado *comandos do SharePoint*. Um comando do SharePoint é um método que chama o modelo de objeto de servidor do SharePoint a partir de uma extensão de ferramentas do SharePoint. Para obter mais informações, consulte [chamam os modelos de objeto SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).|

#### <a name="microsoftvisualstudiosharepointexplorerextensionsdll"></a>Microsoft.VisualStudio.SharePoint.Explorer.Extensions.dll

|Namespace|Descrição|  
|-|-| 
|<xref:Microsoft.VisualStudio.SharePoint.Explorer.Extensions>|Contém tipos que você pode usar para obter informações sobre interno **Gerenciador de servidores** nós que representam componentes individuais em um site do SharePoint, como um nó que representa uma lista, campo ou tipo de conteúdo. Para obter mais informações, consulte [estender o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).|  

### <a name="visual-studio-automation-object-model"></a>Modelo de objeto de automação do Visual Studio
 O modelo de objeto de automação do Visual Studio fornece APIs que você pode usar para automatizar projetos do Visual Studio e o IDE. Use o modelo de objeto do Visual Studio para executar tarefas relacionadas ao projeto que não são específicas para projetos do SharePoint ou executar outras tarefas de automação geral no Visual Studio. Tradicionalmente, esse modelo de objeto é geralmente usado em macros e suplementos do Visual Studio, mas você também pode usá-lo em extensões de ferramentas do SharePoint.  

 A parte principal do modelo de objeto de automação do Visual Studio é definida na *EnvDTE.dll* assembly. O *EnvDTE\\<version>. dll* assemblies fornecem funcionalidade adicional que foi introduzida em versões específicas do Visual Studio. Esses assemblies são incluídos com o Visual Studio.  

 Para obter mais informações sobre o modelo de objeto de automação, consulte [referência de SDK do Visual Studio](../extensibility/visual-studio-sdk-reference.md).  

### <a name="visual-studio-integration-object-model"></a>Modelo de objeto de integração do Visual Studio
 O modelo de objeto de integração fornece APIs que você pode usar para adicionar recursos ao Visual Studio, criando uma *VSPackage*. Um VSPackage é um módulo que estende o Visual Studio IDE, fornecendo recursos personalizados como janelas de ferramentas, editores, designers, serviços e projetos.  

 Se você quiser adicionar um novo recurso do Visual Studio que será usado com as ferramentas internas do SharePoint, você pode usar o modelo de objeto de integração. Por exemplo, se você criar um item de projeto personalizado do SharePoint que representa uma ação personalizada para um site do SharePoint, você também pode criar um VSPackage que implementa um designer para a ação personalizada. Você pode associar o designer com a ação personalizada com a adição de um item de menu de atalho para o item de projeto que representa a ação personalizada no **Gerenciador de soluções**. Você pode abrir o designer, abrindo o menu de atalho (clicando com o item de projeto de ação personalizada ou selecioná-la e, em seguida, escolhendo a **Shift**+**F10** chaves) e, em seguida, escolhendo **Aberto**.  

 Esse modelo de objeto é definido em um conjunto de assemblies que são incluídos com o SDK do Visual Studio. Alguns dos principais assemblies nesse modelo de objeto incluem *Microsoft.VisualStudio.Shell.11.0.dll*, *Microsoft.VisualStudio.Shell.Interop.dll*, e  *Microsoft.VisualStudio.OLE.Interop.dll*.  

 Para obter mais informações sobre o modelo de objeto de integração, consulte [visão geral do modelo de automação](/visualstudio/extensibility/internals/automation-model-overview) e [referência de SDK do Visual Studio](/visualstudio/extensibility/visual-studio-sdk-reference).  

### <a name="sharepoint-object-models"></a>Modelos de objeto do SharePoint
 Extensões de ferramentas do SharePoint podem usar APIs do SharePoint para modificar um site do SharePoint ou para recuperar dados de um site do SharePoint. [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] e [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] fornecem dois modelos de objeto diferentes: um modelo de objeto de servidor e um modelo de objeto do cliente.  

 Você pode usar as APIs em qualquer um dos modelos de objeto em uma extensão de ferramentas do SharePoint, mas cada modelo de objeto tem algumas vantagens e desvantagens no contexto das extensões de ferramentas do SharePoint. Para obter mais informações, consulte [chamam os modelos de objeto SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).  

|Modelo de objeto|Descrição|  
|------------------|-----------------|  
|Modelo de objeto de servidor|O modelo de objeto de servidor fornece acesso a todos os recursos [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] e [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] expor por meio de programação. Esse modelo de objeto foi projetado para ser usado por soluções de SharePoint que são executados no servidor do SharePoint. A maior parte desse modelo de objeto é definida na *dll* assembly. Para obter mais informações sobre o modelo de objeto de servidor, consulte [usando o modelo de objeto de servidor do SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkId=177796).|  
|Modelo de objeto do cliente|O modelo de objeto do cliente é um subconjunto do modelo de objeto de servidor que pode ser usado para interoperar com dados de um cliente remoto ou servidor do SharePoint. Ele é projetado para minimizar o número de viagens de ida e que devem ser executadas para realizar tarefas comuns. A maior parte do modelo de objeto do cliente é definida na *Microsoft.SharePoint.Client.dll* e *Microsoft.SharePoint.Client.Runtime.dll* assemblies. Para obter mais informações sobre o modelo de objeto do cliente, consulte [modelo de objeto de cliente gerenciado](http://go.microsoft.com/fwlink/?LinkId=177797).|  

## <a name="see-also"></a>Consulte também
 [Estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)   
 [Chamar os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md)   
 [Usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md)  

