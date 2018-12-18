---
title: Instalar o Dotfuscator Community Edition (CE)
ms.date: 06/22/2017
ms.devlang: dotnet
ms.prod: visual-studio-dev15
ms.technology: vs-ide-general
ms.topic: conceptual
keywords: Dotfuscator, Dotfuscator CE, PreEmptive, PreEmptive Solutions, PreEmptive Protection, proteção, community edition, ofuscação, .NET, gratuito, Visual Studio 2017, instalar
helpviewer_keywords:
- PreEmptive Protection Dotfuscator
- Dotfuscator Community Edition
- Dotfuscator CE
- Dotfuscator
- obfuscation
- protection
- Dotfuscator installer
- Dotfuscator setup
- install Dotfuscator
- installing Dotfuscator
- set up Dotfuscator
description: Saiba como instalar o Dotfuscator Community Edition gratuito incluído no Visual Studio 2017.
ms.assetid: f2146651-e24a-4e24-ade8-8ddee8ff4e43
author: Joe-Sewell-PreEmptive
ms.author: gewarren
manager: douge
ms.openlocfilehash: d513588a7d00e874b38306150f896157906e2733
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49880358"
---
# <a name="install-dotfuscator-community-edition-ce"></a>Instalar o Dotfuscator Community Edition (CE)

O Visual Studio 2017 introduz uma nova experiência de instalação de baixo impacto.
Como resultado, o Dotfuscator Community Edition (Dotfuscator CE) não está instalado por padrão.
No entanto, é fácil de instalar o Dotfuscator CE mesmo que você já tenha instalado o Visual Studio.

> [!NOTE]
> Além das versões do Dotfuscator CE que acompanham as versões do Visual Studio, a PreEmptive Solutions periodicamente fornece versões atualizadas em seu site.
> Se você quiser baixar a **versão mais recente** diretamente, em vez de instalá-la do Visual Studio, **[clique aqui para ir para a página de Downloads do Dotfuscator][download]**.

## <a name="within-visual-studio"></a>No Visual Studio

Você pode instalar o Dotfuscator CE no IDE do Visual Studio:

1. No barra de pesquisa **Início Rápido** (Ctrl + Q), digite `dotfuscator`. <br/> <br/> ![Início Rápido](media/install_from_vs_12.png) <br/> <br/>
2. Nos resultados do Início Rápido mostrado, no cabeçalho *Instalar*, selecione **PreEmptive Protection – Dotfuscator (Componente Individual)**.
   * Se, em vez disso, você visualizar, no cabeçalho *Menus*, **Ferramentas – PreEmptive Protection – Dotfuscator**, o Dotfuscator CE já estará instalado. Para obter detalhes de uso, consulte [a página de Introdução do Guia completo do usuário do CE Dotfuscator][get-started].
3. Uma janela do Instalador do Visual Studio será inicializada, pré-configurada com instalar Dotfuscator CE.
   * Você pode ser solicitado a fornecer credenciais de administrador para continuar.
4. Feche todas as instâncias do IDE do Visual Studio. <br/> <br/> ![Clicar em Instalar](media/install_from_vs_345.png) <br/> <br/>
5. Na janela do Instalador do Visual Studio, clique em *Instalar*.

Quando a instalação estiver concluída, você poderá começar a usar Dotfuscator CE. Para obter detalhes, consulte [a página de Introdução do Guia do usuário completo do CE Dotfuscator][get-started].

## <a name="during-visual-studio-installation"></a>Durante a instalação do Visual Studio

Se você ainda não tiver instalado o Visual Studio 2017, poderá obter o instalador do [site do Visual Studio][2017-install].
Quando executado, ele exibirá as opções de instalação para a edição selecionada do Visual Studio.

![Opções de instalação](media/install_ui.png)

Então você pode instalar o Dotfuscator CE como um componente individual do Visual Studio 2017:

1. Selecione a guia **Componentes individuais**.
2. Em *Ferramentas de código*, marque o item *PreEmptive Protection – Dotfuscator*.<br/> <br/> ![Componentes individuais](media/install_individually_12.png) <br/> <br/>
3. O painel *Resumo* exibe *PreEmptive Protection – Dotfuscator* na seção *Componentes Individuais*. <br/> <br/> ![Painel de resumo](media/install_individually_3.png) <br/> <br/>
4. Defina quaisquer outras configurações de instalação conforme apropriado para seu ambiente.
5. Quando estiver pronto para instalar o Visual Studio, clique no botão *Instalar*.

Quando a instalação estiver concluída, você poderá começar a usar Dotfuscator CE. Para obter detalhes, consulte [a página de Introdução do Guia do usuário completo do CE Dotfuscator][get-started].

## <a name="see-also"></a>Consulte também

[This topic in the full Dotfuscator CE User Guide]: https://www.preemptive.com/dotfuscator/ce/docs/help/

<!-- Copyright © 2017 PreEmptive Solutions, LLC -->

[2017-install]:  https://visualstudio.microsoft.com/downloads/#vs-2017
[get-started]:  https://www.preemptive.com/dotfuscator/ce/docs/help/gui_getstarted.html

[download]:  https://www.preemptive.com/products/dotfuscator/downloads

[full]:  https://www.preemptive.com/dotfuscator/ce/docs/help/intro_install.html