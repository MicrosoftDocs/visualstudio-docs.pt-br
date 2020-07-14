---
title: Criar etapa de implantação personalizada para projetos do SharePoint
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint commands
- SharePoint development in Visual Studio, extending deployment
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 56fac2be1e73de5df9da8aa13e6631c4cc9d1022
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015889"
---
# <a name="walkthrough-create-a-custom-deployment-step-for-sharepoint-projects"></a>Walkthrough: criar uma etapa de implantação personalizada para projetos do SharePoint
  Quando você implanta um projeto do SharePoint, o Visual Studio executa uma série de etapas de implantação em uma ordem específica. O Visual Studio inclui muitas etapas de implantação internas, mas você também pode criar as suas próprias.

 Neste tutorial, você criará uma etapa de implantação personalizada para atualizar soluções em um servidor que está executando o SharePoint. O Visual Studio inclui etapas de implantação internas para muitas tarefas, como cancelando ou adicionando soluções, mas não inclui uma etapa de implantação para atualizar soluções. Por padrão, quando você implanta uma solução do SharePoint, o Visual Studio primeiro cancela a solução (se ela já estiver implantada) e, em seguida, reimplanta a solução inteira. Para obter mais informações sobre as etapas de implantação internas, consulte [implantar, publicar e atualizar pacotes de solução do SharePoint](../sharepoint/deploying-publishing-and-upgrading-sharepoint-solution-packages.md).

 Este tutorial demonstra as seguintes tarefas:

- Criar uma extensão do Visual Studio que executa duas tarefas principais:

  - A extensão define uma etapa de implantação personalizada para atualizar soluções do SharePoint.

  - A extensão cria uma extensão de projeto que define uma nova configuração de implantação, que é um conjunto de etapas de implantação que são executadas para um determinado projeto. A nova configuração de implantação inclui a etapa de implantação personalizada e várias etapas de implantação internas.

- Crie dois comandos personalizados do SharePoint que o assembly de extensão chama. Os comandos do SharePoint são métodos que podem ser chamados por assemblies de extensão para usar APIs no modelo de objeto de servidor para SharePoint. Para obter mais informações, consulte [chamar os modelos de objeto do SharePoint](../sharepoint/calling-into-the-sharepoint-object-models.md).

- Criando um pacote de VSIX (Visual Studio Extension) para implantar os dois assemblies.

- Testando a nova etapa de implantação.

## <a name="prerequisites"></a>Pré-requisitos
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passos:

- Edições com suporte do Windows, SharePoint e Visual Studio.

- O SDK do Visual Studio. Este tutorial usa o modelo de **projeto VSIX** no SDK para criar um pacote VSIX para implantar a extensão. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).

  O conhecimento dos seguintes conceitos é útil, mas não é necessário, para concluir o passo a passos:

- Usando o modelo de objeto de servidor para SharePoint. Para obter mais informações, consulte [usando o modelo de objeto do SharePoint Foundation Server](/previous-versions/office/developer/sharepoint-2010/ee538251(v=office.14)).

- Soluções do SharePoint. Para obter mais informações, consulte [visão geral de soluções](/previous-versions/office/developer/sharepoint-2010/aa543214(v=office.14)).

- Atualizando soluções do SharePoint. Para obter mais informações, consulte [atualizando uma solução](/previous-versions/office/developer/sharepoint-2010/aa543659(v=office.14)).

## <a name="create-the-projects"></a>Criar os projetos
 Para concluir este passo a passos, você deve criar três projetos:

- Um projeto VSIX para criar o pacote VSIX para implantar a extensão.

- Um projeto de biblioteca de classes que implementa a extensão. Este projeto deve ter como destino o .NET Framework 4,5.

- Um projeto de biblioteca de classes que define os comandos personalizados do SharePoint. Este projeto deve ter como destino o .NET Framework 3,5.

  Inicie o passo a passos criando os projetos.

#### <a name="to-create-the-vsix-project"></a>Para criar o projeto VSIX

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

3. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha o nó **extensibilidade** .

    > [!NOTE]
    > O nó **extensibilidade** só estará disponível se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos anteriormente neste tópico.

4. Na parte superior da caixa de diálogo, escolha **.NET Framework 4,5** na lista de versões do .NET Framework.

5. Escolha o modelo de **projeto VSIX** , nomeie o projeto **UpgradeDeploymentStep**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **UpgradeDeploymentStep** ao **Gerenciador de soluções**.

#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução UpgradeDeploymentStep, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha o nó **Windows** .

3. Na parte superior da caixa de diálogo, escolha **.NET Framework 4,5** na lista de versões do .NET Framework.

4. Escolha o modelo de projeto de **biblioteca de classes** , nomeie o projeto **DeploymentStepExtension**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **DeploymentStepExtension** à solução e abre o arquivo de código de Class1 padrão.

5. Exclua o arquivo de código Class1 do projeto.

#### <a name="to-create-the-sharepoint-command-project"></a>Para criar o projeto de comando do SharePoint

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução UpgradeDeploymentStep, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na caixa de diálogo **novo projeto** , expanda **Visual C#** ou **Visual Basic**e, em seguida, escolha o nó **Windows** .

3. Na parte superior da caixa de diálogo, escolha **.NET Framework 3,5** na lista de versões do .NET Framework.

4. Escolha o modelo de projeto de **biblioteca de classes** , nomeie o projeto **SharePointCommands**e, em seguida, escolha o botão **OK** .

     O Visual Studio adiciona o projeto **SharePointCommands** à solução e abre o arquivo de código de Class1 padrão.

5. Exclua o arquivo de código Class1 do projeto.

## <a name="configure-the-projects"></a>Configurar os projetos
 Antes de escrever o código para criar a etapa de implantação personalizada, você deve adicionar arquivos de código e referências de assembly e deve configurar os projetos.

#### <a name="to-configure-the-deploymentstepextension-project"></a>Para configurar o projeto DeploymentStepExtension

1. No projeto **DeploymentStepExtension** , adicione dois arquivos de código que têm os seguintes nomes:

    - UpgradeStep

    - DeploymentConfigurationExtension

2. Abra o menu de atalho no projeto DeploymentStepExtension e escolha **Adicionar referência**.

3. Na guia **estrutura** , marque a caixa de seleção do assembly System. ComponentModel. composição.

4. Na guia **extensões** , marque a caixa de seleção do assembly Microsoft. VisualStudio. SharePoint e, em seguida, escolha o botão **OK** .

#### <a name="to-configure-the-sharepointcommands-project"></a>Para configurar o projeto SharePointCommands

1. No projeto **SharePointCommands** , adicione um arquivo de código chamado comandos.

2. No **Gerenciador de soluções**, abra o menu de atalho no nó do projeto **SharePointCommands** e escolha **Adicionar referência**.

3. Na guia **extensões** , marque as caixas de seleção dos seguintes assemblies e clique em escolher o botão **OK**

    - Microsoft. SharePoint

    - Microsoft. VisualStudio. SharePoint. Commands

## <a name="define-the-custom-deployment-step"></a>Definir a etapa de implantação personalizada
 Crie uma classe que define a etapa de implantação de atualização. Para definir a etapa de implantação, a classe implementa a <xref:Microsoft.VisualStudio.SharePoint.Deployment.IDeploymentStep> interface. Implemente essa interface sempre que desejar definir uma etapa de implantação personalizada.

#### <a name="to-define-the-custom-deployment-step"></a>Para definir a etapa de implantação personalizada

1. No projeto **DeploymentStepExtension** , abra o arquivo de código UpgradeStep e cole o código a seguir nele.

    > [!NOTE]
    > Depois de adicionar esse código, o projeto terá alguns erros de compilação, mas eles desaparecerão quando você adicionar código em etapas posteriores.

     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#1](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/upgradestep.cs#1)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#1](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/upgradestep.vb#1)]

## <a name="create-a-deployment-configuration-that-includes-the-custom-deployment-step"></a>Criar uma configuração de implantação que inclui a etapa de implantação personalizada
 Crie uma extensão de projeto para a nova configuração de implantação, que inclui várias etapas de implantação internas e a nova etapa de implantação de atualização. Ao criar essa extensão, você ajuda os desenvolvedores do SharePoint a usar a etapa de implantação de atualização em projetos do SharePoint.

 Para criar a configuração de implantação, a classe implementa a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> interface. Implemente essa interface sempre que desejar criar uma extensão de projeto do SharePoint.

#### <a name="to-create-the-deployment-configuration"></a>Para criar a configuração de implantação

1. No projeto **DeploymentStepExtension** , abra o arquivo de código DeploymentConfigurationExtension e cole o código a seguir nele.

     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#2](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/deploymentstepextension/deploymentconfigurationextension.cs#2)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#2](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/deploymentstepextension/deploymentconfigurationextension.vb#2)]

## <a name="create-the-custom-sharepoint-commands"></a>Criar os comandos personalizados do SharePoint
 Crie dois comandos personalizados que chamam o modelo de objeto do servidor para SharePoint. Um comando determina se uma solução já está implantada; o outro comando atualiza uma solução.

#### <a name="to-define-the-sharepoint-commands"></a>Para definir os comandos do SharePoint

1. No projeto **SharePointCommands** , abra o arquivo de código de comandos e cole o código a seguir nele.

     [!code-csharp[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#4](../sharepoint/codesnippet/CSharp/UpgradeDeploymentStep/SharePointCommands/Commands.cs#4)]
     [!code-vb[SPExtensibility.ProjectExtension.UpgradeDeploymentStep#4](../sharepoint/codesnippet/VisualBasic/upgradedeploymentstep/sharepointcommands/commands.vb#4)]

## <a name="checkpoint"></a>Ponto de verificação
 Neste ponto do passo a passo, todo o código para a etapa de implantação personalizada e os comandos do SharePoint agora estão nos projetos. Crie-os para garantir que eles sejam compilados sem erros.

#### <a name="to-build-the-projects"></a>Para compilar os projetos

1. No **Gerenciador de soluções**, abra o menu de atalho para o projeto **DeploymentStepExtension** e escolha **Compilar**.

2. Abra o menu de atalho para o projeto **SharePointCommands** e escolha **Compilar**.

## <a name="create-a-vsix-package-to-deploy-the-extension"></a>Criar um pacote VSIX para implantar a extensão
 Para implantar a extensão, use o projeto VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo Source. Extension. vsixmanifest no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.

#### <a name="to-configure-and-create-the-vsix-package"></a>Para configurar e criar o pacote VSIX

1. No **Gerenciador de soluções**, no projeto **UpgradeDeploymentStep** , abra o menu de atalho para o arquivo **Source. Extension. vsixmanifest** e, em seguida, escolha **abrir**.

     O Visual Studio abre o arquivo no editor de manifesto. O arquivo Source. Extension. vsixmanifest é a base para o arquivo extension. vsixmanifest que todos os pacotes VSIX exigem. Para obter mais informações sobre esse arquivo, consulte [referência do esquema de extensão do VSIX 1,0](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).

2. Na caixa **nome do produto** , digite **etapa de implantação de atualização para projetos do SharePoint**.

3. Na caixa **autor** , digite **contoso**.

4. Na caixa **Descrição** , digite **fornece uma etapa de implantação de atualização personalizada que pode ser usada em projetos do SharePoint**.

5. Na guia **ativos** do editor, escolha o botão **novo** .

     A caixa de diálogo **Adicionar novo ativo** é exibida.

6. Na lista **tipo** , escolha **Microsoft. VisualStudio. MefComponent**.

    > [!NOTE]
    > Esse valor corresponde ao `MefComponent` elemento no arquivo extension. vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [elemento MEFComponent (esquema VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).

7. Na lista **origem** , escolha **um projeto na solução atual**.

8. Na lista **projeto** , escolha **DeploymentStepExtension**e, em seguida, escolha o botão **OK** .

9. No editor de manifesto, escolha o botão **novo** novamente.

     A caixa de diálogo **Adicionar novo ativo** é exibida.

10. Na lista **tipo** , digite **SharePoint. Commands. v4**.

    > [!NOTE]
    > Esse elemento Especifica uma extensão personalizada que você deseja incluir na extensão do Visual Studio. Para obter mais informações, consulte [elemento Asset (esquema VSX)](https://msdn.microsoft.com/9fcfc098-edc7-484b-9d4c-acd17829d737).

11. Na lista **origem** , escolha **um projeto na solução atual**.

12. Na lista **projeto** , escolha **SharePointCommands**e, em seguida, escolha o botão **OK** .

13. Na barra de menus, escolha **criar**  >  **solução de compilação**e, em seguida, certifique-se de que a solução seja compilada sem erros.

14. Verifique se a pasta de saída da compilação do projeto UpgradeDeploymentStep agora contém o arquivo UpgradeDeploymentStep. vsix.

     Por padrão, a pasta de saída da compilação é a.. pasta \bin\Debug sob a pasta que contém o arquivo de projeto.

## <a name="prepare-to-test-the-upgrade-deployment-step"></a>Preparar para testar a etapa de implantação de atualização
 Para testar a etapa de implantação de atualização, você deve primeiro implantar uma solução de exemplo no site do SharePoint. Comece Depurando a extensão na instância experimental do Visual Studio. Em seguida, crie uma definição de lista e uma instância de lista para usar para testar a etapa de implantação e, em seguida, implante-as no site do SharePoint. Em seguida, modifique a definição da lista e a instância da lista e reimplante-as para demonstrar como o processo de implantação padrão substitui soluções no site do SharePoint.

 Mais adiante neste tutorial, você modificará a definição da lista e a instância da lista e, em seguida, as atualizará no site do SharePoint.

#### <a name="to-start-debugging-the-extension"></a>Para iniciar a depuração da extensão

1. Reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução UpgradeDeploymentStep.

2. No projeto DeploymentStepExtension, abra o arquivo de código UpgradeStep e, em seguida, adicione um ponto de interrupção à primeira linha de código nos `CanExecute` `Execute` métodos e.

3. Inicie a depuração escolhendo a tecla **F5** ou, na barra de menus, escolhendo **depurar**  >  **Iniciar Depuração**.

4. O Visual Studio instala a extensão para a etapa de implantação%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Upgrade para o SharePoint Projects\1.0 e inicia uma instância experimental do Visual Studio. Você testará a etapa de implantação de atualização nesta instância do Visual Studio.

#### <a name="to-create-a-sharepoint-project-with-a-list-definition-and-a-list-instance"></a>Para criar um projeto do SharePoint com uma definição de lista e uma instância de lista

1. Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Na caixa de diálogo **novo projeto** , expanda o nó do **Visual C#** ou o nó **Visual Basic** , expanda o nó **SharePoint** e escolha o nó **2010** .

3. Na parte superior da caixa de diálogo, verifique se **.NET Framework 3,5** aparece na lista de versões do .NET Framework.

    Projetos para [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] e [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] exigem esta versão do .NET Framework.

4. Na lista de modelos de projeto, escolha **projeto do SharePoint 2010**, nomeie o projeto **EmployeesListDefinition**e, em seguida, escolha o botão **OK** .

5. No **Assistente para personalização do SharePoint**, insira a URL do site que você deseja usar para depuração.

6. Em **qual é o nível de confiança para esta solução do SharePoint**, escolha o botão de opção **implantar como uma solução de farm** .

   > [!NOTE]
   > A etapa de implantação de atualização não dá suporte a soluções em área restrita.

7. Escolha o botão **Concluir**.

    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]cria o projeto EmployeesListDefinition.

8. Abra o menu de atalho para o projeto EmployeesListDefinition, escolha **Adicionar**e, em seguida, escolha **novo item**.

9. Na caixa de diálogo **Adicionar novo item-EmployeesListDefinition** , expanda o nó do **SharePoint** e escolha o nó **2010** .

10. Escolha o modelo de item de **lista** , nomeie a **lista de funcionários**do item e, em seguida, escolha o botão **Adicionar** .

     O assistente para personalização do SharePoint é exibido

11. Na página **escolher configurações da lista** , verifique as seguintes configurações e, em seguida, escolha o botão **concluir** :

    1. A **lista de funcionários** aparece na caixa **o que nome você deseja exibir para sua lista?** .

    2. O botão de opção **criar uma lista personalizável com base em:** é escolhido.

    3. **Padrão (em branco)** é escolhido na lista **criar uma lista personalizável baseada em:** .

       [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]cria o item de lista Employees com uma coluna Title e uma única instância vazia e abre o designer de lista.

12. No designer de lista, na guia **colunas** , escolha a linha **digite um nome de coluna novo ou existente** e, em seguida, adicione as seguintes colunas na lista **nome de exibição da coluna** :

    1. Nome

    2. Empresa

    3. Telefone comercial

    4. Email

13. Salve todos os arquivos e, em seguida, feche o designer de lista.

14. Em **Gerenciador de soluções**, expanda o nó **lista de funcionários** e, em seguida, expanda o nó filho da instância da **lista de funcionários** .

15. No arquivo *Elements.xml* , substitua o XML padrão neste arquivo pelo XML a seguir. Esse XML altera o nome da lista para **Employees** e adiciona informações para um funcionário chamado Jim Hance.

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

16. Salve e feche o arquivo *Elements.xml* .

17. Abra o menu de atalho para o projeto EmployeesListDefinition e, em seguida, escolha **abrir** ou **Propriedades**.

     O designer de propriedades é aberto.

18. Na guia **SharePoint** , desmarque a caixa de seleção **Cancelar automaticamente após a depuração** e, em seguida, salve as propriedades.

#### <a name="to-deploy-the-list-definition-and-list-instance"></a>Para implantar a definição de lista e a instância de lista

1. Em **Gerenciador de soluções**, escolha o nó do projeto **EmployeesListDefinition** .

2. Na janela **Propriedades** , verifique se a propriedade **configuração de implantação ativa** está definida como **padrão**.

3. Escolha a tecla **F5** ou, na barra de menus, escolha **depurar**  >  **Iniciar Depuração**.

4. Verifique se o projeto é compilado com êxito, se o navegador da Web abre no site do SharePoint, se o item **listas** na barra de início rápido inclui a nova lista **Employees** e se a lista **Employees** inclui a entrada para Jim Hance.

5. Feche o navegador da web.

#### <a name="to-modify-the-list-definition-and-list-instance-and-redeploy-them"></a>Para modificar a definição da lista e a instância da lista e reimplantá-las

1. No projeto EmployeesListDefinition, abra o arquivo *Elements.xml* que é um filho do item de projeto **instância da lista de funcionários** .

2. Remova o `Data` elemento e seus filhos para remover a entrada de Jim Hance da lista.

     Quando você concluir, o arquivo deverá conter o XML a seguir.

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

3. Salve e feche o arquivo *Elements.xml* .

4. Abra o menu de atalho para o item de projeto **lista de funcionários** e, em seguida, escolha **abrir** ou **Propriedades**.

5. No designer de lista, escolha a guia **modos de exibição** .

6. Na lista **colunas selecionadas** , escolha **anexos**e, em seguida, escolha a < chave para mover essa coluna para a lista **colunas disponíveis** .

7. Repita a etapa anterior para mover a coluna de **telefone comercial** da lista **colunas selecionadas** para a lista **colunas disponíveis** .

     Essa ação remove esses campos da exibição padrão da lista de **funcionários** no site do SharePoint.

8. Inicie a depuração escolhendo a tecla **F5** ou, na barra de menus, escolhendo **depurar**  >  **Iniciar Depuração**.

9. Verifique se a caixa de diálogo **conflitos de implantação** é exibida.

     Essa caixa de diálogo aparece quando o Visual Studio tenta implantar uma solução (a instância de lista) em um site do SharePoint no qual essa solução já foi implantada. Essa caixa de diálogo não aparecerá quando você executar a etapa de implantação de atualização posteriormente neste passo a passos.

10. Na caixa de diálogo **conflitos de implantação** , escolha o botão de opção **resolver automaticamente** .

     O Visual Studio exclui a instância de lista no site do SharePoint, implanta o item de lista no projeto e abre o site do SharePoint.

11. Na seção **listas** da barra de início rápido, escolha a lista **funcionários** e, em seguida, verifique os seguintes detalhes:

    - Os **anexos** e as colunas de **telefone residencial** não aparecem neste modo de exibição da lista.

    - A lista está vazia. Quando você usou a configuração de implantação **padrão** para reimplantar a solução, a lista de **funcionários** foi substituída pela nova lista vazia em seu projeto.

## <a name="test-the-deployment-step"></a>Testar a etapa de implantação
 Agora você está pronto para testar a etapa de implantação de atualização. Primeiro, adicione um item à instância de lista no SharePoint. Em seguida, altere a definição da lista e a instância da lista, atualize-as no site do SharePoint e confirme se a etapa de implantação da atualização não substitui o novo item.

#### <a name="to-manually-add-an-item-to-the-list"></a>Para adicionar manualmente um item à lista

1. Na faixa de faixas do site do SharePoint, na guia **ferramentas da lista** , escolha a guia **itens** .

2. No **novo** grupo, escolha **novo item**.

     Como alternativa, você pode escolher o link **Adicionar novo item** na própria lista de itens.

3. Na janela **funcionários-novo item** , na caixa **título** , digite Gerenciador de **instalações**.

4. Na caixa **nome** , digite **Andy**.

5. Na caixa **empresa** , digite **contoso**.

6. Escolha o botão **salvar** , verifique se o novo item aparece na lista e, em seguida, feche o navegador da Web.

     Mais adiante neste tutorial, você usará esse item para verificar se a etapa de implantação de atualização não substitui o conteúdo dessa lista.

#### <a name="to-test-the-upgrade-deployment-step"></a>Para testar a etapa de implantação de atualização

1. Na instância experimental do Visual Studio, em **Gerenciador de soluções**, abra o menu de atalho para o nó do projeto **EmployeesListDefinition** e escolha **Propriedades**.

    O designer/editor de propriedades é aberto.

2. Na guia **SharePoint** , defina a propriedade de **configuração de implantação ativa** como **Atualizar**.

    Essa configuração de implantação personalizada inclui a nova etapa de implantação de atualização.

3. Abra o menu de atalho para o item de projeto **lista de funcionários** e escolha **Propriedades** ou **abrir**.

    O designer/editor de propriedades é aberto.

4. Na guia **modos de exibição** , escolha a coluna **email** e, em seguida, escolha a **<** chave para mover essa coluna da lista **colunas selecionadas** para a lista **colunas disponíveis** .

    Essa ação remove esses campos da exibição padrão da lista de **funcionários** no site do SharePoint.

5. Inicie a depuração escolhendo a tecla **F5** ou, na barra de menus, escolhendo **depurar**  >  **Iniciar Depuração**.

6. Verifique se o código na outra instância do Visual Studio é interrompido no ponto de interrupção que você definiu anteriormente no `CanExecute` método.

7. Escolha a tecla **F5** novamente ou, na barra de menus, escolha **depurar**  >  **continuar**.

8. Verifique se o código é interrompido no ponto de interrupção que você definiu anteriormente no `Execute` método.

9. Escolha a tecla **F5** ou, na barra de menus, escolha **depurar**  >  **continuar** uma hora final.

     O navegador da Web abre o site do SharePoint.

10. Na seção **listas** da área início rápido, escolha a lista **funcionários** e verifique os seguintes detalhes:

    - O item que você adicionou manualmente anteriormente (para Andy, o Gerenciador de instalações) ainda está na lista.

    - As colunas de **telefone comercial** e **endereço de email** não aparecem neste modo de exibição da lista.

      A configuração de implantação de **atualização** modifica a instância de lista de **funcionários** existente no site do SharePoint. Se você usou a configuração de implantação **padrão** em vez da configuração de **atualização** , encontraria um conflito de implantação. O Visual Studio resolveria o conflito, substituindo a lista de **funcionários** e o item de Andy, o Gerenciador de instalações, seria excluído.

## <a name="clean-up-the-development-computer"></a>Limpar o computador de desenvolvimento
 Depois de concluir o teste da etapa de implantação de atualização, remova a instância de lista e a definição de lista do site do SharePoint e remova a extensão da etapa de implantação do Visual Studio.

#### <a name="to-remove-the-list-instance-from-the-sharepoint-site"></a>Para remover a instância de lista do site do SharePoint

1. Abra a lista de **funcionários** no site do SharePoint, se a lista ainda não estiver aberta.

2. Na faixa de faixas do site do SharePoint, escolha a guia **ferramentas de lista** e escolha a guia **lista** .

3. No grupo **configurações** , escolha o item **configurações de lista** .

4. Em **permissões e gerenciamento**, escolha o comando **excluir esta lista** , escolha **OK** para confirmar que deseja enviar a lista para a lixeira e, em seguida, feche o navegador da Web.

#### <a name="to-remove-the-list-definition-from-the-sharepoint-site"></a>Para remover a definição de lista do site do SharePoint

1. Na instância experimental do Visual Studio, na barra de menus, escolha **criar**  >  **Cancelar**.

     O Visual Studio cancela a definição de lista do site do SharePoint.

#### <a name="to-uninstall-the-extension"></a>Para desinstalar a extensão

1. Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas**  >  **extensões e atualizações**.

     A caixa de diálogo **Extensões e Atualizações** é aberta.

2. Na lista de extensões, escolha **Atualizar etapa de implantação para projetos do SharePoint**e, em seguida, escolha o comando **desinstalar** .

3. Na caixa de diálogo exibida, escolha **Sim** para confirmar que deseja desinstalar a extensão e escolha **reiniciar agora** para concluir a desinstalação.

4. Feche as duas instâncias do Visual Studio (a instância experimental e a instância do Visual Studio na qual a solução UpgradeDeploymentStep está aberta).

## <a name="see-also"></a>Consulte também
- [Estender o empacotamento e a implantação do SharePoint](../sharepoint/extending-sharepoint-packaging-and-deployment.md)
