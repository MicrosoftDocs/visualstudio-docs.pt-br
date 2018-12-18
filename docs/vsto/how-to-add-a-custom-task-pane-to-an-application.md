---
title: 'Como: adicionar um painel tarefa personalizada a um aplicativo'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- task panes [Office development in Visual Studio], adding to application
- custom task panes [Office development in Visual Studio], adding to application
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: b8608fcc263be4750c38b6fe3f84967f40dd34ab
ms.sourcegitcommit: 697162f54d3c4e30df702fd0289e447e211e3a85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/25/2018
ms.locfileid: "34548808"
---
# <a name="how-to-add-a-custom-task-pane-to-an-application"></a>Como: adicionar um painel tarefa personalizada a um aplicativo
  Você pode adicionar um painel tarefa personalizada para os aplicativos listados acima usando o suplemento do VSTO. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="add-a-custom-task-pane-to-an-application"></a>Adicionar um painel tarefa personalizada a um aplicativo  
  
### <a name="to-add-a-custom-task-pane-to-an-application"></a>Para adicionar um painel tarefa personalizada a um aplicativo  
  
1.  Abra ou crie um projeto de suplemento do VSTO para um dos aplicativos listados acima. Para obter mais informações, consulte [como: projetos do Office criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
2.  Sobre o **projeto** menu, clique em **adicionar controle de usuário**.  
  
3.  No **Adicionar Novo Item** caixa de diálogo, altere o nome do novo controle de usuário para **MyUserControl**e, em seguida, clique em **adicionar**.  
  
     O controle de usuário é aberto no designer.  
  
4.  Adicionar um ou mais controles de formulários do Windows do **caixa de ferramentas** para o controle de usuário.  
  
5.  Abra o **ThisAddIn.cs** ou **ThisAddIn** arquivo de código.  
  
6.  Adicione o seguinte código para o `ThisAddIn` classe. Esse código declara instâncias do `MyUserControl` e <xref:Microsoft.Office.Tools.CustomTaskPane> como membros de `ThisAddIn` classe.  
  
     [!code-vb[Trin_TaskPaneBasic#1](../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb#1)]
     [!code-csharp[Trin_TaskPaneBasic#1](../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs#1)]  
  
7.  Adicione o seguinte código ao manipulador de eventos do `ThisAddIn_Startup`. Esse código cria um novo <xref:Microsoft.Office.Tools.CustomTaskPane> adicionando o `MyUserControl` o objeto para o `CustomTaskPanes` coleção. O código também exibe o painel de tarefas.  
  
     [!code-vb[Trin_TaskPaneBasic#2](../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb#2)]
     [!code-csharp[Trin_TaskPaneBasic#2](../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs#2)]  
  
    > [!NOTE]  
    >  Esse código associa o painel de tarefas com a janela ativa no aplicativo. Para alguns aplicativos, você talvez queira modificar este código para garantir que o painel de tarefas é exibida com outros documentos ou itens no aplicativo. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)   
 [Painéis de tarefas personalizados](../vsto/custom-task-panes.md)   
 [Passo a passo: Automatizar um aplicativo de um painel tarefa personalizada](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)  
  
  