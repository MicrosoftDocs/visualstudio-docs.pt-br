---
title: Modificar o Visual Studio
titleSuffix: ''
description: Saiba como modificar o Visual Studio, passo a passo.
ms.date: 02/10/2019
ms.topic: how-to
helpviewer_keywords:
- modify Visual Studio
- change visual studio
- changing Visual Studio
- customize Visual Studio
ms.assetid: 3399ea7b-a291-4a9e-80a1-b861a21afa1d
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 2ec3ae3f253997b86c2403ce57d5e8db6e9920b4
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419179"
---
# <a name="modify-visual-studio-by-adding-or-removing-workloads-and-components"></a>Modificar o Visual Studio adicionando ou removendo cargas de trabalho e componentes

::: moniker range="vs-2019"

É fácil modificar o Visual Studio para que ele inclua apenas o que você deseja, quando você deseja. Para fazer isso, abra o Instalador do Visual Studio para adicionar ou remover componentes e cargas de trabalho.

::: moniker-end

::: moniker range="vs-2017"

Não apenas tornamos mais fácil para você personalizar o Visual Studio para corresponder às etapas que deseja realizar, mas também facilitamos a customização do Visual Studio. Para fazer isso, abra o novo Instalador do Visual Studio e faça as alterações desejadas.

::: moniker-end

Veja como.

>[!IMPORTANT]
>Para instalar, atualizar ou modificar o Visual Studio, faça logon com uma conta que tenha permissões administrativas. Para obter mais informações, consulte [permissões de usuário e Visual Studio](../ide/user-permissions-and-visual-studio.md).

>[!NOTE]
> Os procedimentos a seguir pressupõem que você tenha uma conexão com a Internet.
>
> Para obter mais informações sobre como modificar uma [instalação offline](create-an-offline-installation-of-visual-studio.md) do Visual Studio criada anteriormente, confira as páginas [Atualizar uma instalação baseada em rede do Visual Studio](update-a-network-installation-of-visual-studio.md) e [Controlar as atualizações em implantações baseadas em rede do Visual Studio](controlling-updates-to-visual-studio-deployments.md).

## <a name="open-the-visual-studio-installer"></a>Abra o Instalador do Visual Studio

::: moniker range="vs-2017"

1. Localize o Instalador do Visual Studio no computador.

     Por exemplo, em um computador que executa o Windows 10, selecione **Iniciar** e, em seguida, role até a letra **I**, onde ele está listado como **Instalador do Visual Studio**.

     ![Instalador do Visual Studio](media/locate-the-visual-studio-installer.png "Localize o instalador do Microsoft Visual Studio")

     >[!TIP]
     >Em alguns computadores, o Instalador do Visual Studio poderá estar listado sob a letra **“M”** como **Instalador do Microsoft Visual Studio**.<br/><br/> Como alternativa, encontre o Instalador do Visual Studio no seguinte local: `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. Abra o instalador e, em seguida, escolha **Modificar**.

     ![Iniciar ou modificar o Visual Studio](media/modify-visual-studio.png "Modificar o Visual Studio 2017")

     > [!IMPORTANT]
     > Se houver uma atualização pendente, o botão Modificar estará em um local diferente. Dessa forma, você pode modificar o Visual Studio sem atualizá-lo, caso queria. Clique em **Mais** e, em seguida, escolha **Modificar**.
     >
     > ![Atualizar ou modificar o Visual Studio](media/modify-or-update-visual-studio.png "Atualizar ou modificar o Visual Studio 2017")

::: moniker-end

::: moniker range="vs-2019"

1. Localize o Instalador do Visual Studio no computador.

     Por exemplo, em um computador que executa o Windows 10, selecione **Iniciar** e, em seguida, role até a letra **I**, onde ele está listado como **Instalador do Visual Studio**.

     ![Abra o Instalador do Visual Studio no Windows](media/vs-2019/vs-installer-windows-start.png "Abra o Instalador do Visual Studio")

     > [!NOTE]
     > Também é possível encontrar o Instalador do Visual Studio no seguinte local:
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    Talvez você precise atualizar o instalador antes de continuar. Nesse caso, siga os prompts.

1. No instalador, procure a edição do Visual Studio instalada por você e escolha **Modificar**.

     ![Atualizar ou modificar o Visual Studio](media/vs-2019/vs-installer-modify.png "Atualizar ou modificar o Visual Studio 2019")

     > [!IMPORTANT]
     > Se houver uma atualização pendente, o botão Modificar estará em um local diferente. Dessa forma, você pode modificar o Visual Studio sem atualizá-lo, caso queira. Escolha **mais**e, em seguida, escolha **Modificar**.
     >
     > ![Atualizar ou modificar o Visual Studio](media/vs-2019/modify-update-visual-studio.png "Atualizar ou modificar o Visual Studio 2019")

::: moniker-end

## <a name="modify-workloads"></a>Modificar cargas de trabalho

::: moniker range="vs-2017"

 As [cargas de trabalho](https://visualstudio.microsoft.com/vs/support/selecting-workloads-visual-studio-2017/) contêm os recursos necessários para a linguagem de programação ou a plataforma que está sendo usada. Use cargas de trabalho para modificar o Visual Studio para que ele dê suporte ao trabalho que você deseja fazer, quando desejar fazê-lo.

1. Na Instalador do Visual Studio, escolha a guia **cargas de trabalho** e, em seguida, marque ou desmarque as cargas de trabalho desejadas.

    ![Caixa de diálogo de instalação do Visual Studio 2017](media/modify-workloads.png "Escolha uma carga de trabalho no Visual Studio 2019")

1. Escolha se deseja aceitar a opção padrão **Instalar durante o download** ou a opção **Baixar tudo, depois instalar**.

    ![Opções de instalação do Visual Studio 2017](media/vs-2019/vs-installer-choose-install-or-download.png "Escolha instalar durante o download ou para baixar primeiro e instalar mais tarde")

    A opção "Baixar tudo, depois instalar" é útil se você deseja baixar primeiro e instalar mais tarde.

1. Escolha **Modificar**.

1. Depois que as novas cargas de trabalho forem instaladas, escolha **Iniciar** no instalador do Visual Studio para abrir o Visual Studio.

::: moniker-end

::: moniker range="vs-2019"

 As cargas de trabalho contêm os recursos necessários para a linguagem de programação ou plataforma que você está usando. Use cargas de trabalho para modificar o Visual Studio para que ele dê suporte ao trabalho que você deseja fazer, quando desejar fazê-lo.

 > [!TIP]
>Para obter mais informações sobre quais pacotes de ferramentas e componentes são necessários para o desenvolvimento, consulte [cargas de trabalho do Visual Studio](https://visualstudio.microsoft.com/vs/#workloads).

1. No na Instalador do Visual Studio, escolha a guia **cargas de trabalho** e, em seguida, marque ou desmarque as cargas de trabalho desejadas.

    ![Caixa de diálogo de instalação do Visual Studio 2019](media/vs-2019/vs-installer-modify-workloads.png "Escolha uma carga de trabalho no Visual Studio 2019")

1. Escolha se deseja aceitar a opção padrão **Instalar durante o download** ou a opção **Baixar tudo, depois instalar**.

    ![Opções de instalação do Visual Studio 2019](media/vs-2019/vs-installer-choose-install-or-download.png "Escolha instalar durante o download ou para baixar primeiro e instalar mais tarde")

    A opção "Baixar tudo, depois instalar" é útil se você deseja baixar primeiro e instalar mais tarde.

1. Escolha **Modificar**.

1. Depois que as novas cargas de trabalho forem instaladas, escolha **Iniciar** no instalador do Visual Studio para abrir o Visual Studio.

::: moniker-end

## <a name="modify-individual-components"></a>Modificar componentes individuais

Se você não quiser usar cargas de trabalho para personalizar a instalação do Visual Studio, escolha a guia **componentes individuais** na instalador do Visual Studio, selecione os componentes desejados e siga os prompts.

>[!TIP]
> Para obter informações sobre o componente SQL Server Data Tools (SSDT), consulte [baixar e instalar o SSDT para Visual Studio](/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-ver15).

## <a name="modify-language-packs"></a>Modificar pacotes de idiomas

Por padrão, o instalador corresponde ao idioma do sistema operacional quando ele é executado pela primeira vez. No entanto, você pode alterar o idioma sempre que desejar. Para fazer isso, escolha a guia **pacotes de idiomas** na instalador do Visual Studio, selecione o idioma que você preferir e siga os prompts.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Veja também

* [Lista de IDs de componente e carga de trabalho do Visual Studio](workload-and-component-ids.md)
* [Atualizar o Visual Studio](update-visual-studio.md)
* [Atualizar uma instalação em rede do Visual Studio](update-a-network-installation-of-visual-studio.md)
* [Atualizar o Visual Studio enquanto estiver em uma linha de base de manutenção](update-servicing-baseline.md)
* [Atualizações de controle para implantações do Visual Studio com base em rede](controlling-updates-to-visual-studio-deployments.md)
* [Desinstalar o Visual Studio](uninstall-visual-studio.md)
