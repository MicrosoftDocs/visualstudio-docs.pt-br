---
title: Instalar o Visual Studio
titleSuffix: ''
description: Saiba como instalar o Visual Studio, passo a passo.
ms.date: 12/13/2019
ms.custom: seodec18
ms.topic: how-to
f1_keywords:
- vs.about
helpviewer_keywords:
- install Visual Studio
- dev15
- set up Visual Studio
- Visual Studio setup
- Visual Studio installer
author: ornellaalt
ms.author: ornella
manager: jillfra
ms.workload:
- multiple
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.openlocfilehash: 132aaa8da49814c10afe3089e21d391aa2964673
ms.sourcegitcommit: 9e15138a34532b222e80f6b42b1a9de7b2fe0175
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85419153"
---
# <a name="install-visual-studio"></a>Instalar o Visual Studio

::: moniker range="vs-2019"

Bem-vindo ao Visual Studio 2019. Nesta versão, é fácil escolher e instalar apenas os recursos que você precisa. E, devido a seu volume mínimo reduzido, ele é instalado rapidamente e com menos impacto no sistema.

::: moniker-end

::: moniker range="vs-2017"

Bem-vindo a uma nova maneira de instalar o Visual Studio! Nesta versão, facilitamos a seleção e a instalação apenas dos recursos necessários. Também reduzimos os volumes mínimos do Visual Studio para que ele seja instalado mais rapidamente e com menor impacto ao sistema.

::: moniker-end

> [!NOTE]
> Este tópico aplica-se ao Visual Studio no Windows. Para o Visual Studio para Mac, confira [Instalar o Visual Studio para Mac](/visualstudio/mac/installation/).

::: moniker range="vs-2019"

Quer saber mais sobre quais são as outras novidades nesta versão? Consulte nossas [notas de versão](/visualstudio/releases/2019/release-notes/).

::: moniker-end

::: moniker range="vs-2017"

Quer saber mais sobre quais são as outras novidades nesta versão? Consulte nossas [notas de versão](/visualstudio/releasenotes/vs2017-relnotes).

::: moniker-end

Pronto para instalar? Guiaremos você no processo, passo a passo.

## <a name="step-1---make-sure-your-computer-is-ready-for-visual-studio"></a>Etapa 1 - Verificar se o computador está pronto para o Visual Studio

Antes de começar a instalação do Visual Studio:

::: moniker range="vs-2017"

1. Verifique os [requisitos do sistema](/visualstudio/productinfo/vs2017-system-requirements-vs). Esses requisitos ajudam você a saber se o computador dá suporte ao Visual Studio 2017.

1. Aplique as atualizações mais recentes do Windows. Essas atualizações garantem que o computador tenha as atualizações de segurança mais recentes e os componentes de sistema obrigatórios para o Visual Studio.

1. Reinicialize. Isso garante que todas as instalações ou atualizações pendentes não atrapalhem a instalação do Visual Studio.

1. Libere espaço. Remova arquivos e aplicativos desnecessários de %SystemDrive%, por exemplo, executando o aplicativo Limpeza de Disco.

::: moniker-end

::: moniker range="vs-2019"

1. Verifique os [requisitos do sistema](/visualstudio/releases/2019/system-requirements). Esses requisitos ajudam você a saber se o computador dá suporte ao Visual Studio 2019.

1. Aplique as atualizações mais recentes do Windows. Essas atualizações garantem que o computador tenha as atualizações de segurança mais recentes e os componentes de sistema obrigatórios para o Visual Studio.

1. Reinicialize. Isso garante que todas as instalações ou atualizações pendentes não atrapalhem a instalação do Visual Studio.

1. Libere espaço. Remova arquivos e aplicativos desnecessários de %SystemDrive%, por exemplo, executando o aplicativo Limpeza de Disco.

::: moniker-end

::: moniker range="vs-2017"

Para solucionar dúvidas sobre a execução de versões anteriores do Visual Studio lado a lado com o Visual Studio de 2017, consulte [os detalhes de compatibilidade do Visual Studio](/visualstudio/productinfo/vs2017-compatibility-vs#compatibility-with-previous-releases).

::: moniker-end

::: moniker range="vs-2019"

Para solucionar dúvidas sobre a execução de versões anteriores do Visual Studio lado a lado com o Visual Studio 2019, veja a página [Direcionamento e compatibilidade da plataforma Visual Studio 2019](/visualstudio/releases/2019/compatibility/).

::: moniker-end

## <a name="step-2---download-visual-studio"></a>Etapa 2 - Baixar o Visual Studio

Em seguida, baixe o arquivo bootstrapper do Visual Studio.

::: moniker range="vs-2017"

Para obter um bootstrapper para o Visual Studio 2017, consulte a página de download de [versões anteriores do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/) para obter detalhes sobre como fazer isso.

::: moniker-end

::: moniker range="vs-2019"

Para fazer isso, escolha o botão a seguir, escolha a edição desejada do Visual Studio, escolha **Salvar** e, em seguida, escolha **Abrir pasta**.

 > [!div class="button"]
 > [Baixar o Visual Studio](https://visualstudio.microsoft.com/downloads)

::: moniker-end

## <a name="step-3---install-the-visual-studio-installer"></a>Etapa 3 - Instalar o instalador do Visual Studio

Execute o arquivo bootstrapper para instalar o Instalador do Visual Studio. Esse novo instalador leve inclui tudo o que você precisa para instalar e personalizar o Visual Studio.

1. Da sua pasta **Downloads**, clique duas vezes no inicializador que corresponde ou é semelhante a um dos seguintes arquivos:

   * **vs_community.exe** para Visual Studio Community
   * **vs_professional.exe** para Visual Studio Professional
   * **vs_enterprise.exe** para Visual Studio Enterprise

   Se você receber um aviso de Controle de Conta de Usuário, escolha **Sim**.

2. Solicitaremos que você confirme os termos de [licença](https://visualstudio.microsoft.com/license-terms/) da Microsoft e a [política de privacidade](https://privacy.microsoft.com/privacystatement)da Microsoft. Escolha **Continuar**.

   ![Termos de licença e política de privacidade](media/privacy-and-license-terms.png "Termos de licença da Microsoft e política de privacidade")

## <a name="step-4---choose-workloads"></a>Etapa 4 – escolher cargas de trabalho

Após a instalação do instalador, use-o para personalizar sua instalação selecionando os conjuntos de recursos ou cargas de trabalho desejados. Veja como.

 ::: moniker range="vs-2017"

1. Localize a carga de trabalho desejada no **instalador do Visual Studio**.

   ![Visual Studio 2017: instalar uma carga de trabalho](../install/media/vs-installer-installing-workloads.png)

     Por exemplo, escolha a carga de trabalho de “Desenvolvimento de área de trabalho do .NET”. Ela vem com o editor de núcleo padrão, que inclui o suporte à edição de código básico para mais de 20 linguagens, a capacidade de abrir e editar o código de qualquer pasta sem precisar de um projeto e o controle do código-fonte integrado.

1. Depois de escolher as cargas de trabalho desejadas, escolha **Instalar**.

    Em seguida, serão exibidas telas de status que mostram o progresso da instalação do Visual Studio.

 ::: moniker-end

::: moniker range="vs-2019"

1. Localize a carga de trabalho desejada no **instalador do Visual Studio**.

   ![Visual Studio 2019: instalar uma carga de trabalho](../install/media/vs-2019/vs-installer-workloads.png)

     Por exemplo, escolha a carga de trabalho "ASP.NET e desenvolvimento Web". Ela vem com o editor de núcleo padrão, que inclui o suporte à edição de código básico para mais de 20 linguagens, a capacidade de abrir e editar o código de qualquer pasta sem precisar de um projeto e o controle do código-fonte integrado.

1. Depois de escolher as cargas de trabalho desejadas, escolha **Instalar**.

    Em seguida, serão exibidas telas de status que mostram o progresso da instalação do Visual Studio.

 ::: moniker-end

> [!TIP]
> A qualquer momento após a instalação, você pode instalar as cargas de trabalho ou os componentes não instalados inicialmente. Se você tiver o Visual Studio aberto, vá para **ferramentas**  >  **obter ferramentas e recursos...** que abre a instalador do Visual Studio. Outra opção é abrir o **Instalador do Visual Studio** no menu Iniciar. Assim, é possível escolher as cargas de trabalho ou os componentes que você deseja instalar. Em seguida, escolha **Modificar**.

## <a name="step-5---choose-individual-components-optional"></a>Etapa 5 – escolher componentes individuais (opcional)

Se você não quiser usar o recurso de cargas de trabalho para personalizar a instalação do Visual Studio, ou se quiser adicionar mais componentes do que as instalações de uma carga de trabalho, poderá fazer isso instalando ou adicionando componentes individuais da guia **componentes individuais** . escolha o que deseja e siga os prompts.

::: moniker range="vs-2017"

  ![Visual Studio 2017-instalar componentes individuais](media/vs-installer-installing-components.png "Instalar componentes individuais do Visual Studio")

::: moniker-end

::: moniker range="vs-2019"

  ![Visual Studio 2019-instalar componentes individuais](media/vs-2019/vs-installer-individual-components.png "Instalar componentes individuais do Visual Studio")

::: moniker-end

## <a name="step-6---install-language-packs-optional"></a>Etapa 6 - Instalar pacotes de idiomas (opcional)

Por padrão, o programa do instalador tenta encontrar a correspondência do idioma do sistema operacional quando ele é executado pela primeira vez. Para instalar o Visual Studio em um idioma de sua escolha, escolha a guia **Pacotes de idioma** do Instalador do Visual Studio e siga os prompts.

::: moniker range="vs-2017"

  ![Visual Studio 2017-instalar pacotes de idiomas](media/vs-installer-installing-language-packs.png "Instalar pacotes de idiomas do Visual Studio")

::: moniker-end

::: moniker range="vs-2019"

  ![Visual Studio 2019-instalar pacotes de idiomas](media/vs-2019/vs-installer-language-packs.png "Instalar pacotes de idiomas do Visual Studio")

::: moniker-end

### <a name="change-the-installer-language-from-the-command-line"></a>Alterar o idioma de instalação da linha de comando

Outra maneira de alterar o idioma padrão é executar o instalador a partir da linha de comando. Por exemplo, é possível forçar o instalador a ser executado em inglês usando o seguinte comando: `vs_installer.exe --locale en-US`. O instalador memorizará essa configuração quando for executado na próxima vez. O instalador dá suporte aos seguintes tokens de idioma: zh-cn, zh-tw, cs-cz, en-us, es-es, fr-fr, de-de, it-it, ja-jp, ko-kr, pl-pl, pt-br, ru-ru e tr-tr.

## <a name="step-7---select-the-installation-location-optional"></a>Etapa 7 – Selecionar o local de instalação (opcional)

::: moniker range="vs-2017"

**Novidade no 15.7**: agora você pode reduzir o volume de instalação do Visual Studio na unidade do sistema. Você pode optar por mover o cache de download, os componentes compartilhados, os SDKs e as ferramentas para unidades diferentes e manter o Visual Studio na unidade que executá-los com mais rapidez.

  ![Visual Studio 2017-alterar locais de instalação](media/installation-options-by-location.png "Alterar o local de instalação")

::: moniker-end

::: moniker range="vs-2019"

Você pode reduzir o volume de instalação do Visual Studio na unidade do sistema. Você pode optar por mover o cache de download, os componentes compartilhados, os SDKs e as ferramentas para unidades diferentes e manter o Visual Studio na unidade que executá-los com mais rapidez.

  ![Visual Studio 2019 – selecionar locais de instalação](media/vs-2019/vs-installer-installation-locations.png "Selecione o local de instalação")

::: moniker-end

> [!IMPORTANT]
> Você pode selecionar uma unidade diferente apenas quando você instala o Visual Studio pela primeira vez. Se você já tiver instalado e quiser alterar unidades, precisará desinstalar o Visual Studio e, em seguida, reinstalá-lo.

Para obter mais informações, consulte a página [Selecionar locais de instalação](change-installation-locations.md).

## <a name="step-8---start-developing"></a>Etapa 8 – Começar a desenvolver

::: moniker range="vs-2017"

1. Após a conclusão da instalação do Visual Studio, escolha o botão **Iniciar** para ver a introdução ao desenvolvimento com o Visual Studio.

2. Escolha **Arquivo** e, em seguida, **Novo Projeto**.

3. Selecione um tipo de projeto.

   Por exemplo, para [compilar um aplicativo em C++](/cpp/get-started/tutorial-console-cpp), escolha **Instalado**, expanda **Visual C++** e, em seguida, escolha o tipo de projeto C++ que deseja compilar.

   Para [compilar um aplicativo em C#](../get-started/csharp/tutorial-console.md), escolha **Instalado**, expanda **Visual C#** e, em seguida, escolha o tipo de projeto C# que deseja compilar.

::: moniker-end

::: moniker range="vs-2019"

1. Após a conclusão da instalação do Visual Studio, escolha o botão **Iniciar** para ver a introdução ao desenvolvimento com o Visual Studio.

1. Na janela iniciar, escolha **criar um novo projeto**.

1. Na caixa de pesquisa, insira o tipo de aplicativo que deseja criar para ver uma lista de modelos disponíveis. A lista de modelos depende das cargas de trabalho escolhidas durante a instalação. Para ver os diferentes modelos, escolha diferentes cargas de trabalho.

   Você também pode filtrar sua pesquisa para uma linguagem de programação específica usando a lista suspensa **Linguagem de programação**. Você também pode filtrar usando as listas **Plataforma** e **Tipo de projeto**.

1. O Visual Studio abre seu novo projeto e você está pronto para codificar!

::: moniker-end

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Veja também

* [Atualizar o Visual Studio](update-visual-studio.md)
* [Modificar o Visual Studio](modify-visual-studio.md)
* [Desinstalar o Visual Studio](uninstall-visual-studio.md)
* [Criar uma instalação offline do Visual Studio](create-an-offline-installation-of-visual-studio.md)
* [Usar parâmetros de linha de comando para instalar o Visual Studio](use-command-line-parameters-to-install-visual-studio.md)
* [Instalar o Visual Studio para Mac](/visualstudio/mac/installation)
