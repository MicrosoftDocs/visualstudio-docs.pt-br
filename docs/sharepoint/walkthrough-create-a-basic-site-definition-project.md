---
title: 'Walkthrough: criar um projeto básico de definição de site | Microsoft Docs'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, site definitions
- site definitions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: d1c06f4df5d1efe06ad2537bd2e65f2c239f3be2
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86016768"
---
# <a name="walkthrough-create-a-basic-site-definition-project"></a>Walkthrough: criar um projeto de definição de site básico
  Este tutorial mostra como criar uma definição de site básica que contém uma Web Part Visual com alguns controles. Para fins de clareza, a Web Part Visual que você cria tem apenas alguns controles. No entanto, você pode criar definições de site do SharePoint mais sofisticadas que incluem mais funcionalidade.

 Este tutorial demonstra as seguintes tarefas:

- Criando uma definição de site usando o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] modelo de projeto.

- Criar um site do SharePoint usando uma definição de site no SharePoint.

- Adicionar uma Web Part Visual à solução.

- Personalizando a página default. aspx do site adicionando a nova Web Part Visual a ela.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do Microsoft Windows e do SharePoint. Para obter mais informações, consulte Requirements for Developing SharePoint Solutions.

- Visual Studio.

## <a name="create-a-site-definition-solution"></a>Criar uma solução de definição de site
 Primeiro, crie o projeto de definição de site no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] .

#### <a name="to-create-a-site-definition-project"></a>Para criar um projeto de definição do site

1. Na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto**. Se o IDE estiver definido para usar Visual Basic configurações de desenvolvimento, na barra de menus, escolha **arquivo**  >  **novo projeto**.

    A caixa de diálogo **Novo Projeto** aparecerá.

2. Expanda o nó do **Visual C#** ou o nó **Visual Basic** , expanda o nó do **SharePoint** e escolha o nó **2010** .

3. Na lista **modelos** , escolha o modelo de **projeto do SharePoint 2010** .

4. Na caixa **nome** , digite **TestSiteDef**e, em seguida, escolha o botão **OK** .

    O **Assistente para personalização do SharePoint** é exibido.

5. Na página **especificar o site e o nível de segurança para depuração** , insira a URL do site do SharePoint onde você deseja depurar a definição do site ou use o local padrão (<em>nome do sistema</em>http:///).

6. Na seção **o que é o nível de confiança para esta solução do SharePoint?** , escolha o botão de opção **implantar como uma solução de farm** .

    Todos os projetos de definição de site devem ser implantados como soluções de farm. Para obter mais informações sobre soluções em área restrita versus soluções de farm, consulte [Considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).

7. Escolha o botão **Concluir**.

    O projeto aparece no **Gerenciador de soluções**.

8. Em **Gerenciador de soluções**, escolha o nó do projeto e, na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

9. Em **Visual C#** ou **Visual Basic**, expanda o nó do **SharePoint** e escolha o nó **2010** .

10. No painel **modelos** , escolha o modelo **definição de site** , deixe o **nome** como **SiteDefinition1**e, em seguida, escolha o botão **Adicionar** .

## <a name="create-a-visual-web-part"></a>Criar uma Web Part Visual
 Em seguida, crie uma Web Part Visual para aparecer na página principal da definição de site.

#### <a name="to-create-a-visual-web-part"></a>Para criar uma Web Part Visual

1. Em **Gerenciador de soluções**, escolha o botão **Mostrar todos os arquivos** .

2. Escolha o nó do projeto **SiteDefinition1** e, na barra de menus, escolha **projeto**  >  **Adicionar novo item**.

     A caixa de diálogo **Adicionar Novo Item** aparecerá.

3. Expanda o nó do **Visual C#** ou o nó **Visual Basic** , expanda o nó do **SharePoint** e escolha o nó **2010** .

4. Na lista de modelos, escolha o modelo de **Web Part Visual** , mantenha o nome padrão VisualWebPart1 e, em seguida, escolha o botão **Adicionar** .

     O arquivo *VisualWebPart1. ascx* é aberto.

5. Na parte inferior de *VisualWebPart1. ascx*, adicione a marcação a seguir para adicionar três controles ao formulário: uma caixa de texto, um botão e um rótulo:

    ```aspx-csharp
    <table>
      <tr>
        <td>
          <asp:TextBox runat="server" ID="tbName"></asp:TextBox>
        </td>
        <td>
          <asp:Button runat="server" ID="btnSubmit" Text = "Change Label Text" OnClick="btnSubmit_Click"></asp:Button>
        </td>
        <td>
          <asp:Label runat="server" ID="lblName"></asp:Label>
        </td>
      </tr>
    </table>
    ```

6. Em *VisualWebPart1. ascx*, abra o arquivo *VisualWebPart1.ascx.cs* (para [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)] ) ou *VisualWebPart1. ascx. vb* (para [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)] ) e, em seguida, adicione o seguinte código:

     [!code-vb[SP_SimpleSiteDef#1](../sharepoint/codesnippet/VisualBasic/testsitedefvb/sitedefinition/visualwebpart1/visualwebpart1usercontrol.ascx.vb#1)]
     [!code-csharp[SP_SimpleSiteDef#1](../sharepoint/codesnippet/CSharp/testsitedef/sitedefinition/visualwebpart1/visualwebpart1usercontrol.ascx.cs#1)]

     Esse código adiciona a funcionalidade para o clique no botão da Web Part.

## <a name="add-the-visual-web-part-to-the-default-aspx-page"></a>Adicionar a Web Part Visual à página ASPX padrão
 Em seguida, adicione a Web Part Visual à página ASPX padrão da definição de site.

#### <a name="to-add-a-visual-web-part-to-the-default-aspx-page"></a>Para adicionar uma Web Part Visual à página ASPX padrão

1. Abra a página default. aspx e, em seguida, adicione a seguinte linha sob a `WebPartPages` marca:

    ```aspx-csharp
    <%@ Register Tagprefix="MyWebPartControls" Namespace="TestSiteDef.VisualWebPart1" Assembly="$SharePoint.Project.AssemblyFullName$" %>
    ```

     Essa linha associa o nome MyWebPartControls com a Web Part e seu código. O parâmetro *namespace* corresponde ao namespace usado no arquivo de código *VisualWebPart1. ascx* .

2. Após o `</asp:Content>` elemento, substitua a `ContentPlaceHolderId="PlaceHolderMain"` seção inteira e seu conteúdo pelo seguinte código:

    ```aspx-csharp
    <asp:Content ID="Content1" ContentPlaceHolderId="PlaceHolderMain" runat="server">
        <MyWebPartControls:VisualWebPart1 runat="server" />
    </asp:Content>
    ```

     Esse código cria uma referência para a Web Part Visual que você criou anteriormente.

3. No **Gerenciador de soluções**, abra o menu de atalho para o nó **SiteDefinition1** e escolha **definir como item de inicialização**.

## <a name="deploy-and-run-the-site-definition-solution"></a>Implantar e executar a solução de definição de site
 Em seguida, implante o projeto no SharePoint e, em seguida, execute o projeto.

#### <a name="to-deploy-and-run-the-site-definition"></a>Para implantar e executar a definição do site

- Na barra de menus, escolha **Compilar**  >  **implantar TestSiteDef**.

- Pressione a tecla **F5**.

     O Visual Studio compila o código, adiciona seus recursos, empacota todos os arquivos em um arquivo de solução do SharePoint (WSP) e implanta o arquivo WSP no servidor do SharePoint. Em seguida, o SharePoint instala os arquivos e ativa os recursos.

## <a name="create-a-site-based-on-the-site-definition"></a>Criar um site com base na definição do site
 Em seguida, crie um site usando a nova definição de site.

#### <a name="to-create-a-site-by-using-the-site-definition"></a>Para criar um site usando a definição do site

1. No site do SharePoint, a página novo site do SharePoint é exibida.

2. Na seção **título e descrição** , insira **meu novo site** para o título e uma descrição do site.

3. Na seção **endereço do site** , digite **mynewsite** na caixa **nome da URL** .

4. Na seção **modelo** , escolha a guia **personalizações do SharePoint** .

5. Na lista **selecionar um modelo** , escolha **SiteDefinition1**.

6. Deixe as outras configurações com seus valores padrão e, em seguida, escolha o botão **criar** .

     O novo site é exibido.

## <a name="test-the-new-site"></a>Testar o novo site
 Em seguida, teste o novo site para verificar se ele funciona corretamente.

#### <a name="to-test-the-new-site"></a>Para testar o novo site

- Na página ASPX padrão, insira algum texto e, em seguida, escolha o botão **alterar texto do rótulo** ao lado da caixa de texto.

     O texto aparece no rótulo no lado direito do botão.

## <a name="see-also"></a>Consulte também
- [Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
