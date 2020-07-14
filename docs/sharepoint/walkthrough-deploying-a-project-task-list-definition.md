---
title: 'Walkthrough: Implantando uma definição de Lista de Tarefas de projeto | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b5639fe7a1b35dea41b14be3730986ad7c7309b7
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015768"
---
# <a name="walkthrough-deploy-a-project-task-list-definition"></a>Walkthrough: implantar uma definição de lista de tarefas de projeto

Este tutorial mostra como usar o [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] para criar, personalizar, depurar e implantar uma lista do SharePoint para acompanhar as tarefas do projeto.

[!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos

- Edições com suporte do Microsoft Windows e do SharePoint.

- Visual Studio 2017 ou Azure DevOps Services.

## <a name="create-a-sharepoint-list"></a>Criar uma lista do SharePoint

Crie um projeto de lista do SharePoint e associe a definição de lista a tarefas.

1. Abra a caixa de diálogo **novo projeto** , expanda o nó **SharePoint** e escolha o nó **2010** .

2. No painel **modelos** , escolha o modelo de **projeto do SharePoint 2010** , nomeie o projeto **ProjectTaskList**e, em seguida, escolha o botão **OK** .

     O **Assistente para personalização do SharePoint** é exibido.

3. Especifique o site do SharePoint local que você usa para depuração, escolha o botão de opção **implantar como uma solução de farm** e, em seguida, escolha o botão **concluir** .

4. Abra o menu de atalho do projeto e escolha **Adicionar**  >  **novo item**.

5. No painel **modelos** , escolha o modelo de **lista** e, em seguida, escolha o botão **Adicionar** .

     O **Assistente para personalização do SharePoint** é exibido.

6. Na caixa o **nome que você deseja exibir para sua lista?** , insira o **projeto lista de tarefas**.

7. Escolha a **lista criar uma não personalizável com base em um tipo de opção de lista existente** e, em seguida, em sua lista, escolha **tarefas**e, em seguida, escolha o botão **concluir** .

     A lista, o recurso e o pacote aparecem no **Gerenciador de soluções**.

## <a name="add-an-event-receiver"></a>Adicionar um receptor de eventos

Na lista de tarefas, você pode adicionar um receptor de eventos que define automaticamente a data de vencimento e a descrição da tarefa. O procedimento a seguir adiciona um manipulador de eventos simples à instância da lista como um receptor de eventos.

1. Abra o menu de atalho para o nó do projeto, escolha **Adicionar**e, em seguida, escolha **novo item**.

2. Na lista de modelos do SharePoint, escolha o modelo **receptor de eventos** e nomeie-o **ProjectTaskListEventReceiver**.

     O **Assistente para personalização do SharePoint** é exibido.

3. Na página **escolher configurações do receptor de eventos** , escolha **eventos de item de lista** como o receptor de evento, na lista o **tipo de receptor de evento que você deseja** .

4. Na lista o **item que deve ser a origem do evento** , escolha **tarefas**.

5. Na lista de eventos a serem manipulados, marque a caixa de seleção ao lado de **um item foi adicionado**e, em seguida, escolha o botão **concluir** .

     Um novo nó receptor de eventos é adicionado ao projeto com um arquivo de código chamado **ProjectTaskListEventReceiver**.

6. Adicione o código ao `ItemAdded` método no arquivo de código **ProjectTaskListEventReceiver** . Cada vez que uma nova tarefa é adicionada, uma data de vencimento padrão e uma descrição são adicionadas à tarefa. A data de vencimento padrão é 1º de julho de 2009.

     [!code-vb[SPProjectTaskList#1](../sharepoint/codesnippet/VisualBasic/projecttasklist1/projecttasklisteventreceiver/projecttasklisteventreceiver.vb#1)]
     [!code-csharp[SPProjectTaskList#1](../sharepoint/codesnippet/CSharp/projecttasklist/projecttasklisteventreceiver/projecttasklisteventreceiver.cs#1)]

## <a name="customize-the-project-task-list-feature"></a>Personalizar o recurso de lista de tarefas do projeto

Quando você cria uma solução do SharePoint, o Visual Studio cria automaticamente recursos para os itens de projeto padrão. Você pode personalizar as configurações da lista de tarefas do projeto do para o site do SharePoint usando o designer de recursos.

1. Em **Gerenciador de soluções**, expanda **recursos**.

2. Abra o menu de atalho para **Feature1**e escolha **Designer de exibição**.

3. Na caixa **título** , digite **projeto lista de tarefas recurso**.

4. Na lista **escopo** , escolha **Web**.

5. Na janela **Propriedades** , digite **1.0.0.0** como o valor para a propriedade **version** .

## <a name="customize-the-project-task-list-package"></a>Personalizar o pacote da lista de tarefas do projeto

Quando você cria um projeto do SharePoint, o Visual Studio adiciona automaticamente os recursos que contêm os itens de projeto padrão ao pacote. Você pode personalizar as configurações da lista de tarefas do projeto para o site do SharePoint usando o designer de pacotes.

1. No **SolutionExplorer**, abra o menu de atalho para **pacote**e escolha **Designer de exibição**.

2. Na caixa **nome** , digite **ProjectTaskListPackage**.

3. Marque a caixa de seleção **Redefinir servidor Web** .

## <a name="build-and-test-the-project-task-list"></a>Criar e testar a lista de tarefas do projeto

Quando você executa o projeto, o site do SharePoint é aberto. No entanto, você deve navegar manualmente até o local da lista de tarefas.

1. Escolha a tecla **F5** para criar e implantar a lista de tarefas do projeto.

     O site do SharePoint é aberto.

2. Escolha a guia **página inicial** .

3. Na barra lateral esquerda, escolha o link **lista de tarefas do projeto** .

     A página Lista de Tarefas do projeto é exibida.

4. Na guia **ferramentas de lista** , escolha a guia **itens** .

5. No grupo **itens** , escolha o botão **novo item** .

6. Na caixa de texto **título** , digite **Task1**.

7. Escolha o botão **salvar** .

     Depois que o site for atualizado, a tarefa **Task1** aparecerá com uma data de conclusão de 7/1/2009.

8. Escolha **Task1**.

     A exibição detalhada da tarefa é exibida e a descrição mostra "esta é uma tarefa crítica".

## <a name="deploy-the-project-task-list"></a>Implantar a lista de tarefas do projeto

Depois de criar e testar a lista de tarefas do projeto, você pode implantá-la no *sistema local* ou em um *sistema remoto*. O sistema local é o mesmo computador em que você desenvolveu a solução, enquanto que um sistema remoto é um computador diferente.

### <a name="to-deploy-the-project-task-list-to-the-local-system"></a>Para implantar a lista de tarefas do projeto no sistema local

Na barra de menus do Visual Studio, escolha **Compilar**  >  **implantar solução**.

O Visual Studio recicla o pool de aplicativos do IIS, cancela todas as versões existentes da solução, copia o arquivo de pacote de solução (*. wsp*) no SharePoint e ativa seus recursos. Agora você pode usar a solução no SharePoint. Para obter mais informações sobre as etapas de configuração de implantação, consulte [como editar uma configuração de implantação do SharePoint](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md).

### <a name="to-deploy-the-project-task-list-to-a-remote-system"></a>Para implantar a lista de tarefas do projeto em um sistema remoto

1. Na barra de menus do Visual Studio, escolha **Compilar**  >  **publicar**.

2. Na caixa de diálogo **publicar** , escolha o botão de opção **publicar no sistema de arquivos** .

     Você pode alterar o local de destino na caixa de diálogo **publicar** escolhendo o ![ícone](../sharepoint/media/ellipsisicon.gif "Ícone de reticências") de reticências do botão de reticências e, em seguida, navegando para outro local.

3. Escolha o botão **Publicar**.

     Um arquivo *. wsp* é criado para a solução.

4. Copie o arquivo *. wsp* para o sistema remoto do SharePoint.

5. Use o comando do PowerShell `Add-SPUserSolution` para instalar o pacote na instalação remota do SharePoint. (Para soluções de farm, use o `Add-SPSolution` comando.)

     Por exemplo, `Add-SPUserSolution C:\MyProjects\ProjectTaskList\ProjectTaskList\bin\Debug\ProjectTaskList.wsp`.

6. Use o comando do PowerShell `Install-SPUserSolution` para implantar a solução. (Para soluções de farm, use o `Install-SPSolution` comando.)

     Por exemplo, `Install-SPUserSolution -Identity ProjectTaskList.wsp -Site http://NewSiteName`.

     Para obter mais informações sobre a implantação remota, consulte [usando soluções](/previous-versions/office/developer/sharepoint-2010/ee534972(v=office.14)) e [adicionando e implantando soluções com o PowerShell no SharePoint 2010](http://www.dotnetmafia.com/blogs/dotnettipoftheday/archive/2009/12/02/adding-and-deploying-solutions-with-powershell-in-sharepoint-2010.aspx).

## <a name="next-steps"></a>Próximas etapas

Você pode aprender mais sobre como personalizar e implantar soluções do SharePoint dos seguintes tópicos:

- [Walkthrough: criar uma coluna de site, um tipo de conteúdo e uma lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)

- [Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)

- [Windows PowerShell para SharePoint Server 2010](/powershell/module/sharepoint-server)

## <a name="see-also"></a>Consulte também
[Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
