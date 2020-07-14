---
title: 'Como: criar um comando do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 15ea7ff86e90bf7a474f9d64c30a9803e3e20bf5
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016217"
---
# <a name="how-to-create-a-sharepoint-command"></a>Como: criar um comando do SharePoint
  Se você quiser usar o modelo de objeto de servidor em uma extensão de ferramentas do SharePoint, deverá criar um *comando do SharePoint* personalizado para chamar a API. Você define o comando do SharePoint em um assembly que pode chamar diretamente o modelo de objeto de servidor.

 Para obter mais informações sobre a finalidade dos comandos do SharePoint, consulte [chamar os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).

### <a name="to-create-a-sharepoint-command"></a>Para criar um comando do SharePoint

1. Crie um projeto de biblioteca de classes que tenha a seguinte configuração:

    - Tem como alvo o .NET Framework 3,5. Para obter mais informações sobre como selecionar a estrutura de destino, consulte [como: direcionar uma versão do .NET Framework](../ide/visual-studio-multi-targeting-overview.md).

    - Tem como alvo a plataforma AnyCPU ou x64. Por padrão, a plataforma de destino para projetos de biblioteca de classes é AnyCPU. Para obter mais informações sobre como selecionar a plataforma de destino, consulte [como: configurar projetos para plataformas de destino](../ide/how-to-configure-projects-to-target-platforms.md).

    > [!NOTE]
    > Você não pode implementar um comando do SharePoint no mesmo projeto que define uma extensão de ferramentas do SharePoint, pois os comandos do SharePoint visam o .NET Framework 3,5 e as extensões de ferramentas do SharePoint têm como destino o [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)] . Você deve definir os comandos do SharePoint que são usados por sua extensão em um projeto separado. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

2. Adicione referências aos assemblies a seguir:

    - Microsoft. VisualStudio. SharePoint. Commands

    - Microsoft. SharePoint

3. Em uma classe no projeto, crie um método que define o comando do SharePoint. O método deve estar de acordo com as seguintes diretrizes:

    - Ele pode ter um ou dois parâmetros.

         O primeiro parâmetro deve ser um <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> objeto. Esse objeto fornece o Microsoft. SharePoint. SPSite ou o Microsoft. SharePoint. SPWeb no qual o comando é executado. Ele também fornece um <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandLogger> objeto que pode ser usado para gravar mensagens na janela de **saída** ou na janela de **lista de erros** no Visual Studio.

         O segundo parâmetro pode ser um tipo de sua escolha, mas esse parâmetro é opcional. Você pode adicionar esse parâmetro ao comando do SharePoint se precisar passar dados de sua extensão de ferramentas do SharePoint para o comando.

    - Ele pode ter um valor de retorno, mas isso é opcional.

    - O segundo parâmetro e o valor de retorno devem ser um tipo que possa ser serializado pelo Windows Communication Foundation (WCF). Para obter mais informações, consulte [tipos com suporte no serializador de contrato de dados](/dotnet/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer) e [usando a classe XmlSerializer](/dotnet/framework/wcf/feature-details/using-the-xmlserializer-class).

    - O método pode ter qualquer visibilidade (**pública**, **interna**ou **privada**) e pode ser estático ou não estático.

4. Aplique o <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> ao método. Este atributo especifica um identificador exclusivo para o comando; Esse identificador não precisa corresponder ao nome do método.

     Você deve especificar o mesmo identificador exclusivo ao chamar o comando de sua extensão de ferramentas do SharePoint. Para obter mais informações, consulte [como executar um comando do SharePoint](../sharepoint/how-to-execute-a-sharepoint-command.md).

## <a name="example"></a>Exemplo
 O exemplo de código a seguir demonstra um comando do SharePoint que tem o identificador `Contoso.Commands.UpgradeSolution` . Esse comando usa APIs no modelo de objeto de servidor para atualizar para uma solução implantada.

 [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#5](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs#5)]
 [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#5](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb#5)]

 Além do primeiro <xref:Microsoft.VisualStudio.SharePoint.Commands.ISharePointCommandContext> parâmetro implícito, esse comando também tem um parâmetro de cadeia de caracteres personalizado que contém o caminho completo do arquivo. wsp que está sendo atualizado para o site do SharePoint. Para ver esse código no contexto de um exemplo maior, consulte [Walkthrough: criar uma etapa de implantação personalizada para projetos do SharePoint](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md).

## <a name="compiling-the-code"></a>Compilando o código
 Este exemplo requer referências aos seguintes assemblies:

- Microsoft. VisualStudio. SharePoint. Commands

- Microsoft. SharePoint

## <a name="deploying-the-command"></a>Implantando o comando
 Para implantar o comando, inclua o assembly de comando no mesmo [!include[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote do*VSIX*(a mesma extensão) com o assembly de extensão que usa o comando. Você também deve adicionar uma entrada para o assembly de comando no arquivo extension. vsixmanifest. Para obter mais informações, consulte [implantar extensões para as ferramentas do SharePoint no Visual Studio](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md).

## <a name="see-also"></a>Consulte também
- [Chamar para os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [Como executar um comando do SharePoint](../sharepoint/how-to-execute-a-sharepoint-command.md)
- [Walkthrough: estender Gerenciador de Servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
