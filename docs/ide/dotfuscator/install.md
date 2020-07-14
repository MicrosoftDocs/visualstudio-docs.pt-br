---
title: Instalar o Dotfuscator Community
ms.date: 03/28/2019
ms.devlang: dotnet
ms.topic: how-to
keywords: Dotfuscator, Dotfuscator Community, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, proteção, community edition, ofuscação, .NET, gratuito, Visual Studio 2017, Visual Studio 2019, Visual Studio, instalar
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator Community
- Dotfuscator
- obfuscation
- protection
- Dotfuscator installer
- Dotfuscator setup
- install Dotfuscator
- installing Dotfuscator
- set up Dotfuscator
description: Saiba como instalar a cópia gratuita do Dotfuscator Community incluída no Visual Studio.
ms.assetid: f2146651-e24a-4e24-ade8-8ddee8ff4e43
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: befa47e5718d3d2f5d492c49e173b22fc63310e0
ms.sourcegitcommit: f27084e64c79e6428746a20dda92795df996fb31
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85769673"
---
# <a name="install-dotfuscator-community"></a>Instalar o Dotfuscator Community

O Dotfuscator Community é um componente opcional do Visual Studio.
Estas instruções explicam como instalá-lo.

> [!NOTE]
> Além das versões do Dotfuscator Community que acompanham as versões do Visual Studio, a PreEmptive Solutions periodicamente fornece versões atualizadas em seu site.
> Se você quiser baixar a **versão mais recente** diretamente, em vez de instalá-la do Visual Studio, **[clique aqui para ir para a página de Downloads do Dotfuscator][download]**.

## <a name="within-visual-studio"></a>No Visual Studio

::: moniker range="vs-2019"

Você pode instalar o Dotfuscator Community do IDE do Visual Studio:

1. Na **Caixa de pesquisa** (Ctrl+Q), digite `dotfuscator`. <br/> <br/> ![Caixa de pesquisa](media/install_in_vs19_12.png) <br/> <br/>

2. Nos resultados mostrados, no cabeçalho *Componentes*, selecione **Instalar PreEmptive Protection – Dotfuscator**.
   * Se, em vez disso, no cabeçalho *Menus*, você observar o item **Ferramentas – PreEmptive Protection – Dotfuscator**, o Dotfuscator Community já estará instalado. Selecione essa opção para [começar][get-started].

3. Uma janela do Instalador do Visual Studio será inicializada, pré-configurada para instalar o Dotfuscator Community.
   > [!NOTE]
   > Você pode ser solicitado a fornecer credenciais de administrador para continuar.

4. Na janela do Instalador do Visual Studio, clique em *Instalar*. <br/> <br/> ![Clicar em Instalar](media/install_in_vs19_34.png) <br/> <br/>

::: moniker-end

::: moniker range="vs-2017"

Você pode instalar o Dotfuscator Community do IDE do Visual Studio:

1. No barra de pesquisa **Início Rápido** (Ctrl + Q), digite `dotfuscator`. <br/> <br/> ![Início Rápido](media/install_from_vs_12.png) <br/> <br/>

2. Nos resultados do Início Rápido mostrado, no cabeçalho *Instalar*, selecione **PreEmptive Protection – Dotfuscator (Componente Individual)**.
   * Se, em vez disso, você vir, no título *menus* , **ferramentas-Preemptive Protection-Dotfuscator**, então, o Dotfuscator CE já está instalado. Selecione essa opção para [começar][get-started].

3. Uma janela do Instalador do Visual Studio será inicializada, pré-configurada para instalar o Dotfuscator Community.
   > [!NOTE]
   > Você pode ser solicitado a fornecer credenciais de administrador para continuar.

4. Na janela do Instalador do Visual Studio, clique em *Instalar*. <br/> <br/> ![Clicar em Instalar](media/install_from_vs_345.png) <br/> <br/>

::: moniker-end

Quando a instalação for concluída, você poderá [começar a usar a Comunidade do Dotfuscator][get-started].

## <a name="during-visual-studio-installation"></a>Durante a instalação do Visual Studio

Se você ainda não instalou o Visual Studio, pode obter o instalador no [site do Visual Studio][vs-install].
Quando executado, ele exibirá as opções de instalação para a edição selecionada do Visual Studio.

::: moniker range="vs-2019"

![Opções de instalação](media/install_ui.png)

::: moniker-end

::: moniker range="vs-2017"

![Opções de instalação](media/install_ui_17.png)

::: moniker-end

Você poderá, então, instalar o Dotfuscator Community como um componente individual do Visual Studio:

1. Selecione a guia **Componentes individuais**.
2. Em *Ferramentas de código*, marque o item *PreEmptive Protection – Dotfuscator*.<br/> <br/> ![Componentes individuais](media/install_individually_12.png) <br/> <br/>
3. O painel *Resumo* exibe *PreEmptive Protection – Dotfuscator* na seção *Componentes Individuais*. <br/> <br/> ![Painel de resumo](media/install_individually_3.png) <br/> <br/>
4. Defina quaisquer outras configurações de instalação conforme apropriado para seu ambiente.
5. Quando estiver pronto para instalar o Visual Studio, clique no botão *Instalar*.

Quando a instalação estiver concluída, você poderá começar a usar Dotfuscator Community. Para obter detalhes, confira [a página de Introdução do Guia completo do usuário do Dotfuscator Community][get-started].

## <a name="see-also"></a>Confira também

[Este tópico no Guia completo do usuário do Dotfuscator Community](https://www.preemptive.com/dotfuscator/ce/docs/help/)

<!-- Copyright © 2019 PreEmptive Solutions, LLC -->

[vs-install]:  https://visualstudio.microsoft.com/downloads/
[get-started]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_getstarted.html

[download]:  https://www.preemptive.com/products/dotfuscator/downloads

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_install.html
