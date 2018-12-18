---
title: 'Passo a passo: Publicando uma extensão do Visual Studio | Microsoft Docs'
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- publishing web controls
- web controls, publishing
ms.assetid: a7816161-0490-4043-86f5-0f7331ed83b3
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: ae0b9d48e2a2292229b40e3aaf2a1c755e4c844e
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49815735"
---
# <a name="walkthrough-publish-a-visual-studio-extension"></a>Passo a passo: Publicar uma extensão do Visual Studio

Este passo a passo mostra como publicar uma extensão do Visual Studio no Visual Studio Marketplace. Quando você adiciona sua extensão no Marketplace, os desenvolvedores podem usar **extensões e atualizações** para navegar pelas extensões novas e atualizadas.

## <a name="prerequisites"></a>Pré-requisitos

 Para seguir este passo a passo, você deve instalar o SDK do Visual Studio. Para obter mais informações, consulte [instalar o SDK do Visual Studio](../extensibility/installing-the-visual-studio-sdk.md).

## <a name="create-a-visual-studio-extension"></a>Criar uma extensão do Visual Studio

Este artigo usa uma extensão de VSPackage padrão, mas as etapas são válidas para cada tipo de extensão.

1. Criar um VSPackage no c#, chamado `TestPublish` que possui um comando de menu. Para obter mais informações, consulte [criar sua primeira extensão: Olá, mundo](../extensibility/extensibility-hello-world.md).

## <a name="package-your-extension"></a>Empacotar sua extensão

1. Atualizar a extensão *.vsixmanifest* com as informações corretas sobre o nome do produto, autor e versão.

   ![atualizar a extensão vsixmanifest](media/update-extension-vsixmanifest.png)

2. Compile sua extensão **versão** modo. Agora sua extensão é empacotada como um VSIX na pasta \bin\Release.

3. Você pode clicar duas vezes o VSIX para verificar a instalação.

## <a name="test-the-extension"></a>A extensão de teste

 Antes de distribuir a extensão, compilar e testar para verificar se que ele está instalado corretamente na instância experimental do Visual Studio.

1. No Visual Studio, inicie a depuração para abrir uma instância experimental do Visual Studio.

2. Na instância experimental, vá para o **ferramentas** menu e clique em **extensões e atualizações**. A extensão TestPublish deve aparecer no painel central e ser habilitada.

3. Sobre o **ferramentas** menu, verifique se você vir o comando de teste.

## <a name="publish-the-extension-to-the-visual-studio-marketplace"></a>Publicar a extensão para o Visual Studio Marketplace

1. Certifique-se de que você criou a versão de lançamento da sua extensão e que ela seja atualizada.

2. Em um navegador da web, abra o [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) site.

3. No canto superior direito, clique em **entrar**.

4. Use sua conta da Microsoft para entrar. Se você não tiver uma conta da Microsoft, você pode criar um neste momento.

5. Clique em **publicar extensões**.  Essa opção, você é direcionado para a página Gerenciar todas as suas extensões. Se você não tiver uma conta de editor, você precisará criar um neste momento.

   ![Carregar no Marketplace](media/upload-to-marketplace.png)

6. Escolha o editor que você deseja usar para carregar sua extensão. Você pode alterar os editores clicando em nomes de publicador listados à esquerda. Clique em **nova extensão** e selecione **Visual Studio**.

7. Na **1: carregar a extensão**, você pode optar por carregar um arquivo VSIX diretamente no Visual Studio Marketplace ou simplesmente adicionar um link para seu próprio site. Neste exemplo, a extensão *TestPublish.vsix* é carregado. Arraste e solte sua extensão ou use o **clique** link para navegar para o arquivo. Encontre sua extensão na pasta \bin\Release do projeto.  Clique em **Continue**.

8. Na **2: fornecer detalhes da extensão**, alguns campos são preenchidos automaticamente da *vsixmanifest* arquivo da sua extensão. Encontre mais detalhes sobre cada abaixo:

    * **Nome interno** é usado na URL da página de detalhes da extensão. Por exemplo, publicar uma extensão sob o nome do publicador "myname" e especificando o nome interno seja "extensão my" resulta em uma URL de "marketplace.visualstudio\.com/items?itemName=myname.myextension" para obter detalhes da sua extensão página.
    
    * **Nome de exibição** da sua extensão. Esse nome é preenchido automaticamente do *vsixmanifest* arquivo.
   
    * **Versão** número da extensão que você está carregando. Esta versão é preenchido automaticamente do *vsixmanifest* arquivo.
    
    * **ID do VSIX** é o identificador exclusivo que o Visual Studio usa para a sua extensão. Esse identificador é necessário se você gostaria de ter sua extensão atualizadas automaticamente. Esse identificador é preenchido automaticamente do *vsixmanifest* arquivo.
    
   * **Logotipo** que é usado para a sua extensão. Esse logotipo é preenchido automaticamente do *vsixmanifest* arquivo se fornecido.
    
     * **Descrição breve** do que faz a sua extensão. Essa descrição é preenchido automaticamente do *vsixmanifest* arquivo.
    
     * **Visão geral** é um bom lugar para incluir capturas de tela e informações detalhadas sobre o que faz a sua extensão.
    
     * **Suporte para versões do Visual Studio** permite que você escolha quais versões do Visual Studio que sua extensão funcionará em. Sua extensão for instalada apenas para essas versões.
    
     * * * Suporte para o Visual Studio edition permite que você escolha quais edições do Visual Studio que sua extensão funcionará em. Sua extensão for instalada apenas para essas edições.
    
     * **Tipo**. O tipo mais comum de extensões são **ferramentas**.
    
     * **Categorias**. Escolha até três que são uma opção melhor para sua extensão.
    
     * **Marcas** são palavras-chave que ajudam os usuários a encontrar sua extensão. As marcas podem ajudar a aumentar a relevância de pesquisa de suas extensões no Marketplace.
    
     * **Categoria de preços** é o custo da sua extensão.
    
     * **Repositório de código fonte** permite que você compartilhe um link para seu código-fonte com a comunidade.
    
     * **Permitir perguntas e respostas para a sua extensão** permite que os usuários deixe perguntas em sua página de entrada de extensão.

9. Clique em **salvar e carregar**. Essa opção retorná-lo ao seu editor de página Gerenciar. Sua extensão ainda não foi publicada. Para publicar sua extensão, clique com botão direito em sua extensão e selecione **tornar público**. Você pode exibir a sua extensão de aparência, como no Marketplace, selecionando **extensão do modo de exibição**. Para números de aquisição, clique em **relatórios**. Para fazer alterações em sua extensão, clique em **editar**.

   ![Menu da entrada de extensão](media/extension-entry-menu.png)

10. Depois de clicar em **tornar público**, sua extensão agora é pública. Pesquise no Visual Studio Marketplace para a sua extensão.

## <a name="add-additional-users-to-manage-your-publisher-account"></a>Adicionar usuários adicionais para gerenciar sua conta de editor

Marketplace dá suporte a concessão de permissões de usuários adicionais para acessar e gerenciar uma conta de editor.

1. Navegue até a conta de editor que você deseja acrescentar usuários adicionais ao.

2. Selecione **membros** e clique em **Add**.

   ![Adicionar usuário adicional](media/add-users.png)

3. Em seguida, você pode especificar o endereço de email do usuário que você deseja adicionar e conceder o nível certo de acesso sob **selecionar uma função**.  Você pode escolher entre as seguintes opções:

   * **Criador**: O usuário pode publicar extensões, mas não é possível exibir ou gerenciar extensões publicadas por outros usuários.
  
   * **Leitor**: O usuário pode exibir as extensões, mas não é possível publicar ou gerenciar extensões.
  
   * **Colaborador**: O usuário pode publicar e gerenciar extensões, mas não é possível editar configurações do publicador ou gerenciar o acesso.
  
   * **Proprietário**: O usuário pode publicar e gerenciar extensões, edite as configurações do publicador e gerenciar o acesso.
  
## <a name="install-the-extension-from-the-visual-studio-marketplace"></a>Instalar a extensão do Visual Studio Marketplace

Agora que a extensão for publicada, instalá-lo no Visual Studio e testá-lo lá.

1. No Visual Studio, sobre o **ferramentas** menu, clique em **extensões e atualizações**.

2. Clique em **Online** e, em seguida, pesquise por **TestPublish**.

3. Clique em **Baixar**. Então, a extensão está agendada para instalação.

4. Para concluir a instalação, feche todas as instâncias do Visual Studio.

## <a name="remove-the-extension"></a>Remover a extensão

Você pode remover a extensão do Visual Studio Marketplace e do seu computador.

### <a name="to-remove-the-extension-from-the-visual-studio-marketplace"></a>Para remover a extensão do Visual Studio Marketplace

1. Abra o [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) site.

2. No canto superior direito, clique em **publicar** extensões. Escolher o editor que você usou para publicar **TestPublish**. Na listagem **TestPublish** é exibida.

3. Clique com botão direito na entrada de extensão e clique em **remover**. Você será solicitado para confirmar se deseja remover a extensão. Clique em **OK**.

### <a name="to-remove-the-extension-from-your-computer"></a>Para remover a extensão do seu computador

1. No Visual Studio, sobre o **ferramentas** menu, clique em **extensões e atualizações**.

2. Selecione **TestPublish** e, em seguida, clique em **desinstalar**. Então, a extensão está agendada para desinstalação.

3. Para concluir a desinstalação, feche todas as instâncias do Visual Studio.
