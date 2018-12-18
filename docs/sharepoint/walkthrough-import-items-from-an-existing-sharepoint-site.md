---
title: 'Passo a passo: Importar itens de um Site existente do SharePoint | Microsoft Docs'
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
- SharePoint development in Visual Studio, importing items
- importing items [SharePoint development in Visual Studio]
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 86256cdecd878c78c34d7128a05eb7b795067701
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49909751"
---
# <a name="walkthrough-import-items-from-an-existing-sharepoint-site"></a>Passo a passo: Importar itens de um site do SharePoint existente
  Este passo a passo demonstra como importar itens de um site do SharePoint existente para um [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint.  
  
 Este passo a passo demonstra as seguintes tarefas:  
  
- Personalizando um site do SharePoint, adicionando uma coluna de site personalizada (também conhecido como um *campo*.  
  
- Exportando um site do SharePoint para um arquivo. wsp.  
  
- Importar o arquivo. wsp em [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint usando o projeto de importação. wsp.  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Edições com suporte do [!INCLUDE[TLA#tla_win](../sharepoint/includes/tlasharptla-win-md.md)] e do SharePoint.  
  
-   Visual Studio.  
  
## <a name="customize-a-sharepoint-site"></a>Personalizar um site do SharePoint
 Neste exemplo, você criará e personalizar um subsite do SharePoint com a adição de uma nova coluna de site e criando outro subsite para uso posterior. Posteriormente, você irá exportar o subsite primeiro para um arquivo. wsp e, em seguida, importar a coluna de site personalizado para o subsite segundo usando o projeto de importação. wsp.  
  
#### <a name="to-create-and-customize-a-sharepoint-site"></a>Para criar e personalizar um site do SharePoint  
  
1. Abrir um site do SharePoint usando um navegador da Web, como http://<em>nome do sistema</em>/SitePages/Home.aspx.  
  
2. Criar um subsite fora do site principal do SharePoint, abra o **ações do Site** menu e, em seguida, escolhendo **novo Site**.  
  
3. No site do **Create** diálogo caixa, escolha o **Site em branco** tipo.  
  
4. No **Title** , digite **teste 1 da coluna de Site**; na **nome da URL** , digite **columntest1**; deixe as outras configurações no padrão valores; e, em seguida, escolha o **criar** botão.  
  
5. Depois que o site for criado, navegue no navegador para o site principal, http://<em>nome do sistema</em>/SitePages/Home.aspx.  
  
6. Novamente, criar um subsite em branco fora do site principal do SharePoint, abra o **ações do Site** menu, escolhendo **novo Site**e, em seguida, escolhendo o **Site em branco** tipo.  
  
7. No **Title** , digite **teste 2 de coluna de Site**; na **nome da URL** , digite **columntest2**; deixe as outras configurações no padrão valores; e, em seguida, escolha o **criar** botão.  
  
8. Navegue de volta para o primeiro subsite, http://<em>SystemName</em>/columntest1/default.aspx.  
  
9. Sobre o **ações do Site** menu, escolha **configurações de Site** para exibir a página de configurações do Site.  
  
10. No **galerias** , escolha o **colunas de Site** link.  
  
11. Na parte superior dos **Galeria de colunas de Site** , escolha o **criar** botão.  
  
12. No **nome da coluna** , digite **coluna teste**, mantenha os outros valores padrão e, em seguida, escolha o **Okey** botão.  
  
13. O **coluna teste** coluna aparece sob as colunas personalizadas título na Galeria de coluna do Site.  
  
## <a name="exporting-the-sharepoint-site"></a>Exportando o site do SharePoint
 Em seguida, obter um arquivo de instalação (. wsp) do SharePoint que contém os itens do SharePoint e os elementos que você deseja importar para seu [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] projeto do SharePoint. Se você ainda não tiver um arquivo. wsp, em seguida, você deve criar um de um site existente do SharePoint. Neste exemplo, você exportará o site do SharePoint padrão em um arquivo. wsp.  
  
> [!IMPORTANT]  
>  Se você receber um erro de tempo de execução executar o procedimento a seguir, você precisa executar o procedimento em um sistema que tem acesso ao site do SharePoint.  
  
#### <a name="to-export-an-existing-sharepoint-site"></a>Para exportar um site do SharePoint existente  
  
1.  No site do SharePoint, escolha **configurações de Site** sobre o **ações do Site** guia para exibir a página de configurações do Site.  
  
2.  No **ações do Site** seção da página Configurações do Site, escolha o **site Salvar como modelo** link.  
  
3.  No **nome do arquivo** , digite **ExampleSite**e, nas **nome do modelo** , digite **Site de exemplo**.  
  
4.  Neste exemplo, deixe o **incluir conteúdo** caixa de seleção desmarcada.  
  
     Se você selecionar esta caixa, [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] salva todas as listas e bibliotecas de documentos e seu conteúdo, o arquivo. wsp. Embora isso seja útil em algumas circunstâncias, não é necessário para este exemplo.  
  
5.  Quando a operação for concluída com êxito, escolha o **Galeria de soluções** link para exibir o arquivo. wsp.  
  
     Para exibir a página da Galeria de soluções mais adiante, abra o **ações do Site** menu, escolha **configurações de Site**, escolha o **vá para configurações de site de nível superior** link no  **Site Collection Administration** seção e, em seguida, escolha o **soluções** link no **galerias** seção.  
  
6.  Na Galeria de soluções, escolha o **ExampleSite** link.  
  
7.  No **Download de arquivo** diálogo caixa, escolha o **salvar** botão para salvar o arquivo em seu sistema local, por padrão, na pasta Downloads.  
  
## <a name="import-the-wsp-file"></a>Importar o arquivo. wsp
 Agora que você tem um *. wsp* arquivo que contém um item que você deseja reutilizar (a coluna personalizada de site e teste de coluna), importe o *. wsp* arquivo para acessá-lo.  
  
#### <a name="to-import-a-wsp-file"></a>Para importar um arquivo. wsp  
  
1. Na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], na barra de menus, escolha **arquivo** > **New** > **projeto** para exibir o **novo projeto**caixa de diálogo. Se o seu IDE for definido para usar configurações de desenvolvimento do Visual Basic, na barra de menus, escolha **arquivo** > **novo projeto**.  
  
2. Expanda o **SharePoint** nó em um **Visual c#** ou **Visual Basic**e, em seguida, escolha o **2010** nó.  
  
3. Escolha o **Importar pacote de solução do SharePoint 2010** modelo na **modelos** painel, deixe o nome do projeto como WspImportProject1 e, em seguida, escolha o **Okey** botão.  
  
    O **Assistente para personalização do SharePoint** é exibida.  
  
4. Sobre o **especificar o nível de site e segurança para depuração** , insira o [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] para o segundo subsite do SharePoint que você criou anteriormente. Você adicionará o novo personalizado de campo do item, http://<em>nome do sistema</em>/columntest2 desse subsite.  
  
5. No **qual é o nível de confiança para essa solução do SharePoint?** seção, deixe a seleção como **implantar como solução em área restrita**.  
  
6. No **especifique a nova origem do projeto** página, navegue até o local no sistema onde você salvou o *. wsp* arquivo anteriormente e, em seguida, selecione o **próxima** botão.  
  
   > [!NOTE]  
   >  Se você escolher o **terminar** botão nessa página, todos os itens disponíveis na *. wsp* arquivo será importado.  
  
7. No **selecionar itens para importar** caixa, desmarque todas as caixas de seleção na lista, exceto **coluna teste**e, em seguida, escolha o **concluir** botão.  
  
    Como a lista contiver muitos itens, você pode escolher o **Ctrl**+**um** chaves para escolher todos os itens na lista, escolha a tecla de barra de espaços para desmarcar todas as caixas de seleção e, em seguida, selecione apenas a verificação caixa ao lado de **coluna teste** item.  
  
    Depois que a operação de importação for concluída, um novo projeto chamado **WspImportProject1** é criado que contém uma pasta chamada **campos**. Essa pasta é a coluna de site personalizado **coluna teste** e seu arquivo de definição *Elements. XML*.  
  
## <a name="deploy-the-project"></a>Implantar o projeto
 Por fim, implante **WspImportProject1** subsite para a segunda do SharePoint que você criou anteriormente para exibir a coluna de site personalizadas.  
  
#### <a name="to-deploy-the-project"></a>Para implantar o projeto  
  
1.  Na [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)], escolha o **F5** chave para implantar e executar o *. wsp* Importar projeto.  
  
2.  No site do SharePoint, abra o **ações do Site** menu e, em seguida, escolha **configurações de Site** para exibir a página de configurações do Site.  
  
3.  No **galerias** , escolha o **colunas de Site** link.  
  
4.  Role para baixo até a **colunas personalizadas** seção.  
  
     Observe que a coluna de site personalizadas que você importou primeiro site do SharePoint aparece na lista.  
  
## <a name="see-also"></a>Consulte também
 [Importar itens de um site do SharePoint existente](../sharepoint/importing-items-from-an-existing-sharepoint-site.md)   
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)   
 [Criar controles reutilizáveis para web parts ou páginas de aplicativo](../sharepoint/creating-reusable-controls-for-web-parts-or-application-pages.md)  
  
