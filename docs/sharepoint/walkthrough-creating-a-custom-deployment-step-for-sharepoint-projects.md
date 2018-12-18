---
title: 'Passo a passo: Criando uma etapa de implantação para projetos do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands
- SharePoint development in Visual Studio, extending deployment
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: c74feaed6c108f9dcfb5f2b374a72c34526134b0
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51296145"
---
# <a name="walkthrough-create-a-custom-deployment-step-for-sharepoint-projects"></a>Passo a passo: Criar uma etapa de implantação para projetos do SharePoint
  Quando você implanta um projeto do SharePoint, o Visual Studio executa uma série de etapas de implantação em uma ordem específica. O Visual Studio inclui várias etapas de implantação interna, mas você também pode criar seus próprios.  
  
 Neste passo a passo, você criará uma etapa de implantação para atualizar soluções em um servidor que está executando o SharePoint. O Visual Studio inclui as etapas de implantação interna para muitas tarefas, tal Cancelando ou adição de soluções, mas ele não inclui uma etapa de implantação para atualização de soluções. Por padrão, quando você implanta uma solução do SharePoint, o Visual Studio pela primeira vez cancela a solução (se já estiver implantado) e, em seguida, reimplantar a solução inteira. Para obter mais informações sobre as etapas de implantação interna, consulte [implantar, publicar e atualizar pacotes de solução do SharePoint](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md).  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
-   Criando uma extensão do Visual Studio que executa duas tarefas principais:  
  
    -   A extensão define uma etapa de implantação para atualizar soluções do SharePoint.  
  
    -   A extensão cria uma extensão de projeto que define uma nova configuração de implantação, que é um conjunto de etapas de implantação que são executadas para um determinado projeto. A nova configuração de implantação inclui a etapa de implantação personalizada e várias etapas de implantação interna.  
  
-   Crie dois comandos do SharePoint personalizados que chama o assembly de extensão. Comandos do SharePoint são métodos que podem ser chamados por assemblies de extensão para usar APIs no modelo de objeto de servidor para o SharePoint. Para obter mais informações, consulte [chamam os modelos de objeto SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).  
  
-   Criando um pacote de extensão VSIX (Visual Studio) para implantar os assemblies.  
  
-   Teste a nova etapa de implantação.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passo:  
  
- Edições com suporte do Windows, SharePoint e Visual Studio.
  
- O SDK do Visual Studio. Este passo a passo usa o **VSIX Project** modelo no SDK para criar um pacote VSIX para implantar a extensão. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).  
  
  Conhecimento dos conceitos a seguir é útil, mas não necessário para concluir o passo a passo:  
  
- Usando o modelo de objeto de servidor para o SharePoint. Para obter mais informações, consulte [usando o modelo de objeto de servidor do SharePoint Foundation](http://go.microsoft.com/fwlink/?LinkId=177796).  
  
- Soluções do SharePoint. Para obter mais informações, consulte [visão geral das soluções](http://go.microsoft.com/fwlink/?LinkId=169422).  
  
- Atualizando soluções do SharePoint. Para obter mais informações, consulte [atualização de uma solução](http://go.microsoft.com/fwlink/?LinkId=177802).  
  
## <a name="create-the-projects"></a>Crie os projetos
 Para concluir este passo a passo, você deve criar três projetos:  
  
- Um projeto VSIX para criar o pacote VSIX para implantar a extensão.  
  
- Um projeto de biblioteca de classe que implementa a extensão. Este projeto deve ter como destino o .NET Framework 4.5.  
  
- Um projeto de biblioteca de classe que define os comandos do SharePoint personalizados. Este projeto deve ter como destino o .NET Framework 3.5.  
  
  Inicie o passo a passo Criando os projetos.  
  
#### <a name="to-create-the-vsix-project"></a>Para criar o projeto do VSIX  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
3.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha o **extensibilidade** nó.  
  
    > [!NOTE]  
    >  O **extensibilidade** o nó está disponível somente se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos no início deste tópico.  
  
4.  Na parte superior da caixa de diálogo, escolha **.NET Framework 4.5** na lista de versões do .NET Framework.  
  
5.  Escolha o **projeto VSIX** modelo, o nome do projeto **UpgradeDeploymentStep**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **UpgradeDeploymentStep** projeto ao **Gerenciador de soluções**.  
  
#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do nó da solução UpgradeDeploymentStep, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha o **Windows** nó.  
  
3.  Na parte superior da caixa de diálogo, escolha **.NET Framework 4.5** na lista de versões do .NET Framework.  
  
4.  Escolha o **biblioteca de classes** modelo de projeto, nomeie o projeto **DeploymentStepExtension**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **DeploymentStepExtension** projeto à solução e abre o arquivo de código padrão Class1.  
  
5.  Exclua o arquivo de código Class1 do projeto.  
  
#### <a name="to-create-the-sharepoint-command-project"></a>Para criar o projeto de comando do SharePoint  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do nó da solução UpgradeDeploymentStep, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda **Visual c#** ou **Visual Basic**e, em seguida, escolha o **Windows** nó.  
  
3.  Na parte superior da caixa de diálogo, escolha **.NET Framework 3.5** na lista de versões do .NET Framework.  
  
4.  Escolha o **biblioteca de classes** modelo de projeto, nomeie o projeto **SharePointCommands**e, em seguida, escolha o **Okey** botão.  
  
     O Visual Studio adiciona o **SharePointCommands** projeto à solução e abre o arquivo de código padrão Class1.  
  
5.  Exclua o arquivo de código Class1 do projeto.  
  
## <a name="configure-the-projects"></a>Configurar os projetos
 Antes de escrever código para criar a etapa de implantação personalizada, você deve adicionar arquivos de código e referências de assembly, e você deve configurar os projetos.  
  
#### <a name="to-configure-the-deploymentstepextension-project"></a>Para configurar o projeto DeploymentStepExtension
  
1.  No **DeploymentStepExtension** do projeto, adicione dois arquivos de código que têm os seguintes nomes:  
  
    -   UpgradeStep  
  
    -   DeploymentConfigurationExtension  
  
2.  Abra o menu de atalho no projeto DeploymentStepExtension e, em seguida, escolha **adicionar referência**.  
  
3.  Sobre o **Framework** guia, marque a caixa de seleção para o assembly Composition.  
  
4.  Sobre o **extensões** guia, marque a caixa de seleção para o assembly Microsoft.VisualStudio.SharePoint e, em seguida, escolha o **Okey** botão.  
  
#### <a name="to-configure-the-sharepointcommands-project"></a>Para configurar o projeto SharePointCommands
  
1.  No **SharePointCommands** do projeto, adicione um arquivo de código que é chamado de comandos.  
  
2.  Na **Gerenciador de soluções**, abra o menu de atalho na **SharePointCommands** nó do projeto e, em seguida, escolha **Add Reference**.  
  
3.  Sobre o **extensões** guia, marque as caixas de seleção para os assemblies a seguir e, em seguida, clique em escolher a **Okey** botão  
  
    -   Microsoft. SharePoint  
  
    -   Microsoft.VisualStudio.SharePoint.Commands  
  
## <a name="define-the-custom-deployment-step"></a>Definir a etapa de implantação personalizada
 Crie uma classe que define a etapa de implantação de atualização. Para definir a etapa da implantação, a classe implementa o <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> interface. Implemente essa interface sempre que você deseja definir uma etapa de implantação personalizada.  
  
#### <a name="to-define-the-custom-deployment-step"></a>Para definir a etapa de implantação personalizada  
  
1.  No **DeploymentStepExtension** do projeto, abra o arquivo de código UpgradeStep e, em seguida, cole o seguinte código nele.  
  
    > [!NOTE]  
    >  Depois que você adicionar esse código, o projeto terá alguns erros de compilação, mas eles desaparecem quando você adiciona código em etapas posteriores.  
  
     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#1](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs#1)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#1](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb#1)]  
  
## <a name="create-a-deployment-configuration-that-includes-the-custom-deployment-step"></a>Criar uma configuração de implantação que inclui a etapa de implantação personalizada
 Crie uma extensão de projeto para a nova configuração de implantação, que inclui várias etapas de implantação interna e a nova etapa de implantação de atualização. Ao criar essa extensão, você pode ajudar a desenvolvedores do SharePoint para usar a etapa de implantação de atualização em projetos do SharePoint.  
  
 Para criar a configuração de implantação, a classe implementa o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> interface. Implemente essa interface sempre que você deseja criar uma extensão de projeto do SharePoint.  
  
#### <a name="to-create-the-deployment-configuration"></a>Para criar a configuração de implantação  
  
1.  No **DeploymentStepExtension** do projeto, abra o arquivo de código DeploymentConfigurationExtension e, em seguida, cole o seguinte código nele.  
  
     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#2](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/deploymentconfigurationextension.cs#2)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#2](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/deploymentconfigurationextension.vb#2)]  
  
## <a name="create-the-custom-sharepoint-commands"></a>Criar os comandos do SharePoint personalizados
 Crie dois comandos personalizados que chamam o modelo de objeto de servidor para o SharePoint. Um comando determina se uma solução já está implantada; outro comando atualiza uma solução.  
  
#### <a name="to-define-the-sharepoint-commands"></a>Para definir os comandos do SharePoint  
  
1.  No **SharePointCommands** do projeto, abra o arquivo de código de comandos e, em seguida, cole o seguinte código nele.  
  
     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#4](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs#4)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#4](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb#4)]  
  
## <a name="checkpoint"></a>Ponto de verificação  
 Neste momento no passo a passo, todo o código para a etapa de implantação personalizada e os comandos do SharePoint agora estão nos projetos. Criá-los para certificar-se de que eles são compilados sem erros.  
  
#### <a name="to-build-the-projects"></a>Para compilar projetos  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **DeploymentStepExtension** do projeto e, em seguida, escolha **Build**.  
  
2.  Abra o menu de atalho para o **SharePointCommands** do projeto e, em seguida, escolha **Build**.  
  
## <a name="create-a-vsix-package-to-deploy-the-extension"></a>Criar um pacote VSIX para implantar a extensão
 Para implantar a extensão, use o projeto do VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo vsixmanifest no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.  
  
#### <a name="to-configure-and-create-the-vsix-package"></a>Para configurar e criar o pacote VSIX  
  
1.  No **Gerenciador de soluções**, sob o **UpgradeDeploymentStep** do projeto, abra o menu de atalho para o **vsixmanifest** file e, em seguida, escolha  **Abra**.  
  
     Visual Studio abre o arquivo no editor de manifesto. O arquivo vsixmanifest é a base para o arquivo Extension vsixmanifest que exigem todos os pacotes VSIX. Para obter mais informações sobre esse arquivo, consulte [1.0 referência do esquema de extensão do VSIX](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).  
  
2.  No **nome do produto** , digite **atualizar a etapa de implantação para projetos do SharePoint**.  
  
3.  No **autor** , digite **Contoso**.  
  
4.  No **descrição** , digite **fornece uma etapa de implantação de atualização personalizada que pode ser usada em projetos do SharePoint**.  
  
5.  No **ativos** guia do editor, escolha a **New** botão.  
  
     O **adicionar novo ativo** caixa de diálogo é exibida.  
  
6.  No **tipo** , escolha **mefcomponent**.  
  
    > [!NOTE]  
    >  Esse valor corresponde à `MefComponent` elemento no arquivo Extension vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [MEFComponent Element (esquema de VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).  
  
7.  No **fonte** , escolha **um projeto na solução atual**.  
  
8.  No **Project** , escolha **DeploymentStepExtension**e, em seguida, escolha o **Okey** botão.  
  
9. No editor de manifesto, escolha o **New** novamente no botão.  
  
     O **adicionar novo ativo** caixa de diálogo é exibida.  
  
10. No **tipo** , digite **SharePoint.Commands.v4**.  
  
    > [!NOTE]  
    >  Esse elemento Especifica uma extensão personalizada que você deseja incluir na extensão do Visual Studio. Para obter mais informações, consulte [ativo Element (esquema de VSX)](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737).  
  
11. No **fonte** , escolha **um projeto na solução atual**.  
  
12. No **Project** , escolha **SharePointCommands**e, em seguida, escolha o **Okey** botão.  
  
13. Na barra de menus, escolha **construir** > **compilar solução**e, em seguida, certifique-se de que a solução é compilado sem erros.  
  
14. Certifique-se de que a pasta de saída de compilação para o projeto UpgradeDeploymentStep agora contém o arquivo UpgradeDeploymentStep.vsix.  
  
     Por padrão, a pasta de saída de compilação é o... pasta \bin\debug sob a pasta que contém seu arquivo de projeto.  
  
## <a name="prepare-to-test-the-upgrade-deployment-step"></a>Prepare-se para a etapa de implantação de atualização de teste
 Para testar a etapa de implantação de atualização, você deve primeiro implantar uma solução de exemplo no site do SharePoint. Comece a depuração da extensão na instância experimental do Visual Studio. Em seguida, crie uma definição de lista e a instância de lista a ser usada para testar a etapa de implantação e, em seguida, implantá-los para o site do SharePoint. Em seguida, modifique a definição de lista e a instância de lista e reimplantá-los para demonstrar como o processo de implantação padrão substitui as soluções no site do SharePoint.  
  
 Posteriormente neste passo a passo, você modificará a definição de lista e a instância de lista e, em seguida, você irá atualizá-los no site do SharePoint.  
  
#### <a name="to-start-debugging-the-extension"></a>Para iniciar a extensão de depuração  
  
1.  Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução de UpgradeDeploymentStep.  
  
2.  No projeto DeploymentStepExtension, abra o arquivo de código UpgradeStep e, em seguida, adicione um ponto de interrupção para a primeira linha de código na `CanExecute` e `Execute` métodos.  
  
3.  Iniciar a depuração, escolhendo a **F5** chave ou, na barra de menus, escolhendo **Debug** > **iniciar depuração**.  
  
4.  Visual Studio instala a extensão para %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Upgrade etapa de implantação para o SharePoint Projects\1.0 e inicia uma instância experimental do Visual Studio. Você vai testar a etapa de implantação de atualização nesta instância do Visual Studio.  
  
#### <a name="to-create-a-sharepoint-project-with-a-list-definition-and-a-list-instance"></a>Para criar um projeto do SharePoint com uma definição de lista e uma instância de lista  
  
1. Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo** > **New** > **projeto**.  
  
2. No **novo projeto** diálogo caixa, expanda o **Visual c#** nó ou o **Visual Basic** nó, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
3. Na parte superior da caixa de diálogo, verifique se **.NET Framework 3.5** aparece na lista de versões do .NET Framework.  
  
    Projetos para [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] e [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] exigem esta versão do .NET Framework.  
  
4. Na lista de modelos de projeto, escolha **projeto do SharePoint 2010**, nomeie o projeto **EmployeesListDefinition**e, em seguida, escolha o **Okey** botão.  
  
5. No **Assistente para personalização do SharePoint**, insira a URL do site que você deseja usar para depuração.  
  
6. Sob **qual é o nível de confiança para essa solução do SharePoint**, escolha o **implantar como uma solução de farm** botão de opção.  
  
   > [!NOTE]  
   >  A etapa de implantação de atualização não oferece suporte a soluções em área restrita.  
  
7. Escolha o **concluir** botão.  
  
    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o projeto EmployeesListDefinition.  
  
8. Abra o menu de atalho para o projeto EmployeesListDefinition, escolha **Add**e, em seguida, escolha **Novo Item**.  
  
9. No **Adicionar Novo Item – EmployeesListDefinition** diálogo caixa, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
10. Escolha o **lista** modelo de item, o nome do item **lista de funcionários**e, em seguida, escolha o **Add** botão.  
  
     O Assistente para personalização do SharePoint é exibida  
  
11. Sobre o **escolher as configurações da lista** página, verifique as seguintes configurações e, em seguida, escolha o **concluir** botão:  
  
    1. **Lista de funcionários** aparece na **que nome você deseja exibir para sua lista?** caixa.  
  
    2. O **criar uma lista personalizável com base em:** botão de opção é escolhida.  
  
    3. **Padrão (em branco)** é escolhido na **criar uma lista personalizável com base em:** lista.  
  
       [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] cria o item de lista de funcionários com uma coluna de título e uma única instância vazia e abre o Designer de lista.  
  
12. No Designer de lista, na **colunas** guia, escolha o **digite um nome de coluna novo ou existente** linha e, em seguida, adicione as seguintes colunas no **nome de exibição da coluna** lista:  
  
    1.  Nome  
  
    2.  Empresa  
  
    3.  Telefone comercial  
  
    4.  Email  
  
13. Salve todos os arquivos e, em seguida, feche o Designer de lista.  
  
14. Na **Gerenciador de soluções**, expanda o **lista de funcionários** nó e, em seguida, expanda o **instância de lista de funcionários** nó filho.  
  
15. No *Elements. XML* de arquivo, substitua o padrão XML neste arquivo pelo XML a seguir. Esse XML altera o nome da lista para **funcionários** e adiciona informações de um funcionário que possui chamada Jim Hance.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8"?>  
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">  
      <ListInstance Title="Employees"  
                    OnQuickLaunch="TRUE"  
                    TemplateType="10000"  
                    Url="Lists/Employees"  
                    Description="Simple list to test upgrade deployment step">  
        <Data>  
          <Rows>  
            <Row>  
              <Field Name="Title">Hance</Field>  
              <Field Name="FirstName">Jim</Field>  
              <Field Name="Company">Contoso</Field>  
              <Field Name="Business Phone">555-555-5555</Field>  
              <Field Name="E-Mail">jim@contoso.com</Field>  
            </Row>  
          </Rows>  
        </Data>  
      </ListInstance>  
    </Elements>  
    ```  
  
16. Salve e feche o *Elements. XML* arquivo.  
  
17. Abra o menu de atalho para o projeto EmployeesListDefinition e, em seguida, escolha **aberto** ou **propriedades**.  
  
     O Designer de propriedades é aberta.  
  
18. Sobre o **SharePoint** guia, desmarque a **retração automática após a depuração** caixa de seleção e, em seguida, salvar as propriedades.  
  
#### <a name="to-deploy-the-list-definition-and-list-instance"></a>Para implantar a definição de lista e instância de lista  
  
1.  Na **Gerenciador de soluções**, escolha o **EmployeesListDefinition** nó do projeto.  
  
2.  No **propriedades** janela, certifique-se de que o **configuração de implantação ativa** estiver definida como **padrão**.  
  
3.  Escolha o **F5** da chave ou, na barra de menus, escolha **Debug** > **iniciar depuração**.  
  
4.  Verifique se o projeto é compilado com êxito, o que o navegador da web abre o site do SharePoint, que o **listas** inclui o novo item na barra de início rápido **funcionários** lista e que o  **Os funcionários** lista inclui a entrada para Jim Hance.  
  
5.  Feche o navegador da Web.  
  
#### <a name="to-modify-the-list-definition-and-list-instance-and-redeploy-them"></a>Para modificar a definição de lista e a instância de lista e reimplantá-los  
  
1.  No projeto EmployeesListDefinition, abra o *Elements. XML* arquivo que é um filho do **instância de lista de funcionários** item de projeto.  
  
2.  Remover o `Data` elemento e seus filhos para remover a entrada para Jim Hance na lista.  
  
     Quando você terminar, o arquivo deve conter o XML a seguir.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8"?>  
    <Elements xmlns="http://schemas.microsoft.com/sharepoint/">  
      <ListInstance Title="Employees"  
                    OnQuickLaunch="TRUE"  
                    TemplateType="10000"  
                    Url="Lists/Employees"  
                    Description="Simple list to test upgrade deployment step">  
      </ListInstance>  
    </Elements>  
    ```  
  
3.  Salve e feche o *Elements. XML* arquivo.  
  
4.  Abra o menu de atalho para o **lista de funcionários** de item de projeto e, em seguida, escolha **abra** ou **propriedades**.  
  
5.  No Designer de lista, escolha o **modos de exibição** guia.  
  
6.  No **colunas selecionadas** , escolha **anexos**e, em seguida, escolha o < a chave para mover essa coluna para o **colunas disponíveis** lista.  
  
7.  Repita a etapa anterior para mover o **telefone comercial** coluna a partir de **colunas selecionadas** lista para o **colunas disponíveis** lista.  
  
     Esta ação remove esses campos do modo de exibição padrão de **funcionários** lista no site do SharePoint.  
  
8.  Iniciar a depuração, escolhendo a **F5** chave ou, na barra de menus, escolhendo **Debug** > **iniciar depuração**.  
  
9. Verifique se que o **conflitos de implantação** caixa de diálogo é exibida.  
  
     Essa caixa de diálogo aparece quando o Visual Studio tenta implantar uma solução (a instância de lista) para um site do SharePoint ao qual essa solução já foi implantada. Essa caixa de diálogo não aparecerá quando você executar a etapa de implantação de atualização mais adiante neste passo a passo.  
  
10. No **conflitos de implantação** diálogo caixa, escolha o **resolver automaticamente** botão de opção.  
  
     Visual Studio exclui a instância de lista no site do SharePoint, implanta o item de lista no projeto e, em seguida, abre o site do SharePoint.  
  
11. No **listas** seção da barra de início rápido, escolha o **funcionários** lista e, em seguida, verifique se os detalhes a seguir:  
  
    -   O **anexos** e **telefone residencial** colunas não são exibidos neste modo de exibição da lista.  
  
    -   A lista está vazia. Quando você usou o **padrão** configuração de implantação para reimplantar a solução, o **funcionários** lista foi substituída com a nova lista vazia em seu projeto.  
  
## <a name="test-the-deployment-step"></a>A etapa de implantação de teste
 Agora você está pronto para testar a etapa de implantação de atualização. Primeiro, adicione um item para a instância de lista no SharePoint. Em seguida, altere a definição de lista e a instância de lista, atualizá-los no site do SharePoint e confirmar que a etapa de implantação de atualização não substitui o novo item.  
  
#### <a name="to-manually-add-an-item-to-the-list"></a>Para adicionar manualmente um item à lista  
  
1.  Na faixa de opções no site do SharePoint, sob o **ferramentas de lista** guia, escolha o **itens** guia.  
  
2.  No **New** grupo, escolha **Novo Item**.  
  
     Como alternativa, você pode escolher o **adicionar novo item** link na lista de item em si.  
  
3.  No **funcionários - Novo Item** janela, no **título** , digite **gerente de instalações**.  
  
4.  No **First Name** , digite **Andy**.  
  
5.  No **empresa** , digite **Contoso**.  
  
6.  Escolha o **salvar** botão, verifique se o novo item aparece na lista e, em seguida, feche o navegador da web.  
  
     Posteriormente neste passo a passo, você usará este item para verificar que a etapa de implantação de atualização não substitui o conteúdo desta lista.  
  
#### <a name="to-test-the-upgrade-deployment-step"></a>Para testar a etapa de implantação de atualização  
  
1. Na instância experimental do Visual Studio, no **Gerenciador de soluções**, abra o menu de atalho para o **EmployeesListDefinition** nó do projeto e, em seguida, escolha **propriedades**.  
  
    O Designer/Editor de propriedades é aberta.  
  
2. Sobre o **SharePoint** guia, defina o **configuração de implantação ativa** propriedade a ser **atualizar**.  
  
    Essa configuração de implantação personalizado inclui a nova etapa de implantação de atualização.  
  
3. Abra o menu de atalho para o **lista de funcionários** de item de projeto e, em seguida, escolha **propriedades** ou **abrir**.  
  
    O Designer/Editor de propriedades é aberta.  
  
4. No **modos de exibição** guia, escolha o **email** coluna e, em seguida, escolha o **<** tecla para mover essa coluna do **selecionado colunas**listar para o **colunas disponíveis** lista.  
  
    Esta ação remove esses campos do modo de exibição padrão de **funcionários** lista no site do SharePoint.  
  
5. Iniciar a depuração, escolhendo a **F5** chave ou, na barra de menus, escolhendo **Debug** > **iniciar depuração**.  
  
6. Verifique se o código em outra instância do Visual Studio para no ponto de interrupção que você definiu anteriormente no `CanExecute` método.  
  
7. Escolha o **F5** novamente da chave ou, na barra de menus, escolha **Debug** > **continuar**.  
  
8. Verifique se o código para no ponto de interrupção que você definiu anteriormente no `Execute` método.  
  
9. Escolha o **F5** da chave ou, na barra de menus, escolha **Debug** > **continuar** uma última vez.  
  
     O navegador da web abre o site do SharePoint.  
  
10. No **listas** seção da área de início rápido, escolha o **funcionários** lista e, em seguida, verifique se os detalhes a seguir:  
  
    - O item que você adicionou manualmente anteriormente (por Andy, o Gerenciador de recursos) é ainda na lista.  
  
    - O **telefone comercial** e **endereço de email** colunas não são exibidos neste modo de exibição da lista.  
  
      O **Upgrade** configuração de implantação modifica existente **funcionários** instância de lista no site do SharePoint. Se você tiver usado o **padrão** configuração de implantação, em vez da **atualizar** configuração, você deve encontrar um conflito de implantação. Visual Studio deve resolver o conflito, substituindo o **funcionários** lista e o item de Andy, o Gerenciador de recursos seriam excluídos.  
  
## <a name="clean-up-the-development-computer"></a>Limpar o computador de desenvolvimento
 Após concluir o teste a etapa de implantação de atualização, remova a instância de lista e a definição de lista do site do SharePoint e remover a extensão de etapa de implantação do Visual Studio.  
  
#### <a name="to-remove-the-list-instance-from-the-sharepoint-site"></a>Para remover a instância de lista do site do SharePoint  
  
1.  Abra o **funcionários** lista no site do SharePoint, se a lista não estiver aberta.  
  
2.  Na faixa de opções no site do SharePoint, escolha o **ferramentas de lista** guia e, em seguida, escolha o **lista** guia.  
  
3.  No **as configurações** grupo, escolha o **as configurações da lista** item.  
  
4.  Sob **permissões e gerenciamento**, escolha o **excluir esta lista** de comando, escolha **Okey** para confirmar que você deseja enviar a lista para a Lixeira e, em seguida, feche a web Navegador.  
  
#### <a name="to-remove-the-list-definition-from-the-sharepoint-site"></a>Para remover a definição de lista do site do SharePoint  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **construir** > **Retract**.  
  
     Visual Studio cancela a definição de lista do site do SharePoint.  
  
#### <a name="to-uninstall-the-extension"></a>Para desinstalar a extensão  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas** > **extensões e atualizações**.  
  
     A caixa de diálogo **Extensões e Atualizações** é aberta.  
  
2.  Na lista de extensões, escolha **atualizar a etapa de implantação para projetos do SharePoint**e, em seguida, escolha o **desinstalar** comando.  
  
3.  Na caixa de diálogo que aparece, escolha **Yes** para confirmar que você deseja desinstalar a extensão e, em seguida, escolha **reiniciar agora** para concluir a desinstalação.  
  
4.  Feche ambas as instâncias do Visual Studio (a instância experimental e a instância do Visual Studio em que a solução UpgradeDeploymentStep estiver aberta).  
  
## <a name="see-also"></a>Consulte também
 [Estender o SharePoint empacotamento e implantação](../sharepoint/extending-sharepoint-packaging-and-deployment.md)  
  
