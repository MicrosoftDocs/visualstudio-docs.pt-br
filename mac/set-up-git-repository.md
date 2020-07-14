---
title: Configurando um Repositório Git
description: Usando o Git e o Subversion no Visual Studio para Mac.
author: therealjohn
ms.author: johmil
ms.date: 05/13/2020
ms.assetid: E992FA1D-B2AD-4A28-ADC6-47E4FC471060
ms.topic: how-to
ms.openlocfilehash: 9d6fd5ffefcd6696fa67302a8d59fd46e498a472
ms.sourcegitcommit: 5335a9864d5747bc917ed28d4ebeade3076b10e7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2020
ms.locfileid: "85950600"
---
# <a name="set-up-a-git-repository"></a>Configurar um repositório GIT

O Git é um sistema de controle de versão distribuído que permite que as equipes trabalhem nos mesmos documentos simultaneamente. Isso significa que há um único servidor que contém todos os arquivos, mas sempre que um repositório passar por check-out nessa fonte central, todo o repositório será clonado localmente para seu computador.

Há muitos hosts remotos que permitem trabalhar com o Git para controle de versão, porém o mais comuns deles é o GitHub. O exemplo a seguir usa um host do GitHub, mas você pode usar qualquer host Git para controle de versão no Visual Studio para Mac.

Se você quiser usar o GitHub, verifique se tem uma conta criada e configurada antes de seguir as etapas neste artigo.

## <a name="creating-a-remote-repo-on-github"></a>Criando um repositório remoto no GitHub

O exemplo a seguir usa um host do GitHub, mas você pode usar qualquer host Git para controle de versão no Visual Studio para Mac.

Para configurar um repositório Git, execute as seguintes etapas:

1. Crie um novo repositório Git em github.com:

    ![Criar um novo repositório Git](media/version-control-git1-sml.png)

2. Defina o nome do repositório, a descrição e a privacidade. **Não** inicialize o repositório. Defina .gitignore e a licença como Nenhum:

    ![Defina os detalhes do repositório git](media/version-control-git2.png)

3. O próximo local fornecerá uma opção para exibir e copiar o endereço HTTPS ou SSH para o repositório que você criou:

    ![exibir e copiar endereço](media/version-control-git3.png)

   Você precisará do endereço HTTPS para apontar o Visual Studio para Mac para este repositório.

## <a name="publishing-an-existing-project"></a>Publicar um projeto existente

Se você tiver um projeto existente que ainda _não está_ no controle de versão, use as seguintes etapas para configurá-lo no Git:

1. Selecione o nome da Solução do Painel de Soluções do Visual Studio para Mac.

2. Na barra de menus, selecione **controle de versão > publicar no controle de versão** para exibir a caixa de diálogo **clonar repositório** :

    ![Iniciar o check-out no Visual Studio para Mac](media/version-control-git4.png)

    Se esse item de menu aparecer esmaecido no menu, verifique se você selecionou o nome da Solução.

3. Escolha a guia **selecionar de registrado** e pressione o botão **Adicionar** :

    ![](media/version-control-git5.png)

4. Digite o nome do repositório como você gostaria de exibi-lo localmente e cole a URL da etapa 3. A caixa de diálogo de Configuração do repositório deve ser semelhante ao seguinte. Pressione OK:

    ![Caixa de diálogo Insira os detalhes do git](media/version-control-git6.png)

    Também é possível usar SSH para conectar-se ao GIT.

5. Para tentar publicar o aplicativo no git, selecione o repositório e verifique se os campos **nome do módulo** e texto da **mensagem** estão concluídos:

    ![Tentativa de publicar o projeto para o git](media/version-control-git7.png)

6. Clique em **OK** e em **Publicar** na caixa de diálogo de alerta.

7. Na janela **Credenciais do Git**, insira seu nome de usuário do GitHub e a senha. 

> [!NOTE]
> Se sua conta tiver a 2FA (autenticação de dois fatores) habilitada, você precisará criar um token de acesso, que será usado no lugar de uma senha. Se você não criou um token de acesso, siga as etapas na documentação de [Token de acesso](https://help.github.com/articles/creating-an-access-token-for-command-line-use/) do Git.

8. Insira o nome de usuário e o token de acesso pessoal e pressione **OK**:

    ![Insira o nome de usuário e a senha para o git](media/version-control-git9-sml.png)

9. Depois de alguns segundos, a Solução deverá ser publicada com sua confirmação inicial. Confirme que isso foi publicado navegando o item de menu de Controle de versão, que agora deve ser populado com várias opções:

    ![Menu de Controle de versão](media/version-control-git10.png)

10. Depois de começar a fazer alterações adicionais, primeiro use o **controle de versão > menu revisar e confirmar** para abrir o modo de exibição de status. Depois de selecionar e confirmar as alterações, selecione **enviar por** push para enviar as alterações para o repositório remoto. Isso permitirá que todos os usuários apropriados possam exibi-las em github.com:

    ![Efetuar push das alterações para um repositório remoto](media/version-control-git11.png)

## <a name="publishing-a-new-project"></a>Publicar um novo projeto

A caixa de diálogo Novo projeto pode ser usada para criar um novo projeto com um repositório git local. Para habilitá-lo, selecione a caixa de seleção **Usar o git para controle de versão**, conforme ilustrado na captura de tela a seguir. Isso inicializará seu repositório e adicionará um arquivo .gitignore opcional:

![Criar novo projeto com suporte ao git](media/version-control-git-publish-new1.png)

Siga as etapas abaixo para efetuar push do seu novo repositório local para um novo repositório do GitHub:

> [!NOTE]
> Se você ainda não tiver criado um repositório do GitHub, consulte a seção [Criando um repositório remoto no GitHub](#creating-a-remote-repo-on-github).

1. Crie sua primeira confirmação acessando o **controle de versão > revisar e confirmar** na barra de menus.

2. Na guia Status, escolha **Confirmar** no canto superior esquerdo.

3. Escreva uma mensagem de confirmação, por exemplo "Primeira Confirmação", depois clique em **Confirmar**:

    ![Confirmar alterações inicias para o repositório git](media/version-control-git-publish-new2.png)

4. Em seguida, na barra de menus, vá para **Controle de versão > Gerenciar Branches e Remotos**.

5. Vá para a guia **Fontes Remotas** e, em seguida, clique em **Adicionar**.

6. Na janela **Fonte Remota**, adicione os detalhes do seu repositório GitHub criado anteriormente e clique em **OK**:

    ![Configurar fontes remotas para o repositório git](media/version-control-git-publish-new3.png)

7. Feche a janela **Configuração do Repositório Git** e depois, na barra de menus, acesse **Controle de Versão > Efetuar Push das Alterações**.

8. Na janela **Efetuar Push ao Repositório**, clique no botão **Efetuar Push das Alterações**:

    ![Efetuar push das alterações para o repositório remoto](media/version-control-git-publish-new4.png)

9. Quando solicitado, insira seu nome de usuário do GitHub e a senha.

> [!NOTE]
> Se sua conta tiver a 2FA (autenticação de dois fatores) habilitada, você precisará criar um token de acesso, que será usado no lugar de uma senha. Se você não criou um token de acesso, siga as etapas na documentação de [Token de acesso](https://help.github.com/articles/creating-an-access-token-for-command-line-use/) do Git.

O Visual Studio para Mac agora efetuará push das alterações para o repositório remoto do GitHub:

![Confirmação de que a operação efetuar push foi concluída com êxito](media/version-control-git11.png)

## <a name="clone-an-existing-repository"></a>Clonar um repositório existente

Provavelmente você precisará trabalhar com um repositório do GitHub que exista apenas remotamente e não em seu computador local. Visual Studio para Mac permite clonar esse repositório rapidamente. Siga as etapas abaixo para cloná-lo em seu computador:

1. Na barra de menus, selecione **controle de versão > repositório de clones**:

2. Isso exibe a guia **conectar-se com a URL** :

    ![Guia conectar com a URL com detalhes inseridos](media/version-control-git13.png)

3. Na página do GitHub do repositório remoto, pressione o botão **Clonar ou Baixar** e copie a URL fornecida:

    ![url do github exibida](media/version-control-git14.png)

4. Substitua todo o texto no campo entrada de **URL** na guia **conectar com URL** . Isso preencherá a maioria dos outros campos nesta guia para você, conforme ilustrado na imagem na etapa #2.

5. Insira o diretório no qual você deseja clonar o repositório e pressione **clonagem**.

> [!NOTE]
> Poderão ocorrer problemas se o repositório tiver mais de 4 GB de tamanho.

## <a name="troubleshooting"></a>Solução de problemas

Se houver problemas ao inicializar seu projeto com um repositório remoto vazio, você poderá tentar executar as seguintes etapas:

1. Acesse a pasta da solução.
1. Pressione **Command + Shift + .** para mostrar os arquivos e as pastas ocultos.
1. Se houver uma pasta **.git**, exclua-a.
1. Se houver um arquivo **gitignore**, exclua-o.
1. Pressione **Command + Shift + .** para ocultar os arquivos e as pastas.
1. Abra a solução no VS para Mac.
1. No Painel de Soluções, selecione o nó da solução.
1. Navegue para o menu de Controle de versão e escolha **Publicar no controle de versão**.
1. Siga as etapas do tutorial acima a partir da etapa 6.

## <a name="see-also"></a>Veja também

- [Controle de versão no Visual Studio (no Windows)](/visualstudio/version-control/)
