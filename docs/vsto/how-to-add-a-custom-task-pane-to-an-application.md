---
title: 'Como: adicionar um painel de tarefas personalizado a um aplicativo'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- task panes [Office development in Visual Studio], adding to application
- custom task panes [Office development in Visual Studio], adding to application
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 0df4d51795f01c98790f1d5b0525c45cc71899ab
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546205"
---
# <a name="how-to-add-a-custom-task-pane-to-an-application"></a>Como: adicionar um painel de tarefas personalizado a um aplicativo
  Você pode adicionar um painel de tarefas personalizado aos aplicativos listados acima usando o suplemento do VSTO. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="add-a-custom-task-pane-to-an-application"></a>Adicionar um painel de tarefas personalizado a um aplicativo

### <a name="to-add-a-custom-task-pane-to-an-application"></a>Para adicionar um painel de tarefas personalizado a um aplicativo

1. Abra ou crie um projeto de suplemento do VSTO para um dos aplicativos listados acima. Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

2. No menu **projeto** , clique em **Adicionar controle de usuário**.

3. Na caixa de diálogo **Adicionar novo item** , altere o nome do novo controle de usuário para **MyUserControl**e clique em **Adicionar**.

     O controle de usuário é aberto no designer.

4. Adicione um ou mais controles de Windows Forms da **caixa de ferramentas** ao controle de usuário.

5. Abra o arquivo de código **ThisAddIn.cs** ou **ThisAddIn. vb** .

6. Adicione o código a seguir à classe `ThisAddIn` . Esse código declara instâncias do `MyUserControl` e <xref:Microsoft.Office.Tools.CustomTaskPane> como membros da `ThisAddIn` classe.

     [!code-vb[Trin_TaskPaneBasic#1](../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb#1)]
     [!code-csharp[Trin_TaskPaneBasic#1](../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs#1)]

7. Adicione o seguinte código ao manipulador de eventos do `ThisAddIn_Startup`. Esse código cria um novo <xref:Microsoft.Office.Tools.CustomTaskPane> adicionando o `MyUserControl` objeto à `CustomTaskPanes` coleção. O código também exibe o painel de tarefas.

     [!code-vb[Trin_TaskPaneBasic#2](../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb#2)]
     [!code-csharp[Trin_TaskPaneBasic#2](../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs#2)]

    > [!NOTE]
    > Esse código associa o painel de tarefas personalizado à janela ativa no aplicativo. Para alguns aplicativos, talvez você queira modificar esse código para garantir que o painel de tarefas seja exibido com outros documentos ou itens no aplicativo. Para obter mais informações, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).

## <a name="see-also"></a>Confira também
- [Personalização da interface do usuário do Office](../vsto/office-ui-customization.md)
- [Painéis de tarefas personalizados](../vsto/custom-task-panes.md)
- [Walkthrough: automatizar um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
