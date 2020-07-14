---
title: Como recuperar o serviço de projeto do SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project service
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f49883337c5748c0f8bcab5d0a88e02612e51b4c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015556"
---
# <a name="how-to-retrieve-the-sharepoint-project-service"></a>Como recuperar o serviço de projeto do SharePoint
  Você pode acessar o serviço de projeto do SharePoint nos seguintes tipos de soluções:

- Uma extensão do sistema de projeto do SharePoint, como uma extensão de projeto, uma extensão de item de projeto ou uma definição de tipo de item de projeto. Para obter mais informações sobre esses tipos de extensões, consulte [estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md).

- Uma extensão do nó **conexões do SharePoint** no **Gerenciador de servidores**. Para obter mais informações sobre esses tipos de extensões, consulte [estender o nó conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).

- Outro tipo de extensão do Visual Studio, como um VSPackage.

## <a name="retrieve-the-service-in-project-system-extensions"></a>Recuperar o serviço nas extensões do sistema de projeto
 Em qualquer extensão do sistema de projeto do SharePoint, você pode acessar o serviço de projeto usando a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.ProjectService%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject> objeto.

 Você também pode recuperar o serviço de projeto usando os procedimentos a seguir.

#### <a name="to-retrieve-the-service-in-a-project-extension"></a>Para recuperar o serviço em uma extensão de projeto

1. Na sua implementação da <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> interface, localize o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension.Initialize%2A> método.

2. Use o parâmetro *ProjectService* para acessar o serviço.

     O exemplo de código a seguir demonstra como usar o serviço de projeto para gravar uma mensagem na janela de **saída** e **lista de erros** janela em uma extensão de projeto simples.

     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#1](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#1)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#1](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#1)]

     Para obter mais informações sobre como criar extensões de projeto, consulte [como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md).

#### <a name="to-retrieve-the-service-in-a-project-item-extension"></a>Para recuperar o serviço em uma extensão de item de projeto

1. Na sua implementação da <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> interface, localize o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension.Initialize%2A> método.

2. Use a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType.ProjectService%2A> Propriedade do parâmetro *projectItemType* para recuperar o serviço.

     O exemplo de código a seguir demonstra como usar o serviço de projeto para gravar uma mensagem na janela de **saída** e **lista de erros** janela em uma extensão simples do item de projeto de **definição de lista** .

     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#2](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#2)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#2](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#2)]

     Para obter mais informações sobre como criar extensões de item de projeto, consulte [como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md).

#### <a name="to-retrieve-the-service-in-a-project-item-type-definition"></a>Para recuperar o serviço em uma definição de tipo de item de projeto

1. Na sua implementação da <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> interface, localize o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider.InitializeType%2A> método.

2. Use a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition.ProjectService%2A> Propriedade do parâmetro *TypeDefinition* para recuperar o serviço.

     O exemplo de código a seguir demonstra como usar o serviço de projeto para gravar uma mensagem na janela de **saída** e **lista de erros** janela em uma definição de tipo de item de projeto simples.

     [!code-vb[SPExtensibility.ProjectService.FromProjectSystemExtensions#3](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.vb#3)]
     [!code-csharp[SPExtensibility.ProjectService.FromProjectSystemExtensions#3](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromprojectsystemextensions.getprojectservice/extension/extension.cs#3)]

     Para obter mais informações sobre como definir tipos de item de projeto, consulte [como definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md).

## <a name="retrieve-the-service-in-server-explorer-extensions"></a>Recuperar o serviço em extensões de Gerenciador de Servidores
 Em uma extensão do nó **conexões do SharePoint** no **Gerenciador de servidores**, você pode acessar o serviço de projeto usando a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> objeto.

#### <a name="to-retrieve-the-service-in-a-server-explorer-extension"></a>Para recuperar o serviço em uma extensão de Gerenciador de Servidores

1. Obter um <xref:System.IServiceProvider> objeto da <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.ServiceProvider%2A> propriedade de um <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode> objeto em sua extensão.

2. Use o <xref:System.IServiceProvider.GetService%2A> método para solicitar um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> objeto.

     O exemplo de código a seguir demonstra como usar o serviço de projeto para gravar uma mensagem na janela de **saída** e **lista de erros** janela de um menu de atalho que a extensão adiciona aos nós da lista em **Gerenciador de servidores**.

     [!code-vb[SPExtensibility.ProjectService.FromSPExplorerExtensions#1](../sharepoint/codesnippet/VisualBasic/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.vb#1)]
     [!code-csharp[SPExtensibility.ProjectService.FromSPExplorerExtensions#1](../sharepoint/codesnippet/CSharp/spextensibility.projectservice.fromspexplorerextensions.getprojectservice/extension/extension.cs#1)]

     Para obter mais informações sobre como estender o nó **conexões do SharePoint** no **Gerenciador de servidores**, consulte [como: estender um nó do SharePoint no Gerenciador de servidores](../sharepoint/how-to-extend-a-sharepoint-node-in-server-explorer.md).

## <a name="retrieve-the-service-in-other-visual-studio-extensions"></a>Recuperar o serviço em outras extensões do Visual Studio
 Você pode recuperar o serviço de projeto em um VSPackage ou em qualquer extensão do Visual Studio que tenha acesso a um <xref:EnvDTE80.DTE2> objeto no modelo de objeto de automação, como um assistente de modelo de projeto que implementa a <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface.

 Em um VSPackage, você pode solicitar um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> objeto usando um dos seguintes métodos:

- O <xref:System.IServiceProvider.GetService%2A> método de um VSPackage gerenciado que deriva da <xref:Microsoft.VisualStudio.Shell.Package> classe. Para obter mais informações, consulte [como: obter um serviço](../extensibility/how-to-get-a-service.md).

- O <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> método estático. Para obter mais informações, consulte [usar GetGlobalService](../extensibility/internals/service-essentials.md#how-to-use-getglobalservice).

  Em uma extensão do Visual Studio que tem acesso a um <xref:EnvDTE80.DTE2> objeto, você pode solicitar um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> objeto usando o <xref:Microsoft.VisualStudio.Shell.ServiceProvider.GetService%2A> método de um <xref:Microsoft.VisualStudio.Shell.ServiceProvider> objeto. Para obter mais informações, consulte [obtendo um serviço do objeto DTE](../extensibility/how-to-get-a-service.md#getting-a-service-from-the-dte-object).

## <a name="see-also"></a>Consulte também
- [Usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md)
- [Como: obter um serviço](../extensibility/how-to-get-a-service.md)
- [Como: usar assistentes com modelos de projeto](../extensibility/how-to-use-wizards-with-project-templates.md)
