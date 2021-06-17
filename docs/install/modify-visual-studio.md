---
title: Modificar Visual Studio cargas de trabalho, componentes e & pacotes de idiomas
titleSuffix: ''
description: Saiba como modificar o Visual Studio, passo a passo.
ms.date: 10/12/2020
ms.topic: how-to
ms.custom: acquisition
helpviewer_keywords:
- modify Visual Studio
- change visual studio
- changing Visual Studio
- customize Visual Studio
ms.assetid: 3399ea7b-a291-4a9e-80a1-b861a21afa1d
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 3f4040023dd023db351571482ac2a17c18b46e06
ms.sourcegitcommit: 1f27f33852112702ee35fbc0c02fba37899e4cf5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2021
ms.locfileid: "112112926"
---
# <a name="modify-visual-studio-workloads-components-and-language-packs"></a>Modificar Visual Studio cargas de trabalho, componentes e pacotes de idiomas

::: moniker range="vs-2019"

É fácil modificar o Visual Studio para que ele inclua apenas o que você deseja, quando você deseja. Para fazer isso, abra o Instalador do Visual Studio para adicionar ou remover componentes e cargas de trabalho.

::: moniker-end

::: moniker range="vs-2017"

Não apenas tornamos mais fácil para você personalizar o Visual Studio para corresponder às etapas que deseja realizar, mas também facilitamos a customização do Visual Studio. Para fazer isso, abra o novo Instalador do Visual Studio e faça as alterações que você deseja.

::: moniker-end

## <a name="prerequisites"></a>Pré-requisitos

+ Para instalar, atualizar ou modificar o Visual Studio, faça logon com uma conta que tenha permissões administrativas. Para obter mais informações, consulte [Permissões de usuário e Visual Studio](../ide/user-permissions-and-visual-studio.md).

+ Os procedimentos a seguir pressuem que você tenha uma conexão com a Internet. Para obter mais informações sobre como modificar uma [instalação offline](create-an-offline-installation-of-visual-studio.md) do Visual Studio criada anteriormente, confira as páginas [Atualizar uma instalação baseada em rede do Visual Studio](update-a-network-installation-of-visual-studio.md) e [Controlar as atualizações em implantações baseadas em rede do Visual Studio](controlling-updates-to-visual-studio-deployments.md).

## <a name="launch-the-installer"></a>Iniciar o instalador

Para fazer modificações em sua instalação, você precisa iniciar o Visual Studio instalador.

::: moniker range="vs-2017"

1. Localize o Instalador do Visual Studio no computador.

     Por exemplo, em um computador que executa o Windows 10, selecione **Iniciar** e, em seguida, role até a letra **I**, onde ele está listado como **Instalador do Visual Studio**.

     ![Instalador do Visual Studio](media/locate-the-visual-studio-installer.png "Localizar o instalador Microsoft Visual Studio aplicativo")

     >[!TIP]
     >Em alguns computadores, o Instalador do Visual Studio poderá estar listado sob a letra **“M”** como **Instalador do Microsoft Visual Studio**.<br/><br/> Como alternativa, encontre o Instalador do Visual Studio no seguinte local: `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. Abra o instalador e escolha **Modificar**.

     ![Iniciar ou modificar Visual Studio](media/modify-visual-studio.png "Modificar o Visual Studio 2017")

     > [!IMPORTANT]
     > Se houver uma atualização pendente, o botão Modificar estará em um local diferente. Dessa forma, você pode modificar o Visual Studio sem atualizá-lo, caso queria. Clique em **Mais** e, em seguida, escolha **Modificar**.
     >
     > ![Atualizar ou modificar o Visual Studio](media/modify-or-update-visual-studio.png "Atualizar ou modificar Visual Studio 2017")

::: moniker-end

::: moniker range="vs-2019"

1. Localize o **Instalador do Visual Studio** no computador.

     No Menu Iniciar do Windows, você pode pesquisar "instalador".

     ![Instalador do Visual Studio](media/vs-2019/visual-studio-installer.png "Pesquise a Instalador do Visual Studio")

     > [!NOTE]
     > Também é possível encontrar o Instalador do Visual Studio no seguinte local:
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    Talvez você precise atualizar o instalador antes de continuar. Nesse caso, siga os prompts.

1. No instalador, procure a edição do Visual Studio instalada por você e escolha **Modificar**.

     ![Escolha Visual Studio edição e, em seguida, modifique](media/vs-2019/vs-installer-modify.png "Escolha Visual Studio edição 2019 e modifique")

     > [!IMPORTANT]
     > Se houver uma atualização pendente, o botão Modificar estará em um local diferente. Dessa forma, você pode modificar Visual Studio sem atualizá-lo, caso queira. Escolha **Mais** e, em seguida, **escolha Modificar**.
     >
     > ![Atualizar ou modificar o Visual Studio](media/vs-2019/modify-update-visual-studio.png "Atualizar ou modificar Visual Studio 2019")

::: moniker-end

## <a name="change-workloads-or-individual-components"></a>Alterar cargas de trabalho ou componentes individuais

::: moniker range="vs-2017"

 As [cargas de trabalho](https://visualstudio.microsoft.com/vs/support/selecting-workloads-visual-studio-2017/) contêm os recursos necessários para a linguagem de programação ou a plataforma que está sendo usada. Use cargas de trabalho para modificar o Visual Studio para que ele dê suporte ao trabalho que você deseja fazer, quando desejar fazê-lo.

1. No Instalador do Visual Studio, escolha a guia **Cargas** de trabalho e selecione ou desmarque as cargas de trabalho que você deseja.

   Como alternativa, se você não quiser usar cargas de trabalho para  personalizar sua instalação do Visual Studio, escolha a guia Componentes Individuais e selecione os componentes que você deseja e siga os prompts.

    ![Caixa de diálogo de instalação do Visual Studio 2017](media/modify-workloads.png "Escolher uma carga de trabalho Visual Studio 2019")

1. Escolha se deseja aceitar a opção padrão **Instalar durante o download** ou a opção **Baixar tudo, depois instalar**.

    ![Visual Studio opções de instalação do 2017](media/vs-2019/vs-installer-choose-install-or-download.png "Escolha instalar durante o download ou para baixar primeiro e instalar posteriormente")

    A opção "Baixar tudo, depois instalar" é útil se você deseja baixar primeiro e instalar mais tarde.

1. Escolha **Modificar**.

1. Se desejar, escolha a guia **Cargas de** trabalho e selecione ou desmarque as cargas de trabalho desejadas.


1. Depois que as novas cargas de trabalho são instaladas, **escolha** Iniciar no Instalador do Visual Studio para abrir Visual Studio.

::: moniker-end

::: moniker range="vs-2019"

 As cargas de trabalho contêm os recursos necessários para a linguagem de programação ou plataforma que você está usando. Use cargas de trabalho para modificar o Visual Studio para que ele dê suporte ao trabalho que você deseja fazer, quando desejar fazê-lo.

 > [!TIP]
>Para obter mais informações sobre quais pacotes de ferramentas e componentes você precisa para desenvolvimento, [consulte Visual Studio cargas de trabalho](https://visualstudio.microsoft.com/vs/#workloads).

1. No Instalador do Visual Studio, escolha a guia **Cargas** de trabalho e selecione ou desmarque as cargas de trabalho que você deseja.

    ![Visual Studio caixa de diálogo de instalação do 2019](media/vs-2019/vs-installer-modify-workloads.png "Escolher uma carga de trabalho Visual Studio 2019")

1. Escolha se deseja aceitar a opção padrão **Instalar durante o download** ou a opção **Baixar tudo, depois instalar**.

    ![Visual Studio opções de instalação do 2019](media/vs-2019/vs-installer-choose-install-or-download.png "Escolha instalar durante o download ou para baixar primeiro e instalar posteriormente")

    A opção "Baixar tudo, depois instalar" é útil se você deseja baixar primeiro e instalar mais tarde.

1. Escolha **Modificar**.

1. Depois que as novas cargas de trabalho são instaladas, **escolha** Iniciar no Instalador do Visual Studio para abrir Visual Studio.

::: moniker-end


>[!TIP]
> Para obter informações sobre o SQL Server Data Tools (SSDT), consulte Baixar e instalar [o SSDT para Visual Studio](/sql/ssdt/download-sql-server-data-tools-ssdt?view=sql-server-ver15&preserve-view=true).

## <a name="modify-language-packs"></a>Modificar pacotes de idiomas

Por padrão, o instalador corresponde ao idioma do sistema operacional quando é executado pela primeira vez. No entanto, você pode alterar o idioma sempre que quiser. 

Para fazer isso:
1. Escolha a **guia Pacotes de idiomas** na Instalador do Visual Studio.
2. Selecione o idioma de sua preferência.
3. Siga os prompts.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Lista de IDs de componente e carga de trabalho do Visual Studio](workload-and-component-ids.md)
* [Atualizar o Visual Studio](update-visual-studio.md)
* [Atualizar uma instalação em rede do Visual Studio](update-a-network-installation-of-visual-studio.md)
* [Desinstalar o Visual Studio](uninstall-visual-studio.md)
