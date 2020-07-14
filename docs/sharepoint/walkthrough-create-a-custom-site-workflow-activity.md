---
title: 'Walkthrough: criar uma atividade de fluxo de trabalho de site personalizada | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, custom workflow activities
- site workflows [SharePoint development in Visual Studio]
- workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, site workflows
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: dc7eef8b0924be745de436e06acc36785b1cb99b
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016536"
---
# <a name="walkthrough-create-a-custom-site-workflow-activity"></a>Walkthrough: criar uma atividade de fluxo de trabalho de site personalizada
  Este tutorial demonstra como criar uma atividade personalizada para um fluxo de trabalho de nível de site usando o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . (Os fluxos de trabalho de nível de site se aplicam a todo o site, não apenas a uma lista no site.) A atividade personalizada cria uma lista de anúncios de backup e, em seguida, copia o conteúdo da lista de anúncios para ela.

 Este tutorial demonstra as seguintes tarefas:

- Criando um fluxo de trabalho no nível do site.

- Criar uma atividade de fluxo de trabalho personalizada.

- Criando e excluindo uma lista do SharePoint.

- Copiando itens de uma lista para outra.

- Exibindo uma lista na barra de início rápido.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e SharePoint.

- Visual Studio.

## <a name="create-a-site-workflow-custom-activity-project"></a>Criar um projeto de atividade personalizada do fluxo de trabalho do site
 Primeiro, crie um projeto para manter e testar a atividade de fluxo de trabalho personalizada.

#### <a name="to-create-a-site-workflow-custom-activity-project"></a>Para criar um projeto de atividade personalizada de fluxo de trabalho do site

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto** para exibir a caixa de diálogo **novo projeto** .

2. Expanda o nó **do SharePoint** sob o **Visual C#** ou **Visual Basic**e escolha o nó **2010** .

3. No painel **modelos** , escolha o modelo de **projeto do SharePoint 2010** .

4. Na caixa **nome** , digite **AnnouncementBackup**e, em seguida, escolha o botão **OK** .

     O **Assistente para personalização do SharePoint** é exibido.

5. Na página **especificar o site e o nível de segurança para depuração** , escolha o botão de opção **implantar como uma solução de farm** e escolha o botão **concluir** para aceitar o nível de confiança e o site padrão.

     Esta etapa define o nível de confiança para a solução como solução de farm, a única opção disponível para projetos de fluxo de trabalho.

6. Em **Gerenciador de soluções**, escolha o nó do projeto e, na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

7. Em **Visual C#** ou **Visual Basic**, expanda o nó do **SharePoint** e escolha o nó **2010** .

8. No painel **modelos** , escolha o modelo **fluxo de trabalho Sequencial (somente solução de farm)** e, em seguida, escolha o botão **Adicionar** .

     O **Assistente para personalização do SharePoint** é exibido.

9. Na página **especificar o nome do fluxo de trabalho para depuração** , aceite o nome padrão (AnnouncementBackup-Workflow1). Altere o tipo de modelo de fluxo de trabalho para **fluxo de trabalho do site**e, em seguida, escolha o botão **Avançar** .

10. Escolha o botão **concluir** para aceitar as configurações padrão restantes.

## <a name="add-a-custom-workflow-activity-class"></a>Adicionar uma classe de atividade de fluxo de trabalho personalizada
 Em seguida, adicione uma classe ao projeto para conter o código para a atividade de fluxo de trabalho personalizada.

#### <a name="to-add-a-custom-workflow-activity-class"></a>Para adicionar uma classe de atividade de fluxo de trabalho personalizada

1. Na barra de menus, escolha **projeto**  >  **Adicionar novo item** para exibir a caixa de diálogo **Adicionar novo item** .

2. Na exibição de árvore **modelos instalados** , escolha o nó de **código** e escolha o modelo de **classe** na lista de modelos de item de projeto. Use o nome padrão Class1. Clique no botão **Adicionar**.

3. Substitua todo o código em Class1 pelo seguinte:

     [!code-csharp[SP_AnnBackup#1](../sharepoint/codesnippet/CSharp/announcementbackup/class1.cs#1)]
     [!code-vb[SP_AnnBackup#1](../sharepoint/codesnippet/VisualBasic/announcementbackupvb/class1.vb#1)]

4. Salve o projeto e, na barra de menus, escolha **Compilar**  >  **Compilar solução**.

     Class1 é exibido como uma ação personalizada na **caixa de ferramentas** na guia **componentes do AnnouncementBackup** .

## <a name="add-the-custom-activity-to-the-site-workflow"></a>Adicionar a atividade personalizada ao fluxo de trabalho do site
 Em seguida, adicione uma atividade ao fluxo de trabalho para conter o código personalizado.

#### <a name="to-add-a-custom-activity-to-the-site-workflow"></a>Para adicionar uma atividade personalizada ao fluxo de trabalho do site

1. Abra Workflow1 no designer de fluxo de trabalho no modo Design.

2. Arraste Class1 da **caixa de ferramentas** para que ele apareça sob a `onWorkflowActivated1` atividade ou abra o menu de atalho para Class1, escolha **copiar**, abra o menu de atalho da linha sob a `onWorkflowActivated1` atividade e escolha **colar**.

3. Salve o projeto.

## <a name="test-the-site-workflow-custom-activity"></a>Testar a atividade personalizada do fluxo de trabalho do site
 Em seguida, execute o projeto e inicie o fluxo de trabalho do site. A atividade personalizada cria uma lista de anúncios de backup e copia o conteúdo da lista de comunicados atual para ele. O código também verifica se uma lista de backup já existe antes de criar uma. Se uma lista de backup já existir, ela será excluída. O código também adiciona um link para a nova lista na barra de início rápido do site do SharePoint.

#### <a name="to-test-the-site-workflow-custom-activity"></a>Para testar a atividade personalizada do fluxo de trabalho do site

1. Escolha a tecla **F5** para executar o projeto e implantá-lo no SharePoint.

2. Na barra de início rápido, escolha o link **listas** para exibir todas as listas que estão disponíveis no site do SharePoint. Observe que há apenas uma lista de anúncios chamados **comunicados**.

3. Na parte superior da página da Web do SharePoint, escolha o link **fluxos de trabalho do site** .

4. Na seção iniciar um novo fluxo de trabalho, escolha o link **AnnouncementBackup-Workflow1** . Isso inicia o fluxo de trabalho do site e executa o código na ação personalizada.

5. Na barra de início rápido, escolha o link **backup de anúncios** . Observe que todos os comunicados contidos na lista **comunicados** foram copiados para essa nova lista.

## <a name="see-also"></a>Consulte também
- [Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
