---
title: 'Walkthrough: criando uma extensão de projeto do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- projects [SharePoint development in Visual Studio], extending
- SharePoint development in Visual Studio, extending projects
- SharePoint projects, extending
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5df10e2da9e6b4c31894dce0669e9aa0e580b92f
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015080"
---
# <a name="walkthrough-create-a-sharepoint-project-extension"></a>Walkthrough: criar uma extensão de projeto do SharePoint
  Este tutorial ilustra como criar uma extensão para projetos do SharePoint. Você pode usar uma extensão de projeto para responder a eventos de nível de projeto, como quando um projeto é adicionado, excluído ou renomeado. Você também pode adicionar propriedades personalizadas ou responder quando um valor de propriedade for alterado. Ao contrário das extensões de item de projeto, as extensões de projeto não podem ser associadas a um tipo de projeto do SharePoint específico. Quando você cria uma extensão de projeto, a extensão é carregada quando qualquer tipo de projeto do SharePoint é aberto no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

 Neste tutorial, você criará uma propriedade booleana personalizada que é adicionada a qualquer projeto do SharePoint criado no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Quando definido como **true**, a nova propriedade adiciona ou mapeia uma pasta de recursos de imagens ao seu projeto. Quando definido como **false**, a pasta imagens é removida, se existir. Para obter mais informações, consulte [como: Adicionar e remover pastas mapeadas](../sharepoint/how-to-add-and-remove-mapped-folders.md).

 Este tutorial demonstra as seguintes tarefas:

- Criando uma [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] extensão para projetos do SharePoint que faz o seguinte:

  - Adiciona uma propriedade de projeto personalizada à janela Propriedades. A propriedade se aplica a qualquer projeto do SharePoint.

  - Usa o modelo de objeto de projeto do SharePoint para adicionar uma pasta mapeada a um projeto.

  - Usa o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] DTE (modelo de objeto de automação) para excluir uma pasta mapeada do projeto.

- Criando um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] pacote de VSIX (extensão) para implantar o assembly de extensão da Propriedade do projeto.

- Depurando e testando a propriedade do projeto.

## <a name="prerequisites"></a>Pré-requisitos
 Você precisa dos seguintes componentes no computador de desenvolvimento para concluir este passo a passos:

- Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] , SharePoint e [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

- O [!INCLUDE[vssdk_current_long](../sharepoint/includes/vssdk-current-long-md.md)]. Este tutorial usa o modelo de **projeto VSIX** no [!INCLUDE[TLA2#tla_sdk](../sharepoint/includes/tla2sharptla-sdk-md.md)] para criar um pacote VSIX para implantar a extensão de propriedade de projeto. Para obter mais informações, consulte [estender as ferramentas do SharePoint no Visual Studio](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md).

## <a name="create-the-projects"></a>Criar os projetos
 Para concluir este passo a passos, você deve criar dois projetos:

- Um projeto VSIX para criar o pacote VSIX para implantar a extensão do projeto.

- Um projeto de biblioteca de classes que implementa a extensão do projeto.

  Inicie o passo a passos criando os projetos.

#### <a name="to-create-the-vsix-project"></a>Para criar o projeto VSIX

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

3. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha o nó **extensibilidade** .

    > [!NOTE]
    > Esse nó estará disponível somente se você instalar o SDK do Visual Studio. Para obter mais informações, consulte a seção pré-requisitos anteriormente neste tópico.

4. Na parte superior da caixa de diálogo, escolha **.NET Framework 4,5** na lista de versões do .NET Framework e, em seguida, escolha o modelo de **projeto VSIX** .

5. Na caixa **nome** , digite **ProjectExtensionPackage**e, em seguida, escolha o botão **OK** .

     O projeto **ProjectExtensionPackage** aparece na **Gerenciador de soluções**.

#### <a name="to-create-the-extension-project"></a>Para criar o projeto de extensão

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó da solução, escolha **Adicionar**e, em seguida, escolha **novo projeto**.

2. Na caixa de diálogo **novo projeto** , expanda os nós **Visual C#** ou **Visual Basic** e, em seguida, escolha **Windows**.

3. Na parte superior da caixa de diálogo, escolha **.NET Framework 4,5** na lista de versões do .NET Framework e, em seguida, escolha o modelo de projeto de **biblioteca de classes** .

4. Na caixa **nome** , digite **ProjectExtension**e, em seguida, escolha o botão **OK** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Adiciona o projeto **ProjectExtension** à solução e abre o arquivo de código de Class1 padrão.

5. Exclua o arquivo de código Class1 do projeto.

## <a name="configure-the-project"></a>Configurar o projeto
 Antes de escrever o código para criar a extensão do projeto, adicione arquivos de código e referências de assembly ao projeto de extensão.

#### <a name="to-configure-the-project"></a>Para configurar o projeto

1. Adicione um arquivo de código chamado **CustomProperty** ao projeto ProjectExtension.

2. Abra o menu de atalho para o projeto **ProjectExtension** e escolha **Adicionar referência**.

3. Na caixa de diálogo **Gerenciador de referências-personalizadoproperty** , escolha o nó de **estrutura** e marque a caixa de seleção ao lado dos assemblies System. ComponentModel. composição e System. Windows. Forms.

4. Escolha o nó **extensões** , marque a caixa de seleção ao lado dos assemblies Microsoft. VisualStudio. SharePoint e EnvDTE e, em seguida, escolha o botão **OK** .

5. No **Gerenciador de soluções**, na pasta **referências** para o projeto **ProjectExtension** , escolha **EnvDTE**.

6. Na janela **Propriedades** , altere a propriedade **inserir tipos de interoperabilidade** para **false**.

## <a name="define-the-new-sharepoint-project-property"></a>Definir a nova propriedade de projeto do SharePoint
 Crie uma classe que define a extensão do projeto e o comportamento da nova propriedade de projeto. Para definir a nova extensão do projeto, a classe implementa a <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> interface. Implemente essa interface sempre que desejar definir uma extensão para um projeto do SharePoint. Além disso, adicione o <xref:System.ComponentModel.Composition.ExportAttribute> à classe. Esse atributo permite que [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] o descubra e carregue sua <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> implementação. Passe o <xref:Microsoft.VisualStudio.SharePoint.ISharePointProjectExtension> tipo para o construtor do atributo.

#### <a name="to-define-the-new-sharepoint-project-property"></a>Para definir a nova propriedade de projeto do SharePoint

1. Cole o código a seguir no arquivo de código Personalizadoproperty.

     [!code-vb[SPExt_ProjectExtension#1](../sharepoint/codesnippet/VisualBasic/projectextension/customproperty.vb#1)]
     [!code-csharp[SPExt_ProjectExtension#1](../sharepoint/codesnippet/CSharp/projectextension/customproperty.cs#1)]

## <a name="build-the-solution"></a>Compilar a solução
 Em seguida, Compile a solução para certificar-se de que ela seja compilada sem erros.

#### <a name="to-build-the-solution"></a>Para compilar a solução

1. Na barra de menus, escolha **Compilar**compilar  >  **solução**.

## <a name="create-a-vsix-package-to-deploy-the-project-property-extension"></a>Criar um pacote VSIX para implantar a extensão de Propriedade do projeto
 Para implantar a extensão do projeto, use o projeto VSIX em sua solução para criar um pacote VSIX. Primeiro, configure o pacote VSIX modificando o arquivo. Extension. vsixmanifest de origem que está incluído no projeto VSIX. Em seguida, crie o pacote VSIX criando a solução.

#### <a name="to-configure-and-create-the-vsix-package"></a>Para configurar e criar o pacote VSIX

1. No **Gerenciador de soluções**, abra o menu de atalho para o arquivo Source. Extension. vsixmanifest e, em seguida, escolha o botão **abrir** .

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]Abre o arquivo no designer de manifesto. As informações exibidas na guia **metadados** também aparecem nas **extensões e atualizações**. Todos os pacotes VSIX exigem o arquivo extension. vsixmanifest. Para obter mais informações sobre esse arquivo, consulte [referência do esquema de extensão do VSIX 1,0](https://msdn.microsoft.com/76e410ec-b1fb-4652-ac98-4a4c52e09a2b).

2. Na caixa **nome do produto** , digite **propriedade personalizada do projeto**.

3. Na caixa **autor** , digite **contoso**.

4. Na caixa **Descrição** , insira **uma propriedade personalizada do projeto do SharePoint que alterna o mapeamento da pasta de recursos de imagens para o projeto**.

5. Escolha a guia **ativos** e, em seguida, escolha o botão **novo** .

     A caixa de diálogo **Adicionar novo ativo** é exibida.

6. Na lista **tipo** , escolha **Microsoft. VisualStudio. MefComponent**.

    > [!NOTE]
    > Esse valor corresponde ao `MEFComponent` elemento no arquivo extension. vsixmanifest. Esse elemento Especifica o nome de um assembly de extensão no pacote VSIX. Para obter mais informações, consulte [elemento MEFComponent (esquema VSX)](/previous-versions/visualstudio/visual-studio-2010/dd393736\(v\=vs.100\)).

7. Na lista **origem** , escolha o botão de opção **um projeto na solução atual** .

8. Na lista **projeto** , escolha **ProjectExtension**.

     Esse valor identifica o nome do assembly que você está criando no projeto.

9. Escolha **OK** para fechar a caixa de diálogo **Adicionar novo ativo** .

10. Na barra de menus, escolha **arquivo**  >  **salvar tudo** quando terminar e, em seguida, feche o designer de manifesto.

11. Na barra de menus, escolha **criar**  >  **solução de compilação**e, em seguida, certifique-se de que o projeto seja compilado sem erros.

12. No **Gerenciador de soluções**, abra o menu de atalho do projeto **ProjectExtensionPackage** e escolha a **pasta abrir no explorador de arquivos** .

13. No **Explorador de arquivos**, abra a pasta de saída de compilação para o projeto ProjectExtensionPackage e verifique se a pasta contém um arquivo chamado ProjectExtensionPackage. vsix.

     Por padrão, a pasta de saída da compilação é a.. pasta \bin\Debug sob a pasta que contém o arquivo de projeto.

## <a name="test-the-project-property"></a>Testar a propriedade do projeto
 Agora você está pronto para testar a propriedade de projeto personalizada. É mais fácil depurar e testar a nova extensão de propriedade de projeto em uma instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Essa instância do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] é criada quando você executa um VSIX ou outro projeto de extensibilidade. Depois de depurar o projeto, você pode instalar a extensão em seu sistema e, em seguida, continuar a depurá-la e testá-la em uma instância regular do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

#### <a name="to-debug-and-test-the-extension-in-an-experimental-instance-of-visual-studio"></a>Para depurar e testar a extensão em uma instância experimental do Visual Studio

1. Reinicie [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] com credenciais administrativas e, em seguida, abra a solução ProjectExtensionPackage.

2. Inicie uma compilação de depuração do seu projeto escolhendo a tecla **F5** ou, na barra de menus, escolhendo **depurar**  >  **Iniciar Depuração**.

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]instala a extensão para o projeto%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0Exp\Extensions\Contoso\Custom Property\1.0 e inicia uma instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

3. Na instância experimental do [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , crie um projeto do SharePoint para uma solução de farm e use os valores padrão para os outros valores no assistente.

    1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

    2. Na parte superior da caixa de diálogo **novo projeto** , escolha **.NET Framework 3,5** na lista de versões do .NET Framework.

         As extensões de ferramenta do SharePoint requerem recursos nesta versão do [!INCLUDE[dnprdnshort](../sharepoint/includes/dnprdnshort-md.md)] .

    3. No nó **modelos** , expanda o nó **Visual C#** ou **Visual Basic** , escolha o nó **SharePoint** e, em seguida, escolha o nó **2010** .

    4. Escolha o modelo de **projeto do SharePoint 2010** e, em seguida, insira **ModuleTest** como o nome do seu projeto.

4. Em **Gerenciador de soluções**, escolha o nó do projeto **ModuleTest** .

     Uma nova pasta de **imagens de mapa** de propriedade personalizada aparece na janela **Propriedades** com um valor padrão de **false**.

5. Altere o valor dessa propriedade para **true**.

     Uma pasta de recursos de imagens é adicionada ao projeto do SharePoint.

6. Altere o valor dessa propriedade de volta para **false**.

     Se você escolher o botão **Sim** na caixa de diálogo **excluir a pasta imagens?** , a pasta de recursos imagens será excluída do projeto do SharePoint.

7. Feche a instância experimental de [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

## <a name="see-also"></a>Consulte também
- [Estender projetos do SharePoint](../sharepoint/extending-sharepoint-projects.md)
- [Como: adicionar uma propriedade a projetos do SharePoint](../sharepoint/how-to-add-a-property-to-sharepoint-projects.md)
- [Converter entre os tipos do sistema de projeto do SharePoint e outros tipos de projeto do Visual Studio](../sharepoint/converting-between-sharepoint-project-system-types-and-other-visual-studio-project-types.md)
- [Salvar dados em extensões do sistema de projeto do SharePoint](../sharepoint/saving-data-in-extensions-of-the-sharepoint-project-system.md)
- [Associar dados personalizados a extensões de ferramentas do SharePoint](../sharepoint/associating-custom-data-with-sharepoint-tools-extensions.md)
