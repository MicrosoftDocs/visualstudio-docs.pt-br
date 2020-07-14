---
title: Como tratar conflitos de implantação | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
helpviewer_keywords:
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5df9677fd349825983cc33c5a8ed2648f34b8c9e
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015307"
---
# <a name="how-to-handle-deployment-conflicts"></a>Como tratar conflitos de implantação
  Você pode fornecer seu próprio código para lidar com conflitos de implantação para um item de projeto do SharePoint. Por exemplo, você pode determinar se algum arquivo no item de projeto atual já existe no local de implantação e, em seguida, excluir os arquivos implantados antes de o item de projeto atual ser implantado. Para obter mais informações sobre conflitos de implantação, consulte [estendendo o empacotamento e a implantação do SharePoint](../sharepoint/extending-sharepoint-packaging-and-deployment.md).

### <a name="to-handle-a-deployment-conflict"></a>Para manipular um conflito de implantação

1. Crie uma extensão de item de projeto, uma extensão de projeto ou uma definição de um novo tipo de item de projeto. Para obter mais informações, consulte estes tópicos:

    - [Como: criar uma extensão de item de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-item-extension.md)

    - [Como: criar uma extensão de projeto do SharePoint](../sharepoint/how-to-create-a-sharepoint-project-extension.md)

    - [Como definir um tipo de item de projeto do SharePoint](../sharepoint/how-to-define-a-sharepoint-project-item-type.md)

2. Na extensão, manipule o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> evento de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemType> objeto (em uma extensão de item de projeto ou extensão de projeto) ou um <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeDefinition> objeto (em uma definição de um novo tipo de item de projeto).

3. No manipulador de eventos, determine se há um conflito entre o item de projeto que está sendo implantado e a solução implantada no site do SharePoint, com base nos critérios que se aplicam ao seu cenário. Você pode usar a <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemEventArgs.ProjectItem%2A> Propriedade do parâmetro de argumentos de evento para analisar o item de projeto que está sendo implantado e pode analisar os arquivos no local de implantação chamando um comando do SharePoint que você define para essa finalidade.

     Para muitos tipos de conflitos, você pode primeiro querer determinar qual etapa de implantação está em execução. Você pode fazer isso usando a <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.DeploymentStepInfo%2A> Propriedade do parâmetro argumentos do evento. Embora normalmente faça sentido detectar conflitos durante a <xref:Microsoft.VisualStudio.SharePoint.Deployment.DeploymentStepIds.AddSolution> etapa de implantação interna, você pode verificar se há conflitos durante qualquer etapa de implantação.

4. Se houver um conflito, use o <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> método da <xref:Microsoft.VisualStudio.SharePoint.DeploymentStepStartedEventArgs.Conflicts%2A> propriedade dos argumentos do evento para criar um novo <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> objeto. Esse objeto representa o conflito de implantação. Em sua chamada para o <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflictCollection.Add%2A> método, especifique também o método que é chamado para resolver o conflito.

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra o processo básico para manipular um conflito de implantação em uma extensão de item de projeto para itens de projeto de definição de lista. Para lidar com um conflito de implantação para um tipo diferente de item de projeto, passe uma cadeia de caracteres diferente para o <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> . Para obter mais informações, consulte [estender itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md).

 Para simplificar, o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> manipulador de eventos neste exemplo supõe que exista um conflito de implantação (ou seja, ele sempre adiciona um novo <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> objeto) e o `Resolve` método simplesmente retorna **true** para indicar que o conflito foi resolvido. Em um cenário real, o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.DeploymentStepStarted> manipulador de eventos determinará primeiro se existe um conflito entre um arquivo no item de projeto atual e um arquivo no local de implantação e, em seguida, adicionará um <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentConflict> objeto somente se houver um conflito. Por exemplo, você pode usar a `e.ProjectItem.Files` propriedade no manipulador de eventos para analisar os arquivos no item de projeto e pode chamar um comando do SharePoint para analisar os arquivos no local de implantação. Da mesma forma, em um cenário real, o `Resolve` método pode chamar um comando do SharePoint para resolver o conflito no site do SharePoint. Para obter mais informações sobre como criar comandos do SharePoint, consulte [como: criar um comando do SharePoint](../sharepoint/how-to-create-a-sharepoint-command.md).

 [!code-vb[SPExtensibility.ProjectItemExtension.DeploymentConflict#1](../sharepoint/codesnippet/VisualBasic/deploymentconflict/extension/deploymentconflictextension.vb#1)]
 [!code-csharp[SPExtensibility.ProjectItemExtension.DeploymentConflict#1](../sharepoint/codesnippet/CSharp/deploymentconflict/extension/deploymentconflictextension.cs#1)]

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer referências aos seguintes assemblies:

- Microsoft. VisualStudio. SharePoint

- System. ComponentModel. composição

## <a name="deploy-the-extension"></a>Implantar a extensão
 Para implantar a extensão, crie um [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para o assembly e quaisquer outros arquivos que você deseja distribuir com a extensão. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Estender o empacotamento e a implantação do SharePoint](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
- [Estender itens de projeto do SharePoint](../sharepoint/extending-sharepoint-project-items.md)
- [Como executar código quando as etapas de implantação são executadas](../sharepoint/how-to-run-code-when-deployment-steps-are-executed.md)
- [Como: criar um comando do SharePoint](../sharepoint/how-to-create-a-sharepoint-command.md)
