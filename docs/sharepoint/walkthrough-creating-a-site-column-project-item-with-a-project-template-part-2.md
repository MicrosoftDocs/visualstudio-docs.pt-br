---
title: Criar item de projeto de coluna de site com modelo de projeto, parte 2
ms.date: 02/02/2017
ms.topic: how-to
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], creating template wizards
- SharePoint project items, creating template wizards
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: c3b84d901a1fd94d72ff14ec5c481e04676c5cbc
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016402"
---
# <a name="walkthrough-create-a-site-column-project-item-with-a-project-template-part-2"></a>Walkthrough: criar um item de projeto de coluna de site com um modelo de projeto, parte 2
  Depois de definir um tipo personalizado de item de projeto do SharePoint e associá-lo a um modelo de projeto no Visual Studio, talvez você também queira fornecer um assistente para o modelo. Você pode usar o assistente para coletar informações de usuários quando eles usam seu modelo para criar um novo projeto que contém o item de projeto. As informações coletadas podem ser usadas para inicializar o item do projeto.

 Neste tutorial, você adicionará um assistente ao modelo de projeto de coluna de site que é demonstrado em [Walkthrough: Criando um item de projeto de coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md). Quando um usuário cria um projeto de coluna de site, o assistente coleta informações sobre a coluna de site (como seu tipo e grupo base) e adiciona essas informações ao arquivo de *Elements.xml* no novo projeto.

 Este tutorial demonstra as seguintes tarefas:

- Criar um assistente para um tipo de item de projeto personalizado do SharePoint que está associado a um modelo de projeto.

- Definir uma interface do usuário do assistente personalizada que se assemelha aos assistentes internos para projetos do SharePoint no Visual Studio.

- Criar dois *comandos do SharePoint* que são usados para chamar o site local do SharePoint enquanto o assistente está em execução. Os comandos do SharePoint são métodos que podem ser usados pelas extensões do Visual Studio para chamar APIs no modelo de objeto do SharePoint Server. Para obter mais informações, consulte [chamando os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).

- Usando parâmetros substituíveis para inicializar arquivos de projeto do SharePoint com dados coletados no assistente.

- Criando um novo arquivo. snk em cada nova instância de projeto de coluna de site. Esse arquivo é usado para assinar a saída do projeto para que o assembly da solução do SharePoint possa ser implantado no cache de assembly global.

- Depurando e testando o assistente.

> [!NOTE]
> Para obter uma série de fluxos de trabalho de exemplo, consulte [exemplos de fluxo de trabalho do SharePoint](/sharepoint/dev/general-development/sharepoint-workflow-samples).

## <a name="prerequisites"></a>Pré-requisitos
 Para executar este passo a passos, você deve primeiro criar a solução SiteColumnProjectItem concluindo o [passo a passos: Criando um item de projeto de coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md).

 Você também precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passos:

- Edições com suporte do Windows, SharePoint e Visual Studio.

- O SDK do Visual Studio. Este tutorial usa o modelo de **projeto VSIX** no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).

  O conhecimento dos seguintes conceitos é útil, mas não é necessário, para concluir o passo a passos:

- Assistentes para modelos de projeto e item no Visual Studio. Para obter mais informações, consulte [como: usar assistentes com modelos de projeto](../extensibility/how-to-use-wizards-with-project-templates.md) e a <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface.

- Colunas do site no SharePoint. Para obter mais informações, consulte [colunas](/previous-versions/office/developer/sharepoint-2010/ms196085(v=office.14)).

## <a name="understand-the-wizard-components"></a>Entender os componentes do assistente
 O assistente que é demonstrado neste guia explicativo contém vários componentes. A tabela a seguir descreve esses componentes.

|Componente|Descrição|
|---------------|-----------------|
|Implementação do assistente|Essa é uma classe, chamada `SiteColumnProjectWizard` , que implementa a <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface. Essa interface define os métodos que o Visual Studio chama quando o assistente é iniciado e concluído e em determinados momentos durante a execução do assistente.|
|Interface do usuário do assistente|Essa é uma janela baseada no WPF, chamada `WizardWindow` . Essa janela inclui dois controles de usuário, chamados `Page1` e `Page2` . Esses controles de usuário representam as duas páginas do assistente.<br /><br /> Neste tutorial, o <xref:Microsoft.VisualStudio.TemplateWizard.IWizard.RunStarted%2A> método da implementação do assistente exibe a interface do usuário do assistente.|
|Modelo de dados do assistente|Essa é uma classe intermediária, chamada `SiteColumnWizardModel` , que fornece uma camada entre a interface do usuário do assistente e a implementação do assistente. Este exemplo usa essa classe para ajudar a abstrair a implementação do assistente e a interface do usuário do assistente umas das outras; Essa classe não é um componente necessário de todos os assistentes.<br /><br /> Neste tutorial, a implementação do assistente passa um `SiteColumnWizardModel` objeto para a janela do assistente quando ele exibe a interface do usuário do assistente. A interface do usuário do assistente usa métodos desse objeto para salvar os valores dos controles na interface do usuário e para executar tarefas como verificar se a URL do site de entrada é válida. Depois que o usuário concluir o assistente, a implementação do assistente usará o `SiteColumnWizardModel` objeto para determinar o estado final da interface do usuário.|
|Gerenciador de assinatura de projeto|Essa é uma classe auxiliar, chamada `ProjectSigningManager` , que é usada pela implementação do assistente para criar um novo arquivo Key. snk em cada nova instância de projeto.|
|comandos do SharePoint|Esses são métodos que são usados pelo modelo de dados do assistente para chamar o site do SharePoint local enquanto o assistente está em execução. Como os comandos do SharePoint devem ter como destino o .NET Framework 3,5, esses comandos são implementados em um assembly diferente do restante do código do assistente.|

## <a name="create-the-projects"></a>Criar os projetos
 Para concluir este passo a passos, você precisa adicionar vários projetos à solução SiteColumnProjectItem que você criou em [passo a passos: criar um item de projeto de coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md):

- Um projeto do WPF. Você implementará a <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface e definirá a interface do usuário do assistente neste projeto.

- Um projeto de biblioteca de classes que define os comandos do SharePoint. Este projeto deve ter como destino a estrutura the.NET 3,5.

  Inicie o passo a passos criando os projetos.

#### <a name="to-create-the-wpf-project"></a>Para criar o projeto WPF

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , abra a solução SiteColumnProjectItem.

2. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução **SiteColumnProjectItem** , escolha **Adicionar**e, em seguida, escolha **novo projeto**.

3. Na parte superior da caixa de diálogo **Adicionar novo projeto** , certifique-se de que **.NET Framework 4,5** seja escolhido na lista de versões do .NET Framework.

4. Expanda o nó do **Visual C#** ou o nó **Visual Basic** e escolha o nó do **Windows** .

5. Na lista de modelos de projeto, escolha **biblioteca de controle de usuário do WPF**, nomeie o projeto **ProjectTemplateWizard**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **ProjectTemplateWizard** à solução e abre o arquivo UserControl1. XAML padrão.

6. Exclua o arquivo UserControl1. XAML do projeto.

#### <a name="to-create-the-sharepoint-commands-project"></a>Para criar o projeto de comandos do SharePoint

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução SiteColumnProjectItem, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na parte superior da caixa de diálogo **Adicionar novo projeto** , escolha **.NET Framework 3,5** na lista de versões do .NET Framework.

3. Expanda o nó do **Visual C#** ou o nó **Visual Basic** e, em seguida, escolha o nó do **Windows** .

4. Escolha o modelo de projeto de **biblioteca de classes** , nomeie o projeto **SharePointCommands**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **SharePointCommands** à solução e abre o arquivo de código de Class1 padrão.

5. Exclua o arquivo de código Class1 do projeto.

## <a name="configure-the-projects"></a>Configurar os projetos
 Antes de criar o assistente, você deve adicionar alguns arquivos de código e referências de assembly aos projetos.

#### <a name="to-configure-the-wizard-project"></a>Para configurar o projeto do assistente

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó do projeto **ProjectTemplateWizard** e escolha **Propriedades**.

2. No **Designer de projeto**, escolha a guia **aplicativo** para um projeto do Visual C# ou a guia **Compilar** para um projeto Visual Basic.

3. Verifique se a estrutura de destino está definida como a .NET Framework 4,5, não o perfil de cliente .NET Framework 4,5.

     Para obter mais informações, consulte [como: direcionar uma versão do .NET Framework](../ide/visual-studio-multi-targeting-overview.md).

4. Abra o menu de atalho para o projeto **ProjectTemplateWizard** , escolha **Adicionar**e, em seguida, escolha **novo item**.

5. Escolha o item **janela (WPF)** , nomeie o item **WizardWindow**e, em seguida, escolha o botão **Adicionar** .

6. Adicione dois itens de **controle de usuário (WPF)** ao projeto e nomeie-os como **página1** e **página2**.

7. Adicione quatro arquivos de código ao projeto e forneça os seguintes nomes:

    - SiteColumnProjectWizard

    - SiteColumnWizardModel

    - ProjectSigningManager

    - CommandIds

8. Abra o menu de atalho para o nó do projeto **ProjectTemplateWizard** e escolha **Adicionar referência**.

9. Expanda o nó **assemblies** , escolha o nó **extensões** e, em seguida, marque as caixas de seleção ao lado dos seguintes assemblies:

    - EnvDTE

    - Microsoft. VisualStudio. OLE. Interop

    - Microsoft. VisualStudio. SharePoint

    - Microsoft. VisualStudio. Shell. 11.0

    - Microsoft. VisualStudio. Shell. Interop. 10.0

    - Microsoft. VisualStudio. Shell. Interop. 11.0

    - Microsoft. VisualStudio. TemplateWizardInterface

10. Escolha o botão **OK** para adicionar os assemblies ao projeto.

11. No **Gerenciador de soluções**, na pasta **referências** para o projeto **ProjectTemplateWizard** , escolha **EnvDTE**.

12. Na janela **Propriedades** , altere o valor da propriedade **inserir tipos de interoperabilidade** para **false**.

13. Se você estiver desenvolvendo um projeto Visual Basic, importe o namespace ProjectTemplateWizard para seu projeto usando o **Designer de projeto**.

     Para obter mais informações, consulte [como: Adicionar ou remover namespaces Importados &#40;Visual Basic&#41;](../ide/how-to-add-or-remove-imported-namespaces-visual-basic.md).

#### <a name="to-configure-the-sharepointcommands-project"></a>Para configurar o projeto SharePointcommands

1. Em **Gerenciador de soluções**, escolha o nó do projeto **SharePointCommands** .

2. Na barra de menus, escolha **projeto**, **Adicionar item existente**.

3. Na caixa de diálogo **Adicionar item existente** , navegue até a pasta que contém os arquivos de código do projeto ProjectTemplateWizard e escolha o arquivo de código **CommandIds** .

4. Escolha a seta ao lado do botão **Adicionar** e, em seguida, escolha a opção **Adicionar como link** no menu exibido.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o arquivo de código ao projeto **SharePointCommands** como um link. O arquivo de código está localizado no projeto **ProjectTemplateWizard** , mas o código no arquivo também é compilado no projeto **SharePointCommands** .

5. No projeto **SharePointCommands** , adicione outro arquivo de código chamado comandos.

6. Escolha o projeto SharePointCommands e, em seguida, na barra de menus, escolha **projeto**  >  **Adicionar referência**.

7. Expanda o nó **assemblies** , escolha o nó **extensões** e, em seguida, marque as caixas de seleção ao lado dos seguintes assemblies:

    - Microsoft. SharePoint

    - Microsoft. VisualStudio. SharePoint. Commands

8. Escolha o botão **OK** para adicionar os assemblies ao projeto.

## <a name="create-the-wizard-model-signing-manager-and-sharepoint-command-ids"></a>Criar o modelo do assistente, o Gerenciador de assinatura e as IDs de comando do SharePoint
 Adicione código ao projeto ProjectTemplateWizard para implementar os seguintes componentes no exemplo:

- As IDs de comando do SharePoint. Essas cadeias de caracteres identificam os comandos do SharePoint que o assistente usa. Mais adiante neste tutorial, você adicionará código ao projeto SharePointCommands para implementar os comandos.

- O modelo de dados do assistente.

- O Gerenciador de assinatura do projeto.

  Para obter mais informações sobre esses componentes, consulte [entender os componentes do assistente](#understand-the-wizard-components).

#### <a name="to-define-the-sharepoint-command-ids"></a>Para definir as IDs de comando do SharePoint

1. No projeto ProjectTemplateWizard, abra o arquivo de código CommandIds e, em seguida, substitua todo o conteúdo desse arquivo pelo código a seguir.

     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#5](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/commandids.cs#5)]
     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#5](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/commandids.vb#5)]

#### <a name="to-create-the-wizard-model"></a>Para criar o modelo do assistente

1. Abra o arquivo de código SiteColumnWizardModel e substitua todo o conteúdo desse arquivo pelo código a seguir.

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#6](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.vb#6)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#6](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnwizardmodel.cs#6)]

#### <a name="to-create-the-project-signing-manager"></a>Para criar o Gerenciador de assinatura de projeto

1. Abra o arquivo de código ProjectSigningManager e, em seguida, substitua todo o conteúdo desse arquivo pelo código a seguir.

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#8](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.vb#8)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#8](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/projectsigningmanager.cs#8)]

## <a name="create-the-wizard-ui"></a>Criar a interface do usuário do assistente
 Adicione o XAML para definir a interface do usuário da janela do assistente e os dois controles de usuário que fornecem a interface do usuário para as páginas do assistente e adicione o código para definir o comportamento dos controles Window e User. O assistente que você cria é semelhante ao assistente interno para projetos do SharePoint no Visual Studio.

> [!NOTE]
> Nas etapas a seguir, seu projeto terá alguns erros de compilação depois que você adicionar XAML ou código ao seu projeto. Esses erros vão desaparecer quando você adiciona código em etapas posteriores.

#### <a name="to-create-the-wizard-window-ui"></a>Para criar a interface do usuário da janela do assistente

1. No projeto ProjectTemplateWizard, abra o menu de atalho do arquivo WizardWindow. XAML e, em seguida, escolha **abrir** para abrir a janela no designer.

2. Na exibição XAML do designer, substitua o XAML atual pelo XAML a seguir. O XAML define uma interface do usuário que inclui um título, um <xref:System.Windows.Controls.Grid> que contém as páginas do assistente e os botões de navegação na parte inferior da janela.

     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#10](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml#10)]

    > [!NOTE]
    > A janela que é criada neste XAML é derivada da <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> classe base. Quando você adiciona uma caixa de diálogo personalizada do WPF ao Visual Studio, recomendamos que você Derive sua caixa de diálogo dessa classe para ter estilos consistentes com outras caixas de diálogo do Visual Studio e para evitar problemas de caixa de diálogo modais que poderiam ocorrer. Para obter mais informações, consulte [criando e gerenciando caixas de diálogo modais](../extensibility/creating-and-managing-modal-dialog-boxes.md).

3. Se você estiver desenvolvendo um projeto Visual Basic, remova o `ProjectTemplateWizard` namespace do `WizardWindow` nome da classe no `x:Class` atributo do `Window` elemento. Esse elemento está na primeira linha do XAML. Quando terminar, a primeira linha deverá ser parecida com o exemplo a seguir.

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. Abra o arquivo code-behind para o arquivo WizardWindow. XAML.

5. Substitua o conteúdo desse arquivo, exceto pelas `using` declarações na parte superior do arquivo, pelo código a seguir.

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#4](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.vb#4)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#4](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/wizardwindow.xaml.cs#4)]

#### <a name="to-create-the-first-wizard-page-ui"></a>Para criar a primeira interface do usuário da página do assistente

1. No projeto ProjectTemplateWizard, abra o menu de atalho para o arquivo página1. XAML e, em seguida, escolha **abrir** para abrir o controle de usuário no designer.

2. Na exibição XAML do designer, substitua o XAML atual pelo XAML a seguir. O XAML define uma interface do usuário que inclui uma caixa de texto onde os usuários podem inserir a URL dos sites locais que desejam usar para depuração. A interface do usuário também inclui botões de opção com os quais os usuários podem especificar se o projeto está em área restrita.

     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#11](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page1.xaml#11)]

3. Se você estiver desenvolvendo um projeto Visual Basic, remova o `ProjectTemplateWizard` namespace do `Page1` nome da classe no `x:Class` atributo do `UserControl` elemento. Isso está na primeira linha do XAML. Quando terminar, a primeira linha deverá ser parecida com a seguinte.

    ```xml
    <UserControl x:Class="Page1"
    ```

4. Substitua o conteúdo do arquivo página1. XAML, exceto pelas `using` declarações na parte superior do arquivo, pelo código a seguir.

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#2](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.vb#2)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#2](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page1.xaml.cs#2)]

#### <a name="to-create-the-second-wizard-page-ui"></a>Para criar a segunda interface do usuário da página de assistente

1. No projeto ProjectTemplateWizard, abra o menu de atalho para o arquivo página2. XAML e, em seguida, escolha **abrir**.

     O controle de usuário é aberto no designer.

2. No modo de exibição XAML, substitua o XAML atual pelo XAML a seguir. O XAML define uma interface do usuário que inclui uma lista suspensa para escolher o tipo base da coluna site, uma caixa de combinação para especificar um grupo interno ou personalizado no qual exibir a coluna site na galeria e uma caixa de texto para especificar o nome da coluna site.

     [!code-xml[SPExtensibility.ProjectItem.SiteColumn#12](../sharepoint/codesnippet/Xaml/sitecolumnprojectitem/projecttemplatewizard/page2.xaml#12)]

3. Se você estiver desenvolvendo um projeto Visual Basic, remova o `ProjectTemplateWizard` namespace do `Page2` nome da classe no `x:Class` atributo do `UserControl` elemento. Isso está na primeira linha do XAML. Quando terminar, a primeira linha deverá ser parecida com a seguinte.

    ```xml
    <UserControl x:Class="Page2"
    ```

4. Substitua o conteúdo do arquivo code-behind do arquivo página2. XAML, exceto pelas `using` declarações na parte superior do arquivo, pelo código a seguir.

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#3](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.vb#3)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#3](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/page2.xaml.cs#3)]

## <a name="implement-the-wizard"></a>Implementar o assistente
 Defina a funcionalidade principal do assistente implementando a <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface. Essa interface define os métodos que o Visual Studio chama quando o assistente é iniciado e concluído e em determinados momentos durante a execução do assistente.

#### <a name="to-implement-the-wizard"></a>Para implementar o assistente

1. No projeto ProjectTemplateWizard, abra o arquivo de código SiteColumnProjectWizard.

2. Substitua todo o conteúdo deste arquivo pelo código a seguir.

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#7](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.vb#7)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#7](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/projecttemplatewizard/sitecolumnprojectwizard.cs#7)]

## <a name="create-the-sharepoint-commands"></a>Criar os comandos do SharePoint
 Crie dois comandos personalizados que chamam o modelo de objeto do SharePoint Server. Um comando determina se a URL do site que o usuário digita no assistente é válida. O outro comando obtém todos os tipos de campo do site do SharePoint especificado para que os usuários possam selecionar qual deles usar como base para sua nova coluna de site.

#### <a name="to-define-the-sharepoint-commands"></a>Para definir os comandos do SharePoint

1. No projeto **SharePointCommands** , abra o arquivo de código de comandos.

2. Substitua todo o conteúdo deste arquivo pelo código a seguir.

     [!code-vb[SPExtensibility.ProjectItem.SiteColumn#9](../sharepoint/codesnippet/VisualBasic/sitecolumnprojectitem/sharepointcommands/commands.vb#9)]
     [!code-csharp[SPExtensibility.ProjectItem.SiteColumn#9](../sharepoint/codesnippet/CSharp/sitecolumnprojectitem/sharepointcommands/commands.cs#9)]

## <a name="checkpoint"></a>Ponto de verificação
 Neste ponto do passo a passo, todo o código do assistente agora está no projeto. Compile o projeto para certificar-se de que ele seja compilado sem erros.

#### <a name="to-build-your-project"></a>Para compilar seu projeto

1. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

## <a name="removing-the-keysnk-file-from-the-project-template"></a>Removendo o arquivo Key. SNK do modelo de projeto
 Em [Walkthrough: criar um item de projeto de coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md), o modelo de projeto que você criou contém um arquivo Key. snk que é usado para assinar cada instância de projeto de coluna de site. Este arquivo Key. SNK não é mais necessário porque o assistente agora gera um novo arquivo Key. SNK para cada projeto. Remova o arquivo Key. SNK do modelo de projeto e remova as referências a esse arquivo.

#### <a name="to-remove-the-keysnk-file-from-the-project-template"></a>Para remover o arquivo Key. SNK do modelo de projeto

1. No **Gerenciador de soluções**, no nó **SiteColumnProjectTemplate** , abra o menu de atalho para o arquivo **Key. SNK** e escolha **excluir**.

2. Na caixa de diálogo de confirmação que aparece, escolha o botão **OK** .

3. No nó **SiteColumnProjectTemplate** , abra o arquivo SiteColumnProjectTemplate. vstemplate e, em seguida, remova o seguinte elemento dele.

    ```xml
    <ProjectItem ReplaceParameters="false" TargetFileName="key.snk">key.snk</ProjectItem>
    ```

4. Salve e feche o arquivo.

5. No nó **SiteColumnProjectTemplate** , abra o arquivo ProjectTemplate. csproj ou ProjectTemplate. vbproj e, em seguida, remova o seguinte `PropertyGroup` elemento dele.

    ```xml
    <PropertyGroup>
      <SignAssembly>true</SignAssembly>
      <AssemblyOriginatorKeyFile>key.snk</AssemblyOriginatorKeyFile>
    </PropertyGroup>
    ```

6. Remova o elemento a seguir `None` .

    ```xml
    <None Include="key.snk" />
    ```

7. Salve e feche o arquivo.

## <a name="associating-the-wizard-with-the-project-template"></a>Associando o assistente ao modelo de projeto
 Agora que você implementou o assistente, deve associar o assistente ao modelo de projeto de **coluna de site** . Há três procedimentos que você deve concluir para fazer isso:

1. Assine o assembly do assistente com um nome forte.

2. Obtenha o token de chave pública para o assembly do assistente.

3. Adicione uma referência ao assembly do assistente no arquivo. vstemplate para o modelo de projeto **coluna do site** .

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>Para assinar o assembly do assistente com um nome forte

1. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **ProjectTemplateWizard** e escolha **Propriedades**.

2. Na guia **Assinatura**, marque a caixa de seleção **Assinar o assembly**.

3. Na lista **escolher um arquivo de chave de nome forte** , escolha **\<New...>** .

4. Na caixa de diálogo **criar chave de nome forte** , insira um nome para o novo arquivo de chave, desmarque a caixa de seleção **proteger meu arquivo de chave com uma senha** e escolha o botão **OK** .

5. Abra o menu de atalho para o projeto **ProjectTemplateWizard** e escolha **Compilar** para criar o arquivo de ProjectTemplateWizard.dll.

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>Para obter o token de chave pública para o assembly do assistente

1. No **menu iniciar**, escolha **todos os programas**, escolha **Microsoft Visual Studio**, escolha **Ferramentas do Visual Studio**e, em seguida, escolha **prompt de comando do desenvolvedor**.

     Uma janela de prompt de comando do Visual Studio é aberta.

2. Execute o comando a seguir, substituindo *PathToWizardAssembly* pelo caminho completo para o assembly de ProjectTemplateWizard.dll criado para o projeto ProjectTemplateWizard em seu computador de desenvolvimento:

    ```cmd
    sn.exe -T PathToWizardAssembly
    ```

     O token de chave pública para o assembly ProjectTemplateWizard.dll é gravado na janela do prompt de comando do Visual Studio.

3. Mantenha a janela do prompt de comando do Visual Studio aberta. Você precisará do token de chave pública durante o próximo procedimento.

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>Para adicionar uma referência ao assembly do assistente no arquivo. vstemplate

1. Em **Gerenciador de soluções**, expanda o nó do projeto **SiteColumnProjectTemplate** e abra o arquivo SiteColumnProjectTemplate. vstemplate.

2. Próximo ao final do arquivo, adicione o seguinte `WizardExtension` elemento entre as `</TemplateContent>` marcas e `</VSTemplate>` . Substitua o valor de *token* do `PublicKeyToken` atributo pelo token de chave pública que você obteve no procedimento anterior.

    ```xml
    <WizardExtension>
      <Assembly>ProjectTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=your token</Assembly>
      <FullClassName>ProjectTemplateWizard.SiteColumnProjectWizard</FullClassName>
    </WizardExtension>
    ```

     Para obter mais informações sobre o `WizardExtension` elemento, consulte o [elemento WizardExtension &#40;modelos do Visual Studio&#41;](../extensibility/wizardextension-element-visual-studio-templates.md).

3. Salve e feche o arquivo.

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-project-template"></a>Adicionar parâmetros substituíveis ao arquivo de Elements.xml no modelo de projeto
 Adicione vários parâmetros substituíveis ao arquivo de *Elements.xml* no projeto SiteColumnProjectTemplate. Esses parâmetros são inicializados no `RunStarted` método na `SiteColumnProjectWizard` classe que você definiu anteriormente. Quando um usuário cria um projeto de coluna de site, o Visual Studio substitui automaticamente esses parâmetros no arquivo de *Elements.xml* no novo projeto com os valores que eles especificaram no assistente.

 Um parâmetro substituível é um token que começa e termina com o caractere de cifrão ($). Além de definir seus próprios parâmetros substituíveis, você pode usar parâmetros internos que são definidos e inicializados pelo sistema de projeto do SharePoint. Para obter mais informações, consulte [parâmetros substituíveis](../sharepoint/replaceable-parameters.md).

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>Para adicionar parâmetros substituíveis ao arquivo de Elements.xml

1. No projeto SiteColumnProjectTemplate, substitua o conteúdo do arquivo *Elements.xml* pelo seguinte XML.

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

     O novo XML altera os valores dos `Name` atributos, `DisplayName` , `Type` e `Group` para parâmetros substituíveis personalizados.

2. Salve e feche o arquivo.

## <a name="add-the-wizard-to-the-vsix-package"></a>Adicionar o assistente ao pacote VSIX
 Para implantar o assistente com o pacote VSIX que contém o modelo de projeto coluna de site, adicione referências ao projeto do assistente e ao projeto de comandos do SharePoint ao arquivo Source. Extension. vsixmanifest no projeto VSIX.

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>Para adicionar o assistente ao pacote VSIX

1. No **Gerenciador de soluções**, no projeto **SiteColumnProjectItem** , abra o menu de atalho para o arquivo **Source. Extension. vsixmanifest** e, em seguida, escolha **abrir**.

     O Visual Studio abre o arquivo no editor de manifesto.

2. Na guia **ativos** do editor, escolha o botão **novo** .

     A caixa de diálogo **Adicionar novo ativo** é aberta.

3. Na lista **tipo** , escolha **Microsoft. VisualStudio. assembly**.

4. Na lista **origem** , escolha **um projeto na solução atual**.

5. Na lista **projeto** , escolha **ProjectTemplateWizard**e, em seguida, escolha o botão **OK** .

6. Na guia **ativos** do editor, escolha o botão **novo** novamente.

     A caixa de diálogo **Adicionar novo ativo** é aberta.

7. Na lista **tipo** , digite **SharePoint. Commands. v4**.

8. Na lista **origem** , escolha **um projeto na solução atual**.

9. Na lista **projeto** , escolha o projeto **SharePointCommands** e, em seguida, escolha o botão **OK** .

10. Na barra de menus, escolha **criar**  >  **solução de compilação**e, em seguida, certifique-se de que a solução seja compilada sem erros.

## <a name="test-the-wizard"></a>Testar o assistente
 Agora você está pronto para testar o assistente. Primeiro, inicie a depuração da solução SiteColumnProjectItem na instância experimental do Visual Studio. Em seguida, teste o assistente para o projeto de coluna de site na instância experimental do Visual Studio. Por fim, compile e execute o projeto para verificar se a coluna site funciona conforme o esperado.

#### <a name="to-start-debugging-the-solution"></a>Para iniciar a depuração da solução

1. Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução SiteColumnProjectItem.

2. No projeto ProjectTemplateWizard, abra o arquivo de código SiteColumnProjectWizard e, em seguida, adicione um ponto de interrupção à primeira linha de código no `RunStarted` método.

3. Na barra de menus, escolha **depurar**  >  **exceções**.

4. Na caixa de diálogo **exceções** , certifique-se de que as caixas de seleção **lançado** e não **manipulado pelo usuário** para **exceções do Common Language Runtime** sejam limpas e, em seguida, escolha o botão **OK** .

5. Inicie a depuração escolhendo a tecla **F5** ou, na barra de menus, escolhendo **depurar**  >  **Iniciar Depuração**.

     O Visual Studio instala a extensão para%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Site Column\1.0 e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.

#### <a name="to-test-the-wizard-in-visual-studio"></a>Para testar o assistente no Visual Studio

1. Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Expanda o nó do **Visual C#** ou o nó **Visual Basic** (dependendo do idioma ao qual o modelo de projeto dá suporte), expanda o nó do **SharePoint** e escolha o nó **2010** .

3. Na lista de modelos de projeto, escolha **site coluna**, nomeie o projeto **SiteColumnWizardTest**e, em seguida, escolha o botão **OK** .

4. Verifique se o código na outra instância do Visual Studio é interrompido no ponto de interrupção que você definiu anteriormente no `RunStarted` método.

5. Continue a depurar o projeto escolhendo a tecla **F5** ou, na barra de menus, escolhendo **depurar**  >  **continuar**.

6. No **Assistente para personalização do SharePoint**, insira a URL do site que você deseja usar para depuração e, em seguida, escolha o botão **Avançar** .

7. Na segunda página do **Assistente para personalização do SharePoint**, faça as seguintes seleções:

   - Na lista **tipo** , escolha **booliano**.

   - Na lista **grupo** , escolha **Personalizar colunas Sim/não**.

   - Na caixa **nome** , insira **minha coluna Sim/não**e, em seguida, escolha o botão **concluir** .

     No **Gerenciador de soluções**, um novo projeto é exibido e contém um item de projeto chamado **Field1**e o Visual Studio abre o arquivo de *Elements.xml* do projeto no editor.

8. Verifique se *Elements.xml* contém os valores que você especificou no assistente.

#### <a name="to-test-the-site-column-in-sharepoint"></a>Para testar a coluna site no SharePoint

1. Na instância experimental do Visual Studio, escolha a tecla **F5** .

     A coluna site é empacotada e implantada no site do SharePoint que a propriedade **URL do site** do projeto especifica. O navegador da Web é aberto na página padrão deste site.

    > [!NOTE]
    > Se a caixa de diálogo **depuração de script desabilitada** for exibida, escolha o botão **Sim** para continuar a depurar o projeto.

2. No menu **ações do site** , escolha **configurações do site**.

3. Na página Configurações do site, em **galerias**, escolha o link **colunas do site** .

4. Na lista de colunas do site, verifique se um grupo de **colunas Sim/não personalizado** contém uma coluna chamada **minha coluna Sim/não**e, em seguida, feche o navegador da Web.

## <a name="clean-up-the-development-computer"></a>Limpar o computador de desenvolvimento
 Depois de concluir o teste do item de projeto, remova o modelo de projeto da instância experimental do Visual Studio.

#### <a name="to-clean-up-the-development-computer"></a>Para limpar o computador de desenvolvimento

1. Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas**  >  **extensões e atualizações**.

     A caixa de diálogo **Extensões e Atualizações** é aberta.

2. Na lista de extensões, escolha **site coluna**e, em seguida, escolha o botão **desinstalar** .

3. Na caixa de diálogo exibida, escolha o botão **Sim** para confirmar que você deseja desinstalar a extensão e, em seguida, escolha o botão **reiniciar agora** para concluir a desinstalação.

4. Feche a instância experimental do Visual Studio e a instância na qual a solução CustomActionProjectItem está aberta.

     Para obter informações sobre como implantar [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] extensões, consulte [enviando extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md).

## <a name="see-also"></a>Consulte também
- [Walkthrough: criar um item de projeto de coluna de site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)
- [Definir tipos de item de projeto personalizados do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [Criando modelos de item e de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Como usar assistentes com modelos do projeto](../extensibility/how-to-use-wizards-with-project-templates.md)
