---
title: Instalar versões do Visual Studio lado a lado
description: Saiba como instalar o Visual Studio em um computador que tenha uma versão anterior ou posterior Visual Studio já instalada.
ms.custom: SEO-VS-2020
ms.date: 03/29/2021
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: conceptual
helpviewer_keywords:
- side-by-side installations [Visual Studio]
- Help [Visual Studio], installing
- install multiple versions of Visual Studio
author: j-martens
ms.author: jmartens
manager: jmartens
ms.openlocfilehash: c8d1da5f8cb5c237fe02a41197825d5086fc6471
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112307015"
---
# <a name="install-visual-studio-versions-side-by-side"></a>Instalar versões do Visual Studio lado a lado

É possível instalar o Visual Studio em um computador que já tenha uma versão anterior dele instalada.

::: moniker range="vs-2017"

Antes de instalar as versões lado a lado, revise as seguintes condições:

* Se você usar o Visual Studio 2017 para abrir uma solução que foi criada no Visual Studio 2015, você poderá, posteriormente, abrir e modificar a solução novamente na versão anterior desde que você não tenha implementado quaisquer recursos que são específicos do Visual Studio 2017.

* Se você tentar usar o Visual Studio 2017 para abrir uma solução que foi criada no Visual Studio 2015 ou em uma versão anterior, talvez você precise alterar seus projetos e arquivos para que fiquem compatíveis com o Visual Studio 2017. Para obter mais informações, veja a página [Portar, migrar e atualizar projetos do Visual Studio](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017&preserve-view=true).

::: moniker-end

::: moniker range="vs-2019"

Antes de instalar as versões lado a lado, revise as seguintes condições:

* Se você usar o Visual Studio 2019 para abrir uma solução que foi criada no Visual Studio 2017, você poderá, posteriormente, abrir e modificar a solução novamente na versão anterior desde que você não tenha implementado quaisquer recursos que são específicos do Visual Studio 2019.

* Se você tentar usar o Visual Studio 2019 para abrir uma solução que foi criada no Visual Studio 2017 ou em uma versão anterior, talvez você precise alterar seus projetos e arquivos para que fiquem compatíveis com o Visual Studio 2019. Para obter mais informações, veja a página [Portar, migrar e atualizar projetos do Visual Studio](../porting/port-migrate-and-upgrade-visual-studio-projects.md).

::: moniker-end

::: moniker range=">=vs-2022"

Antes de instalar as versões lado a lado, revise as seguintes condições:

* Se você usar o Visual Studio 2022 para abrir uma solução criada no Visual Studio 2017 ou no Visual Studio 2019, poderá abrir e modificar a solução mais tarde na versão anterior, desde que não tenha implementado recursos específicos do Visual Studio 2022.

* Se você tentar usar o Visual Studio 2022 para abrir uma solução que foi criada no Visual Studio 2019 ou em uma versão anterior, talvez seja necessário modificar seus projetos e arquivos para serem compatíveis com o Visual Studio 2022. Para obter mais informações, veja a página [Portar, migrar e atualizar projetos do Visual Studio](../porting/port-migrate-and-upgrade-visual-studio-projects.md).

::: moniker-end

* Se você desinstalar uma versão do Visual Studio em um computador que tem mais de uma versão instalada, as associações de arquivo do Visual Studio serão removidas para todas as versões.

* O Visual Studio não atualiza automaticamente extensões porque nem todas as extensões são compatíveis. Você deverá reinstalar as extensões do [Visual Studio Marketplace](https://marketplace.visualstudio.com/) ou do fornecedor de software.

## <a name="install-minor-visual-studio-versions-side-by-side"></a>Instalar versões Visual Studio secundárias lado a lado

Ao atualizar de uma versão secundária do Visual Studio para a próxima, o instalador do Visual Studio atualizará, por padrão, sua instalação atual para a versão mais recente nesse canal. Por exemplo, suponha que 16.9.4 foi lançado recentemente. O instalador tentará substituir a instalação atual do 16.9.3 (ou inferior) pela 16.9.4, pois ambas as versões fazem parte do canal de lançamento [do Visual Studio 2019.](/visualstudio/productinfo/release-rhythm) Substituir a versão mais antiga pela versão mais recente durante a atualização ajuda a garantir que as versões mais antigas do Visual Studio não estão ocupando espaço em seu computador. No entanto, em alguns casos específicos, pode ser útil instalar diferentes versões secundárias do Visual Studio lado a lado. Por exemplo, talvez você queira ter 16.9.3 e 16.9.4 no mesmo computador.

::: moniker range="vs-2017"

1. Baixe o bootstrapper mais recente do Visual Studio 2017 versão 15.9 da página de versões anteriores do Visual Studio para a versão que você gostaria de instalar lado a lado com sua versão existente do [Visual Studio.](https://visualstudio.microsoft.com/vs/older-downloads/)

1. Abra o prompt de comando no modo de administrador. Para fazer isso, abra o windows menu Iniciar, digite "cmd", clique com o botão direito do mouse no resultado da pesquisa do Prompt de Comando e selecione **Executar como administrador.** No prompt de comando, altere o diretório para a pasta em que o arquivo Visual Studio bootstrapper está localizado.

1. Execute o comando a seguir, especificando um novo caminho de pasta para o local de instalação e substituindo o nome do arquivo .exe pelo nome do bootstrapper apropriado para a versão do Visual Studio que você está instalando. O .exe arquivo deve corresponder ou ser semelhante a um dos seguintes arquivos:

   * vs_enterprise.exe para Visual Studio Enterprise
   * vs_professional.exe para Visual Studio Professional

1. Siga as caixas de diálogo do instalador para selecionar os componentes necessários para sua instalação. Para obter mais informações, consulte [Instalar Visual Studio](install-visual-studio.md#step-4---choose-workloads).

::: moniker-end

::: moniker range="vs-2019"

1. Baixe o arquivo de bootstrapper do Visual Studio 2019 da página [de downloads](https://visualstudio.microsoft.com/downloads) do Visual Studio ou da página [Versões do Visual Studio 2019](/visualstudio/releases/2019/history#installing-an-earlier-release) para a versão secundária que você gostaria de instalar lado a lado com sua versão existente do Visual Studio.

1. Abra o prompt de comando no modo de administrador. Para fazer isso, abra o windows menu Iniciar, digite "cmd", clique com o botão direito do mouse no resultado da pesquisa do Prompt de Comando e selecione **Executar como administrador.** No prompt de comando, altere o diretório para a pasta em que o arquivo Visual Studio bootstrapper está localizado.

1. Execute o comando a seguir, especificando um novo caminho de pasta para o local de instalação e substituindo o nome do arquivo .exe pelo nome do bootstrapper apropriado para a versão do Visual Studio que você está instalando. O .exe arquivo deve corresponder ou ser semelhante a um dos seguintes arquivos:

   * vs_enterprise.exe para Visual Studio Enterprise
   * vs_professional.exe para Visual Studio Professional
   * vs_community.exe para Visual Studio Community

   ```shell
   vs_Enterprise.exe --installPath "C:\Program Files (x86)\Microsoft Visual Studio\<AddNewPath>"
   ```

1. Siga as caixas de diálogo do instalador para selecionar os componentes necessários para sua instalação. Para obter mais informações, consulte [Instalar Visual Studio](install-visual-studio.md#step-4---choose-workloads).

::: moniker-end

::: moniker range=">=vs-2022"

1. Baixe o arquivo de bootstrapper do Visual Studio 2022 da página [de downloads](https://visualstudio.microsoft.com/downloads) do Visual Studio ou da página [Versões do Visual Studio 2022](/visualstudio/releases/2022/history) para a versão secundária que você gostaria de instalar lado a lado com sua versão existente do Visual Studio.

1. Abra o prompt de comando no modo de administrador. Para fazer isso, abra o windows menu Iniciar, digite "cmd", clique com o botão direito do mouse no resultado da pesquisa do Prompt de Comando e selecione **Executar como administrador.** No prompt de comando, altere o diretório para a pasta em que o arquivo Visual Studio bootstrapper está localizado.

1. Execute o comando a seguir, especificando um novo caminho de pasta para o local de instalação e substituindo o nome do arquivo .exe pelo nome do bootstrapper apropriado para a versão do Visual Studio que você está instalando. O .exe arquivo deve corresponder ou ser semelhante a um dos seguintes arquivos:

   * vs_enterprise.exe para Visual Studio Enterprise
   * vs_professional.exe para Visual Studio Professional
   * vs_community.exe para Visual Studio Community

   ```shell
   vs_Enterprise.exe --installPath "C:\Program Files\Microsoft Visual Studio\<AddNewPath>"
   ```

1. Siga as caixas de diálogo do instalador para selecionar os componentes necessários para sua instalação. Para obter mais informações, consulte [Instalar Visual Studio](install-visual-studio.md#step-4---choose-workloads).
   
::: moniker-end

## <a name="net-framework-versions-and-side-by-side-installations"></a>Versões do .NET Framework e instalações lado a lado

Os projetos Visual Basic, Visual C# e Visual F# usam a opção **Estrutura de Destino** no **Designer de Projeto** para especificar qual versão do .NET Framework um projeto usa. Para um projeto do C++, é possível alterar manualmente a estrutura de destino alterando o arquivo .vcxproj. Para obter mais informações, veja a página [Compatibilidade de versão no .NET Framework](/dotnet/framework/migration-guide/version-compatibility).

Ao criar um projeto, você pode especificar a qual versão do .NET Framework o projeto é direcionado na lista **.NET Framework** na caixa de diálogo **Novo Projeto**.

Para informações específicas do idioma, consulte o tópico apropriado na tabela a seguir.

::: moniker range="vs-2017"

| Idioma     | Tópico                                                                                                                                                   |
|--------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|
| Visual Basic | [Página de Aplicativo, Designer de Projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md?view=vs-2017&preserve-view=true) |
| Visual C#    | [Página Aplicativo, Designer de Projeto (C#)](../ide/reference/application-page-project-designer-csharp.md?view=vs-2017&preserve-view=true)                 |
| Visual F#    | [Desenvolver com o Visual F# no Visual Studio](../ide/fsharp-visual-studio.md?view=vs-2017&preserve-view=true)                                               |
| C++          | [Como: Modificar a estrutura de destino e o conjunto de ferramentas da plataforma](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/)                         |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar o Visual Studio](install-visual-studio.md?view=vs-2017&preserve-view=true)
* [Portar, migrar e atualizar Visual Studio projetos](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017&preserve-view=true)
* [Como compilar assemblies lado a lado e aplicativos isolados do C/C++](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end

::: moniker range=">= vs-2019"

| Idioma     | Tópico                                                                                                                           |
|--------------|---------------------------------------------------------------------------------------------------------------------------------|
| Visual Basic | [Página de Aplicativo, Designer de Projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md)         |
| Visual C#    | [Página Aplicativo, Designer de Projeto (C#)](../ide/reference/application-page-project-designer-csharp.md)                         |
| Visual F#    | [Desenvolver com o Visual F# no Visual Studio](../ide/fsharp-visual-studio.md)                                                       |
| C++          | [Como: Modificar a estrutura de destino e o conjunto de ferramentas da plataforma](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/) |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Portar, migrar e atualizar Visual Studio projetos](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
* [Como compilar assemblies lado a lado e aplicativos isolados do C/C++](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end
