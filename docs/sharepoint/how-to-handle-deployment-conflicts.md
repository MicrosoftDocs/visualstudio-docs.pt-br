---
title: 'Como: manipular conflitos de implantação | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: d7c30a7c634c30c9fe3e92ef988d7d8fc043cf6b
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118461"
---
# <a name="how-to-handle-deployment-conflicts"></a>Como: manipular conflitos de implantação
  Você pode fornecer seu próprio código para lidar com conflitos de implantação para um item de projeto do SharePoint. Por exemplo, você pode determinar se todos os arquivos no item de projeto atual já existem no local de implantação e, em seguida, excluir os arquivos implantados antes que o item de projeto atual seja implantado. Para obter mais informações sobre conflitos de implantação, consulte [estendendo SharePoint empacotamento e implantação](../sharepoint/extending-sharepoint-packaging-and-deployment.md).  
  
### <a name="to-handle-a-deployment-conflict"></a>Para lidar com um conflito de implantação  
  
1.  Crie uma extensão de item de projeto, uma extensão de projeto ou uma definição de um novo tipo de item de projeto. Para mais informações, consulte os seguintes tópicos:  
  
    -   [Como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)  
  
    -   [Como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md)  
  
    -   [Como: definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)  
  
2.  Na extensão, lidar com o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> eventos de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> objeto (em uma extensão de item de projeto ou a extensão de projeto) ou um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> objeto (em uma definição de um novo tipo de item de projeto).  
  
3.  No manipulador de eventos, determine se há um conflito entre o item de projeto que está sendo implantado e a solução implantada no site do SharePoint, com base nos critérios que se aplicam ao seu cenário. Você pode usar o <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemEventArgs.ProjectItem%2A> propriedade do parâmetro de argumentos de evento para analisar o item de projeto que está sendo implantado e você pode analisar os arquivos no local de implantação ao chamar um comando do SharePoint que você define para essa finalidade.  
  
     Para muitos tipos de conflitos, primeiro convém determinar qual etapa de implantação está em execução. Você pode fazer isso usando o <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.DeploymentStepInfo%2A> propriedade do parâmetro de argumentos de evento. Embora geralmente faz sentido para detectar conflitos durante o interno <xref:Microsoft.VisualStudio.SharePoint.Deployment.DeploymentStepIds.AddSolution> etapa de implantação, você pode verificar conflitos durante qualquer etapa de implantação.  
  
4.  Se houver um conflito, use o <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> método da <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.Conflicts%2A> propriedade dos argumentos do evento para criar um novo <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> objeto. Este objeto representa o conflito de implantação. Em sua chamada para o <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> método, especifique também o método que é chamado para resolver o conflito.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra o processo básico para lidar com um conflito de implantação em uma extensão de item de projeto para itens de projeto de definição de lista. Para lidar com um conflito de implantação para um tipo diferente de item de projeto, passe uma cadeia de caracteres diferente para o <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute>. Para obter mais informações, consulte [itens de projeto do SharePoint estender](../sharepoint/extending-sharepoint-project-items.md).  
  
 Para simplificar, o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> manipulador de eventos neste exemplo pressupõe que existe um conflito de implantação (ou seja, ele sempre adiciona um novo <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> objeto) e o `Resolve` método simplesmente retorna **true** para indicar que o conflito foi resolvido. Em um cenário real, sua <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> manipulador de eventos seria determinar primeiro se houver um conflito entre um arquivo no item de projeto atual e um arquivo no local de implantação e, em seguida, adicione um <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> objeto apenas se houver um conflito. Por exemplo, você pode usar o `e.ProjectItem.Files` propriedade no manipulador de eventos para analisar os arquivos no item de projeto e você pode chamar um comando do SharePoint para analisar os arquivos no local de implantação. Da mesma forma, em um cenário real de `Resolve` método pode chamar um comando do SharePoint para resolver o conflito no site do SharePoint. Para obter mais informações sobre como criar comandos do SharePoint, consulte [como: criar um comando do SharePoint](../sharepoint/how-to-create-a-sharepoint-command.md).  
  
 [!code-vb[SPExtensibility.ProjectItemExtension.DeploymentConflict#1](../sharepoint/codesnippet/VisualBasic/deploymentconflict/extension/deploymentconflictextension.vb#1)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.DeploymentConflict#1](../sharepoint/codesnippet/CSharp/deploymentconflict/extension/deploymentconflictextension.cs#1)]  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer referências aos assemblies a seguir:  
  
-   Microsoft.VisualStudio.SharePoint  
  
-   System.ComponentModel.Composition  
  
## <a name="deploy-the-extension"></a>Implantar a extensão  
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de extensão (VSIX) para o assembly e outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="see-also"></a>Consulte também
 [Estender o SharePoint empacotamento e implantação](../sharepoint/extending-sharepoint-packaging-and-deployment.md)   
 [Estender os itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md)   
 [Como: executar o código quando etapas de implantação são executadas](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)   
 [Como: criar um comando do SharePoint](../sharepoint/how-to-create-a-sharepoint-command.md)  
  
