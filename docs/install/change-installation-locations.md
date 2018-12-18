---
title: Selecionar locais de instalação no Visual Studio 2017
description: Saiba como reduzir o volume de instalação na unidade do sistema mudando a localização do cache de download, dos componentes compartilhados, dos SDKs e das ferramentas para unidades diferentes.
ms.date: 11/07/2018
ms.technology: vs-acquisition
ms.prod: visual-studio-dev15
ms.topic: conceptual
helpviewer_keywords:
- change installation locations for Visual Studio
- select an installation location for Visual Studio files
- move installation files to different drives
- use the D drive
author: TerryGLee
ms.author: tglee
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: ed3b54674c24e3becf62e7568be127344104de0f
ms.sourcegitcommit: 0a8ac5f2a685270d9ca79bb39d26fd90099bfa29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2018
ms.locfileid: "51295027"
---
# <a name="select-the-installation-locations-in-visual-studio-2017"></a>Selecionar os locais de instalação no Visual Studio 2017

**Novidade no 15.7**: você pode reduzir o volume de instalação do Visual Studio na unidade do sistema alterando a localização de alguns dos arquivos. Especificamente, você pode usar uma localização diferente para o cache de download, para os componentes compartilhados, os SDKs e os arquivos de ferramentas.

   > [!NOTE]
   > Há algumas ferramentas e SDKs que têm regras diferentes sobre o local em que podem ser instalados. Essas ferramentas e SDKs são instalados em sua unidade do sistema, mesmo que você escolha outra localização.

Pronto para começar? Veja como.

1. Ao instalar o Visual Studio, escolha a guia **Locais de instalação**.

   ![Visual Studio 2017 – Selecionar a localização de instalação](media/vs-installation-locations.png "Selecionar a localização de instalação.")

1. Na seção **IDE do Visual Studio**, aceite o padrão. O Visual Studio instala o produto principal e inclui arquivos específicos desta versão do Visual Studio.

   ![Seção de IDE do Visual Studio da guia Localizações de Instalação](media/vs-installation-locations-ide.png "Aceitar o padrão para a seção de IDE do Visual Studio da guia Localização de Instalações.")

   > [!TIP]
   > Se a unidade do sistema é uma SSD (unidade de estado sólido), recomendamos que você aceite a localização padrão na unidade do sistema. Por quê? Ao desenvolver com o Visual Studio, você lê e grava em vários arquivos, aumentando a atividade de E/S do disco. É melhor escolher sua unidade mais rápida para lidar com a carga.

1. Na seção **Cache de download**, decida se deseja manter o cache de download e, em seguida, decida em que local você deseja armazenar os arquivos.

     ![Seção Cache de Download da guia Locais de Instalação](media/vs-installation-locations-cache.png "Escolher se deseja manter o cache de download após a instalação e, em seguida, especificar a unidade em que você deseja armazenar os arquivos.")

    1. Marque ou desmarque **Manter o cache de download após a instalação**.

       Se você optar por não manter o cache de download, o local será usado somente temporariamente. Essa ação não afetará ou excluirá arquivos de instalações anteriores.

    1. Especifique a unidade na qual deseja armazenar os manifestos e os arquivos de instalação do cache de download.

        Por exemplo, se você selecionar a carga de trabalho "Desenvolvimento para desktop com C++", o tamanho temporário necessário será de 1,58 GB na unidade do sistema, que será liberado assim que a instalação for concluída.

       > [!IMPORTANT]
       > Essa localização é definida com sua primeira instalação e não pode ser alterada posteriormente usando a interface do usuário do instalador. Em vez disso, você precisará [usar parâmetros de linha de comando](use-command-line-parameters-to-install-visual-studio.md) para mover o cache de download.

1. Na seção **Componentes, SDKs e ferramentas compartilhados**, especifique a unidade na qual você deseja armazenar os arquivos compartilhados pelas instalações lado a lado do Visual Studio. Os SDKs e as ferramentas também são armazenados nesse diretório.

   ![Seção de Componentes, Ferramentas e SDKs Compartilhados da guia Locais de Instalação](media/vs-installation-locations-shared.png "Especificar a localização em que você deseja armazenar SDKs, ferramentas e componentes compartilhados.")

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Consulte também

* [Instalar o Visual Studio 2017](install-visual-studio.md)
* [Atualizar o Visual Studio 2017](update-visual-studio.md)
* [Modificar o Visual Studio 2017](update-visual-studio.md)
* [Desinstalar o Visual Studio 2017](uninstall-visual-studio.md)
