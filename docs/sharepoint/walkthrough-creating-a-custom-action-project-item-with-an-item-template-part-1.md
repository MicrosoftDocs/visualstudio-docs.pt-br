---
title: 'Passo a passo: Criando um Item de projeto de ação personalizado com um modelo de Item, parte 1 | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint project items, creating custom templates
- SharePoint project items, defining your own types
- project items [SharePoint development in Visual Studio], defining your own types
- SharePoint development in Visual Studio, defining new project item types
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 8144723f68b9343c1c7d74f7a940aec569dd7969
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296119"
---
# <a name="walkthrough-create-a-custom-action-project-item-with-an-item-template-part-1"></a>Passo a passo: Criar um item de projeto de ação personalizado com um modelo de item, parte 1
  Você pode estender o sistema de projeto do SharePoint no Visual Studio com a criação de tipos de item de seu próprio projeto. Neste passo a passo, você criará um item de projeto que pode ser adicionado a um projeto do SharePoint para criar uma ação personalizada em um site do SharePoint. A ação personalizada adiciona um item de menu para o **ações do Site** menu do site do SharePoint.  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
- Criando uma extensão do Visual Studio que define um novo tipo de item de projeto do SharePoint para uma ação personalizada. O novo tipo de item de projeto implementa vários recursos personalizados:  
  
  -   Um menu de atalho que serve como ponto de partida para tarefas adicionais relacionados ao item do projeto, como a exibição de um designer para a ação personalizada no Visual Studio.  
  
  -   Código que é executado quando um desenvolvedor altera determinadas propriedades de item de projeto e o projeto que o contém.  
  
  -   Um ícone personalizado que aparece ao lado do item de projeto no **Gerenciador de soluções**.  
  
- Criando um modelo de item do Visual Studio para o item de projeto.  
  
- Criando um pacote de extensão VSIX (Visual Studio) para implantar o modelo de item de projeto e o assembly de extensão.  
  
- Depurando e testando o item de projeto.  
  
  Esse é um passo a passo autônoma. Depois de concluir este passo a passo, você pode aprimorar o item de projeto com a adição de um Assistente para o modelo de item. Para obter mais informações, consulte [instruções passo a passo: criar um item de projeto de ação personalizado com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md).  
  
> [!NOTE]  
>  Você pode baixar um exemplo de [Github](https://github.com/SharePoint/PnP/tree/master/Samples/Workflow.Activities) que mostra como criar atividades personalizadas para um fluxo de trabalho.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passo:  
  
- Edições com suporte do Microsoft Windows, SharePoint e do Visual Studio.
  
- O [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]. Este passo a passo usa o **VSIX Project** modelo no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).  
  
  Conhecimento dos conceitos a seguir é útil, mas não necessário para concluir o passo a passo:  
  
- Ações personalizadas no SharePoint. Para obter mais informações, consulte [ação personalizada](http://go.microsoft.com/fwlink/?LinkId=177800).  
  
- Modelos de item no Visual Studio. Para obter mais informações, consulte [Criando modelos de item e de projeto](/visualstudio/ide/creating-project-and-item-templates).  
  
## <a name="create-the-projects"></a>Crie os projetos
 Para concluir este passo a passo, você precisa criar três projetos:  
  
- Um projeto VSIX. Esse projeto cria o pacote VSIX para implantar o item de projeto do SharePoint.  
  
- Um projeto de modelo de item. Esse projeto cria um modelo de item que pode ser usado para adicionar o item de projeto do SharePoint a um projeto do SharePoint.  
  
- Um projeto de biblioteca de classes. Este projeto implementa uma extensão do Visual Studio que define o comportamento do item de projeto do SharePoint.  
  
  Inicie o passo a passo Criando os projetos.  
  
#### <a name="to-create-the-vsix-project"></a>Para criar o projeto do VSIX  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
3.  Na lista na parte superior dos **novo projeto** diálogo caixa, certifique-se de que **.NET Framework 4.5** está selecionado.  
  
4.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha o **extensibilidade** nó.  
  
    > [!NOTE]  
    >  O **extensibilidade** o nó está disponível somente se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos no início deste tópico.  
  
5.  Escolha o **VSIX Project** modelo.  
  
6.  No **nome** , digite **CustomActionProjectItem**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **CustomActionProjectItem** projeto ao **Gerenciador de soluções**.  
  
#### <a name="to-create-the-item-template-project"></a>Para criar o projeto de modelo de item  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do nó da solução, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
2.  Na lista na parte superior dos **novo projeto** diálogo caixa, certifique-se de que **.NET Framework 4.5** está selecionado.  
  
3.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha o **extensibilidade** nó.  
  
4.  Na lista de modelos de projeto, escolha o **modelo de Item de c#** ou **modelo de Item do Visual Basic** modelo.  
  
5.  No **nome** , digite **ItemTemplate**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **ItemTemplate** projeto à solução.  
  
#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do nó da solução, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
2.  Na lista na parte superior dos **novo projeto** diálogo caixa, certifique-se de que **.NET Framework 4.5** está selecionado.  
  
3.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós, escolha o **Windows** nó e, em seguida, escolha o  **Biblioteca de classes** modelo de projeto.  
  
4.  No **nome** , digite **ProjectItemDefinition**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **ProjectItemDefinition** projeto à solução e abre o arquivo de código padrão Class1.  
  
5.  Exclua o arquivo de código Class1 do projeto.  
  
## <a name="configure-the-extension-project"></a>Configurar o projeto de extensão
 Antes de escrever código para definir o tipo de item de projeto do SharePoint, você precisa adicionar os arquivos de código e referências de assembly ao projeto de extensão.  
  
#### <a name="to-configure-the-project"></a>Para configurar o projeto  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **ProjectItemDefinition** do projeto, escolha **adicionar**, em seguida, escolha **Novo Item**.  
  
2.  Na lista de itens de projeto, escolha **arquivo de código**.  
  
3.  No **nome** , digite o nome **CustomAction** com os devidos a extensão de nome de arquivo e, em seguida, escolha o **Add** botão.  
  
4.  Na **Gerenciador de soluções**, abra o menu de atalho para o **ProjectItemDefinition** do projeto e, em seguida, escolha **Add Reference**.  
  
5.  No **Gerenciador de referências - ProjectItemDefinition** diálogo caixa, escolha o **Assemblies** nó e, em seguida, escolha o **Framework** nó.  
  
6.  Marque a caixa de seleção ao lado de cada um dos seguintes assemblies:  
  
    -   System.ComponentModel.Composition  
  
    -   System.Windows.Forms  
  
7.  Escolha o **extensões** nó, selecione a caixa de seleção ao lado do assembly Microsoft.VisualStudio.Sharepoint e, em seguida, escolha o **Okey** botão.  
  
## <a name="define-the-new-sharepoint-project-item-type"></a>Definir o novo tipo de item de projeto do SharePoint
 Criar uma classe que implementa o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeProvider> interface para definir o comportamento do novo tipo de item de projeto. Implemente essa interface sempre que você deseja definir um novo tipo de item de projeto.  
  
#### <a name="to-define-the-new-sharepoint-project-item-type"></a>Para definir o novo tipo de item de projeto do SharePoint  
  
1.  No projeto ProjectItemDefinition, abra o arquivo de código CustomAction.  
  
2.  Substitua o código nesse arquivo com o código a seguir.  
  
     [!code-csharp[SPExtensibility.ProjectItem.CustomAction#1](../sharepoint/codesnippet/CSharp/customactionprojectitem/projectitemtypedefinition/customaction.cs#1)]
     [!code-vb[SPExtensibility.ProjectItem.CustomAction#1](../sharepoint/codesnippet/VisualBasic/customactionprojectitem/projectitemdefinition/customaction.vb#1)]  
  
## <a name="create-an-icon-for-the-project-item-in-solution-explorer"></a>Criar um ícone para o item de projeto no Gerenciador de soluções
 Quando você cria um item de projeto personalizado do SharePoint, você pode associar uma imagem (um ícone ou bitmap) com o item de projeto. Essa imagem é exibida próxima ao item de projeto no **Gerenciador de soluções**.  
  
 No procedimento a seguir, você cria um ícone para o item de projeto e incorporar o ícone no assembly de extensão. Esse ícone é referenciado pela <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemIconAttribute> do `CustomActionProjectItemTypeProvider` classe que você criou anteriormente.  
  
#### <a name="to-create-a-custom-icon-for-the-project-item"></a>Para criar um ícone personalizado para o item de projeto  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **ProjectItemDefinition** do projeto, escolha **Add**e, em seguida, escolha **Novo Item...** .  
  
2.  Na lista de itens de projeto, escolha o **arquivo de ícone** item.  
  
    > [!NOTE]  
    >  Em projetos do Visual Basic, você deve escolher o **gerais** nó para exibir o **arquivo de ícone** item.  
  
3.  No **nome** , digite **CustomAction_SolutionExplorer.ico**e, em seguida, escolha o **Add** botão.  
  
     O novo ícone abre na **Editor de imagens**.  
  
4.  Edite a versão de 16x16 do ícone de arquivo para que ele tenha um design que você pode reconhecer e, em seguida, salve o arquivo de ícone.  
  
5.  Na **Gerenciador de soluções**, escolha **CustomAction_SolutionExplorer.ico**.  
  
6.  No **propriedades** janela, escolha a seta ao lado de **Build Action** propriedade.  
  
7.  Na lista que aparece, escolha **Embedded Resource**.  
  
## <a name="checkpoint"></a>Ponto de verificação  
 Neste momento no passo a passo, todo o código para o item de projeto agora está no projeto. Compile o projeto para verificar se ele é compilado sem erros.  
  
#### <a name="to-build-your-project"></a>Para compilar seu projeto  
  
1.  Abra o menu de atalho para o **ProjectItemDefinition** do projeto e escolha **Build**.  
  
## <a name="create-a-visual-studio-item-template"></a>Criar um modelo de item do Visual Studio
 Para habilitar outros desenvolvedores a usar o item de projeto, você deve criar um modelo de projeto ou o modelo de item. Os desenvolvedores usar esses modelos no Visual Studio para criar uma instância do seu item de projeto, criando um novo projeto, ou adicionando um item a um projeto existente. Para este passo a passo, use o projeto ItemTemplate para configurar seu item de projeto.  
  
#### <a name="to-create-the-item-template"></a>Para criar o modelo de item  
  
1.  Exclua o arquivo de código Class1 do projeto ItemTemplate.  
  
2.  No projeto ItemTemplate, abra o *ItemTemplate.vstemplate* arquivo.  
  
3.  Substitua o conteúdo do arquivo pelo XML a seguir e, em seguida, salve e feche o arquivo.  
  
    > [!NOTE]  
    >  O XML a seguir é para um modelo de item do Visual c#. Se você estiver criando um modelo de item do Visual Basic, substitua o valor de `ProjectType` elemento com `VisualBasic`.  
  
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
  
     Esse arquivo define o conteúdo e o comportamento do modelo de item. Para obter mais informações sobre o conteúdo desse arquivo, consulte [referência de esquema de modelo do Visual Studio](/visualstudio/extensibility/visual-studio-template-schema-reference).  
  
4.  Na **Gerenciador de soluções**, abra o menu de atalho para o **ItemTemplate** do projeto, escolha **Add**e, em seguida, escolha **Novo Item**.  
  
5.  No **Adicionar Novo Item** diálogo caixa, escolha o **arquivo de texto** modelo.  
  
6.  No **nome** , digite **CustomAction.spdata**e, em seguida, escolha o **Add** botão.  
  
7.  Adicione o seguinte XML para o *CustomAction.spdata* de arquivo e, em seguida, salve e feche o arquivo.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8"?>  
    <ProjectItem Type="Contoso.CustomAction" DefaultFile="Elements.xml"   
     xmlns="http://schemas.microsoft.com/VisualStudio/2010/SharePointTools/SharePointProjectItemModel">  
      <Files>  
        <ProjectItemFile Source="Elements.xml" Target="$fileinputname$\" Type="ElementManifest" />  
      </Files>  
    </ProjectItem>  
    ```  
  
     Esse arquivo contém informações sobre os arquivos contidos no item de projeto. O `Type` atributo do `ProjectItem` elemento deve ser definido para a mesma cadeia de caracteres que é passada para o <xref:Microsoft.VisualStudio.SharePoint.SharePointProjectItemTypeAttribute> na definição do item de projeto (o `CustomActionProjectItemTypeProvider` classe que você criou anteriormente neste passo a passo). Para obter mais informações sobre o conteúdo do *. spdata* arquivos, consulte [referência de esquema de item de projeto do SharePoint](../sharepoint/sharepoint-project-item-schema-reference.md).  
  
8.  Na **Gerenciador de soluções**, abra o menu de atalho para o **ItemTemplate** do projeto, escolha **Add**e, em seguida, escolha **Novo Item**.  
  
9. No **Adicionar Novo Item** diálogo caixa, escolha o **arquivo XML** modelo.  
  
10. No **nome** , digite **Elements. XML**e, em seguida, escolha o **Add** botão.  
  
11. Substitua o conteúdo do *Elements. XML* do arquivo pelo XML a seguir e, em seguida, salve e feche o arquivo.  
  
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
  
     Esse arquivo define uma ação personalizada padrão que cria um item de menu sob o **ações do Site** menu do site do SharePoint. Quando um usuário escolhe o item de menu, a URL especificada no `UrlAction` elemento é aberta no navegador da web. Para obter mais informações sobre os elementos XML que você pode usar para definir uma ação personalizada, consulte [definições personalizadas de ação](http://go.microsoft.com/fwlink/?LinkId=177801).  
  
12. Opcionalmente, abra o *ItemTemplate.ico* de arquivo e modificá-lo para que ele tenha um design que você pode reconhecer. Esse ícone será exibido próximo ao item de projeto na **Adicionar Novo Item** caixa de diálogo.  
  
13. Na **Gerenciador de soluções**, abra o menu de atalho para o **ItemTemplate** do projeto e, em seguida, escolha **descarregar projeto**.  
  
14. Abra o menu de atalho para o **ItemTemplate** do projeto novamente e, em seguida, escolha **Editar ItemTemplate.csproj** ou **ItemTemplate.vbproj editar**.  
  
15. Localize o seguinte `VSTemplate` elemento no arquivo de projeto.  
  
    ```xml  
    <VSTemplate Include="ItemTemplate.vstemplate">  
    ```  
  
16. Substituir isso `VSTemplate` elemento com o XML a seguir e, depois, salve e feche o arquivo.  
  
    ```xml  
    <VSTemplate Include="ItemTemplate.vstemplate">  
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>  
    </VSTemplate>  
    ```  
  
     O `OutputSubPath` elemento Especifica as pastas adicionais no caminho em que o modelo de item é criado quando você compila o projeto. As pastas especificadas aqui Certifique-se de que o modelo de item estará disponível somente quando os clientes abrir o **Adicionar Novo Item** diálogo caixa, expanda o **SharePoint** nó e, em seguida, escolha o **2010**  nó.  
  
17. Na **Gerenciador de soluções**, abra o menu de atalho para o **ItemTemplate** do projeto e, em seguida, escolha **recarregar projeto**.  
  
## <a name="create-a-vsix-package-to-deploy-the-project-item"></a>Criar um pacote VSIX para implantar o item de projeto
 Para implantar a extensão, use o projeto do VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo vsixmanifest que está incluído no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.  
  
#### <a name="to-configure-and-create-the-vsix-package"></a>Para configurar e criar o pacote VSIX  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **vsixmanifest** arquivo no projeto CustomActionProjectItem e, em seguida, escolha **abrir**.  
  
     Visual Studio abre o arquivo no editor de manifesto. O arquivo vsixmanifest é a base para o arquivo Extension vsixmanifest que exigem todos os pacotes VSIX. Para obter mais informações sobre esse arquivo, consulte [1.0 referência do esquema de extensão do VSIX](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).  
  
2.  No **nome do produto** , digite **Item de projeto de ação personalizado**.  
  
3.  No **autor** , digite **Contoso**.  
  
4.  No **descrição** , digite **SharePoint de um item de projeto que representa uma ação personalizada**.  
  
5.  Sobre o **ativos** guia, escolha o **New** botão.  
  
     O **adicionar novo ativo** caixa de diálogo é exibida.  
  
6.  No **tipo** , escolha **Microsoft.VisualStudio.ItemTemplate**.  
  
    > [!NOTE]  
    >  Esse valor corresponde à `ItemTemplate` elemento no arquivo Extension vsixmanifest. Este elemento identifica a subpasta no pacote VSIX que contém o modelo de item de projeto. Para obter mais informações, consulte [ItemTemplate Element (esquema de VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\)).  
  
7.  No **fonte** , escolha **um projeto na solução atual**.  
  
8.  No **Project** , escolha **ItemTemplate**e, em seguida, escolha o **Okey** botão.  
  
9. No **ativos** guia, escolha o **New** novamente no botão.  
  
     O **adicionar novo ativo** caixa de diálogo é exibida.  
  
10. No **tipo** , escolha **mefcomponent**.  
  
    > [!NOTE]  
    >  Esse valor corresponde à `MefComponent` elemento no arquivo Extension vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [MEFComponent Element (esquema de VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).  
  
11. No **fonte** , escolha **um projeto na solução atual**.  
  
12. No **Project** , escolha **ProjectItemDefinition**.  
  
13. Escolha o botão **OK**.  
  
14. Na barra de menus, escolha **construir** > **compilar solução**e, em seguida, certifique-se de que o projeto é compilado sem erros.  
  
15. Certifique-se de que a pasta de saída de compilação para o projeto CustomActionProjectItem contém o arquivo CustomActionProjectItem.vsix.  
  
     Por padrão, a pasta de saída de compilação é o... pasta \bin\debug sob a pasta que contém o projeto CustomActionProjectItem.  
  
## <a name="test-the-project-item"></a>O item de projeto de teste
 Agora você está pronto para testar o item de projeto. Primeiro, inicie a depuração da solução CustomActionProjectItem na instância experimental do Visual Studio. Em seguida, testar o **ação personalizada** item de projeto em um projeto do SharePoint na instância experimental do Visual Studio. Por fim, compile e execute o projeto do SharePoint para verificar se a ação personalizada funciona conforme o esperado.  
  
#### <a name="to-start-debugging-the-solution"></a>Para iniciar a depuração da solução  
  
1.  Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução de CustomActionProjectItem.  
  
2.  Abra o arquivo de código CustomAction e, em seguida, adicione um ponto de interrupção para a primeira linha de código no `InitializeType` método.  
  
3.  Escolha o **F5** tecla para iniciar a depuração.  
  
     Visual Studio instala a extensão para %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\Custom Item\1.0 de projeto de ação e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.  
  
#### <a name="to-test-the-project-item-in-visual-studio"></a>Para testar o item de projeto no Visual Studio  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo** > **New** > **projeto**.  
  
2.  Expandir **Visual c#** ou **Visual Basic** (dependendo da linguagem que dá suporte a seu modelo de item), expanda **SharePoint**e, em seguida, escolha o **2010**  nó.  
  
3.  Na lista de modelos de projeto, escolha **projeto do SharePoint 2010**.  
  
4.  No **nome** , digite **CustomActionTest**e, em seguida, escolha o **Okey** botão.  
  
5.  No **Assistente para personalização do SharePoint**, insira a URL do site que você deseja usar para depuração e, em seguida, escolha o **concluir** botão.  
  
6.  Na **Gerenciador de soluções**, abra o menu de atalho do nó do projeto, escolha **Add**e, em seguida, escolha **Novo Item**.  
  
7.  No **Adicionar Novo Item** diálogo caixa, escolha o **2010** nó sob o **SharePoint** nó.  
  
     Verifique se que o **ação personalizada** item aparece na lista de itens de projeto.  
  
8.  Escolha o **ação personalizada** item e, em seguida, escolha o **Add** botão.  
  
     O Visual Studio adiciona um item que é denominado **CustomAction1** ao seu projeto e abrirá o *Elements. XML* arquivo no editor.  
  
9. Verifique se o código em outra instância do Visual Studio para no ponto de interrupção que você definiu anteriormente no `InitializeType` método.  
  
10. Escolha o **F5** tecla para continuar a depuração do projeto.  
  
11. Na instância experimental do Visual Studio, no **Gerenciador de soluções**, abra o menu de atalho para o **CustomAction1** nó e, em seguida, escolha **Designer de exibição da ação personalizada**.  
  
12. Verifique se uma caixa de mensagem é exibida e, em seguida, escolha o **Okey** botão.  
  
     Você pode usar esse menu de atalho para fornecer comandos ou opções adicionais para desenvolvedores, como a exibição de um designer para a ação personalizada.  
  
13. Na barra de menus, escolha **modo de exibição** > **saída**.  
  
     O **saída** janela é aberta.  
  
14. Na **Gerenciador de soluções**, abra o menu de atalho para o **CustomAction1** item e, em seguida, altere seu nome para **MyCustomAction**.  
  
     No **saída** janela, uma mensagem de confirmação é exibida. Essa mensagem é gravada o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemEvents.ProjectItemNameChanged> manipulador de eventos que você definiu no `CustomActionProjectItemTypeProvider` classe. Você pode manipular esse evento e outros eventos de item de projeto para implementar o comportamento personalizado quando o desenvolvedor modifica o item de projeto.  
  
#### <a name="to-test-the-custom-action-in-sharepoint"></a>Para testar a ação personalizada no SharePoint  
  
1.  Na instância experimental do Visual Studio, abra o *Elements. XML* arquivo que é um filho do **MyCustomAction** item de projeto.  
  
2.  No *Elements. XML* de arquivo, faça as seguintes alterações e, em seguida, salve o arquivo:  
  
    -   No `CustomAction` elemento, defina o `Id` atributo para um GUID ou outra cadeia de caracteres alguns exclusiva, como mostra o exemplo a seguir:  
  
        ```xml  
        Id="cd85f6a7-af2e-44ab-885a-0c795b52121a"  
        ```  
  
    -   No `CustomAction` elemento, defina o `Title` atributo, como mostra o exemplo a seguir:  
  
        ```xml  
        Title="SharePoint Developer Center"  
        ```  
  
    -   No `CustomAction` elemento, defina o `Description` atributo, como mostra o exemplo a seguir:  
  
        ```xml  
        Description="Opens the SharePoint Developer Center Web site."  
        ```  
  
    -   No `UrlAction` elemento, defina o `Url` atributo, como mostra o exemplo a seguir:  
  
        ```xml  
        Url="https://docs.microsoft.com/sharepoint/dev/"  
        ```  
  
3.  Pressione a tecla **F5**.  
  
     A ação personalizada é empacotada e implantada para o site do SharePoint que é especificado na **URL do Site** propriedade do projeto. O navegador da web abre a página padrão deste site.  
  
    > [!NOTE]  
    >  Se o **Script Debugging Disabled** caixa de diálogo for exibida, escolha o **Sim** botão para continuar a depuração do projeto.  
  
4.  Sobre o **ações do Site** menu, escolha **Central de desenvolvedores do SharePoint**, verifique se o navegador abre o site https://docs.microsoft.com/sharepoint/dev/e, em seguida, feche o navegador da web.  
  
## <a name="clean-up-the-development-computer"></a>Limpar o computador de desenvolvimento
 Após concluir o teste o item de projeto, remova o modelo de item de projeto da instância experimental do Visual Studio.  
  
#### <a name="to-clean-up-the-development-computer"></a>Para limpar o computador de desenvolvimento  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas** > **extensões e atualizações**.  
  
     A caixa de diálogo **Extensões e Atualizações** é aberta.  
  
2.  Na lista de extensões, escolha **Item de projeto de ação personalizado**e, em seguida, escolha o **desinstalar** botão.  
  
3.  Na caixa de diálogo que aparece, escolha o **Sim** botão para confirmar que você deseja desinstalar a extensão.  
  
4.  Escolha o **reiniciar agora** botão para concluir a desinstalação.  
  
5.  Feche a instância experimental do Visual Studio e a instância na qual a solução de CustomActionProjectItem está aberta.  
  
## <a name="next-steps"></a>Próximas etapas
 Depois de concluir este passo a passo, você pode adicionar um Assistente para o modelo de item. Quando um usuário adiciona um item de projeto de ação personalizada para um projeto do SharePoint, o assistente coleta informações sobre a ação (como sua localização e a URL para navegar quando a ação é escolhida) e adiciona essas informações para o *Elements. XML*arquivos no novo item de projeto. Para obter mais informações, consulte [instruções passo a passo: criar um item de projeto de ação personalizado com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md).  
  
## <a name="see-also"></a>Consulte também
 [Passo a passo: Criar um item de projeto de ação personalizado com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)   
 [Definir tipos personalizados de item de projeto do SharePoint](../sharepoint/defining-custom-sharepoint-project-item-types.md)   
 [Criar modelos de projeto do SharePoint para itens de projeto e modelos de item](../sharepoint/creating-item-templates-and-project-templates-for-sharepoint-project-items.md)   
 [Usar o serviço de projeto do SharePoint](../sharepoint/using-the-sharepoint-project-service.md)   
 [Referência de esquema de modelo do Visual Studio](/visualstudio/extensibility/visual-studio-template-schema-reference)   
 [Editor de imagens para ícones](/cpp/windows/image-editor-for-icons)   
 [Criando um ícone ou outra imagem &#40;Editor de imagens para ícones&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)  
  
