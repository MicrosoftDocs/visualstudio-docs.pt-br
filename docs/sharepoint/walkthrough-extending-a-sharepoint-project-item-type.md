---
title: 'Passo a passo: Estendendo um tipo de Item de projeto do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- project items [SharePoint development in Visual Studio], extending
- SharePoint project items, extending
- SharePoint development in Visual Studio, extending project items
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 756486daa709efd6ce1ff697d6d190bb7f4a2e34
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295716"
---
# <a name="walkthrough-extend-a-sharepoint-project-item-type"></a>Passo a passo: Estender um tipo de item de projeto do SharePoint
  Você pode usar o **modelo de conectividade de dados corporativos** item de projeto para criar um modelo para o serviço de conectividade de dados comerciais (BDC) no SharePoint. Por padrão, quando você cria um modelo usando esse item de projeto, os dados no modelo não são exibidos aos usuários. Você também deve criar uma lista externa no SharePoint para permitir que os usuários exibam os dados.  
  
 Neste passo a passo, você criará uma extensão para o **modelo de conectividade de dados corporativos** item de projeto. Os desenvolvedores podem usar a extensão para criar uma lista externa no seu projeto que exibe os dados no modelo de BDC. Este passo a passo demonstra as seguintes tarefas:  
  
-   Criando uma extensão do Visual Studio que executa duas tarefas principais:  
  
    -   Ele gera uma lista externa que exibe os dados em um modelo BDC. A extensão usa o modelo de objeto para o sistema de projeto do SharePoint para gerar uma *Elements. XML* arquivo que define a lista. Ele também adiciona o arquivo ao projeto para que ele é implantado junto com o modelo BDC.  
  
    -   Ele adiciona um item de menu de atalho para o **modelo de conectividade de dados corporativos** itens de projeto do **Gerenciador de soluções**. Os desenvolvedores podem clicar neste item de menu para gerar uma lista externa para o modelo BDC.  
  
-   Criando um pacote de extensão VSIX (Visual Studio) para implantar o assembly de extensão.  
  
-   A extensão de teste.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passo:  
  
- Edições com suporte do Microsoft Windows, SharePoint e do Visual Studio.  
  
- O [!include[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]. Este passo a passo usa o **VSIX Project** modelo no SDK para criar um pacote VSIX para implantar o item de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).  
  
  Conhecimento dos conceitos a seguir é útil, mas não necessário para concluir o passo a passo:  
  
- O serviço BDC no [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)]. Para obter mais informações, consulte [arquitetura BDC](http://go.microsoft.com/fwlink/?LinkId=177798).  
  
- O esquema XML para modelos BDC. Para obter mais informações, consulte [infraestrutura de modelo BDC](http://go.microsoft.com/fwlink/?LinkId=177799).  
  
## <a name="create-the-projects"></a>Crie os projetos
 Para concluir este passo a passo, você precisa criar dois projetos:  
  
- Um projeto VSIX para criar o pacote VSIX para implantar a extensão de item de projeto.  
  
- Um projeto de biblioteca de classe que implementa a extensão de item de projeto.  
  
  Inicie o passo a passo Criando os projetos.  
  
#### <a name="to-create-the-vsix-project"></a>Para criar o projeto do VSIX  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
3.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha o **extensibilidade** nó.  
  
    > [!NOTE]  
    >  O **extensibilidade** o nó está disponível somente se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos no início deste tópico.  
  
4.  Na lista na parte superior a **novo projeto** diálogo caixa, escolha **.NET Framework 4.5**.  
  
     Extensões de ferramentas do SharePoint exigem recursos nesta versão do .NET Framework.  
  
5.  Escolha o **VSIX Project** modelo.  
  
6.  No **nome** , digite **GenerateExternalDataLists**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **GenerateExternalDataLists** projeto ao **Gerenciador de soluções**.  
  
7.  Se o arquivo vsixmanifest não abrir automaticamente, abra o menu de atalho no projeto GenerateExternalDataLists e escolha **abrir**  
  
8.  Verifique se o arquivo vsixmanifest tem uma entrada não está em branco (insira Contoso) para o campo de autor, salve o arquivo e, em seguida, fechá-lo.  
  
#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o **GenerateExternalDataLists** nó da solução, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
2.  No **adicionar novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha o **Windows** nó.  
  
3.  Na lista na parte superior da caixa de diálogo, escolha **.NET Framework 4.5**.  
  
4.  Na lista de modelos de projeto, escolha **biblioteca de classes**.  
  
5.  No **nome** , digite **BdcProjectItemExtension**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **BdcProjectItemExtension** projeto à solução e abre o arquivo de código padrão Class1.  
  
6.  Exclua o arquivo de código Class1 do projeto.  
  
## <a name="configure-the-extension-project"></a>Configurar o projeto de extensão
 Antes de escrever código para criar a extensão de item de projeto, adicione arquivos de código e referências de assembly ao projeto de extensão.  
  
#### <a name="to-configure-the-project"></a>Para configurar o projeto  
  
1.  No projeto BdcProjectItemExtension, adicione dois arquivos de código que têm os seguintes nomes:  
  
    -   ProjectItemExtension  
  
    -   GenerateExternalDataLists  
  
2.  Escolha o projeto BdcProjectItemExtension e, em seguida, na barra de menus, escolha **Project** > **Add Reference**.  
  
3.  Sob o **Assemblies** nó, escolher o **Framework** nó e selecione a caixa de seleção para cada um dos seguintes assemblies:  
  
    -   System.ComponentModel.Composition  
  
    -   WindowsBase  
  
4.  Sob o **Assemblies** nó, escolher o **extensões** nó e, em seguida, marque a caixa de seleção para o assembly a seguir:  
  
    -   Microsoft.VisualStudio.SharePoint  
  
5.  Escolha o botão **OK**.  
  
## <a name="define-the-project-item-extension"></a>Definir a extensão de item de projeto
 Criar uma classe que define a extensão para o **modelo de conectividade de dados corporativos** item de projeto. Para definir a extensão, a classe implementa o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectItemTypeExtension> interface. Implemente essa interface sempre que você deseja estender um tipo existente de item de projeto.  
  
#### <a name="to-define-the-project-item-extension"></a>Para definir a extensão de item de projeto  
  
1.  Cole o código a seguir no arquivo de código ProjectItemExtension.  
  
    > [!NOTE]  
    >  Depois de adicionar esse código, o projeto terá alguns erros de compilação. Esses erros serão eliminados quando você adicionar o código em etapas posteriores.  
  
     [!code-csharp[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#1](../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/projectitemextension.cs#1)]
     [!code-vb[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#1](../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/projectitemextension.vb#1)]  
  
## <a name="create-the-external-data-lists"></a>Criar as listas de dados externa
 Adicionar uma definição parcial do `GenerateExternalDataListsExtension` classe que cria uma lista de dados externa para cada entidade no modelo de BDC. Para criar a lista de dados externa, esse código lê primeiro os dados de entidade no modelo BDC analisando os dados XML no arquivo de modelo BDC. Em seguida, ele cria uma instância de lista com base no modelo BDC e adiciona essa instância de lista ao projeto.  
  
#### <a name="to-create-the-external-data-lists"></a>Para criar as listas de dados externa  
  
1.  Cole o código a seguir no arquivo de código GenerateExternalDataLists.  
  
     [!code-vb[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#2](../sharepoint/codesnippet/VisualBasic/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.vb#2)]
     [!code-csharp[SPExtensibility.ProjectItemExtension.BDCGenerateExternalDataLists#2](../sharepoint/codesnippet/CSharp/generateexternaldatalists/bdcprojectitemextension/generateexternaldatalists.cs#2)]  
  
## <a name="checkpoint"></a>Ponto de verificação  
 Neste momento no passo a passo, todo o código para a extensão de item de projeto está agora no projeto. Compile a solução para certificar-se de que o projeto é compilado sem erros.  
  
#### <a name="to-build-the-solution"></a>Para compilar a solução  
  
1.  Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
## <a name="create-a-vsix-package-to-deploy-the-project-item-extension"></a>Criar um pacote VSIX para implantar a extensão de item de projeto
 Para implantar a extensão, use o projeto do VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo vsixmanifest que está incluído no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.  
  
#### <a name="to-configure-and-create-the-vsix-package"></a>Para configurar e criar o pacote VSIX  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o arquivo vsixmanifest no projeto GenerateExternalDataLists e, em seguida, escolha **abrir**.  
  
     Visual Studio abre o arquivo no editor de manifesto. O arquivo vsixmanifest é que a base para o arquivo Extension vsixmanifest é necessária para todos os pacotes VSIX. Para obter mais informações sobre esse arquivo, consulte [1.0 referência do esquema de extensão do VSIX](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).  
  
2.  No **nome do produto** , digite **gerador de lista de dados externos**.  
  
3.  No **autor** , digite **Contoso**.  
  
4.  No **descrição** , digite **uma extensão para itens de projeto de modelo de conectividade de dados de negócios que pode ser usado para gerar listas de dados externa**.  
  
5.  Sobre o **ativos** guia do editor, escolha a **New** botão.  
  
     O **adicionar novo ativo** caixa de diálogo é exibida.  
  
6.  No **tipo** , escolha **mefcomponent**.  
  
    > [!NOTE]  
    >  Esse valor corresponde à `MefComponent` elemento no arquivo Extension vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [MEFComponent Element (esquema de VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).  
  
7.  No **fonte** , escolha **um projeto na solução atual**.  
  
8.  No **Project** , escolha **BdcProjectItemExtension**e, em seguida, escolha o **Okey** botão.  
  
9. Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
10. Certifique-se de que o projeto seja criado e compilado sem erros.  
  
11. Certifique-se de que a pasta de saída de compilação para o projeto GenerateExternalDataLists agora contém o arquivo Generateexternaldatalists.  
  
     Por padrão, a pasta de saída de compilação é o... pasta \bin\debug sob a pasta que contém seu arquivo de projeto.  
  
## <a name="test-the-project-item-extension"></a>A extensão de item de projeto de teste
 Agora você está pronto para testar a extensão de item de projeto. Primeiro, inicie a depuração do projeto de extensão na instância experimental do Visual Studio. Em seguida, use a extensão na instância experimental do Visual Studio para gerar uma lista externa para um modelo BDC. Por fim, abra a lista externa no site do SharePoint para verificar se ele funciona conforme o esperado.  
  
#### <a name="to-start-debugging-the-extension"></a>Para iniciar a extensão de depuração  
  
1.  Se necessário, reinicie o Visual Studio com credenciais administrativas e, em seguida, abra a solução GenerateExternalDataLists.  
  
2.  No projeto BdcProjectItemExtension, abra o arquivo de código ProjectItemExtension e, em seguida, adicione um ponto de interrupção à linha de código no `Initialize` método.  
  
3.  Abra o arquivo de código GenerateExternalDataLists e, em seguida, adicione um ponto de interrupção para a primeira linha de código no `GenerateExternalDataLists_Execute` método.  
  
4.  Iniciar a depuração, escolhendo a **F5** chave ou, na barra de menus, escolhendo **Debug** > **iniciar depuração**.  
  
     Visual Studio instala a extensão para %UserProfile%\AppData\Local\Microsoft\VisualStudio\10.0Exp\Extensions\Contoso\External Data List Generator\1.0 e inicia uma instância experimental do Visual Studio. Você testará o item de projeto nesta instância do Visual Studio.  
  
#### <a name="to-test-the-extension"></a>Para testar a extensão  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **arquivo** > **New** > **projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda o **modelos** nó, expanda o **Visual c#** nó, expanda o **SharePoint** nó e, em seguida, escolher **2010**.  
  
3.  Na lista na parte superior da caixa de diálogo, verifique se **.NET Framework 3.5** está selecionado. Projetos para [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] exigem esta versão do .NET Framework.  
  
4.  Na lista de modelos de projeto, escolha **projeto do SharePoint 2010**.  
  
5.  No **nome** , digite **SharePointProjectTestBDC**e, em seguida, escolha o **Okey** botão.  
  
6.  No Assistente de personalização do SharePoint, insira a URL do site que você deseja usar para depuração, escolha **implantar como uma solução de farm**e, em seguida, escolha o **concluir** botão.  
  
7.  Abra o menu de atalho do projeto SharePointProjectTestBDC, escolha **Add**e, em seguida, escolha **Novo Item**.  
  
8.  No **adicionar novo – SharePointProjectTestBDC** diálogo caixa, expanda o nó do idioma instalado, expanda o **SharePoint** nó.  
  
9. Escolha o **2010** nó e, em seguida, escolha o **modelo de conectividade de dados corporativos (somente solução de Farm)** modelo.  
  
10. No **nome** , digite **TestBDCModel**e, em seguida, escolha o **Add** botão.  
  
11. Verifique se o código em outra instância do Visual Studio para no ponto de interrupção que você definiu no `Initialize` método do arquivo de código ProjectItemExtension.  
  
12. Na versão interrompida do Visual Studio, escolha o **F5** chave ou na barra de menus, escolha **Debug** > **continuar** para continuar a depuração do projeto.  
  
13. Na instância experimental do Visual Studio, escolha o **F5** da chave ou, na barra de menus, escolha **Debug** > **iniciar depuração** para compilar, implantar e executar o **TestBDCModel** projeto.  
  
     O navegador da web abre a página padrão do site do SharePoint que é especificada para depuração.  
  
14. Verifique se que o **lista** seção na área de início rápido ainda não contém uma lista com base no modelo BDC padrão no projeto. Você primeiro deve criar uma lista de dados externos, usando a interface do usuário do SharePoint ou usando a extensão de item de projeto.  
  
15. Feche o navegador da Web.  
  
16. Na instância do Visual Studio que tem o projeto TestBDCModel aberto, abra o menu de atalho para o **TestBDCModel** nó no **Gerenciador de soluções**e, em seguida, escolha **gerar dados externos Lista**.  
  
17. Verifique se o código em outra instância do Visual Studio para no ponto de interrupção que você definiu no `GenerateExternalDataLists_Execute` método. Escolha o **F5** da chave ou, na barra de menus, escolha **Debug** > **continuar** para continuar a depuração do projeto.  
  
18. A instância experimental do Visual Studio adiciona uma instância de lista que é denominada **Entity1DataList** para TestBDCModel projeto e a instância também gera um recurso chamado **Feature2** para obter a lista instância.  
  
19. Escolha o **F5** da chave ou, na barra de menus, escolha **Debug** > **iniciar depuração** para compilar, implantar e executar o projeto TestBDCModel.  
  
     O navegador da web abre a página padrão do site do SharePoint que é usado para depuração.  
  
20. No **listas** seção da área de início rápido, escolha o **Entity1DataList** lista.  
  
21. Verifique se a lista contém as colunas que são chamadas Identifier1 e Message, além de um item que tem um valor de Identifier1 de 0 e um valor de mensagem do Hello World.  
  
     O **modelo de conectividade de dados corporativos** modelo de projeto gera o modelo BDC padrão que fornece todos esses dados.  
  
22. Feche o navegador da Web.  
  
## <a name="clean-up-the-development-computer"></a>Limpar o computador de desenvolvimento
 Depois de terminar de testar a extensão de item de projeto, remover a lista externa e o modelo BDC do site do SharePoint e remova a extensão de item de projeto do Visual Studio.  
  
#### <a name="to-remove-the-external-data-list-from-the-sharepoint-site"></a>Para remover a lista de dados externa do site do SharePoint  
  
1.  Na área de início rápido do site do SharePoint, escolha o **Entity1DataList** lista.  
  
2.  Na faixa de opções no site do SharePoint, escolha o **lista** guia.  
  
3.  No **lista** guia, o **configurações** de grupo, escolha **configurações da lista**.  
  
4.  Sob **permissões e gerenciamento**, escolha **excluir esta lista**e, em seguida, escolha **Okey** para confirmar que você deseja enviar a lista para a Lixeira.  
  
5.  Feche o navegador da Web.  
  
#### <a name="to-remove-the-bdc-model-from-the-sharepoint-site"></a>Para remover o modelo BDC do site do SharePoint  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **construir** > **Retract**.  
  
     Visual Studio remove o modelo BDC do site do SharePoint.  
  
#### <a name="to-remove-the-project-item-extension-from-visual-studio"></a>Para remover a extensão de item de projeto do Visual Studio  
  
1.  Na instância experimental do Visual Studio, na barra de menus, escolha **ferramentas** > **extensões e atualizações**.  
  
     A caixa de diálogo **Extensões e Atualizações** é aberta.  
  
2.  Na lista de extensões, escolha **gerador de lista de dados externos**e, em seguida, escolha o **desinstalar** botão.  
  
3.  Na caixa de diálogo que aparece, escolha **Sim** para confirmar que você deseja desinstalar a extensão.  
  
4.  Escolher **reiniciar agora** para concluir a desinstalação.  
  
5.  Feche ambas as instâncias do Visual Studio (a instância experimental e a instância na qual a solução GenerateExternalDataLists está aberta).  
  
## <a name="see-also"></a>Consulte também
 [Estender o sistema de projeto do SharePoint](../sharepoint/extending-the-sharepoint-project-system.md)   
 [Criar um modelo de conectividade de dados corporativos](../sharepoint/creating-a-business-data-connectivity-model.md)   
 [Criar um modelo de conectividade de dados corporativos](../sharepoint/designing-a-business-data-connectivity-model.md)  
  
  
