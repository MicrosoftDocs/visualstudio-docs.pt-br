---
title: 'Passo a passo: Implantando uma definição de lista de tarefas do projeto | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 0e0a0338f14ecdea36c5a5678a42a76ae234bb6d
ms.sourcegitcommit: 1ab675a872848c81a44d6b4bd3a49958fe673c56
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44280357"
---
# <a name="walkthrough-deploy-a-project-task-list-definition"></a>Passo a passo: Implantar uma definição de lista de tarefas de projeto

Este passo a passo mostra como usar [!INCLUDE[vs_dev11_long](../sharepoint/includes/vs-dev11-long-md.md)] para criar, personalizar, depurar e implantar uma lista do SharePoint para controlar tarefas do projeto.

[!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos

- Edições com suporte do Microsoft Windows e do SharePoint.

- Visual Studio 2017 ou serviços de DevOps do Azure.

## <a name="create-a-sharepoint-list"></a>Criar uma lista do SharePoint

Crie um projeto de lista do SharePoint e associar a definição de lista de tarefas.

1. Abra o **novo projeto** diálogo caixa, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.

2. No **modelos** painel, escolha o **o projeto do SharePoint 2010** modelo, nomeie o projeto **ProjectTaskList**e, em seguida, escolha o **Okey**botão.

     O **Assistente para personalização do SharePoint** é exibida.

3. Especifique o site local do SharePoint que você pode usar para depuração, escolha o **implantar como uma solução de farm** botão de opção e, em seguida, escolha o **concluir** botão.

4. Abra o menu de atalho para o projeto e, em seguida, escolha **Add** > **Novo Item**.

5. No **modelos** painel, escolha o **lista** modelo e, em seguida, escolha o **Add** botão.

     O **Assistente para personalização do SharePoint** é exibida.

6. No **que nome você deseja exibir para sua lista?** , digite **lista de tarefas do projeto**.

7. Escolha o **criar uma lista não personalizável com base em um tipo de lista existente de** botão de opção e, em seguida, na lista, escolha **tarefas**e, em seguida, escolha o **concluir** botão.

     A lista, recurso e pacote aparecem no **Gerenciador de soluções**.

## <a name="add-an-event-receiver"></a>Adicionar um receptor de eventos

Na lista de tarefas, você pode adicionar um receptor de eventos que define automaticamente o vencimento Data e a descrição da tarefa. O procedimento a seguir adiciona um manipulador de eventos simples para a instância de lista como um receptor de eventos.

1. Abra o menu de atalho do nó do projeto, escolha **Add**e, em seguida, escolha **Novo Item**.

2. Na lista de modelos do SharePoint, escolha o **receptor de evento** modelo e, em seguida, nomeie- **ProjectTaskListEventReceiver**.

     O **Assistente para personalização do SharePoint** é exibida.

3. No **escolher configurações do receptor de evento** , escolha **eventos de Item de lista** como o tipo de receptor de evento no **que tipo de receptor de eventos você deseja** lista.

4. No **qual item deve ser a origem do evento** , escolha **tarefas**.

5. Na lista de eventos para manipular, marque a caixa de seleção ao lado **um item foi adicionado**e, em seguida, escolha o **concluir** botão.

     Um novo nó de receptor de evento é adicionado ao projeto com um arquivo de código que é denominado **ProjectTaskListEventReceiver**.

6. Adicione código para o `ItemAdded` método na **ProjectTaskListEventReceiver** arquivo de código. Cada vez que uma nova tarefa for adicionada, um padrão de data de vencimento e uma descrição é adicionado à tarefa. O padrão de vencimento data é 1º de julho de 2009.

     [!code-vb[SPProjectTaskList#1](../sharepoint/codesnippet/VisualBasic/projecttasklist1/projecttasklisteventreceiver/projecttasklisteventreceiver.vb#1)]
     [!code-csharp[SPProjectTaskList#1](../sharepoint/codesnippet/CSharp/projecttasklist/projecttasklisteventreceiver/projecttasklisteventreceiver.cs#1)]

## <a name="customize-the-project-task-list-feature"></a>Personalizar o recurso de lista de tarefas do projeto

Quando você cria uma solução do SharePoint, o Visual Studio cria automaticamente os recursos para o padrão itens de projeto. Você pode personalizar as configurações de lista de tarefas do projeto para o site do SharePoint usando o Designer de recursos.

1. Na **Gerenciador de soluções**, expanda **recursos**.

2. Abra o menu de atalho **Feature1**e, em seguida, escolha **View Designer**.

3. No **Title** , digite **recurso de lista de tarefas do projeto**.

4. No **escopo** , escolha **Web**.

5. No **propriedades** janela, insira **1.0.0.0** como o valor para o **versão** propriedade.

## <a name="customize-the-project-task-list-package"></a>Personalizar o pacote de lista de tarefas do projeto

Quando você cria um projeto do SharePoint, o Visual Studio adiciona automaticamente os recursos que contêm os itens de projeto padrão para o pacote. Você pode personalizar as configurações de lista de tarefas do projeto para o site do SharePoint usando o Designer de pacote.

1. Na **SolutionExplorer**, abra o menu de atalho **pacote**e, em seguida, escolha **View Designer**.

2. No **nome** , digite **ProjectTaskListPackage**.

3. Selecione o **redefinir o servidor de Web** caixa de seleção.

## <a name="build-and-test-the-project-task-list"></a>Compilar e testar a lista de tarefas do projeto

Quando você executa o projeto, abre o site do SharePoint. No entanto, você deve navegar manualmente para o local da lista de tarefas.

1. Escolha o **F5** chave para criar e implantar sua lista de tarefas do projeto.

     Abre o site do SharePoint.

2. Escolha o **Home** guia.

3. Na barra lateral esquerda, escolha o **lista de tarefas do projeto** link.

     A página de lista de tarefas do projeto aparece.

4. No **ferramentas de lista** guia, escolha o **itens** guia.

5. No **itens** grupo, escolha o **Novo Item** botão.

6. No **Title** texto, digite **Task1**.

7. Escolha o **salvar** botão.

     Depois que o site é atualizado, o **Task1** tarefa aparece com uma data de vencimento de 7/1/2009.

8. Escolher **Task1**.

     A exibição detalhada da tarefa é exibida e a descrição mostra "É uma tarefa crítica."

## <a name="deploy-the-project-task-list"></a>Implantar a lista de tarefas do projeto

Depois que você compilar e testar a lista de tarefas do projeto, você pode implantá-lo para o *sistema local* ou um *sistema remoto*. O sistema local é o mesmo computador em que você desenvolveu a solução, enquanto um sistema remoto é um computador diferente.

### <a name="to-deploy-the-project-task-list-to-the-local-system"></a>Para implantar a lista de tarefas do projeto no sistema local

Na barra de menus do Visual Studio, escolha **construir** > **implantar solução**.

Visual Studio recicla o pool de aplicativos do IIS, cancela todas as versões existentes da solução, copia o pacote de solução (*. wsp*) do arquivo no SharePoint e, em seguida, ativa seus recursos. Agora você pode usar a solução no SharePoint. Para obter mais informações sobre as etapas de configuração de implantação, consulte [como: editar uma configuração de implantação do SharePoint](../sharepoint/how-to-edit-a-sharepoint-deployment-configuration.md).

### <a name="to-deploy-the-project-task-list-to-a-remote-system"></a>Para implantar a lista de tarefas do projeto em um sistema remoto

1. Na barra de menus do Visual Studio, escolha **construir** > **publicar**.

2. No **Publish** diálogo caixa, escolha o **publicar no sistema de arquivos** botão de opção.

     Você pode alterar o local de destino na **Publish** caixa de diálogo escolhendo o botão de reticências ![no ícone reticências](../sharepoint/media/ellipsisicon.gif "ícone de reticências") e, em seguida, navegar para outro local.

3. Escolha o **publicar** botão.

     Um *. wsp* arquivo é criado para a solução.

4. Cópia de *. wsp* arquivo no sistema remoto do SharePoint.

5. Usar o PowerShell `Add-SPUserSolution` comando para instalar o pacote de instalação remota do SharePoint. (Para soluções de farm, use o `Add-SPSolution` comando.)

     Por exemplo, `Add-SPUserSolution C:\MyProjects\ProjectTaskList\ProjectTaskList\bin\Debug\ProjectTaskList.wsp`.

6. Usar o PowerShell `Install-SPUserSolution` comando para implantar a solução. (Para soluções de farm, use o `Install-SPSolution` comando.)

     Por exemplo, `Install-SPUserSolution -Identity ProjectTaskList.wsp -Site http://NewSiteName`.

     Para obter mais informações sobre a implantação remota, consulte [soluções usando](http://go.microsoft.com/fwlink/?LinkId=217680) e [adicionando e implantando soluções com o PowerShell no SharePoint 2010](http://go.microsoft.com/fwlink/?LinkId=217682).

## <a name="next-steps"></a>Próximas etapas

Você pode aprender mais sobre como personalizar e implantar soluções do SharePoint dos seguintes tópicos:

- [Passo a passo: Criar uma coluna de site, o tipo de conteúdo e a lista para o SharePoint](../sharepoint/walkthrough-create-a-site-column-content-type-and-list-for-sharepoint.md)

- [Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)

- [Windows PowerShell para o SharePoint Server 2010](http://go.microsoft.com/fwlink/?LinkId=217684)

## <a name="see-also"></a>Consulte também
[Empacotar e implantar soluções do SharePoint](../sharepoint/packaging-and-deploying-sharepoint-solutions.md)
