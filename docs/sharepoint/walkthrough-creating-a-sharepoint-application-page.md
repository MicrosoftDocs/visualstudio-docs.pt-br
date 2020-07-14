---
title: 'Walkthrough: criando uma página de aplicativo do SharePoint | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 76375c15077bf672eaba01c840ba406228046435
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016488"
---
# <a name="walkthrough-create-a-sharepoint-application-page"></a>Walkthrough: criar uma página de aplicativo do SharePoint

Uma página de aplicativo é uma forma especializada de uma página ASP.NET. As páginas de aplicativo contêm conteúdo que é mesclado com uma página mestra do SharePoint. Para obter mais informações, consulte [criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).

Este tutorial mostra como criar uma página de aplicativo e depurá-la usando um site do SharePoint local. Esta página mostra todos os itens que cada usuário criou ou modificou em todos os sites no farm de servidores.

Este passo a passo ilustra as seguintes tarefas:

- Criando um projeto do SharePoint.
- Adicionando uma página de aplicativo ao projeto do SharePoint.
- Adicionar controles ASP.NET à página do aplicativo.
- Adicionando código por trás dos controles ASP.NET.
- Testando a página do aplicativo.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, consulte [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos

- Edições com suporte do Windows e do SharePoint.

## <a name="create-a-sharepoint-project"></a>Criar um projeto do SharePoint

Primeiro, crie um **projeto do SharePoint vazio**. Posteriormente, você adicionará um item de **página de aplicativo** a este projeto.

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. Abra a caixa de diálogo **novo projeto** , expanda o nó **Office/SharePoint** sob o idioma que você deseja usar e, em seguida, escolha o nó **soluções do SharePoint** .

3. No painel **modelos instalados do Visual Studio** , escolha o modelo de **projeto do SharePoint 2010-vazio** . Nomeie o projeto **MySharePointProject**e, em seguida, escolha o botão **OK** .

     O **Assistente para personalização do SharePoint** é exibido. Este assistente permite que você selecione o site que será usado para depurar o projeto e o nível de confiança da solução.

4. Escolha o botão de opção **implantar como uma solução de farm** e, em seguida, escolha o botão **concluir** para aceitar o site do SharePoint local padrão.

## <a name="create-an-application-page"></a>Criar uma página de aplicativo

Para criar uma página de aplicativo, adicione um item de **página de aplicativo** ao projeto.

1. Em **Gerenciador de soluções**, escolha o projeto **MySharePointProject** .

2. Na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

3. Na caixa de diálogo **Adicionar novo item** , escolha a **página do aplicativo (modelo somente solução de farm** .

4. Nomeie a página **SearchItems**e, em seguida, escolha o botão **Adicionar** .

     O designer do Visual Web Developer exibe a página do aplicativo no modo de exibição de **origem** , onde você pode ver os elementos HTML da página. O designer exibe a marcação para vários <xref:System.Web.UI.WebControls.Content> controles. Cada controle é mapeado para um <xref:System.Web.UI.WebControls.ContentPlaceHolder> controle que é definido na página mestra do aplicativo padrão.

## <a name="design-the-layout-of-the-application-page"></a>Criar o layout da página do aplicativo

O item de página do aplicativo permite que você use um designer para adicionar controles ASP.NET à página do aplicativo. Esse designer é o mesmo designer usado no Visual Web Developer. Adicione um rótulo, uma lista de botões de opção e uma tabela à exibição de **origem** do designer e, em seguida, defina as propriedades como você faria ao criar qualquer página ASP.NET padrão.

1. Na barra de menus, escolha **Exibir**  >  **caixa de ferramentas**.

2. No nó padrão da caixa de **ferramentas**, execute uma das seguintes etapas:

    - Abra o menu de atalho para o item de **rótulo** , escolha **copiar**, abra o menu de atalho da linha sob o controle de conteúdo **PlaceHolderMain** no designer e, em seguida, escolha **colar**.

    - Arraste o item de **rótulo** da **caixa de ferramentas** para o corpo do controle de conteúdo **PlaceHolderMain** .

3. Repita a etapa anterior para adicionar um item **DropDownList** e um item de **tabela** ao controle de conteúdo **PlaceHolderMain** .

4. No designer, altere o valor do `Text` atributo do controle rótulo para **Mostrar todos os itens**.

5. No designer, substitua o `<asp:DropDownList>` elemento pelo seguinte XML.

    ```xml
    <asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="true"
     OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged">
        <asp:ListItem Text="Created by me" Value="Author"></asp:ListItem>
        <asp:ListItem Text="Modified by me" Value="Editor"></asp:ListItem>
    </asp:DropDownList>
    ```

## <a name="handle-the-events-of-controls-on-the-page"></a>Manipular os eventos de controles na página

Manipule controles em uma página de aplicativo da mesma forma que faria com qualquer página do ASP.NET. Neste procedimento, você manipulará o `SelectedIndexChanged` evento da lista suspensa.

1. No menu **Exibir** , escolha **código**.

     O arquivo de código de página do aplicativo é aberto no editor de código.

2. Adicione o método a seguir à classe `SearchItems`. Esse código manipula o <xref:System.Web.UI.WebControls.ListControl.SelectedIndexChanged> evento do <xref:System.Web.UI.WebControls.DropDownList> chamando um método que você criará mais tarde neste passo a passos.

     [!code-vb[SP_ApplicationPage#5](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#5)]
     [!code-csharp[SP_ApplicationPage#5](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#5)]

3. Adicione as instruções a seguir à parte superior do arquivo de código de página do aplicativo.

     [!code-vb[SP_ApplicationPage#1](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#1)]
     [!code-csharp[SP_ApplicationPage#1](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#1)]

4. Adicione o método a seguir à classe `SearchItems`. Esse método itera em todos os sites no farm de servidores e procura itens criados ou modificados pelo usuário atual.

     [!code-vb[SP_ApplicationPage#2](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#2)]
     [!code-csharp[SP_ApplicationPage#2](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#2)]

5. Adicione o método a seguir à classe `SearchItems`. Esse método exibe itens criados ou modificados pelo usuário atual na tabela.

     [!code-vb[SP_ApplicationPage#3](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#3)]
     [!code-csharp[SP_ApplicationPage#3](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#3)]

## <a name="test-the-application-page"></a>Testar a página do aplicativo

Quando você executa o projeto, o site do SharePoint é aberto e a página do aplicativo é exibida.

1. No **Gerenciador de soluções**, abra o menu de atalho da página do aplicativo e escolha **definir como item de inicialização**.

2. Pressione a tecla **F5**.

     O site do SharePoint é aberto.

3. Na página do aplicativo, escolha a opção **modificado por mim** .

     A página do aplicativo é atualizada e exibe todos os itens que você modificou em todos os sites no farm de servidores.

4. Na página do aplicativo, escolha **criado por mim** na lista.

     A página do aplicativo é atualizada e exibe todos os itens que você criou em todos os sites no farm de servidores.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre páginas de aplicativo do SharePoint, consulte [criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).

Você pode aprender mais sobre como criar conteúdo de página do SharePoint usando o Visual Web Designer a partir destes tópicos:

- [Crie Web Parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md).

- [Crie controles reutilizáveis para Web Parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md).

## <a name="see-also"></a>Consulte também

[Como: criar uma página](../sharepoint/how-to-create-an-application-page.md) 
 de aplicativo [Tipo de página de _layouts de aplicativo](/previous-versions/office/aa979604(v=office.14))
