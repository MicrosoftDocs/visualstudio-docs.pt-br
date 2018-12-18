---
title: Instalar uma versão prévia
description: Instruções para atualizar o Visual Studio para Mac e acessar as versões prévias, incluindo versões prévias do Visual Studio 2019 para Mac.
zone_pivot_groups: mac-ide-version
author: conceptdev
ms.author: crdun
ms.date: 11/03/2018
ms.topic: article
ms.technology: vs-ide-install
ms.assetid: 0E1EF257-9DE4-4653-9DF4-805CE007A1A1
ms.openlocfilehash: b5eea8c2c894b7eeaa13c83ae6698d1297de9297
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52896751"
---
# <a name="install-a-preview-release"></a>Instalar uma versão prévia

::: zone pivot="vsmac2019"

> [!TIP]
> A versão prévia do Visual Studio 2019 para Mac agora está disponível. Pela primeira vez, ela está disponível para instalação lado a lado com a versão estável mais recente do Visual Studio para Mac.

## <a name="requirements-for-the-visual-studio-2019-for-mac-preview"></a>Requisitos para a versão prévia do Visual Studio 2019 para Mac

* Um Mac com macOS High Sierra 10.13 ou superior.

Para criar aplicativos Xamarin para iOS ou macOS, você também precisará de:

* Xcode 10.0 ou posterior. A versão estável mais recente geralmente é recomendada.
* Uma ID da Apple. Se ainda não tiver uma ID da Apple, crie uma nova em https://appleid.apple.com. Será necessário ter uma ID da Apple para instalar e entrar no Xcode.

## <a name="installing-the-preview"></a>Instalando a versão prévia

1. Baixe o instalador da versão prévia da [página da versão prévia do Visual Studio para Mac](https://aka.ms/vs4mac-preview).
2. Depois que o download for concluído, clique no **VisualStudioforMacPreviewInstaller.dmg** para montar o instalador e, em seguida, execute-o clicando duas vezes no logotipo de seta:

    [![Clique na seta grande para iniciar a instalação](media/install-preview-installer-sml.png)](media/install-preview-installer.png#lightbox)

3. Poderá ser apresentado a você um aviso de que o aplicativo está sendo baixado da Internet. Clique em **Abrir**.
4. Aguarde enquanto o instalador verifica seu sistema:

    [![O instalador verifica o sistema em busca de componentes instalados](media/install-preview-checking-sml.png)](media/install-preview-checking.png#lightbox)

5. Um alerta será exibido solicitando que você reconheça os termos de licença e privacidade. Siga os links para lê-los e, em seguida, pressione **Continuar** se você concordar com eles:

    [![Siga os links para a privacidade e termos e, em seguida, continue se você concordar com eles](media/install-preview-privacy-sml.png)](media/install-preview-privacy.png#lightbox)

6. A lista de cargas de trabalho disponíveis é exibida. Selecione aquelas que você deseja usar:

    [![Escolha quais recursos opcionais de carga de trabalho você deseja instalar](media/install-preview-selection-sml.png)](media/install-preview-selection.png#lightbox)

    Se o Visual Studio para Mac 2017 atual for anterior à versão 7.7, será solicitado que você aprove uma atualização para a versão estável mais recente (que é necessária para dar suporte à instalação lado a lado). Pressione **Continuar** para aprovar a atualização:

    ![A atualização da versão estável para 7.7 é necessária](media/install-preview-older-upgrade.png)

7. Após você ter feito suas seleções, pressione o botão **Instalar**.
8. O instalador exibirá o andamento conforme o download acontece e instalará o Visual Studio para Mac e as cargas de trabalho selecionadas. Talvez seja solicitado que você insira sua senha para conceder os privilégios necessários para a instalação.
9. Use o **Visual Studio (Preview)** sempre que quiser testar a versão prévia ou então volte para a versão estável mais recente do Visual Studio para o seu trabalho de produção. Os dois ícones são mostrados aqui:

    ![Diferenças entre os ícones de versão prévia e estável](media/install-preview-icons-sml.png)

Se você tiver problemas de rede durante a instalação em um ambiente corporativo, examine as instruções em [instalação por trás de um firewall ou proxy](https://docs.microsoft.com/visualstudio/mac/installation#install-visual-studio-for-mac-behind-a-firewall-or-proxy-server).

Saiba mais sobre as novidades nas [notas sobre a versão](https://docs.microsoft.com/visualstudio/releasenotes/vs2019-mac-preview-relnotes).

::: zone-end
::: zone pivot="vsmac2017"

## <a name="install-an-update-for-visual-studio-2017-for-mac"></a>Instalar uma atualização para o Visual Studio 2017 para Mac

Antes que uma nova versão do Visual Studio para Mac seja lançada oficialmente, ela está disponível como uma versão prévia. A versão prévia permite que você experimente novos recursos e receba as correções de bug mais recentes antes que eles sejam totalmente incorporados ao produto.

Versões prévias do Visual Studio para Mac são distribuídas como atualizações, e não por meio de um download separado. O Visual Studio para Mac tem três canais de atualização, conforme descrito no artigo sobre [atualização](update.md): Alfa, Beta e Estável.

A maioria das versões prévias estarão disponíveis por meio dos canais **Beta** e **Alpha**, mas sempre consulte as [Notas de versão prévia](/visualstudio/releasenotes/vs2017-mac-preview-relnotes) para obter as informações mais precisas.

Para instalar a versão prévia do Visual Studio para Mac, siga as seguintes etapas:

1. Acesse **Visual Studio > Verificar se há atualizações**.
2. Na caixa de combinação Atualizar canal, selecione **Beta**.
3. Selecione o botão **Alternar canal** para passar para o canal selecionado e iniciar o download de novas atualizações.
4. Selecione o botão **Reiniciar e Instalar Atualizações** para começar a instalar as atualizações.

Para obter mais informações sobre atualizações no Visual Studio para Mac, consulte o artigo sobre [atualização](update.md).

::: zone-end