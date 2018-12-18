---
title: 'Passo a passo: Criando uma extensão de projeto do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 8d68347f2b6b9f538555e05c91b15dcb045b46d6
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295976"
---
# <a name="walkthrough-create-a-sharepoint-project-extension"></a>Passo a passo: Criar uma extensão de projeto do SharePoint
  Este passo a passo ilustra como criar uma extensão para projetos do SharePoint. Você pode usar uma extensão de projeto para responder a eventos de nível de projeto, como quando um projeto é adicionado, excluído ou renomeado. Você também pode adicionar propriedades personalizadas ou responder quando um valor da propriedade muda. Diferentemente de extensões de item de projeto, as extensões de projeto não podem ser associadas um tipo específico de projeto do SharePoint. Quando você cria uma extensão de projeto, a extensão carrega quando qualquer tipo de projeto do SharePoint é aberto no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
 Neste passo a passo, você criará uma propriedade booleana personalizada que é adicionada a qualquer projeto do SharePoint criado no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Quando definido como **verdadeira**, a nova propriedade adiciona ou mapas, uma pasta de recursos de imagens ao seu projeto. Quando definido como **falsos**, a pasta de imagens é removida, se ele existir. Para obter mais informações, consulte [como: adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md).  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
-   Criando um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] extensão para projetos do SharePoint que faz o seguinte:  
  
    -   Adiciona uma propriedade de projeto personalizados para a janela Propriedades. A propriedade se aplica a qualquer projeto do SharePoint.  
  
    -   Usa o modelo de objeto de projeto do SharePoint para adicionar uma pasta mapeada para um projeto.  
  
    -   Usa o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] o modelo de objeto de automação DTE () para excluir uma pasta mapeada do projeto.  
  
-   Criando um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] assembly de extensão da propriedade de projeto de implantação do pacote VSIX (extensão).  
  
-   Depurando e testando a propriedade do projeto.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passo:  
  
-   Edições do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)], SharePoint e [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
-   O [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]. Este passo a passo usa o **projeto VSIX** modelo no [!INCLUDE[TLA2#tla_sdk](../sharepoint/includes/tla2sharptla-sdk-md.md)] para criar um pacote VSIX para implantar a extensão de propriedade do projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).  
  
## <a name="create-the-projects"></a>Crie os projetos
 Para concluir este passo a passo, você deve criar dois projetos:  
  
- Um projeto VSIX para criar o pacote VSIX para implantar a extensão de projeto.  
  
- Um projeto de biblioteca de classe que implementa a extensão de projeto.  
  
  Inicie o passo a passo Criando os projetos.  
  
#### <a name="to-create-the-vsix-project"></a>Para criar o projeto do VSIX  
  
1.  Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
2.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
3.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha o **extensibilidade** nó.  
  
    > [!NOTE]  
    >  Este nó estará disponível somente se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos no início deste tópico.  
  
4.  Na parte superior da caixa de diálogo, escolha **.NET Framework 4.5** na lista de versões do .NET Framework e, em seguida, escolha o **projeto VSIX** modelo.  
  
5.  No **nome** , digite **ProjectExtensionPackage**e, em seguida, escolha o **Okey** botão.  
  
     O **ProjectExtensionPackage** projeto aparece na **Gerenciador de soluções**.  
  
#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do nó da solução, escolha **Add**e, em seguida, escolha **novo projeto**.  
  
2.  No **novo projeto** diálogo caixa, expanda o **Visual c#** ou **Visual Basic** nós e, em seguida, escolha **Windows**.  
  
3.  Na parte superior da caixa de diálogo, escolha **.NET Framework 4.5** na lista de versões do .NET Framework e, em seguida, escolha o **biblioteca de classes** modelo de projeto.  
  
4.  No **nome** , digite **ProjectExtension**e, em seguida, escolha o **Okey** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Adiciona o **ProjectExtension** projeto à solução e abre o arquivo de código padrão Class1.  
  
5.  Exclua o arquivo de código Class1 do projeto.  
  
## <a name="configure-the-project"></a>Configurar o projeto
 Antes de escrever código para criar a extensão de projeto, adicione arquivos de código e referências de assembly ao projeto de extensão.  
  
#### <a name="to-configure-the-project"></a>Para configurar o projeto  
  
1.  Adicionar um arquivo de código que é denominado **CustomProperty** ao projeto de ProjectExtension.  
  
2.  Abra o menu de atalho para o **ProjectExtension** do projeto e, em seguida, escolha **adicionar referência**.  
  
3.  No **Gerenciador de referências - CustomProperty** diálogo caixa, escolha o **Framework** nó e, em seguida, selecione a caixa de seleção ao lado de assemblies Composition e System.  
  
4.  Escolha o **extensões** nó, selecione a caixa de seleção ao lado de assemblies Microsoft.VisualStudio.SharePoint e EnvDTE e, em seguida, escolha o **Okey** botão.  
  
5.  Na **Gerenciador de soluções**, sob o **referências** pasta para o **ProjectExtension** do projeto, escolha **EnvDTE**.  
  
6.  No **propriedades** janela, altere o **inserir tipos Interop** propriedade a ser **False**.  
  
## <a name="define-the-new-sharepoint-project-property"></a>Definir a nova propriedade de projeto do SharePoint
 Crie uma classe que define a extensão de projeto e o comportamento da nova propriedade de projeto. Para definir a nova extensão de projeto, a classe implementa o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> interface. Implemente essa interface sempre que você deseja definir uma extensão para um projeto do SharePoint. Além disso, adicione o <xref:System.ComponentModel.Composition.ExportAttribute> à classe. Este atributo permite [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] para descobrir e carregar seu <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> implementação. Passar o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> tipo para o construtor do atributo.  
  
#### <a name="to-define-the-new-sharepoint-project-property"></a>Para definir a nova propriedade de projeto do SharePoint  
  
1.  Cole o código a seguir no arquivo de código CustomProperty.  
  
     [!code-vb[SPExt_ProjectExtension#1](../sharepoint/codesnippet/VisualBasic/projectextension/customproperty.vb#1)]
     [!code-csharp[SPExt_ProjectExtension#1](../sharepoint/codesnippet/CSharp/projectextension/customproperty.cs#1)]  
  
## <a name="build-the-solution"></a>Criar a solução
 Em seguida, compile a solução para certificar-se de que ele foi compilado sem erros.  
  
#### <a name="to-build-the-solution"></a>Para compilar a solução  
  
1.  Na barra de menus, escolha **Compilar** > **Compilar Solução**.  
  
## <a name="create-a-vsix-package-to-deploy-the-project-property-extension"></a>Criar um pacote VSIX para implantar a extensão de propriedade do projeto
 Para implantar a extensão de projeto, use o projeto VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo vsixmanifest que está incluído no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.  
  
#### <a name="to-configure-and-create-the-vsix-package"></a>Para configurar e criar o pacote VSIX  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho para o arquivo vsixmanifest e, em seguida, escolha o **abrir** botão.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o arquivo no designer de manifesto. As informações que aparecem na **metadados** guia também aparece na **extensões e atualizações**. Todos os pacotes VSIX exigem o arquivo Extension vsixmanifest. Para obter mais informações sobre esse arquivo, consulte [1.0 referência do esquema de extensão do VSIX](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).  
  
2.  No **nome do produto** , digite **propriedade de projeto personalizado**.  
  
3.  No **autor** , digite **Contoso**.  
  
4.  No **descrição** , digite **uma propriedade de projeto personalizada do SharePoint que alterna o mapeamento da pasta de recursos de imagens ao projeto**.  
  
5.  Escolha o **ativos** guia e, em seguida, escolha o **New** botão.  
  
     O **adicionar novo ativo** caixa de diálogo é exibida.  
  
6.  No **tipo** , escolha **mefcomponent**.  
  
    > [!NOTE]  
    >  Esse valor corresponde à `MEFComponent` elemento no arquivo Extension vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [MEFComponent Element (esquema de VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).  
  
7.  No **fonte** , escolha o **um projeto na solução atual** botão de opção.  
  
8.  No **Project** , escolha **ProjectExtension**.  
  
     Esse valor identifica o nome do assembly que você está compilando no projeto.  
  
9. Escolher **Okey** para fechar o **adicionar novo ativo** caixa de diálogo.  
  
10. Na barra de menus, escolha **arquivo** > **Salvar tudo** quando você concluir e, em seguida, feche o designer de manifesto.  
  
11. Na barra de menus, escolha **construir** > **compilar solução**e, em seguida, certifique-se de que o projeto é compilado sem erros.  
  
12. Na **Gerenciador de soluções**, abra o menu de atalho para o **ProjectExtensionPackage** do projeto e escolha o **Abrir pasta no Explorador de arquivos** botão.  
  
13. Na **Explorador de arquivos**, abra a pasta de saída de compilação para o projeto ProjectExtensionPackage e, em seguida, verifique se a pasta contém um arquivo chamado ProjectExtensionPackage.vsix.  
  
     Por padrão, a pasta de saída de compilação é o... pasta \bin\debug sob a pasta que contém seu arquivo de projeto.  
  
## <a name="test-the-project-property"></a>A propriedade do projeto de teste
 Agora você está pronto para testar a propriedade de projeto personalizado. É mais fácil depurar e testar a nova extensão de propriedade do projeto em uma instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]. Esta instância de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] é criado quando você executa um VSIX ou outro projeto de extensibilidade. Depois de depurar o projeto, você pode instalar a extensão em seu sistema e, em seguida, continuar a depuração e teste-o em uma instância normal do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
#### <a name="to-debug-and-test-the-extension-in-an-experimental-instance-of-visual-studio"></a>Para depurar e testar a extensão em uma instância experimental do Visual Studio  
  
1.  Reiniciar [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] com credenciais administrativas e, em seguida, abra a solução ProjectExtensionPackage.  
  
2.  Iniciar uma compilação de depuração do seu projeto, escolha o **F5** chave ou, na barra de menus, escolhendo **Debug** > **iniciar depuração**.  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] instala a extensão para %UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom Property\1.0 de projeto e inicia uma instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
3.  Na instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], criar um projeto para uma solução de farm do SharePoint e usar os valores padrão para os outros valores no assistente.  
  
    1.  Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**.  
  
    2.  Na parte superior dos **novo projeto** diálogo caixa, escolha **.NET Framework 3.5** na lista de versões do .NET Framework.  
  
         As extensões de ferramentas do SharePoint exigem recursos nesta versão do [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)].  
  
    3.  Sob o **modelos** nó, expanda o **Visual c#** ou **Visual Basic** nó, escolha o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
    4.  Escolha o **projeto do SharePoint 2010** modelo e, em seguida, insira **ModuleTest** como o nome do seu projeto.  
  
4.  Na **Gerenciador de soluções**, escolha o **ModuleTest** nó do projeto.  
  
     Uma nova propriedade personalizada **pasta de imagens de mapa** aparece na **Properties** janela com um valor padrão de **False**.  
  
5.  Altere o valor dessa propriedade para **verdadeira**.  
  
     Uma pasta de recursos de imagens é adicionada ao projeto do SharePoint.  
  
6.  Altere o valor da propriedade de volta para **falsos**.  
  
     Se você escolher o **Sim** botão na **exclua a pasta de imagens?** caixa de diálogo, as imagens na pasta de recurso é excluída do projeto do SharePoint.  
  
7.  Feche a instância experimental de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
## <a name="see-also"></a>Consulte também
 [Estender projetos do SharePoint](../sharepoint/extending-sharepoint-projects.md)   
 [Como: adicionar uma propriedade a projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)   
 [Converter entre tipos de sistema de projeto do SharePoint e outros tipos de projeto do Visual Studio](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)   
 [Salvar os dados nas extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)   
 [Associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)  
  
