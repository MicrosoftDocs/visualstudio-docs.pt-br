---
title: 'Passo a passo: Importar de uma região de formulário projetada no Outlook'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- importing form regions
- form regions [Office development in Visual Studio], importing
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 413d2fed56da809b2fdb8c1fad867818e0cce010
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49903511"
---
# <a name="walkthrough-import-a-form-region-that-is-designed-in-outlook"></a>Passo a passo: Importar de uma região de formulário projetada no Outlook
  Este passo a passo demonstra como criar uma região de formulário no Microsoft Office Outlook e, em seguida, importe a região do formulário para um projeto de suplemento do VSTO do Outlook usando o **nova região de formulário** assistente. Criando a região de formulário do Outlook torna possível para adicionar controles nativos do Outlook para a região de formulário associar a dados do Outlook. Depois de importar a região do formulário, você pode manipular os eventos de cada controle.  
  
 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
- Criando uma região de formulário usando o designer de região de formulário do Outlook.  
  
- Importando uma região de formulário para um projeto de suplemento do VSTO do Outlook.  
  
- Manipulando os eventos de controles na região do formulário.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   [!INCLUDE[Outlook_15_short](../vsto/includes/outlook-15-short-md.md)] ou [!INCLUDE[Outlook_14_short](../vsto/includes/outlook-14-short-md.md)].  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
 ![link para vídeo](../vsto/media/playvideo.gif "link para vídeo") para uma demonstração em vídeo relacionada, consulte [How do i: Criar formulário do Outlook usando o Visual Studio 2008?](http://go.microsoft.com/fwlink/?LinkID=130305).  
## <a name="design-a-form-region-by-using-the-form-region-designer-in-outlook"></a>Cria uma região de formulário usando o designer de região de formulário do Outlook  
 Nesta etapa, você criará uma região de formulário do Outlook. Em seguida, você irá salvar em um local fácil de encontrar a região do formulário para que você pode importá-lo para [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
 Esta região do formulário de exemplo substitui completamente o formulário de tarefa comum. Ele fornece uma maneira de acompanhar o progresso de todas as tarefas que devem ser concluídas antes que a tarefa principal possa ser executada (tarefas de pré-requisito). A região do formulário exibe uma lista de tarefas de pré-requisito e mostra o status de conclusão para cada tarefa na lista. Os usuários podem adicionar tarefas à lista e removê-los. Eles também podem atualizar o status de conclusão de cada tarefa.  
  
### <a name="to-design-a-form-region-by-using-the-form-region-designer-in-outlook"></a>Para criar uma região de formulário usando o designer de região de formulário do Outlook  
  
1.  Inicie o Microsoft Office Outlook.  
  
2.  No Outlook, sobre o **Developer** , clique em **criar um formulário**. Para obter mais informações, consulte [como: Mostrar a guia Desenvolvedor na faixa de opções](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md).  
  
3.  No **Design Form** , clique em **tarefa**e, em seguida, clique em **abrir**.  
  
4.  No Outlook, na **desenvolvedor** guia o **Design** , clique em **nova região de formulário**.  
  
     Abre uma nova região de formulário. Se o **seletor de campos** não aparecer, clique em **seletor de campo** no **ferramentas** grupo.  
  
5.  Arraste o **assunto** campo e o **% concluída** campo o **seletor de campo** à região do formulário.  
  
6.  No **ferramentas** , clique em **ferramentas de controle** para abrir o **caixa de ferramentas**.  
  
7.  Arraste um rótulo da **caixa de ferramentas** para a região do formulário. Posição do rótulo abaixo de **assunto** e **% concluída** campos.  
  
8.  Clique com botão direito no rótulo e, em seguida, clique em **propriedades avançadas**.  
  
9. No **propriedades** janela, defina as **legenda** propriedade a ser **essa tarefa depende das tarefas a seguir**, defina o **largura** propriedade para **200**e, em seguida, clique em **aplicar**.  
  
10. Arraste um controle de caixa de listagem dos **caixa de ferramentas** para a região do formulário. Posicione a caixa de listagem sob o **essa tarefa depende das tarefas a seguir** rótulo.  
  
11. Marque a caixa de lista que você acabou de adicionar.  
  
12. No **propriedades** janela, defina **largura** para **300**e, em seguida, clique em **aplicar**.  
  
13. Arraste um rótulo da **caixa de ferramentas** para a região do formulário. Posição do rótulo abaixo da caixa de listagem.  
  
14. Selecione o rótulo que você acabou de adicionar.  
  
15. No **propriedades** janela, defina as **legenda** propriedade a ser **selecione uma tarefa para adicionar à lista de tarefas dependentes**, defina o **largura** propriedade para **200**e, em seguida, clique em **aplicar**.  
  
16. Arraste um controle de caixa de combinação dos **caixa de ferramentas** para a região do formulário. Posicione a caixa de combinação sob o **selecione uma tarefa para adicionar à lista de tarefas dependentes** rótulo.  
  
17. Marque a caixa de combinação que você acabou de adicionar.  
  
18. No **propriedades** janela, defina as **largura** propriedade a ser **300**e, em seguida, clique em **aplicar**.  
  
19. Arraste um controle CommandButton dos **caixa de ferramentas** para a região do formulário. Posição do botão de comando ao lado da caixa de combinação.  
  
20. Selecione o botão de comando que você acabou de adicionar.  
  
21. No **propriedades** janela, defina **nome** para **AddDependentTask**, defina **legenda** para **adicionar tarefa dependente**, defina **largura** para **100**e, em seguida, clique em **aplicar**.  
  
22. No **seletor de campos**, clique em **New**.  
  
23. No **novo campo** caixa de diálogo, digite **hiddenField** no **nome** campo e, em seguida, clique em **Okey**.  
  
24. Arraste o **hiddenField** campo o **seletor de campo** à região do formulário.  
  
25. No **propriedades** janela, defina **Visible** para **0 - FALSO**e, em seguida, clique em **aplicar**.  
  
26. No Outlook, na **Developer** guia da **Design** , clique no **salvar** e, em seguida, clique **salvar região de formulário como**.  
  
     O nome da região de formulário **TaskFormRegion** e salvá-lo em um diretório local no seu computador.  
  
     O Outlook salva a região do formulário como um armazenamento de formulário do Outlook (*ofs*) arquivos. A região do formulário é salvo com o nome *TaskFormRegion.ofs*.  
  
27. Saia do Outlook.  
  
## <a name="create-a-new-outlook-add-in-project"></a>Criar um novo projeto de suplemento do Outlook  
 Nesta etapa, você criará um projeto de suplemento do VSTO do Outlook. Posteriormente neste passo a passo, você importará a região do formulário ao projeto.  
  
### <a name="to-create-a-new-outlook-vsto-add-in-project"></a>Para criar um novo projeto de suplemento do VSTO do Outlook  
  
1.  Na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], crie um projeto de suplemento do VSTO do Outlook com o nome **TaskAddIn**.  
  
2.  No **novo projeto** caixa de diálogo, selecione **criar diretório para solução**.  
  
3.  Salve o projeto no diretório de projeto padrão.  
  
     Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
## <a name="import-the-form-region"></a>Importar a região do formulário  
 Você pode importar a região do formulário projetada no Outlook para o projeto de suplemento do VSTO do Outlook usando o **nova região de formulário do Outlook** assistente.  
  
### <a name="to-import-the-form-region-into-the-outlook-vsto-add-in-project"></a>Para importar a região do formulário para o projeto de suplemento do VSTO do Outlook  
  
1.  No **Gerenciador de soluções**, com o botão direito do **TaskAddIn** do projeto, aponte para **Add**e, em seguida, clique em **Novo Item**.  
  
2.  No **modelos** painel, selecione **região de formulário do Outlook**, nomeie o arquivo **TaskFormRegion**e, em seguida, clique em **adicionar**.  
  
     O **região do formulário NewOutlook** assistente é iniciado.  
  
3.  Sobre o **selecione como você deseja criar a região do formulário** , clique em **importar de um armazenamento de formulário do Outlook (. ofs) arquivo**e, em seguida, clique em **procurar**.  
  
4.  No **arquivo local de região de formulário Outlook existente** caixa de diálogo, navegue até o local do *TaskFormRegion.ofs*, selecione **TaskFormRegion.ofs**, clique em **Abertos**e, em seguida, clique em **próxima**.  
  
5.  Sobre o **selecione o tipo da região de formulário que você deseja criar** , clique em **Substituir tudo**e, em seguida, clique em **próxima**.  
  
     Um *Substituir tudo* região do formulário substitui todo o formulário do Outlook. Para obter mais informações sobre os tipos de região de formulário, consulte [regiões de formulário do Outlook criar](../vsto/creating-outlook-form-regions.md).  
  
6.  Sobre o **fornecer um texto descritivo e selecionar suas preferências de exibição** , clique em **próxima**.  
  
7.  No **identificar as classes de mensagem que exibirão esta região do formulário** página, o **quais classes de mensagem personalizadas exibirão esta região do formulário** , digite **IPM. Task.TaskFormRegion**e, em seguida, clique em **concluir**.  
  
     Um *TaskFormRegion.cs* ou *TaskFormRegion.vb* arquivo é adicionado ao seu projeto.  
  
## <a name="handle-the-events-of-controls-on-the-form-region"></a>Manipular os eventos de controles na região do formulário  
 Agora que você tem a região do formulário no projeto, você pode adicionar código que manipula o `Microsoft.Office.Interop.Outlook.OlkCommandButton.Click` evento do botão que você adicionou à região de formulário do Outlook.  
  
 Além disso, adicione código para o <xref:Microsoft.Office.Tools.Outlook.FormRegionControl.FormRegionShowing> evento que atualiza os controles na região do formulário quando a região de formulário é exibida.  
  
### <a name="to-handle-the-events-of-controls-on-the-form-region"></a>Para tratar os eventos de controles na região do formulário  
  
1. Na **Gerenciador de soluções**, clique com botão direito *TaskFormRegion.cs* ou *TaskFormRegion.vb*e, em seguida, clique em **Exibir código**.  
  
    *TaskFormRegion.cs* ou *TaskFormRegion.vb* é aberto no Editor de códigos.  
  
2. Adicione o seguinte código para o `TaskFormRegion` classe. Esse código preenche a caixa de combinação na região do formulário com a linha de assunto de cada tarefa da pasta de tarefas do Outlook.  
  
    [!code-csharp[Trin_Outlook_FR_Import#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs#1)]
    [!code-vb[Trin_Outlook_FR_Import#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb#1)]  
  
3. Adicione o seguinte código para o `TaskFormRegion` classe. Esse código executa as seguintes tarefas:  
  
   - Localiza o `Microsoft.Office.Interop.Outlook.TaskItem` na pasta tarefas chamando o `FindTaskBySubjectName` método auxiliar e passando o assunto da tarefa desejada. Você adicionará o `FindTaskBySubjectName` método auxiliar na próxima etapa.  
  
   - Adiciona o `Microsoft.Office.Interop.Outlook.TaskItem.Subject` e `Microsoft.Office.Interop.Outlook.TaskItem.PercentComplete` valores à caixa de listagem de tarefa dependente.  
  
   - Adiciona o assunto da tarefa para o campo oculto na região do formulário. O campo oculto armazena esses valores como parte do item do Outlook.  
  
     [!code-csharp[Trin_Outlook_FR_Import#2](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs#2)]
     [!code-vb[Trin_Outlook_FR_Import#2](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb#2)]  
  
4. Adicione o seguinte código para o `TaskFormRegion` classe. Esse código fornece o método auxiliar `FindTaskBySubjectName` que foi descrito na etapa anterior.  
  
    [!code-csharp[Trin_Outlook_FR_Import#3](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs#3)]
    [!code-vb[Trin_Outlook_FR_Import#3](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb#3)]  
  
5. Adicione o seguinte código para o `TaskFormRegion` classe. Esse código executa as seguintes tarefas:  
  
   - Atualiza a caixa de listagem na região do formulário com o atual status de conclusão de cada tarefa dependente.  
  
   - Analisa o campo de texto oculto para obter o assunto de cada tarefa dependente. Em seguida, localiza cada `Microsoft.Office.Interop.Outlook.TaskItem` no *tarefas* pasta chamando o `FindTaskBySubjectName` método auxiliar e passando o assunto de cada tarefa.  
  
   - Adiciona o `Microsoft.Office.Interop.Outlook.TaskItem.Subject` e `Microsoft.Office.Interop.Outlook.TaskItem.PercentComplete` valores à caixa de listagem de tarefa dependente.  
  
     [!code-csharp[Trin_Outlook_FR_Import#4](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs#4)]
     [!code-vb[Trin_Outlook_FR_Import#4](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb#4)]  
  
6. Substitua o `TaskFormRegion_FormRegionShowing` manipulador de eventos com o código a seguir. Esse código executa as seguintes tarefas:  
  
   - Preenche a caixa de combinação na região do formulário com assuntos das tarefas quando a região de formulário é exibida.  
  
   - Chamadas a `RefreshTaskListBox` método auxiliar quando a região de formulário é exibida. Isso exibe as tarefas dependentes que foram adicionadas à caixa de listagem, quando o item foi aberto anteriormente.  
  
     [!code-csharp[Trin_Outlook_FR_Import#5](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Import/TaskFormRegion.cs#5)]
     [!code-vb[Trin_Outlook_FR_Import#5](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Import_O12/TaskFormRegion.vb#5)]  
  
## <a name="test-the-outlook-form-region"></a>Testar a região de formulário do Outlook  
 Para testar a região do formulário, adicione tarefas à lista de tarefas de pré-requisito na região do formulário. Atualizar o status de conclusão de uma tarefa de pré-requisitos e, em seguida, exibir o status de conclusão atualizadas da tarefa na lista de tarefas de pré-requisito.  
  
### <a name="to-test-the-form-region"></a>Para testar a região do formulário  
  
1.  Pressione **F5** para executar o projeto.  
  
     O Outlook inicia.  
  
2.  No Outlook, sobre o **Home** , clique em **novos itens**e, em seguida, clique em **tarefa**.  
  
3.  No formulário de tarefa, digite **tarefa dependente** na **assunto** campo.  
  
4.  Sobre o **tarefa** guia da faixa de opções, no **ações** de grupo, clique em **salvar e fechar**.  
  
5.  No Outlook, sobre o **Home** , clique em **novos itens**, clique em **mais itens**e, em seguida, clique em **Escolher formulário**.  
  
6.  No **Escolher formulário** caixa de diálogo, clique em **TaskFormRegion**e, em seguida, clique em **abrir**.  
  
     O **TaskFormRegion** região do formulário é exibida. Este formulário substitui o formulário de tarefa inteira. O **selecione uma tarefa para adicionar à lista de tarefas dependentes** caixa de combinação é preenchida com outras tarefas na pasta tarefas.  
  
7.  No formulário de tarefa, na **assunto** , digite **tarefa principal**.  
  
8.  No **selecione uma tarefa para adicionar à lista de tarefas dependentes** caixa de combinação, selecione **tarefa dependente**e, em seguida, clique em **adicionar tarefa dependente**.  
  
     **0% concluída--tarefa dependente** aparece na **essa tarefa depende das tarefas a seguir** caixa de listagem. Isso demonstra que você tratado com êxito o `Microsoft.Office.Interop.Outlook.OlkCommandButton.Click` evento do botão.  
  
9. Salve e feche o **tarefa principal** item.  
  
10. Reabra o item de tarefa dependente no Outlook.  
  
11. No formulário de tarefa dependente, alterar o **% concluída** campo **50%**.  
  
12. No **tarefa** guia da faixa de opções tarefa dependente, no **ações** , clique em **salvar e fechar**.  
  
13. Reabra o **tarefa principal** item no Outlook.  
  
     **50% concluída--tarefa dependente** agora aparece na **essa tarefa depende das tarefas a seguir** caixa de listagem.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre como personalizar a interface do usuário de um aplicativo do Outlook com estes tópicos:  
  
-   Para saber mais sobre como criar a aparência de uma região de formulário ao arrastar controles gerenciados em um designer visual, consulte [instruções passo a passo: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md).  
  
-   Para saber mais sobre como personalizar a faixa de opções de um item do Outlook, consulte [personalizar uma faixa de opções para Outlook](../vsto/customizing-a-ribbon-for-outlook.md).  
  
-   Para saber mais sobre como adicionar um painel de tarefas personalizado para o Outlook, consulte [painéis de tarefas personalizados](../vsto/custom-task-panes.md).  
  
## <a name="see-also"></a>Consulte também  
 [Acessar uma região de formulário em tempo de execução](../vsto/accessing-a-form-region-at-run-time.md)   
 [Criar regiões de formulário do Outlook](../vsto/creating-outlook-form-regions.md)   
 [Diretrizes para criar regiões de formulário do Outlook](../vsto/guidelines-for-creating-outlook-form-regions.md)   
 [Passo a passo: Criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md)   
 [Como: adicionar uma região de formulário a um projeto de suplemento do Outlook](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)   
 [Associar uma região de formulário uma classe de mensagem do Outlook](../vsto/associating-a-form-region-with-an-outlook-message-class.md)   
 [Personalizar ações em regiões de formulário do Outlook](../vsto/custom-actions-in-outlook-form-regions.md)   
 [Como: evitar que o Outlook exiba uma região de formulário](../vsto/how-to-prevent-outlook-from-displaying-a-form-region.md)  
  
  