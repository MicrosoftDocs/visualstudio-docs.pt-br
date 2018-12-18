---
title: 'Passo a passo: Criando uma página de aplicativo do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- application pages [SharePoint development in Visual Studio], developing
- application pages [SharePoint development in Visual Studio], creating
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 52ff6b3431ac3f87c85eefcf728cfe4c4875f884
ms.sourcegitcommit: 55f7ce2d5d2e458e35c45787f1935b237ee5c9f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/22/2018
ms.locfileid: "42634781"
---
# <a name="walkthrough-create-a-sharepoint-application-page"></a>Passo a passo: Criar uma página de aplicativo do SharePoint
 
Uma página de aplicativo é uma forma especializada de uma página ASP.NET. Páginas de aplicativos têm conteúdo que é mesclado com uma página mestra do SharePoint. Para obter mais informações, consulte [criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).

Este passo a passo mostra como criar uma página de aplicativo e depurá-lo por meio de um site do SharePoint local. Esta página mostra todos os itens que cada usuário criou ou modificou em todos os sites do farm de servidores.

Esta explicação passo a passo ilustra as seguintes tarefas:

- Criando um projeto do SharePoint.
- Adicionando uma página de aplicativo para o projeto do SharePoint.
- Adicionando controles ASP.NET à página do aplicativo.
- Adicionando código atrás dos controles ASP.NET.
- Testando a página do aplicativo.

> [!NOTE]
> Seu computador pode mostrar diferentes nomes ou locais para alguns dos elementos de interface do usuário do Visual Studio nas instruções a seguir. A edição do Visual Studio que você possui e as configurações que você usa determinam esses elementos. Para obter mais informações, confira [Personalizar o IDE do Visual Studio](../ide/personalizing-the-visual-studio-ide.md).

## <a name="prerequisites"></a>Pré-requisitos

- Edições com suporte do Windows e do SharePoint.

## <a name="create-a-sharepoint-project"></a>Criar um projeto do SharePoint

Primeiro, crie uma **projeto vazio do SharePoint**. Posteriormente, você adicionará um **página de aplicativo** item a este projeto.

1. Inicie o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].

2. Abra o **novo projeto** diálogo caixa, expanda o **Office/SharePoint** nó sob o idioma que você deseja usar e, em seguida, escolha o **soluções do SharePoint** nó.

3. No **Visual Studio Installed Templates** painel, escolha o **SharePoint 2010 - projeto vazio** modelo. Nomeie o projeto **MySharePointProject**e, em seguida, escolha o **Okey** botão.

     O **Assistente para personalização do SharePoint** é exibida. Este assistente permite que você selecione o site que você usará para depurar o projeto e o nível de confiança da solução.

4. Escolha o **implantar como uma solução de farm** botão de opção e, em seguida, escolha o **concluir** botão para aceitar o site do SharePoint local padrão.

## <a name="create-an-application-page"></a>Criar uma página de aplicativo

Para criar uma página de aplicativo, adicione uma **página de aplicativo** item ao projeto.

1. Na **Gerenciador de soluções**, escolha o **MySharePointProject** projeto.

2. Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.

3. No **Adicionar Novo Item** diálogo caixa, escolha o **página de aplicativo (somente solução de Farm** modelo.

4. Nomeie a página **SearchItems**e, em seguida, escolha o **Add** botão.

     O designer do Visual Web Developer exibe a página de aplicativo no **origem** modo em que você pode ver os elementos da página HTML. O designer exibe a marcação para vários <xref:System.Web.UI.WebControls.Content> controles. Cada controle é mapeado para um <xref:System.Web.UI.WebControls.ContentPlaceHolder> controle que é definido na página mestra padrão do aplicativo.

## <a name="design-the-layout-of-the-application-page"></a>Criar o layout da página do aplicativo

O item de página de aplicativo permite que você use um designer para adicionar controles ASP.NET à página do aplicativo. Esse designer é o mesmo designer usado no Visual Web Developer. Adicionar um rótulo, uma lista de botão de rádio e uma tabela para o **origem** exibir do designer e, em seguida, defina propriedades exatamente como você faria quando você cria alguma página ASP.NET padrão.

1. Na barra de menus, escolha **modo de exibição** > **caixa de ferramentas**.

2. No nó do padrão de **caixa de ferramentas**, execute uma das seguintes etapas:

    - Abra o menu de atalho para o **rótulo** item, escolha **cópia**, abra o menu de atalho para a linha sob o **PlaceHolderMain** controle no designer, de conteúdo e, em seguida, escolher **colar**.

    - Arraste o **rótulo** item do **caixa de ferramentas** no corpo do **PlaceHolderMain** controle de conteúdo.

3. Repita a etapa anterior para adicionar um **DropDownList** item e uma **tabela** item para o **PlaceHolderMain** controle de conteúdo.

4. No designer, altere o valor da `Text` atributo do controle de rótulo para **Show All Items**.

5. No designer, substitua o `<asp:DropDownList>` elemento com o XML a seguir.

    ```xml
    <asp:DropDownList ID="DropDownList1" runat="server" AutoPostBack="true"
     OnSelectedIndexChanged="DropDownList1_SelectedIndexChanged">
        <asp:ListItem Text="Created by me" Value="Author"></asp:ListItem>
        <asp:ListItem Text="Modified by me" Value="Editor"></asp:ListItem>
    </asp:DropDownList>
    ```

## <a name="handle-the-events-of-controls-on-the-page"></a>Manipular os eventos dos controles na página

Manipule os controles em uma página de aplicativo como faria qualquer página do ASP.NET. Neste procedimento, você irá manipular o `SelectedIndexChanged` eventos da lista suspensa.

1. Sobre o **modo de exibição** menu, escolha **código**.

     O arquivo de código da página de aplicativo é aberto no Editor de códigos.

2. Adicione o seguinte método à classe `SearchItems`. Esse código manipula o <xref:System.Web.UI.WebControls.ListControl.SelectedIndexChanged> eventos do <xref:System.Web.UI.WebControls.DropDownList> chamando um método que você criará posteriormente neste passo a passo.

     [!code-vb[SP_ApplicationPage#5](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#5)]
     [!code-csharp[SP_ApplicationPage#5](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#5)]

3. Adicione as seguintes instruções à parte superior do arquivo de código de página do aplicativo.

     [!code-vb[SP_ApplicationPage#1](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#1)]
     [!code-csharp[SP_ApplicationPage#1](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#1)]

4. Adicione o seguinte método à classe `SearchItems`. Esse método itera em todos os sites do farm de servidores e procura por itens criados ou modificados pelo usuário atual.

     [!code-vb[SP_ApplicationPage#2](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#2)]
     [!code-csharp[SP_ApplicationPage#2](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#2)]

5. Adicione o seguinte método à classe `SearchItems`. Esse método exibe os itens criados ou modificados pelo usuário atual na tabela.

     [!code-vb[SP_ApplicationPage#3](../sharepoint/codesnippet/VisualBasic/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.vb#3)]
     [!code-csharp[SP_ApplicationPage#3](../sharepoint/codesnippet/CSharp/sp_applicationpage/layouts/sp_applicationpage/SearchItems.aspx.cs#3)]

## <a name="test-the-application-page"></a>Testar a página de aplicativo

Quando você executa o projeto, o site do SharePoint é aberta e a página de aplicativo é exibida.

1. Na **Gerenciador de soluções**, abra o menu de atalho para a página de aplicativo e, em seguida, escolha **definir como Item de inicialização**.

2. Pressione a tecla **F5**.

     Abre o site do SharePoint.

3. Na página do aplicativo, escolha o **modificado por mim** opção.

     A página de aplicativo atualiza e exibe todos os itens que você modificou em todos os sites do farm de servidores.

4. Na página do aplicativo, escolha **criados por mim** na lista.

     A página de aplicativo atualiza e exibe todos os itens que você criou em todos os sites do farm de servidores.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre páginas de aplicativo do SharePoint, consulte [criar páginas de aplicativo para o SharePoint](../sharepoint/creating-application-pages-for-sharepoint.md).

Você pode aprender mais sobre como projetar o conteúdo da página do SharePoint usando o Visual Web Designer nesses tópicos:

- [Criar web parts para SharePoint](../sharepoint/creating-web-parts-for-sharepoint.md).

- [Criar controles reutilizáveis para web parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md).

## <a name="see-also"></a>Consulte também

[Como: criar uma página de aplicativo](../sharepoint/how-to-create-an-application-page.md)  
[Tipo de página layouts do aplicativo](http://go.microsoft.com/fwlink/?LinkID=169274)
