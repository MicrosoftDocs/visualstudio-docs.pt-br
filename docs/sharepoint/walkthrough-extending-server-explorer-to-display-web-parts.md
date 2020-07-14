---
title: 'Walkthrough: estendendo Gerenciador de Servidores para exibir Web Parts | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint commands
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5e5221d1cce065a352051ca700cf0fc5ef4ae843
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015639"
---
# <a name="walkthrough-extend-server-explorer-to-display-web-parts"></a>Walkthrough: estender Gerenciador de Servidores para exibir Web Parts
  No Visual Studio, você pode usar o nó **conexões do SharePoint** de **Gerenciador de servidores** para exibir componentes em sites do SharePoint. No entanto, o **Gerenciador de servidores** não exibe alguns componentes por padrão. Neste tutorial, você estenderá **Gerenciador de servidores** para que ele exiba a Galeria de Web Parts em cada site do SharePoint conectado.

 Este tutorial demonstra as seguintes tarefas:

- Criar uma extensão do Visual Studio que estenda **Gerenciador de servidores** das seguintes maneiras:

  - A extensão adiciona um nó **da Galeria de Web Parts** em cada nó do site do SharePoint no **Gerenciador de servidores**. Esse novo nó contém nós filho que representam cada Web Part na Galeria de Web Parts no site.

  - A extensão define um novo tipo de nó que representa uma instância de Web Part. Esse novo tipo de nó é a base para os nós filho no novo nó **da Galeria de Web Parts** . O novo tipo de nó da Web Part exibe informações na janela **Propriedades** sobre a Web Part que ela representa. O tipo de nó também inclui um item de menu de atalho personalizado que você pode usar como um ponto de partida para executar outras tarefas relacionadas à Web Part.

- Crie dois comandos personalizados do SharePoint que o assembly de extensão chama. Os comandos do SharePoint são métodos que podem ser chamados por assemblies de extensão para usar APIs no modelo de objeto de servidor para SharePoint. Neste tutorial, você cria comandos que recuperam informações de Web Part do site do SharePoint local no computador de desenvolvimento. Para obter mais informações, consulte [chamar os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).

- Criando um pacote de VSIX (Visual Studio Extension) para implantar a extensão.

- Depurando e testando a extensão.

> [!NOTE]
> Para obter uma versão alternativa deste passo a passos que usa o modelo de objeto de cliente para SharePoint em vez de seu modelo de objeto de servidor, consulte [passo a passos: chamar no modelo de objeto de cliente do SharePoint em uma extensão de Gerenciador de servidores](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passos:

- Edições com suporte do Windows, SharePoint e Visual Studio.

- O SDK do Visual Studio. Este tutorial usa o modelo de **projeto VSIX** no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).

  O conhecimento dos seguintes conceitos é útil, mas não é necessário, para concluir o passo a passos:

- Usando o modelo de objeto de servidor para SharePoint. Para obter mais informações, consulte [usando o modelo de objeto do SharePoint Foundation Server](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14)).

- Web Parts em soluções do SharePoint. Para obter mais informações, consulte [Web Parts visão geral](/previous-versions/office/ms432401(v=office.14)).

## <a name="create-the-projects"></a>Criar os projetos
 Para concluir este passo a passos, você deve criar três projetos:

- Um projeto VSIX para criar o pacote VSIX para implantar a extensão.

- Um projeto de biblioteca de classes que implementa a extensão. Este projeto deve ter como destino o .NET Framework 4,5.

- Um projeto de biblioteca de classes que define os comandos personalizados do SharePoint. Este projeto deve ter como destino a estrutura the.NET 3,5.

  Inicie o passo a passos criando os projetos.

#### <a name="to-create-the-vsix-project"></a>Para criar o projeto VSIX

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

3. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha o nó **extensibilidade** .

    > [!NOTE]
    > O nó **extensibilidade** só estará disponível se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos anteriormente neste tópico.

4. Na parte superior da caixa de diálogo, escolha **.NET Framework 4,5** na lista de versões do .NET Framework.

5. Escolha o modelo de **projeto VSIX** , nomeie o projeto **WebPartNode**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **WebPartNode** ao **Gerenciador de soluções**.

#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na caixa de diálogo **novo projeto** , expanda o nó do **Visual C#** ou **Visual Basic** nó e, em seguida, o nó escolher **Windows** .

3. Na parte superior da caixa de diálogo, escolha **.NET Framework 4,5** na lista de versões do .NET Framework.

4. Na lista de modelos de projeto, escolha **biblioteca de classes**, nomeie o projeto **WebPartNodeExtension**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **WebPartNodeExtension** à solução e abre o arquivo de código de Class1 padrão.

5. Exclua o arquivo de código Class1 do projeto.

#### <a name="to-create-the-sharepoint-commands-project"></a>Para criar o projeto de comandos do SharePoint

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na caixa de diálogo **novo projeto** , expanda o nó do **Visual C#** ou **Visual Basic** nó e, em seguida, escolha o nó do **Windows** .

3. Na parte superior da caixa de diálogo, escolha **.NET Framework 3,5** na lista de versões do .NET Framework.

4. Na lista de modelos de projeto, escolha **biblioteca de classes**, nomeie o projeto **WebPartCommands**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **WebPartCommands** à solução e abre o arquivo de código de Class1 padrão.

5. Exclua o arquivo de código Class1 do projeto.

## <a name="configure-the-projects"></a>Configurar os projetos
 Antes de escrever o código para criar a extensão, você deve adicionar arquivos de código e referências de assembly e definir as configurações do projeto.

#### <a name="to-configure-the-webpartnodeextension-project"></a>Para configurar o projeto WebPartNodeExtension

1. No projeto WebPartNodeExtension, adicione quatro arquivos de código que têm os seguintes nomes:

    - SiteNodeExtension

    - WebPartNodeTypeProvider

    - WebPartNodeInfo

    - WebPartCommandIds

2. Abra o menu de atalho para o projeto **WebPartNodeExtension** e escolha **Adicionar referência**.

3. Na caixa de diálogo **Gerenciador de referências-WebPartNodeExtension** , escolha a guia **estrutura** e marque a caixa de seleção para cada um dos seguintes assemblies:

    - System. ComponentModel. composição

    - System.Windows.Forms

4. Escolha a guia **extensões** , marque a caixa de seleção do assembly Microsoft. VisualStudio. SharePoint e, em seguida, escolha o botão **OK** .

5. No **Gerenciador de soluções**, abra o menu de atalho para o nó do projeto **WebPartNodeExtension** e escolha **Propriedades**.

     O **Designer de Projeto** é aberto.

6. Escolha a guia **Aplicativo**.

7. Na caixa **namespace padrão** (C#) ou no **namespace raiz** ( [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] ), digite **ServerExplorer. SharePointConnections. WebPartNode**.

#### <a name="to-configure-the-webpartcommands-project"></a>Para configurar o projeto WebPartCommands

1. No projeto WebPartCommands, adicione um arquivo de código chamado WebPartCommands.

2. No **Gerenciador de soluções**, abra o menu de atalho para o nó do projeto **WebPartCommands** , escolha **Adicionar**e, em seguida, escolha **Item existente**.

3. Na caixa de diálogo **Adicionar item existente** , navegue até a pasta que contém os arquivos de código do projeto WebPartNodeExtension e escolha os arquivos de código WebPartNodeInfo e WebPartCommandIds.

4. Escolha a seta ao lado do botão **Adicionar** e, em seguida, escolha **Adicionar como link** no menu exibido.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona os arquivos de código ao projeto WebPartCommands como links. Como resultado, os arquivos de código estão localizados no projeto WebPartNodeExtension, mas o código nos arquivos também é compilado no projeto WebPartCommands.

5. Abra o menu de atalho para o projeto **WebPartCommands** novamente e escolha **Adicionar referência**.

6. Na caixa de diálogo **Gerenciador de referências-WebPartCommands** , escolha a guia **extensões** , marque a caixa de seleção de cada um dos seguintes assemblies e, em seguida, escolha o botão **OK** :

    - Microsoft. SharePoint

    - Microsoft. VisualStudio. SharePoint. Commands

7. Em **Gerenciador de soluções**, abra o menu de atalho para o projeto **WebPartCommands** novamente e escolha **Propriedades**.

     O **Designer de Projeto** é aberto.

8. Escolha a guia **Aplicativo**.

9. Na caixa **namespace padrão** (C#) ou no **namespace raiz** ( [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] ), digite **ServerExplorer. SharePointConnections. WebPartNode**.

## <a name="create-icons-for-the-new-nodes"></a>Criar ícones para os novos nós
 Crie dois ícones para a extensão de **Gerenciador de servidores** : um ícone para o novo nó **da Galeria de Web Parts** e outro ícone para cada nó da Web Part filho sob o nó da **Galeria de Web Parts** . Mais adiante neste tutorial, você escreverá um código que associa esses ícones aos nós.

#### <a name="to-create-icons-for-the-nodes"></a>Para criar ícones para os nós

1. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **WebPartNodeExtension** e escolha **Propriedades**.

2. O **Designer de Projeto** é aberto.

3. Escolha a guia **recursos** e, em seguida, escolha **este projeto não contém um arquivo de recursos padrão. Clique aqui para criar um** link.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Cria um arquivo de recurso e o abre no designer.

4. Na parte superior do designer, escolha a seta ao lado do comando de menu **Adicionar recurso** e escolha **Adicionar novo ícone** no menu que aparece.

5. Na caixa de diálogo **Adicionar novo recurso** , nomeie o ícone novo **WebPartsNode**e, em seguida, escolha o botão **Adicionar** .

     O novo ícone é aberto no **Editor de imagem**.

6. Edite a versão de 16x16 do ícone para que ele tenha um design que você possa reconhecer facilmente.

7. Abra o menu de atalho da versão 32x32 do ícone e escolha **excluir tipo de imagem**.

8. Repita as etapas de 5 a 8 para adicionar um segundo ícone aos recursos do projeto e nomeie esse ícone **WebPart**.

9. No **Gerenciador de soluções**, na pasta **recursos** do projeto **WebPartNodeExtension** , abra o menu de atalho para **WebPartsNode. ico**.

10. Na janela **Propriedades** , escolha a seta ao lado de **criar ação**e, em seguida, escolha **recurso incorporado** no menu que aparece.

11. Repita as duas últimas etapas para **WebPart. ico**.

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>Adicione o nó Galeria de Web Parts a Gerenciador de Servidores
 Crie uma classe que adiciona o novo nó **da Galeria de Web Parts** a cada nó do site do SharePoint. Para adicionar o novo nó, a classe implementa a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> interface. Implemente essa interface sempre que desejar estender o comportamento de um nó existente no **Gerenciador de servidores**, como adicionar um nó filho a um nó.

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>Para adicionar o nó Galeria de Web Parts a Gerenciador de Servidores

1. No projeto WebPartNodeExtension, abra o arquivo de código SiteNodeExtension e cole o código a seguir nele.

    > [!NOTE]
    > Depois de adicionar esse código, o projeto terá alguns erros de compilação, mas eles desaparecerão quando você adicionar código em etapas posteriores.

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#1](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/sitenodeextension.cs#1)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#1](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/sitenodeextension.vb#1)]

## <a name="define-a-node-type-that-represents-a-web-part"></a>Definir um tipo de nó que representa uma Web Part
 Crie uma classe que define um novo tipo de nó que representa uma Web Part. O Visual Studio usa esse novo tipo de nó para exibir os nós filho no nó **da Galeria de Web Parts** . Cada nó filho representa uma única Web Part no site do SharePoint.

 Para definir o novo tipo de nó, a classe implementa a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> interface. Implemente essa interface sempre que desejar definir um novo tipo de nó no **Gerenciador de servidores**.

#### <a name="to-define-the-web-part-node-type"></a>Para definir o tipo de nó de Web Part

1. No projeto WebPartNodeExtension, abra o arquivo de código WebPartNodeTypeProvder e cole o código a seguir nele.

     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#2](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb#2)]
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#2](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodetypeprovider.cs#2)]

## <a name="define-the-web-part-data-class"></a>Definir a classe de dados da Web Part
 Defina uma classe que contém dados sobre uma única Web Part no site do SharePoint. Mais adiante neste guia, você criará um comando personalizado do SharePoint que recupera dados sobre cada Web Part no site e, em seguida, atribui os dados a instâncias dessa classe.

#### <a name="to-define-the-web-part-data-class"></a>Para definir a classe de dados da Web Part

1. No projeto WebPartNodeExtension, abra o arquivo de código WebPartNodeInfo e cole o código a seguir nele.

     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#3](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodeinfo.vb#3)]
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#3](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodeinfo.cs#3)]

## <a name="define-the-ids-for-the-sharepoint-commands"></a>Definir as IDs para os comandos do SharePoint
 Defina várias cadeias de caracteres que identificam os comandos personalizados do SharePoint. Você implementará esses comandos posteriormente neste passo a passos.

#### <a name="to-define-the-command-ids"></a>Para definir as IDs de comando

1. No projeto WebPartNodeExtension, abra o arquivo de código WebPartCommandIds e cole o código a seguir nele.

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#4](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartcommandids.cs#4)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#4](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartcommandids.vb#4)]

## <a name="create-the-custom-sharepoint-commands"></a>Criar os comandos personalizados do SharePoint
 Crie comandos personalizados que chamam o modelo de objeto de servidor para SharePoint para recuperar dados sobre o Web Parts no site do SharePoint. Cada comando é um método que tem o <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> aplicado a ele.

#### <a name="to-define-the-sharepoint-commands"></a>Para definir os comandos do SharePoint

1. No projeto WebPartCommands, abra o arquivo de código WebPartCommands e cole o código a seguir nele.

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#6](../sharepoint/codesnippet/CSharp/WebPartNode/WebPartCommands/WebPartCommands.cs#6)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#6](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartcommands/webpartcommands.vb#6)]

## <a name="checkpoint"></a>Ponto de verificação
 Neste ponto do passo a passo, todo o código para o nó **da Galeria de Web Parts** e os comandos do SharePoint agora estão nos projetos. Compile a solução para garantir que os dois projetos sejam compilados sem erros.

#### <a name="to-build-the-solution"></a>Para compilar a solução

1. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

    > [!WARNING]
    > Neste ponto, o projeto WebPartNode pode ter um erro de compilação porque o arquivo de manifesto do VSIX não tem um valor para o autor. Esse erro desaparecerá quando você adicionar um valor em etapas posteriores.

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>Criar um pacote VSIX para implantar a extensão
 Para implantar a extensão, use o projeto VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo Source. Extension. vsixmanifest no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.

#### <a name="to-configure-the-vsix-package"></a>Para configurar o pacote VSIX

1. No **Gerenciador de soluções**, no projeto WebPartNode, abra o arquivo **Source. Extension. vsixmanifest** no editor de manifesto.

     O arquivo Source. Extension. vsixmanifest é a base para o arquivo extension. vsixmanifest que todos os pacotes VSIX exigem. Para obter mais informações sobre esse arquivo, consulte [referência do esquema de extensão do VSIX 1,0](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).

2. Na caixa **nome do produto** , insira o **nó Galeria de Web parts para Gerenciador de servidores**.

3. Na caixa **autor** , digite **contoso**.

4. Na caixa **Descrição** , digite **adiciona um nó de galeria de Web Parts personalizado ao nó conexões do SharePoint no Gerenciador de servidores. Essa extensão usa um comando personalizado do SharePoint para chamar o modelo de objeto do servidor.**

5. Escolha a guia **ativos** do editor e, em seguida, escolha o botão **novo** .

     A caixa de diálogo **Adicionar novo ativo** é exibida.

6. Na lista **tipo** , escolha **Microsoft. VisualStudio. MefComponent**.

    > [!NOTE]
    > Esse valor corresponde ao `MefComponent` elemento no arquivo extension. vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [elemento MEFComponent (esquema VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).

7. Na lista **origem** , escolha **um projeto na solução atual**.

8. Na lista **projeto** , escolha **WebPartNodeExtension** e, em seguida, escolha o botão **OK** .

9. No editor de manifesto, escolha o botão **novo** novamente.

     A caixa de diálogo **Adicionar novo ativo** é exibida.

10. Na caixa **tipo** , digite **SharePoint. Commands. v4**.

    > [!NOTE]
    > Esse elemento Especifica uma extensão personalizada que você deseja incluir na extensão do Visual Studio. Para obter mais informações, consulte [elemento Asset (esquema VSX)](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737).

11. Na lista **origem** , escolha o item **um projeto na lista de soluções atual** .

12. Na lista **projeto** , escolha **WebPartCommands**e, em seguida, escolha o botão **OK** .

13. Na barra de menus, escolha **criar**  >  **solução de compilação**e, em seguida, certifique-se de que a solução seja compilada sem erros.

14. Verifique se a pasta de saída da compilação do projeto WebPartNode agora contém o arquivo WebPartNode. vsix.

     Por padrão, a pasta de saída da compilação é a.. pasta \bin\Debug sob a pasta que contém o arquivo de projeto.

## <a name="test-the-extension"></a>Testar a extensão
 Agora você está pronto para testar o novo nó **Galeria de Web Parts** em **Gerenciador de servidores**. Primeiro, comece a depurar a extensão em uma instância experimental do Visual Studio. Em seguida, use o novo nó **Web Parts** na instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

#### <a name="to-start-debugging-the-extension"></a>Para iniciar a depuração da extensão

1. Reinicie [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] com credenciais administrativas e, em seguida, abra a solução WebPartNode.

2. No projeto WebPartNodeExtension, abra o arquivo de código SiteNodeExtension e, em seguida, adicione um ponto de interrupção à primeira linha de código nos `NodeChildrenRequested` `CreateWebPartNodes` métodos e.

3. Escolha a tecla **F5** para iniciar a depuração.

     O Visual Studio instala a extensão para a extensão de nó da galeria do%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web Part para o servidor Explorer\1.0 e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.

#### <a name="to-test-the-extension"></a>Para testar a extensão

1. Na instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , na barra de menus, escolha **Exibir**  >  **Gerenciador de servidores**.

2. Execute as etapas a seguir se o site do SharePoint que você deseja usar para teste não aparecer no nó **conexões do SharePoint** no **Gerenciador de servidores**:

    1. No **Gerenciador de servidores**, abra o menu de atalho para **conexões do SharePoint**e, em seguida, escolha **Adicionar conexão**.

    2. Na caixa de diálogo **Adicionar conexão do SharePoint** , digite a URL do site do SharePoint ao qual você deseja se conectar e escolha o botão **OK** .

         Para especificar o site do SharePoint no seu computador de desenvolvimento, digite **http://localhost** .

3. Expanda o nó conexão do site (que exibe a URL do seu site) e, em seguida, expanda um nó de site filho (por exemplo, **site de equipe**).

4. Verifique se o código na outra instância do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] é interrompido no ponto de interrupção que você definiu anteriormente no `NodeChildrenRequested` método e, em seguida, escolha **F5** para continuar a depurar o projeto.

5. Na instância experimental do Visual Studio, verifique se um novo nó chamado **Galeria de Web Parts** aparece sob o nó do site de nível superior e, em seguida, expanda o nó **Galeria de Web Parts** .

6. Verifique se o código na outra instância do Visual Studio é interrompido no ponto de interrupção que você definiu anteriormente no `CreateWebPartNodes` método e, em seguida, escolha a tecla **F5** para continuar a depurar o projeto.

7. Na instância experimental do Visual Studio, verifique se todos os Web Parts no site conectado aparecem no nó **Galeria de Web Parts** no **Gerenciador de servidores**.

8. No **Gerenciador de servidores**, abra o menu de atalho para um dos Web Parts e escolha **Propriedades**.

9. Na instância do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] que você está Depurando, verifique se os detalhes sobre a Web Part aparecem na janela **Propriedades** .

## <a name="uninstall-the-extension-from-visual-studio"></a>Desinstalar a extensão do Visual Studio
 Depois de concluir o teste da extensão, desinstale a extensão do Visual Studio.

#### <a name="to-uninstall-the-extension"></a>Para desinstalar a extensão

1. Na instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , na barra de menus, escolha **ferramentas**  >  **extensões e atualizações**.

     A caixa de diálogo **Extensões e Atualizações** é aberta.

2. Na lista de extensões, escolha **extensão de nó da Galeria de Web Parts para Gerenciador de servidores**e, em seguida, escolha o botão **desinstalar** .

3. Na caixa de diálogo exibida, escolha o botão **Sim** para confirmar que você deseja desinstalar a extensão e, em seguida, escolha o botão **reiniciar agora** para concluir a desinstalação.

4. Feche as duas instâncias do Visual Studio (a instância experimental e a instância do Visual Studio na qual a solução WebPartNode está aberta).

## <a name="see-also"></a>Consulte também
- [Estenda o nó conexões do SharePoint no Gerenciador de Servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [Walkthrough: chamar o modelo de objeto de cliente do SharePoint em uma extensão Gerenciador de Servidores](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)
- [Editor de imagem para ícones](/cpp/windows/image-editor-for-icons)
- [Criando um ícone ou outro editor de imagem de &#40;de imagem para ícones&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)
