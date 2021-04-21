---
title: 'Walkthrough: importar uma região de formulário projetada no Outlook'
description: Saiba como criar uma região de formulário no Microsoft Outlook e, em seguida, importar a região de formulário para um projeto de suplemento do VSTO do Outlook usando o assistente de nova região de formulário.
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- importing form regions
- form regions [Office development in Visual Studio], importing
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 4ce8c334be74f2643bfc7fa263b01a74db109eb7
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107827741"
---
# <a name="walkthrough-import-a-form-region-that-is-designed-in-outlook"></a>Walkthrough: importar uma região de formulário projetada no Outlook
  Este tutorial demonstra como criar uma região de formulário no Microsoft Office Outlook e, em seguida, importar a região de formulário para um projeto de suplemento do VSTO do Outlook usando o assistente de **nova região de formulário** . A criação da região de formulário no Outlook possibilita que você adicione controles nativos do Outlook à região do formulário que se associam aos dados do Outlook. Depois de importar a região do formulário, você pode manipular os eventos de cada controle.

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Criar uma região de formulário usando o designer de região de formulário no Outlook.

- Importando uma região de formulário para um projeto de suplemento do VSTO do Outlook.

- Manipulando os eventos de controles na região do formulário.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- [!INCLUDE[Outlook_15_short](../vsto/includes/outlook-15-short-md.md)] ou [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)].

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="design-a-form-region-by-using-the-form-region-designer-in-outlook"></a>Criar uma região de formulário usando o designer de região de formulário no Outlook
 Nesta etapa, você criará uma região de formulário no Outlook. Em seguida, você salvará a região do formulário em um local fácil de encontrar para que possa importá-la para o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

 Esta região de formulário de exemplo substitui completamente o formulário de tarefa usual. Ele fornece uma maneira de acompanhar o progresso de todas as tarefas que devem ser concluídas antes que a tarefa principal possa ser executada (tarefas de pré-requisito). A região de formulário exibe uma lista das tarefas de pré-requisito e mostra o status de conclusão de cada tarefa na lista. Os usuários podem adicionar tarefas à lista e removê-las. Eles também podem atualizar o status de conclusão de cada tarefa.

### <a name="to-design-a-form-region-by-using-the-form-region-designer-in-outlook"></a>Para criar uma região de formulário usando o designer de região de formulário no Outlook

1. Inicie o Microsoft Office Outlook.

2. No Outlook, na guia **desenvolvedor** , clique em **criar um formulário**. Para obter mais informações, consulte [como: mostrar a guia Desenvolvedor na faixa de faixas](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).

3. Na caixa **formulário de design** , clique em **tarefa** e, em seguida, clique em **abrir**.

4. No Outlook, na guia **desenvolvedor** , no grupo **design** , clique em **nova região de formulário**.

     Uma nova região de formulário é aberta. Se o **seletor de campo** não aparecer, clique em **seletor de campo** no grupo **ferramentas** .

5. Arraste o campo **assunto** e o campo **% Complete** do **seletor de campo** para a região de formulário.

6. No grupo **ferramentas** , clique em **caixa de ferramentas de controle** para abrir a **caixa de ferramentas**.

7. Arraste um rótulo da **caixa de ferramentas** para a região do formulário. Posicione o rótulo abaixo dos campos **assunto** e **% completo** .

8. Clique com o botão direito do mouse no rótulo e clique em **Propriedades avançadas**.

9. Na janela **Propriedades** , defina a propriedade **legenda** como **esta tarefa depende das seguintes tarefas**, defina a propriedade **largura** como **200** e clique em **aplicar**.

10. Arraste um controle ListBox da **caixa de ferramentas** para a região do formulário. Posicionar a caixa de listagem abaixo **dessa tarefa depende do rótulo de tarefas a seguir** .

11. Selecione a caixa de listagem que você acabou de adicionar.

12. Na janela **Propriedades** , defina **largura** como **300** e clique em **aplicar**.

13. Arraste um rótulo da **caixa de ferramentas** para a região do formulário. Posicione o rótulo abaixo da caixa de listagem.

14. Selecione o rótulo que você acabou de adicionar.

15. Na janela **Propriedades** , defina a propriedade **legenda** para **selecionar uma tarefa a ser adicionada à lista de tarefas dependentes**, defina a **Propriedade largura** como **200** e clique em **aplicar**.

16. Arraste um controle ComboBox da **caixa de ferramentas** para a região do formulário. Posicione a caixa de combinação sob a **seleção selecionar uma tarefa a ser adicionada ao rótulo lista de tarefas dependentes** .

17. Selecione a caixa de combinação que você acabou de adicionar.

18. Na janela **Propriedades** , defina a propriedade **largura** como **300** e clique em **aplicar**.

19. Arraste um controle CommandButton da **caixa de ferramentas** para a região do formulário. Posicione o botão de comando ao lado da caixa de combinação.

20. Selecione o botão de comando que você acabou de adicionar.

21. Na janela **Propriedades** , defina **nome** como **AddDependentTask**, defina **legenda** para **Adicionar tarefa dependente**, defina **largura** como **100** e clique em **aplicar**.

22. No **seletor de campo**, clique em **novo**.

23. Na caixa de diálogo **novo campo** , digite **HiddenField** no campo **nome** e clique em **OK**.

24. Arraste o campo **HiddenField** do **seletor de campo** para a região de formulário.

25. Na janela **Propriedades** , defina **visível** como **0-falso** e clique em **aplicar**.

26. No Outlook, na guia **desenvolvedor** , no grupo **design** , clique no botão **salvar** e, em seguida, clique em **Salvar região de formulário como**.

     Nomeie a região de formulário **TaskFormRegion** e salve-a em um diretório local em seu computador.

     O Outlook salva a região do formulário como um arquivo de armazenamento de formulário do Outlook (*. OFS*). A região de formulário é salva com o nome *TaskFormRegion. OFS*.

27. Saia do Outlook.

## <a name="create-a-new-outlook-add-in-project"></a>Criar um novo projeto de suplemento do Outlook
 Nesta etapa, você criará um projeto de suplemento do VSTO do Outlook. Mais adiante neste tutorial, você importará a região do formulário para o projeto.

### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>Para criar um novo projeto de suplemento do VSTO do Outlook

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , crie um projeto de suplemento do VSTO do Outlook com o nome **TaskAddIn**.

2. Na caixa de diálogo **novo projeto** , selecione **criar diretório para solução**.

3. Salve o projeto no diretório de projeto padrão.

     Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

## <a name="import-the-form-region"></a>Importar a região do formulário
 Você pode importar a região de formulário que você criou no Outlook para o projeto de suplemento do VSTO do Outlook usando o assistente de **nova região de formulário do Outlook** .

### <a name="to-import-the-form-region-into-the-outlook-vsto-add-in-project"></a>Para importar a região de formulário para o projeto de suplemento do VSTO do Outlook

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **TaskAddIn** , aponte para **Adicionar** e clique em **novo item**.

2. No painel **modelos** , selecione **região de formulário do Outlook**, nomeie o arquivo **TaskFormRegion** e clique em **Adicionar**.

     O assistente de **região de formulário NewOutlook** é iniciado.

3. Na página **Selecione como você deseja criar a região do formulário** , clique em **importar um arquivo de armazenamento de formulário do Outlook (. ofs)** e, em seguida, clique em **procurar**.

4. Na caixa de diálogo **local do arquivo de região de formulário do Outlook existente** , navegue até o local de *TaskFormRegion. OFS*, selecione **TaskFormRegion. OFS**, clique em **abrir** e, em seguida, clique em **Avançar**.

5. Na página **Selecione o tipo de região de formulário que você deseja criar** , clique em **substituir** e em **Avançar**.

     Uma região de formulário *substituir tudo* substitui todo o formulário do Outlook. Para obter mais informações sobre tipos de região de formulário, consulte [criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md).

6. No **texto descritivo do fornecimento e selecione sua página preferências de exibição** , clique em **Avançar**.

7. Na página **identificar as classes de mensagem que exibirão esta região de formulário** , no campo as **classes de mensagens personalizadas que exibirão este formulário de região** , digite **IPM. Task. TaskFormRegion** e clique em **concluir**.

     Um arquivo *TaskFormRegion. cs* ou *TaskFormRegion. vb* é adicionado ao seu projeto.

## <a name="handle-the-events-of-controls-on-the-form-region"></a>Manipular os eventos de controles na região do formulário
 Agora que você tem a região de formulário no projeto, é possível adicionar código que manipula o `Microsoft.Office.Interop.Outlook.OlkCommandButton.Click` evento do botão que você adicionou à região de formulário no Outlook.

 Além disso, adicione o código ao <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> evento que atualiza os controles na região do formulário quando a região do formulário é exibida.

### <a name="to-handle-the-events-of-controls-on-the-form-region"></a>Para manipular os eventos de controles na região do formulário

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em *TaskFormRegion. cs* ou *TaskFormRegion. vb* e clique em **Exibir código**.

    O *TaskFormRegion. cs* ou o *TaskFormRegion. vb* é aberto no editor de códigos.

2. Adicione o código a seguir à classe `TaskFormRegion` . Esse código popula a caixa de combinação na região de formulário com a linha de assunto de cada tarefa da pasta tarefas do Outlook.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs" id="Snippet1":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb" id="Snippet1":::

3. Adicione o código a seguir à classe `TaskFormRegion` . Esse código executa as seguintes tarefas:

   - Localiza o `Microsoft.Office.Interop.Outlook.TaskItem` na pasta tarefas chamando o `FindTaskBySubjectName` método auxiliar e passando o assunto da tarefa desejada. Você adicionará o `FindTaskBySubjectName` método auxiliar na próxima etapa.

   - Adiciona os `Microsoft.Office.Interop.Outlook.TaskItem.Subject` `Microsoft.Office.Interop.Outlook.TaskItem.PercentComplete` valores e à caixa de listagem de tarefas dependente.

   - Adiciona o assunto da tarefa ao campo oculto na região do formulário. O campo oculto armazena esses valores como parte do item do Outlook.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb" id="Snippet2":::

4. Adicione o código a seguir à classe `TaskFormRegion` . Esse código fornece o método auxiliar `FindTaskBySubjectName` que foi descrito na etapa anterior.

    :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs" id="Snippet3":::
    :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb" id="Snippet3":::

5. Adicione o código a seguir à classe `TaskFormRegion` . Esse código executa as seguintes tarefas:

   - Atualiza a caixa de listagem na região do formulário com o status de conclusão atual de cada tarefa dependente.

   - Analisa o campo de texto oculto para obter o assunto de cada tarefa dependente. Em seguida, ele localiza cada uma delas `Microsoft.Office.Interop.Outlook.TaskItem` na pasta *tarefas* chamando o `FindTaskBySubjectName` método auxiliar e passando o assunto de cada tarefa.

   - Adiciona os `Microsoft.Office.Interop.Outlook.TaskItem.Subject` `Microsoft.Office.Interop.Outlook.TaskItem.PercentComplete` valores e à caixa de listagem de tarefas dependente.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs" id="Snippet4":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb" id="Snippet4":::

6. Substitua o `TaskFormRegion_FormRegionShowing` manipulador de eventos pelo código a seguir. Esse código executa as seguintes tarefas:

   - Popula a caixa de combinação na região do formulário com os assuntos da tarefa quando a região do formulário é exibida.

   - Chama o `RefreshTaskListBox` método auxiliar quando a região de formulário é exibida. Isso exibe as tarefas dependentes que foram adicionadas à caixa de listagem quando o item foi aberto anteriormente.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs" id="Snippet5":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb" id="Snippet5":::

## <a name="test-the-outlook-form-region"></a>Testar a região de formulário do Outlook
 Para testar a região do formulário, adicione tarefas à lista de tarefas de pré-requisito na região do formulário. Atualize o status de conclusão de uma tarefa de pré-requisito e, em seguida, exiba o status de conclusão atualizado da tarefa na lista de tarefas pré-requisito.

### <a name="to-test-the-form-region"></a>Para testar a região do formulário

1. Pressione **F5** para executar o projeto.

     O Outlook é iniciado.

2. No Outlook, na guia **início** , clique em **novos itens** e em **tarefa**.

3. No formulário tarefa, digite **tarefa dependente** no campo **assunto** .

4. Na guia **tarefa** da faixa de, no grupo **ações** , clique em **salvar & fechar**.

5. No Outlook, na guia **início** , clique em **novos itens**, clique em **mais itens** e, em seguida, clique em **escolher formulário**.

6. Na caixa de diálogo **escolher formulário** , clique em **TaskFormRegion** e em **abrir**.

     A região de formulário **TaskFormRegion** é exibida. Esse formulário substitui todo o formulário de tarefa. A caixa de combinação **selecionar uma tarefa a ser adicionada à lista de tarefas dependentes** é preenchida com outras tarefas na pasta tarefas.

7. No formulário de tarefas, no campo **assunto** , digite **tarefa principal**.

8. Na caixa de combinação **selecionar uma tarefa a ser adicionada à lista de tarefas dependentes** , selecione **tarefa dependente** e clique em **Adicionar tarefa dependente**.

     **0% concluído--a tarefa dependente** aparece na caixa de listagem **esta tarefa depende da seguinte lista de tarefas** . Isso demonstra que você tratou com êxito o `Microsoft.Office.Interop.Outlook.OlkCommandButton.Click` evento do botão.

9. Salve e feche o item de **tarefa principal** .

10. Reabra o item de tarefa dependente no Outlook.

11. No formulário de tarefa dependente, altere o campo **% Complete** para **50%**.

12. Na guia **tarefa** da faixa de tarefas dependente, no grupo **ações** , clique em **salvar & fechar**.

13. Reabra o item de **tarefa principal** no Outlook.

     **50% concluído – a tarefa dependente** agora aparece na caixa de listagem **esta tarefa depende da seguinte lista de tarefas** .

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como personalizar a interface do usuário de um aplicativo do Outlook a partir destes tópicos:

- Para saber mais sobre como criar a aparência de uma região de formulário arrastando controles gerenciados para um designer visual, consulte [passo a passos: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md).

- Para saber mais sobre como personalizar a faixa de visualização de um item do Outlook, confira [personalizar uma faixa de visualização para o Outlook](../vsto/customizing-a-ribbon-for-outlook.md).

- Para saber mais sobre como adicionar um painel de tarefas personalizado ao Outlook, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).

## <a name="see-also"></a>Consulte também
- [Acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)
- [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)
- [Diretrizes para criar regiões de formulário do Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)
- [Walkthrough: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [Como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [Associar uma região de formulário a uma classe de mensagem do Outlook](../vsto/associating-a-form-region-with-an-outlook-message-class.md)
- [Ações personalizadas nas regiões de formulário do Outlook](../vsto/custom-actions-in-outlook-form-regions.md)
- [Como: impedir que o Outlook exiba uma região de formulário](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)
