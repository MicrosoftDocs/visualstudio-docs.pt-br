---
title: 'Passo a passo: Estendendo o Gerenciador de servidores para exibir Web Parts | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint Connections [SharePoint development in Visual Studio], extending a node
- SharePoint commands
- SharePoint development in Visual Studio, extending SharePoint Connections node in Server Explorer
- SharePoint Connections [SharePoint development in Visual Studio], creating a new node type
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 6d32f76965c0dbef359e54bda114221e460a9bfd
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296379"
---
# <a name="walkthrough-extend-server-explorer-to-display-web-parts"></a>Passo a passo: Estenda o Gerenciador de servidores para exibir web parts
  No Visual Studio, você pode usar o **conexões do SharePoint** nó do **Gerenciador de servidores** para componentes de exibição nos sites do SharePoint. No entanto, **Gerenciador de servidores** não exibe alguns componentes por padrão. Neste passo a passo, você estenderá **Gerenciador de servidores** para que ele exiba a Galeria de Web Parts em cada uma conectada site do SharePoint.  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
-   Criando uma extensão do Visual Studio que estende **Gerenciador de servidores** das seguintes maneiras:  
  
    -   Adiciona a extensão de um **Galeria de Web Parts** nó em cada nó do site do SharePoint no **Gerenciador de servidores**. Esse novo nó contém nós filho que representam cada Web Part na Galeria de Web Parts no site.  
  
    -   A extensão define um novo tipo de nó que representa uma instância de Web Part. Esse novo tipo de nó é a base para os nós filho sob a nova **Galeria de Web Parts** nó. O novo tipo de nó de Web Part exibe informações de **propriedades** janela sobre a Web Part que ele representa. O tipo de nó também inclui um item de menu de atalho personalizado que você pode usar como ponto de partida para executar outras tarefas relacionadas à Web Part.  
  
-   Crie dois comandos do SharePoint personalizados que chama o assembly de extensão. Comandos do SharePoint são métodos que podem ser chamados por assemblies de extensão para usar APIs no modelo de objeto de servidor para o SharePoint. Neste passo a passo, você deve criar comandos que recuperam informações de Web Part do site do SharePoint local no computador de desenvolvimento. Para obter mais informações, consulte [chamam os modelos de objeto SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).  
  
-   Criando um pacote de extensão VSIX (Visual Studio) para implantar a extensão.  
  
-   Depurando e testando a extensão.  
  
> [!NOTE]  
>  Para obter uma versão alternativa deste passo a passo que usa o modelo de objeto do cliente para o SharePoint, em vez de seu modelo de objeto de servidor, consulte [instruções passo a passo: chamar o modelo de objeto de cliente do SharePoint em uma extensão do Gerenciador de servidores](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passo:  
  
- Edições com suporte do Windows, SharePoint e do Visual Studio.  
  
- O SDK do Visual Studio. Este passo a passo usa o **VSIX Project** modelo no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).  
  
  Conhecimento dos conceitos a seguir é útil, mas não necessário para concluir o passo a passo:  
  
- Usando o modelo de objeto de servidor para o SharePoint. Para obter mais informações, consulte [usando o modelo de objeto de servidor do SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkId=177796).  
  
- Web Parts em soluções do SharePoint. Para obter mais informações, consulte [Web Parts Overview](http://go.microsoft.com/fwlink/?LinkId=177803).  
  
## <a name="create-the-projects"></a>Crie os projetos
 Para concluir este passo a passo, você deve criar três projetos:  
  
- Um projeto VSIX para criar o pacote VSIX para implantar a extensão.  
  
- Um projeto de biblioteca de classe que implementa a extensão. Este projeto deve ter como destino o .NET Framework 4.5.  
  
- Um projeto de biblioteca de classe que define os comandos do SharePoint personalizados. Este projeto deve ter como destino o.NET Framework 3.5.  
  
  Inicie o passo a passo Criando os projetos.  
  
#### <a name="to-create-the-vsix-project"></a>Para criar o projeto do VSIX  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
3.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha o **extensibilidade** nó.  
  
    > [!NOTE]  
    >  O **extensibilidade** o nó está disponível somente se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos no início deste tópico.  
  
4.  Na parte superior da caixa de diálogo, escolha **.NET Framework 4.5** na lista de versões do .NET Framework.  
  
5.  Escolha o **projeto VSIX** modelo, o nome do projeto **WebPartNode**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **WebPartNode** projeto ao **Gerenciador de soluções**.  
  
#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do nó da solução, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda o **Visual c#** nó ou **Visual Basic** nó e, em seguida, escolha **Windows** nó.  
  
3.  Na parte superior da caixa de diálogo, escolha **.NET Framework 4.5** na lista de versões do .NET Framework.  
  
4.  Na lista de modelos de projeto, escolha **biblioteca de classes**, nomeie o projeto **WebPartNodeExtension**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **WebPartNodeExtension** projeto à solução e abre o arquivo de código padrão Class1.  
  
5.  Exclua o arquivo de código Class1 do projeto.  
  
#### <a name="to-create-the-sharepoint-commands-project"></a>Para criar o projeto de comandos do SharePoint  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do nó da solução, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda o **Visual c#** nó ou **Visual Basic** nó e, em seguida, escolha o **Windows** nó.  
  
3.  Na parte superior da caixa de diálogo, escolha **.NET Framework 3.5** na lista de versões do .NET Framework.  
  
4.  Na lista de modelos de projeto, escolha **biblioteca de classes**, nomeie o projeto **WebPartCommands**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **WebPartCommands** projeto à solução e abre o arquivo de código padrão Class1.  
  
5.  Exclua o arquivo de código Class1 do projeto.  
  
## <a name="configure-the-projects"></a>Configurar os projetos
 Antes de escrever código para criar a extensão, você deve adicionar arquivos de código e referências de assembly e defina as configurações de projeto.  
  
#### <a name="to-configure-the-webpartnodeextension-project"></a>Para configurar o projeto WebPartNodeExtension
  
1.  No projeto WebPartNodeExtension, adicione quatro arquivos de código que têm os seguintes nomes:  
  
    -   SiteNodeExtension  
  
    -   WebPartNodeTypeProvider  
  
    -   WebPartNodeInfo  
  
    -   WebPartCommandIds  
  
2.  Abra o menu de atalho para o **WebPartNodeExtension** do projeto e, em seguida, escolha **adicionar referência**.  
  
3.  No **Gerenciador de referências - WebPartNodeExtension** diálogo caixa, escolha o **Framework** guia e, em seguida, selecione a caixa de seleção para cada um dos seguintes assemblies:  
  
    -   System.ComponentModel.Composition  
  
    -   System.Windows.Forms  
  
4.  Escolha o **extensões** guia, marque a caixa de seleção para o assembly Microsoft.VisualStudio.SharePoint e, em seguida, escolha o **Okey** botão.  
  
5.  Na **Gerenciador de soluções**, abra o menu de atalho para o **WebPartNodeExtension** nó do projeto e, em seguida, escolha **propriedades**.  
  
     O **Designer de Projeto** é aberto.  
  
6.  Escolha a guia **Aplicativo**.  
  
7.  No **namespace padrão** caixa (c#) ou **namespace raiz** caixa ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]), insira **ServerExplorer.SharePointConnections.WebPartNode**.  
  
#### <a name="to-configure-the-webpartcommands-project"></a>Para configurar o projeto webpartcommands
  
1.  No projeto WebPartCommands, adicione um arquivo de código chamado WebPartCommands.  
  
2.  Na **Gerenciador de soluções**, abra o menu de atalho para o **WebPartCommands** nó do projeto, escolha **Add**e, em seguida, escolha **Item existente**.  
  
3.  No **Add Existing Item** caixa de diálogo, navegue até a pasta que contém os arquivos de código para o projeto WebPartNodeExtension e, em seguida, escolha os arquivos de código WebPartNodeInfo e WebPartCommandIds.  
  
4.  Escolha a seta ao lado de **Add** botão e, em seguida, escolha **adicionar como vínculo** no menu que aparece.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona os arquivos de código ao projeto WebPartCommands como links. Como resultado, os arquivos de código estão localizados no projeto WebPartNodeExtension, mas o código nos arquivos também são compilados no projeto WebPartCommands.  
  
5.  Abra o menu de atalho para o **WebPartCommands** do projeto novamente e, em seguida, escolha **adicionar referência**.  
  
6.  No **Gerenciador de referências - WebPartCommands** diálogo caixa, escolha o **extensões** guia, marque a caixa de seleção para cada um dos assemblies a seguir e, em seguida, escolha o **Okey** botão:  
  
    -   Microsoft. SharePoint  
  
    -   Microsoft.VisualStudio.SharePoint.Commands  
  
7.  Na **Gerenciador de soluções**, abra o menu de atalho para o **WebPartCommands** projeto novamente e, em seguida, escolha **propriedades**.  
  
     O **Designer de Projeto** é aberto.  
  
8.  Escolha a guia **Aplicativo**.  
  
9. No **namespace padrão** caixa (c#) ou **namespace raiz** caixa ([!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]), insira **ServerExplorer.SharePointConnections.WebPartNode**.  
  
## <a name="create-icons-for-the-new-nodes"></a>Criar ícones para os novos nós
 Criar dois ícones para o **Gerenciador de servidores** extensão: um ícone para o novo **Galeria de Web Parts** nó e outro ícone para cada nó de Web Part filho sob o **Galeria de Web Parts** nó. Posteriormente neste passo a passo, você irá escrever código que associa esses ícones com os nós.  
  
#### <a name="to-create-icons-for-the-nodes"></a>Para criar os ícones para os nós  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **WebPartNodeExtension** do projeto e, em seguida, escolha **propriedades**.  
  
2.  O **Designer de Projeto** é aberto.  
  
3.  Escolha o **recursos** guia e, em seguida, escolha o **este projeto não contém um arquivo de recursos padrão. Clique aqui para criar um** link.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria um arquivo de recurso e o abre no designer.  
  
4.  Na parte superior do designer, escolha a seta ao lado de **adicionar recurso** menu de comando e, em seguida, escolha **adicionar novo ícone** no menu que aparece.  
  
5.  No **adicionar novo recurso** caixa de diálogo, o nome do novo ícone **WebPartsNode**e, em seguida, escolha o **Add** botão.  
  
     O novo ícone abre na **Editor de imagens**.  
  
6.  Edite a versão de 16x16 do ícone para que ele tenha um design que você pode reconhecer facilmente.  
  
7.  Abra o menu de atalho para a versão de 32 x 32 do ícone e, em seguida, escolha **excluir tipo de imagem**.  
  
8.  Repita as etapas 5 a 8 para adicionar um segundo ícone aos recursos do projeto e nomeie esse ícone **WebPart**.  
  
9. No **Gerenciador de soluções**, sob o **recursos** pasta para o **WebPartNodeExtension** do projeto, abra o menu de atalho do **WebPartsNode.ico**.  
  
10. No **propriedades** janela, escolha a seta ao lado **Build Action**e, em seguida, escolha **Embedded Resource** no menu que aparece.  
  
11. Repita as duas últimas etapas para **WebPart.ico**.  
  
## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>Adicionar o nó da Galeria de Web Parts ao Gerenciador de servidores
 Criar uma classe que adiciona o novo **Galeria de Web Parts** nó para cada nó do site do SharePoint. Para adicionar o novo nó, a classe implementa o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> interface. Implementar essa interface sempre que você deseja estender o comportamento de um nó existente no **Gerenciador de servidores**, como a adição de um nó filho para um nó.  
  
#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>Para adicionar o nó de galeria de Web Parts ao Gerenciador de servidores
  
1.  No projeto WebPartNodeExtension, abra o arquivo de código SiteNodeExtension e, em seguida, cole o seguinte código nele.  
  
    > [!NOTE]  
    >  Depois que você adicionar esse código, o projeto terá alguns erros de compilação, mas eles desaparecem quando você adiciona código em etapas posteriores.  
  
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#1](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/sitenodeextension.cs#1)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#1](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/sitenodeextension.vb#1)]  
  
## <a name="define-a-node-type-that-represents-a-web-part"></a>Definir um tipo de nó que representa uma web part
 Crie uma classe que define um novo tipo de nó que representa uma Web Part. Visual Studio usa esse novo tipo de nó para exibir nós filho sob a **Galeria de Web Parts** nó. Cada nó filho representa uma única Web Part no site do SharePoint.  
  
 Para definir o novo tipo de nó, a classe implementa o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> interface. Implementar essa interface sempre que você deseja definir um novo tipo de nó no **Gerenciador de servidores**.  
  
#### <a name="to-define-the-web-part-node-type"></a>Para definir o tipo de nó da web part
  
1.  No projeto WebPartNodeExtension, abra o arquivo de código WebPartNodeTypeProvder e, em seguida, cole o seguinte código nele.  
  
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#2](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb#2)]
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#2](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodetypeprovider.cs#2)]  
  
## <a name="define-the-web-part-data-class"></a>Definir a classe de dados da web part
 Defina uma classe que contém dados sobre uma única Web Part no site do SharePoint. Posteriormente neste passo a passo, você criará um comando do SharePoint personalizado que recupera dados sobre cada Web Part no site e, em seguida, atribui os dados para as instâncias dessa classe.  
  
#### <a name="to-define-the-web-part-data-class"></a>Para definir a classe de dados da web part
  
1.  No projeto WebPartNodeExtension, abra o arquivo de código WebPartNodeInfo e, em seguida, cole o seguinte código nele.  
  
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#3](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartnodeinfo.vb#3)]
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#3](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartnodeinfo.cs#3)]  
  
## <a name="define-the-ids-for-the-sharepoint-commands"></a>Defina as IDs para os comandos do SharePoint
 Defina várias cadeias de caracteres que identificam os comandos do SharePoint personalizados. Você irá implementar esses comandos posteriormente neste passo a passo.  
  
#### <a name="to-define-the-command-ids"></a>Para definir as IDs de comando
  
1.  No projeto WebPartNodeExtension, abra o arquivo de código WebPartCommandIds e, em seguida, cole o seguinte código nele.  
  
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#4](../sharepoint/codesnippet/CSharp/WebPartNode/webpartnodeextension/webpartcommandids.cs#4)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#4](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartnodeextension/webpartcommandids.vb#4)]  
  
## <a name="create-the-custom-sharepoint-commands"></a>Criar os comandos do SharePoint personalizados
 Crie comandos personalizados que chamam o modelo de objeto do servidor do SharePoint para recuperar dados sobre as Web Parts no site do SharePoint. Cada comando é um método que tem o <xref:Microsoft.VisualStudio.SharePoint.Commands.SharePointCommandAttribute> aplicado a ele.  
  
#### <a name="to-define-the-sharepoint-commands"></a>Para definir os comandos do SharePoint  
  
1.  No projeto WebPartCommands, abra o arquivo de código WebPartCommands e, em seguida, cole o seguinte código nele.  
  
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNodeWithCommands#6](../sharepoint/codesnippet/CSharp/WebPartNode/WebPartCommands/WebPartCommands.cs#6)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNodeWithCommands#6](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnodewithcommands.webpartnode/webpartcommands/webpartcommands.vb#6)]  
  
## <a name="checkpoint"></a>Ponto de verificação  
 Neste ponto do passo a passo, todo o código para o **Galeria de Web Parts** nó e os comandos do SharePoint agora estão nos projetos. Compile a solução para certificar-se de que ambos os projetos compilar sem erros.  
  
#### <a name="to-build-the-solution"></a>Para compilar a solução  
  
1.  Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
    > [!WARNING]  
    >  Neste ponto, o projeto WebPartNode pode ter um erro de compilação porque o arquivo de manifesto do VSIX não tem um valor para o autor. Esse erro desaparecerá quando você adiciona um valor em etapas posteriores.  
  
## <a name="create-a-vsix-package-to-deploy-the-extension"></a>Criar um pacote VSIX para implantar a extensão
 Para implantar a extensão, use o projeto do VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo vsixmanifest no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.  
  
#### <a name="to-configure-the-vsix-package"></a>Para configurar o pacote VSIX  
  
1.  Na **Gerenciador de soluções**, sob o projeto WebPartNode, abra o **vsixmanifest** arquivo no editor de manifesto.  
  
     O arquivo vsixmanifest é a base para o arquivo Extension vsixmanifest que exigem todos os pacotes VSIX. Para obter mais informações sobre esse arquivo, consulte [1.0 referência do esquema de extensão do VSIX](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).  
  
2.  No **nome do produto** , digite **Web parte Galeria de nó do Gerenciador de servidores**.  
  
3.  No **autor** , digite **Contoso**.  
  
4.  No **descrição** , digite **adiciona um nó de galeria de Web Parts personalizado para o nó de conexões do SharePoint no Gerenciador de servidores. Essa extensão usa um comando do SharePoint personalizado para chamar o modelo de objeto do servidor.**  
  
5.  Escolha o **ativos** guia do editor e, em seguida, escolha o **New** botão.  
  
     O **adicionar novo ativo** caixa de diálogo é exibida.  
  
6.  No **tipo** , escolha **mefcomponent**.  
  
    > [!NOTE]  
    >  Esse valor corresponde à `MefComponent` elemento no arquivo Extension vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [MEFComponent Element (esquema de VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).  
  
7.  No **fonte** , escolha **um projeto na solução atual**.  
  
8.  No **Project** , escolha **WebPartNodeExtension** e, em seguida, escolha o **Okey** botão.  
  
9. No editor de manifesto, escolha o **New** novamente no botão.  
  
     O **adicionar novo ativo** caixa de diálogo é exibida.  
  
10. No **tipo** , digite **SharePoint.Commands.v4**.  
  
    > [!NOTE]  
    >  Esse elemento Especifica uma extensão personalizada que você deseja incluir na extensão do Visual Studio. Para obter mais informações, consulte [ativo Element (esquema de VSX)](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737).  
  
11. No **fonte** , escolha o **um projeto na solução atual** item de lista.  
  
12. No **Project** , escolha **WebPartCommands**e, em seguida, escolha o **Okey** botão.  
  
13. Na barra de menus, escolha **construir** > **compilar solução**e, em seguida, certifique-se de que a solução é compilado sem erros.  
  
14. Certifique-se de que a pasta de saída de compilação para o projeto WebPartNode agora contém o arquivo WebPartNode.vsix.  
  
     Por padrão, a pasta de saída de compilação é o... pasta \bin\debug sob a pasta que contém seu arquivo de projeto.  
  
## <a name="test-the-extension"></a>A extensão de teste
 Agora você está pronto para testar a nova **Galeria de Web Parts** nó no **Gerenciador de servidores**. Primeiro, inicie a depuração da extensão em uma instância experimental do Visual Studio. Em seguida, use o novo **Web Parts** nó na instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
#### <a name="to-start-debugging-the-extension"></a>Para iniciar a extensão de depuração  
  
1.  Reiniciar [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] com credenciais administrativas e, em seguida, abra a solução WebPartNode.  
  
2.  No projeto WebPartNodeExtension, abra o arquivo de código SiteNodeExtension e, em seguida, adicione um ponto de interrupção para a primeira linha de código na `NodeChildrenRequested` e `CreateWebPartNodes` métodos.  
  
3.  Escolha o **F5** tecla para iniciar a depuração.  
  
     Visual Studio instalará a extensão para o servidor Explorer\1.0 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web extensão de galeria de parte do nó e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.  
  
#### <a name="to-test-the-extension"></a>Para testar a extensão  
  
1.  Na instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], na barra de menus, escolha **modo de exibição** > **Gerenciador de servidores**.  
  
2.  Execute as seguintes etapas se o site do SharePoint que você deseja usar para teste não aparecer sob o **conexões do SharePoint** nó no **Gerenciador de servidores**:  
  
    1.  Na **Gerenciador de servidores**, abra o menu de atalho **conexões do SharePoint**e, em seguida, escolha **Adicionar Conexão**.  
  
    2.  No **Adicionar Conexão do SharePoint** diálogo caixa, digite a URL do site do SharePoint ao qual você deseja se conectar e, em seguida, escolha o **Okey** botão.  
  
         Para especificar o site do SharePoint no computador de desenvolvimento, insira **http://localhost**.  
  
3.  Expanda o nó de conexão de site (que exibe a URL do seu site) e, em seguida, expanda um nó do site filho (por exemplo, **Site de equipe**).  
  
4.  Verifique o código em outra instância do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] para no ponto de interrupção que você definiu anteriormente em de `NodeChildrenRequested` método e, em seguida, escolha **F5** para continuar a depuração do projeto.  
  
5.  Na instância experimental do Visual Studio, verifique se um novo nó nomeado **Galeria de Web Parts** aparece sob o nó do site de nível superior e, em seguida, expanda o **Galeria de Web Parts** nó.  
  
6.  Verifique se o código em outra instância do Visual Studio para no ponto de interrupção que você definiu anteriormente na `CreateWebPartNodes` método e, em seguida, escolha o **F5** tecla para continuar a depuração do projeto.  
  
7.  Na instância experimental do Visual Studio, verifique se todas as Web Parts no site conectado aparecem sob o **Galeria de Web Parts** nó no **Gerenciador de servidores**.  
  
8.  Na **Gerenciador de servidores**, abra o menu de atalho para uma das partes da Web e, em seguida, escolha **propriedades**.  
  
9. Na instância do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] que você está depurando, verifique se os detalhes sobre a Web Part aparecem em de **propriedades** janela.  
  
## <a name="uninstall-the-extension-from-visual-studio"></a>Desinstalar a extensão do Visual Studio
 Depois de terminar de testar a extensão, desinstale a extensão do Visual Studio.  
  
#### <a name="to-uninstall-the-extension"></a>Para desinstalar a extensão  
  
1.  Na instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], na barra de menus, escolha **ferramentas** > **extensões e atualizações**.  
  
     A caixa de diálogo **Extensões e Atualizações** é aberta.  
  
2.  Na lista de extensões, escolha **extensão de nó de galeria da Web parte do Gerenciador de servidores**e, em seguida, escolha o **desinstalar** botão.  
  
3.  Na caixa de diálogo que aparece, escolha o **Yes** botão para confirmar que você deseja desinstalar a extensão e, em seguida, escolha o **reiniciar agora** botão para concluir a desinstalação.  
  
4.  Feche ambas as instâncias do Visual Studio (a instância experimental e a instância do Visual Studio em que a solução WebPartNode estiver aberta).  
  
## <a name="see-also"></a>Consulte também
 [Estender o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)   
 [Passo a passo: Chamar o modelo de objeto de cliente do SharePoint em uma extensão do Gerenciador de servidores](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)   
 [Editor de imagens para ícones](/cpp/windows/image-editor-for-icons)   
 [Criando um ícone ou outra imagem &#40;Editor de imagens para ícones&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)  
  
