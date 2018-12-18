---
title: 'Passo a passo: Criar uma guia personalizada usando o XML da faixa de opções'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Ribbon [Office development in Visual Studio], tabs
- customizing the Ribbon, tabscustom Ribbon, tabs
- Ribbon [Office development in Visual Studio], XML
- XML [Office development in Visual Studio], Ribbon
- Ribbon [Office development in Visual Studio], customizing
- Custom tab [Office development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 45e35b7cf97a6b9a1f310149817f8e79956a47aa
ms.sourcegitcommit: c57ae28181ffe14a30731736661bf59c3eff1211
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38808918"
---
# <a name="walkthrough-create-a-custom-tab-by-using-ribbon-xml"></a>Passo a passo: Criar uma guia personalizada usando o XML da faixa de opções
  Este passo a passo demonstra como criar uma guia de faixa de opções personalizada usando o **da faixa de opções (XML)** item.  
  
 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]  
  
 Esta explicação passo a passo ilustra as seguintes tarefas:  
  
-   Adicionando botões para o **Add-Ins** guia. O **Add-Ins** guia é o padrão que é definido no arquivo XML de faixa de opções.  
  
-   Automatizando o Microsoft Office Word usando os botões na **Add-Ins** guia.  
  
> [!NOTE]  
>  Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]  
  
-   Microsoft Word.  
  
## <a name="create-the-project"></a>Criar o projeto  
 A primeira etapa é criar um projeto de suplemento do VSTO do Word. Mais tarde você personalizará a **Add-Ins** guia deste documento.  
  
### <a name="to-create-a-new-project"></a>Para criar um novo projeto  
  
1.  Criar uma **Word Add-in** projeto com o nome **MyRibbonAddIn**.  
  
     Para obter mais informações, consulte [como: projetos do Office de criar no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).  
  
     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o **ThisAddIn.cs** ou **ThisAddIn. vb** arquivo de código e adiciona os **MyRibbonAddIn** projeto ao **Gerenciador de soluções**.  
  
## <a name="create-the-vsto-add-ins-tab"></a>Criar a guia Suplementos do VSTO  
 Para criar o **Add-Ins** guia, adicione um **da faixa de opções (XML)** item ao seu projeto. Posteriormente neste passo a passo, você irá adicionar alguns botões a essa guia.  
  
### <a name="to-create-the-add-ins-tab"></a>Para criar a guia Add-ins  
  
1.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
2.  No **Adicionar Novo Item** caixa de diálogo, selecione **da faixa de opções (XML)**.  
  
3.  Altere o nome da nova faixa de opções para **MyRibbon**e clique em **Add**.  
  
     O **MyRibbon.cs** ou **Myribbon** arquivo é aberto no designer. Um arquivo XML que é denominado **MyRibbon.xml** também é adicionado ao seu projeto.  
  
4.  Na **Gerenciador de soluções**, clique com botão direito **ThisAddin.cs** ou **ThisAddIn. vb**e, em seguida, clique em **Exibir código**.  
  
5.  Adicione o seguinte código para o **ThisAddin** classe. Esse código substitui o `CreateRibbonExtensibilityObject` método e retorna o XML da faixa de opções de classe para o aplicativo do Office.  
  
     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs#1)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb#1)]  
  
6.  Na **Gerenciador de soluções**, com o botão direito do **MyRibbonAddIn** do projeto e, em seguida, clique em **Build**. Verifique se o projeto é compilado sem erros.  
  
## <a name="add-buttons-to-the-add-ins-tab"></a>Adicionar botões à guia Suplementos  
 A meta para este suplemento do VSTO é dar aos usuários uma maneira de adicionar texto clichê e uma tabela específica para o documento ativo. Para fornecer a interface do usuário, adicione dois botões para o **Add-Ins** guia modificando o arquivo XML de faixa de opções. Posteriormente neste passo a passo, você vai definir métodos de retorno de chamada para os botões. Para obter mais informações sobre o arquivo XML de faixa de opções, consulte [XML da faixa de opções](../vsto/ribbon-xml.md).  
  
### <a name="to-add-buttons-to-the-add-ins-tab"></a>Para adicionar botões à guia Suplementos  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **MyRibbon.xml** e, em seguida, clique em **abrir**.  
  
2.  Substitua o conteúdo do **guia** elemento com o XML a seguir. Esse XML altera o rótulo do grupo de controle padrão para **conteúdo**, e adiciona dois novos botões com os rótulos **Insert Text** e **Inserir tabela**.  
  
    ```xml  
    <tab idMso="TabAddIns">  
        <group id="ContentGroup" label="Content">  
            <button id="textButton" label="Insert Text"  
                 screentip="Text" onAction="OnTextButton"  
                 supertip="Inserts text at the cursor location."/>  
            <button id="tableButton" label="Insert Table"  
                 screentip="Table" onAction="OnTableButton"  
                 supertip="Inserts a table at the cursor location."/>  
        </group>  
    </tab>  
    ```  
  
## <a name="automate-the-document-by-using-the-buttons"></a>Automatizar o documento usando os botões  
 Você deve adicionar `onAction` métodos de retorno de chamada para o **inserir texto** e **Inserir tabela** botões para executar ações quando o usuário clica neles. Para obter mais informações sobre os métodos de retorno de chamada para controles da faixa de opções, consulte [XML da faixa de opções](../vsto/ribbon-xml.md).  
  
### <a name="to-add-callback-methods-for-the-buttons"></a>Para adicionar métodos de retorno de chamada para os botões  
  
1.  Na **Gerenciador de soluções**, clique com botão direito **MyRibbon.cs** ou **Myribbon**e, em seguida, clique em **abrir**.  
  
2.  Adicione o seguinte código na parte superior do **MyRibbon.cs** ou **Myribbon** arquivo. Esse código cria um alias para o <xref:Microsoft.Office.Interop.Word> namespace.  
  
     [!code-csharp[Trin_RibbonButtons#1](../vsto/codesnippet/CSharp/Trin_RibbonButtons/MyRibbon.cs#1)]
     [!code-vb[Trin_RibbonButtons#1](../vsto/codesnippet/VisualBasic/Trin_RibbonButtons/MyRibbon.vb#1)]  
  
3.  Adicione o seguinte método à classe `MyRibbon`. Esse é um método de retorno de chamada para o **Insert Text** botão que adiciona uma cadeia de caracteres para o documento ativo no local atual do cursor.  
  
     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#2](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.cs#2)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#2](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.vb#2)]  
  
4.  Adicione o seguinte método à classe `MyRibbon`. Esse é um método de retorno de chamada para o **Inserir tabela** botão que adiciona uma tabela ao documento ativo no local atual do cursor.  
  
     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#3](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.cs#3)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#3](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.vb#3)]  
  
## <a name="testing-the-vsto-add-in"></a>Testando o suplemento do VSTO  
 Quando você executa o projeto, o Word é aberto e a guia denominada **Add-Ins** aparece na faixa de opções. Clique o **Insert Text** e **Inserir tabela** botões a **Add-Ins** guia para testar o código.  
  
### <a name="to-test-your-vsto-add-in"></a>Para testar o suplemento do VSTO  
  
1.  Pressione **F5** para executar o projeto.  
  
2.  Confirme se o **Add-Ins** guia estiver visível na faixa de opções.  
  
3.  Clique o **Add-Ins** guia.  
  
4.  Confirme se o **conteúdo** grupo está visível na faixa de opções.  
  
5.  Clique o **Insert Text** botão na **conteúdo** grupo.  
  
     Uma cadeia de caracteres é adicionada ao documento no local atual do cursor.  
  
6.  Clique o **Inserir tabela** botão na **conteúdo** grupo.  
  
     Uma tabela é adicionada ao documento no local atual do cursor.  
  
## <a name="next-steps"></a>Próximas etapas  
 Você pode aprender mais sobre como personalizar a interface do usuário do Office nesses tópicos:  
  
-   Personalize a faixa de opções de outro aplicativo do Office. Para obter mais informações sobre os aplicativos que dão suporte à personalização da faixa de opções, consulte [visão geral da faixa de opções](../vsto/ribbon-overview.md).  
  
-   Personalize a faixa de opções de um aplicativo do Office usando o Designer de faixa de opções. Para obter mais informações, consulte [Fitas](../vsto/ribbon-designer.md).  
  
-   Crie um painel de ações personalizadas. Para obter mais informações, consulte [visão geral do painel de ações](../vsto/actions-pane-overview.md).  
  
-   Personalize a interface do usuário do Microsoft Office Outlook usando regiões de formulário do Outlook. Para obter mais informações, consulte [instruções passo a passo: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md).  
  
## <a name="see-also"></a>Consulte também  
 [Visão geral da faixa de opções](../vsto/ribbon-overview.md)   
 [XML da faixa de opções](../vsto/ribbon-xml.md)   
 [Passo a passo: Criar uma guia personalizada usando o Designer de faixa de opções](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)  
  
  