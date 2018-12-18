---
title: Trabalhar com várias contas de usuário | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b73c865c-74e0-420e-89cc-43524f4aafd0
caps.latest.revision: 17
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 93f029a067e5a45930c2ac827862c1807e32aff8
ms.sourcegitcommit: 9ceaf69568d61023868ced59108ae4dd46f720ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49176261"
---
# <a name="work-with-multiple-user-accounts"></a>Trabalhar com várias contas de usuário
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Se você tem várias contas da Microsoft e/ou contas corporativas ou de estudante, é possível adicionar todas elas no Visual Studio para acessar os recursos de qualquer conta sem a necessidade de entrar nas contas separadamente. A partir da data do Visual Studio 2015 RTM, os serviços do Azure, Application Insights, Team Foundation Server e do Office 365 dão suporte a experiência de entrada simplificada. Serviços adicionais podem ser disponibilizados com o passar do tempo.  
  
 Depois de adicionar várias contas em um computador, esse conjunto de contas se moverá com você ao entrar no Visual Studio em outro computador. É importante observar que, embora os nomes de conta usem perfil móvel, as credenciais não. Portanto, você será solicitado a inserir as credenciais das outras contas na primeira vez que tentar usar os recursos dessas contas no novo computador.  
  
 Este passo a passo mostra como adicionar várias contas no Visual Studio e como ver que os recursos acessíveis dessas contas são refletidos em locais como a caixa de diálogo **Adicionar Serviço Conectado**, o **Gerenciador de Servidores** e o **Team Explorer**.  
  
#### <a name="sign-in-to-visual-studio"></a>Entrar no Visual Studio  
  
1.  Entrar no Visual Studio 2015 com uma conta da Microsoft ou uma conta organizacional. Você verá seu nome de usuário refletida no canto superior direito da janela, semelhante a esta:  
  
     ![Usuário atualmente conectado](../ide/media/vs2015-username.png "VS2015_UserName")  
  
### <a name="access-your-azure-account-in-server-explorer"></a>Acessar sua conta do Azure no Gerenciador de Servidores  
 Pressione **Ctrl + Alt + S** abrir o **Gerenciador de Servidores**. Clique no ícone do Azure e quando ele se expandir, você deve ver os recursos disponíveis na conta do Azure que está associada com a ID que você usou para fazer logon no Visual Studio 2015. Ele deve ser semelhante isso, exceto que os seus próprios recursos, não o SR. Guido:  
  
 ![Gerenciador de Servidores mostrando o nó de Ferramentas do Azure expandido](../ide/media/vs2015-serverexplorer.png "VS2015_ServerExplorer")  
  
 Na primeira vez que você usar o Visual Studio em qualquer dispositivo específico, a caixa de diálogo mostrará apenas as assinaturas registradas na ID que você usou para entrar no IDE. Você pode acessar os recursos de qualquer uma das outras contas diretamente do **Gerenciador de Servidores** clicando com o botão direito do mouse no nó do Azure e escolhendo **Gerenciar e Filtrar Assinaturas** e, em seguida, adicionar suas contas do controle de seletor de conta. Você pode escolher outra conta, se desejar, clicando na seta para baixo e escolhendo na lista de contas. Depois de escolher a conta, é possível escolher qual assinatura dessa conta você deseja exibir no Gerenciador de Servidores.  
  
 ![Caixa de diálogo Gerenciar Assinaturas do Azure](../ide/media/vs2015-manage-subs.png "vs2015_manage_subs")  
  
 Na próxima vez que você abrir o Gerenciador de Servidores, os recursos dessa(s) assinatura(s) serão exibidos.  
  
### <a name="access-your-azure-account-via-add-connected-service-dialog"></a>Acessar sua conta do Azure através da caixa de diálogo Adicionar Serviço Conectado  
  
1.  Crie um projeto de Aplicativo Universal no C#.  
  
2.  Clique com o botão direito no nó do projeto no Gerenciador de soluções e escolha **Add > serviço conectado**. ID da Adicionar serviço conectado assistente é exibida e mostra a lista de serviços na conta do Azure que está associado com seu logon do Visual Studio. Observe que você não precisa entrar separadamente no Azure. No entanto, é necessário entrar nas outras contas na primeira vez que você tentar acessar os recursos delas de um determinado computador.  
  
    > [!WARNING]
    >  Se esta for a primeira vez que você está criando um aplicativo da Store no Visual Studio 2015 em um computador específico, você será solicitado a habilitar o dispositivo para o modo de desenvolvimento acessando **configurações &#124; . Segurança e atualizações &#124; para desenvolvedores** em seu computador. Para obter mais informações, consulte [Habilitar seu dispositivo para desenvolvimento](https://msdn.microsoft.com/library/windows/apps/dn706236.aspx).  
  
###  <a name="access_azure"></a> Acessar o Azure Active Directory em um projeto Web  
 O Azure AD habilita o suporte para o logon única do usuário final em aplicativos Web ASP.NET MVC ou autenticação AD nos serviços de API Web. A autenticação de domínio é diferente da autenticação de conta de usuário individual. Os usuários que têm acesso ao seu domínio do Active Directory podem usar suas contas existentes do Azure AD para conectar-se aos aplicativos Web. Os aplicativos do Office 365 também podem usar a autenticação de domínio. Para ver isso em ação, crie um aplicativo web (**arquivo > Novo projeto > c# > nuvem > aplicativo Web ASP.NET**). Na caixa de diálogo Novo Projeto ASP.NET escolha **Alterar Autenticação**. O assistente de autenticação aparece e habilita você a escolher o tipo de autenticação a ser usado em seu aplicativo.  
  
 ![Caixa de diálogo Alterar autenticação para o ASP.NET](../ide/media/vs2015-change-authentication.png "VS2015_change_authentication")  
  
 Para obter mais informações sobre os diferentes tipos de autenticação no ASP.NET, consulte [Criando projetos Web do ASP.NET no Visual Studio 2013](http://www.asp.net/visual-studio/overview/2013/creating-web-projects-in-visual-studio#orgauth) (as informações sobre a autenticação ainda são relevantes para o Visual Studio 2015).  
  
### <a name="access-your-visual-studio-team-services-account"></a>Acessar sua conta do Visual Studio Team Services  
 No menu principal, escolha **equipe > conectar-se ao Team Foundation Server** para abrir o **Team Explorer** janela. Clique em **Selecionar Projetos de Equipe**e, em seguida, na caixa de listagem em **Selecionar um Team Foundation Server**, você verá a URL de sua conta do Visual Studio Team Services. Ao selecionar a URL você será conectado sem precisar reinserir suas credenciais.  
  
## <a name="add-a-second-user-account-to-visual-studio"></a>Adicionar uma segunda conta de usuário no Visual Studio  
 Clique na seta para baixo ao lado de seu nome de usuário no canto superior direito do Visual Studio. Em seguida, clique no **configurações de conta** item de menu. A caixa de diálogo **Gerenciador de Conta** aparece e exibe a conta com a qual você entrou. Clique o **adicionar uma conta** link no canto inferior esquerdo da caixa de diálogo para adicionar uma nova conta da Microsoft ou uma nova conta corporativa ou escolar.  
  
 ![Seletor de conta do Visual Studio](../ide/media/vs2015-acct-picker.png "VS2015_acct_picker")  
  
 Siga as solicitações para ingressar as credenciais da nova conta. A ilustração a seguir mostra o Gerenciador de Conta depois que um usuário adicionou sua conta corporativa Contoso.com.  
  
 ![Gerenciador de Conta](../ide/media/vs2015-accountmanager.gif "VS2015_AccountManager")  
  
## <a name="revisit-the-add-connected-services-wizard-and-server-explorer"></a>Rever o Assistente para Adicionar Serviços Conectados e o Gerenciador de Servidores  
 Vá novamente até o **Gerenciador de Servidores**, clique com botão direito do mouse no nó do Azure e escolha **Gerenciar e filtrar assinaturas**. Escolha a nova conta, clicando na seta suspensa ao lado da conta atual e, em seguida, escolha quais assinaturas você deseja exibir no Gerenciador de Servidores. Você deve ver todos os serviços associados à assinatura especificada. Mesmo que você não esteja conectado ao IDE do Visual Studio com a segunda conta, você está conectado aos serviços e recursos dessa conta. O mesmo é verdadeiro para **projeto > Adicionar serviço conectado** e **equipe > conectar-se ao Team Foundation Server**.



