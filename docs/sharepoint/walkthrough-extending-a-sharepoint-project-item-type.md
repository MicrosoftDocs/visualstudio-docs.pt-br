---
title: 'Walkthrough: estendendo um tipo de item de projeto do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f949329c7db71386a12c3ab8d7fccf1483b8cca2
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015678"
---
# <a name="walkthrough-extend-a-sharepoint-project-item-type"></a>Walkthrough: estender um tipo de item de projeto do SharePoint
  Você pode usar o item de projeto **modelo de conectividade de dados corporativos** para criar um modelo para o serviço corporativo de conectividade de dados (BDC) no SharePoint. Por padrão, quando você cria um modelo usando esse item de projeto, os dados no modelo não são exibidos aos usuários. Você também deve criar uma lista externa no SharePoint para permitir que os usuários exibam os dados.

 Neste tutorial, você criará uma extensão para o item de projeto **modelo de conectividade de dados corporativos** . Os desenvolvedores podem usar a extensão para criar uma lista externa em seu projeto que exibe os dados no modelo do BDC. Este tutorial demonstra as seguintes tarefas:

- Criar uma extensão do Visual Studio que executa duas tarefas principais:

  - Ele gera uma lista externa que exibe os dados em um modelo BDC. A extensão usa o modelo de objeto para o sistema de projeto do SharePoint para gerar um arquivo de *Elements.xml* que define a lista. Ele também adiciona o arquivo ao projeto para que ele seja implantado junto com o modelo BDC.

  - Ele adiciona um item de menu de atalho aos itens de projeto **modelo de conectividade de dados corporativos** em **Gerenciador de soluções**. Os desenvolvedores podem clicar nesse item de menu para gerar uma lista externa para o modelo BDC.

- Criando um pacote de VSIX (Visual Studio Extension) para implantar o assembly de extensão.

- Testando a extensão.

## <a name="prerequisites"></a>Pré-requisitos
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passos:

- Edições com suporte do Microsoft Windows, SharePoint e Visual Studio.

- O [!include[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]. Este tutorial usa o modelo de **projeto VSIX** no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).

  O conhecimento dos seguintes conceitos é útil, mas não é necessário, para concluir o passo a passos:

- O serviço do BDC no [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] . Para obter mais informações, consulte [arquitetura do BDC](/previous-versions/office/developer/sharepoint-2010/ee558876(v=office.14)).

- O esquema XML para modelos de BDC. Para obter mais informações, consulte [infraestrutura de modelo do BDC](/previous-versions/office/developer/sharepoint-2010/ee556378(v=office.14)).

## <a name="create-the-projects"></a>Criar os projetos
 Para concluir este passo a passos, você precisa criar dois projetos:

- Um projeto VSIX para criar o pacote VSIX para implantar a extensão de item de projeto.

- Um projeto de biblioteca de classes que implementa a extensão de item de projeto.

  Inicie o passo a passos criando os projetos.

#### <a name="to-create-the-vsix-project"></a>Para criar o projeto VSIX

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

3. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha o nó **extensibilidade** .

    > [!NOTE]
    > O nó **extensibilidade** só estará disponível se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos anteriormente neste tópico.

4. Na lista na parte superior da caixa de diálogo **novo projeto** , escolha **.NET Framework 4,5**.

     As extensões de ferramentas do SharePoint exigem recursos nesta versão do .NET Framework.

5. Escolha o modelo de **projeto VSIX** .

6. Na caixa **nome** , digite **GenerateExternalDataLists**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **GenerateExternalDataLists** ao **Gerenciador de soluções**.

7. Se o arquivo Source. Extension. vsixmanifest não abrir automaticamente, abra o menu de atalho no projeto GenerateExternalDataLists e, em seguida, escolha **abrir**

8. Verifique se o arquivo Source. Extension. vsixmanifest tem uma entrada que não está em branco (Insira contoso) para o campo autor, salve o arquivo e feche-o.

#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução **GenerateExternalDataLists** , escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na caixa de diálogo **Adicionar novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha o nó **Windows** .

3. Na lista na parte superior da caixa de diálogo, escolha **.NET Framework 4,5**.

4. Na lista de modelos de projeto, escolha **biblioteca de classes**.

5. Na caixa **nome** , digite **BdcProjectItemExtension**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **BdcProjectItemExtension** à solução e abre o arquivo de código de Class1 padrão.

6. Exclua o arquivo de código Class1 do projeto.

## <a name="configure-the-extension-project"></a>Configurar o projeto de extensão
 Antes de escrever o código para criar a extensão de item de projeto, adicione arquivos de código e referências de assembly ao projeto de extensão.

#### <a name="to-configure-the-project"></a>Para configurar o projeto

1. No projeto BdcProjectItemExtension, adicione dois arquivos de código que têm os seguintes nomes:

    - ProjectItemExtension

    - GenerateExternalDataLists

2. Escolha o projeto BdcProjectItemExtension e, em seguida, na barra de menus, escolha **projeto**  >  **Adicionar referência**.

3. No nó **assemblies** , escolha o nó **estrutura** e marque a caixa de seleção para cada um dos seguintes assemblies:

    - System. ComponentModel. composição

    - WindowsBase

4. No nó **assemblies** , escolha o nó **extensões** e marque a caixa de seleção para o seguinte assembly:

    - Microsoft. VisualStudio. SharePoint

5. Clique no botão **OK**.

## <a name="define-the-project-item-extension"></a>Definir a extensão do item de projeto
 Crie uma classe que define a extensão para o item de projeto **modelo de conectividade de dados corporativos** . Para definir a extensão, a classe implementa a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> interface. Implemente essa interface sempre que desejar estender um tipo existente de item de projeto.

#### <a name="to-define-the-project-item-extension"></a>Para definir a extensão de item de projeto

1. Cole o código a seguir no arquivo de código ProjectItemExtension.

    > [!NOTE]
    > Depois de adicionar esse código, o projeto terá alguns erros de compilação. Esses erros vão desaparecer quando você adiciona código em etapas posteriores.

     [!code-csharp[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#1](../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/projectitemextension.cs#1)]
     [!code-vb[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#1](../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/projectitemextension.vb#1)]

## <a name="create-the-external-data-lists"></a>Criar listas de dados externos
 Adicione uma definição parcial da `GenerateExternalDataListsExtension` classe que cria uma lista de dados externos para cada entidade no modelo BDC. Para criar a lista de dados externos, esse código primeiro lê os dados da entidade no modelo do BDC analisando os dados XML no arquivo de modelo do BDC. Em seguida, ele cria uma instância de lista baseada no modelo do BDC e adiciona essa instância de lista ao projeto.

#### <a name="to-create-the-external-data-lists"></a>Para criar as listas de dados externos

1. Cole o código a seguir no arquivo de código GenerateExternalDataLists.

     [!code-vb[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#2](../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.vb#2)]
     [!code-csharp[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#2](../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.cs#2)]

## <a name="checkpoint"></a>Ponto de verificação
 Neste ponto do passo a passo, todo o código para a extensão de item de projeto agora está no projeto. Compile a solução para garantir que o projeto seja compilado sem erros.

#### <a name="to-build-the-solution"></a>Para compilar a solução

1. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

## <a name="create-a-vsix-package-to-deploy-the-project-item-extension"></a>Criar um pacote VSIX para implantar a extensão de item de projeto
 Para implantar a extensão, use o projeto VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo. Extension. vsixmanifest de origem que está incluído no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.

#### <a name="to-configure-and-create-the-vsix-package"></a>Para configurar e criar o pacote VSIX

1. No **Gerenciador de soluções**, abra o menu de atalho do arquivo Source. Extension. vsixmanifest no projeto GenerateExternalDataLists e, em seguida, escolha **abrir**.

     O Visual Studio abre o arquivo no editor de manifesto. O arquivo Source. Extension. vsixmanifest é a base para o arquivo de extensão. vsixmanifest é exigido por todos os pacotes VSIX. Para obter mais informações sobre esse arquivo, consulte [referência do esquema de extensão do VSIX 1,0](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).

2. Na caixa **nome do produto** , insira **gerador de lista de dados externos**.

3. Na caixa **autor** , digite **contoso**.

4. Na caixa **Descrição** , insira **uma extensão para itens de projeto modelo de conectividade de dados corporativos que podem ser usados para gerar listas de dados externos**.

5. Na guia **ativos** do editor, escolha o botão **novo** .

     A caixa de diálogo **Adicionar novo ativo** é exibida.

6. Na lista **tipo** , escolha **Microsoft. VisualStudio. MefComponent**.

    > [!NOTE]
    > Esse valor corresponde ao `MefComponent` elemento no arquivo extension. vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [elemento MEFComponent (esquema VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).

7. Na lista **origem** , escolha **um projeto na solução atual**.

8. Na lista **projeto** , escolha **BdcProjectItemExtension**e, em seguida, escolha o botão **OK** .

9. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

10. Certifique-se de que o projeto seja compilado e compilado sem erros.

11. Verifique se a pasta de saída da compilação do projeto GenerateExternalDataLists agora contém o arquivo GenerateExternalDataLists. vsix.

     Por padrão, a pasta de saída da compilação é a.. pasta \bin\Debug sob a pasta que contém o arquivo de projeto.

## <a name="test-the-project-item-extension"></a>Testar a extensão de item do projeto
 Agora você está pronto para testar a extensão de item do projeto. Primeiro, inicie a depuração do projeto de extensão na instância experimental do Visual Studio. Em seguida, use a extensão na instância experimental do Visual Studio para gerar uma lista externa para um modelo de BDC. Por fim, abra a lista externa no site do SharePoint para verificar se ele funciona conforme o esperado.

#### <a name="to-start-debugging-the-extension"></a>Para iniciar a depuração da extensão

1. Se necessário, reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução GenerateExternalDataLists.

2. No projeto BdcProjectItemExtension, abra o arquivo de código ProjectItemExtension e, em seguida, adicione um ponto de interrupção à linha de código no `Initialize` método.

3. Abra o arquivo de código GenerateExternalDataLists e, em seguida, adicione um ponto de interrupção à primeira linha de código no `GenerateExternalDataLists_Execute` método.

4. Inicie a depuração escolhendo a tecla **F5** ou, na barra de menus, escolhendo **depurar**  >  **Iniciar Depuração**.

     O Visual Studio instala a extensão para a lista de dados do%UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\External Generator\1.0 e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.

#### <a name="to-test-the-extension"></a>Para testar a extensão

1. Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

2. Na caixa de diálogo **novo projeto** , expanda o nó **modelos** , expanda o nó **Visual C#** , expanda o nó **SharePoint** e, em seguida, escolha **2010**.

3. Na lista na parte superior da caixa de diálogo, verifique se **.NET Framework 3,5** está selecionado. Os projetos para [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] exigem esta versão do .NET Framework.

4. Na lista de modelos de projeto, escolha **projeto do SharePoint 2010**.

5. Na caixa **nome** , digite **SharePointProjectTestBDC**e, em seguida, escolha o botão **OK** .

6. No Assistente para personalização do SharePoint, insira a URL do site que você deseja usar para depuração, escolha **implantar como uma solução de farm**e, em seguida, escolha o botão **concluir** .

7. Abra o menu de atalho para o projeto SharePointProjectTestBDC, escolha **Adicionar**e, em seguida, escolha **novo item**.

8. Na caixa de diálogo **Adicionar newItem-SharePointProjectTestBDC** , expanda o nó idioma instalado, expanda o nó do **SharePoint** .

9. Escolha o nó **2010** e escolha o modelo do modelo de **conectividade de dados corporativos (somente solução de farm)** .

10. Na caixa **nome** , digite **TestBDCModel**e, em seguida, escolha o botão **Adicionar** .

11. Verifique se o código na outra instância do Visual Studio é interrompido no ponto de interrupção que você definiu no `Initialize` método do arquivo de código ProjectItemExtension.

12. Na instância interrompida do Visual Studio, escolha a tecla **F5** ou, na barra de menus, escolha **depurar**  >  **continuar** para continuar a depurar o projeto.

13. Na instância experimental do Visual Studio, escolha a tecla **F5** ou, na barra de menus, escolha **depurar**  >  **Iniciar Depuração** para compilar, implantar e executar o projeto **TestBDCModel** .

     O navegador da Web é aberto na página padrão do site do SharePoint que é especificado para depuração.

14. Verifique se a seção **listas** na área início rápido ainda não contém uma lista baseada no modelo BDC padrão no projeto. Você deve primeiro criar uma lista de dados externa usando a interface do usuário do SharePoint ou usando a extensão de item do projeto.

15. Feche o navegador da web.

16. Na instância do Visual Studio que tem o projeto TestBDCModel aberto, abra o menu de atalho do nó **TestBDCModel** no **Gerenciador de soluções**e escolha **gerar lista de dados externos**.

17. Verifique se o código na outra instância do Visual Studio é interrompido no ponto de interrupção que você definiu no `GenerateExternalDataLists_Execute` método. Escolha a tecla **F5** ou, na barra de menus, escolha **depurar**  >  **continuar** para continuar a depurar o projeto.

18. A instância experimental do Visual Studio adiciona uma instância de lista denominada **Entity1DataList** ao projeto TestBDCModel, e a instância também gera um recurso chamado **Feature2** para a instância de lista.

19. Escolha a tecla **F5** ou, na barra de menus, escolha **depurar**  >  **Iniciar Depuração** para compilar, implantar e executar o projeto TestBDCModel.

     O navegador da Web é aberto na página padrão do site do SharePoint que é usada para depuração.

20. Na seção **listas** da área início rápido, escolha a lista **Entity1DataList** .

21. Verifique se a lista contém colunas nomeadas identifier1 e Message, além de um item que tenha um valor de identifier1 de 0 e um valor de mensagem de Olá, Mundo.

     O modelo de projeto **modelo de conectividade de dados corporativos** gera o modelo BDC padrão que fornece todos esses dados.

22. Feche o navegador da web.

## <a name="clean-up-the-development-computer"></a>Limpar o computador de desenvolvimento
 Depois de concluir o teste da extensão de item de projeto, remova a lista externa e o modelo BDC do site do SharePoint e remova a extensão de item de projeto do Visual Studio.

#### <a name="to-remove-the-external-data-list-from-the-sharepoint-site"></a>Para remover a lista de dados externos do site do SharePoint

1. Na área início rápido do site do SharePoint, escolha a lista **Entity1DataList** .

2. Na faixa de faixas do site do SharePoint, escolha a guia **lista** .

3. Na guia **lista** , no grupo **configurações** , escolha configurações da **lista**.

4. Em **permissões e gerenciamento**, escolha **excluir esta lista**e, em seguida, escolha **OK** para confirmar que você deseja enviar a lista para a lixeira.

5. Feche o navegador da web.

#### <a name="to-remove-the-bdc-model-from-the-sharepoint-site"></a>Para remover o modelo BDC do site do SharePoint

1. Na instância experimental do Visual Studio, na barra de menus, escolha **criar**  >  **Cancelar**.

     O Visual Studio remove o modelo BDC do site do SharePoint.

#### <a name="to-remove-the-project-item-extension-from-visual-studio"></a>Para remover a extensão de item de projeto do Visual Studio

1. Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas**  >  **extensões e atualizações**.

     A caixa de diálogo **Extensões e Atualizações** é aberta.

2. Na lista de extensões, escolha **gerador de lista de dados externos**e, em seguida, escolha o botão **desinstalar** .

3. Na caixa de diálogo exibida, escolha **Sim** para confirmar que você deseja desinstalar a extensão.

4. Escolha **reiniciar agora** para concluir a desinstalação.

5. Feche as duas instâncias do Visual Studio (a instância experimental e a instância na qual a solução GenerateExternalDataLists está aberta).

## <a name="see-also"></a>Consulte também
- [Estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md)
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)
- [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)
