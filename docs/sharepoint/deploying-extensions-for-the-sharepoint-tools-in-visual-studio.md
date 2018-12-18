---
title: Implantando extensões para as ferramentas do SharePoint no Visual Studio | Microsoft Docs
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, deploying extensions
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c3bf20f945c40dd963820b1bf3f4032a2dd517ca
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295963"
---
# <a name="deploy-extensions-for-the-sharepoint-tools-in-visual-studio"></a>Implantar extensões para ferramentas do SharePoint no Visual Studio

Para implantar uma extensão de ferramentas do SharePoint, crie um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de extensão (VSIX) que contém o assembly de extensão e outros arquivos que você deseja distribuir com a extensão. Um pacote VSIX é um arquivo compactado que segue o padrão Open Packaging Conventions (OPC). Pacotes VSIX tem o *VSIX* extensão.

Depois de criar um pacote VSIX, outros usuários podem executar o arquivo. VSIX para instalar sua extensão. Quando um usuário instala a extensão, todos os arquivos são instalados na pasta %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions. Para implantar a extensão, você pode carregar o pacote VSIX para o [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=123847) site da Web, ou você pode distribuir o pacote para seus clientes por outros meios, como o pacote em um compartilhamento de rede ou algum outro site de hospedagem.

Para obter mais informações sobre como criar pacotes VSIX e implantá-los para o [Galeria do Visual Studio](http://go.microsoft.com/fwlink/?LinkID=123847), consulte [envio extensões do Visual Studio](../extensibility/shipping-visual-studio-extensions.md).

 Você pode criar um pacote VSIX usando o **VSIX Project** modelo no Visual Studio, ou você pode criar manualmente um pacote VSIX.

## <a name="use-vsix-projects-to-create-vsix-packages"></a>Usar os projetos VSIX para criar pacotes VSIX

Você pode usar o **VSIX Project** modelo fornecido pelo SDK do Visual Studio para criar pacotes VSIX para extensões de ferramentas do SharePoint. Usando um projeto VSIX oferece várias vantagens sobre a criação de um pacote VSIX manualmente:

-   Visual Studio gera automaticamente o pacote VSIX, quando você compila o projeto. Tarefas como adicionar os arquivos de implantação para o pacote e criar o arquivo [Content_Types]. XML do pacote são feitas por você.

-   Você pode configurar o projeto VSIX para incluir a saída de compilação do seu projeto de extensão e outros arquivos, como modelos de projeto e modelos de item, no pacote VSIX.

Para obter mais informações sobre como usar um projeto VSIX, consulte [modelo de projeto do VSIX](../extensibility/vsix-project-template.md).

### <a name="organize-your-projects"></a>Organizar seus projetos

Por padrão, os projetos de VSIX apenas geram pacotes VSIX, não assemblies. Portanto, você normalmente não implementar uma extensão de ferramentas do SharePoint em um projeto VSIX. Em geral, você trabalha com pelo menos dois projetos:

-   Um projeto VSIX.

-   Um projeto de biblioteca de classe que implementa a sua extensão.

Também é possível trabalhar com projetos adicionais para determinados tipos de extensões:

-   Um projeto de biblioteca de classe que implementa os comandos de SharePoint que são usados por sua extensão. Para um passo a passo que demonstre este cenário, consulte [instruções passo a passo: estenda o Gerenciador de servidores para exibir web parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md).

-   Um projeto de modelo de Item ou o modelo de projeto que cria um modelo de item ou um modelo de projeto, se sua extensão define um novo tipo de item de projeto do SharePoint. Para um passo a passo que demonstre este cenário, consulte [instruções passo a passo: criar um item de projeto de ação personalizado com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md).

-   Um projeto de biblioteca de classe que implementa um assistente personalizado para um modelo de item ou o modelo de projeto, se sua extensão incluir um modelo. Para um passo a passo que demonstre este cenário, consulte [instruções passo a passo: criar um item de projeto de ação personalizado com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md).

Se você incluir todos os projetos na mesma solução do Visual Studio, você pode modificar o arquivo vsixmanifest no projeto VSIX para incluir a saída de build dos projetos de biblioteca de classe.

### <a name="edit-the-vsix-manifest"></a>Editar o manifesto do VSIX

Você deve editar o arquivo vsixmanifest no projeto VSIX para incluir entradas para todos os itens que você deseja incluir em sua extensão. Quando você abre o arquivo vsixmanifest no seu menu de atalho, o arquivo aparece em um designer que fornece uma interface do usuário para editar o XML no arquivo. Para obter mais informações, consulte [Designer de manifesto do VSIX](../extensibility/vsix-manifest-designer.md).

Você deve adicionar entradas no arquivo vsixmanifest para os seguintes itens:

-   O assembly de extensão.

-   O assembly que implementa os comandos de SharePoint que são usados por sua extensão.

-   Quaisquer modelos de projeto ou modelos de item que estão associados com sua extensão.

-   Um assistente personalizado para um modelo que está associado a sua extensão.

Os procedimentos a seguir descrevem como adicionar entradas no arquivo .vsixmanifest para cada um desses itens.

#### <a name="to-include-the-extension-assembly"></a>Para incluir o assembly de extensão

1.  No projeto VSIX, abra o menu de atalho para o arquivo vsixmanifest e, em seguida, escolha **abrir**.

     O arquivo é aberto no designer

2.  Sobre o **ativos** guia do editor, escolha a **New** botão.

     O **adicionar novo ativo** caixa de diálogo é aberta.

3.  No **tipo** , escolha **mefcomponent**.

4.  No **origem** lista, execute uma das seguintes etapas:

    -   Se o assembly de extensão é criado a partir de um projeto que está na mesma solução que o projeto do VSIX, escolha **um projeto na solução atual**. No **projeto** , escolha o nome do projeto.

    -   Se o assembly de extensão é incluído como um arquivo em seu projeto, escolha **arquivo no sistema de arquivos**. No **caminho** lista, digite o caminho completo para o arquivo do assembly de extensão ou usar o **procurar** botão para localizar e escolher o arquivo do assembly.

5.  Escolha o botão **OK**.

#### <a name="to-include-a-sharepoint-command-assembly"></a>Para incluir um assembly de comando do SharePoint

1.  No projeto VSIX, abra o menu de atalho para o arquivo vsixmanifest e, em seguida, escolha o **abrir** botão.

     O arquivo é aberto no designer.

2.  No **ativos** seção do editor, escolha a **New** botão.

     O **adicionar novo ativo** caixa de diálogo é aberta.

3.  No **tipo** , digite **SharePoint.Commands.v4**.

4.  No **origem** lista, execute uma das seguintes etapas:

    -   Se o assembly do comando é criado a partir de um projeto que está na mesma solução que o projeto do VSIX, escolha **um projeto na solução atual**. No **projeto** , escolha o nome do projeto.

    -   Se o assembly de comando está incluído como um arquivo em seu projeto, escolha **arquivo no sistema de arquivos**. No **caminho** lista, digite o caminho completo para o arquivo do assembly de extensão ou usar o **procurar** botão para localizar e escolher o arquivo do assembly.

5.  Escolha o botão **OK**.

#### <a name="to-include-a-template-that-you-create"></a>Para incluir um modelo que você criar

1.  No projeto VSIX, abra o menu de atalho para o arquivo vsixmanifest e, em seguida, escolha o **abrir** botão.

     O arquivo é aberto no designer.

2.  No **ativos** seção do editor, escolha a **New** botão.

     O **adicionar novo ativo** caixa de diálogo é aberta.

3.  No **tipo** , escolha **Microsoft.VisualStudio.ProjectTemplate** ou **Microsoft.VisualStudio.ItemTemplate**.

4.  No **fonte** , escolha **um projeto na solução atual**.

5.  No **Project** lista, escolha o nome do projeto e, em seguida, escolha o **Okey** botão.

6.  Na **Gerenciador de soluções**, abra o menu de atalho para o seu projeto de modelo de projeto ou Item de modelo e, em seguida, escolha **descarregar projeto**.

7.  Abra o menu de atalho do nó do projeto novamente e, em seguida, escolha **edite**_YourTemplateProjectName_**csproj** ou **editar**  _YourTemplateProjectName_**. vbproj**.

8.  Localize o seguinte `VSTemplate` elemento no arquivo de projeto.

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
    ```

9. Substitua esse elemento pelo XML a seguir.

    ```xml
    <VSTemplate Include="YourTemplateName.vstemplate">
      <OutputSubPath>SharePoint\SharePoint14</OutputSubPath>
    </VSTemplate>
    ```

     O `OutputSubPath` elemento Especifica as pastas adicionais no caminho em que o modelo de projeto é criado quando você compila o projeto. As pastas especificadas aqui Certifique-se de que o modelo de item estará disponível somente quando os clientes abrir o **adicionar novo projeto** diálogo caixa, expanda o **SharePoint** nó e, em seguida, escolha o **2010**  nó.

10. Salve e feche o arquivo.

11. Na **Gerenciador de soluções**, abra o menu de atalho para o projeto de modelo de projeto ou Item de modelo e, em seguida, escolha **recarregar projeto**.

#### <a name="to-include-a-template-that-you-create-manually"></a>Para incluir um modelo que você cria manualmente

1.  No projeto VSIX, adicione uma nova pasta para o projeto para conter o modelo.

2.  Nessa nova pasta, crie as seguintes subpastas e, em seguida, adicione o arquivo de modelo (. zip) para o *identificação de localidade* pasta.

     *YourTemplateFolder*

     **SharePoint**

     **SharePoint14**

     *Identificação de localidade*

     *YourTemplateName*. zip

     Por exemplo, se você tiver um modelo de item chamado ContosoCustomAction.zip que dá suporte à localidade inglês (Estados Unidos), pode ser o caminho completo *ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip*.

3.  Na **Gerenciador de soluções**, escolha o arquivo de modelo (*YourTemplateName*. zip).

4.  No **propriedades** janela, defina as **Build Action** propriedade a ser **conteúdo**.

5.  Abra o menu de atalho para o arquivo vsixmanifest e, em seguida, escolha **aberto**.

     O arquivo é aberto no designer.

6.  No **ativos** seção do editor, escolha a **New** botão.

     O **adicionar novo ativo** caixa de diálogo é aberta.

7.  No **tipo** , escolha **Microsoft.VisualStudio.ItemTemplate** ou **Microsoft.VisualStudio.ProjectTemplate**.

8.  No **fonte** , escolha **arquivo no sistema de arquivos**.

9. No **caminho** , insira o caminho completo para o assembly (por exemplo, *ItemTemplates\SharePoint\SharePoint14\1033\ContosoCustomAction.zip*, ou usar o **procurar**botão para localizar e escolher o assembly e, em seguida, escolha o **Okey** botão.

#### <a name="to-include-a-wizard-for-a-project-template-or-item-template"></a>Para incluir um Assistente para um modelo de projeto ou o modelo de item

1.  No projeto VSIX, abra o menu de atalho para o arquivo vsixmanifest e, em seguida, escolha **abrir**.

     O arquivo é aberto no designer.

2.  No **ativos** seção do editor, escolha a **New** botão.

     O **adicionar novo ativo** caixa de diálogo é aberta.

3.  No **tipo** , escolha **Microsoft.VisualStudio.Assembly**.

4.  No **origem** lista, execute uma das seguintes etapas:

    -   Se o assembly de assistente é criado a partir de um projeto que está na mesma solução que o projeto do VSIX, escolha **um projeto na solução atual**. No **projeto** , escolha o nome do projeto.

    -   Se o assembly de assistente é incluído como um arquivo em seu projeto, escolha **arquivo no sistema de arquivos**. No **caminho** campo, insira o caminho completo para o arquivo de assembly ou usar o **procurar** botão para localizar e escolher o assembly.

5.  Escolha o botão **OK**.

### <a name="related-walkthroughs"></a>Passo a passo relacionados

A tabela a seguir lista as instruções passo a passo que demonstram como usar um projeto de VSIX para implantar diferentes tipos de extensões de ferramentas do SharePoint.

|Tipo de extensão|Passo a passo relacionados|
|--------------------|--------------------------|
|Uma extensão que inclui apenas o assembly de extensão|[Passo a passo: Estender um tipo de item de projeto do SharePoint](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)<br /><br /> [Passo a passo: Criar uma extensão de projeto do SharePoint](../sharepoint/walkthrough-creating-a-sharepoint-project-extension.md)<br /><br /> [Passo a passo: Chamar o modelo de objeto de cliente do SharePoint em uma extensão do Gerenciador de servidores](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)|
|Uma extensão que inclui comandos do SharePoint|[Passo a passo: Criar uma etapa de implantação para projetos do SharePoint](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)<br /><br /> [Passo a passo: Estenda o Gerenciador de servidores para exibir web parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)<br /><br /> [Passo a passo: Criar um item de projeto da coluna de site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|
|Uma extensão que inclui um modelo do Visual Studio|[Passo a passo: Criar um item de projeto de ação personalizado com um modelo de item, parte 1](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)<br /><br /> [Passo a passo: Criar um item de projeto da coluna de Site com um modelo de projeto, parte 1](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-1.md)|
|Uma extensão que inclui um Assistente de modelo|[Passo a passo: Criar um item de projeto de ação personalizado com um modelo de item, parte 2](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-2.md)<br /><br /> [Passo a passo: Criar um item de projeto da coluna de Site com um modelo de projeto, parte 2](../sharepoint/walkthrough-creating-a-site-column-project-item-with-a-project-template-part-2.md)|

## <a name="create-vsix-packages-manually"></a>Criar pacotes VSIX manualmente

Se você quiser criar manualmente o pacote VSIX para a sua extensão de ferramentas do SharePoint, execute as seguintes etapas:

1.  Crie o arquivo Extension vsixmanifest e o arquivo [Content_Types]. XML em uma nova pasta. Para obter mais informações, consulte [Anatomia de um pacote VSIX](../extensibility/anatomy-of-a-vsix-package.md).

2.  No Windows Explorer, clique com botão direito na pasta que contém os dois arquivos XML, clique em Enviar para e, em seguida, clique em pasta compactada (zipada). Renomeie o arquivo. zip resultante para Filename.vsix, onde Filename é o nome do arquivo redistribuível que instala o pacote.

3.  Adicione seu assembly de extensão para o pacote VSIX. Se sua extensão incluir um comando do SharePoint, também adicione o assembly que implementa o comando do SharePoint para o pacote VSIX.

4.  Modifique o arquivo Extension vsixmanifest:

    -   Adicionar um `Microsoft.VisualStudio.MefComponent` elemento sob o `Assets` elemento e, em seguida, defina o valor do novo elemento para o caminho relativo do assembly que implementa a sua extensão no pacote VSIX. Para obter mais informações, consulte [MEFComponent Element (esquema de VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).

    -   Se sua extensão incluir um comando do SharePoint que chama o modelo de objeto de servidor para o SharePoint, adicione uma `Microsoft.VisualStudio.Assembly` elemento sob o `Assets` elemento. Defina o valor do novo elemento para o caminho relativo do assembly que implementa o comando do SharePoint no pacote VSIX. Para obter mais informações, consulte [ativo Element (esquema de VSX)](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737).

    -   Se sua extensão incluir um modelo de projeto ou o modelo de item, adicione uma `ProjectTemplate` ou `ItemTemplate` elemento sob o `Assets` elemento. Defina o valor do novo elemento para o caminho relativo da pasta que contém o modelo no pacote VSIX. Para obter mais informações, consulte [ProjectTemplate Element (esquema de VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393735\(v\=vs.100\)) e [ItemTemplate Element (esquema de VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393681\(v\=vs.100\)).

    -   Se sua extensão inclui um assistente personalizado para um modelo de projeto ou o modelo de item, adicione uma `Assembly` elemento sob o `Assets` elemento. Defina o valor do novo elemento para o caminho relativo do assembly no pacote VSIX e, em seguida, defina o `AssemblyName` de atributo para o nome completo do assembly (incluindo a versão, cultura e token de chave pública). Para obter mais informações, consulte [dependência Element (esquema de VSX)](https://msdn.microsoft.com/1f63f60a-98ad-48ec-8e44-4eba383d3e37).

### <a name="example"></a>Exemplo

O exemplo a seguir mostra o conteúdo de um arquivo Extension vsixmanifest para uma extensão de ferramentas do SharePoint. A extensão é implementada em um assembly denominado Contoso.ProjectExtension.dll. A extensão inclui um assembly de comando do SharePoint que é chamado Contoso.ExtensionCommands.dll e um modelo de item em uma pasta chamada **ItemTemplates** no pacote VSIX. Este exemplo pressupõe que os assemblies na mesma pasta que o arquivo Extension vsixmanifest no pacote VSIX.

```xml
<PackageManifest Version="2.0.0" xmlns="http://schemas.microsoft.com/developer/vsx-schema/2011">
  <Metadata>
    <Identity Id="CustomActionProjectItem.Microsoft.b99efe4d-cef3-4afd-b9af-034ca0c52743" Version="1.0" Language="en-US" Publisher="Microsoft" />
    <DisplayName>CustomActionProjectItem</DisplayName>
    <Description>Empty VSIX Project.</Description>
  </Metadata>
  <Installation>
    <InstallationTarget Id="Microsoft.VisualStudio.Pro" Version="11.0" />
  </Installation>
  <Dependencies>
    <Dependency Id="Microsoft.Framework.NDP" DisplayName="Microsoft .NET Framework" Version="4.5" />
  </Dependencies>
  <Assets>
    <Asset Type="Microsoft.VisualStudio.ItemTemplate" Path="ItemTemplates" />
    <Asset Type="Microsoft.VisualStudio.MefComponent" Path="ProjectItemDefinition.dll" />
  </Assets>
</PackageManifest>
```

## <a name="see-also"></a>Consulte também

- [Estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md)
- [Estender o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [Chamar os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [Depurar extensões para ferramentas do SharePoint no Visual Studio](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)
