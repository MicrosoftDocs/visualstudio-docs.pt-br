---
title: Executar o código quando o projeto do SharePoint for implantado ou retraído
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
ms.openlocfilehash: 5bd60c9d7b30d4620630d1f6752bd4c7e8bf1182
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016068"
---
# <a name="how-to-run-code-when-a-sharepoint-project-is-deployed-or-retracted"></a>Como executar código quando um projeto do SharePoint é implantado ou retraído
  Se você quiser executar tarefas adicionais quando um projeto do SharePoint for implantado ou retraído, poderá manipular eventos gerados pelo Visual Studio. Para obter mais informações, consulte [estender o empacotamento e a implantação do SharePoint](../sharepoint/extending-sharepoint-packaging-and-deployment.md).

### <a name="to-run-code-when-a-sharepoint-project-is-deployed-or-retracted"></a>Para executar o código quando um projeto do SharePoint é implantado ou retraído

1. Crie uma extensão de item de projeto, uma extensão de projeto ou uma definição de um novo tipo de item de projeto. Para obter mais informações, consulte estes tópicos:

   - [Como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

   - [Como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

   - [Como definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. Na extensão, acesse o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService> objeto. Para obter mais informações, consulte [como recuperar o serviço de projeto do SharePoint](../sharepoint/how-to-retrieve-the-sharepoint-project-service.md).

3. Manipule os <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentStarted> <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentCompleted> eventos e do serviço de projeto.

4. Nos manipuladores de eventos, use o <xref:Microsoft.VisualStudio.SharePoint.DeploymentEventArgs> parâmetro para obter informações sobre a sessão de implantação atual. Por exemplo, você pode determinar qual projeto está na sessão de implantação atual e se ele está sendo implantado ou cancelado.

   O exemplo de código a seguir demonstra como manipular <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentStarted> os <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectEvents.DeploymentCompleted> eventos e em uma extensão de projeto. Essa extensão grava uma mensagem adicional na janela de **saída** quando a implantação é iniciada e concluída para um projeto do SharePoint.

   [!code-csharp[SPExtensibility.ProjectSystemExtension.General#12](../sharepoint/codesnippet/CSharp/projectsystemexamples/extension/handleprojectdeploymentevents.cs#12)]
   [!code-vb[SPExtensibility.ProjectSystemExtension.General#12](../sharepoint/codesnippet/VisualBasic/projectsystemexamples/extension/handleprojectdeploymentevents.vb#12)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer referências aos seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Estender o empacotamento e a implantação do SharePoint](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [Como executar código quando as etapas de implantação são executadas](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
