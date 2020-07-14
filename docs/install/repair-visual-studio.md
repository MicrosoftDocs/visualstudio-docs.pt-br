---
title: Reparar o Visual Studio
titleSuffix: ''
description: Saiba como reparar uma instalação do Visual Studio 2017
ms.date: 06/15/2020
ms.custom: seodec18
ms.topic: how-to
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: fda72206059e5c14c46d332e44ea0de481004296
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85418958"
---
# <a name="repair-visual-studio"></a>Reparar o Visual Studio

Às vezes, a instalação do Visual Studio é danificada ou corrompida. Um reparo é útil para corrigir problemas de tempo de instalação em todas as operações de instalação, incluindo atualizações.

## <a name="when-to-use-repair"></a>Quando usar o reparo
* Se você tiver problemas de carga de instalação. Isso pode acontecer quando a gravação do arquivo no disco não é bem-sucedida e não pode ser corrigida com a exclusão do arquivo corrompido. O reparo pode adquirir novamente os arquivos necessários. 
* Se você estiver tendo problemas de download no lado do cliente. Supondo que você resolveu quaisquer problemas de conexão ou proxy, o reparo pode ajudar. 
* Se você estiver tendo problemas para atualizar o Visual Studio. O reparo corrige muitos problemas comuns de atualização. 

> [!TIP] 
> Se o problema de instalação for causado por um problema em um serviço Windows subjacente, como Windows Installer, o reparo poderá atingir o mesmo problema. Os problemas do sistema podem incluir uma conexão de internet instável ou Windows Installer interrompida. Para verificar se há um problema do sistema, use o relatório de erros gerado pela operação de instalação.

> [!NOTE] 
> O reparo do Visual Studio redefine as configurações do usuário e instala novamente os assemblies que você já tem. Se você estiver enfrentando um problema de produto, crie um [tíquete de comentários do Visual Studio](https://developercommunity.visualstudio.com/content/problem/post.html?space=8), pois o reparo pode não resolver o problema.

## <a name="how-to-repair"></a>Como reparar
::: moniker range="vs-2017"

1. Localize o **Instalador do Visual Studio** no computador.

     Por exemplo, em um computador que executa a Atualização de Aniversário do Windows 10 ou posterior, selecione **Iniciar** e, em seguida, role até a letra **V**, onde ele estará listado como **Instalador do Visual Studio**.

   > [!NOTE]
   > Em alguns computadores, o Instalador do Visual Studio poderá estar listado sob a letra **“M”** como **Instalador do Microsoft Visual Studio**.
   >
   > Como alternativa, encontre o Instalador do Visual Studio no seguinte local: `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

1. Abra o instalador, escolha **Mais** e, em seguida, escolha **Reparar**.

    ![Reparar o Visual Studio do Instalador do Visual Studio](media/repair-visual-studio.png "Reparar o Visual Studio do Instalador do Visual Studio")

   > [!NOTE]
   > Reparar o Visual Studio redefinirá o ambiente. As personalizações locais, como as extensões do usuário instaladas sem elevação, as configurações de usuário e os perfis serão removidos. As configurações sincronizadas, como temas, cores, associações de teclas serão restauradas.
   >

   > [!TIP]
   > A opção **Reparar** aparecerá apenas em instâncias instaladas do Visual Studio. Se você não vir a opção **Reparar**, pode ser que tenha selecionado **Mais** em uma versão que estava listada no Instalador do Visual Studio como "Disponível" em vez de "Instalada".

::: moniker-end

::: moniker range="vs-2019"

1. Localize o **Instalador do Visual Studio** no computador.

     Por exemplo, em um computador que executa o Windows 10, selecione **Iniciar** e, em seguida, role até a letra **I**, onde ele está listado como **Instalador do Visual Studio**.

     ![Abra o Instalador do Visual Studio](media/vs-2019/vs-installer-windows-start.png "Abra o Instalador do Visual Studio")

     > [!NOTE]
     > Também é possível encontrar o Instalador do Visual Studio no seguinte local:
     >
     > `C:\Program Files (x86)\Microsoft Visual Studio\Installer\vs_installer.exe`

    Talvez você precise atualizar o instalador antes de continuar. Nesse caso, siga os prompts.

1. No instalador, procure a edição do Visual Studio instalada por você. Em seguida, escolha **Mais** e escolha **Reparar**.

     ![Reparar o Visual Studio 2019](media/vs-2019/vs-installer-repair.png "Reparar o Visual Studio 2019")

   > [!NOTE]
   > Reparar o Visual Studio redefinirá o ambiente. As personalizações locais, como as extensões do usuário instaladas sem elevação, as configurações de usuário e os perfis serão removidos. As configurações sincronizadas, como temas, cores, associações de teclas serão restauradas.
   >

   > [!TIP]
   > A opção **Reparar** aparecerá apenas em instâncias instaladas do Visual Studio. Se você não vir a opção **Reparar**, pode ser que tenha selecionado **Mais** em uma versão que estava listada no Instalador do Visual Studio como "Disponível" em vez de "Instalada".

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Veja também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Atualizar o Visual Studio](update-visual-studio.md)
* [Desinstalar o Visual Studio](uninstall-visual-studio.md)
* [Solução de problemas de instalação e atualização do Visual Studio](troubleshooting-installation-issues.md)
