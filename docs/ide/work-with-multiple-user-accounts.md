---
title: Trabalhar com várias contas de usuário
description: Saiba como adicionar todas as suas contas da Microsoft ao Visual Studio para que você possa acessar os recursos de qualquer conta sem precisar entrar nele separadamente.
ms.custom: SEO-VS-2020
ms.date: 03/02/2021
ms.topic: conceptual
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 6740eb4c23d739f439103b2ecdd0e8882018204d
ms.sourcegitcommit: 5654b7a57a9af111a6f29239212d76086bc745c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/03/2021
ms.locfileid: "101683787"
---
# <a name="work-with-multiple-user-accounts"></a>Trabalhar com várias contas de usuário

Se você tem várias contas da Microsoft e/ou contas corporativas ou de estudante, é possível adicionar todas elas no Visual Studio para acessar os recursos de qualquer conta sem a necessidade de entrar nas contas separadamente. Os serviços Azure, Application Insights, Azure DevOps e Microsoft 365 oferecem suporte à experiência de entrada simplificada.

Depois que você adicionar várias contas em um computador, esse conjunto de contas fará parte de seu perfil móvel se você entrar no Visual Studio em outro computador.

> [!NOTE]
> Embora os nomes de conta usem perfis móveis, isso não ocorre com as credenciais. Você deverá inserir as credenciais das outras contas na primeira vez que tentar usar os recursos delas em um novo computador.

Este artigo mostra como adicionar várias contas ao Visual Studio. Ele também mostra como ver os recursos acessíveis nessas contas em locais como a caixa de diálogo **Adicionar Serviço Conectado**, o **Gerenciador de Servidores**, e o **Team Explorer**.

## <a name="sign-in-to-visual-studio"></a>Entrar no Visual Studio

Entre no Visual Studio com uma conta da Microsoft ou uma conta organizacional. Você verá seu nome de usuário exibido no canto superior da janela, semelhante a isso:

![Usuário atualmente conectado](../ide/media/vs2015_username.png)

### <a name="access-your-azure-account-in-server-explorer"></a>Acessar sua conta do Azure no Gerenciador de Servidores

Para abrir Gerenciador de servidores, escolha **Exibir**  >  **Gerenciador de servidores** (ou, se você estiver usando as [configurações de ambiente](../ide/environment-settings.md)"geral", pressione **Ctrl** + **ALT** + **S**). Expanda o nó **Azure** e observe que ele contém os recursos disponíveis na conta do Azure associada à conta que você usou para entrar no Visual Studio. Ele é semelhante à seguinte imagem:

![Gerenciador de Servidores com o nó do Azure expandido](../ide/media/work-with-multiple-user-accounts/server-explorer.png)

Na primeira vez que você usa o Visual Studio em qualquer dispositivo específico, a caixa de diálogo mostra apenas as assinaturas registradas na conta que você usou para entrar. Acesse os recursos de uma das outras contas diretamente no **Gerenciador de Servidores** clicando com o botão direito do mouse no nó do **Azure**, escolhendo **Gerenciar e Filtrar Assinaturas** e, em seguida, adicionando suas contas por meio do controle de seletor de conta. Você pode escolher outra conta, se desejar, clicando na seta para baixo e escolhendo na lista de contas. Depois de escolher a conta, você poderá personalizar quais assinaturas dessa conta serão exibidas no **Gerenciador de Servidores**.

![Caixa de diálogo Gerenciar assinaturas do Azure](../ide/media/vs2015_manage_subs.png)

Na próxima vez que você abrir o **Gerenciador de Servidores**, os recursos dessa assinatura serão exibidos.

### <a name="access-your-azure-account-via-add-connected-service-dialog"></a>Acessar sua conta do Azure através da caixa de diálogo Adicionar Serviço Conectado

1. Abra um projeto existente ou crie um projeto.

1. Escolha o nó do projeto no **Gerenciador de Soluções** e, em seguida, clique com o botão direito do mouse e escolha **Adicionar** > **Serviço Conectado**.

   O assistente **Adicionar Serviço Conectado** é exibido e mostra a lista de serviços na conta do Azure associada à sua conta de personalização do Visual Studio. Você não precisa entrar separadamente no Azure. No entanto, você precisará entrar nas outras contas na primeira vez que tentar acessar os recursos delas em outro computador.

### <a name="access-azure-active-directory-in-a-web-project"></a>Acessar o Azure Active Directory em um projeto Web

O AAD (Azure Active Directory) habilita o suporte para logon único do usuário final em aplicativos Web ASP.NET MVC ou a autenticação do AD em serviços de API Web. A autenticação de domínio é diferente da autenticação de conta de usuário individual. Os usuários que têm acesso ao domínio do Active Directory podem usar suas contas existentes do AAD para se conectarem aos aplicativos Web. Microsoft 365 aplicativos também podem usar a autenticação de domínio.

::: moniker range="vs-2017"

Para ver isso em ação, crie um projeto de **Aplicativo Web ASP.NET Core**. Na caixa de diálogo **Novo Aplicativo Web ASP.NET Core**, escolha o modelo **Aplicativo Web** e escolha **Alterar Autenticação**.

::: moniker-end

::: moniker range=">=vs-2019"

Para ver isso em ação, crie um novo projeto de **aplicativo Web ASP.NET Core** . Na página **criar um novo aplicativo Web ASP.NET Core** , escolha **ASP.NET Core 3,1** na lista suspensa, escolha o modelo de **aplicativo Web** e, em seguida, escolha **alterar** em **autenticação**.

::: moniker-end

A caixa de diálogo **Alterar Autenticação** aparece e nela você pode escolher o tipo de autenticação a ser usado no aplicativo.

![Caixa de diálogo Alterar autenticação para ASP.NET](../ide/media/vs2015_change_authentication.png)

Para obter mais informações sobre os diferentes tipos de autenticação no ASP.NET, confira [Criar projetos Web ASP.NET no Visual Studio](/aspnet/visual-studio/overview/2013/creating-web-projects-in-visual-studio#authentication-methods).

### <a name="access-your-azure-devops-organization"></a>Acessar sua organização do Azure DevOps

No menu principal, escolha **equipe**  >  **gerenciar conexões** para abrir a janela **Team Explorer-Connect** . Escolha **gerenciar conexões**  >  **conectar a um projeto**. Na caixa de diálogo **Conectar-se a um Projeto**, selecione um projeto da lista (ou selecione **Adicionar Servidor TFS** e insira a URL do servidor). Ao selecionar uma URL, você será conectado sem precisar reinserir suas credenciais.

Para obter mais informações, confira [Conectar-se a projetos no Team Explorer](connect-team-project.md).

## <a name="add-an-additional-account-to-visual-studio"></a>Adicionar outra conta ao Visual Studio

Para adicionar outra conta ao Visual Studio:

1. Escolha **arquivo**  >  **configurações de conta**.

1. Em **Todas as Contas**, escolha **Adicionar uma conta**.

1. Na página **Entrar em sua conta**, selecione a conta ou escolha **Usar outra conta**. Siga as solicitações para ingressar as credenciais da nova conta.

(Opcional) Agora você pode acessar o **Gerenciador de Servidores** e ver os serviços do Azure associados à conta recém-adicionada. No **Gerenciador de Servidores**, clique com o botão direito do mouse no nó do **Azure** e escolha **Gerenciar e Filtrar Assinaturas**. Escolha a nova conta clicando na seta suspensa ao lado da conta atual e, em seguida, escolha quais assinaturas você deseja exibir no **Gerenciador de Servidores**. Você deverá ver todos os serviços associados à assinatura especificada. Embora você não esteja atualmente conectado ao Visual Studio com a segunda conta, você está conectado aos serviços e aos recursos dessa conta. O mesmo vale para o **projeto**  >  **Adicionar serviço conectado** e o **Team**  >  **Connect a Team Foundation Server**.

### <a name="add-an-account-using-device-code-flow"></a>Adicionar uma conta usando o fluxo de código do dispositivo

Em alguns casos, você não pode entrar em sua conta nem adicionar uma conta da maneira normal. Isso pode acontecer se o Internet Explorer está bloqueado por algum motivo ou se a rede está protegida por um firewall. Para resolver esse problema, habilite o *fluxo de código do dispositivo* para adicionar uma conta ou reautenticar sua conta. O fluxo de código do dispositivo permite que você entre em sua conta usando outro navegador ou computador – um computador físico ou uma VM (máquina virtual).

Para entrar usando o fluxo de código do dispositivo:

1. Abra a página [**Contas**](reference/accounts-environment-options-dialog-box.md) em **Ferramentas** > **Opções** > **Ambiente** e, em seguida, selecione **Habilitar fluxo de código do dispositivo ao adicionar ou reautenticar uma conta**. Escolha **OK** para fechar as páginas de opções.

1. Escolha   >  **configurações de conta** de arquivo para abrir a página de gerenciamento de conta.

1. Escolha **Adicionar uma conta** em **Todas as Contas**.

   Uma caixa de diálogo mostra uma URL e um código para colar em um navegador da Web.

   ![URL e código do fluxo de código do dispositivo](media/work-with-multiple-user-accounts/device-login-code.png)

1. Pressione **Ctrl** + **C** para copiar o texto da caixa de diálogo e, em seguida, escolha **OK** para fechar a caixa de diálogo. Cole o texto copiado em um editor de texto como o Bloco de notas. Isso facilita a cópia do código na próxima etapa.

1. Navegue para a URL de logon do dispositivo no computador ou no navegador da Web que deseja usar para entrar no Visual Studio e, em seguida, cole ou insira o código copiado na caixa que indica **Código**.

   O nome do aplicativo **Visual Studio** deverá ser exibido mais adiante na página.

1. Em **Visual Studio**, escolha **Continuar**.

   ![Captura de tela da página de logon do dispositivo mostrando a opção continuar.](media/work-with-multiple-user-accounts/device-login-page.png)

1. Siga os prompts para inserir as credenciais de sua conta.

   Uma página é exibida, informando que você entrou no Visual Studio por meio de seu dispositivo e que a janela do navegador pode ser fechada.

   ![Conexão ao Visual Studio por meio do navegador concluída](media/work-with-multiple-user-accounts/sign-in-browser-complete.png)

1. Volte para a página de gerenciamento de contas no Visual Studio e você verá a conta recém-adicionada listada em **Todas as Contas**. Escolha **Fechar**.

::: moniker range=">=vs-2019"

### <a name="add-a-github-account-to-visual-studio"></a>Adicionar uma conta do GitHub ao Visual Studio

A partir da versão 16,8, você poderá adicionar as contas do GitHub e do GitHub empresarial ao seu conjunto de chaves. Você poderá adicioná-los e aproveitá-los da mesma forma como faz com contas da Microsoft, o que significa que você terá um tempo mais fácil de acessar seus recursos do GitHub no Visual Studio.

Para obter instruções detalhadas, consulte [trabalhar com contas do GitHub no Visual Studio](work-with-github-accounts.md).
::: moniker-end

## <a name="see-also"></a>Confira também

- [Entrar no Visual Studio](signing-in-to-visual-studio.md)
- [Entrar no Visual Studio para Mac](/visualstudio/mac/signing-in)
