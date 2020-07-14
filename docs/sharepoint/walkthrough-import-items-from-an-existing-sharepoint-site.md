---
title: 'Walkthrough: importar itens de um site existente do SharePoint | Microsoft Docs'
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
ms.openlocfilehash: 46bc2ceacfde599a70b4e84bba134c4a4d5f9757
ms.sourcegitcommit: f9e44f5ab6a1dfb56c945c9986730465e1adb6fc
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86017114"
---
# <a name="walkthrough-import-items-from-an-existing-sharepoint-site"></a>Walkthrough: importar itens de um site existente do SharePoint
  Este tutorial demonstra como importar itens de um site existente do SharePoint para um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint.

 Este tutorial demonstra as seguintes tarefas:

- Personalização de um site do SharePoint adicionando uma coluna de site personalizada (também conhecida como um *campo*.

- Exportando um site do SharePoint para um arquivo. wsp.

- Importar o arquivo. wsp para [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] o SharePoint usando o projeto de importação. wsp.

  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

## <a name="prerequisites"></a>Pré-requisitos
 Você precisará dos seguintes componentes para concluir este passo a passo:

- Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e SharePoint.

- Visual Studio.

## <a name="customize-a-sharepoint-site"></a>Personalizar um site do SharePoint
 Para este exemplo, você criará e personalizará um subsite do SharePoint adicionando uma nova coluna de site a ele e criando outro subsite para uso posterior. Posteriormente, você vai exportar o primeiro subsite para um arquivo. wsp e, em seguida, importar a coluna site personalizado para o segundo subsite usando o projeto de importação. wsp.

### <a name="to-create-and-customize-a-sharepoint-site"></a>Para criar e personalizar um site do SharePoint

1. Abra um site do SharePoint usando um navegador da Web, como http://<em>nome do sistema</em>/SitePages/Home.aspx.

2. Crie um subsite fora do site principal do SharePoint abrindo o menu **ações do site** e escolhendo **novo site**.

3. Na caixa de diálogo **criar** do site, escolha o tipo de **site em branco** .

4. Na caixa **título** , digite **site coluna teste 1**; na caixa **nome da URL** , digite **columntest1**; Deixe as outras configurações com seus valores padrão; e, em seguida, escolha o botão **criar** .

5. Depois que o site for criado, navegue no navegador de volta para o site principal, http://<em>nome do sistema</em>/SitePages/Home.aspx.

6. Novamente, crie um subsite em branco fora do site principal do SharePoint abrindo o menu **ações do site** , escolhendo **novo site**e escolhendo o tipo de **site em branco** .

7. Na caixa **título** , insira o **site coluna teste 2**; na caixa **nome da URL** , digite **columntest2**; Deixe as outras configurações com seus valores padrão; e, em seguida, escolha o botão **criar** .

8. Navegar de volta para o primeiro subsite, http://<em>SystemName</em>/columntest1/default.aspx.

9. No menu **ações do site** , escolha **configurações do site** para exibir a página Configurações do site.

10. Na seção **galerias** , escolha o link **colunas do site** .

11. Na parte superior da página da **Galeria de colunas do site** , escolha o botão **criar** .

12. Na caixa **nome da coluna** , insira a **coluna de teste**, mantenha os outros valores padrão e, em seguida, escolha o botão **OK** .

13. A coluna de **coluna de teste** aparece sob o título colunas personalizadas na Galeria de colunas do site.

## <a name="exporting-the-sharepoint-site"></a>Exportando o site do SharePoint
 Em seguida, obtenha um arquivo de instalação do SharePoint (. wsp) que contém os itens e elementos do SharePoint que você deseja importar para o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint. Se você ainda não tiver um arquivo. wsp, deverá criar um a partir de um site existente do SharePoint. Para este exemplo, você vai exportar o site padrão do SharePoint para um arquivo. wsp.

> [!IMPORTANT]
> Se você receber um erro de tempo de execução executando o procedimento a seguir, será necessário executar o procedimento em um sistema que tenha acesso ao site do SharePoint.

### <a name="to-export-an-existing-sharepoint-site"></a>Para exportar um site existente do SharePoint

1. No site do SharePoint, escolha **configurações de site** na guia **ações do site** para exibir a página Configurações do site.

2. Na seção **ações do site** da página Configurações do site, escolha o link **salvar site como modelo** .

3. Na caixa **nome do arquivo** , digite **ExampleSite**e, na caixa **nome do modelo** , digite **site de exemplo**.

4. Para este exemplo, deixe a caixa de seleção **incluir conteúdo** desmarcada.

     Se você marcar essa caixa, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] o salvará todas as listas e bibliotecas de documentos, e seu conteúdo, no arquivo. wsp. Embora isso seja útil em algumas circunstâncias, ele não é necessário para este exemplo.

5. Quando a operação for concluída com êxito, escolha o link **Galeria de soluções** para exibir o arquivo. wsp.

     Para exibir a página da Galeria de soluções mais tarde, abra o menu **ações do site** , escolha **configurações do site**, escolha o link **ir para configurações de site de nível superior** na seção **Administração do conjunto de sites** e, em seguida, escolha o link **soluções** na seção **galerias** .

6. Na Galeria de soluções, escolha o link **ExampleSite** .

7. Na caixa de diálogo **download de arquivo** , escolha o botão **salvar** para salvar o arquivo no sistema local, por padrão, na pasta downloads.

## <a name="import-the-wsp-file"></a>Importar o arquivo. wsp
 Agora que você tem um arquivo *. wsp* que contém um item que deseja reutilizar (a coluna de teste coluna de site personalizada), importe o arquivo *. wsp* para acessá-lo.

### <a name="to-import-a-wsp-file"></a>Para importar um arquivo. wsp

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , na barra de menus, escolha **arquivo**  >  **novo**  >  **projeto** para exibir a caixa de diálogo **novo projeto** . Se o IDE estiver definido para usar Visual Basic configurações de desenvolvimento, na barra de menus, escolha **arquivo**  >  **novo projeto**.

2. Expanda o nó **do SharePoint** sob o **Visual C#** ou **Visual Basic**e escolha o nó **2010** .

3. Escolha o modelo **Importar pacote de solução do SharePoint 2010** no painel **modelos** , deixe o nome do projeto como WspImportProject1 e, em seguida, escolha o botão **OK** .

    O **Assistente para personalização do SharePoint** é exibido.

4. Na página **especificar o site e o nível de segurança para depuração** , insira o [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] para o segundo subsite do SharePoint que você criou anteriormente. Você adicionará o novo item de campo personalizado, http://<em>nome do sistema</em>/columntest2, a esse subsite.

5. Na seção o **que é o nível de confiança para esta solução do SharePoint?** , deixe a seleção como **implantar como uma solução em área restrita**.

6. Na página **especificar a nova origem do projeto** , navegue até o local no sistema em que você salvou o arquivo *. wsp* anteriormente e, em seguida, escolha o botão **Avançar** .

   > [!NOTE]
   > Se você escolher o botão **concluir** nesta página, todos os itens disponíveis no arquivo *. wsp* serão importados.

7. Na caixa **selecionar itens a serem importados** , desmarque todas as caixas de seleção na lista, exceto a **coluna de teste**, e escolha o botão **concluir** .

    Como a lista contém muitos itens, você pode escolher as **Ctrl** + **A** teclas CTRL para escolher todos os itens na lista, escolher a tecla barra de espaços para desmarcar todas as caixas de seleção e, em seguida, selecionar apenas a caixa de seleção ao lado do item de **coluna de teste** .

    Depois que a operação de importação for concluída, um novo projeto chamado **WspImportProject1** será criado e conterá uma pasta denominada **campos**. Nessa pasta está a **coluna de teste** coluna de site personalizada e seu arquivo de definição *Elements.xml*.

## <a name="deploy-the-project"></a>Implantar o projeto
 Por fim, implante **WspImportProject1** no segundo subsite do SharePoint que você criou anteriormente para exibir a coluna site personalizado.

### <a name="to-deploy-the-project"></a>Para implantar o projeto

1. No [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] , escolha a tecla **F5** para implantar e executar o projeto de importação *. wsp* .

2. No site do SharePoint, abra o menu **ações do site** e, em seguida, escolha configurações do **site** para exibir a página Configurações do site.

3. Na seção **galerias** , escolha o link **colunas do site** .

4. Role para baixo até a seção **colunas personalizadas** .

     Observe que a coluna de site personalizada que você importou do primeiro site do SharePoint aparece na lista.

## <a name="see-also"></a>Consulte também
- [Importar itens de um site existente do SharePoint](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)
- [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)
- [Criar controles reutilizáveis para Web Parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)
