---
title: 'Passo a passo: Criar um projeto de definição de Site básico | Microsoft Docs'
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
- SharePoint development in Visual Studio, site definitions
- site definitions [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 8a9a879db7c1d24dbfd8312dbc75d9b0bbaa8803
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49844390"
---
# <a name="walkthrough-create-a-basic-site-definition-project"></a>Passo a passo: Criar um projeto de definição de site básico
  Este passo a passo mostra como criar uma definição de site básico que contém uma Web part visual com alguns controles nele. Para clareza, a Web part visual que você cria tem apenas alguns controles. No entanto, você pode criar definições de site do SharePoint mais sofisticadas que incluem mais funcionalidade.  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
- Criando uma definição de site usando o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] modelo de projeto.  
  
- Criando um site do SharePoint por meio de uma definição de site no SharePoint.  
  
- Adicionando uma Web part visual à solução.  
  
- Personalizando a página de Default. aspx do site com a adição de nova Web part visual.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Edições com suporte do Microsoft Windows e do SharePoint. Para obter mais informações, consulte requisitos para desenvolver soluções do SharePoint.  
  
-   Visual Studio.  
  
## <a name="create-a-site-definition-solution"></a>Criar uma solução de definição de site
 Primeiro, crie o projeto de definição de site no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
#### <a name="to-create-a-site-definition-project"></a>Para criar um projeto de definição do site  
  
1. Na barra de menus, selecione **Arquivo** > **Novo** > **Projeto**. Se o seu IDE for definido para usar configurações de desenvolvimento do Visual Basic, na barra de menus, escolha **arquivo** > **novo projeto**.  
  
    A caixa de diálogo **Novo Projeto** é exibida.  
  
2. Expanda o **Visual c#** nó ou o **Visual Basic** nó, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
3. No **modelos** , escolha o **o projeto do SharePoint 2010** modelo.  
  
4. No **nome** , digite **TestSiteDef**e, em seguida, escolha o **Okey** botão.  
  
    O **Assistente para personalização do SharePoint** é exibida.  
  
5. Sobre o **especificar o nível de site e segurança para depuração** página, insira a URL do site do SharePoint onde você deseja depurar a definição de site ou usar o local padrão (http://<em>nome do sistema</em>/).  
  
6. No **qual é o nível de confiança para essa solução do SharePoint?** , escolha o **implantar como uma solução de farm** botão de opção.  
  
    Todos os projetos de definição de site devem ser implantados como soluções de farm. Para obter mais informações sobre soluções em área restrita em comparação com soluções de farm, consulte [considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).  
  
7. Escolha o **concluir** botão.  
  
    O projeto aparece na **Gerenciador de soluções**.  
  
8. Na **Gerenciador de soluções**, escolha o nó do projeto e, em seguida, na barra de menus, escolha **Project** > **Add New Item**.  
  
9. Em um **Visual c#** ou **Visual Basic**, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
10. No **modelos** painel, escolha o **definição de Site** modelo, deixe o **nome** como **SiteDefinition1**e, em seguida, escolha o  **Adicionar** botão.  
  
## <a name="create-a-visual-web-part"></a>Criar uma web part visual
 Em seguida, crie uma Web part visual para aparecer na página principal da definição de site.  
  
#### <a name="to-create-a-visual-web-part"></a>Para criar uma web part visual
  
1.  Na **Gerenciador de soluções**, escolha o **Mostrar todos os arquivos** botão.  
  
2.  Escolha o **SiteDefinition1** nó do projeto e, em seguida, na barra de menus, escolha **Project** > **Add New Item**.  
  
     A caixa de diálogo **Adicionar Novo Item** é exibida.  
  
3.  Expanda o **Visual c#** nó ou o **Visual Basic** nó, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
4.  Na lista de modelos, escolha o **Web Part Visual** modelo, mantenha o padrão nomeie VisualWebPart1 e, em seguida, escolha o **Add** botão.  
  
     O *VisualWebPart1.ascx* arquivo é aberto.  
  
5.  Na parte inferior da *VisualWebPart1.ascx*, adicione a seguinte marcação para adicionar três controles ao formulário: uma caixa de texto, um botão e um rótulo:  
  
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
  
6.  Sob *VisualWebPart1.ascx*, abra o *VisualWebPart1.ascx.cs* arquivo (para [!INCLUDE[csprcs](../sharepoint/includes/csprcs-md.md)]) ou *VisualWebPart1.ascx.vb* (para [!INCLUDE[vbprvb](../sharepoint/includes/vbprvb-md.md)]) e, em seguida, adicione o código a seguir:  
  
     [!code-vb[SP_SimpleSiteDef#1](../sharepoint/codesnippet/VisualBasic/testsitedefvb/sitedefinition/visualwebpart1/visualwebpart1usercontrol.ascx.vb#1)]
     [!code-csharp[SP_SimpleSiteDef#1](../sharepoint/codesnippet/CSharp/testsitedef/sitedefinition/visualwebpart1/visualwebpart1usercontrol.ascx.cs#1)]  
  
     Esse código adiciona a funcionalidade de clique do botão da web part.  
  
## <a name="add-the-visual-web-part-to-the-default-aspx-page"></a>Adicionar a web part visual à página ASPX padrão
 Em seguida, adicione a Web part visual à página ASPX padrão da definição de site.  
  
#### <a name="to-add-a-visual-web-part-to-the-default-aspx-page"></a>Para adicionar uma web part visual à página ASPX padrão
  
1.  Abra a página Default. aspx e, em seguida, adicione a seguinte linha sob o `WebPartPages` marca:  
  
    ```aspx-csharp  
    <%@ Register Tagprefix="MyWebPartControls" Namespace="TestSiteDef.VisualWebPart1" Assembly="$SharePoint.Project.AssemblyFullName$" %>  
    ```  
  
     Esta linha associa o nome MyWebPartControls com a Web part e seu código. O *Namespace* parâmetro corresponda ao namespace que é usado na *VisualWebPart1.ascx* arquivo de código.  
  
2.  Após o `</asp:Content>` elemento, substitua todo o `ContentPlaceHolderId="PlaceHolderMain"` seção e seu conteúdo pelo seguinte código:  
  
    ```aspx-csharp  
    <asp:Content ID="Content1" ContentPlaceHolderId="PlaceHolderMain" runat="server">  
        <MyWebPartControls:VisualWebPart1 runat="server" />      
    </asp:Content>  
    ```  
  
     Esse código cria uma referência para a Web part visual que você criou anteriormente.  
  
3.  Na **Gerenciador de soluções**, abra o menu de atalho para o **SiteDefinition1** nó e, em seguida, escolha **definir como Item de inicialização**.  
  
## <a name="deploy-and-run-the-site-definition-solution"></a>Implantar e executar a solução de definição de site
 Em seguida, implantar o projeto do SharePoint e, em seguida, execute o projeto.  
  
#### <a name="to-deploy-and-run-the-site-definition"></a>Para implantar e executar a definição do site  
  
-   Na barra de menus, escolha **construir** > **TestSiteDef implantar**.  
  
-   Pressione a tecla **F5**.  
  
     Visual Studio compila o código, adiciona a seus recursos, empacota todos os arquivos em um arquivo de solução (WSP) do SharePoint e implanta o arquivo WSP para o SharePoint Server. SharePoint, em seguida, instala os arquivos e, em seguida, ativa os recursos.  
  
## <a name="create-a-site-based-on-the-site-definition"></a>Criar um site com base na definição do site
 Em seguida, crie um site usando a nova definição de site.  
  
#### <a name="to-create-a-site-by-using-the-site-definition"></a>Para criar um site usando a definição do site  
  
1.  No site do SharePoint, é exibida a página Novo Site do SharePoint.  
  
2.  No **Title e Description** , digite **meu novo Site** para o título e uma descrição do site.  
  
3.  No **endereço do Site** , digite **mynewsite** no **nome da URL** caixa.  
  
4.  No **modelo** , escolha o **personalizações do SharePoint** guia.  
  
5.  No **selecione um modelo** , escolha **SiteDefinition1**.  
  
6.  Deixe as outras configurações em seus valores padrão e, em seguida, escolha o **criar** botão.  
  
     O novo site é exibido.  
  
## <a name="test-the-new-site"></a>Testar o novo site
 Em seguida, teste o novo site para verificar se ele funciona corretamente.  
  
#### <a name="to-test-the-new-site"></a>Para testar o novo site  
  
-   Na página ASPX padrão, digite algum texto e, em seguida, escolha o **alterar o texto de rótulo** botão ao lado da caixa de texto.  
  
     O texto é exibido no rótulo à direita do botão.  
  
## <a name="see-also"></a>Consulte também
 [Como: criar um receptor de eventos](../sharepoint/how-to-create-an-event-receiver.md)   
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)  
  
