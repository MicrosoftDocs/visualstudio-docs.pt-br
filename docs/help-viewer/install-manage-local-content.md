---
title: Instalar a documentação de Ajuda local
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- hv_manage
helpviewer_keywords:
- changing content installation source [Help Viewer]
- updating local content [Help Viewer]
- Help Viewer, content installation source
- Help Viewer, updating local content
- Help Viewer, changing content installation source
- installing local content [Help Viewer]
- content installation source [Help Viewer]
- downloading content [Help Viewer]
- removing local content [Help Viewer]
- Help Viewer, removing local content
- Help Viewer, installing local content
- Help Viewer, downloading content
ms.assetid: efd9df4c-2e69-4c50-992c-9678a8d8cf19
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 70bb90856fb88738bbc82434c47e375ea453fd08
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85284900"
---
# <a name="install-and-manage-local-content"></a>Instalar e gerenciar o conteúdo local

Usando o Microsoft Help Viewer, você pode adicionar, remover, atualizar e mover o conteúdo de Ajuda instalado no seu computador para atender às suas necessidades de desenvolvimento de software.

Para gerenciar o conteúdo em seu computador local, faça logon com uma conta que tenha permissões de administrador. Além disso, você poderá não conseguir gerenciar o conteúdo local se trabalhar em um ambiente empresarial, pois os administradores de sistema podem tomar essas decisões para sua organização. Para obter mais informações, consulte o [Guia do administrador do Help Viewer](../help-viewer/administrator-guide.md).

## <a name="change-the-content-installation-source"></a>Alterar a fonte de instalação de conteúdo

Por padrão, o Visualizador de Ajuda instala o conteúdo usando um serviço online da Microsoft como origem. Geralmente, você não deve alterar a fonte de conteúdo, a menos que trabalhe em um ambiente corporativo para o qual um administrador do sistema já tenha instalado conteúdo em outro local.

### <a name="to-change-the-content-installation-source"></a>Para alterar a origem da instalação de conteúdo

1. Na guia **Gerenciar Conteúdo**, escolha o botão de opção **Disco**.

    > [!NOTE]
    > A opção **Disco** não estará disponível se o administrador o impediu de modificar a origem de instalação de conteúdo. Para obter mais informações, consulte o [Guia do administrador do Help Viewer](../help-viewer/administrator-guide.md).

2. Execute uma das seguintes etapas:

    - Insira o caminho de um arquivo *. msha* ou a URL de um ponto de extremidade de serviço.

    - Escolha o botão procurar (**...**) para navegar para um arquivo *. msha* .

    - Na lista, escolha a entrada usada mais recentemente.

## <a name="download-and-install-content-locally"></a>Baixar e instalar o conteúdo localmente

Se você baixar e instalar o conteúdo em seu computador local, poderá exibir tópicos quando não tiver uma conexão de Internet.

> [!IMPORTANT]
> Para instalar o conteúdo, faça logon com uma conta que tenha permissões administrativas.

> [!NOTE]
> Se o IDE do Visual Studio estiver definido como um idioma diferente do inglês, você poderá instalar o conteúdo em inglês, o conteúdo localizado ou ambos. No entanto, nenhum conteúdo aparecerá se você instalar apenas a versão em inglês e a caixa de seleção **Incluir conteúdo em inglês em todas as guias de navegação e solicitações F1** na caixa de diálogo **Opções do Visualizador** estiver desmarcada.

### <a name="to-download-and-install-content"></a>Para baixar e instalar conteúdo

1. Escolha a guia **Gerenciar Conteúdo**.

2. Na lista de conteúdos, escolha o link **Adicionar** ao lado do livro ou dos livros que você deseja baixar e instalar.

     O livro é adicionado à lista **Alterações pendentes** e o tamanho estimado do livro ou dos livros especificados é exibido abaixo da lista. Como alguns livros compartilham tópicos, o tamanho total do download de vários livros pode ser menor do que o resultado da soma dos tamanhos de cada livro especificado.

3. Escolha o botão **Atualizar**.

     O livro ou os livros especificados são instalados junto com todas as atualizações de livros que já estão no seu computador. Os tempos de instalação variam, mas você pode exibir o progresso na barra de status.

## <a name="remove-local-content"></a>Remover o conteúdo local

Você pode economizar espaço em disco removendo conteúdo indesejado do seu computador.

> [!IMPORTANT]
> É preciso ter permissões administrativas para remover conteúdo.

> [!NOTE]
> Nenhum conteúdo aparecerá se o IDE do Visual Studio estiver definido como um idioma diferente do inglês, você remover o conteúdo localizado e a caixa de seleção **Incluir conteúdo em inglês em todas as guias de navegação e solicitações F1** na caixa de diálogo **Opções do Visualizador** estiver desmarcada.

### <a name="to-remove-content"></a>Para remover conteúdo

1. Escolha a guia **Gerenciar Conteúdo**.

2. Na lista de conteúdos, escolha o link **Remover** ao lado do livro ou dos livros que você deseja remover.

     O livro é adicionado à lista **Alterações pendentes**.

3. Escolha o botão **Atualizar**.

     O livro ou os livros especificados são removidos do seu computador.

## <a name="update-local-content"></a>Atualizar o conteúdo local

A barra de status indica quando estão disponíveis atualizações para o conteúdo instalado.

> [!IMPORTANT]
> Se desejar que o **Visualizador da ajuda** verifique automaticamente se há atualizações online, abra a caixa de diálogo **Opções do visualizador** e marque a caixa de seleção **ficar online para verificar se há atualizações de conteúdo** .

### <a name="to-update-local-content"></a>Para atualizar o conteúdo local

- No canto inferior direito da barra de status, escolha o link **Clique aqui para baixar agora**.

Os tempos de atualização podem variar, mas você pode exibir o progresso da atualização na barra de status.

## <a name="move-local-content"></a>Mover o conteúdo local

Você pode economizar espaço em disco movendo conteúdo instalado do computador local para um compartilhamento de rede ou outra partição no computador local.

> [!IMPORTANT]
> Para mover o conteúdo, faça logon com uma conta que tenha permissões administrativas.

### <a name="to-move-local-content"></a>Para mover o conteúdo local

1. Na guia **Gerenciar Conteúdo**, escolha o botão **Mover** em **Caminho do Repositório Local**.

     A caixa de diálogo **Mover Conteúdo** se abre.

2. Na caixa de texto **Para**, insira um local diferente para o conteúdo e, em seguida, escolha o botão **OK**.

3. Escolha o botão **Fechar** quando o conteúdo tiver sido movido.

## <a name="see-also"></a>Veja também

- [Microsoft Help Viewer](../help-viewer/overview.md)