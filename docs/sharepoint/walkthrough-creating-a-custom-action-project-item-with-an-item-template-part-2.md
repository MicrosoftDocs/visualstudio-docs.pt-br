---
title: 'Passo a passo: Criando um Item de projeto de ação personalizado com um modelo de Item, parte 2 | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], creating template wizards
- SharePoint project items, creating template wizards
- SharePoint development in Visual Studio, defining new project item types
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 2c37ab6f42be8e363dcba8a3e2aa6ef78816bff0
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296236"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-2"></a>Passo a passo: Criar um item de projeto de ação personalizado com um modelo de item, parte 2
  Depois de definir um tipo personalizado de item de projeto do SharePoint e associá-lo a um modelo de item no Visual Studio, você também poderá fornecer um assistente do modelo. Você pode usar o Assistente para coletar informações dos usuários quando eles usam seu modelo para adicionar uma nova instância do item de projeto a um projeto. As informações que você coleta podem ser usadas para inicializar o item de projeto.  
  
 Neste passo a passo, você adicionará um Assistente para o item de projeto de ação personalizada que é demonstrado [instruções passo a passo: criar um item de projeto de ação personalizado com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md). Quando um usuário adiciona um item de projeto de ação personalizada para um projeto do SharePoint, o assistente coleta informações sobre a ação personalizada (como sua localização e a URL para navegar quando um usuário final escolhe-lo) e adiciona essas informações para o *Elements. XML* arquivos no novo item de projeto.  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
-   Criando um Assistente para um tipo de item de projeto do SharePoint personalizado que está associado um modelo de item.  
  
-   Definindo um assistente personalizado da interface do usuário que se parece com os assistentes internos para itens de projeto do SharePoint no Visual Studio.  
  
-   Usando parâmetros substituíveis para inicializar os arquivos de projeto do SharePoint com os dados coletados no assistente.  
  
-   Depurando e testando o assistente.  
  
> [!NOTE]  
>  Você pode baixar um exemplo de [Github](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) que mostra como criar atividades personalizadas para um fluxo de trabalho.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar este passo a passo, você deve primeiro criar a solução CustomActionProjectItem completando [instruções passo a passo: criar um item de projeto de ação personalizado com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md).  
  
 Você também precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passo:  
  
- Edições com suporte do Windows, SharePoint e Visual Studio.
  
- O SDK do Visual Studio. Este passo a passo usa o **VSIX Project** modelo no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).  
  
  Conhecimento dos conceitos a seguir é útil, mas não necessário para concluir o passo a passo:  
  
- Assistentes para modelos de projeto e item no Visual Studio. Para obter mais informações, consulte [como: usar assistentes com modelos de projeto](../extensibility/how-to-use-wizards-with-project-templates.md) e o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface.  
  
- Ações personalizadas no SharePoint. Para obter mais informações, consulte [ação personalizada](http://go.microsoft.com/fwlink/?LinkId=177800).  
  
## <a name="create-the-wizard-project"></a>Criar o projeto de Assistente
 Para concluir este passo a passo, você deve adicionar um projeto à solução CustomActionProjectItem que você criou na [instruções passo a passo: criar um item de projeto de ação personalizado com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md). Você implementará o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> de interface e definir o Assistente de interface do usuário neste projeto.  
  
#### <a name="to-create-the-wizard-project"></a>Para criar o projeto de Assistente  
  
1.  No Visual Studio, abra a solução de CustomActionProjectItem  
  
2.  Na **Gerenciador de soluções**, abra o menu de atalho do nó da solução, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
3.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha o **Windows** nó.  
  
4.  Na parte superior a **novo projeto** diálogo caixa, certifique-se de que **.NET Framework 4.5** for escolhido na lista de versões do .NET Framework.  
  
5.  Escolha o **biblioteca de controle de usuário do WPF** modelo de projeto, nomeie o projeto **ItemTemplateWizard**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **ItemTemplateWizard** projeto à solução.  
  
6.  Exclua o item de UserControl1 do projeto.  
  
## <a name="configure-the-wizard-project"></a>Configurar o projeto de Assistente
 Antes de criar o assistente, você deve adicionar uma janela do Windows Presentation Foundation (WPF), um arquivo de código e referências de assembly ao projeto.  
  
#### <a name="to-configure-the-wizard-project"></a>Para configurar o projeto de Assistente  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do **ItemTemplateWizard** nó do projeto e, em seguida, escolha **propriedades**.  
  
2.  No **Designer de projeto**, certifique-se de que a estrutura de destino é definida como o .NET Framework 4.5.  
  
     Para projetos do Visual c#, você pode definir esse valor sobre o **aplicativo** guia. Para projetos do Visual Basic, você pode definir esse valor na **compilar** guia. Para obter mais informações, consulte [Como definir uma versão do .NET Framework como destino](../ide/how-to-target-a-version-of-the-dotnet-framework.md).  
  
3.  No **ItemTemplateWizard** do projeto, adicione uma **janela (WPF)** item ao projeto e, em seguida, o nome do item **WizardWindow**.  
  
4.  Adicione dois arquivos de código que são nomeados CustomActionWizard e cadeias de caracteres.  
  
5.  Abra o menu de atalho para o **ItemTemplateWizard** do projeto e, em seguida, escolha **adicionar referência**.  
  
6.  No **Gerenciador de referências - ItemTemplateWizard** caixa de diálogo do **Assemblies** nó, escolha o **extensões** nó.  
  
7.  Selecione as caixas de seleção ao lado de assemblies a seguir e, em seguida, escolha o **Okey** botão:  
  
    -   EnvDTE  
  
    -   Microsoft.VisualStudio.Shell.11.0  
  
    -   Microsoft.VisualStudio.TemplateWizardInterface  
  
8.  Na **Gerenciador de soluções**, no **referências** pasta do projeto ItemTemplateWizard, escolha o **EnvDTE** referência.  
  
9. No **propriedades** janela, altere o valor da **inserir tipos Interop** propriedade a ser **False**.  
  
## <a name="define-the-default-location-and-id-strings-for-custom-actions"></a>Definir o local padrão e cadeias de caracteres de ID para ações personalizadas
 Todas as ações personalizadas tem um local e uma ID que é especificado na `GroupID` e `Location` atributos da `CustomAction` elemento no *Elements. XML* arquivo. Nesta etapa, você define algumas das cadeias de caracteres válidas para esses atributos no projeto ItemTemplateWizard. Quando você concluir este passo a passo, essas cadeias de caracteres são gravadas para o *Elements. XML* arquivo no item de projeto de ação personalizada quando os usuários no Assistente para especificar um local e uma ID.  
  
 Para simplificar, este exemplo dá suporte a apenas um subconjunto dos locais disponíveis padrão e IDs. Para obter uma lista completa, consulte [locais de ação personalizada padrão e IDs de](http://go.microsoft.com/fwlink/?LinkId=181964).  
  
#### <a name="to-define-the-default-location-and-id-strings"></a>Para definir o local padrão e cadeias de caracteres de ID
  
1.  Abra.  
  
2.  No **ItemTemplateWizard** do projeto, substitua o código no arquivo de código de cadeias de caracteres com o código a seguir.  
  
     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#6](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/strings.cs#6)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#6](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/strings.vb#6)]  
  
## <a name="create-the-wizard-ui"></a>Criar o Assistente de interface do usuário
 Adicione o XAML para definir a interface do usuário do assistente e adicionar algum código para associar alguns dos controles no Assistente para as cadeias de caracteres de ID. O assistente que você cria se parece com o Assistente interno para projetos do SharePoint no Visual Studio.  
  
#### <a name="to-create-the-wizard-ui"></a>Para criar o Assistente de interface do usuário
  
1.  No **ItemTemplateWizard** do projeto, abra o menu de atalho para o **WizardWindow.xaml** file e, em seguida, escolha **abrir** para abrir a janela no designer.  
  
2.  No modo de exibição XAML, substitua o XAML atual com o XAML a seguir. O XAML define uma interface do usuário que inclui um título, controla para especificar o comportamento da ação personalizada e botões de navegação na parte inferior da janela.  
  
    > [!NOTE]  
    >  O projeto terá alguns erros de compilação, depois de adicionar esse código. Esses erros serão eliminados quando você adicionar o código em etapas posteriores.  
  
     [!code-xml[SPExtensibility.ProjectItem.CustomAction#9](../sharepoint/codesnippet/Xaml/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml#9)]  
  
    > [!NOTE]  
    >  A janela que é criada nesse XAML é derivada de <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> classe base. Quando você adiciona uma caixa de diálogo do WPF personalizada para o Visual Studio, é recomendável que você derive sua caixa de diálogo desta classe ter estilo consistentes com as outras caixas de diálogo no Visual Studio e para evitar problemas que possam ocorrer com caixas de diálogo modal. Para obter mais informações, consulte [criando e gerenciando as caixas de diálogo Modal](/visualstudio/extensibility/creating-and-managing-modal-dialog-boxes).  
  
3.  Se você estiver desenvolvendo um projeto do Visual Basic, remova os `ItemTemplateWizard` namespace do `WizardWindow` nome da classe a `x:Class` atributo do `Window` elemento. Esse elemento é na primeira linha do XAML. Quando terminar, a primeira linha deve se parecer com o código a seguir:  
  
    ```xml  
    <Window x:Class="WizardWindow"  
    ```  
  
4.  No arquivo de code-behind para o arquivo WizardWindow.xaml, substitua o código atual com o código a seguir.  
  
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#7](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.vb#7)]
     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#7](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.cs#7)]  
  
## <a name="implement-the-wizard"></a>O Assistente de implementação
 Define a funcionalidade do assistente Implementando o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface.  
  
#### <a name="to-implement-the-wizard"></a>Para implementar o Assistente  
  
1.  No **ItemTemplateWizard** projeto, abra o **CustomActionWizard** arquivo de código e, em seguida, substitua o código atual nesse arquivo com o código a seguir:  
  
     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#8](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/customactionwizard.cs#8)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#8](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/customactionwizard.vb#8)]  
  
## <a name="checkpoint"></a>Ponto de verificação  
 Neste momento no passo a passo, todo o código para que o assistente está agora no projeto. Compile o projeto para certificar-se de que ele foi compilado sem erros.  
  
#### <a name="to-build-your-project"></a>Para compilar seu projeto  
  
1.  Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
## <a name="associate-the-wizard-with-the-item-template"></a>Associar o assistente com o modelo de item
 Agora que você implementou o assistente, você deve associá-lo com o **ação personalizada** modelo de item Concluindo três etapas principais:  
  
1.  Assine o assembly de assistente com um nome forte.  
  
2.  Obter token de chave pública para o assembly de assistente.  
  
3.  Adicione uma referência ao assembly de assistente no arquivo. vstemplate para o **ação personalizada** modelo de item.  
  
#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>Para assinar o assembly de assistente com um nome forte  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do **ItemTemplateWizard** nó do projeto e, em seguida, escolha **propriedades**.  
  
2.  Sobre o **Signing** guia, selecione o **assinar o assembly** caixa de seleção.  
  
3.  No **escolher um arquivo de chave de nome forte** , escolha  **\<novo... >**.  
  
4.  No **criar chave de nome forte** caixa de diálogo, digite um nome, limpe o **proteger o arquivo de chave com uma senha** caixa de seleção e, em seguida, escolha o **Okey** botão.  
  
5.  Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>Para obter a chave pública token para o assembly de Assistente  
  
1.  Em uma janela de Prompt de comando do Visual Studio, execute o seguinte comando, substituindo *PathToWizardAssembly* com o caminho completo para o assembly ItemTemplateWizard.dll compilado para o projeto ItemTemplateWizard em seu desenvolvimento computador.  
  
    ```xml  
    sn.exe -T PathToWizardAssembly  
    ```  
  
     O token de chave pública para o *ItemTemplateWizard.dll* assembly estiver gravado para a janela de Prompt de comando do Visual Studio.  
  
2.  Mantenha a janela de Prompt de comando do Visual Studio aberta. Você precisará do token de chave pública para concluir o procedimento a seguir.  
  
#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>Para adicionar uma referência ao assembly de assistente no arquivo. vstemplate  
  
1.  Na **Gerenciador de soluções**, expanda o **ItemTemplate** nó do projeto e, em seguida, abra o *ItemTemplate.vstemplate* arquivo.  
  
2.  No final do arquivo, adicione o seguinte `WizardExtension` elemento entre os `</TemplateContent>` e `</VSTemplate>` marcas. Substitua os *YourToken* valor o `PublicKeyToken` atributo com o token de chave pública que você obteve no procedimento anterior.  
  
    ```xml  
    <WizardExtension>  
      <Assembly>ItemTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=YourToken</Assembly>  
      <FullClassName>ItemTemplateWizard.CustomActionWizard</FullClassName>  
    </WizardExtension>  
    ```  
  
     Para obter mais informações sobre o `WizardExtension` elemento, consulte [elemento WizardExtension &#40;modelos do Visual Studio&#41;](/visualstudio/extensibility/wizardextension-element-visual-studio-templates).  
  
3.  Salve e feche o arquivo.  
  
## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-item-template"></a>Adicionar parâmetros substituíveis para o *Elements. XML* arquivo no modelo de item
 Adicionar vários parâmetros substituíveis para o *Elements. XML* arquivo no projeto ItemTemplate. Esses parâmetros são inicializados na `PopulateReplacementDictionary` método no `CustomActionWizard` classe que você definiu anteriormente. Quando um usuário adiciona um item de projeto de ação personalizada a um projeto, o Visual Studio automaticamente substitui esses parâmetros na *Elements. XML* arquivos no novo item de projeto com os valores que elas especificados no assistente.  
  
 Um parâmetro de substituição é um token que começa e termina com o caractere de cifrão ($). Além de definir seus próprios parâmetros substituíveis, você pode usar os parâmetros internos que o sistema de projeto do SharePoint define e inicializa. Para obter mais informações, consulte [parâmetros substituíveis](../sharepoint/replaceable-parameters.md).  
  
#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>Para adicionar parâmetros substituíveis para o *Elements. XML* arquivo
  
1.  No projeto ItemTemplate, substitua o conteúdo do *Elements. XML* arquivo pelo XML a seguir.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <Elements Id="$guid8$" xmlns="http://schemas.microsoft.com/sharepoint/">  
      <CustomAction Id="$IdValue$"  
                    GroupId="$GroupIdValue$"  
                    Location="$LocationValue$"  
                    Sequence="1000"  
                    Title="$TitleValue$"  
                    Description="$DescriptionValue$" >  
        <UrlAction Url="$UrlValue$"/>  
      </CustomAction>  
    </Elements>  
    ```  
  
     O novo XML altera os valores da `Id`, `GroupId`, `Location`, `Description`, e `Url` atributos a parâmetros substituíveis.  
  
2.  Salve e feche o arquivo.  
  
## <a name="add-the-wizard-to-the-vsix-package"></a>O Assistente de adição ao pacote VSIX
 No arquivo vsixmanifest no projeto VSIX, adicione uma referência ao projeto do Assistente para que ele seja implantado com o pacote VSIX que contém o item de projeto.  
  
#### <a name="to-add-the-wizard-to-the-vsix-package"></a>Para adicionar o Assistente para o pacote VSIX  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do **vsixmanifest** arquivo no projeto CustomActionProjectItem e, em seguida, escolha **abrir** para abrir o arquivo no editor de manifesto.  
  
2.  No editor de manifesto, escolha o **ativos** guia e, em seguida, escolha o **New** botão.  
  
     O **adicionar novo ativo** caixa de diálogo é exibida.  
  
3.  No **tipo** , escolha **Microsoft.VisualStudio.Assembly**.  
  
4.  No **fonte** , escolha **um projeto na solução atual**.  
  
5.  No **Project** , escolha **ItemTemplateWizard**e, em seguida, escolha o **Okey** botão.  
  
6.  Na barra de menus, escolha **construir** > **compilar solução**e, em seguida, certifique-se de que a solução é compilado sem erros.  
  
## <a name="test-the-wizard"></a>O Assistente de teste
 Agora você está pronto para testar o assistente. Primeiro, começar a depurar a solução CustomActionProjectItem na instância experimental do Visual Studio. Em seguida, teste o Assistente para o item de projeto de ação personalizada em um projeto do SharePoint na instância experimental do Visual Studio. Por fim, compile e execute o projeto do SharePoint para verificar se a ação personalizada funciona conforme o esperado.  
  
#### <a name="to-start-to-debug-the-solution"></a>Para começar a depurar a solução  
  
1.  Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução de CustomActionProjectItem.  
  
2.  No projeto ItemTemplateWizard, abra o arquivo de código CustomActionWizard e, em seguida, adicione um ponto de interrupção para a primeira linha de código no `RunStarted` método.  
  
3.  Na barra de menus, escolha **Debug** > **exceções**.  
  
4.  No **exceções** diálogo caixa, certifique-se de que o **lançada** e **User-unhandled** caixas de seleção **exceções Common Language Runtime**são limpos e, em seguida, escolha o **Okey** botão.  
  
5.  Iniciar a depuração, escolhendo a **F5** chave, ou, na barra de menus, escolhendo **Debug** > **iniciar depuração**.  
  
     Visual Studio instala a extensão para %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom Item\1.0 de projeto de ação e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.  
  
#### <a name="to-test-the-wizard-in-visual-studio"></a>Para testar o assistente no Visual Studio  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo** > **New** > **projeto**.  
  
2.  Expanda o **Visual c#** ou **Visual Basic** nó (dependendo da linguagem que dá suporte a seu modelo de item), expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
3.  Na lista de modelos de projeto, escolha **projeto do SharePoint 2010**, nomeie o projeto **CustomActionWizardTest**e, em seguida, escolha o **Okey** botão.  
  
4.  No **Assistente para personalização do SharePoint**, insira a URL do site que você deseja usar para depuração e, em seguida, escolha o **concluir** botão.  
  
5.  Na **Gerenciador de soluções**, abra o menu de atalho do nó do projeto, escolha **Add**e, em seguida, escolha **Novo Item**.  
  
6.  No **Adicionar Novo Item – CustomItemWizardTest** diálogo caixa, expanda o **SharePoint** nó e, em seguida, expanda o **2010** nó.  
  
7.  Na lista de itens de projeto, escolha o **ação personalizada** item e, em seguida, escolha o **Add** botão.  
  
8.  Verifique se o código em outra instância do Visual Studio para no ponto de interrupção que você definiu anteriormente no `RunStarted` método.  
  
9. Continuar a depuração do projeto, escolhendo a **F5** chave ou, na barra de menus, escolhendo **Debug** > **continuar**.  
  
     O Assistente para personalização do SharePoint é exibida.  
  
10. Sob **local**, escolha o **lista Editar** botão de opção.  
  
11. No **ID do grupo** , escolha **comunicações**.  
  
12. No **Title** , digite **Central de desenvolvedores do SharePoint**.  
  
13. No **descrição** , digite **abre o site do SharePoint Developer Center**.  
  
14. No **URL** , digite **https://docs.microsoft.com/sharepoint/dev/** e, em seguida, escolha o **concluir** botão.  
  
     O Visual Studio adiciona um item que é denominado **CustomAction1** ao seu projeto e abrirá o *Elements. XML* arquivo no editor. Verifique *Elements. XML* contém os valores que você especificou no assistente.  
  
#### <a name="to-test-the-custom-action-in-sharepoint"></a>Para testar a ação personalizada no SharePoint  
  
1.  Na instância experimental do Visual Studio, escolha o **F5** da chave ou, na barra de menus, escolha **Debug** > **iniciar depuração**.  
  
     A ação personalizada é empacotada e implantada para o site do SharePoint especificado pela **URL do Site** propriedade do projeto e o navegador da web abre a página padrão deste site.  
  
    > [!NOTE]  
    >  Se o **Script Debugging Disabled** caixa de diálogo for exibida, escolha o **Sim** botão.  
  
2.  Na área de listas do site do SharePoint, escolha o **tarefas** link.  
  
     O **tarefas - todas as tarefas** página será exibida.  
  
3.  No **ferramentas de lista** guia da faixa de opções, escolha o **lista** guia e, em seguida, no **configurações** grupo, escolha **as configurações da lista**.  
  
     O **as configurações da lista** página será exibida.  
  
4.  Sob o **comunicações** título na parte superior da página, escolha o **Central de desenvolvedores do SharePoint** vincular, verifique se o navegador abre o site https://docs.microsoft.com/sharepoint/dev/e, em seguida, feche o navegador.  
  
## <a name="cleaning-up-the-development-computer"></a>Limpando o computador de desenvolvimento
 Após concluir o teste o item de projeto, remova o modelo de item de projeto da instância experimental do Visual Studio.  
  
#### <a name="to-clean-up-the-development-computer"></a>Para limpar o computador de desenvolvimento  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas** > **extensões e atualizações**.  
  
     A caixa de diálogo **Extensões e Atualizações** é aberta.  
  
2.  Na lista de extensões, escolha o **Item de projeto de ação personalizado** extensão e, em seguida, escolha o **desinstalar** botão.  
  
3.  Na caixa de diálogo que aparece, escolha o **Yes** botão para confirmar que você deseja desinstalar a extensão e, em seguida, escolha o **reiniciar agora** botão para concluir a desinstalação.  
  
4.  Feche ambas as instâncias do Visual Studio (a instância experimental e a instância do Visual Studio em que a solução CustomActionProjectItem estiver aberta).  
  
## <a name="see-also"></a>Consulte também
 [Passo a passo: Criar um item de projeto de ação personalizado com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)   
 [Definir tipos personalizados de item de projeto do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)   
 [Criar modelos de projeto do SharePoint para itens de projeto e modelos de item](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)   
 [Referência de esquema de modelo do Visual Studio](/visualstudio/extensibility/visual-studio-template-schema-reference)   
 [Como: usar assistentes com modelos de projeto](../extensibility/how-to-use-wizards-with-project-templates.md)   
 [IDs e os locais padrão de ação personalizada](http://go.microsoft.com/fwlink/?LinkId=181964)  
  
