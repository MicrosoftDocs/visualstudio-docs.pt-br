---
title: Como executar código quando as etapas de implantação são executadas | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b2b0431ab4f985d801a78159fc2d324a29f8b638
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015525"
---
# <a name="how-to-run-code-when-deployment-steps-are-executed"></a>Como executar código quando as etapas de implantação são executadas
  Se você quiser executar tarefas adicionais para uma etapa de implantação em um projeto do SharePoint, poderá manipular eventos que são gerados por itens de projeto do SharePoint antes e depois que o Visual Studio executa cada etapa de implantação. Para obter mais informações, consulte [estendendo a implantação e empacotamento do SharePoint](../sharepoint/extending-sharepoint-packaging-and-deployment.md).

### <a name="to-run-code-when-deployment-steps-are-executed"></a>Para executar o código quando as etapas de implantação são executadas

1. Crie uma extensão de item de projeto, uma extensão de projeto ou uma definição de um novo tipo de item de projeto. Para obter mais informações, consulte estes tópicos:

    - [Como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [Como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [Como definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. Na extensão, manipule os <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> eventos e <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> objeto (em uma extensão de item de projeto ou extensão de projeto) ou um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> objeto (em uma definição de um novo tipo de item de projeto).

3. Nos manipuladores de eventos, use os <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs> <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepCompletedEventArgs> parâmetros e para obter informações sobre a etapa de implantação. Por exemplo, você pode determinar qual etapa de implantação está em execução e se a solução está sendo implantada ou cancelada.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como manipular <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> os <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepCompleted> eventos e em uma extensão para o item de projeto de instância de lista. Essa extensão grava uma mensagem adicional na janela de **saída** quando o Visual Studio recicla o pool de aplicativos enquanto implanta e cancela a solução.

 [!code-vb[SPExtensibility.ProjectSystemExtension.General#4](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handledeploymentstepevents.vb#4)]
 [!code-csharp[SPExtensibility.ProjectSystemExtension.General#4](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handledeploymentstepevents.cs#4)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer referências aos seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Estender o empacotamento e a implantação do SharePoint](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [Walkthrough: criar uma etapa de implantação personalizada para projetos do SharePoint](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)
- [Como executar código quando um projeto do SharePoint é implantado ou retraído](../sharepoint/how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted.md)
