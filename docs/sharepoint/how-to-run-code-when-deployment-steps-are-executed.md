---
title: 'Como: executar código quando etapas de implantação são executadas | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: cebd88cc49afa1092dfcd1d67ffdbf0fa3567ad0
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118439"
---
# <a name="how-to-run-code-when-deployment-steps-are-executed"></a>Como: executar o código quando etapas de implantação são executadas
  Se você quiser realizar tarefas adicionais para uma etapa de implantação em um projeto do SharePoint, você pode manipular eventos que são gerados por itens de projeto do SharePoint antes e após cada etapa de implantação de execução do Visual Studio. Para obter mais informações, consulte [estendendo SharePoint empacotamento e implantação](../sharepoint/extending-sharepoint-packaging-and-deployment.md).  
  
### <a name="to-run-code-when-deployment-steps-are-executed"></a>Para executar código quando etapas de implantação são executadas  
  
1.  Crie uma extensão de item de projeto, uma extensão de projeto ou uma definição de um novo tipo de item de projeto. Para mais informações, consulte os seguintes tópicos:  
  
    -   [Como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)  
  
    -   [Como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md)  
  
    -   [Como: definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)  
  
2.  Na extensão, lidar com o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> e <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> eventos de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> objeto (em uma extensão de item de projeto ou a extensão de projeto) ou um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> objeto (em uma definição de um novo tipo de item de projeto).  
  
3.  No evento manipuladores, use o <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs> e <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepCompletedEventArgs> parâmetros para obter informações sobre a etapa de implantação. Por exemplo, você pode determinar qual etapa de implantação está em execução e se a solução está sendo implantado ou cancelado.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como lidar com o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> e <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> eventos em uma extensão para o item de projeto de instância de lista. Essa extensão grava uma mensagem adicional para o **saída** janela quando o Visual Studio recicla o pool de aplicativos durante a implantação e o cancelamento da solução.  
  
 [!code-vb[SPExtensibility.ProjectSystemExtension.General#4](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handledeploymentstepevents.vb#4)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#4](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handledeploymentstepevents.cs#4)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer referências aos assemblies a seguir:  
  
-   Microsoft.VisualStudio.SharePoint  
  
-   System.ComponentModel.Composition  
  
## <a name="deploy-the-extension"></a>Implantar a extensão  
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de extensão (VSIX) para o assembly e outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também
 [Estender o SharePoint empacotamento e implantação](../sharepoint/extending-sharepoint-packaging-and-deployment.md)   
 [Passo a passo: Criar uma etapa de implantação para projetos do SharePoint](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)   
 [Como: executar o código quando um projeto do SharePoint é implantado ou cancelado](../sharepoint/how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted.md)  
  
  
