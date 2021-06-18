---
title: Reparar o Visual Studio
titleSuffix: ''
description: Saiba como reparar uma instalação do Visual Studio 2017
ms.date: 10/12/2020
ms.custom: acquisition
ms.topic: how-to
author: j-martens
ms.author: jmartens
manager: jmartens
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 5fd791b035bc99d46f53d499339a9e9f80a42905
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112306937"
---
# <a name="repair-visual-studio"></a>Reparar o Visual Studio

Às vezes, a instalação do Visual Studio é danificada ou corrompida. Um reparo é útil para corrigir problemas de tempo de instalação em todas as operações de instalação, incluindo atualizações.

## <a name="when-to-use-repair"></a>Quando usar o reparo
* Se você estiver tendo problemas de carga de instalação. Isso pode acontecer quando a escrita do arquivo no disco não é bem-sucedida e não pode ser corrigida excluindo o arquivo corrompido. O reparo pode adquirir os arquivos necessários. 
* Se você estiver tendo problemas de download do lado do cliente. Supondo que você tenha resolvido problemas de conexão ou proxy, o reparo pode ajudar. 
* Se você estiver tendo problemas para atualizar Visual Studio. O reparo corrige muitos problemas comuns de atualização. 

> [!TIP] 
> Se o problema de instalação for causado por um problema em um serviço Windows subjacente, como Windows Installer, o reparo poderá ter o mesmo problema. Problemas sistêmicos podem incluir uma conexão de Windows Installer ou instável com a Internet. Para verificar se há um problema sistêmico, use o relatório de erros gerado da operação de instalação.

> [!NOTE] 
> O reparo Visual Studio redefine as configurações do usuário e reins instala novamente os assemblies que você já tem. Se você estiver enfrentando um problema de produto, crie um [tíquete Visual Studio comentários,](https://aka.ms/feedback/suggest?space=8)pois o reparo pode não resolver o problema.

## <a name="how-to-repair"></a>Como reparar
::: moniker range="vs-2017"

1. Localize o **Instalador do Visual Studio** no computador.

     Por exemplo, em um computador que executa a Atualização de Aniversário do Windows 10 ou posterior, selecione **Iniciar** e, em seguida, role até a letra **V**, onde ele estará listado como **Instalador do Visual Studio**.

   > [!NOTE]
   > Em alguns computadores, o Instalador do Visual Studio poderá estar listado sob a letra **“M”** como **Instalador do Microsoft Visual Studio**.
   >
   > Como alternativa, encontre o Instalador do Visual Studio no seguinte local: `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. Abra o instalador, escolha **Mais** e, em seguida, escolha **Reparar**.

    ![Reparar Visual Studio do Instalador do Visual Studio](media/repair-visual-studio.png "Reparar Visual Studio do Instalador do Visual Studio")

   > [!NOTE]
   > Reparar o Visual Studio redefinirá o ambiente. As personalizações locais, como as extensões do usuário instaladas sem elevação, as configurações de usuário e os perfis serão removidos. As configurações sincronizadas, como temas, cores, associações de teclas serão restauradas.
   >

   > [!TIP]
   > A opção **Reparar** aparecerá apenas em instâncias instaladas do Visual Studio. Se você não vir a opção **Reparar**, pode ser que tenha selecionado **Mais** em uma versão que estava listada no Instalador do Visual Studio como "Disponível" em vez de "Instalada".

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

1. No instalador, procure a edição do Visual Studio instalada por você. Em seguida, escolha **Mais** e escolha **Reparar**.

     ![Reparar Visual Studio 2019](media/vs-2019/vs-installer-repair.png "Reparar Visual Studio 2019")

   > [!NOTE]
   > Reparar o Visual Studio redefinirá o ambiente. As personalizações locais, como as extensões do usuário instaladas sem elevação, as configurações de usuário e os perfis serão removidos. As configurações sincronizadas, como temas, cores, associações de teclas serão restauradas.
   >

   > [!TIP]
   > A opção **Reparar** aparecerá apenas em instâncias instaladas do Visual Studio. Se você não vir a opção **Reparar**, pode ser que tenha selecionado **Mais** em uma versão que estava listada no Instalador do Visual Studio como "Disponível" em vez de "Instalada".

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Atualizar o Visual Studio](update-visual-studio.md)
* [Desinstalar o Visual Studio](uninstall-visual-studio.md)
* [Solução de problemas de instalação e atualização do Visual Studio](troubleshooting-installation-issues.md)
