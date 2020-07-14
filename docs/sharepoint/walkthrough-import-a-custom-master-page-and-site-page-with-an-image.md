---
title: Importar página mestra personalizada & página do site com imagem
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 311124b2e0b81e70c4c2a7b40754207e6c66b749
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86015691"
---
# <a name="walkthrough-import-a-custom-master-page-and-site-page-with-an-image"></a>Walkthrough: importar uma página mestra personalizada e uma página do site com uma imagem
  Este tutorial demonstra como importar uma página mestra personalizada do SharePoint e uma página do site que tem uma imagem em um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint.

 Esta explicação passo a passo mostra como realizar as tarefas seguintes:

- Crie uma página mestra personalizada e uma página do site usando uma imagem no SharePoint Designer.

- Exporte uma página mestra personalizada, uma imagem e uma página do site para um arquivo de solução do SharePoint (*. wsp*).

- Importe e implante o arquivo *. wsp* em um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint usando o projeto importar pacote de solução do SharePoint.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você deve ter os seguintes componentes para concluir este passo a passos:

- Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e SharePoint.

- Visual Studio.

- SharePoint Designer 2010.

## <a name="create-items-in-sharepoint-designer"></a>Criar itens no SharePoint Designer
 Este exemplo mostra como criar três itens no SharePoint Designer para exportação: uma página mestra personalizada, uma página do site que faz referência à página mestra personalizada e um arquivo de imagem a ser exibido na página do site. A imagem é adicionada à pasta/images/no SharePoint.

#### <a name="to-create-a-custom-master-page-in-sharepoint-designer"></a>Para criar uma página mestra personalizada no SharePoint Designer

1. No SharePoint Designer, no painel de navegação, escolha o objeto site de **páginas mestras** .

2. Na faixa de seleção **páginas mestras** , escolha **página mestra em branco**.

3. Escolha a nova página mestra e, na faixa de faixas **páginas mestras** , escolha **Editar arquivo**.

4. Na parte inferior do SharePoint Designer, escolha a guia **código** .

5. Substitua a marcação existente pela marcação a seguir.

    ```aspx-csharp
    <%@ Master Language="C#" %>
    <%@ Register tagprefix="SharePoint" namespace="Microsoft.SharePoint.WebControls" assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <html dir="ltr">
    <head runat="server">
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <SharePoint:RobotsMetaTag runat="server" __designer:Preview="" __designer:Values="<P N='InDesign' T='False' /><P N='ID' T='ctl00' /><P N='Page' ID='1' /><P N='TemplateControl' ID='2' /><P N='AppRelativeTemplateSourceDirectory' R='-1' />"></SharePoint:RobotsMetaTag>
    <title>Web Page</title>
    </head>
    <body>
    <form id="form1" runat="server">
    <asp:ContentPlaceHolder id="ContentPlaceHolderMain"
            runat="server">
          </asp:ContentPlaceHolder>
    </form>
    </body>
    </html>
    ```

6. Salve a página, escolha a guia **páginas mestras** e renomeie a página mestra como **mybasic1. Master**.

## <a name="add-an-image-to-the-content-database-in-sharepoint-designer"></a>Adicionar uma imagem ao banco de dados de conteúdo no SharePoint Designer
 Agora você pode adicionar uma imagem a ser exibida na página do site. A imagem é implantada no banco de dados de conteúdo do SharePoint.

#### <a name="to-add-an-image-to-the-content-database-in-sharepoint-designer"></a>Para adicionar uma imagem ao banco de dados de conteúdo no SharePoint Designer

1. No painel de navegação, escolha o objeto do site **todos os arquivos** e, em seguida, no modo de exibição de árvore, escolha a pasta **imagens** .

2. Na faixa de opções **todos os arquivos** , escolha **importar arquivos**, escolha um arquivo de sua escolha e, em seguida, escolha o botão **OK** . Neste exemplo, o arquivo é denominado **myimg1.png**.

     Opcionalmente, você pode criar uma subpasta para ajudar a organizar as imagens.

3. Feche a caixa de diálogo **importar** .

## <a name="create-a-site-page"></a>Criar uma página do site
 Essa página de site básica usa a página mestra personalizada e exibe a imagem que você adicionou na etapa anterior.

#### <a name="to-create-a-site-page"></a>Para criar uma página do site

1. No painel de navegação, escolha o objeto **páginas do site** .

2. Na faixa de seleção **páginas** , escolha o botão **página** , escolha o tipo de página **aspx** e, em seguida, nomeie o novo arquivo **mycontentpage1. aspx**.

     Opcionalmente, você pode criar uma subpasta para ajudar a organizar as páginas do site.

3. Na lista páginas do site, escolha **MyContentPage1. aspx** para abrir sua página de propriedades e, na parte inferior da página, escolha o link **Editar arquivo** .

     Se uma mensagem aparecer e informar que essa página não contém regiões que são editáveis no modo de segurança e pergunta se você deseja abrir esta página no modo avançado, escolha o botão **Sim** .

4. Na parte inferior da página, escolha o botão **código** .

5. Substitua a marcação existente pela marcação a seguir.

    ```aspx-csharp
    <%@ Import Namespace="Microsoft.SharePoint.ApplicationPages" %>
    <%@ Register Tagprefix="SharePoint" Namespace="Microsoft.SharePoint.WebControls" Assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Register Tagprefix="Utilities" Namespace="Microsoft.SharePoint.Utilities" Assembly="Microsoft.SharePoint, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Register Tagprefix="asp" Namespace="System.Web.UI" Assembly="System.Web.Extensions, Version=3.5.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" %>
    <%@ Import Namespace="Microsoft.SharePoint" %>
    <%@ Assembly Name="Microsoft.Web.CommandUI, Version=14.0.0.0, Culture=neutral, PublicKeyToken=71e9bce111e9429c" %>
    <%@ Page Language="C#" Inherits="Microsoft.SharePoint.WebControls.LayoutsPageBase" MasterPageFile="../_catalogs/masterpage/mybasic1.master" meta:progid="SharePoint.WebPartPage.Document" %>

    <asp:Content ID="Main" ContentPlaceHolderID="ContentPlaceHolderMain" runat="server">
    <img alt="My Image" longdesc="My image from images folder" src="../images/myimg1.png" />
    </asp:Content>
    ```

6. Salve a página do site atualizada.

## <a name="export-the-items-from-sharepoint"></a>Exportar os itens do SharePoint
 Exporte os itens do SharePoint para um arquivo de solução do SharePoint (*. wsp*).

#### <a name="to-export-items-from-sharepoint-designer"></a>Para exportar itens do SharePoint Designer

1. No SharePoint Designer, no painel de navegação, escolha o objeto **site da equipe** e, em seguida, na faixa de seleção do **site** , escolha **salvar como modelo**.

2. Na caixa de diálogo **salvar como modelo** , insira um nome de arquivo e um nome de modelo, marque a caixa de seleção **incluir conteúdo** e, em seguida, escolha o botão **OK** .

     Isso salva o conteúdo do site no arquivo *. wsp* .

3. Depois que a solução for exportada, escolha o link **Galeria de soluções** para exibir a lista de arquivos de solução disponíveis.

4. Abra o menu de atalho para o novo arquivo *. wsp* e escolha **Salvar destino como** para salvá-lo no sistema.

## <a name="import-the-items-into-visual-studio"></a>Importar os itens para o Visual Studio
 Importe o arquivo *. wsp* para [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . Depois que o conteúdo é importado, você pode personalizá-lo, adicionar mais itens e, em seguida, implantá-lo.

#### <a name="to-import-items-from-the-wsp-file-into-visual-studio"></a>Para importar itens do arquivo. wsp para o Visual Studio

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , crie um projeto de **pacote de solução de importação do SharePoint 2010** .

2. Na página **selecionar itens a serem importados** , em **módulo** na coluna **tipo** , marque as caixas de seleção somente para os arquivos na tabela a seguir para importação.

   | Nome do Arquivo | Descrição |
   |------------------------|-----------------------------------------------|
   | \_catalogsmasterpage\_ | A página mestra personalizada. |
   | images_ | O arquivo de imagem no sistema de arquivos do SharePoint. |
   | SitePages_ | A página do site. |

3. Escolha o botão **concluir** para importar os itens selecionados.

4. Em **Gerenciador de soluções**, escolha o \_ \_ nó catalogsmasterpage e defina o valor de sua propriedade de **resolução de conflito de implantação** como **automática**.

    Isso ajuda a garantir que todos os conflitos de implantação sejam resolvidos automaticamente.

5. Se sua nova página mestra tiver o mesmo nome de uma página existente, verifique se a página existente não está marcada como uma página mestra padrão ou uma página mestra personalizada no SharePoint Designer.

    Se uma página mestra existente estiver marcada como página mestra padrão ou página mestra personalizada, você receberá um erro de implantação que indica que a página mestra não pode ser excluída. Para evitar esse problema, faça o seguinte:

   - Se a página mestra existente estiver definida como página mestra padrão, defina temporariamente outra página mestra como página mestra padrão. Depois de implantar os arquivos no SharePoint, defina sua nova página mestra como página mestra padrão.

   - Se a página mestra existente for definida como página mestra personalizada, defina temporariamente outra página mestra como página mestra personalizada. Depois de implantar os arquivos no SharePoint, defina sua nova página mestra como página mestra personalizada.

6. Na barra de menus, escolha **Compilar**  >  **implantar solução**.

7. Abra o site do SharePoint para exibir os itens implantados.

   Uma maneira alternativa de importar arquivos [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e implantá-los no SharePoint é adicionar os arquivos em módulos no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] . [!INCLUDE[crdefault](../sharepoint/includes/crdefault-md.md)][Como importar uma página mestra ou tema](../sharepoint/how-to-import-a-master-page-or-theme.md) e [usar módulos para incluir arquivos na solução](../sharepoint/using-modules-to-include-files-in-the-solution.md).

## <a name="see-also"></a>Consulte também
- [Importando itens de um site existente do SharePoint](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
- [Criar controles reutilizáveis para Web Parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
