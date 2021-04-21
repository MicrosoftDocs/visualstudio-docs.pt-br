---
title: Exibir painéis de tarefas personalizados com mensagens de email no Outlook
description: Saiba como exibir uma instância exclusiva de um painel de tarefas personalizado com cada mensagem de email no Microsoft Outlook que é criada ou aberta.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], custom task panes
- task panes [Office development in Visual Studio], displaying with e-mail messages
- displaying custom task panes in e-mail
- e-mail [Office development in Visual Studio], custom task panes displayed in
- custom task panes [Office development in Visual Studio], displaying with e-mail messages
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: bb1aed5ef110b726dae6e51337b0934ae0a8e69d
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107824205"
---
# <a name="walkthrough-display-custom-task-panes-with-email-messages-in-outlook"></a>Walkthrough: Exibir painéis de tarefas personalizados com mensagens de email no Outlook
  Este tutorial demonstra como exibir uma instância exclusiva de um painel de tarefas personalizado com cada mensagem de email que é criada ou aberta. Os usuários podem exibir ou ocultar o painel de tarefas personalizado usando um botão na faixa de de cada mensagem de email.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 Para exibir um painel de tarefas personalizado com várias janelas do Explorer ou do Inspetor, você deve criar uma instância do painel de tarefas personalizado para cada janela aberta. Para obter mais informações sobre o comportamento de painéis de tarefas personalizados no Windows do Outlook, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).

> [!NOTE]
> Este tutorial apresenta o código do suplemento do VSTO em pequenas seções para facilitar a discussão da lógica por trás do código.

 Este passo a passo ilustra as seguintes tarefas:

- Criação da interface do usuário (IU) do painel de tarefas personalizado.

- Criando uma interface do usuário personalizada da faixa de uma.

- Exibindo a interface do usuário da faixa de para personalizada com mensagens de email.

- Criar uma classe para gerenciar janelas de inspetores e painéis de tarefas personalizados.

- Inicializando e limpando os recursos usados pelo suplemento do VSTO.

- Sincronizando o botão de alternância da faixa de opção com o painel de tarefas personalizado.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft [!INCLUDE[Outlook_15_short](../vsto/includes/outlook-15-short-md.md)] ou Microsoft Outlook 2010.

## <a name="create-the-project"></a>Criar o projeto
 Os painéis de tarefas personalizados são implementados nos suplementos do VSTO. Comece criando um projeto de suplemento do VSTO para Outlook.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de **suplemento do Outlook** com o nome **OutlookMailItemTaskPane**. Use o modelo de projeto de **suplemento do Outlook** . Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o arquivo de código *ThisAddIn. cs* ou *ThisAddIn. vb* e adiciona o projeto **OutlookMailItemTaskPane** ao **Gerenciador de soluções**.

## <a name="design-the-user-interface-of-the-custom-task-pane"></a>Criar a interface do usuário do painel de tarefas personalizado
 Não há nenhum designer visual para os painéis de tarefas personalizados, mas você pode criar um controle de usuário com a interface que desejar. O painel de tarefas personalizado neste suplemento do VSTO tem uma interface do usuário simples que contém um <xref:System.Windows.Forms.TextBox> controle. Mais adiante neste tutorial, você adicionará o controle de usuário ao painel de tarefas personalizado.

### <a name="to-design-the-user-interface-of-the-custom-task-pane"></a>Para criar a interface do usuário do painel de tarefas personalizado

1. Em **Gerenciador de soluções**, clique no projeto **OutlookMailItemTaskPane** .

2. No menu **projeto** , clique em **Adicionar controle de usuário**.

3. Na caixa de diálogo **Adicionar novo item** , altere o nome do controle de usuário para **TaskPaneControl** e clique em **Adicionar**.

     O controle de usuário é aberto no designer.

4. Na guia **controles comuns** da caixa de **ferramentas**, arraste um controle **TextBox** para o controle de usuário.

## <a name="design-the-user-interface-of-the-ribbon"></a>Criar a interface do usuário da faixa de faixas
 Uma das metas para esse suplemento do VSTO é fornecer aos usuários uma maneira de ocultar ou exibir o painel de tarefas personalizado da faixa de opção de cada mensagem de email. Para fornecer a interface do usuário, crie uma interface de usuário da faixa de opção personalizada que exibe um botão de alternância no qual os usuários podem clicar para exibir ou ocultar o painel de tarefas personalizado.

### <a name="to-create-a-custom-ribbon-ui"></a>Para criar uma interface do usuário personalizada

1. No menu **Projeto** , clique em **Adicionar Novo Item**.

2. Na caixa de diálogo **Adicionar novo item** , selecione **faixa de opções (designer visual)**.

3. Altere o nome da nova faixa de forma para **ManageTaskPaneRibbon** e clique em **Adicionar**.

     O arquivo *ManageTaskPaneRibbon. cs* ou *ManageTaskPaneRibbon. vb* é aberto no designer de faixa de faixas e exibe uma guia e um grupo padrão.

4. No designer de faixa de faixas, clique em **grupo1**.

5. Na janela **Propriedades** , defina a propriedade **rótulo** como **Gerenciador de painéis de tarefas**.

6. Na guia **controles da faixa** de **ferramentas** do Office, arraste um controle ToggleButton para o grupo **Gerenciador de painéis de tarefas** .

7. Clique em **toggleButton1**.

8. Na janela **Propriedades** , defina a propriedade **rótulo** para **mostrar o painel de tarefas**.

## <a name="display-the-custom-ribbon-user-interface-with-email-messages"></a>Exibir a interface do usuário da faixa de medida personalizada com mensagens de email
 O painel de tarefas personalizado que você cria neste passo a passos é projetado para aparecer somente com janelas de inspetor que contêm mensagens de email. Portanto, defina as propriedades para exibir a interface do usuário da faixa de medida personalizada somente com essas janelas.

### <a name="to-display-the-custom-ribbon-ui-with-email-messages"></a>Para exibir a interface do usuário da faixa de para personalizada com mensagens de email

1. No designer de faixa de faixas, clique na faixa de **ManageTaskPaneRibbon** .

2. Na janela **Propriedades** , clique na lista suspensa ao lado de **RibbonType** e selecione **Microsoft. Outlook. mail. Compose** e **Microsoft. Outlook. mail. Read**.

## <a name="create-a-class-to-manage-inspector-windows-and-custom-task-panes"></a>Criar uma classe para gerenciar janelas de inspetores e painéis de tarefas personalizados
 Há vários casos em que o suplemento do VSTO deve identificar qual painel de tarefas personalizado está associado a uma mensagem de email específica. Esses casos incluem o seguinte:

- Quando o usuário fecha uma mensagem de email. Nesse caso, o suplemento do VSTO deve remover o painel de tarefas personalizado correspondente para garantir que os recursos usados pelo suplemento do VSTO sejam limpos corretamente.

- Quando o usuário fecha o painel de tarefas personalizado. Nesse caso, o suplemento do VSTO deve atualizar o estado do botão de alternância na faixa de opção da mensagem de email.

- Quando o usuário clica no botão de alternância na faixa de opção. Nesse caso, o suplemento do VSTO deve ocultar ou exibir o painel de tarefas correspondente.

  Para habilitar o suplemento do VSTO para manter o controle de qual painel de tarefas personalizado está associado a cada mensagem de email aberta, crie uma classe personalizada que encapsula pares <xref:Microsoft.Office.Interop.Outlook.Inspector> de <xref:Microsoft.Office.Tools.CustomTaskPane> objetos e. Essa classe cria um novo objeto de painel de tarefas personalizado para cada mensagem de email e exclui o painel de tarefas personalizado quando a mensagem de email correspondente é fechada.

### <a name="to-create-a-class-to-manage-inspector-windows-and-custom-task-panes"></a>Para criar uma classe para gerenciar janelas de inspetores e painéis de tarefas personalizados

1. No **Gerenciador de soluções**, clique com o botão direito do mouse no arquivo *ThisAddIn. cs* ou *ThisAddIn. vb* e clique em **Exibir código**.

2. Adicione as instruções a seguir à parte superior do arquivo.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet2":::

3. Adicione o código a seguir ao arquivo *ThisAddIn. cs* ou *ThisAddIn. vb* , fora da `ThisAddIn` classe (para Visual C#, adicione este código dentro do `OutlookMailItemTaskPane` namespace). A `InspectorWrapper` classe gerencia um par de <xref:Microsoft.Office.Interop.Outlook.Inspector> <xref:Microsoft.Office.Tools.CustomTaskPane> objetos e. Você concluirá a definição dessa classe nas etapas a seguir.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet3":::

4. Adicione o Construtor a seguir após o código que você adicionou na etapa anterior. Esse construtor cria e inicializa um novo painel de tarefas personalizado que está associado ao <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto que é passado. No C#, o Construtor também anexa manipuladores de eventos ao <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_Event.Close> evento do <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto e ao <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> evento do <xref:Microsoft.Office.Tools.CustomTaskPane> objeto.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet4":::

5. Adicione o seguinte método após o código que você adicionou na etapa anterior. Esse método é um manipulador de eventos para o <xref:Microsoft.Office.Tools.CustomTaskPane.VisibleChanged> evento do <xref:Microsoft.Office.Tools.CustomTaskPane> objeto que está contido na `InspectorWrapper` classe. Esse código atualiza o estado do botão de alternância sempre que o usuário abre ou fecha o painel de tarefas personalizado.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet5":::

6. Adicione o seguinte método após o código que você adicionou na etapa anterior. Esse método é um manipulador de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorEvents_Event.Close> evento do <xref:Microsoft.Office.Interop.Outlook.Inspector> objeto que contém a mensagem de email atual. O manipulador de eventos libera recursos quando a mensagem de email é fechada. O manipulador de eventos também remove o painel de tarefas personalizado atual da `CustomTaskPanes` coleção. Isso ajuda a evitar várias instâncias do painel de tarefas personalizado quando a próxima mensagem de email é aberta.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet6":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet6":::

7. Adicione o código a seguir após o código que você adicionou na etapa anterior. Mais adiante neste tutorial, você chamará essa propriedade de um método na interface do usuário da faixa de passos personalizada para exibir ou ocultar o painel de tarefas personalizado.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet7":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet7":::

## <a name="initialize-and-clean-up-resources-used-by-the-add-in"></a>Inicializar e limpar os recursos usados pelo suplemento
 Adicione código à `ThisAddIn` classe para inicializar o suplemento do VSTO quando ele for carregado e para limpar os recursos usados pelo suplemento do VSTO quando ele for descarregado. Você inicializa o suplemento do VSTO Configurando um manipulador de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> evento e passando todas as mensagens de email existentes para esse manipulador de eventos. Quando o suplemento do VSTO for descarregado, desanexe o manipulador de eventos e limpe os objetos usados pelo suplemento do VSTO.

### <a name="to-initialize-and-clean-up-resources-used-by-the-vsto-add-in"></a>Para inicializar e limpar os recursos usados pelo suplemento do VSTO

1. No arquivo *ThisAddIn. cs* ou *ThisAddIn. vb* , localize a definição da `ThisAddIn` classe.

2. Adicione as seguintes declarações à `ThisAddIn` classe:

   - O `inspectorWrappersValue` campo contém todos os <xref:Microsoft.Office.Interop.Outlook.Inspector> `InspectorWrapper` objetos e que são gerenciados pelo suplemento do VSTO.

   - O `inspectors` campo mantém uma referência à coleção de janelas de Inspetor na instância atual do Outlook. Essa referência impede que o coletor de lixo libere a memória que contém o manipulador de eventos para o <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> evento, que você irá declarar na próxima etapa.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet8":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet8":::

3. Substitua o método `ThisAddIn_Startup` pelo seguinte código. Esse código anexa um manipulador de eventos ao <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> evento e passa todos <xref:Microsoft.Office.Interop.Outlook.Inspector> os objetos existentes para o manipulador de eventos. Se o usuário carregar o suplemento do VSTO depois que o Outlook já estiver em execução, o suplemento do VSTO usará essas informações para criar painéis de tarefas personalizados para todas as mensagens de email que já estiverem abertas.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet9":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet9":::

4. Substitua o método `ThisAddIn_ShutDown` pelo seguinte código. Esse código desanexa o <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> manipulador de eventos e limpa os objetos usados pelo suplemento do VSTO.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet10":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet10":::

5. Adicione o seguinte <xref:Microsoft.Office.Interop.Outlook.InspectorsEvents_Event.NewInspector> manipulador de eventos à `ThisAddIn` classe. Se um novo <xref:Microsoft.Office.Interop.Outlook.Inspector> contiver uma mensagem de email, o método criará uma instância de um novo `InspectorWrapper` objeto para gerenciar a relação entre a mensagem de email e o painel de tarefas correspondente.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet11":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet11":::

6. Adicione a propriedade a seguir à `ThisAddIn` classe. Essa propriedade expõe o `inspectorWrappersValue` campo particular ao código fora da `ThisAddIn` classe.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ThisAddIn.cs" id="Snippet12":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ThisAddIn.vb" id="Snippet12":::

## <a name="checkpoint"></a>Ponto de verificação
 Crie seu projeto para garantir que ele seja compilado sem erros.

### <a name="to-build-your-project"></a>Para compilar seu projeto

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **OutlookMailItemTaskPane** e clique em **Compilar**. Verifique se o projeto é compilado sem erros.

## <a name="synchronize-the-ribbon-toggle-button-with-the-custom-task-pane"></a>Sincronizar o botão de alternância da faixa de opção com o painel de tarefas personalizado
 O botão de alternância parecerá ser pressionado quando o painel de tarefas estiver visível e parecerá não ser pressionado quando o painel de tarefas estiver oculto. Para sincronizar o estado do botão com o painel de tarefas personalizado, modifique o <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> manipulador de eventos do botão de alternância.

### <a name="to-synchronize-the-custom-task-pane-with-the-toggle-button"></a>Para sincronizar o painel de tarefas personalizado com o botão de alternância

1. No designer de faixa de opção, clique duas vezes no botão de alternância **Mostrar painel de tarefas** .

     O Visual Studio gera automaticamente um manipulador de eventos chamado `toggleButton1_Click` , que manipula o <xref:Microsoft.Office.Tools.Ribbon.RibbonToggleButton.Click> evento do botão de alternância. O Visual Studio também abre o arquivo *ManageTaskPaneRibbon. cs* ou *ManageTaskPaneRibbon. vb* no editor de códigos.

2. Adicione as instruções a seguir à parte superior do arquivo *ManageTaskPaneRibbon. cs* ou *ManageTaskPaneRibbon. vb* .

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.cs" id="Snippet14":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.vb" id="Snippet14":::

3. Substitua o `toggleButton1_Click` manipulador de eventos pelo código a seguir. Quando o usuário clica no botão de alternância, esse método oculta ou exibe o painel de tarefas personalizado que está associado à janela do Inspetor atual.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.cs" id="Snippet15":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_OutlookMailItemTaskPane/ManageTaskPaneRibbon.vb" id="Snippet15":::

## <a name="test-the-project"></a>Testar o projeto
 Quando você inicia a depuração do projeto, o Outlook é aberto e o suplemento do VSTO é carregado. O suplemento do VSTO exibe uma instância exclusiva do painel de tarefas personalizado com cada mensagem de email aberta. Crie várias novas mensagens de email para testar o código.

### <a name="to-test-the-vsto-add-in"></a>Para testar o suplemento do VSTO

1. Pressione **F5**.

2. No Outlook, clique em **novo** para criar uma nova mensagem de email.

3. Na faixa de bits da mensagem de email, clique na guia **suplementos** e, em seguida, clique no botão **Mostrar painel de tarefas** .

    Verifique se um painel de tarefas com o título **meu painel de tarefas** é exibido com a mensagem de email.

4. No painel de tarefas, digite o **primeiro painel de tarefas** na caixa de texto.

5. Feche o painel de tarefas.

    Verifique se o estado do botão **Mostrar painel de tarefas** é alterado para que ele não seja mais pressionado.

6. Clique no botão **Mostrar painel de tarefas** novamente.

    Verifique se o painel de tarefas é aberto e se a caixa de texto ainda contém o **primeiro painel de tarefas** cadeia de caracteres.

7. No Outlook, clique em **novo** para criar uma segunda mensagem de email.

8. Na faixa de bits da mensagem de email, clique na guia **suplementos** e, em seguida, clique no botão **Mostrar painel de tarefas** .

    Verifique se um painel de tarefas com o título **meu painel de tarefas** é exibido com a mensagem de email e se a caixa de texto neste painel de tarefas está vazia.

9. No painel de tarefas, digite o **segundo painel de tarefas** na caixa de texto.

10. Altere o foco para a primeira mensagem de email.

     Verifique se o painel de tarefas que está associado a essa mensagem de email ainda exibe o **primeiro painel de tarefas** na caixa de texto.

    Esse suplemento do VSTO também trata cenários mais avançados que você pode experimentar. Por exemplo, você pode testar o comportamento ao exibir emails usando os botões **próximo item** e **item anterior** . Você também pode testar o comportamento ao descarregar o suplemento do VSTO, abrir várias mensagens de email e recarregar o suplemento do VSTO.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como criar painéis de tarefas personalizados a partir destes tópicos:

- Crie um painel de tarefas personalizado em um suplemento do VSTO para um aplicativo diferente. Para obter mais informações sobre os aplicativos que dão suporte a painéis de tarefas personalizados, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).

- Automatize um aplicativo Microsoft Office usando um painel de tarefas personalizado. Para obter mais informações, consulte [Walkthrough: automatizar um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md).

- Crie um botão da faixa de medida no Excel que possa ser usado para ocultar ou exibir um painel de tarefas personalizado. Para obter mais informações, consulte [Walkthrough: sincronizar um painel de tarefas personalizado com um botão Ribbon](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md).

## <a name="see-also"></a>Consulte também
- [Painéis de tarefas personalizados](../vsto/custom-task-panes.md)
- [Como: adicionar um painel de tarefas personalizado a um aplicativo](../vsto/how-to-add-a-custom-task-pane-to-an-application.md)
- [Walkthrough: automatizar um aplicativo de um painel de tarefas personalizado](../vsto/walkthrough-automating-an-application-from-a-custom-task-pane.md)
- [Walkthrough: sincronizar um painel de tarefas personalizado com um botão da faixa de das](../vsto/walkthrough-synchronizing-a-custom-task-pane-with-a-ribbon-button.md)
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [Visão geral do modelo de objeto do Outlook](../vsto/outlook-object-model-overview.md)
- [Acessar a faixa de faixas em tempo de execução](../vsto/accessing-the-ribbon-at-run-time.md)
