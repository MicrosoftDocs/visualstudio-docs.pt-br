---
title: 'Gerenciador de Servidores: estendendo o nó conexões do SharePoint'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, client object model
- SharePoint commands [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: ebd7d500767e896ce9576a3d007a4357b9c5281c
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86014635"
---
# <a name="walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension"></a>Walkthrough: chamando o modelo de objeto de cliente do SharePoint em uma extensão Gerenciador de Servidores
  Este tutorial demonstra como chamar o modelo de objeto do cliente do SharePoint de uma extensão para o nó **conexões do SharePoint** no **Gerenciador de servidores**. Para obter mais informações sobre como usar o modelo de objeto de cliente do SharePoint, consulte [chamar os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).

 Este tutorial demonstra as seguintes tarefas:

- Criar uma [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] extensão que estenda o nó **conexões do SharePoint** de **Gerenciador de servidores** das seguintes maneiras:

  - A extensão adiciona um nó **da Galeria de Web Parts** em cada nó do site do SharePoint no **Gerenciador de servidores**. Esse novo nó contém nós filho que representam cada Web Part na Galeria de Web Parts no site.

  - A extensão define um novo tipo de nó que representa uma instância de Web Part. Esse novo tipo de nó é a base para os nós filho no novo nó **da Galeria de Web Parts** . O novo tipo de nó da Web Part exibe informações na janela **Propriedades** sobre a Web Part que o nó representa.

- Criando um pacote de VSIX (Visual Studio Extension) para implantar a extensão.

- Depurando e testando a extensão.

> [!NOTE]
> A extensão que você cria neste passo a passos é semelhante à extensão que você cria em [Walkthrough: estender Gerenciador de servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md). Essa instrução usa o modelo de objeto do SharePoint Server, mas este passo a passos realiza as mesmas tarefas usando o modelo de objeto do cliente.

## <a name="prerequisites"></a>Pré-requisitos
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passos:

- Edições com suporte do Windows, SharePoint e Visual Studio.

- O SDK do Visual Studio. Este tutorial usa o modelo de **projeto VSIX** no SDK para criar um pacote VSIX para implantar a extensão. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).

O conhecimento dos seguintes conceitos é útil, mas não é necessário, para concluir o passo a passos:

- Usando o modelo de objeto de cliente do SharePoint. Para obter mais informações, consulte [modelo de objeto de cliente gerenciado](/previous-versions/office/developer/sharepoint-2010/ee537247(v=office.14)).

- Web Parts no SharePoint. Para obter mais informações, consulte [Web Parts visão geral](/previous-versions/office/ms432401(v=office.14)).

## <a name="create-the-projects"></a>Criar os projetos
 Para concluir este passo a passos, você deve criar dois projetos:

- Um projeto VSIX para criar o pacote VSIX para implantar a extensão **Gerenciador de servidores** .

- Um projeto de biblioteca de classes que implementa a extensão de **Gerenciador de servidores** .

  Inicie o passo a passos criando os projetos.

#### <a name="to-create-the-vsix-project"></a>Para criar o projeto VSIX

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

3. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e escolha **extensibilidade**.

    > [!NOTE]
    > O nó **extensibilidade** só estará disponível se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos anteriormente neste tópico.

4. Na parte superior da caixa de diálogo, escolha **.NET Framework 4,5** na lista de versões do .NET Framework.

     As extensões de ferramenta do SharePoint exigem recursos nesta versão do .NET Framework.

5. Escolha o modelo de **projeto VSIX** .

6. Na caixa **nome** , digite **WebPartNode**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **WebPartNode** ao **Gerenciador de soluções**.

#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha **Windows**.

3. Na parte superior da caixa de diálogo, escolha **.NET Framework 4,5** na lista de versões do .NET Framework.

4. Na lista de modelos de projeto, escolha **biblioteca de classes**.

5. Na caixa **nome** , digite **WebPartNodeExtension**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **WebPartNodeExtension** à solução e abre o arquivo de código de Class1 padrão.

6. Exclua o arquivo de código Class1 do projeto.

## <a name="configure-the-extension-project"></a>Configurar o projeto de extensão
 Antes de escrever o código para criar a extensão, você deve adicionar arquivos de código e referências de assembly ao seu projeto, e você deve atualizar o namespace padrão.

#### <a name="to-configure-the-project"></a>Para configurar o projeto

1. No projeto **WebPartNodeExtension** , adicione dois arquivos de código chamados SiteNodeExtension e WebPartNodeTypeProvider.

2. Abra o menu de atalho para o projeto WebPartNodeExtension e escolha **Adicionar referência**.

3. Na caixa de diálogo **Gerenciador de referências-WebPartNodeExtension** , escolha o nó **estrutura** e marque as caixas de seleção dos assemblies System. ComponentModel. composição e System. Windows. Forms.

4. Escolha o nó **extensões** , marque a caixa de seleção de cada um dos seguintes assemblies e, em seguida, escolha o botão **OK** :

    - Microsoft. SharePoint. Client

    - Microsoft. SharePoint. Client. Runtime

    - Microsoft. VisualStudio. SharePoint

5. Abra o menu de atalho para o projeto **WebPartNodeExtension** e escolha **Propriedades**.

     O **Designer de Projeto** é aberto.

6. Escolha a guia **Aplicativo**.

7. Na caixa **namespace padrão** (C#) ou no **namespace raiz** (Visual Basic), digite **ServerExplorer. SharePointConnections. WebPartNode**.

## <a name="create-icons-for-the-new-nodes"></a>Criar ícones para os novos nós
 Crie dois ícones para a extensão de **Gerenciador de servidores** : um ícone para o novo nó **da Galeria de Web Parts** e outro ícone para cada nó da Web Part filho sob o nó da **Galeria de Web Parts** . Mais adiante neste tutorial, você escreverá um código que associa esses ícones aos nós.

#### <a name="to-create-icons-for-the-nodes"></a>Para criar ícones para os nós

1. No **Designer de projeto** do projeto WebPartNodeExtension, escolha a guia **recursos** .

2. Escolha o link **este projeto não contém um arquivo de recursos padrão. Clique aqui para criar um.**

     O Visual Studio cria um arquivo de recurso e o abre no designer.

3. Na parte superior do designer, escolha a seta no comando de menu **Adicionar recurso** e escolha **Adicionar novo ícone**.

4. Digite **WebPartsNode** para o nome do novo ícone e, em seguida, escolha o botão **Adicionar** .

     O novo ícone é aberto no **Editor de imagem**.

5. Edite a versão de 16x16 do ícone para que ele tenha um design que você possa reconhecer facilmente.

6. Abra o menu de atalho da versão 32x32 do ícone e escolha **excluir tipo de imagem**.

7. Repita as etapas de 3 a 7 para adicionar um segundo ícone aos recursos do projeto e nomeie esta **WebPart**de ícone.

8. No **Gerenciador de soluções**, na pasta de **recursos** do projeto **WebPartNodeExtension** , escolha *WebPartsNode. ico*.

9. Na janela **Propriedades** , abra a lista **ação de compilação** e, em seguida, escolha **recurso incorporado**.

10. Repita as duas últimas etapas para *WebPart. ico*.

## <a name="add-the-web-part-gallery-node-to-server-explorer"></a>Adicione o nó Galeria de Web Parts a Gerenciador de Servidores
 Crie uma classe que adiciona o novo nó **da Galeria de Web Parts** a cada nó do site do SharePoint. Para adicionar o novo nó, a classe implementa a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeExtension> interface. Implemente essa interface sempre que desejar estender o comportamento de um nó existente no **Gerenciador de servidores**, como adicionar um novo nó filho a um nó.

#### <a name="to-add-the-web-part-gallery-node-to-server-explorer"></a>Para adicionar o nó Galeria de Web Parts a Gerenciador de Servidores

1. Cole o código a seguir no arquivo de código **SiteNodeExtension** para o projeto **WebPartNodeExtension** .

    > [!NOTE]
    > Depois de adicionar esse código, o projeto terá alguns erros de compilação. Esses erros vão desaparecer quando você adiciona código em etapas posteriores.

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNode#1](../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/sitenodeextension.cs#1)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNode#1](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/sitenodeextension.vb#1)]

## <a name="define-a-node-type-that-represents-a-web-part"></a>Definir um tipo de nó que representa uma Web Part
 Crie uma classe que define um novo tipo de nó que representa uma Web Part. O Visual Studio usa esse novo tipo de nó para exibir os nós filho no nó **da Galeria de Web Parts** . Cada um desses nós filho representa uma única Web Part no site do SharePoint.

 Para definir o novo tipo de nó, a classe implementa a <xref:Microsoft.VisualStudio.SharePoint.Explorer.IExplorerNodeTypeProvider> interface. Implemente essa interface sempre que desejar definir um novo tipo de nó no **Gerenciador de servidores**.

#### <a name="to-define-the-web-part-node-type"></a>Para definir o tipo de nó de Web Part

1. Cole o código a seguir no arquivo de código **WebPartNodeTypeProvider** para o projeto **WebPartNodeExtension** .

     [!code-csharp[SPExtensibility.SPExplorer.WebPartNode#2](../sharepoint/codesnippet/CSharp/webpartnode/webpartnodeextension/webpartnodetypeprovider.cs#2)]
     [!code-vb[SPExtensibility.SPExplorer.WebPartNode#2](../sharepoint/codesnippet/VisualBasic/spextensibility.spexplorer.webpartnode.webpartnode/webpartnodeextension/webpartnodetypeprovider.vb#2)]

## <a name="checkpoint"></a>Ponto de verificação
 Neste ponto do passo a passo, todo o código do nó **da Galeria de Web Parts** agora está no projeto. Compile o projeto **WebPartNodeExtension** para certificar-se de que ele seja compilado sem erros.

#### <a name="to-build-the-project"></a>Para compilar o projeto

1. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **WebPartNodeExtension** e escolha **Compilar**.

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>Criar um pacote VSIX para implantar a extensão
 Para implantar a extensão, use o projeto VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo Source. Extension. vsixmanifest que está incluído no projeto. Em seguida, crie o pacote VSIX criando a solução.

#### <a name="to-configure-the-vsix-package"></a>Para configurar o pacote VSIX

1. No **Gerenciador de soluções**, no projeto **WebPartNode** , abra o arquivo **Source. Extension. vsixmanifest** no editor de manifesto.

     O arquivo Source. Extension. vsixmanifest é a base para o arquivo extension. vsixmanifest que todos os pacotes VSIX exigem. Para obter mais informações sobre esse arquivo, consulte [referência do esquema de extensão do VSIX 1,0](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).

2. Na caixa **nome do produto** , insira o **nó Galeria de Web parts para Gerenciador de servidores**.

3. Na caixa **autor** , digite **contoso**.

4. Na caixa **Descrição** , digite **adiciona um nó de galeria de Web Parts personalizado ao nó conexões do SharePoint no Gerenciador de servidores**.

5. Na guia **ativos** do editor, escolha o botão **novo** .

6. Na caixa de diálogo **Adicionar novo ativo** , na lista **tipo** , escolha **Microsoft. VisualStudio. MefComponent**.

    > [!NOTE]
    > Esse valor corresponde ao `MefComponent` elemento no arquivo extension. vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [elemento MEFComponent (esquema VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).

7. Na lista **origem** , escolha **um projeto na solução atual**.

8. Na lista **projeto** , escolha **WebPartNodeExtension**e, em seguida, escolha o botão **OK** .

9. Na barra de menus, escolha **criar**  >  **solução de compilação**e, em seguida, certifique-se de que a solução seja compilada sem erros.

10. Verifique se a pasta de saída da compilação do projeto WebPartNode agora contém o arquivo WebPartNode. vsix.

     Por padrão, a pasta de saída da compilação é a.. pasta \bin\Debug sob a pasta que contém o arquivo de projeto.

## <a name="test-the-extension"></a>Testar a extensão
 Agora você está pronto para testar o novo nó **Galeria de Web Parts** em **Gerenciador de servidores**. Primeiro, comece a depurar o projeto de extensão em uma instância experimental do Visual Studio. Em seguida, use o novo nó **Web Parts** na instância experimental do Visual Studio.

#### <a name="to-start-debugging-the-extension"></a>Para iniciar a depuração da extensão

1. Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução **WebPartNode** .

2. No projeto WebPartNodeExtension, abra o arquivo de código **SiteNodeExtension** e, em seguida, adicione um ponto de interrupção às primeiras linhas de código nos `NodeChildrenRequested` `CreateWebPartNodes` métodos e.

3. Escolha a tecla **F5** para iniciar a depuração.

     O Visual Studio instala a extensão para a extensão de nó da galeria do%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Web Part para o servidor Explorer\1.0 e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.

#### <a name="to-test-the-extension"></a>Para testar a extensão

1. Na instância experimental do Visual Studio, na barra de menus, escolha **Exibir**  >  **Gerenciador de servidores**.

2. Verifique se o site do SharePoint que você deseja usar para teste aparece no nó **conexões do SharePoint** no **Gerenciador de servidores**. Se não estiver listado, siga estas etapas:

    1. Abra o menu de atalho para **conexões do SharePoint**e, em seguida, escolha **Adicionar conexão**.

    2. Na caixa de diálogo **Adicionar conexão do SharePoint** , digite a URL do site do SharePoint ao qual você deseja se conectar e escolha o botão **OK** .

         Para especificar o site do SharePoint no computador de desenvolvimento, digite **http://localhost** .

3. Expanda o nó conexão do site (que exibe a URL do seu site) e, em seguida, expanda um nó de site filho (por exemplo, **site de equipe**).

4. Verifique se o código na outra instância do Visual Studio é interrompido no ponto de interrupção que você definiu anteriormente no `NodeChildrenRequested` método e, em seguida, escolha a tecla **F5** para continuar a depurar o projeto.

5. Na instância experimental do Visual Studio, expanda o nó **Galeria de Web Parts** , que aparece sob o nó de site de nível superior.

6. Verifique se o código na outra instância do Visual Studio é interrompido no ponto de interrupção que você definiu anteriormente no `CreateWebPartNodes` método e, em seguida, escolha a tecla **F5** para continuar a depurar o projeto.

7. Na instância experimental do Visual Studio, verifique se todos os Web Parts no site conectado aparecem no nó Galeria de **Web Parts** no **Gerenciador de servidores**.

8. Abra o menu de atalho para uma Web Part e, em seguida, escolha **Propriedades**.

9. Na janela **Propriedades** , verifique se os detalhes sobre a Web Part são exibidos.

10. No **Gerenciador de servidores**, abra o menu de atalho para a mesma Web Part e escolha **Exibir mensagem**.

     Na caixa de mensagem exibida, escolha o botão **OK** .

## <a name="uninstall-the-extension-from-visual-studio"></a>Desinstalar a extensão do Visual Studio
 Depois de concluir o teste da extensão, desinstale-a do Visual Studio.

#### <a name="to-uninstall-the-extension"></a>Para desinstalar a extensão

1. Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas**  >  **extensões e atualizações**.

     A caixa de diálogo **Extensões e Atualizações** é aberta.

2. Na lista de extensões, escolha **nó da Galeria de Web Parts para Gerenciador de servidores**e, em seguida, escolha o botão **desinstalar** .

3. Na caixa de diálogo exibida, escolha o botão **Sim** .

4. Escolha o botão **reiniciar agora** para concluir a desinstalação.

     O item de projeto também é desinstalado.

5. Feche as duas instâncias do Visual Studio (a instância experimental e a instância do Visual Studio na qual a solução WebPartNode está aberta).

## <a name="see-also"></a>Consulte também
- [Chamar para os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md)
- [Estenda o nó conexões do SharePoint no Gerenciador de Servidores](../sharepoint/extending-the-sharepoint-connections-node-in-server-explorer.md)
- [Walkthrough: estender Gerenciador de Servidores para exibir Web Parts](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)
- [Editor de imagem para ícones](/cpp/windows/image-editor-for-icons)
- [Criando um ícone ou outro editor de imagem de &#40;de imagem para ícones&#41;](/cpp/windows/creating-an-icon-or-other-image-image-editor-for-icons)
