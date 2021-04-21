---
title: Painéis de tarefas personalizados
description: Saiba que os painéis de tarefas personalizados fornecem uma maneira de criar seu próprio painel de tarefas e fornecer aos usuários uma interface familiar para acessar os recursos da solução.
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, task panes
- user interface panels [Office development in Visual Studio]
- task panes [Office development in Visual Studio]
- user interfaces [Office development in Visual Studio], custom task panes
- custom task panes [Office development in Visual Studio], creating
- task panes [Office development in Visual Studio]. multiple application windows
- custom task panes [Office development in Visual Studio], multiple application windows
- task panes [Office development in Visual Studio], creating
- application-level add-ins [Office development in Visual Studio], custom task panes
- multiple applications windows with custom task panes [Office development in Visual Studio]
- add-ins [Office development in Visual Studio], custom task panes
- custom task panes [Office development in Visual Studio]
- task panes [Office development in Visual Studio], about custom task panes
- custom task panes [Office development in Visual Studio], about custom task panes
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 6c35d963b426fe24a43bef24617f79c042c272e9
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107828157"
---
# <a name="custom-task-panes"></a>Painéis de tarefas personalizados
  Os painéis de tarefas são painéis de interface do usuário que normalmente são encaixados em um lado de uma janela em um aplicativo Microsoft Office. Os painéis de tarefas personalizados fornecem uma maneira de criar seu próprio painel de tarefas e fornecer aos usuários uma interface familiar para acessar os recursos da solução. Por exemplo, a interface pode conter controles que executam código para modificar documentos ou exibir dados de uma fonte de dados.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

> [!NOTE]
> Um painel de tarefas personalizado é diferente do painel Ações. O painel Ações faz parte das personalizações em nível de documento para Microsoft Office Word e Microsoft Office Excel. Para obter mais informações, consulte [visão geral do painel Ações](../vsto/actions-pane-overview.md).

## <a name="benefits-of-custom-task-panes"></a>Benefícios dos painéis de tarefas personalizados
 Os painéis de tarefas personalizados permitem integrar seus recursos a uma interface do usuário familiar. Você pode criar um painel de tarefas personalizado rapidamente usando as ferramentas do Visual Studio.

### <a name="familiar-user-interface"></a>Interface do usuário familiar
 Os usuários de aplicativos no sistema de Microsoft Office já estão familiarizados com o uso de painéis de tarefas, como o painel de tarefas **estilos e formatação** no Word. Os painéis de tarefas personalizados se comportam como outros painéis de tarefas no sistema Microsoft Office. Os usuários podem encaixar painéis de tarefas personalizados em diferentes lados da janela do aplicativo, ou podem arrastar painéis de tarefas personalizados para qualquer local na janela. Você pode criar um suplemento do VSTO que exibe vários painéis de tarefas personalizados ao mesmo tempo, e os usuários podem controlar cada painel de tarefas individualmente.

### <a name="windows-forms-support"></a>Suporte do Windows Forms
 A interface do usuário de um painel de tarefas personalizado que você cria usando as ferramentas de desenvolvimento do Office no Visual Studio é baseada em controles de Windows Forms. Você pode usar o Designer de Formulários do Windows familiar para criar a interface do usuário para um painel de tarefas personalizado. Você também pode usar o suporte de vinculação de dados no Windows Forms para associar uma fonte de dados a controles no painel de tarefas.

## <a name="create-a-custom-task-pane"></a>Criar um painel de tarefas personalizado
 Você pode criar um painel de tarefas personalizado básico em duas etapas:

1. Crie uma interface do usuário para seu painel de tarefas personalizado adicionando Windows Forms controles a um <xref:System.Windows.Forms.UserControl> objeto.

2. Crie uma instância do painel de tarefas personalizado passando o controle de usuário para o <xref:Microsoft.Office.Tools.CustomTaskPaneCollection> objeto em seu suplemento do VSTO. Essa coleção retorna um novo <xref:Microsoft.Office.Tools.CustomTaskPane> objeto que você pode usar para modificar a aparência do painel de tarefas e responder a eventos de usuário.

   Para obter mais informações, consulte [como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md).

### <a name="create-the-user-interface"></a>Criar a interface do usuário
 Todos os painéis de tarefas personalizados criados usando as ferramentas de desenvolvimento do Office no Visual Studio contêm um <xref:System.Windows.Forms.UserControl> objeto. Esse controle de usuário fornece a interface do usuário do seu painel de tarefas personalizado. Você pode criar o controle de usuário em tempo de design ou em tempo de execução. Se você criar o controle de usuário em tempo de design, poderá usar o Designer de Formulários do Windows para construir a interface do usuário do seu painel de tarefas.

### <a name="instantiate-the-custom-task-pane"></a>Criar uma instância do painel de tarefas personalizado
 Depois de criar um controle de usuário que contém a interface do usuário do painel de tarefas personalizado, você precisa criar uma instância de um <xref:Microsoft.Office.Tools.CustomTaskPane> . Para fazer isso, passe o controle de usuário para o <xref:Microsoft.Office.Tools.CustomTaskPaneCollection> em seu suplemento do VSTO chamando um dos <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> métodos. Essa coleção é exposta como o `CustomTaskPanes` campo da `ThisAddIn` classe. O exemplo de código a seguir deve ser executado da `ThisAddIn` classe.

 :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_TaskPaneBasic/ThisAddIn.vb" id="Snippet2":::
 :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_TaskPaneBasic/ThisAddIn.cs" id="Snippet2":::

 Os <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> métodos retornam um novo <xref:Microsoft.Office.Tools.CustomTaskPane> objeto. Você pode usar esse objeto para modificar a aparência do painel de tarefas e para responder a eventos de usuário.

### <a name="control-the-task-pane-in-multiple-windows"></a>Controlar o painel de tarefas em várias janelas
 Os painéis de tarefas personalizados são associados a uma janela de quadro do documento, que apresenta uma exibição de um documento ou item para o usuário. O painel de tarefas fica visível somente quando a janela associada está visível.

 Para determinar qual janela exibe o painel de tarefas personalizado, use a <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> sobrecarga do método apropriado ao criar o painel de tarefas:

- Para associar o painel de tarefas à janela ativa, use o <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> método.

- Para associar o painel de tarefas a um documento hospedado por uma janela especificada, use o <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> método.

  Alguns aplicativos do Office exigem instruções explícitas para quando criar ou exibir o painel de tarefas quando mais de uma janela estiver aberta. Isso torna importante considerar onde criar uma instância do painel de tarefas personalizado em seu código para garantir que o painel de tarefas apareça com os documentos ou itens apropriados no aplicativo. Para obter mais informações, consulte [gerenciar painéis de tarefas personalizados em janelas de aplicativos](#Managing).

## <a name="access-the-application-from-the-task-pane"></a>Acessar o aplicativo no painel de tarefas
 Se você quiser automatizar o aplicativo do controle de usuário, poderá acessar diretamente o modelo de objeto usando `Globals.ThisAddIn.Application` no seu código. A `Globals` classe estática fornece acesso ao `ThisAddIn` objeto. O `Application` campo desse objeto é o ponto de entrada no modelo de objeto do aplicativo.

 Para obter mais informações sobre o `Application` campo do `ThisAddIn` objeto, consulte [programar suplementos do VSTO](../vsto/programming-vsto-add-ins.md). Para obter instruções que demonstram como automatizar um aplicativo a partir de um painel de tarefas personalizado, consulte [explicação: automática de um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md). Para obter mais informações sobre a `Globals` classe, consulte [acesso global a objetos em projetos do Office](../vsto/global-access-to-objects-in-office-projects.md).

## <a name="manage-the-user-interface-of-the-task-pane"></a>Gerenciar a interface do usuário do painel de tarefas
 Depois de criar o painel de tarefas, você pode usar propriedades e eventos do <xref:Microsoft.Office.Tools.CustomTaskPane> objeto para controlar a interface do usuário do painel de tarefas e responder quando o usuário alterar o painel de tarefas.

### <a name="make-the-custom-task-pane-visible"></a>Tornar o painel de tarefas personalizado visível
 Por padrão, o painel de tarefas não é visível. Para tornar o painel de tarefas visível, você deve definir a <xref:Microsoft.Office.Tools.CustomTaskPane.Visible%2A> propriedade como **true**.

 Os usuários podem fechar um painel de tarefas a qualquer momento clicando no botão **fechar** (X) no canto do painel de tarefas. No entanto, não há uma maneira padrão para os usuários abrirem o painel de tarefas personalizado novamente. Se um usuário fechar um painel de tarefas personalizado, esse usuário não poderá exibir o painel de tarefas personalizado novamente, a menos que você forneça uma maneira de exibi-lo.

 Se você criar um painel de tarefas personalizado em seu suplemento do VSTO, você também deverá criar um elemento de interface do usuário, como um botão, que os usuários possam clicar para exibir ou ocultar seu painel de tarefas personalizado. Se você criar um painel de tarefas personalizado em um aplicativo Microsoft Office que ofereça suporte à personalização da faixa de faixas, poderá adicionar um grupo de controle à faixa de uma com um botão que exibe ou oculta o painel de tarefas personalizado. Para obter instruções que demonstram como fazer isso, consulte [Walkthrough: sincronizar um painel de tarefas personalizado com um botão Ribbon](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md).

 Se você criar um painel de tarefas personalizado em um aplicativo Microsoft Office que não ofereça suporte à personalização da faixa de faixas, poderá adicionar um <xref:Microsoft.Office.Core.CommandBarButton> que exibe ou oculta o painel de tarefas personalizado.

### <a name="modify-the-appearance-of-the-task-pane"></a>Modificar a aparência do painel de tarefas
 Você pode controlar o tamanho e o local de um painel de tarefas personalizado usando as propriedades do <xref:Microsoft.Office.Tools.CustomTaskPane> objeto. Você pode fazer muitas outras alterações na aparência de um painel de tarefas personalizado usando as propriedades do <xref:System.Windows.Forms.UserControl> objeto contido no painel de tarefas personalizado. Por exemplo, você pode especificar uma imagem de plano de fundo para um painel de tarefas personalizado usando a <xref:System.Windows.Forms.Control.BackgroundImage%2A> Propriedade do controle de usuário.

 A tabela a seguir lista as alterações que você pode fazer em um painel de tarefas personalizado usando <xref:Microsoft.Office.Tools.CustomTaskPane> Propriedades.

|Tarefa|Propriedade|
|----------|--------------|
|Para alterar o tamanho do painel de tarefas|<xref:Microsoft.Office.Tools.CustomTaskPane.Height%2A><br /><br /> <xref:Microsoft.Office.Tools.CustomTaskPane.Width%2A>|
|Para alterar o local do painel de tarefas|<xref:Microsoft.Office.Tools.CustomTaskPane.DockPosition%2A>|
|Para ocultar o painel de tarefas ou torná-lo visível|<xref:Microsoft.Office.Tools.CustomTaskPane.Visible%2A>|
|Para impedir que o usuário altere o local do painel de tarefas|<xref:Microsoft.Office.Tools.CustomTaskPane.DockPositionRestrict%2A>|

### <a name="program-custom-task-pane-events"></a>Eventos do painel de tarefas personalizado do programa
 Talvez você queira que seu suplemento do VSTO responda quando o usuário modificar o painel de tarefas personalizado. Por exemplo, se o usuário alterar a orientação do painel de vertical para horizontal, talvez você queira reposicionar os controles.

 A tabela a seguir lista os eventos que você pode manipular para responder a alterações que o usuário faz no painel de tarefas personalizado.

|Tarefa|Evento|
|----------|-----------|
|Para responder quando o usuário altera o local do painel de tarefas.|<xref:Microsoft.Office.Tools.CustomTaskPane.DockPositionChanged>|
|Para responder quando o usuário oculta o painel de tarefas ou o torna visível.|<xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged>|

## <a name="clean-up-resources-used-by-the-task-pane"></a>Limpar os recursos usados pelo painel de tarefas
 Depois de criar um painel de tarefas personalizado, o <xref:Microsoft.Office.Tools.CustomTaskPane> objeto permanece na memória, contanto que seu suplemento do VSTO esteja em execução. O objeto permanece na memória mesmo depois que o usuário clica no botão **fechar** (X) no canto do painel de tarefas.

 Para limpar os recursos usados pelo painel de tarefas enquanto o suplemento do VSTO ainda está em execução, use os <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Remove%2A> <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.RemoveAt%2A> métodos ou. Esses métodos removem o <xref:Microsoft.Office.Tools.CustomTaskPane> objeto especificado da `CustomTaskPanes` coleção e chamam o `Dispose` método do objeto.

 O [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] limpa automaticamente os recursos usados pelo painel de tarefas personalizado quando o suplemento do VSTO é descarregado. Não chame os <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Remove%2A> métodos ou <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.RemoveAt%2A> no manipulador de `ThisAddIn_Shutdown` eventos em seu projeto. Esses métodos gerarão um <xref:System.ObjectDisposedException> , pois o [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] limpa os recursos usados pelo <xref:Microsoft.Office.Tools.CustomTaskPane> objeto antes de `ThisAddIn_Shutdown` ser chamado. Para obter mais informações sobre o `ThisAddIn_Shutdown` , consulte [eventos em projetos do Office](../vsto/events-in-office-projects.md).

## <a name="manage-custom-task-panes-in-multiple-application-windows"></a><a name="Managing"></a> Gerenciar painéis de tarefas personalizados em várias janelas de aplicativos
 Quando você cria um painel de tarefas personalizado em um aplicativo que usa várias janelas para exibir documentos e outros itens, você precisa executar etapas adicionais para garantir que o painel de tarefas fique visível quando o usuário espera que ele esteja.

 Painéis de tarefas personalizados em todos os aplicativos são associados a uma janela de quadro do documento, que apresenta uma exibição de um documento ou item para o usuário. O painel de tarefas fica visível somente quando a janela associada está visível. No entanto, nem todos os aplicativos usam janelas de quadro de documento da mesma maneira.

 Os seguintes grupos de aplicativos têm requisitos de desenvolvimento diferentes:

- [Outlook](#Outlook)

- [Word, InfoPath e PowerPoint](#WordAndInfoPath)

## <a name="outlook"></a><a name="Outlook"></a> Outlook
 Quando você cria um painel de tarefas personalizado para o Outlook, o painel de tarefas personalizado é associado a uma janela específica do Explorer ou do Inspetor. Os gerenciadores são janelas que exibem o conteúdo de uma pasta e os inspetores são janelas que exibem um item, como uma mensagem de email ou uma tarefa.

 Se desejar exibir um painel de tarefas personalizado com várias janelas do Explorer ou do Inspetor, você precisará criar uma nova instância do painel de tarefas personalizado quando uma janela do Explorer ou do Inspetor for aberta. Para fazer isso, manipule um evento que é gerado quando uma janela Explorer ou inspector é criada e, em seguida, cria o painel de tarefas no manipulador de eventos. Você também pode manipular eventos Explorer e inspector para ocultar ou exibir painéis de tarefas, dependendo de qual janela está visível.

 Para associar o painel de tarefas a um Gerenciador ou Inspetor específico, use o <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> método para criar o painel de tarefas e passe <xref:Microsoft.Office.Interop.Outlook.Explorer> o <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto ou para o parâmetro de *janela* . Para obter mais informações sobre como criar painéis de tarefas personalizados, consulte [visão geral dos painéis de tarefas personalizados](../vsto/custom-task-panes.md).

- <xref:Microsoft.Office.Interop.Outlook.ExplorersEvents_Event.NewExplorer>

- <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Activate>

- <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Close>

- <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Deactivate>

  Para monitorar o estado das janelas do Inspetor, você pode manipular os seguintes eventos relacionados ao inspetor:

- <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector>

- <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_10_Event.Activate>

- <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_10_Event.Close>

- <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_10_Event.Deactivate>

### <a name="prevent-multiple-instances-of-a-custom-task-pane-in-outlook"></a>Impedir várias instâncias de um painel de tarefas personalizado no Outlook
 Para impedir que janelas do Outlook exibam várias instâncias de um painel de tarefas personalizado, remova explicitamente o painel de tarefas personalizado da `CustomTaskPanes` coleção da `ThisAddIn` classe quando cada janela é fechada. Chame o <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Remove%2A> método em um evento que é gerado quando uma janela é fechada, como <xref:Microsoft.Office.Interop.Outlook.ExplorerEvents_10_Event.Close> ou <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_10_Event.Close> .

 Se você não remover explicitamente o painel de tarefas personalizado, o Windows Outlook poderá exibir várias instâncias do painel de tarefas personalizado. Às vezes, o Outlook recicla as janelas e reciclaram as referências a todos os painéis de tarefas personalizados que foram anexados a eles.

## <a name="word-infopath-and-powerpoint"></a><a name="WordAndInfoPath"></a> Word, InfoPath e PowerPoint
 Word, InfoPath e PowerPoint exibem cada documento em uma janela de quadro de documento diferente. Quando você cria um painel de tarefas personalizado para esses aplicativos, o painel de tarefas personalizado é associado somente a um documento específico. Se o usuário abrir um documento diferente, o painel de tarefas personalizado ficará oculto até que o documento anterior fique visível novamente.

 Se você quiser exibir um painel de tarefas personalizado com vários documentos, crie uma nova instância do painel de tarefas personalizado quando o usuário criar um novo documento ou abrir um documento existente. Para fazer isso, manipule eventos que são gerados quando um documento é criado ou aberto e, em seguida, crie o painel de tarefas nos manipuladores de eventos. Você também pode manipular eventos de documento para ocultar ou exibir painéis de tarefas, dependendo de qual documento está visível.

 Para associar o painel de tarefas a uma janela de documento específica, use o <xref:Microsoft.Office.Tools.CustomTaskPaneCollection.Add%2A> método para criar o painel de tarefas e passar um <xref:Microsoft.Office.Interop.Word.Window> (for Word),  <xref:Microsoft.Office.Interop.InfoPath.WindowObject> (para InfoPath) ou [DocumentWindow](/previous-versions/office/developer/office-2010/ff762047(v=office.14)) (para PowerPoint) para o parâmetro *Window* .

### <a name="word-events"></a>Eventos do Word
 Para monitorar o estado das janelas de documentos no Word, você pode manipular os seguintes eventos:

- <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentBeforeClose>

- <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.DocumentOpen>

- <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.NewDocument>

- <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.WindowActivate>

- <xref:Microsoft.Office.Interop.Word.ApplicationEvents4_Event.WindowDeactivate>

### <a name="infopath-events"></a>Eventos do InfoPath
 Para monitorar o estado das janelas de documentos no InfoPath, você pode manipular os seguintes eventos:

- <xref:Microsoft.Office.Interop.InfoPath._ApplicationEvents_Event.NewXDocument>

- <xref:Microsoft.Office.Interop.InfoPath._ApplicationEvents_Event.WindowActivate>

- <xref:Microsoft.Office.Interop.InfoPath._ApplicationEvents_Event.WindowDeactivate>

- <xref:Microsoft.Office.Interop.InfoPath._ApplicationEvents_Event.XDocumentBeforeClose>

- <xref:Microsoft.Office.Interop.InfoPath._ApplicationEvents_Event.XDocumentOpen>

### <a name="powerpoint-events"></a>Eventos do PowerPoint
 Para monitorar o estado das janelas de documentos no PowerPoint, você pode manipular os seguintes eventos:

- [Microsoft.Office.Interop.PowerPoint.EApplication_Event. AfterNewPresentation](/previous-versions/office/developer/office-2010/ff761105(v%3doffice.14))

- [Microsoft.Office.Interop.PowerPoint.EApplication_Event. AfterPresentationOpen](/previous-versions/office/developer/office-2010/ff762843(v%3doffice.14))

- [Microsoft.Office.Interop.PowerPoint.EApplication_Event. NewPresentation](/previous-versions/office/developer/office-2010/ff761498(v%3doffice.14))

- [Microsoft.Office.Interop.PowerPoint.EApplication_Event. PresentationOpen](/previous-versions/office/developer/office-2010/ff760423(v=office.14))

- [Microsoft.Office.Interop.PowerPoint.EApplication_Event. WindowActivate](/previous-versions/office/developer/office-2010/ff761153(v=office.14))

- [Microsoft.Office.Interop.PowerPoint.EApplication_Event. WindowDeactivate](/previous-versions/office/developer/office-2010/ff763093(v=office.14))

## <a name="see-also"></a>Consulte também
- [Como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [Walkthrough: automatizar um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
- [Walkthrough: sincronizar um painel de tarefas personalizado com um botão da faixa de das](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)
- [Walkthrough: Exibir painéis de tarefas personalizados com mensagens de email no Outlook](../vsto/walkthrough-displaying-custom-task-panes-with-e-mail-messages-in-outlook.md)
