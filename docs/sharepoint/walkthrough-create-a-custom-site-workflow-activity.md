---
title: 'Passo a passo: Criar uma atividade de fluxo de trabalho de Site personalizados | Microsoft Docs'
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
- custom workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, custom workflow activities
- site workflows [SharePoint development in Visual Studio]
- workflow activities [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, site workflows
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 2adb6dd8788027d89a743518adee4425e424ce60
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49894164"
---
# <a name="walkthrough-create-a-custom-site-workflow-activity"></a>Passo a passo: Criar uma atividade de fluxo de trabalho de site personalizada
  Este passo a passo demonstra como criar uma atividade personalizada para um fluxo de trabalho de nível de site usando [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. (Fluxos de trabalho de nível de site se aplica a todo o site, não apenas uma lista no site.) A atividade personalizada cria uma lista de avisos de backup e, em seguida, copia o conteúdo da lista de anúncios para ele.  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
- Criando um fluxo de trabalho de nível de site.  
  
- Criar uma atividade de fluxo de trabalho personalizado.  
  
- Criar e excluir uma lista do SharePoint.  
  
- Copiar itens de uma lista para outro.  
  
- Exibindo uma lista na barra de início rápido.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e do SharePoint.
  
-   Visual Studio.  
  
## <a name="create-a-site-workflow-custom-activity-project"></a>Criar um projeto de atividade personalizada do fluxo de trabalho de site
 Primeiro, crie um projeto para manter e testar a atividade de fluxo de trabalho personalizado.  
  
#### <a name="to-create-a-site-workflow-custom-activity-project"></a>Para criar um projeto de atividade personalizada do fluxo de trabalho de site  
  
1.  Na barra de menus, escolha **arquivo** > **New** > **projeto** para exibir o **novo projeto** caixa de diálogo.  
  
2.  Expanda o **SharePoint** nó em um **Visual c#** ou **Visual Basic**e, em seguida, escolha o **2010** nó.  
  
3.  No **modelos** painel, escolha o **o projeto do SharePoint 2010** modelo.  
  
4.  No **nome** , digite **AnnouncementBackup**e, em seguida, escolha o **Okey** botão.  
  
     O **Assistente para personalização do SharePoint** é exibida.  
  
5.  No **especificar o nível de site e segurança para depuração** , escolha o **implantar como uma solução de farm** botão de opção e, em seguida, escolha o **concluir** botão para aceitar o site padrão e o nível de confiança.  
  
     Esta etapa define o nível de confiança para a solução como solução de farm, a única opção disponível para projetos de fluxo de trabalho.  
  
6.  Na **Gerenciador de soluções**, escolha o nó do projeto e, em seguida, na barra de menus, escolha **Project** > **Add New Item**.  
  
7.  Em um **Visual c#** ou **Visual Basic**, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
8.  No **modelos** painel, escolha o **fluxo de trabalho sequencial (somente solução de Farm)** modelo e, em seguida, escolha o **Add** botão.  
  
     O **Assistente para personalização do SharePoint** é exibida.  
  
9. Sobre o **especifique o nome do fluxo de trabalho para depuração** página, aceite o nome padrão (AnnouncementBackup - Workflow1). Altere o tipo de modelo de fluxo de trabalho para **fluxo de trabalho do Site**e, em seguida, escolha o **próxima** botão.  
  
10. Escolha o **concluir** botão para aceitar as configurações padrão restantes.  
  
## <a name="add-a-custom-workflow-activity-class"></a>Adicionar uma classe de atividade de fluxo de trabalho personalizado
 Em seguida, adicione uma classe ao projeto para conter o código para a atividade de fluxo de trabalho personalizado.  
  
#### <a name="to-add-a-custom-workflow-activity-class"></a>Para adicionar uma classe de atividade de fluxo de trabalho personalizado  
  
1.  Na barra de menus, escolha **Project** > **Adicionar Novo Item** para exibir o **Add New Item** caixa de diálogo.  
  
2.  No **modelos instalados** exibição de árvore, escolha o **código** nó e, em seguida, escolha o **classe** modelo na lista de modelos de item de projeto. Use o nome padrão Class1. Escolha o botão **Adicionar**.  
  
3.  Substitua todo o código em Class1 pelo seguinte:  
  
     [!code-csharp[SP_AnnBackup#1](../sharepoint/codesnippet/CSharp/announcementbackup/class1.cs#1)]
     [!code-vb[SP_AnnBackup#1](../sharepoint/codesnippet/VisualBasic/announcementbackupvb/class1.vb#1)]  
  
4.  Salve o projeto e, em seguida, na barra de menus, escolha **construir** > **compilar solução**.  
  
     Class1 aparece como uma ação personalizada na **caixa de ferramentas** sobre o **AnnouncementBackup componentes** guia.  
  
## <a name="add-the-custom-activity-to-the-site-workflow"></a>Adicionar a atividade personalizada para o fluxo de trabalho do site
 Em seguida, adicione uma atividade ao fluxo de trabalho para conter o código personalizado.  
  
#### <a name="to-add-a-custom-activity-to-the-site-workflow"></a>Para adicionar uma atividade personalizada para o fluxo de trabalho do site
  
1.  Abra Workflow1 no designer de fluxo de trabalho no modo de exibição de design.  
  
2.  Arraste Class1 do **caixa de ferramentas** para que ele apareça sob o `onWorkflowActivated1` atividade ou abrir o menu de atalho para Class1, escolha **cópia**, abra o menu de atalho para a linha sob o `onWorkflowActivated1` atividade e, em seguida, escolha **colar**.  
  
3.  Salvar o projeto.  
  
## <a name="test-the-site-workflow-custom-activity"></a>Testar a atividade personalizada do fluxo de trabalho de site
 Em seguida, execute o projeto e iniciar o fluxo de trabalho do site. A atividade personalizada cria uma lista de anúncios de backup e copia o conteúdo da lista de avisos atual para ele. O código também verifica se já existe uma lista de backup antes de criar uma. Se já existir uma lista de backup, ele será excluído. O código também adiciona um link para a nova lista na barra de início rápido do site do SharePoint.  
  
#### <a name="to-test-the-site-workflow-custom-activity"></a>Para testar a atividade personalizada do fluxo de trabalho de site  
  
1.  Escolha o **F5** tecla para executar o projeto e implantá-lo no SharePoint.  
  
2.  Na barra de início rápido, escolha o **lista** link para exibir todas as listas que estão disponíveis no site do SharePoint. Observe que há apenas uma lista para ver anúncios sobre denominado **anúncios**.  
  
3.  Na parte superior da página da Web do SharePoint, escolha o **fluxos de trabalho de Site** link.  
  
4.  No início de uma seção do novo fluxo de trabalho, escolha o **AnnouncementBackup - Workflow1** link. Isso inicia o fluxo de trabalho do site e executa o código na ação personalizada.  
  
5.  Na barra de início rápido, escolha o **anúncios Backup** link. Observe que todos os comunicados que estão contidos na **anúncios** lista foram copiados para essa nova lista.  
  
## <a name="see-also"></a>Consulte também
 [Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)   
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)  
  
