---
title: Selecionar os locais de instalação
description: Saiba como reduzir o volume de instalação do Visual Studio na unidade do sistema alterando a localização do cache de download, dos componentes compartilhados, dos SDKs e das ferramentas para unidades diferentes. Por exemplo, mover alguns arquivos da unidade C para a unidade D.
ms.date: 03/30/2019
ms.custom: seodec18
ms.topic: how-to
helpviewer_keywords:
- change installation locations for Visual Studio
- select an installation location for Visual Studio files
- move installation files to different drives
- use the D drive
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 5751ddeca2ba690ec29ff905ec7e8330a7199eab
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419114"
---
# <a name="select-the-installation-locations-in-visual-studio"></a>Selecionar os locais de instalação no Visual Studio

::: moniker range="vs-2019"

Reduza o volume de instalação do Visual Studio na unidade do sistema alterando a localização de alguns dos arquivos. Especificamente, você pode usar uma localização diferente para o cache de download, para os componentes compartilhados, os SDKs e os arquivos de ferramentas.

::: moniker-end

::: moniker range="vs-2017"

**Novidade na versão 15,7**: você pode reduzir a superfície de instalação do Visual Studio na unidade do sistema alterando o local de alguns de seus arquivos. Especificamente, você pode usar uma localização diferente para o cache de download, para os componentes compartilhados, os SDKs e os arquivos de ferramentas.

::: moniker-end

   > [!NOTE]
   > Há algumas ferramentas e SDKs que têm regras diferentes sobre o local em que podem ser instalados. Essas ferramentas e SDKs são instalados em sua unidade do sistema, mesmo que você escolha outra localização.

Pronto para começar? Veja como.

::: moniker range="vs-2017"

1. Ao instalar o Visual Studio, escolha a guia **Locais de instalação**.

   ![Visual Studio 2017 – selecione o local de instalação](media/vs-installation-locations.png "Selecione o local de instalação.")

1. Na seção **IDE do Visual Studio**, aceite o padrão. O Visual Studio instala o produto principal e inclui arquivos específicos desta versão do Visual Studio.

   ![Seção IDE do Visual Studio da guia locais de instalação](media/vs-installation-locations-ide.png "Aceite o padrão para a seção IDE do Visual Studio da guia local de instalações.")

   > [!TIP]
   > Se a unidade do sistema é uma SSD (unidade de estado sólido), recomendamos que você aceite a localização padrão na unidade do sistema. Por quê? Ao desenvolver com o Visual Studio, você lê e grava em vários arquivos, aumentando a atividade de E/S do disco. É melhor escolher sua unidade mais rápida para lidar com a carga.

1. Na seção **Cache de download**, decida se deseja manter o cache de download e, em seguida, decida em que local você deseja armazenar os arquivos.

     ![Seção de cache de download da guia locais de instalação](media/vs-installation-locations-cache.png "Escolha se deseja manter o cache de download após a instalação e especifique a unidade em que deseja armazenar os arquivos.")

    1. Marque ou desmarque **Manter o cache de download após a instalação**.

       Se você optar por não manter o cache de download, o local será usado somente temporariamente. Essa ação não afetará ou excluirá arquivos de instalações anteriores.

    1. Especifique a unidade na qual deseja armazenar os manifestos e os arquivos de instalação do cache de download.

        Por exemplo, se você selecionar a carga de trabalho "Desenvolvimento para desktop com C++", o tamanho temporário necessário será de 1,58 GB na unidade do sistema, que será liberado assim que a instalação for concluída.

       > [!IMPORTANT]
       > Essa localização é definida com sua primeira instalação e não pode ser alterada posteriormente usando a interface do usuário do instalador. Em vez disso, você precisará [usar parâmetros de linha de comando](use-command-line-parameters-to-install-visual-studio.md) para mover o cache de download.

1. Na seção **Componentes, SDKs e ferramentas compartilhados**, especifique a unidade na qual você deseja armazenar os arquivos compartilhados pelas instalações lado a lado do Visual Studio. Os SDKs e as ferramentas também são armazenados nesse diretório.

   ![Seção componentes, ferramentas e SDKs compartilhados da guia locais de instalação](media/vs-installation-locations-shared.png "Especifique o local onde você deseja armazenar componentes compartilhados, ferramentas e SDKs.")

::: moniker-end

::: moniker range="vs-2019"

1. Ao instalar o Visual Studio, escolha a guia **Locais de instalação**.

   ![Visual Studio 2019 – selecione o local de instalação](media/vs-2019/vs-installer-installation-locations.png "Selecione o local de instalação.")

1. Na seção **IDE do Visual Studio**, aceite o padrão. O Visual Studio instala o produto principal e inclui arquivos específicos desta versão do Visual Studio.

   > [!TIP]
   > Se a unidade do sistema é uma SSD (unidade de estado sólido), recomendamos que você aceite a localização padrão na unidade do sistema. Por quê? Ao desenvolver com o Visual Studio, você lê e grava em vários arquivos, aumentando a atividade de E/S do disco. É melhor escolher sua unidade mais rápida para lidar com a carga.

1. Na seção **Cache de download**, decida se deseja manter o cache de download e, em seguida, decida em que local você deseja armazenar os arquivos.

    * Marque ou desmarque **Manter o cache de download após a instalação**.

       Se você optar por não manter o cache de download, o local será usado somente temporariamente. Essa ação não afetará ou excluirá arquivos de instalações anteriores.

    * Especifique a unidade na qual deseja armazenar os manifestos e os arquivos de instalação do cache de download.

        Por exemplo, se você selecionar a carga de trabalho "Desenvolvimento para desktop com C++", o tamanho temporário necessário será de 1,58 GB na unidade do sistema, que será liberado assim que a instalação for concluída.

       > [!IMPORTANT]
       > Essa localização é definida com sua primeira instalação e não pode ser alterada posteriormente usando a interface do usuário do instalador. Em vez disso, você precisará [usar parâmetros de linha de comando](use-command-line-parameters-to-install-visual-studio.md) para mover o cache de download.

1. Na seção **Componentes, ferramentas e SDKs compartilhados**, observe que ele usa a mesma unidade que você escolheu na seção "Cache de download". O diretório \Microsoft\VisualStudio\Shared é o local em que o Visual Studio armazena os arquivos que são compartilhados por instalações lado a lado do Visual Studio. Os SDKs e as ferramentas também são armazenados nesse diretório.

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Veja também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Atualizar o Visual Studio](update-visual-studio.md)
* [Modificar o Visual Studio](update-visual-studio.md)
* [Desinstalar o Visual Studio](uninstall-visual-studio.md)
