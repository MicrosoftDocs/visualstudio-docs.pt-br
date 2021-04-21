---
title: 'Walkthrough: criar uma guia personalizada usando o XML da faixa de uma'
description: Saiba como você pode adicionar botões à guia Add-Ins e automatizar o Microsoft Word usando a faixa de palavras (XML).
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
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
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a5d7992462ac3ece9782b0168feedd87577c2d0e
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/21/2021
ms.locfileid: "107826324"
---
# <a name="walkthrough-create-a-custom-tab-by-using-ribbon-xml"></a>Walkthrough: criar uma guia personalizada usando o XML da faixa de uma
  Este tutorial demonstra como criar uma guia de faixa de forma personalizada usando o item da faixa de para **(XML)** .

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

 Este passo a passo ilustra as seguintes tarefas:

- Adicionando botões à guia **suplementos** . A guia Suplementos é a guia padrão definida no arquivo XML da faixa de **bits** .

- Automatizando Microsoft Office Word usando os botões na guia **suplementos** .

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- [!INCLUDE[vsto_vsprereq](../vsto/includes/vsto-vsprereq-md.md)]

- Microsoft Word.

## <a name="create-the-project"></a>Criar o projeto
 A primeira etapa é criar um projeto de suplemento do VSTO do Word. Posteriormente, você personalizará a guia de **suplementos** deste documento.

### <a name="to-create-a-new-project"></a>Para criar um novo projeto

1. Crie um projeto de **suplemento do Word** com o nome **MyRibbonAddIn**.

     Para obter mais informações, consulte [como: criar projetos do Office no Visual Studio](../vsto/how-to-create-office-projects-in-visual-studio.md).

     [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] Abre o arquivo de código **ThisAddIn. cs** ou **ThisAddIn. vb** e adiciona o projeto **MyRibbonAddIn** ao **Gerenciador de soluções**.

## <a name="create-the-vsto-add-ins-tab"></a>Criar a guia de suplementos do VSTO
 Para criar a guia de **suplementos** , adicione um item **da faixa de bits (XML)** ao seu projeto. Mais adiante neste tutorial, você adicionará alguns botões a essa guia.

### <a name="to-create-the-add-ins-tab"></a>Para criar a guia de suplementos

1. No menu **Projeto** , clique em **Adicionar Novo Item**.

2. Na caixa de diálogo **Adicionar novo item** , selecione **faixa de opções (XML)**.

3. Altere o nome da nova faixa de forma para **MyRibbon** e clique em **Adicionar**.

     O arquivo **MyRibbon. cs** ou **MyRibbon. vb** é aberto no designer. Um arquivo XML chamado **MyRibbon.xml** também é adicionado ao seu projeto.

4. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **ThisAddIn. cs** ou em **ThisAddIn. vb** e clique em **Exibir código**.

5. Adicione o código a seguir à classe **ThisAddIn** . Esse código substitui o `CreateRibbonExtensibilityObject` método e retorna a classe XML da faixa de forma para o aplicativo do Office.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb" id="Snippet1":::

6. Em **Gerenciador de soluções**, clique com o botão direito do mouse no projeto **MyRibbonAddIn** e clique em **Compilar**. Verifique se o projeto é compilado sem erros.

## <a name="add-buttons-to-the-add-ins-tab"></a>Adicionar botões à guia suplementos
 O objetivo desse suplemento do VSTO é fornecer aos usuários uma maneira de adicionar texto clichê e uma tabela específica ao documento ativo. Para fornecer a interface do usuário, adicione dois botões à guia suplementos modificando o arquivo XML da faixa de **bits** . Mais adiante neste tutorial, você definirá métodos de retorno de chamada para os botões. Para obter mais informações sobre o arquivo XML da faixa de faixas, consulte [XML da faixa](../vsto/ribbon-xml.md)de visualização.

### <a name="to-add-buttons-to-the-add-ins-tab"></a>Para adicionar botões à guia suplementos

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **MyRibbon.xml** e clique em **abrir**.

2. Substitua o conteúdo do elemento de **guia** pelo seguinte XML. Esse XML altera o rótulo do grupo de controle padrão para **conteúdo** e adiciona dois novos botões com os rótulos **Inserir texto** e **Inserir Tabela**.

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
 Você deve adicionar `onAction` métodos de retorno de chamada para os botões **Inserir texto** e **Inserir Tabela** para executar ações quando o usuário clicar neles. Para obter mais informações sobre métodos de retorno de chamada para controles de faixa de chamadas, consulte [XML da faixa](../vsto/ribbon-xml.md)de de

### <a name="to-add-callback-methods-for-the-buttons"></a>Para adicionar métodos de retorno de chamada para os botões

1. Em **Gerenciador de soluções**, clique com o botão direito do mouse em **MyRibbon. cs** ou **MyRibbon. vb** e clique em **abrir**.

2. Adicione o código a seguir à parte superior do arquivo **MyRibbon. cs** ou **MyRibbon. vb** . Esse código cria um alias para o <xref:Microsoft.Office.Interop.Word> namespace.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_RibbonButtons/MyRibbon.cs" id="Snippet1":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_RibbonButtons/MyRibbon.vb" id="Snippet1":::

3. Adicione o método a seguir à classe `MyRibbon`. Esse é um método de retorno de chamada para o botão **Inserir texto** que adiciona uma cadeia de caracteres ao documento ativo no local atual do cursor.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.cs" id="Snippet2":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.vb" id="Snippet2":::

4. Adicione o método a seguir à classe `MyRibbon`. Esse é um método de retorno de chamada para o botão **Inserir Tabela** que adiciona uma tabela ao documento ativo no local atual do cursor.

     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.cs" id="Snippet3":::
     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/MyRibbon.vb" id="Snippet3":::

## <a name="testing-the-vsto-add-in"></a>Testando o suplemento do VSTO
 Quando você executa o projeto, o Word é aberto e a guia denominada **suplementos** é exibida na faixa de palavras. Clique nos botões **Inserir texto** e **Inserir Tabela** na guia **suplementos** para testar o código.

### <a name="to-test-your-vsto-add-in"></a>Para testar o suplemento do VSTO

1. Pressione **F5** para executar o projeto.

2. Confirme se a guia **suplementos** está visível na faixa de bits.

3. Clique na guia **suplementos** .

4. Confirme se o grupo de **conteúdo** está visível na faixa de faixas.

5. Clique no botão **Inserir texto** no grupo de **conteúdo** .

     Uma cadeia de caracteres é adicionada ao documento no local atual do cursor.

6. Clique no botão **Inserir Tabela** no grupo de **conteúdo** .

     Uma tabela é adicionada ao documento no local atual do cursor.

## <a name="next-steps"></a>Próximas etapas
 Você pode aprender mais sobre como personalizar a interface do usuário do Office a partir destes tópicos:

- Personalize a faixa de faixas de um aplicativo do Office diferente. Para obter mais informações sobre os aplicativos que dão suporte à personalização da faixa de faixas, consulte [visão geral do Ribbon](../vsto/ribbon-overview.md).

- Personalize a faixa de de um aplicativo do Office usando o designer de faixa de faixas. Para obter mais informações, consulte [Fitas](../vsto/ribbon-designer.md).

- Crie um painel Ações personalizadas. Para obter mais informações, consulte [visão geral do painel Ações](../vsto/actions-pane-overview.md).

- Personalize a interface do usuário do Microsoft Office Outlook usando as regiões de formulário do Outlook. Para obter mais informações, consulte [Walkthrough: criar uma região de formulário do Outlook](../vsto/walkthrough-designing-an-outlook-form-region.md).

## <a name="see-also"></a>Consulte também
- [Visão geral da faixa de faixas](../vsto/ribbon-overview.md)
- [XML da faixa de opções](../vsto/ribbon-xml.md)
- [Walkthrough: criar uma guia personalizada usando o designer de faixa de faixas](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
