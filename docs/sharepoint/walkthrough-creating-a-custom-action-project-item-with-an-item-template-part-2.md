---
title: Criar item de projeto de ação personalizada com modelo de item, parte 2
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
ms.openlocfilehash: c96546f85b21ee0ca8a559059a16158b743cb915
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016107"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-2"></a>Walkthrough: criar um item de projeto de ação personalizada com um modelo de item, parte 2
  Depois de definir um tipo personalizado de item de projeto do SharePoint e associá-lo a um modelo de item no Visual Studio, talvez você também queira fornecer um assistente para o modelo. Você pode usar o assistente para coletar informações de usuários quando eles usam seu modelo para adicionar uma nova instância do item de projeto a um projeto. As informações coletadas podem ser usadas para inicializar o item do projeto.

 Neste tutorial, você adicionará um assistente ao item de projeto de ação personalizada que é demonstrado em [Walkthrough: criar um item de projeto de ação personalizada com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md). Quando um usuário adiciona um item de projeto de ação personalizada a um projeto do SharePoint, o assistente coleta informações sobre a ação personalizada (como seu local e a URL para navegar até quando um usuário final o escolhe) e adiciona essas informações ao arquivo de *Elements.xml* no novo item de projeto.

 Este tutorial demonstra as seguintes tarefas:

- Criar um assistente para um tipo de item de projeto personalizado do SharePoint que está associado a um modelo de item.

- Definir uma interface do usuário do assistente personalizada que se assemelha aos assistentes internos para itens de projeto do SharePoint no Visual Studio.

- Usando parâmetros substituíveis para inicializar arquivos de projeto do SharePoint com dados coletados no assistente.

- Depurando e testando o assistente.

> [!NOTE]
> Você pode baixar um exemplo do [GitHub](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) que mostra como criar atividades personalizadas para um fluxo de trabalho.

## <a name="prerequisites"></a>Pré-requisitos
 Para executar este passo a passos, você deve primeiro criar a solução CustomActionProjectItem concluindo o [passo a passos: criar um item de projeto de ação personalizada com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md).

 Você também precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passos:

- Edições com suporte do Windows, SharePoint e Visual Studio.

- O SDK do Visual Studio. Este tutorial usa o modelo de **projeto VSIX** no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).

  O conhecimento dos seguintes conceitos é útil, mas não é necessário, para concluir o passo a passos:

- Assistentes para modelos de projeto e item no Visual Studio. Para obter mais informações, consulte [como: usar assistentes com modelos de projeto](../extensibility/how-to-use-wizards-with-project-templates.md) e a <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface.

- Ações personalizadas no SharePoint. Para obter mais informações, consulte [ação personalizada](/previous-versions/office/developer/sharepoint-2010/ms458635(v=office.14)).

## <a name="create-the-wizard-project"></a>Criar o projeto do assistente
 Para concluir este passo a passos, você deve adicionar um projeto à solução CustomActionProjectItem que você criou no [passo a passo: criar um item de projeto de ação personalizada com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md). Você implementará a <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface e definirá a interface do usuário do assistente neste projeto.

#### <a name="to-create-the-wizard-project"></a>Para criar o projeto do assistente

1. No Visual Studio, abra a solução CustomActionProjectItem

2. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

3. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha o nó **Windows** .

4. Na parte superior da caixa de diálogo **novo projeto** , certifique-se de que **.NET Framework 4,5** seja escolhido na lista de versões do .NET Framework.

5. Escolha o modelo de projeto de **biblioteca de controle de usuário do WPF** , nomeie o projeto **ItemTemplateWizard**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **ItemTemplateWizard** à solução.

6. Exclua o item UserControl1 do projeto.

## <a name="configure-the-wizard-project"></a>Configurar o projeto do assistente
 Antes de criar o assistente, você deve adicionar uma janela Windows Presentation Foundation (WPF), um arquivo de código e referências de assembly ao projeto.

#### <a name="to-configure-the-wizard-project"></a>Para configurar o projeto do assistente

1. No **Gerenciador de soluções**, abra o menu de atalho do nó do projeto **ItemTemplateWizard** e escolha **Propriedades**.

2. No **Designer de projeto**, verifique se a estrutura de destino está definida como .NET Framework 4,5.

     Para projetos do Visual C#, você pode definir esse valor na guia **aplicativo** . Para projetos Visual Basic, você pode definir esse valor na guia **Compilar** . Para obter mais informações, consulte [como: direcionar uma versão do .NET Framework](../ide/visual-studio-multi-targeting-overview.md).

3. No projeto **ItemTemplateWizard** , adicione um item **Window (WPF)** ao projeto e, em seguida, nomeie o item **WizardWindow**.

4. Adicione dois arquivos de código denominados CustomActionWizard e cadeias de caracteres.

5. Abra o menu de atalho para o projeto **ItemTemplateWizard** e escolha **Adicionar referência**.

6. Na caixa de diálogo **Gerenciador de referências-ItemTemplateWizard** , no nó **assemblies** , escolha o nó **extensões** .

7. Marque as caixas de seleção ao lado dos seguintes assemblies e escolha o botão **OK** :

    - EnvDTE

    - Microsoft. VisualStudio. Shell. 11.0

    - Microsoft. VisualStudio. TemplateWizardInterface

8. Em **Gerenciador de soluções**, na pasta **referências** para o projeto ItemTemplateWizard, escolha a referência **EnvDTE** .

9. Na janela **Propriedades** , altere o valor da propriedade **inserir tipos de interoperabilidade** para **false**.

## <a name="define-the-default-location-and-id-strings-for-custom-actions"></a>Definir o local padrão e as cadeias de caracteres de ID para ações personalizadas
 Cada ação personalizada tem um local e ID que é especificado nos `GroupID` atributos e `Location` do `CustomAction` elemento no arquivo de *Elements.xml* . Nesta etapa, você define algumas das cadeias de caracteres válidas para esses atributos no projeto ItemTemplateWizard. Quando você concluir este passo a passos, essas cadeias de caracteres serão gravadas no arquivo de *Elements.xml* no item de projeto de ação personalizada quando os usuários especificarem um local e uma ID no assistente.

 Para simplificar, este exemplo dá suporte apenas a um subconjunto dos locais e IDs padrão disponíveis. Para obter uma lista completa, consulte [locais e IDs da ação personalizada padrão](/previous-versions/office/developer/sharepoint-2010/bb802730(v=office.14)).

#### <a name="to-define-the-default-location-and-id-strings"></a>Para definir o local padrão e as cadeias de caracteres de ID

1. abrir.

2. No projeto **ItemTemplateWizard** , substitua o código no arquivo de código de cadeia de caracteres pelo código a seguir.

     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#6](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/strings.cs#6)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#6](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/strings.vb#6)]

## <a name="create-the-wizard-ui"></a>Criar a interface do usuário do assistente
 Adicione XAML para definir a interface do usuário do assistente e adicione algum código para associar alguns dos controles do assistente às cadeias de caracteres de ID. O assistente que você cria é semelhante ao assistente interno para projetos do SharePoint no Visual Studio.

#### <a name="to-create-the-wizard-ui"></a>Para criar a interface do usuário do assistente

1. No projeto **ItemTemplateWizard** , abra o menu de atalho do arquivo **WizardWindow. XAML** e, em seguida, escolha **abrir** para abrir a janela no designer.

2. No modo de exibição XAML, substitua o XAML atual pelo XAML a seguir. O XAML define uma interface do usuário que inclui um título, controles para especificar o comportamento da ação personalizada e botões de navegação na parte inferior da janela.

    > [!NOTE]
    > Seu projeto terá alguns erros de compilação depois que você adicionar esse código. Esses erros vão desaparecer quando você adiciona código em etapas posteriores.

     [!code-xml[SPExtensibility.ProjectItem.CustomAction#9](../sharepoint/codesnippet/Xaml/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml#9)]

    > [!NOTE]
    > A janela que é criada neste XAML é derivada da <xref:Microsoft.VisualStudio.PlatformUI.DialogWindow> classe base. Quando você adiciona uma caixa de diálogo personalizada do WPF ao Visual Studio, recomendamos que você Derive sua caixa de diálogo dessa classe para ter estilos consistentes com outras caixas de diálogo no Visual Studio e para evitar problemas que podem ocorrer de outra forma com caixas de diálogo modais. Para obter mais informações, consulte [criando e gerenciando caixas de diálogo modais](../extensibility/creating-and-managing-modal-dialog-boxes.md).

3. Se você estiver desenvolvendo um projeto Visual Basic, remova o `ItemTemplateWizard` namespace do `WizardWindow` nome da classe no `x:Class` atributo do `Window` elemento. Esse elemento está na primeira linha do XAML. Quando terminar, a primeira linha deverá ser semelhante ao seguinte código:

    ```xml
    <Window x:Class="WizardWindow"
    ```

4. No arquivo code-behind do arquivo WizardWindow. XAML, substitua o código atual pelo código a seguir.

     [!code-vb[SPExtensibility.ProjectItem.CustomAction#7](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.vb#7)]
     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#7](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/wizardwindow.xaml.cs#7)]

## <a name="implement-the-wizard"></a>Implementar o assistente
 Defina a funcionalidade do assistente implementando a <xref:Microsoft.VisualStudio.TemplateWizard.IWizard> interface.

#### <a name="to-implement-the-wizard"></a>Para implementar o assistente

1. No projeto **ItemTemplateWizard** , abra o arquivo de código **CustomActionWizard** e, em seguida, substitua o código atual neste arquivo pelo seguinte código:

     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#8](../sharepoint/codesnippet/CSharp/customactionprojectitem/itemtemplatewizard/customactionwizard.cs#8)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#8](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/itemtemplatewizard/customactionwizard.vb#8)]

## <a name="checkpoint"></a>Ponto de verificação
 Neste ponto do passo a passo, todo o código do assistente agora está no projeto. Compile o projeto para certificar-se de que ele seja compilado sem erros.

#### <a name="to-build-your-project"></a>Para compilar seu projeto

1. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

## <a name="associate-the-wizard-with-the-item-template"></a>Associar o assistente ao modelo de item
 Agora que você implementou o assistente, você deve associá-lo ao modelo de item de **ação personalizado** , concluindo três etapas principais:

1. Assine o assembly do assistente com um nome forte.

2. Obtenha o token de chave pública para o assembly do assistente.

3. Adicione uma referência ao assembly do assistente no arquivo. vstemplate para o modelo de item de **ação personalizado** .

#### <a name="to-sign-the-wizard-assembly-with-a-strong-name"></a>Para assinar o assembly do assistente com um nome forte

1. No **Gerenciador de soluções**, abra o menu de atalho do nó do projeto **ItemTemplateWizard** e escolha **Propriedades**.

2. Na guia **Assinatura**, marque a caixa de seleção **Assinar o assembly**.

3. Na lista **escolher um arquivo de chave de nome forte** , escolha **\<New...>** .

4. Na caixa de diálogo **criar chave de nome forte** , insira um nome, desmarque a caixa de seleção **proteger meu arquivo de chave com uma senha** e escolha o botão **OK** .

5. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

#### <a name="to-get-the-public-key-token-for-the-wizard-assembly"></a>Para obter o token de chave pública para o assembly do assistente

1. Em uma janela de prompt de comando do Visual Studio, execute o comando a seguir, substituindo *PathToWizardAssembly* pelo caminho completo do assembly de ItemTemplateWizard.dll criado para o projeto ItemTemplateWizard no seu computador de desenvolvimento.

    ```xml
    sn.exe -T PathToWizardAssembly
    ```

     O token de chave pública para o assembly *ItemTemplateWizard.dll* é gravado na janela do prompt de comando do Visual Studio.

2. Mantenha a janela do prompt de comando do Visual Studio aberta. Você precisará do token de chave pública para concluir o próximo procedimento.

#### <a name="to-add-a-reference-to-the-wizard-assembly-in-the-vstemplate-file"></a>Para adicionar uma referência ao assembly do assistente no arquivo. vstemplate

1. Em **Gerenciador de soluções**, expanda o nó do projeto **ItemTemplate** e, em seguida, abra o arquivo *ItemTemplate. vstemplate* .

2. Próximo ao final do arquivo, adicione o seguinte `WizardExtension` elemento entre as `</TemplateContent>` marcas e `</VSTemplate>` . Substitua o valor *YourToken* do `PublicKeyToken` atributo pelo token de chave pública que você obteve no procedimento anterior.

    ```xml
    <WizardExtension>
      <Assembly>ItemTemplateWizard, Version=1.0.0.0, Culture=neutral, PublicKeyToken=YourToken</Assembly>
      <FullClassName>ItemTemplateWizard.CustomActionWizard</FullClassName>
    </WizardExtension>
    ```

     Para obter mais informações sobre o `WizardExtension` elemento, consulte o [elemento WizardExtension &#40;modelos do Visual Studio&#41;](../extensibility/wizardextension-element-visual-studio-templates.md).

3. Salve e feche o arquivo.

## <a name="add-replaceable-parameters-to-the-elementsxml-file-in-the-item-template"></a>Adicionar parâmetros substituíveis ao arquivo de *Elements.xml* no modelo de item
 Adicione vários parâmetros substituíveis ao arquivo de *Elements.xml* no projeto ItemTemplate. Esses parâmetros são inicializados no `PopulateReplacementDictionary` método na `CustomActionWizard` classe que você definiu anteriormente. Quando um usuário adiciona um item de projeto de ação personalizada a um projeto, o Visual Studio substitui automaticamente esses parâmetros no arquivo de *Elements.xml* no novo item de projeto pelos valores que eles especificaram no assistente.

 Um parâmetro substituível é um token que inicia e termina com o caractere de cifrão ($). Além de definir seus próprios parâmetros substituíveis, você pode usar parâmetros internos que o sistema de projeto do SharePoint define e inicializa. Para obter mais informações, consulte [parâmetros substituíveis](../sharepoint/replaceable-parameters.md).

#### <a name="to-add-replaceable-parameters-to-the-elementsxml-file"></a>Para adicionar parâmetros substituíveis ao arquivo de *Elements.xml*

1. No projeto ItemTemplate, substitua o conteúdo do arquivo *Elements.xml* pelo seguinte XML.

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

     O novo XML altera os valores dos `Id` atributos, `GroupId` , `Location` , `Description` e `Url` para parâmetros substituíveis.

2. Salve e feche o arquivo.

## <a name="add-the-wizard-to-the-vsix-package"></a>Adicionar o assistente ao pacote VSIX
 No arquivo Source. Extension. vsixmanifest no projeto VSIX, adicione uma referência ao projeto do assistente para que ele seja implantado com o pacote VSIX que contém o item do projeto.

#### <a name="to-add-the-wizard-to-the-vsix-package"></a>Para adicionar o assistente ao pacote VSIX

1. No **Gerenciador de soluções**, abra o menu de atalho do arquivo **Source. Extension. vsixmanifest** no projeto CustomActionProjectItem e, em seguida, escolha **abrir** para abrir o arquivo no editor de manifesto.

2. No editor de manifesto, escolha a guia **ativos** e, em seguida, escolha o botão **novo** .

     A caixa de diálogo **Adicionar novo ativo** é exibida.

3. Na lista **tipo** , escolha **Microsoft. VisualStudio. assembly**.

4. Na lista **origem** , escolha **um projeto na solução atual**.

5. Na lista **projeto** , escolha **ItemTemplateWizard**e, em seguida, escolha o botão **OK** .

6. Na barra de menus, escolha **criar**  >  **solução de compilação**e, em seguida, certifique-se de que a solução seja compilada sem erros.

## <a name="test-the-wizard"></a>Testar o assistente
 Agora você está pronto para testar o assistente. Primeiro, comece a depurar a solução CustomActionProjectItem na instância experimental do Visual Studio. Em seguida, teste o assistente para o item de projeto de ação personalizada em um projeto do SharePoint na instância experimental do Visual Studio. Por fim, compile e execute o projeto do SharePoint para verificar se a ação personalizada funciona conforme o esperado.

#### <a name="to-start-to-debug-the-solution"></a>Para começar a depurar a solução

1. Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução CustomActionProjectItem.

2. No projeto ItemTemplateWizard, abra o arquivo de código CustomActionWizard e, em seguida, adicione um ponto de interrupção à primeira linha de código no `RunStarted` método.

3. Na barra de menus, escolha **depurar**  >  **exceções**.

4. Na caixa de diálogo **exceções** , certifique-se de que as caixas de seleção **lançado** e não **manipulado pelo usuário** para **exceções do Common Language Runtime** sejam limpas e, em seguida, escolha o botão **OK** .

5. Inicie a depuração escolhendo a tecla **F5** ou, na barra de menus, escolhendo **depurar**  >  **Iniciar Depuração**.

     O Visual Studio instala a extensão para o projeto de ação%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom Item\1.0 e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.

#### <a name="to-test-the-wizard-in-visual-studio"></a>Para testar o assistente no Visual Studio

1. Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Expanda o nó **Visual C#** ou **Visual Basic** (dependendo do idioma ao qual o modelo de item dá suporte), expanda o nó do **SharePoint** e escolha o nó **2010** .

3. Na lista de modelos de projeto, escolha **projeto do SharePoint 2010**, nomeie o projeto **CustomActionWizardTest**e, em seguida, escolha o botão **OK** .

4. No **Assistente para personalização do SharePoint**, insira a URL do site que você deseja usar para depuração e, em seguida, escolha o botão **concluir** .

5. No **Gerenciador de soluções**, abra o menu de atalho para o nó do projeto, escolha **Adicionar**e, em seguida, escolha **novo item**.

6. Na caixa de diálogo **Adicionar novo item-CustomItemWizardTest** , expanda o nó do **SharePoint** e, em seguida, expanda o nó **2010** .

7. Na lista de itens de projeto, escolha o item de **ação personalizada** e, em seguida, escolha o botão **Adicionar** .

8. Verifique se o código na outra instância do Visual Studio é interrompido no ponto de interrupção que você definiu anteriormente no `RunStarted` método.

9. Continue a depurar o projeto escolhendo a tecla **F5** ou, na barra de menus, escolhendo **depurar**  >  **continuar**.

     O assistente para personalização do SharePoint é exibido.

10. Em **local**, escolha o botão de opção **lista de edição** .

11. Na lista **ID do grupo** , escolha **comunicações**.

12. Na caixa **título** , insira **centro de desenvolvedores do SharePoint**.

13. Na caixa **Descrição** , digite **abre o site do centro de desenvolvedores do SharePoint**.

14. Na caixa **URL** , digite **https://docs.microsoft.com/sharepoint/dev/** e, em seguida, escolha o botão **concluir** .

     O Visual Studio adiciona um item chamado **CustomAction1** ao seu projeto e abre o arquivo *Elements.xml* no editor. Verifique se *Elements.xml* contém os valores que você especificou no assistente.

#### <a name="to-test-the-custom-action-in-sharepoint"></a>Para testar a ação personalizada no SharePoint

1. Na instância experimental do Visual Studio, escolha a tecla **F5** ou, na barra de menus, escolha **depurar**  >  **Iniciar Depuração**.

     A ação personalizada é empacotada e implantada no site do SharePoint especificado pela propriedade **URL do site** do projeto e o navegador da Web é aberto na página padrão deste site.

    > [!NOTE]
    > Se a caixa de diálogo **depuração de script desabilitada** for exibida, escolha o botão **Sim** .

2. Na área listas do site do SharePoint, escolha o link **tarefas** .

     A página **tarefas – todas as tarefas** é exibida.

3. Na guia **ferramentas de lista** da faixa de opções, escolha a guia **lista** e, em seguida, no grupo **configurações** , escolha **configurações da lista**.

     A página **configurações da lista** é exibida.

4. No título **comunicações** próximo à parte superior da página, escolha o link **centro de desenvolvimento do SharePoint** , verifique se o navegador abre o site https://docs.microsoft.com/sharepoint/dev/ e feche o navegador.

## <a name="cleaning-up-the-development-computer"></a>Limpando o computador de desenvolvimento
 Depois de concluir o teste do item do projeto, remova o modelo de item do projeto da instância experimental do Visual Studio.

#### <a name="to-clean-up-the-development-computer"></a>Para limpar o computador de desenvolvimento

1. Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas**  >  **extensões e atualizações**.

     A caixa de diálogo **Extensões e Atualizações** é aberta.

2. Na lista de extensões, escolha a extensão de **item de projeto de ação personalizada** e, em seguida, escolha o botão **desinstalar** .

3. Na caixa de diálogo exibida, escolha o botão **Sim** para confirmar que você deseja desinstalar a extensão e, em seguida, escolha o botão **reiniciar agora** para concluir a desinstalação.

4. Feche as duas instâncias do Visual Studio (a instância experimental e a instância do Visual Studio na qual a solução CustomActionProjectItem está aberta).

## <a name="see-also"></a>Consulte também
- [Walkthrough: criar um item de projeto de ação personalizada com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)
- [Definir tipos de item de projeto personalizados do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [Criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Como usar assistentes com modelos do projeto](../extensibility/how-to-use-wizards-with-project-templates.md)
- [IDs e locais de ação personalizada padrão](/previous-versions/office/developer/sharepoint-2010/bb802730(v=office.14))
