---
title: Criar item de projeto de ação personalizada com modelo de item, parte 1
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, creating custom templates
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: eccb9038b9fd929c713422aa79082c94ade512fa
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015935"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-1"></a>Walkthrough: criar um item de projeto de ação personalizada com um modelo de item, parte 1
  Você pode estender o sistema de projeto do SharePoint no Visual Studio criando seus próprios tipos de item de projeto. Neste tutorial, você criará um item de projeto que pode ser adicionado a um projeto do SharePoint para criar uma ação personalizada em um site do SharePoint. A ação personalizada adiciona um item de menu ao menu **ações do site** do site do SharePoint.

 Este tutorial demonstra as seguintes tarefas:

- Criar uma extensão do Visual Studio que define um novo tipo de item de projeto do SharePoint para uma ação personalizada. O novo tipo de item de projeto implementa vários recursos personalizados:

  - Um menu de atalho que serve como um ponto de partida para tarefas adicionais relacionadas ao item do projeto, como exibir um designer para a ação personalizada no Visual Studio.

  - Código que é executado quando um desenvolvedor altera determinadas propriedades do item de projeto e o projeto que a contém.

  - Um ícone personalizado que aparece ao lado do item de projeto em **Gerenciador de soluções**.

- Criando um modelo de item do Visual Studio para o item de projeto.

- Criando um pacote de VSIX (Visual Studio Extension) para implantar o modelo de item de projeto e o assembly de extensão.

- Depurando e testando o item do projeto.

  Trata-se de uma explicação autônoma. Depois de concluir este passo a passos, você pode aprimorar o item de projeto adicionando um assistente ao modelo de item. Para obter mais informações, consulte [Walkthrough: criar um item de projeto de ação personalizada com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md).

> [!NOTE]
> Você pode baixar um exemplo do [GitHub](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) que mostra como criar atividades personalizadas para um fluxo de trabalho.

## <a name="prerequisites"></a>Pré-requisitos
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passos:

- Edições com suporte do Microsoft Windows, SharePoint e Visual Studio.

- O [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]. Este tutorial usa o modelo de **projeto VSIX** no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).

  O conhecimento dos seguintes conceitos é útil, mas não é necessário, para concluir o passo a passos:

- Ações personalizadas no SharePoint. Para obter mais informações, consulte [ação personalizada](/previous-versions/office/developer/sharepoint-2010/ms458635(v=office.14)).

- Modelos de item no Visual Studio. Para obter mais informações, consulte [Criando modelos de item e de projeto](../ide/creating-project-and-item-templates.md).

## <a name="create-the-projects"></a>Criar os projetos
 Para concluir este passo a passos, você precisa criar três projetos:

- Um projeto VSIX. Este projeto cria o pacote VSIX para implantar o item de projeto do SharePoint.

- Um projeto de modelo de item. Este projeto cria um modelo de item que pode ser usado para adicionar o item de projeto do SharePoint a um projeto do SharePoint.

- Um projeto de biblioteca de classes. Este projeto implementa uma extensão do Visual Studio que define o comportamento do item de projeto do SharePoint.

  Inicie o passo a passos criando os projetos.

#### <a name="to-create-the-vsix-project"></a>Para criar o projeto VSIX

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

3. Na lista na parte superior da caixa de diálogo **novo projeto** , verifique se **.NET Framework 4,5** está selecionado.

4. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha o nó **extensibilidade** .

    > [!NOTE]
    > O nó **extensibilidade** só estará disponível se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos anteriormente neste tópico.

5. Escolha o modelo de **projeto VSIX** .

6. Na caixa **nome** , digite **CustomActionProjectItem**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **CustomActionProjectItem** ao **Gerenciador de soluções**.

#### <a name="to-create-the-item-template-project"></a>Para criar o projeto de modelo de item

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na lista na parte superior da caixa de diálogo **novo projeto** , verifique se **.NET Framework 4,5** está selecionado.

3. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha o nó **extensibilidade** .

4. Na lista de modelos do projeto, escolha o modelo de **Item C#** ou modelo de **modelo de item de Visual Basic** .

5. Na caixa **nome** , digite **ItemTemplate**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **ItemTemplate** à solução.

#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na lista na parte superior da caixa de diálogo **novo projeto** , verifique se **.NET Framework 4,5** está selecionado.

3. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** , escolha o nó **Windows** e, em seguida, escolha o modelo de projeto de **biblioteca de classes** .

4. Na caixa **nome** , digite **ProjectItemDefinition**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **ProjectItemDefinition** à solução e abre o arquivo de código de Class1 padrão.

5. Exclua o arquivo de código Class1 do projeto.

## <a name="configure-the-extension-project"></a>Configurar o projeto de extensão
 Antes de escrever o código para definir o tipo de item de projeto do SharePoint, você precisa adicionar arquivos de código e referências de assembly ao projeto de extensão.

#### <a name="to-configure-the-project"></a>Para configurar o projeto

1. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **ProjectItemDefinition** , escolha **Adicionar**e, em seguida, escolha **novo item**.

2. Na lista de itens de projeto, escolha **arquivo de código**.

3. Na caixa **nome** , digite o nome **CustomAction** com a extensão de nome de arquivo apropriada e, em seguida, escolha o botão **Adicionar** .

4. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **ProjectItemDefinition** e escolha **Adicionar referência**.

5. Na caixa de diálogo **Gerenciador de referências-ProjectItemDefinition** , escolha o nó **assemblies** e, em seguida, escolha o nó **estrutura** .

6. Marque a caixa de seleção ao lado de cada um dos seguintes assemblies:

    - System. ComponentModel. composição

    - System.Windows.Forms

7. Escolha o nó **extensões** , marque a caixa de seleção ao lado do assembly Microsoft. VisualStudio. SharePoint e, em seguida, escolha o botão **OK** .

## <a name="define-the-new-sharepoint-project-item-type"></a>Definir o novo tipo de item de projeto do SharePoint
 Crie uma classe que implemente a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> interface para definir o comportamento do novo tipo de item de projeto. Implemente essa interface sempre que desejar definir um novo tipo de item de projeto.

#### <a name="to-define-the-new-sharepoint-project-item-type"></a>Para definir o novo tipo de item de projeto do SharePoint

1. No projeto ProjectItemDefinition, abra o arquivo de código CustomAction.

2. Substitua o código deste arquivo pelo código a seguir.

     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#1](../sharepoint/codesnippet/CSharp/customactionprojectitem/projectitemtypedefinition/customaction.cs#1)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#1](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/projectitemdefinition/customaction.vb#1)]

## <a name="create-an-icon-for-the-project-item-in-solution-explorer"></a>Criar um ícone para o item de projeto no Gerenciador de Soluções
 Ao criar um item de projeto personalizado do SharePoint, você pode associar uma imagem (um ícone ou bitmap) ao item do projeto. Essa imagem é exibida ao lado do item de projeto em **Gerenciador de soluções**.

 No procedimento a seguir, você cria um ícone para o item de projeto e insere o ícone no assembly de extensão. Esse ícone é referenciado pelo <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute> da `CustomActionProjectItemTypeProvider` classe que você criou anteriormente.

#### <a name="to-create-a-custom-icon-for-the-project-item"></a>Para criar um ícone personalizado para o item de projeto

1. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **ProjectItemDefinition** , escolha **Adicionar**e, em seguida, escolha **novo item...**.

2. Na lista de itens de projeto, escolha o item de **arquivo de ícone** .

    > [!NOTE]
    > Em projetos Visual Basic, você deve escolher o nó **geral** para exibir o item de **arquivo de ícone** .

3. Na caixa **nome** , digite **CustomAction_SolutionExplorer. ico**e, em seguida, escolha o botão **Adicionar** .

     O novo ícone é aberto no **Editor de imagem**.

4. Edite a versão 16x16 do arquivo de ícone para que ele tenha um design que você possa reconhecer e, em seguida, salve o arquivo de ícone.

5. Em **Gerenciador de soluções**, escolha **CustomAction_SolutionExplorer. ico**.

6. Na janela **Propriedades** , escolha a seta ao lado da propriedade **criar ação** .

7. Na lista exibida, escolha **recurso inserido**.

## <a name="checkpoint"></a>Ponto de verificação
 Neste ponto do passo a passo, todo o código para o item de projeto agora está no projeto. Compile o projeto para verificar se ele é compilado sem erros.

#### <a name="to-build-your-project"></a>Para compilar seu projeto

1. Abra o menu de atalho para o projeto **ProjectItemDefinition** e escolha **Compilar**.

## <a name="create-a-visual-studio-item-template"></a>Criar um modelo de item do Visual Studio
 Para permitir que outros desenvolvedores usem seu item de projeto, você deve criar um modelo de projeto ou um modelo de item. Os desenvolvedores usam esses modelos no Visual Studio para criar uma instância do item de projeto criando um novo projeto ou adicionando um item a um projeto existente. Para esta explicação, use o projeto ItemTemplate para configurar o item do projeto.

#### <a name="to-create-the-item-template"></a>Para criar o modelo de item

1. Exclua o arquivo de código Class1 do projeto ItemTemplate.

2. No projeto ItemTemplate, abra o arquivo *ItemTemplate. vstemplate* .

3. Substitua o conteúdo do arquivo pelo XML a seguir e, em seguida, salve e feche o arquivo.

    > [!NOTE]
    > O XML a seguir é para um modelo de item do Visual C#. Se você estiver criando um modelo de item de Visual Basic, substitua o valor do `ProjectType` elemento por `VisualBasic` .

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <VSTemplate Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vstemplate/2005" Type="Item">
      <TemplateData>
        <DefaultName>CustomAction</DefaultName>
        <Name>Custom Action</Name>
        <Description>SharePoint Custom Action by Contoso</Description>
        <ProjectType>CSharp</ProjectType>
        <SortOrder>1000</SortOrder>
        <Icon>ItemTemplate.ico</Icon>
        <ProvideDefaultName>true</ProvideDefaultName>
      </TemplateData>
      <TemplateContent>
        <ProjectItem ReplaceParameters="true" TargetFileName="$fileinputname$\Elements.xml">Elements.xml</ProjectItem>
        <ProjectItem ReplaceParameters="true" TargetFileName="$fileinputname$\SharePointProjectItem.spdata">CustomAction.spdata</ProjectItem>
      </TemplateContent>
    </VSTemplate>
    ```

     Esse arquivo define o conteúdo e o comportamento do modelo de item. Para obter mais informações sobre o conteúdo desse arquivo, consulte [referência de esquema de modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md).

4. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **ItemTemplate** , escolha **Adicionar**e, em seguida, escolha **novo item**.

5. Na caixa de diálogo **Adicionar novo item** , escolha o modelo de **arquivo de texto** .

6. Na caixa **nome** , digite **CustomAction. OnData**e, em seguida, escolha o botão **Adicionar** .

7. Adicione o seguinte XML ao arquivo *CustomAction. OnData* e salve e feche o arquivo.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <ProjectItem Type="Contoso.CustomAction" DefaultFile="Elements.xml"
     xmlns="http://schemas.microsoft.com/VisualStudio/2010/SharePointTools/SharePointProjectItemModel">
      <Files>
        <ProjectItemFile Source="Elements.xml" Target="$fileinputname$\" Type="ElementManifest" />
      </Files>
    </ProjectItem>
    ```

     Esse arquivo contém informações sobre os arquivos contidos no item de projeto. O `Type` atributo do `ProjectItem` elemento deve ser definido como a mesma cadeia de caracteres que é passada para a <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> na definição de item do projeto (a `CustomActionProjectItemTypeProvider` classe que você criou anteriormente neste passo a passos). Para obter mais informações sobre o conteúdo de arquivos *. OnData* , consulte [referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md).

8. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **ItemTemplate** , escolha **Adicionar**e, em seguida, escolha **novo item**.

9. Na caixa de diálogo **Adicionar novo item** , escolha o modelo de **arquivo XML** .

10. Na caixa **nome** , digite **Elements.xml**e, em seguida, escolha o botão **Adicionar** .

11. Substitua o conteúdo do arquivo de *Elements.xml* pelo seguinte XML e, em seguida, salve e feche o arquivo.

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Elements Id="$guid8$" xmlns="http://schemas.microsoft.com/sharepoint/">
      <CustomAction Id="Replace this with a GUID or some other unique string"
                    GroupId="SiteActions"
                    Location="Microsoft.SharePoint.StandardMenu"
                    Sequence="1000"
                    Title="Replace this with your title"
                    Description="Replace this with your description" >
        <UrlAction Url="~site/Lists/Tasks/AllItems.aspx"/>
      </CustomAction>
    </Elements>
    ```

     Esse arquivo define uma ação personalizada padrão que cria um item de menu no menu **ações** do site do site do SharePoint. Quando um usuário escolhe o item de menu, a URL especificada no `UrlAction` elemento é aberta no navegador da Web. Para obter mais informações sobre os elementos XML que você pode usar para definir uma ação personalizada, consulte [definições de ação personalizadas](/sharepoint/dev/schema/custom-action-definition-schema).

12. Opcionalmente, abra o arquivo *ItemTemplate. ico* e modifique-o para que ele tenha um design que você possa reconhecer. Esse ícone será exibido ao lado do item de projeto na caixa de diálogo **Adicionar novo item** .

13. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **ItemTemplate** e escolha **descarregar projeto**.

14. Abra o menu de atalho para o projeto **ItemTemplate** novamente e escolha **Editar ItemTemplate. csproj** ou **Editar ItemTemplate. vbproj**.

15. Localize o seguinte `VSTemplate` elemento no arquivo de projeto.

    ```xml
    <VSTemplate Include="ItemTemplate.vstemplate">
    ```

16. Substitua esse `VSTemplate` elemento pelo XML a seguir e, em seguida, salve e feche o arquivo.

    ```xml
    <VSTemplate Include="ItemTemplate.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     O `OutputSubPath` elemento especifica pastas adicionais no caminho em que o modelo de item é criado quando você cria o projeto. As pastas especificadas aqui garantem que o modelo de item estará disponível somente quando os clientes abrirem a caixa de diálogo **Adicionar novo item** , expandir o nó do **SharePoint** e, em seguida, escolher o nó **2010** .

17. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **ItemTemplate** e, em seguida, escolha **recarregar projeto**.

## <a name="create-a-vsix-package-to-deploy-the-project-item"></a>Criar um pacote VSIX para implantar o item de projeto
 Para implantar a extensão, use o projeto VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo. Extension. vsixmanifest de origem que está incluído no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.

#### <a name="to-configure-and-create-the-vsix-package"></a>Para configurar e criar o pacote VSIX

1. No **Gerenciador de soluções**, abra o menu de atalho do arquivo **Source. Extension. vsixmanifest** no projeto CustomActionProjectItem e, em seguida, escolha **abrir**.

     O Visual Studio abre o arquivo no editor de manifesto. O arquivo Source. Extension. vsixmanifest é a base para o arquivo extension. vsixmanifest que todos os pacotes VSIX exigem. Para obter mais informações sobre esse arquivo, consulte [referência do esquema de extensão do VSIX 1,0](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).

2. Na caixa **nome do produto** , insira **item de projeto de ação personalizada**.

3. Na caixa **autor** , digite **contoso**.

4. Na caixa **Descrição** , insira **um item de projeto do SharePoint que representa uma ação personalizada**.

5. Na guia **ativos** , escolha o botão **novo** .

     A caixa de diálogo **Adicionar novo ativo** é exibida.

6. Na lista **tipo** , escolha **Microsoft. VisualStudio. ItemTemplate**.

    > [!NOTE]
    > Esse valor corresponde ao `ItemTemplate` elemento no arquivo extension. vsixmanifest. Esse elemento identifica a subpasta no pacote VSIX que contém o modelo de item de projeto. Para obter mais informações, consulte [elemento ItemTemplate (esquema VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\)).

7. Na lista **origem** , escolha **um projeto na solução atual**.

8. Na lista **projeto** , escolha **ItemTemplate**e, em seguida, escolha o botão **OK** .

9. Na guia **ativos** , escolha o botão **novo** novamente.

     A caixa de diálogo **Adicionar novo ativo** é exibida.

10. Na lista **tipo** , escolha **Microsoft. VisualStudio. MefComponent**.

    > [!NOTE]
    > Esse valor corresponde ao `MefComponent` elemento no arquivo extension. vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [elemento MEFComponent (esquema VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).

11. Na lista **origem** , escolha **um projeto na solução atual**.

12. Na lista **projeto** , escolha **ProjectItemDefinition**.

13. Clique no botão **OK**.

14. Na barra de menus, escolha **criar**  >  **solução de compilação**e, em seguida, certifique-se de que o projeto seja compilado sem erros.

15. Verifique se a pasta de saída da compilação do projeto CustomActionProjectItem contém o arquivo CustomActionProjectItem. vsix.

     Por padrão, a pasta de saída da compilação é a.. \bin\Debug na pasta que contém o projeto CustomActionProjectItem.

## <a name="test-the-project-item"></a>Testar o item do projeto
 Agora você está pronto para testar o item do projeto. Primeiro, inicie a depuração da solução CustomActionProjectItem na instância experimental do Visual Studio. Em seguida, teste o item de projeto de **ação personalizada** em um projeto do SharePoint na instância experimental do Visual Studio. Por fim, compile e execute o projeto do SharePoint para verificar se a ação personalizada funciona conforme o esperado.

#### <a name="to-start-debugging-the-solution"></a>Para iniciar a depuração da solução

1. Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução CustomActionProjectItem.

2. Abra o arquivo de código CustomAction e, em seguida, adicione um ponto de interrupção à primeira linha de código no `InitializeType` método.

3. Escolha a tecla **F5** para iniciar a depuração.

     O Visual Studio instala a extensão para o projeto de ação%UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\Custom Item\1.0 e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.

#### <a name="to-test-the-project-item-in-visual-studio"></a>Para testar o item de projeto no Visual Studio

1. Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Expanda **Visual C#** ou **Visual Basic** (dependendo do idioma ao qual o modelo de item dá suporte), expanda **SharePoint**e escolha o nó **2010** .

3. Na lista de modelos de projeto, escolha **projeto do SharePoint 2010**.

4. Na caixa **nome** , digite **CustomActionTest**e, em seguida, escolha o botão **OK** .

5. No **Assistente para personalização do SharePoint**, insira a URL do site que você deseja usar para depuração e, em seguida, escolha o botão **concluir** .

6. No **Gerenciador de soluções**, abra o menu de atalho para o nó do projeto, escolha **Adicionar**e, em seguida, escolha **novo item**.

7. Na caixa de diálogo **Adicionar novo item** , escolha o nó **2010** no nó do **SharePoint** .

     Verifique se o item de **ação personalizada** aparece na lista de itens de projeto.

8. Escolha o item de **ação personalizada** e, em seguida, escolha o botão **Adicionar** .

     O Visual Studio adiciona um item chamado **CustomAction1** ao seu projeto e abre o arquivo *Elements.xml* no editor.

9. Verifique se o código na outra instância do Visual Studio é interrompido no ponto de interrupção que você definiu anteriormente no `InitializeType` método.

10. Escolha a tecla **F5** para continuar a depurar o projeto.

11. Na instância experimental do Visual Studio, em **Gerenciador de soluções**, abra o menu de atalho para o nó **CustomAction1** e escolha **Exibir Designer de ação personalizado**.

12. Verifique se uma caixa de mensagem aparece e, em seguida, escolha o botão **OK** .

     Você pode usar esse menu de atalho para fornecer opções adicionais ou comandos para desenvolvedores, como exibir um designer para a ação personalizada.

13. Na barra de menus, escolha **Exibir**  >  **saída**.

     A janela **saída** é aberta.

14. No **Gerenciador de soluções**, abra o menu de atalho do item **CustomAction1** e altere seu nome para **MyCustomAction**.

     Na janela **saída** , uma mensagem de confirmação é exibida. Essa mensagem é escrita pelo <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemNameChanged> manipulador de eventos que você definiu na `CustomActionProjectItemTypeProvider` classe. Você pode manipular esse evento e outros eventos de item de projeto para implementar o comportamento personalizado quando o desenvolvedor modifica o item de projeto.

#### <a name="to-test-the-custom-action-in-sharepoint"></a>Para testar a ação personalizada no SharePoint

1. Na instância experimental do Visual Studio, abra o arquivo *Elements.xml* que é um filho do item de projeto **mycustomizable** .

2. No arquivo de *Elements.xml* , faça as seguintes alterações e, em seguida, salve o arquivo:

    - No `CustomAction` elemento, defina o `Id` atributo como um GUID ou alguma outra cadeia de caracteres exclusiva, como mostra o exemplo a seguir:

        ```xml
        Id="cd85f6a7-af2e-44ab-885a-0c795b52121a"
        ```

    - No `CustomAction` elemento, defina o `Title` atributo como mostra o exemplo a seguir:

        ```xml
        Title="SharePoint Developer Center"
        ```

    - No `CustomAction` elemento, defina o `Description` atributo como mostra o exemplo a seguir:

        ```xml
        Description="Opens the SharePoint Developer Center Web site."
        ```

    - No `UrlAction` elemento, defina o `Url` atributo como mostra o exemplo a seguir:

        ```xml
        Url="https://docs.microsoft.com/sharepoint/dev/"
        ```

3. Pressione a tecla **F5**.

     A ação personalizada é empacotada e implantada no site do SharePoint que é especificado na propriedade **URL do site** do projeto. O navegador da Web é aberto na página padrão deste site.

    > [!NOTE]
    > Se a caixa de diálogo **depuração de script desabilitada** for exibida, escolha o botão **Sim** para continuar a depurar o projeto.

4. No menu **ações do site** , escolha **centro de desenvolvimento do SharePoint**, verifique se o navegador abre o site https://docs.microsoft.com/sharepoint/dev/ e, em seguida, feche o navegador da Web.

## <a name="clean-up-the-development-computer"></a>Limpar o computador de desenvolvimento
 Depois de concluir o teste do item do projeto, remova o modelo de item do projeto da instância experimental do Visual Studio.

#### <a name="to-clean-up-the-development-computer"></a>Para limpar o computador de desenvolvimento

1. Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas**  >  **extensões e atualizações**.

     A caixa de diálogo **Extensões e Atualizações** é aberta.

2. Na lista de extensões, escolha **item de projeto de ação personalizada**e, em seguida, escolha o botão **desinstalar** .

3. Na caixa de diálogo exibida, escolha o botão **Sim** para confirmar que você deseja desinstalar a extensão.

4. Escolha o botão **reiniciar agora** para concluir a desinstalação.

5. Feche a instância experimental do Visual Studio e a instância na qual a solução CustomActionProjectItem está aberta.

## <a name="next-steps"></a>Próximas etapas
 Depois de concluir este passo a passos, você pode adicionar um assistente ao modelo de item. Quando um usuário adiciona um item de projeto de ação personalizada a um projeto do SharePoint, o assistente coleta informações sobre a ação (como sua localização e a URL para navegar quando a ação é escolhida) e adiciona essas informações ao arquivo de *Elements.xml* no novo item de projeto. Para obter mais informações, consulte [Walkthrough: criar um item de projeto de ação personalizada com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md).

## <a name="see-also"></a>Consulte também

- [Walkthrough: criar um item de projeto de ação personalizada com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)
- [Definir tipos de item de projeto personalizados do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)
- [Criar modelos de item e modelos de projeto para itens de projeto do SharePoint](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)
- [Usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md)
- [Referência de esquema do modelo do Visual Studio](../extensibility/visual-studio-template-schema-reference.md)
- [Editor de imagem para ícones](/cpp/windows/image-editor-for-icons)
- [Criando um ícone ou outro editor de imagem de &#40;de imagem para ícones&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)