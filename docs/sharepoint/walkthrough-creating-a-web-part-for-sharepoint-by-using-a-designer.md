---
title: Criar Web Part para o SharePoint usando o designer
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Web Parts [SharePoint development in Visual Studio], designer
- Web Parts [SharePoint development in Visual Studio], creating
- Web Parts [SharePoint development in Visual Studio], designing
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 732bd9fe3d34a768e0c6f71315f212c49bdf02af
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016387"
---
# <a name="walkthrough-create-a-web-part-for-sharepoint-by-using-a-designer"></a>Walkthrough: criar uma Web Part para o SharePoint usando um designer

Se você criar Web Parts para um site do SharePoint, os usuários poderão modificar diretamente o conteúdo, a aparência e o comportamento das páginas nesse site usando um navegador. Este tutorial mostra como criar uma Web Part visualmente usando o modelo de projeto de **Web Part Visual** do SharePoint no Visual Studio.

A Web Part que você criará exibe uma exibição de calendário mensal e uma caixa de seleção para cada lista de calendários no site. Os usuários podem especificar quais listas de calendário incluir no modo de exibição de calendário mensal marcando as caixas de seleção.

Este passo a passo ilustra as seguintes tarefas:

- Criar uma Web Part usando o modelo de projeto de **Web Part Visual** .
- Criando a Web Part usando o designer do Visual Web Developer no Visual Studio.
- Adicionar código para manipular os eventos de controles na Web Part.
- Testando a Web Part no SharePoint.

    > [!NOTE]
    > O computador pode mostrar diferentes nomes ou locais para alguns elementos da interface do usuário para o Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos

Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do Windows e do SharePoint.

## <a name="create-a-web-part-project"></a>Criar um projeto de Web Part

Primeiro, crie um projeto de Web Part usando o modelo de projeto de **Web Part Visual** .

1. Comece [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] usando a opção **Executar como administrador** .

2. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**.

     A caixa de diálogo **Novo Projeto** aparecerá.

3. Na caixa de diálogo **novo projeto** , em **Visual C#** ou **Visual Basic**, expanda **Office/SharePoint**e, em seguida, escolha a categoria **soluções do SharePoint** .

4. Na lista de modelos, escolha o modelo **SharePoint 2013-Web Part Visual** e, em seguida, escolha o botão **OK** .

     O **Assistente para personalização do SharePoint** é exibido. Usando esse assistente, você pode especificar o site que será usado para depurar o projeto e o nível de confiança da solução.

5. Na seção **o que é o nível de confiança para esta solução do SharePoint?** , escolha o botão de opção **implantar como uma solução de farm** .

6. Escolha o botão **concluir** para aceitar o site do SharePoint local padrão.

## <a name="designing-the-web-part"></a>Criando a Web Part

Projete a Web Part adicionando controles da caixa de **ferramentas** à superfície do designer do Visual Web Developer.

1. No designer do Visual Web Developer, escolha a guia **design** para alternar para modo de exibição de design.

2. Na barra de menus, escolha **Exibir**  >  **caixa de ferramentas**.

3. No nó **padrão** da caixa de **ferramentas**, escolha o controle **CheckBoxList** e execute uma das seguintes etapas:

    - Abra o menu de atalho para o controle **CheckBoxList** , escolha **copiar**, abra o menu de atalho da primeira linha no designer e, em seguida, escolha **colar**.

    - Arraste o controle **CheckBoxList** da **caixa de ferramentas**e conecte o controle à primeira linha no designer.

4. Repita a etapa anterior, mas mova um botão para a próxima linha do designer.

5. No designer, escolha o botão **Button1** .

6. Na barra de menus, escolha **Exibir**  >  **janela de propriedades**.

     A janela **Propriedades** é aberta.

7. Na propriedade **texto** do botão, insira **atualização**.

## <a name="handling-the-events-of-controls-on-the-web-part"></a>Manipulando os eventos de controles na Web Part

Adicione o código que permite ao usuário adicionar calendários à exibição do calendário mestre.

1. Realize um dos seguintes conjuntos de etapas:

   - No designer, clique duas vezes no botão **Atualizar** .

   - Na janela **Propriedades** do botão **Atualizar** , escolha o botão **eventos** . Na propriedade de **clique** , digite **Button1_Click**e, em seguida, escolha a tecla Enter.

     O arquivo de código de controle de usuário é aberto no editor de código e o `Button1_Click` manipulador de eventos é exibido. Posteriormente, você adicionará código a esse manipulador de eventos.

2. Adicione as instruções a seguir à parte superior do arquivo de código de controle de usuário.

     [!code-vb[SP_VisualWebPart#1](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#1)]
     [!code-csharp[SP_VisualWebPart#1](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#1)]

3. Adicione a seguinte linha de código à `VisualWebPart1` classe. Esse código declara um controle de exibição de calendário mensal.

     [!code-vb[SP_VisualWebPart#2](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#2)]
     [!code-csharp[SP_VisualWebPart#2](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#2)]

4. Substitua o `Page_Load` método da `VisualWebPart1` classe pelo código a seguir. Esse código executa as seguintes tarefas:

   - Adiciona uma exibição de calendário mensal ao controle de usuário.

   - Adiciona uma caixa de seleção para cada lista de calendário no site.

   - Especifica um modelo para cada tipo de item que aparece no modo de exibição de calendário.

     [!code-vb[SP_VisualWebPart#3](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#3)]
     [!code-csharp[SP_VisualWebPart#3](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#3)]

5. Substitua o `Button1_Click` método da `VisualWebPart1` classe pelo código a seguir. Esse código adiciona itens de cada calendário selecionado à exibição de calendário mestre.

     [!code-vb[SP_VisualWebPart#4](../sharepoint/codesnippet/VisualBasic/sp_visualwebpart.vb/visualwebpart1/visualwebpart1usercontrol.ascx.vb#4)]
     [!code-csharp[SP_VisualWebPart#4](../sharepoint/codesnippet/CSharp/sp_visualwebpart.cs/visualwebpart1/visualwebpart1usercontrol.ascx.cs#4)]

## <a name="test-the-web-part"></a>Testar a Web Part

Quando você executa o projeto, o site do SharePoint é aberto. A Web Part é adicionada automaticamente à galeria de Web Parts no SharePoint. Para testar esse projeto, você executará as seguintes tarefas:

- Adicione um evento a cada uma das duas listas de calendários separadas.
- Adicione a Web Part a uma página de Web Part.
- Especifique as listas a serem incluídas no modo de exibição de calendário mensal.

### <a name="to-add-events-to-calendar-lists-on-the-site"></a>Para adicionar eventos a listas de calendário no site

1. No Visual Studio, escolha a tecla **F5** .

     O site do SharePoint é aberto e a [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] barra de início rápido é exibida na página.

2. Na barra Início rápido, em **listas**, escolha o link **calendário** .

     A página **calendário** é exibida.

     Se nenhum link de calendário aparecer na barra de início rápido, escolha o link **conteúdo do site** . Se a página conteúdo do site não mostrar um item de **calendário** , crie um.

3. Na página calendário, escolha um dia e, em seguida, escolha o link **Adicionar** no dia selecionado para adicionar um evento.

4. Na caixa **título** , digite **evento no calendário padrão**e, em seguida, escolha o botão **salvar** .

5. Escolha o link **conteúdo do site** e, em seguida, escolha o bloco **Adicionar um aplicativo** .

6. Na página **criar** , escolha o tipo de **calendário** , nomeie o calendário e, em seguida, escolha o botão **criar** .

7. Adicione um evento ao novo calendário, nomeie o evento de evento **no calendário personalizado**e, em seguida, escolha o botão **salvar** .

### <a name="to-add-the-web-part-to-a-web-part-page"></a>Para adicionar a Web Part a uma página de Web Parts

1. Na página **conteúdo do site** , abra a pasta **páginas do site** .

2. Na faixa de seleção, escolha a guia **arquivos** , abra o menu **novo documento** e escolha o comando **página da Web Part** .

3. Na página **nova página de Web Parts** , nomeie a página **SampleWebPartPage. aspx**e, em seguida, escolha o botão **criar** .

     A página Web Part é exibida.

4. Na zona superior da página de Web Parts, escolha a guia **Inserir** e, em seguida, escolha o botão **Web Part** .

5. Escolha a pasta **personalizada** , escolha a Web Part **VisualWebPart1** e, em seguida, escolha o botão **Adicionar** .

     A Web Part aparece na página. Os seguintes controles aparecem na Web Part:

    - Um modo de exibição de calendário mensal.

    - Um botão de **atualização** .

    - Uma caixa de seleção de **calendário** .

    - Uma caixa de seleção de **calendário personalizado** .

### <a name="to-specify-lists-to-include-in-the-monthly-calendar-view"></a>Para especificar listas a serem incluídas no modo de exibição de calendário mensal

Na Web Part, especifique os calendários que você deseja incluir no modo de exibição de calendário mensal e, em seguida, escolha o botão **Atualizar** .

Os eventos de todos os calendários que você especificou aparecem no modo de exibição de calendário mensal.

## <a name="see-also"></a>Consulte também

[Criar Web Parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md) 
 [Como: criar uma Web Part](../sharepoint/how-to-create-a-sharepoint-web-part.md) 
 do SharePoint [Walkthrough: criar uma Web Part para o SharePoint](../sharepoint/walkthrough-creating-a-web-part-for-sharepoint.md)
