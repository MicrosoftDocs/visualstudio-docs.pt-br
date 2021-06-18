---
title: Desinstalar o Visual Studio
titleSuffix: ''
description: Saiba como desinstalar o Visual Studio, passo a passo.
ms.date: 10/12/2020
ms.custom: seodec18
ms.topic: how-to
f1_keywords:
- uninstall
- uninstall Visual Studio
ms.assetid: 0e445255-b796-426d-ad93-a4d8e36da2c5
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 7d34a5be9598682982c3918aafec7725e59d6f92
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306781"
---
# <a name="uninstall-visual-studio"></a>Desinstalar o Visual Studio

Esta página guia você pela desinstalação do Visual Studio, nosso pacote integrado de ferramentas de produtividade para desenvolvedores.

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Desinstalar o Visual Studio para Mac](/visualstudio/mac/uninstall).

> [!TIP]
> Se você estiver tendo problemas com sua instância do Visual Studio, experimente a **ferramenta** Reparar. Para obter mais informações, consulte [Reparar Visual Studio](../install/repair-visual-studio.md). 
>
> Se você quiser alterar o local de alguns dos arquivos Visual Studio, é possível fazer isso sem desinstalar a instância atual. Para obter mais informações, [consulte Selecionar os locais de instalação no Visual Studio](../install/change-installation-locations.md).
>
> Para ver dicas gerais de solução de problemas, consulte [Solucionar Visual Studio problemas de instalação e atualização.](../install/troubleshooting-installation-issues.md)

::: moniker range="vs-2017"

1. Localize o Instalador do Visual Studio no computador.

     Por exemplo, em um computador que executa a Atualização de Aniversário do Windows 10 ou posterior, selecione **Iniciar** e role até a letra **V**, onde ele estará listado como **Instalador do Visual Studio**.

     ![Instalador do Visual Studio](media/locate-the-visual-studio-installer.png "Localizar o instalador Microsoft Visual Studio aplicativo")

   > [!NOTE]
   > Em alguns computadores, o Instalador do Visual Studio poderá estar listado sob a letra **“M”** como **Instalador do Microsoft Visual Studio**.<br/><br/> Como alternativa, encontre o Instalador do Visual Studio no seguinte local: `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. No instalador, procure a edição do Visual Studio instalada por você. Em seguida, escolha **Mais** e depois **Desinstalar**.

     ![Desinstalar o Visual Studio 2017](media/uninstall-visual-studio.png "Desinstalar o Visual Studio 2017")

1. Clique em **OK** para confirmar sua escolha.

Se você mudar de ideia posteriormente e desejar reinstalar o Visual Studio 2017, inicie o Instalador do Visual Studio novamente e, em seguida, selecione **Instalar** na tela de seleção.

## <a name="uninstall-visual-studio-installer"></a>Desinstalar o Instalador do Visual Studio

Para remover completamente todas as instalações do Visual Studio 2017 e o Instalador do Visual Studio do seu computador, desinstale-os em Aplicativos e Recursos.

1. No Windows 10, digite **Aplicativos e Recursos** na caixa "Digite aqui para pesquisar".
1. Localize **Microsoft Visual Studio 2017** (ou **Visual Studio 2017**).
1. Escolha **Desinstalar**.
1. Em seguida, localize **Instalador do Microsoft Visual Studio**.
1. Escolha **Desinstalar**.

::: moniker-end

::: moniker range=">=vs-2019"

1. Localize o **Instalador do Visual Studio** no computador.

     No Menu Iniciar do Windows, você pode pesquisar "instalador".

     ![Instalador do Visual Studio](media/vs-2019/visual-studio-installer.png "Pesquise a Instalador do Visual Studio")

     > [!NOTE]
     > Também é possível encontrar o Instalador do Visual Studio no seguinte local:
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    Talvez você precise atualizar o instalador antes de continuar. Nesse caso, siga os prompts.

1. No instalador, procure a edição do Visual Studio instalada por você. Em seguida, escolha **Mais** e depois **Desinstalar**.

     ![Desinstalar Visual Studio 2019](media/vs-2019/vs-installer-uninstall.png "Desinstalar Visual Studio 2019")

1. Clique em **OK** para confirmar sua escolha.

     ![Desinstalar Visual Studio confirmação](media/vs-2019/uninstall-visualstudio-confirm.png "Confirme se você deseja desinstalar o Visual Studio 2019")

Se você mudar de ideia mais tarde e quiser reinstalar o Visual Studio 2019 ou 2022, inicie o Instalador do Visual Studio novamente, escolha a guia Disponível, escolha a edição do Visual Studio que deseja instalar e selecione **Instalar**. 

## <a name="uninstall-visual-studio-installer"></a>Desinstalar o Instalador do Visual Studio

Para remover todas as instalações do Visual Studio 2019, Visual Studio 2022 e o Instalador do Visual Studio do seu computador, desinstale-o de Aplicativos & Recursos.

1. No Windows 10, digite **Aplicativos e Recursos** na caixa "Digite aqui para pesquisar".
1. Encontre **Visual Studio 2019** ou **Visual Studio 2022.**
1. Escolha **Desinstalar**.
1. Em seguida, localize **Instalador do Microsoft Visual Studio**.
1. Escolha **Desinstalar**.

::: moniker-end

## <a name="remove-all-files"></a>Remover todos os arquivos

Se você tiver um erro catastrófico e não puder desinstalar o Visual Studio usando as instruções anteriores, haverá uma opção de "último recurso" que você pode considerar usando. Para obter mais informações sobre como remover todos os Visual Studio de instalação e informações do produto completamente, consulte a [página Remover Visual Studio](remove-visual-studio.md) dados.

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Modificar o Visual Studio](modify-visual-studio.md)
* [Atualizar o Visual Studio](update-visual-studio.md)
