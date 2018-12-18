---
title: 'Como: executar um comando do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], executing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: ce195dd34c7c0b509f9de4cbe2cfd14d9a477f87
ms.sourcegitcommit: d9e4ea95d0ea70827de281754067309a517205a1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37118542"
---
# <a name="how-to-execute-a-sharepoint-command"></a>Como: executar um comando do SharePoint
  Se você quiser usar o modelo de objeto de servidor em uma extensão de ferramentas do SharePoint, você deve criar um personalizado *comando do SharePoint* para chamar a API. Depois de definir o comando e implantá-lo com sua extensão de ferramentas do SharePoint, sua extensão pode executar o comando para chamar o modelo de objeto de servidor do SharePoint. Para executar o comando, use um dos métodos de ExecuteCommand um <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> objeto.  
  
 Para obter mais informações sobre a finalidade dos comandos do SharePoint, consulte [chamam os modelos de objeto SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).  
  
### <a name="to-execute-a-sharepoint-command"></a>Para executar um comando do SharePoint  
  
1.  Em sua extensão de ferramentas do SharePoint, obtenha um <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> objeto. A maneira que você obtenha um <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> objeto depende do tipo de extensão que você está criando:  
  
    -   Em uma extensão do sistema de projeto do SharePoint, use o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProject.SharePointConnection%2A> propriedade.  
  
         Para obter mais informações sobre as extensões de sistema do projeto, consulte [estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md).  
  
    -   Em uma extensão do **conexões do SharePoint** nó no **Gerenciador de servidores**, use o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext.SharePointConnection%2A> propriedade. Para obter um <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeContext> do objeto, use o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNode.Context%2A> propriedade.  
  
         Para obter mais informações sobre **Gerenciador de servidores** extensões, consulte [estender o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md).  
  
    -   No código que não faz parte de uma extensão das ferramentas do SharePoint, como um Assistente de modelo de projeto, use o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectService.SharePointConnection%2A> propriedade.  
  
         Para obter mais informações sobre como recuperar o serviço de projeto, consulte [usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md).  
  
2.  Chame um dos métodos de ExecuteCommand a <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection> objeto. Passe o nome do comando que você deseja executar ao primeiro argumento do método ExecuteCommand. Se seu comando tiver um parâmetro personalizado, passe esse parâmetro para o segundo argumento do método ExecuteCommand.  
  
     Há uma sobrecarga de ExecuteCommand diferente para cada assinatura de comando com suporte. A tabela a seguir lista as assinaturas com suporte e qual sobrecarregar a ser usado para cada assinatura.  
  
    |Assinatura de comando|Sobrecarga de ExecuteCommand usar|  
    |-----------------------|------------------------------------|  
    |O comando tem apenas o padrão <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> parâmetro e nenhum valor de retorno.|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|  
    |O comando tem apenas o padrão <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> parâmetro e um valor de retorno.|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|  
    |O comando tem dois parâmetros (o padrão <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> parâmetro e um parâmetro personalizado) e nenhum valor de retorno.|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|  
    |O comando tem dois parâmetros e um valor de retorno.|<xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A>|  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir demonstra como usar o <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> sobrecarga para chamar o `Contoso.Commands.UpgradeSolution` comando que é descrito em [como: criar um comando do SharePoint](../sharepoint/how-to-create-a-sharepoint-command.md).  
  
 [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#6](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs#6)]
 [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#6](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb#6)]  
  
 O `Execute` método mostrado neste exemplo é uma implementação do <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep.Execute%2A> método o <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> interface em uma etapa de implantação personalizada. Para ver esse código no contexto de um exemplo maior, consulte [instruções passo a passo: criar uma etapa de implantação para projetos do SharePoint](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md).  
  
 Observe os seguintes detalhes sobre a chamada para o <xref:Microsoft.VisualStudio.SharePoint.ISharePointConnection.ExecuteCommand%2A> método:  
  
-   O primeiro parâmetro identifica o comando que você deseja chamar. Essa cadeia de caracteres corresponde ao valor que você passa para o <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> na definição de comando.  
  
-   O segundo parâmetro é o valor que você deseja passar para o segundo parâmetro personalizado do comando. Nesse caso, é o caminho completo do *. wsp* arquivo que está sendo atualizado para o site do SharePoint.  
  
-   O código não passar implícito <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> parâmetro ao comando. Esse parâmetro é passado para o comando automaticamente quando você chama o comando de uma extensão do sistema de projeto do SharePoint ou uma extensão do **conexões do SharePoint** nó no **Server Explorer**. Em outros tipos de soluções, como em um Assistente de modelo de projeto que implementa o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface, esse parâmetro é **nulo**.  
  
## <a name="compile-the-code"></a>Compilar o código  
 Este exemplo requer uma referência ao assembly Microsoft.VisualStudio.SharePoint.  
  
## <a name="see-also"></a>Consulte também
 [Chamar os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md)   
 [Como: criar um comando do SharePoint](../sharepoint/how-to-create-a-sharepoint-command.md)   
 [Passo a passo: Estenda o Gerenciador de servidores para exibir web parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)  
  
