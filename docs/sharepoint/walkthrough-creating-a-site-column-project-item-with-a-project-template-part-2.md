---
title: 'Passo a passo: Criando um Item de projeto da coluna de Site com um modelo de projeto, parte 2 | Microsoft Docs'
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
ms.openlocfilehash: d4512dc15d394cdf2442d8bfcf440ccb31623a29
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49942069"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-2"></a>Passo a passo: Criar um item de projeto da coluna de site com um modelo de projeto, parte 2
  Depois de definir um tipo personalizado de item de projeto do SharePoint e associá-lo a um modelo de projeto no Visual Studio, você também poderá fornecer um assistente do modelo. Você pode usar o Assistente para coletar informações dos usuários quando eles usam seu modelo para criar um novo projeto que contém o item de projeto. As informações que você coleta podem ser usadas para inicializar o item de projeto.  
  
 Neste passo a passo, você adicionará um Assistente para o modelo de projeto da coluna de Site que é demonstrado [instruções passo a passo: Criando um Item de projeto da coluna de Site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md). Quando um usuário cria um projeto de coluna de Site, o assistente coleta informações sobre a coluna de site (como seu tipo base e o grupo) e adiciona essas informações para o *Elements. XML* arquivos no novo projeto.  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
-   Criando um Assistente para um tipo de item de projeto do SharePoint personalizado que está associado um modelo de projeto.  
  
-   Definindo um assistente personalizado da interface do usuário que se parece com os assistentes internos para projetos do SharePoint no Visual Studio.  
  
-   A criação de dois *comandos do SharePoint* que são usados para chamar o site do SharePoint local enquanto o assistente está em execução. Comandos do SharePoint são métodos que podem ser usados pelas extensões do Visual Studio para chamar APIs no modelo de objeto do SharePoint server. Para obter mais informações, consulte [chamando os modelos de objeto SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).  
  
-   Usando parâmetros substituíveis para inicializar os arquivos de projeto do SharePoint com os dados coletados no assistente.  
  
-   Criando um novo arquivo. snk em cada nova instância de projeto da coluna de Site. Esse arquivo é usado para assinar o projeto de saída para que o assembly da solução do SharePoint possa ser implantado no cache de assembly global.  
  
-   Depurando e testando o assistente.  
  
> [!NOTE]  
> Para uma série de fluxos de trabalho de exemplo, consulte [exemplos de fluxo de trabalho do SharePoint](https://docs.microsoft.com/sharepoint/dev/general-development/sharepoint-workflow-samples).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar este passo a passo, você deve primeiro criar a solução SiteColumnProjectItem completando [instruções passo a passo: Criando um Item de projeto da coluna de Site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md).  
  
 Você também precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passo:  
  
- Edições com suporte do Windows, SharePoint e Visual Studio.
  
- O SDK do Visual Studio. Este passo a passo usa o **VSIX Project** modelo no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).  
  
  Conhecimento dos conceitos a seguir é útil, mas não necessário para concluir o passo a passo:  
  
- Assistentes para modelos de projeto e item no Visual Studio. Para obter mais informações, consulte [como: usar assistentes com modelos de projeto](../extensibility/how-to-use-wizards-with-project-templates.md) e o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface.  
  
- Colunas de site no SharePoint. Para obter mais informações, consulte [colunas](http://go.microsoft.com/fwlink/?LinkId=183547).  
  
## <a name="understand-the-wizard-components"></a>Compreender os componentes do Assistente
 O assistente que é demonstrado neste passo a passo contém vários componentes. A tabela a seguir descreve esses componentes.  
  
|Componente|Descrição|  
|---------------|-----------------|  
|Implementação do Assistente|Essa é uma classe, denominada `SiteColumnProjectWizard`, que implementa o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface. Essa interface define os métodos que o Visual Studio chama quando o assistente inicia e termina e em determinados momentos enquanto o assistente é executado.|  
|Assistente de interface do usuário|Esta é uma janela baseada no WPF, chamada `WizardWindow`. Essa janela inclui dois controles de usuário, denominados `Page1` e `Page2`. Esses controles de usuário representam as duas páginas do assistente.<br /><br /> Neste passo a passo, o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> método da implementação do assistente exibe o Assistente de interface do usuário.|  
|Modelo de dados do Assistente|Esta é uma classe intermediária, chamada `SiteColumnWizardModel`, que fornece uma camada entre o Assistente de interface do usuário e a implementação do assistente. Este exemplo usa essa classe para ajudar a abstrair a implementação do assistente e o Assistente de interface do usuário do outro; Essa classe não é um componente obrigatório de todos os assistentes.<br /><br /> Neste passo a passo, a implementação do assistente passa um `SiteColumnWizardModel` objeto para a janela do assistente quando ele exibe o Assistente de interface do usuário. O Assistente de interface do usuário utiliza métodos desse objeto para salvar os valores dos controles na interface do usuário e executar tarefas como verificar se a URL do site de entrada é válida. Depois que o usuário termina o assistente, a implementação de assistente usa o `SiteColumnWizardModel` objeto para determinar o estado final da interface do usuário.|  
|Assinatura do gerente de projeto|Essa é uma classe auxiliar, chamada `ProjectSigningManager`, que é usado pela implementação do Assistente para criar um novo arquivo snk em cada nova instância de projeto.|  
|comandos do SharePoint|Esses são métodos que são usados pelo modelo de dados do Assistente para chamar o site do SharePoint local enquanto o assistente está em execução. Porque os comandos do SharePoint devem ter como destino o .NET Framework 3.5, esses comandos são implementados em um assembly diferente do restante do código do assistente.|  
  
## <a name="create-the-projects"></a>Crie os projetos
 Para concluir este passo a passo, você precisa adicionar vários projetos à solução SiteColumnProjectItem que você criou na [instruções passo a passo: criar um item de projeto da coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md):  
  
- Um projeto WPF. Você implementará o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> de interface e definir o Assistente de interface do usuário neste projeto.  
  
- Um projeto de biblioteca de classe que define os comandos do SharePoint. Este projeto deve ter como destino o.NET Framework 3.5.  
  
  Inicie o passo a passo Criando os projetos.  
  
#### <a name="to-create-the-wpf-project"></a>Para criar o projeto WPF
  
1.  No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], abra a solução SiteColumnProjectItem.  
  
2.  Na **Gerenciador de soluções**, abra o menu de atalho para o **SiteColumnProjectItem** nó da solução, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
3.  Na parte superior a **adicionar novo projeto** diálogo caixa, certifique-se de que **.NET Framework 4.5** for escolhido na lista de versões do .NET Framework.  
  
4.  Expanda o **Visual c#** nó ou o **Visual Basic** nó e escolha o **Windows** nó.  
  
5.  Na lista de modelos de projeto, escolha **biblioteca de controle de usuário do WPF**, nomeie o projeto **ProjectTemplateWizard**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **ProjectTemplateWizard** projeto à solução e abre o arquivo de Usercontrol1 padrão.  
  
6.  Exclua o arquivo UserControl1.xaml do projeto.  
  
#### <a name="to-create-the-sharepoint-commands-project"></a>Para criar o projeto de comandos do SharePoint  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do nó da solução SiteColumnProjectItem, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
2.  Na parte superior a **adicionar novo projeto** diálogo caixa, escolha **.NET Framework 3.5** na lista de versões do .NET Framework.  
  
3.  Expanda o **Visual c#** nó ou o **Visual Basic** nó e, em seguida, escolha o **Windows** nó.  
  
4.  Escolha o **biblioteca de classes** modelo de projeto, nomeie o projeto **SharePointCommands**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **SharePointCommands** projeto à solução e abre o arquivo de código padrão Class1.  
  
5.  Exclua o arquivo de código Class1 do projeto.  
  
## <a name="configure-the-projects"></a>Configurar os projetos
 Antes de criar o assistente, você deve adicionar alguns arquivos de código e referências de assembly para os projetos.  
  
#### <a name="to-configure-the-wizard-project"></a>Para configurar o projeto de Assistente  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **ProjectTemplateWizard** nó do projeto e, em seguida, escolha **propriedades**.  
  
2.  No **Designer de projeto**, escolha o **Application** guia para um projeto do Visual c# ou o **compilar** guia para um projeto do Visual Basic.  
  
3.  Certifique-se de que a estrutura de destino é definida como o .NET Framework 4.5, não o perfil de cliente do .NET Framework 4.5.  
  
     Para obter mais informações, consulte [Como definir uma versão do .NET Framework como destino](../ide/how-to-target-a-version-of-the-dotnet-framework.md).  
  
4.  Abra o menu de atalho para o **ProjectTemplateWizard** do projeto, escolha **Add**e, em seguida, escolha **Novo Item**.  
  
5.  Escolha o **janela (WPF)** item, o nome do item **WizardWindow**e, em seguida, escolha o **Add** botão.  
  
6.  Adicione duas **controle de usuário (WPF)** itens ao projeto e nomeá-los **Page1** e **Page2**.  
  
7.  Adicione quatro arquivos de código ao projeto e dar-lhes nomes a seguir:  
  
    -   SiteColumnProjectWizard  
  
    -   SiteColumnWizardModel  
  
    -   ProjectSigningManager  
  
    -   CommandIds  
  
8.  Abra o menu de atalho para o **ProjectTemplateWizard** nó do projeto e, em seguida, escolha **adicionar referência**.  
  
9. Expanda o **Assemblies** nó, escolher o **extensões** nó e, em seguida, selecione as caixas de seleção ao lado de assemblies a seguir:  
  
    -   EnvDTE  
  
    -   Microsoft.VisualStudio.OLE.Interop  
  
    -   Microsoft.VisualStudio.SharePoint  
  
    -   Microsoft.VisualStudio.Shell.11.0  
  
    -   Microsoft.VisualStudio.Shell.Interop.10.0  
  
    -   Microsoft.VisualStudio.Shell.Interop.11.0  
  
    -   Microsoft.VisualStudio.TemplateWizardInterface  
  
10. Escolha o **Okey** botão para adicionar os assemblies para o projeto.  
  
11. Na **Gerenciador de soluções**, sob o **referências** pasta para o **ProjectTemplateWizard** do projeto, escolha **EnvDTE**.  
  
12. No **propriedades** janela, altere o valor da **inserir tipos Interop** propriedade a ser **False**.  
  
13. Se você estiver desenvolvendo um projeto do Visual Basic, importar o namespace ProjectTemplateWizard para seu projeto usando o **Designer de projeto**.  
  
     Para obter mais informações, consulte [como: Adicionar ou remover Namespaces importados &#40;Visual Basic&#41;](../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md).  
  
#### <a name="to-configure-the-sharepointcommands-project"></a>Para configurar o projeto SharePointcommands
  
1.  Na **Gerenciador de soluções**, escolha o **SharePointCommands** nó do projeto.  
  
2.  Na barra de menus, escolha **Project**, **Add Existing Item**.  
  
3.  No **Adicionar Item existente** caixa de diálogo, navegue até a pasta que contém os arquivos de código para o projeto ProjectTemplateWizard e, em seguida, escolha o **CommandIds** arquivo de código.  
  
4.  Escolha a seta ao lado de **Add** botão e, em seguida, escolha o **adicionar como vínculo** opção no menu que aparece.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o arquivo de código para o **SharePointCommands** projeto como um link. O arquivo de código está localizado na **ProjectTemplateWizard** projeto, mas o código no arquivo também é compilado na **SharePointCommands** projeto.  
  
5.  No **SharePointCommands** do projeto, adicione outro arquivo de código que é chamado de comandos.  
  
6.  Escolha o projeto SharePointCommands e, em seguida, na barra de menus, escolha **Project** > **Add Reference**.  
  
7.  Expanda o **Assemblies** nó, escolher o **extensões** nó e, em seguida, selecione as caixas de seleção ao lado de assemblies a seguir:  
  
    -   Microsoft. SharePoint  
  
    -   Microsoft.VisualStudio.SharePoint.Commands  
  
8.  Escolha o **Okey** botão para adicionar os assemblies para o projeto.  
  
## <a name="create-the-wizard-model-signing-manager-and-sharepoint-command-ids"></a>Criar o modelo de assistente, o Gerenciador de assinatura e IDs de comando do SharePoint
 Adicione código ao projeto ProjectTemplateWizard para implementar os seguintes componentes no exemplo:  
  
- As IDs de comando do SharePoint. Essas cadeias de caracteres identificam os comandos do SharePoint que usa o assistente. Posteriormente neste passo a passo, você adicionará código ao projeto SharePointCommands para implementar os comandos.  
  
- O modelo de dados do assistente.  
  
- O Gerenciador de assinatura do projeto.  
  
  Para obter mais informações sobre esses componentes, consulte [Noções básicas sobre o Assistente de componentes](#wizardcomponents).  
  
#### <a name="to-define-the-sharepoint-command-ids"></a>Para definir as IDs de comando do SharePoint
  
1.  No projeto ProjectTemplateWizard, abra o arquivo de código CommandIds e, em seguida, substitua todo o conteúdo deste arquivo pelo código a seguir.  
  
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#5](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/commandids.cs#5)]
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#5](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/commandids.vb#5)]  
  
#### <a name="to-create-the-wizard-model"></a>Para criar o modelo de Assistente  
  
1.  Abra o arquivo de código SiteColumnWizardModel e substitua todo o conteúdo deste arquivo pelo código a seguir.  
  
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#6](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.vb#6)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#6](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.cs#6)]  
  
#### <a name="to-create-the-project-signing-manager"></a>Para criar o Gerenciador de assinatura do projeto  
  
1.  Abra o arquivo de código ProjectSigningManager e, em seguida, substitua todo o conteúdo deste arquivo pelo código a seguir.  
  
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#8](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.vb#8)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#8](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.cs#8)]  
  
## <a name="create-the-wizard-ui"></a>Criar o Assistente de interface do usuário
 Adicione o XAML para definir a interface do usuário da janela do assistente e os dois controles de usuário que fornecem a interface do usuário para as páginas do assistente e adicione código para definir o comportamento dos controles de usuário e a janela. O assistente que você cria se parece com o Assistente interno para projetos do SharePoint no Visual Studio.  
  
> [!NOTE]  
>  Nas etapas a seguir, o projeto terá alguns erros de compilação, depois de adicionar o XAML ou código ao seu projeto. Esses erros serão eliminados quando você adicionar o código em etapas posteriores.  
  
#### <a name="to-create-the-wizard-window-ui"></a>Para criar a janela do Assistente da interface do usuário
  
1.  No projeto ProjectTemplateWizard, abra o menu de atalho para o arquivo WizardWindow.xaml e, em seguida, escolha **abrir** para abrir a janela no designer.  
  
2.  Na exibição do designer XAML, substitua o XAML atual com o XAML a seguir. O XAML define uma interface do usuário que inclui um título, um <xref:System.Windows.Controls.Grid> que contém as páginas do assistente, e botões de navegação na parte inferior da janela.  
  
     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#10](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml#10)]  
  
    > [!NOTE]  
    >  A janela que é criada nesse XAML é derivada de <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> classe base. Quando você adiciona uma caixa de diálogo do WPF personalizada para o Visual Studio, é recomendável que você derive sua caixa de diálogo desta classe ter estilo consistentes com as outras caixas de diálogo do Visual Studio e para evitar problemas de caixa de diálogo modal que possam ocorrer. Para obter mais informações, consulte [criando e gerenciando as caixas de diálogo Modal](/visualstudio/extensibility/creating-and-managing-modal-dialog-boxes).  
  
3.  Se você estiver desenvolvendo um projeto do Visual Basic, remova os `ProjectTemplateWizard` namespace do `WizardWindow` nome da classe a `x:Class` atributo do `Window` elemento. Esse elemento é na primeira linha do XAML. Quando terminar, a primeira linha deve parecer com o exemplo a seguir.  
  
    ```xml  
    <Window x:Class="WizardWindow"  
    ```  
  
4.  Abra o arquivo code-behind para o arquivo WizardWindow.xaml.  
  
5.  Substitua o conteúdo desse arquivo, exceto para o `using` declarações na parte superior do arquivo, com o código a seguir.  
  
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#4](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.vb#4)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#4](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.cs#4)]  
  
#### <a name="to-create-the-first-wizard-page-ui"></a>Para criar a primeira página do Assistente da interface do usuário
  
1.  No projeto ProjectTemplateWizard, abra o menu de atalho para o arquivo Page1.xaml e, em seguida, escolha **abrir** para abrir o controle de usuário no designer.  
  
2.  Na exibição do designer XAML, substitua o XAML atual com o XAML a seguir. O XAML define uma interface do usuário que inclui uma caixa de texto onde os usuários podem inserir a URL dos sites locais que deseja usar para depuração. A interface do usuário também inclui botões de opção com a qual os usuários podem especificar se o projeto está em modo seguro.  
  
     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#11](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page1.xaml#11)]  
  
3.  Se você estiver desenvolvendo um projeto do Visual Basic, remova os `ProjectTemplateWizard` namespace do `Page1` nome da classe a `x:Class` atributo do `UserControl` elemento. Essa é a primeira linha do XAML. Quando você terminar, a primeira linha deve ser semelhante ao seguinte.  
  
    ```xml  
    <UserControl x:Class="Page1"  
    ```  
  
4.  Substitua o conteúdo do arquivo Page1.xaml, exceto para o `using` declarações na parte superior do arquivo, com o código a seguir.  
  
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#2](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.vb#2)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#2](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.cs#2)]  
  
#### <a name="to-create-the-second-wizard-page-ui"></a>Para criar a segunda página do Assistente da interface do usuário
  
1.  No projeto ProjectTemplateWizard, abra o menu de atalho para o arquivo Page2.xaml e, em seguida, escolha **abrir**.  
  
     O controle de usuário é aberto no designer.  
  
2.  No modo de exibição XAML, substitua o XAML atual com o XAML a seguir. O XAML define uma interface do usuário que inclui uma lista suspensa para escolher o tipo base para a coluna de site, uma caixa de combinação para especificar um grupo interno ou personalizado em que a coluna de site são exibidos na galeria e uma caixa de texto para especificar o nome da coluna de site.  
  
     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#12](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page2.xaml#12)]  
  
3.  Se você estiver desenvolvendo um projeto do Visual Basic, remova os `ProjectTemplateWizard` namespace do `Page2` nome da classe a `x:Class` atributo do `UserControl` elemento. Essa é a primeira linha do XAML. Quando você terminar, a primeira linha deve ser semelhante ao seguinte.  
  
    ```xml  
    <UserControl x:Class="Page2"  
    ```  
  
4.  Substitua o conteúdo do arquivo code-behind para o arquivo Page2.xaml, exceto para o `using` declarações na parte superior do arquivo, com o código a seguir.  
  
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#3](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.vb#3)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#3](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.cs#3)]  
  
## <a name="implement-the-wizard"></a>O Assistente de implementação
 Define a funcionalidade principal do assistente Implementando o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface. Essa interface define os métodos que o Visual Studio chama quando o assistente inicia e termina e em determinados momentos enquanto o assistente é executado.  
  
#### <a name="to-implement-the-wizard"></a>Para implementar o Assistente  
  
1.  No projeto ProjectTemplateWizard, abra o arquivo de código SiteColumnProjectWizard.  
  
2.  Substitua todo o conteúdo deste arquivo pelo código a seguir.  
  
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#7](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.vb#7)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#7](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.cs#7)]  
  
## <a name="create-the-sharepoint-commands"></a>Criar os comandos do SharePoint
 Crie dois comandos personalizados que chamam o modelo de objeto do SharePoint server. Um comando determina se a URL do site que o usuário digita no assistente é válida. Outro comando obtém todos os tipos de campo do site do SharePoint especificado para que os usuários podem selecionar qual delas usar como base para sua nova coluna de site.  
  
#### <a name="to-define-the-sharepoint-commands"></a>Para definir os comandos do SharePoint  
  
1.  No **SharePointCommands** do projeto, abra o arquivo de código de comandos.  
  
2.  Substitua todo o conteúdo deste arquivo pelo código a seguir.  
  
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#9](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/sharepointcommands/commands.vb#9)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#9](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/sharepointcommands/commands.cs#9)]  
  
## <a name="checkpoint"></a>Ponto de verificação  
 Neste momento no passo a passo, todo o código para que o assistente está agora no projeto. Compile o projeto para certificar-se de que ele foi compilado sem erros.  
  
#### <a name="to-build-your-project"></a>Para compilar seu projeto  
  
1.  Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
## <a name="removing-the-keysnk-file-from-the-project-template"></a>Removendo o arquivo snk do modelo de projeto
 Na [instruções passo a passo: criar um item de projeto da coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md), o modelo de projeto que você criou contém um arquivo de snk que é usado para assinar cada instância de projeto da coluna de Site. Esse arquivo snk não é mais necessário porque o assistente agora gera um novo arquivo snk para cada projeto. Remova o arquivo de snk do modelo de projeto e remover as referências a esse arquivo.  
  
#### <a name="to-remove-the-keysnk-file-from-the-project-template"></a>Para remover o arquivo de snk do modelo de projeto  
  
1.  No **Gerenciador de soluções**, sob o **SiteColumnProjectTemplate** nó, abra o menu de atalho para o **snk** file e, em seguida, escolha **excluir**.  
  
2.  Na caixa de diálogo de confirmação é exibida, escolha o **Okey** botão.  
  
3.  Sob o **SiteColumnProjectTemplate** nó, abra o arquivo SiteColumnProjectTemplate.vstemplate e, em seguida, remover o seguinte elemento dela.  
  
    ```xml  
    <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>  
    ```  
  
4.  Salve e feche o arquivo.  
  
5.  Sob o **SiteColumnProjectTemplate** nó, abra o arquivo ProjectTemplate.csproj ou ProjectTemplate.vbproj e, em seguida, remova a seguinte `PropertyGroup` elemento dele.  
  
    ```xml  
    <PropertyGroup>  
      <SignAssembly>true</SignAssembly>  
      <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>  
    </PropertyGroup>  
    ``` 
  
6.  Remova a seguinte `None` elemento.  
  
    ```xml  
    <None Include="key.snk" />  
    ```  
  
7.  Salve e feche o arquivo.  
  
## <a name="associating-the-wizard-with-the-project-template"></a>Associando o assistente com o modelo de projeto
 Agora que você implementou o assistente, você deve associar o assistente com o **coluna de Site** modelo de projeto. Há três procedimentos que devem ser concluídas para fazer isso:  
  
1.  Assine o assembly de assistente com um nome forte.  
  
2.  Obter token de chave pública para o assembly de assistente.  
  
3.  Adicione uma referência ao assembly de assistente no arquivo. vstemplate para o **coluna de Site** modelo de projeto.  
  
#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>Para assinar o assembly de assistente com um nome forte  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **ProjectTemplateWizard** do projeto e, em seguida, escolha **propriedades**.  
  
2.  Sobre o **Signing** guia, selecione o **assinar o assembly** caixa de seleção.  
  
3.  No **escolher um arquivo de chave de nome forte** , escolha  **\<novo... >**.  
  
4.  No **criar chave de nome forte** caixa de diálogo, digite um nome para o novo arquivo de chave, limpe o **proteger o arquivo de chave com uma senha** caixa de seleção e, em seguida, escolha o **Okey** botão.  
  
5.  Abra o menu de atalho para o **ProjectTemplateWizard** do projeto e, em seguida, escolha **Build** para criar o arquivo ProjectTemplateWizard.dll.  
  
#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>Para obter a chave pública token para o assembly de Assistente  
  
1.  Sobre o **Menu Iniciar**, escolha **todos os programas**, escolha **Microsoft Visual Studio**, escolha **ferramentas do Visual Studio**e, em seguida, escolha  **Prompt de comando do desenvolvedor**.  
  
     Abre uma janela de Prompt de comando do Visual Studio.  
  
2.  Execute o seguinte comando, substituindo *PathToWizardAssembly* com o caminho completo para o assembly ProjectTemplateWizard.dll compilado para o projeto ProjectTemplateWizard no computador de desenvolvimento:  
  
    ```cmd  
    sn.exe -T PathToWizardAssembly  
    ```  
  
     O token de chave pública para o assembly ProjectTemplateWizard.dll é gravado para a janela de Prompt de comando do Visual Studio.  
  
3.  Mantenha a janela de Prompt de comando do Visual Studio aberta. Você precisará do token de chave pública durante o próximo procedimento.  
  
#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>Para adicionar uma referência ao assembly de assistente no arquivo. vstemplate  
  
1.  Na **Gerenciador de soluções**, expanda o **SiteColumnProjectTemplate** nó do projeto e abra o arquivo SiteColumnProjectTemplate.vstemplate.  
  
2.  No final do arquivo, adicione o seguinte `WizardExtension` elemento entre os `</TemplateContent>` e `</VSTemplate>` marcas. Substitua os *seu token* valor da `PublicKeyToken` atributo com o token de chave pública que você obteve no procedimento anterior.  
  
    ```xml  
    <WizardExtension>  
      <Assembly>ProjectTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=your token</Assembly>  
      <FullClassName>ProjectTemplateWizard.SiteColumnProjectWizard</FullClassName>  
    </WizardExtension>  
    ```  
  
     Para obter mais informações sobre o `WizardExtension` elemento, consulte [elemento WizardExtension &#40;modelos do Visual Studio&#41;](/visualstudio/extensibility/wizardextension-element-visual-studio-templates).  
  
3.  Salve e feche o arquivo.  
  
## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-project-template"></a>Adicionar parâmetros substituíveis no arquivo Elements. XML no modelo de projeto
 Adicionar vários parâmetros substituíveis para o *Elements. XML* arquivo no projeto SiteColumnProjectTemplate. Esses parâmetros são inicializados na `RunStarted` método no `SiteColumnProjectWizard` classe que você definiu anteriormente. Quando um usuário cria um projeto de coluna de Site, o Visual Studio automaticamente substitui esses parâmetros na *Elements. XML* arquivos no novo projeto com os valores que elas especificados no assistente.  
  
 Um parâmetro de substituição é um token que começa e termina com o caractere de cifrão ($). Além de definir seus próprios parâmetros substituíveis, você pode usar os parâmetros internos que são definidos e inicializados pelo sistema do projeto do SharePoint. Para obter mais informações, consulte [parâmetros substituíveis](../sharepoint/replaceable-parameters.md).  
  
#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>Para adicionar parâmetros substituíveis no arquivo Elements. XML
  
1.  No projeto SiteColumnProjectTemplate, substitua o conteúdo do *Elements. XML* arquivo pelo XML a seguir.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8"?>  
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">  
      <Field ID="{$guid5$}"   
             Name="$fieldname$"   
             DisplayName="$fieldname$"   
             Type="$selectedfieldtype$"   
             Group="$selectedgrouptype$">  
      </Field>  
    </Elements>  
    ```  
  
     O novo XML altera os valores da `Name`, `DisplayName`, `Type`, e `Group` atributos a parâmetros substituíveis personalizados.  
  
2.  Salve e feche o arquivo.  
  
## <a name="add-the-wizard-to-the-vsix-package"></a>O Assistente de adição ao pacote VSIX
 Para implantar o assistente com o pacote VSIX que contém o modelo de projeto da coluna de Site, adicione referências para o projeto de assistente e o projeto de comandos do SharePoint para o arquivo vsixmanifest no projeto VSIX.  
  
#### <a name="to-add-the-wizard-to-the-vsix-package"></a>Para adicionar o Assistente para o pacote VSIX  
  
1.  Na **Gerenciador de soluções**, no **SiteColumnProjectItem** do projeto, abra o menu de atalho para o **vsixmanifest** file e, em seguida, escolha **Abra**.  
  
     Visual Studio abre o arquivo no editor de manifesto.  
  
2.  Sobre o **ativos** guia do editor, escolha a **New** botão.  
  
     O **adicionar novo ativo** caixa de diálogo é aberta.  
  
3.  No **tipo** , escolha **Microsoft.VisualStudio.Assembly**.  
  
4.  No **fonte** , escolha **um projeto na solução atual**.  
  
5.  No **Project** , escolha **ProjectTemplateWizard**e, em seguida, escolha o **Okey** botão.  
  
6.  Sobre o **ativos** guia do editor, escolha a **New** novamente no botão.  
  
     O **adicionar novo ativo** caixa de diálogo é aberta.  
  
7.  No **tipo** , digite **SharePoint.Commands.v4**.  
  
8.  No **fonte** , escolha **um projeto na solução atual**.  
  
9. No **Project** , escolha o **SharePointCommands** do projeto e, em seguida, escolha o **Okey** botão.  
  
10. Na barra de menus, escolha **construir** > **compilar solução**e, em seguida, certifique-se de que a solução é compilada sem erros.  
  
## <a name="test-the-wizard"></a>O Assistente de teste
 Agora você está pronto para testar o assistente. Primeiro, inicie a depuração da solução SiteColumnProjectItem na instância experimental do Visual Studio. Em seguida, teste o Assistente para o projeto da coluna de Site na instância experimental do Visual Studio. Por fim, compile e execute o projeto para verificar se a coluna de site funciona conforme o esperado.  
  
#### <a name="to-start-debugging-the-solution"></a>Para iniciar a depuração da solução  
  
1.  Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução de SiteColumnProjectItem.  
  
2.  No projeto ProjectTemplateWizard, abra o arquivo de código SiteColumnProjectWizard e, em seguida, adicione um ponto de interrupção para a primeira linha de código no `RunStarted` método.  
  
3.  Na barra de menus, escolha **Debug** > **exceções**.  
  
4.  No **exceções** diálogo caixa, certifique-se de que o **lançada** e **User-unhandled** caixas de seleção **exceções Common Language Runtime**são limpos e, em seguida, escolha o **Okey** botão.  
  
5.  Iniciar a depuração, escolhendo a **F5** chave ou, na barra de menus, escolhendo **Debug** > **iniciar depuração**.  
  
     Visual Studio instala a extensão para %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Site Column\1.0 e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.  
  
#### <a name="to-test-the-wizard-in-visual-studio"></a>Para testar o assistente no Visual Studio  
  
1. Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo** > **New** > **projeto**.  
  
2. Expanda o **Visual c#** nó ou o **Visual Basic** nó (dependendo da linguagem que dá suporte a seu modelo de projeto), expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
3. Na lista de modelos de projeto, escolha **coluna de Site**, nomeie o projeto **SiteColumnWizardTest**e, em seguida, escolha o **Okey** botão.  
  
4. Verifique se o código em outra instância do Visual Studio para no ponto de interrupção que você definiu anteriormente no `RunStarted` método.  
  
5. Continuar a depuração do projeto, escolhendo a **F5** chave ou, na barra de menus, escolhendo **Debug** > **continuar**.  
  
6. No **Assistente para personalização do SharePoint**, insira a URL do site que você deseja usar para depuração e, em seguida, escolha o **próxima** botão.  
  
7. Na segunda página do **Assistente para personalização do SharePoint**, faça as seguintes seleções:  
  
   - No **tipo** , escolha **booliano**.  
  
   - No **grupo** , escolha **personalizado Sim colunas**.  
  
   - No **nome** , digite **minha coluna de Sim**e, em seguida, escolha o **concluir** botão.  
  
     Na **Gerenciador de soluções**, um novo projeto aparece e contém um item de projeto é denominado **campo1**, e o Visual Studio abre o projeto *Elements. XML* arquivo no editor.  
  
8. Verifique *Elements. XML* contém os valores que você especificou no assistente.  
  
#### <a name="to-test-the-site-column-in-sharepoint"></a>Para testar a coluna de site no SharePoint  
  
1.  Na instância experimental do Visual Studio, escolha o **F5** chave.  
  
     A coluna de site é empacotada e implantada para o SharePoint do site que o **URL do Site** Especifica a propriedade do projeto. O navegador da web abre a página padrão deste site.  
  
    > [!NOTE]  
    >  Se o **Script Debugging Disabled** caixa de diálogo for exibida, escolha o **Sim** botão para continuar a depuração do projeto.  
  
2.  Sobre o **ações do Site** menu, escolha **configurações de Site**.  
  
3.  Na página Configurações do Site, sob **galerias**, escolha o **colunas de Site** link.  
  
4.  Na lista de colunas de site, verifique se que um **personalizado Sim colunas** grupo contém uma coluna que é denominada **minha coluna de Sim**e, em seguida, feche o navegador da web.  
  
## <a name="clean-up-the-development-computer"></a>Limpar o computador de desenvolvimento
 Após concluir o teste o item de projeto, remova o modelo de projeto da instância experimental do Visual Studio.  
  
#### <a name="to-clean-up-the-development-computer"></a>Para limpar o computador de desenvolvimento  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas** > **extensões e atualizações**.  
  
     A caixa de diálogo **Extensões e Atualizações** é aberta.  
  
2.  Na lista de extensões, escolha **coluna de Site**e, em seguida, escolha o **desinstalar** botão.  
  
3.  Na caixa de diálogo que aparece, escolha o **Yes** botão para confirmar que você deseja desinstalar a extensão e, em seguida, escolha o **reiniciar agora** botão para concluir a desinstalação.  
  
4.  Feche a instância experimental do Visual Studio e a instância na qual a solução de CustomActionProjectItem está aberta.  
  
     Para obter informações sobre como implantar [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] as extensões, consulte [envio extensões do Visual Studio](/visualstudio/extensibility/shipping-visual-studio-extensions).  
  
## <a name="see-also"></a>Consulte também
 [Passo a passo: Criar um item de projeto da coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)   
 [Definir tipos personalizados de item de projeto do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)   
 [Criando modelos de projeto e modelos de Item para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)   
 [Referência de esquema de modelo do Visual Studio](/visualstudio/extensibility/visual-studio-template-schema-reference)   
 [Como usar assistentes com modelos do projeto](../extensibility/how-to-use-wizards-with-project-templates.md)  
  
