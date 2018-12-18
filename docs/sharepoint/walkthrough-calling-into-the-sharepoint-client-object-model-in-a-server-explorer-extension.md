---
title: 'Passo a passo: Chamando o modelo de objeto do cliente do SharePoint em uma extensão do Gerenciador de servidores | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, client object model
- SharePoint commands [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: f4510aa820e0f82c2fcd73ccb83ed0f8120a1399
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296028"
---
# <a name="walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension"></a>Passo a passo: Chamando o modelo de objeto de cliente do SharePoint em uma extensão do Gerenciador de servidores
  Este passo a passo demonstra como chamar o modelo de objeto de cliente do SharePoint de uma extensão para o **conexões do SharePoint** nó no **Gerenciador de servidores**. Para obter mais informações sobre como usar o modelo de objeto de cliente do SharePoint, consulte [chamam os modelos de objeto SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
-   Criando um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] extensão estende o **conexões do SharePoint** nó do **Gerenciador de servidores** das seguintes maneiras:  
  
    -   Adiciona a extensão de um **Galeria de Web Parts** nó em cada nó do site do SharePoint no **Gerenciador de servidores**. Esse novo nó contém nós filho que representam cada Web Part na Galeria de Web Parts no site.  
  
    -   A extensão define um novo tipo de nó que representa uma instância de Web Part. Esse novo tipo de nó é a base para os nós filho sob a nova **Galeria de Web Parts** nó. O novo tipo de nó de Web Part exibe informações na **propriedades** janela sobre a Web Part que o nó representa.  
  
-   Criando um pacote de extensão VSIX (Visual Studio) para implantar a extensão.  
  
-   Depurando e testando a extensão.  
  
> [!NOTE]  
>  A extensão que você cria neste passo a passo se parece com a extensão que você cria no [instruções passo a passo: estenda o Gerenciador de servidores para exibir web parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md). Essa explicação passo a passo usa o modelo de objeto do SharePoint server, mas este passo a passo realiza as mesmas tarefas usando o modelo de objeto do cliente.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passo:  
  
-   Edições com suporte do Windows, SharePoint e Visual Studio.
  
-   O SDK do Visual Studio. Este passo a passo usa o **VSIX Project** modelo no SDK para criar um pacote VSIX para implantar a extensão. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).  
  
Conhecimento dos conceitos a seguir é útil, mas não necessário para concluir o passo a passo:  
  
-   Usando o modelo de objeto de cliente do SharePoint. Para obter mais informações, consulte [modelo de objeto de cliente gerenciado](http://go.microsoft.com/fwlink/?LinkId=177797).  
  
-   Web parts no SharePoint. Para obter mais informações, consulte [Web Parts Overview](http://go.microsoft.com/fwlink/?LinkId=177803).  
  
## <a name="create-the-projects"></a>Crie os projetos
 Para concluir este passo a passo, você deve criar dois projetos:  
  
- Um projeto VSIX para criar o pacote VSIX para implantar o **Gerenciador de servidores** extensão.  
  
- Um projeto de biblioteca de classe que implementa o **Gerenciador de servidores** extensão.  
  
  Inicie o passo a passo Criando os projetos.  
  
#### <a name="to-create-the-vsix-project"></a>Para criar o projeto do VSIX  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
3.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha **extensibilidade**.  
  
    > [!NOTE]  
    >  O **extensibilidade** o nó está disponível somente se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos no início deste tópico.  
  
4.  Na parte superior da caixa de diálogo, escolha **.NET Framework 4.5** na lista de versões do .NET Framework.  
  
     As extensões de ferramentas do SharePoint exigem recursos nesta versão do .NET Framework.  
  
5.  Escolha o **VSIX Project** modelo.  
  
6.  No **nome** , digite **WebPartNode**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **WebPartNode** projeto ao **Gerenciador de soluções**.  
  
#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do nó da solução, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha **Windows**.  
  
3.  Na parte superior da caixa de diálogo, escolha **.NET Framework 4.5** na lista de versões do .NET Framework.  
  
4.  Na lista de modelos de projeto, escolha **biblioteca de classes**.  
  
5.  No **nome** , digite **WebPartNodeExtension**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **WebPartNodeExtension** projeto à solução e abre o arquivo de código padrão Class1.  
  
6.  Exclua o arquivo de código Class1 do projeto.  
  
## <a name="configure-the-extension-project"></a>Configurar o projeto de extensão
 Antes de escrever código para criar a extensão, você deve adicionar arquivos de código e referências de assembly ao seu projeto, e você deve atualizar o namespace padrão.  
  
#### <a name="to-configure-the-project"></a>Para configurar o projeto  
  
1.  No **WebPartNodeExtension** do projeto, adicione dois arquivos de código que são nomeados SiteNodeExtension e WebPartNodeTypeProvider.  
  
2.  Abra o menu de atalho para o projeto WebPartNodeExtension e, em seguida, escolha **adicionar referência**.  
  
3.  No **Gerenciador de referências - WebPartNodeExtension** diálogo caixa, escolha o **Framework** nó e, em seguida, selecione as caixas de seleção para o Composition e System assemblies.  
  
4.  Escolha o **extensões** nó, selecione a caixa de seleção para cada um dos assemblies a seguir e, em seguida, escolha o **Okey** botão:  
  
    -   Microsoft  
  
    -   Microsoft.SharePoint.Client.Runtime  
  
    -   Microsoft.VisualStudio.SharePoint  
  
5.  Abra o menu de atalho para o **WebPartNodeExtension** do projeto e, em seguida, escolha **propriedades**.  
  
     O **Designer de Projeto** é aberto.  
  
6.  Escolha a guia **Aplicativo**.  
  
7.  No **namespace padrão** caixa (c#) ou **namespace raiz** (Visual Basic), digite **ServerExplorer.SharePointConnections.WebPartNode**.  
  
## <a name="create-icons-for-the-new-nodes"></a>Criar ícones para os novos nós
 Criar dois ícones para o **Gerenciador de servidores** extensão: um ícone para o novo **Galeria de Web Parts** nó e outro ícone para cada nó de Web Part filho sob o **Galeria de Web Parts** nó. Posteriormente neste passo a passo, você escreverá código que associa esses ícones com os nós.  
  
#### <a name="to-create-icons-for-the-nodes"></a>Para criar os ícones para os nós  
  
1.  No **Designer de projeto** para o projeto WebPartNodeExtension, escolha o **recursos** guia.  
  
2.  Escolha o link **este projeto não contém um arquivo de recursos padrão. Clique aqui para criar um.**  
  
     Visual Studio cria um arquivo de recurso e abre no designer.  
  
3.  Na parte superior do designer, escolha a seta na **adicionar recurso** menu de comando e, em seguida, escolha **adicionar novo ícone**.  
  
4.  Insira **WebPartsNode** para o ícone do novo nome e, em seguida, escolha o **Add** botão.  
  
     O novo ícone abre na **Editor de imagens**.  
  
5.  Edite a versão de 16x16 do ícone para que ele tenha um design que você pode reconhecer facilmente.  
  
6.  Abra o menu de atalho para a versão de 32 x 32 do ícone e, em seguida, escolha **excluir tipo de imagem**.  
  
7.  Repita as etapas 3 a 7 para adicionar um segundo ícone aos recursos do projeto e nomeie esse ícone **WebPart**.  
  
8.  Na **Gerenciador de soluções**, no **recursos** pasta para o **WebPartNodeExtension** do projeto, escolha *WebPartsNode.ico*.  
  
9. No **propriedades** janela, abra o **Build Action** lista e, em seguida, escolha **Embedded Resource**.  
  
10. Repita as duas últimas etapas para *WebPart.ico*.  
  
## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>Adicionar o nó de galeria da web part ao Gerenciador de servidores
 Criar uma classe que adiciona o novo **Galeria de Web Parts** nó para cada nó do site do SharePoint. Para adicionar o novo nó, a classe implementa o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> interface. Implementar essa interface sempre que você deseja estender o comportamento de um nó existente no **Gerenciador de servidores**, como adicionar um novo nó filho a um nó.  
  
#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>Para adicionar o nó de galeria da web part ao Gerenciador de servidores
  
1.  Cole o seguinte código para o **SiteNodeExtension** arquivo de código para o **WebPartNodeExtension** projeto.  
  
    > [!NOTE]  
    >  Depois de adicionar esse código, o projeto terá alguns erros de compilação. Esses erros serão eliminados quando você adicionar o código em etapas posteriores.  
  
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNode#1](../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/sitenodeextension.cs#1)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNode#1](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/sitenodeextension.vb#1)]  
  
## <a name="define-a-node-type-that-represents-a-web-part"></a>Definir um tipo de nó que representa uma web part
 Crie uma classe que define um novo tipo de nó que representa uma Web Part. Visual Studio usa esse novo tipo de nó para exibir nós filho sob a **Galeria de Web Parts** nó. Cada um de nós filho representa uma única Web Part no site do SharePoint.  
  
 Para definir o novo tipo de nó, a classe implementa o <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> interface. Implementar essa interface sempre que você deseja definir um novo tipo de nó no **Gerenciador de servidores**.  
  
#### <a name="to-define-the-web-part-node-type"></a>Para definir o tipo de nó da web part
  
1.  Cole o seguinte código para o **WebPartNodeTypeProvider** arquivo de código para o **WebPartNodeExtension** projeto.  
  
     [!code-csharp[SPExtensibility.SPExplorer.WebPartNode#2](../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/webpartnodetypeprovider.cs#2)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNode#2](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb#2)]  
  
## <a name="checkpoint"></a>Ponto de verificação  
 Neste ponto do passo a passo, todo o código para o **Galeria de Web Parts** nó agora está no projeto. Criar o **WebPartNodeExtension** projeto para ter certeza de que ele foi compilado sem erros.  
  
#### <a name="to-build-the-project"></a>Para compilar o projeto  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **WebPartNodeExtension** do projeto e, em seguida, escolha **Build**.  
  
## <a name="create-a-vsix-package-to-deploy-the-extension"></a>Criar um pacote VSIX para implantar a extensão
 Para implantar a extensão, use o projeto do VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo vsixmanifest que está incluído no projeto. Em seguida, crie o pacote VSIX criando a solução.  
  
#### <a name="to-configure-the-vsix-package"></a>Para configurar o pacote VSIX  
  
1.  Na **Gerenciador de soluções**, no **WebPartNode** projeto, abra **vsixmanifest** arquivo no editor de manifesto.  
  
     O arquivo vsixmanifest é a base para o arquivo Extension vsixmanifest que exigem todos os pacotes VSIX. Para obter mais informações sobre esse arquivo, consulte [1.0 referência do esquema de extensão do VSIX](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).  
  
2.  No **nome do produto** , digite **Web parte Galeria de nó do Gerenciador de servidores**.  
  
3.  No **autor** , digite **Contoso**.  
  
4.  No **descrição** , digite **adiciona um nó de galeria de Web Parts personalizado para o nó de conexões do SharePoint no Gerenciador de servidores**.  
  
5.  Sobre o **ativos** guia do editor, escolha a **New** botão.  
  
6.  No **adicionar novo ativo** na caixa de **tipo** , escolha **mefcomponent**.  
  
    > [!NOTE]  
    >  Esse valor corresponde à `MefComponent` elemento no arquivo Extension vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [MEFComponent Element (esquema de VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).  
  
7.  No **fonte** , escolha **um projeto na solução atual**.  
  
8.  No **Project** , escolha **WebPartNodeExtension**e, em seguida, escolha o **Okey** botão.  
  
9. Na barra de menus, escolha **construir** > **compilar solução**e, em seguida, certifique-se de que a solução é compilado sem erros.  
  
10. Certifique-se de que a pasta de saída de compilação para o projeto WebPartNode agora contém o arquivo WebPartNode.vsix.  
  
     Por padrão, a pasta de saída de compilação é o... pasta \bin\debug sob a pasta que contém seu arquivo de projeto.  
  
## <a name="test-the-extension"></a>A extensão de teste
 Agora você está pronto para testar a nova **Galeria de Web Parts** nó no **Gerenciador de servidores**. Primeiro, começar a depurar o projeto de extensão em uma instância experimental do Visual Studio. Em seguida, use o novo **Web Parts** nó na instância experimental do Visual Studio.  
  
#### <a name="to-start-debugging-the-extension"></a>Para iniciar a extensão de depuração  
  
1.  Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra o **WebPartNode** solução.  
  
2.  No projeto WebPartNodeExtension, abra o **SiteNodeExtension** arquivo de código e, em seguida, adicione um ponto de interrupção para as primeiras linhas de código na `NodeChildrenRequested` e `CreateWebPartNodes` métodos.  
  
3.  Escolha o **F5** tecla para iniciar a depuração.  
  
     Visual Studio instalará a extensão para o servidor Explorer\1.0 %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web extensão de galeria de parte do nó e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.  
  
#### <a name="to-test-the-extension"></a>Para testar a extensão  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **modo de exibição** > **Gerenciador de servidores**.  
  
2.  Verifique se o site do SharePoint que você deseja usar para teste aparece sob o **conexões do SharePoint** nó no **Gerenciador de servidores**. Se não estiver listado, siga estas etapas:  
  
    1.  Abra o menu de atalho **conexões do SharePoint**e, em seguida, escolha **Adicionar Conexão**.  
  
    2.  No **Adicionar Conexão do SharePoint** diálogo caixa, digite a URL do site do SharePoint ao qual você deseja se conectar e, em seguida, escolha o **Okey** botão.  
  
         Para especificar o site do SharePoint no computador de desenvolvimento, digite **http://localhost**.  
  
3.  Expanda o nó de conexão de site (que exibe a URL do seu site) e, em seguida, expanda um nó do site filho (por exemplo, **Site de equipe**).  
  
4.  Verifique se o código em outra instância do Visual Studio para no ponto de interrupção que você definiu anteriormente na `NodeChildrenRequested` método e, em seguida, escolha o **F5** tecla para continuar a depuração do projeto.  
  
5.  Na instância experimental do Visual Studio, expanda o **Galeria de Web Parts** nó, que aparece sob o nó do site de nível superior.  
  
6.  Verifique se o código em outra instância do Visual Studio para no ponto de interrupção que você definiu anteriormente na `CreateWebPartNodes` método e, em seguida, escolha o **F5** tecla para continuar a depuração do projeto.  
  
7.  Na instância experimental do Visual Studio, verifique se todas as Web Parts no site conectado aparecem sob o **Galeria de Web Parts** nó no **Gerenciador de servidores**.  
  
8.  Abra o menu de atalho para uma Web Part e, em seguida, escolha **propriedades**.  
  
9. No **propriedades** janela, verifique se os detalhes sobre a Web Part aparecem.  
  
10. Na **Gerenciador de servidores**, abra o menu de atalho para a Web Part do mesmo e, em seguida, escolha **Exibir mensagem**.  
  
     Na caixa de mensagem que aparece, escolha o **Okey** botão.  
  
## <a name="uninstall-the-extension-from-visual-studio"></a>Desinstalar a extensão do Visual Studio
 Depois de concluir a extensão de teste, você deve desinstalá-lo do Visual Studio.  
  
#### <a name="to-uninstall-the-extension"></a>Para desinstalar a extensão  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas** > **extensões e atualizações**.  
  
     A caixa de diálogo **Extensões e Atualizações** é aberta.  
  
2.  Na lista de extensões, escolha **Web Part Galeria de nó do Gerenciador de servidores**e, em seguida, escolha o **desinstalar** botão.  
  
3.  Na caixa de diálogo que aparece, escolha o **Sim** botão.  
  
4.  Escolha o **reiniciar agora** botão para concluir a desinstalação.  
  
     O item de projeto também será desinstalado.  
  
5.  Feche ambas as instâncias do Visual Studio (a instância experimental e a instância do Visual Studio em que a solução WebPartNode estiver aberta).  
  
## <a name="see-also"></a>Consulte também
 [Chamar os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md)   
 [Estender o nó de conexões do SharePoint no Gerenciador de servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)   
 [Passo a passo: Estenda o Gerenciador de servidores para exibir web parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)   
 [Editor de imagens para ícones](/cpp/windows/image-editor-for-icons)   
 [Criando um ícone ou outra imagem &#40;Editor de imagens para ícones&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)