---
title: 'Passo a passo: Criar uma coluna de Site, o tipo de conteúdo e a lista do SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 02/02/2017
ms.technology:
- office-development
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.ListDesigner.GeneralMessageHelp
- Microsoft.VisualStudio.SharePoint.Designers.ListDesigner.ViewModels.ListViewModel.SortingAndGrouping
- VS.SharePointTools.ListDesigner.SortingGrouping
dev_langs:
- VB
- CSharp
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, list definitions
- SharePoint development in Visual Studio, list instances
- SharePoint development in Visual Studio, fields
- SharePoint development in Visual Studio, content types
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- office
ms.openlocfilehash: 2fb78f5c40a04bb69d2f95d7f872b05e3d501113
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49900118"
---
# <a name="walkthrough-create-a-site-column-content-type-and-list-for-sharepoint"></a>Passo a passo: Criar uma coluna de site, o tipo de conteúdo e a lista para o SharePoint
  Os procedimentos a seguir demonstram como criar colunas de site do SharePoint personalizadas — ou *campos*— bem como um tipo de conteúdo que usa as colunas de site. Ele também mostra como criar uma lista que usa o novo tipo de conteúdo.  
  
 Esta explicação passo a passo inclui as seguintes tarefas:  
  
- [Criando colunas de Site personalizadas](#BKMK_CreatingCustSiteCols).  
  
- [Criando um tipo de conteúdo personalizado](#BKMK_CreateCustContType).  
  
- [Criando uma lista](#BKMK_CreateList).  
  
- [Criando uma lista](#BKMK_CreateList).  
  
- [Testando o aplicativo](#BKMK_TestApp).  
  
  [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Você precisa dos seguintes componentes para concluir esta instrução passo a passo:  
  
-   Edições com suporte do Windows e do SharePoint.
  
-   Visual Studio.  
  
## <a name="create-custom-site-columns"></a>Criar colunas de site personalizada
 Este exemplo cria uma lista para o gerenciamento de pacientes em um hospital. Primeiro, você deve criar um projeto do SharePoint no [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] e adicionar colunas de site a ele, da seguinte maneira.  
  
#### <a name="to-create-the-project"></a>Para criar o projeto  
  
1.  Sobre o [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] **arquivo** menu, escolha **New** > **projeto**.  
  
2.  No **novo projeto** caixa de diálogo, em qualquer um **Visual c#** ou **Visual Basic**, expanda o **SharePoint** nó e, em seguida, escolha **2010**.  
  
3.  No **modelos** painel, escolha **o projeto do SharePoint 2010**, altere o nome do projeto para **clínica**e, em seguida, escolha o **Okey** botão.  
  
     O modelo de projeto do SharePoint 2010 é um projeto vazio que é usado neste exemplo para conter as colunas de site e outros itens de projeto que forem adicionadas posteriormente.  
  
4.  Sobre o **especificar o nível de site e segurança para depuração** página, insira a URL do site do SharePoint local para o qual você deseja adicionar o novo item de campo personalizado ou usar o local padrão (`http://<`*SystemName* `>/)`.  
  
5.  No **qual é o nível de confiança para essa solução do SharePoint?** seção, use o valor padrão **implantar como solução em área restrita**.  
  
     Para obter mais informações sobre a área restrita e soluções em farm, consulte [considerações sobre a solução em área restrita](../sharepoint/sandboxed-solution-considerations.md).  
  
6.  Escolha o **concluir** botão. O projeto deve agora estar listado em **Gerenciador de soluções**.  
  
#### <a name="to-add-site-columns"></a>Para adicionar colunas de site  
  
1.  Adicione uma nova coluna de site. Para fazer isso, em **Gerenciador de soluções**, abra o menu de atalho **clínica**e, em seguida, escolha **Add** > **Novo Item**.  
  
2.  No **Adicionar Novo Item** diálogo caixa, escolha **coluna de Site**, altere o nome para **paciente nome**e, em seguida, escolha o **adicionar** botão.  
  
3.  Na coluna de site *Elements. XML* do arquivo, deixe o **tipo** definir como **texto**e altere o **grupo** definindo como  **Colunas de Site clínica**. Ao concluir, a coluna de site *Elements. XML* arquivo deve parecer com o exemplo a seguir.  
  
    ```xml  
    <Field  
         ID="{f9ba60d1-5631-41fb-b016-a38cf48eef63}"  
         Name="Clinic - Patient Name"  
         DisplayName="Patient Name"  
         Type="Text"  
         Required="FALSE"  
         Group="Clinic Site Columns">  
    </Field>  
    ```  
  
4.  Usando o mesmo procedimento, adicione mais duas colunas de site ao projeto: **ID do paciente** (tipo = "Integer") e **Doutor nome** (tipo = "Text"). Definir seu valor de grupo **colunas de Site clínica**.  
  
## <a name="create-a-custom-content-type"></a>Criar um tipo de conteúdo personalizado
 Em seguida, crie um tipo de conteúdo — com base no tipo de conteúdo contatos — que inclui as colunas de site que você criou no procedimento anterior. Baseando um tipo de conteúdo em um tipo de conteúdo existente, você pode economizar tempo porque o tipo de conteúdo base fornece várias colunas de site para uso no novo tipo de conteúdo.  
  
#### <a name="to-create-a-custom-content-type"></a>Para criar um tipo de conteúdo personalizado  
  
1.  Adicione um tipo de conteúdo para o projeto. Para fazer isso, em **Gerenciador de soluções**, escolha o nó do projeto  
  
2.  Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.  
  
3.  Em um **Visual c#** ou **Visual Basic**, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
4.  No **modelos** painel, escolha o **tipo de conteúdo** modelo, altere o nome para **informações do paciente**e, em seguida, escolha o **adicionar** botão.  
  
     O **Assistente para personalização do SharePoint** é aberta.  
  
5.  No **qual tipo de conteúdo base esse tipo de conteúdo deve herdar de** , escolha **contato** como o tipo de conteúdo no qual basear o novo tipo de conteúdo e, em seguida, escolha o **concluir**botão.  
  
     Isso fornece acesso a outras colunas de site potencialmente útil no contato tipo de conteúdo, além das colunas de site que você definiu anteriormente.  
  
6.  Após o tipo de conteúdo designer é exibido, além de **colunas** guia, adicione as três colunas que você definiu anteriormente do site: **paciente nome**, **ID do paciente**e **Doutor nome**. Para adicionar essas colunas, escolha a primeira caixa de listagem na lista de colunas de site sob **nome de exibição**e, em seguida, escolher cada coluna de site na lista uma por vez.  
  
    > [!TIP]  
    >  Para escolher as colunas de site mais rapidamente, filtre a lista, digitando as primeiras letras do nome da coluna.  
  
7.  Além de três colunas de site personalizado, adicione a **comentários** coluna de site da lista de colunas de site.  
  
8.  Selecione o **necessária** caixa de seleção para o **nome do paciente** e **ID do paciente** campos obrigatórios de colunas de site para torná-los.  
  
9. Sobre o **Content Type** guia, certifique-se de que o nome do tipo de conteúdo é **informações do paciente**e, em seguida, altere a descrição a ser **cartão de informações do paciente**.  
  
10. Alteração **nome do grupo** à **tipos de conteúdo de clínica**e deixe as outras configurações em seus valores padrão.  
  
11. Na barra de menus, escolha **arquivo** > **Salvar tudo**e, em seguida, feche o designer de tipo de conteúdo.  
  
## <a name="create-a-list"></a>Criar uma lista
 Agora, crie uma lista que usa as novas colunas de site e tipo de conteúdo.  
  
#### <a name="to-create-a-list"></a>Para criar uma lista  
  
1.  Adicione uma lista ao projeto. Para fazer isso, em **Gerenciador de soluções**, escolha o nó do projeto.  
  
2.  Na barra de menus, escolha **Projeto** > **Adicionar Novo Item**.  
  
3.  Em um **Visual c#** ou **Visual Basic**, expanda o **SharePoint** nó e, em seguida, escolha o **2010** nó.  
  
4.  No **modelos** painel, escolha o **lista** modelo, altere o nome para **pacientes**e, em seguida, escolha o **adicionar** botão.  
  
5.  Deixe o **personalizar a lista com base no** definir como **padrão (em branco)** e, em seguida, escolha o **concluir** botão.  
  
6.  No Designer de lista, escolha o **tipos de conteúdo** botão para exibir o **configurações de tipo de conteúdo** caixa de diálogo.  
  
7.  Escolha a nova linha, escolha o **informações do paciente** tipo na lista de tipos de conteúdo de conteúdo e, em seguida, escolha o **Okey** botão.  
  
     Isso adiciona todas as colunas de site do **informações do paciente** tipo na lista de conteúdo.  
  
8.  Exclua todas as colunas de site na lista, exceto os seguintes:  
  
    -   ID do paciente  
  
    -   Nome do paciente  
  
    -   Telefone residencial  
  
    -   Email  
  
    -   Nome do Doutor  
  
    -   Comentários  
  
9. Sob **nome de exibição da coluna**, escolha uma linha vazia, adicione uma coluna de lista personalizada e nomeie- **Hospital**. Deixe seu tipo de dados como **linha única de texto**.  
  
     A coluna de lista personalizada só se aplica a essa lista. Quando você adiciona uma coluna de lista personalizada a uma lista, um nova lista Tipo de conteúdo, incluindo todas as colunas adicionadas à lista, é criado e definido como a lista padrão.  
  
    > [!TIP]  
    >  Se você escolher uma coluna na lista de colunas de site, uma coluna de site existente será usada. No entanto, se você inserir um valor de nome de coluna sem escolher nenhuma coluna na lista, uma coluna de lista personalizada é criada, mesmo se uma coluna com o mesmo nome já existe na lista.  
  
     Opcionalmente, em vez de definir o tipo de dados da coluna de lista personalizada para **linha única de texto**, em vez disso, você pode definir o tipo de dados para essa coluna para pesquisa e seus valores deve ser recuperados de uma tabela ou outra lista. Para obter informações sobre colunas de pesquisa, consulte [relações de lista no SharePoint 2010](http://go.microsoft.com/fwlink/?LinkId=224994) e [pesquisas e relações de lista](http://go.microsoft.com/fwlink/?LinkID=224995).  
  
10. Lado a **ID do paciente** e **nome do paciente** caixas, selecionadas o **necessária** caixa de seleção.  
  
11. Sobre o **modos de exibição** guia, escolha uma linha vazia para criar uma exibição. Insira **detalhes do paciente**.  
  
     Sobre o **modos de exibição** guia, você pode especificar as colunas que você deseja que apareça na lista do SharePoint.  
  
12. Escolha o novo **detalhes do paciente** linha e, em seguida, escolha o **definir como padrão** botão.  
  
     O novo modo de exibição agora é a exibição padrão para a lista.  
  
13. Adicione as seguintes colunas para o **colunas selecionadas** lista na seguinte ordem:  
  
    -   ID do paciente  
  
    -   Nome do paciente  
  
    -   Telefone residencial  
  
    -   Email  
  
    -   Nome do Doutor  
  
    -   Hospital  
  
    -   Comentários  
  
14. No **propriedades** , escolha o **classificando e agrupando** propriedade e, em seguida, escolha o botão de reticências ![ícone de reticências](../sharepoint/media/ellipsisicon.gif "noíconereticências")para exibir o **classificando e agrupando** caixa de diálogo.  
  
15. No **nome da coluna** , escolha **paciente nome**, certifique-se de que o **classificação** coluna estiver definida como **crescente**e, em seguida, escolha o  **Okey** botão.  
  
## <a name="test-the-application"></a>Testar o aplicativo
 Agora que as colunas de site personalizadas, o tipo de conteúdo e a lista estiverem prontos, implantá-los no SharePoint e execute o aplicativo para testá-lo.  
  
#### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Na barra de menus, escolha **Arquivo** > **Salvar Todos**.  
  
2.  Escolha o **F5** chave para executar o aplicativo.  
  
     O aplicativo é compilado e, em seguida, seus recursos são implantados no SharePoint e ativados.  
  
3.  Na barra de navegação rápida, escolha o **pacientes** link para exibir o **pacientes** lista.  
  
     Os nomes de coluna na lista devem corresponder àquelas que você inseriu na **modos de exibição** guia [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)].  
  
4.  Escolha o **adicionar novo item** link para criar um cartão de informações do paciente.  
  
5.  Insira as informações nos campos e, em seguida, escolha o **salvar** botão.  
  
     O novo registro aparece na lista.  
  
## <a name="see-also"></a>Consulte também
 [Criar colunas de site, tipos de conteúdo e listas para o SharePoint](../sharepoint/creating-site-columns-content-types-and-lists-for-sharepoint.md)   
 [Desenvolver soluções do SharePoint](../sharepoint/developing-sharepoint-solutions.md)   
 [Como: criar um tipo de campo personalizado](http://go.microsoft.com/fwlink/?LinkId=192079)   
 [Tipos de conteúdo](http://go.microsoft.com/fwlink/?LinkId=192080)   
 [Colunas](http://go.microsoft.com/fwlink/?LinkId=192081)  
  
