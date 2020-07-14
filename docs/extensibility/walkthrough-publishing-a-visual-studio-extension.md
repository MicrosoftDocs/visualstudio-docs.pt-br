---
title: 'Walkthrough: publicando uma extensão do Visual Studio | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d6bd7a5d9622f7aea7382522dcf69ce660b61ae7
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904732"
---
# <a name="walkthrough-publish-a-visual-studio-extension"></a>Walkthrough: publicar uma extensão do Visual Studio

Este tutorial mostra como publicar uma extensão do Visual Studio para o Visual Studio Marketplace. Quando você adiciona sua extensão ao Marketplace, os desenvolvedores podem usar **extensões e atualizações** para procurar extensões novas e atualizadas.

## <a name="prerequisites"></a>Pré-requisitos

 Para seguir este passo a passos, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-visual-studio-extension"></a>Criar uma extensão do Visual Studio

Este artigo usa uma extensão VSPackage padrão, mas as etapas são válidas para cada tipo de extensão.

1. Crie um VSPackage em C# chamado `TestPublish` que tenha um comando de menu. Para obter mais informações, consulte [criar sua primeira extensão: Olá, mundo](../extensibility/extensibility-hello-world.md).

## <a name="package-your-extension"></a>Empacotar sua extensão

1. Atualize a extensão *. vsixmanifest* com as informações corretas sobre o nome do produto, o autor e a versão.

   ![atualizar vsixmanifest de extensão](media/update-extension-vsixmanifest.png)

2. Crie sua extensão no modo de **versão** . Agora, sua extensão é empacotada como um VSIX na pasta \bin\Release.

3. Você pode clicar duas vezes no VSIX para verificar a instalação.

## <a name="test-the-extension"></a>Testar a extensão

 Antes de distribuir a extensão, crie-a e teste-a para verificar se ela está instalada corretamente na instância experimental do Visual Studio.

1. No Visual Studio, inicie a depuração para abrir uma instância experimental do Visual Studio.

2. Na instância experimental, vá para o menu **ferramentas** e clique em **extensões e atualizações**. A extensão TestPublish deve aparecer no painel central e ser habilitada.

3. No menu **ferramentas** , verifique se você vê o comando de teste.

## <a name="publish-the-extension-to-the-visual-studio-marketplace"></a>Publicar a extensão para o Visual Studio Marketplace

1. Certifique-se de que você criou a versão de lançamento da sua extensão e que ela está atualizada.

2. Em um navegador da Web, abra o site do [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) .

3. No canto superior direito, clique em **entrar**.

4. Use seu conta Microsoft para entrar. Se você não tiver um conta Microsoft, poderá criar um neste ponto.

5. Clique em **extensões de publicação**.  Essa opção o navega para a página Gerenciar para todas as suas extensões. Se você não tiver uma conta de editor, será solicitado a criar uma no momento.

   ![Carregar no Marketplace](media/upload-to-marketplace.png)

6. Escolha o Publicador que você deseja usar para carregar sua extensão. Você pode alterar os Publicadores clicando nos nomes dos editores listados à esquerda. Clique em **nova extensão** e selecione **Visual Studio**.

7. Em **1: carregar a extensão**, você pode optar por carregar um arquivo VSIX diretamente no Visual Studio Marketplace ou apenas adicionar um link para seu próprio site. Neste exemplo, a extensão, *TestPublish. vsix* , é carregada. Arraste e solte sua extensão ou use o link **clique** para procurar o arquivo. Localize sua extensão na pasta \bin\Release do projeto.  Clique em **Continue**.

8. Em **2: fornecer detalhes de extensão**, alguns campos são preenchidos automaticamente do arquivo *Source. Extension. vsixmanifest* de sua extensão. Encontre mais detalhes sobre cada um deles:

    * O **nome interno** é usado na URL da página de detalhes da extensão. Para obter um exemplo, a publicação de uma extensão sob o nome do Publicador "myname" e a especificação do nome interno como "minha extensão" resulta em uma URL de "marketplace. VisualStudio \. com/items? ItemName = myname. MyExtension" para a página de detalhes da extensão.

    * **Nome de exibição** da extensão. Esse nome é preenchido automaticamente a partir do arquivo *Source. Extension. vsixmanifest* .

    * Número de **versão** da extensão que você está carregando. Esta versão é preenchida automaticamente do arquivo *Source. Extension. vsixmanifest* .

    * A **ID do VSIX** é o identificador exclusivo que o Visual Studio usa para sua extensão. Esse identificador será necessário se você quiser que sua extensão seja atualizada automaticamente. Esse identificador é preenchido automaticamente a partir do arquivo *Source. Extension. vsixmanifest* .

    * **Logotipo** usado para sua extensão. Esse logotipo é preenchido automaticamente do arquivo *Source. Extension. vsixmanifest* , se fornecido.

    * **Breve descrição** do que sua extensão faz. Essa descrição é preenchida automaticamente do arquivo *Source. Extension. vsixmanifest* .

    * A **visão geral** é um bom lugar para incluir capturas de tela e informações detalhadas sobre o que sua extensão faz.

    * **As versões do Visual Studio com suporte** permitem escolher em quais versões do Visual Studio sua extensão trabalhará. Sua extensão é instalada somente nessas versões.

    * * * A edição do Visual Studio com suporte permite que você escolha em quais edições do Visual Studio sua extensão trabalhará. Sua extensão é instalada somente nessas edições.

    * **Tipo**. O tipo mais comum de extensões são as **ferramentas**.

    * **Categorias**. Escolha até três que são a melhor opção para sua extensão.

    * **Marcas** são palavras-chave que ajudam os usuários a localizar sua extensão. As marcas podem ajudar a aumentar a relevância de pesquisa de suas extensões no Marketplace.

    * A **categoria de preços** é o custo de sua extensão.

    * O **repositório de código-fonte** permite que você compartilhe um link para o código-fonte com a Comunidade.

    * **Permitir Q&a para sua extensão** permite que os usuários deixem perguntas em sua página de entrada de extensão.

9. Clique em **salvar & carregar**. Essa opção leva você de volta à sua página de gerenciamento do Publicador. Sua extensão ainda não foi publicada. Para publicar sua extensão, clique com o botão direito do mouse em sua extensão e selecione **tornar pública**. Você pode exibir como sua extensão se parecerá no Marketplace selecionando a **extensão de exibição**. Para números de aquisição, clique em **relatórios**. Para fazer alterações em sua extensão, clique em **Editar**.

   ![Menu de entrada de extensão](media/extension-entry-menu.png)

10. Depois de clicar em **tornar público**, sua extensão agora é pública. Pesquise o Visual Studio Marketplace para sua extensão.

## <a name="add-additional-users-to-manage-your-publisher-account"></a>Adicionar usuários adicionais para gerenciar sua conta do Publicador

O Marketplace dá suporte à concessão de permissões adicionais a usuários para acessar e gerenciar uma conta de editor.

1. Navegue até a conta do Publicador à qual você deseja adicionar usuários adicionais.

2. Selecione **Membros** e clique em **Adicionar**.

   ![Adicionar usuário adicional](media/add-users.png)

3. Em seguida, você pode especificar o endereço de email do usuário que deseja adicionar e conceder o nível certo de acesso em **selecionar uma função**.  É possível escolher um das seguintes opções:

   * **Criador**: o usuário pode publicar extensões, mas não pode exibir ou gerenciar extensões publicadas por outros usuários.

   * **Leitor**: o usuário pode exibir extensões, mas não pode publicar ou gerenciar extensões.

   * **Colaborador**: o usuário pode publicar e gerenciar extensões, mas não pode editar as configurações do Publicador ou gerenciar o acesso.

   * **Proprietário**: o usuário pode publicar e gerenciar extensões, editar configurações de Publicador e gerenciar o acesso.

## <a name="install-the-extension-from-the-visual-studio-marketplace"></a>Instalar a extensão do Visual Studio Marketplace

Agora que a extensão foi publicada, instale-a no Visual Studio e teste-a lá.

1. No Visual Studio, no menu **ferramentas** , clique em **extensões e atualizações**.

2. Clique em **online** e procure por **TestPublish**.

3. Clique em **Download**. Em seguida, a extensão é agendada para instalação.

4. Para concluir a instalação, feche todas as instâncias do Visual Studio.

## <a name="remove-the-extension"></a>Remover a extensão

Você pode remover a extensão da Visual Studio Marketplace e do seu computador.

### <a name="to-remove-the-extension-from-the-visual-studio-marketplace"></a>Para remover a extensão da Visual Studio Marketplace

1. Abra o site [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) .

2. No canto superior direito, clique em **publicar** extensões. Escolha o Publicador que você usou para publicar o **TestPublish**. A listagem para **TestPublish** é exibida.

3. Clique com o botão direito do mouse na entrada de extensão e clique em **remover**. Você será solicitado a confirmar se deseja remover a extensão. Clique em **OK**.

### <a name="to-remove-the-extension-from-your-computer"></a>Para remover a extensão do seu computador

1. No Visual Studio, no menu **ferramentas** , clique em **extensões e atualizações**.

2. Selecione **TestPublish** e clique em **desinstalar**. Em seguida, a extensão é agendada para desinstalação.

3. Para concluir a desinstalação, feche todas as instâncias do Visual Studio.
