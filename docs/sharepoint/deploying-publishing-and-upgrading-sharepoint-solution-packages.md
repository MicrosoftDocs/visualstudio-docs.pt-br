---
title: Implantando, publicando e atualizando pacotes de soluções do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SharePointProjectPropertyTab
- VS.SharePointTools.Project.Publishing
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- deploying [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, deploying
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 17578fbfb58d354f06e91c78f067d228b92860fe
ms.sourcegitcommit: e6b13898cfbd89449f786c2e8f3e3e7377afcf25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/22/2018
ms.locfileid: "36327197"
---
# <a name="deploy-publish-and-upgrade-sharepoint-solution-packages"></a>Implantar, publicar e atualizar pacotes de solução do SharePoint
  Depois de desenvolver uma solução do SharePoint no Visual Studio, você pode implantar o seu arquivo de pacote (. wsp) em um servidor SharePoint local ou publicá-lo em um servidor do SharePoint local ou remoto. Se você implantar os arquivos, você pode personalizar como os arquivos de pacote (. wsp) são implantados.  
  
> [!NOTE]  
>  Atualmente, apenas soluções em área restrita podem ser publicadas em servidores remotos do SharePoint. Para obter mais informações, consulte [considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).  
  
## <a name="deploy-publish-and-upgrade"></a>Implantar, publicar e atualizar
 *Implantando* refere-se à cópia de um arquivo de solução do SharePoint criado a partir de um projeto do SharePoint no Visual Studio para um host local. Em uma solução implantada, você pode configurar as etapas de implantação, como Reciclando o pool de serviços de informações da Internet (IIS), ativando a solução após a implantação e assim por diante. Para implantar, usar o **Deploy** comando o **Build** menu. Para obter mais informações, consulte [como: editar uma configuração de implantação do SharePoint](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md) e [como: implantar e publicar uma solução do SharePoint em um site do SharePoint Local](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md).  
  
 *Publicando* refere-se ao carregamento de um arquivo de solução em área restrita do SharePoint para SharePoint remoto site; ou seja, um site localizado em outro sistema. Você também pode publicar um arquivo de solução de área restrita do SharePoint para um site do SharePoint local, mas, independentemente se o site publicado é local ou remoto, você não pode configurar suas etapas de implantação.  
  
 *Atualizando* refere-se para atualizar uma existente remotamente ou localmente publicada solução do SharePoint. Depois que todas as alterações são feitas para a solução do SharePoint no Visual Studio, você alterar o nome de arquivo do pacote da solução, republicar a solução e, em seguida, atualize a solução depois que ele republica com êxito. Se você publicar novamente uma solução publicada localmente, você pode substituir o arquivo de solução existentes.  
  
## <a name="deploy-packages"></a>Implantar pacotes
 Você pode implantar os arquivos de pacote para o servidor do SharePoint no computador de desenvolvimento para teste e depuração. Você também pode criar um arquivo de pacote que você pode instalar em outro computador, escolhendo o **publicar no sistema de arquivos** botão de opção a **publicar** caixa de diálogo. O pacote é criado e copiado para o caminho de arquivo local especificado. Para implantar uma solução do SharePoint no servidor local, use o **Deploy** comando o **Build** menu. Para obter mais informações, consulte [como: implantar e publicar uma solução do SharePoint em um site do SharePoint local](../sharepoint/how-to-deploy-and-publish-a-sharepoint-solution-to-a-local-sharepoint-site.md).  
  
 Para saber como implantar uma definição de lista, adicione um receptor de eventos e usar o Designer de pacote e o Designer de recursos, consulte [instruções passo a passo: implantar uma definição de lista de tarefas de projeto](../sharepoint/walkthrough-deploying-a-project-task-list-definition.md).  
  
## <a name="customize-the-deployment-process"></a>Personalizar o processo de implantação
 A tabela a seguir mostra as duas configurações de implantação que você pode usar ao depurar e implantar uma solução do SharePoint.  
  
|Configuração de implantação|Descrição|  
|------------------------------|-----------------|  
|Padrão|A configuração de implantação padrão. As seguintes etapas de implantação são executadas:<br /><br /> 1.  Execute o comando de pré-implantação.<br />2.  Recicle pool de aplicativos do IIS.<br />3.  Cancele a solução.<br />4.  Adicione a solução.<br />5.  Ative recursos.<br />6.  Execute o comando de pós-implantação.<br /><br /> Quando um pacote é desinstalado, as seguintes etapas de cancelamento são executadas.<br /><br /> 1.  Recicle pool de aplicativos do IIS.<br />2.  Cancele a solução.|  
|Nenhuma ativação|Essa configuração de implantação executa as mesmas etapas como a configuração padrão, mas ignora a etapa de ativação.|  
  
 Você pode criar suas próprias configurações de implantação para concluir uma única etapa ou alterar a ordem das etapas no processo de implantação. Para obter mais informações, consulte [como: editar uma configuração de implantação do SharePoint](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md).  

 Você também pode adicionar comandos a serem executados antes e após a implantação. Para obter mais informações, consulte [como: comandos de implantação do SharePoint definir](../sharepoint/how-to-set-sharepoint-deployment-commands.md).  
  
## <a name="publish-packages-to-a-remote-or-local-server"></a>Publicar pacotes em um servidor local ou remoto
 Para publicar uma solução em área restrita do SharePoint em um servidor remoto, na barra de menus, escolha **construir**, **Publish**e, em seguida, no **publicar** caixa de diálogo, escolha o **Publicar no Site do SharePoint** botão de opção, fornecendo a URL do servidor remoto, como **https://someremoteserver.sharepoint.microsoftonline.com**.  
  
 Para publicar uma solução do SharePoint em um servidor local, no **Publish** caixa de diálogo, escolha o **publicar no sistema de arquivos** botão de opção, fornecendo um caminho de sistema local.  
  
 Depois que uma solução com êxito publica no SharePoint, a solução aparece na **Galeria de soluções** onde você pode ativá-la. Para obter mais informações, consulte [como: implantar, publicar e atualizar soluções do SharePoint em um servidor remoto](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md).  
  
### <a name="upgrade-published-packages"></a>Atualizar pacotes publicados
 Se você fizer alterações para um projeto do SharePoint no Visual Studio depois que ela é publicada, o pacote publicado deve ser atualizado para incluir as alterações. Para atualizar com êxito, um pacote deve ter um nome exclusivo. Se um pacote com o mesmo nome é encontrado no site do SharePoint, que pode ocorrer quando você estiver atualizando um aplicativo existente – os alertas de um erro você ao nome do arquivo em conflito e permite que você renomeie o pacote. Após seja republicado, o novo pacote é exibido no site do SharePoint e pode ser atualizado. Um pacote atualizado atualiza a solução usando os dados do pacote mais antigo e, em seguida, ativa a solução no SharePoint. Para obter mais informações, consulte [como: implantar, publicar e atualizar soluções do SharePoint em um servidor remoto](../sharepoint/how-to-deploy-publish-and-upgrade-sharepoint-solutions-on-a-remote-server.md).  
  
## <a name="see-also"></a>Consulte também
 [Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)  
  
