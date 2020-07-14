---
title: Como executar um comando do SharePoint | Microsoft Docs
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], executing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 789b77f3161b5fe566ea033060e8cab16cbaecc7
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016985"
---
# <a name="how-to-execute-a-sharepoint-command"></a>Como executar um comando do SharePoint
  Se você quiser usar o modelo de objeto de servidor em uma extensão de ferramentas do SharePoint, deverá criar um *comando do SharePoint* personalizado para chamar a API. Depois de definir o comando e implantá-lo com a extensão de ferramentas do SharePoint, sua extensão poderá executar o comando para chamar o modelo de objeto do SharePoint Server. Para executar o comando, use um dos métodos ExecuteCommand de um <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> objeto.

 Para obter mais informações sobre a finalidade dos comandos do SharePoint, consulte [chamar os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).

### <a name="to-execute-a-sharepoint-command"></a>Para executar um comando do SharePoint

1. Em sua extensão de ferramentas do SharePoint, obtenha um <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> objeto. A maneira como você obtém um <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> objeto depende do tipo de extensão que está criando:

    - Em uma extensão do sistema de projeto do SharePoint, use a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.SharePointConnection%2A> propriedade.

         Para obter mais informações sobre extensões de sistema de projeto, consulte [estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md).

    - Em uma extensão do nó **conexões do SharePoint** no **Gerenciador de servidores**, use a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext.SharePointConnection%2A> propriedade. Para obter um <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext> objeto, use a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.Context%2A> propriedade.

         Para obter mais informações sobre extensões de **Gerenciador de servidores** , consulte [estender o nó conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).

    - No código que não faz parte de uma extensão das ferramentas do SharePoint, como um assistente de modelo de projeto, use a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.SharePointConnection%2A> propriedade.

         Para obter mais informações sobre como recuperar o serviço de projeto, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).

2. Chame um dos métodos ExecuteCommand do <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> objeto. Passe o nome do comando que você deseja executar para o primeiro argumento do método ExecuteCommand. Se o comando tiver um parâmetro personalizado, passe esse parâmetro para o segundo argumento do método ExecuteCommand.

     Há uma sobrecarga ExecuteCommand diferente para cada assinatura de comando com suporte. A tabela a seguir lista as assinaturas com suporte e qual sobrecarga usar para cada assinatura.

    |Assinatura de comando|Sobrecarga de ExecuteCommand a ser usada|
    |-----------------------|------------------------------------|
    |O comando tem apenas o <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> parâmetro padrão e nenhum valor de retorno.|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |O comando tem apenas o <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> parâmetro padrão e um valor de retorno.|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |O comando tem dois parâmetros (o <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> parâmetro padrão e um parâmetro personalizado) e nenhum valor de retorno.|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|
    |O comando tem dois parâmetros e um valor de retorno.|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra como usar a <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> sobrecarga para chamar o `Contoso.Commands.UpgradeSolution` comando descrito em [como criar um comando do SharePoint](../sharepoint/how-to-create-a-sharepoint-command.md).

 [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#6](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs#6)]
 [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#6](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb#6)]

 O `Execute` método mostrado neste exemplo é uma implementação do <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep.Execute%2A> método da <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> interface em uma etapa de implantação personalizada. Para ver esse código no contexto de um exemplo maior, consulte [Walkthrough: criar uma etapa de implantação personalizada para projetos do SharePoint](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md).

 Observe os seguintes detalhes sobre a chamada para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> método:

- O primeiro parâmetro identifica o comando que você deseja chamar. Essa cadeia de caracteres corresponde ao valor que você passa para o <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> na definição do comando.

- O segundo parâmetro é o valor que você deseja passar para o segundo parâmetro personalizado do comando. Nesse caso, é o caminho completo do arquivo *. wsp* que está sendo atualizado para o site do SharePoint.

- O código não passa o parâmetro implícito <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> para o comando. Esse parâmetro é passado para o comando automaticamente quando você chama o comando de uma extensão do sistema de projeto do SharePoint ou de uma extensão do nó **conexões do SharePoint** no **Gerenciador de servidores**. Em outros tipos de soluções, como em um assistente de modelo de projeto que implementa a <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface, esse parâmetro é **NULL**.

## <a name="compile-the-code"></a>Compilar o código
 Este exemplo requer uma referência ao assembly Microsoft. VisualStudio. SharePoint.

## <a name="see-also"></a>Consulte também
- [Chamar para os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [Como: criar um comando do SharePoint](../sharepoint/how-to-create-a-sharepoint-command.md)
- [Walkthrough: estender Gerenciador de Servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
