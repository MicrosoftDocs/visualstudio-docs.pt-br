---
title: Instalar versões do Visual Studio lado a lado
description: Saiba como instalar o Visual Studio em um computador que tenha uma versão anterior ou posterior do Visual Studio já instalada.
ms.custom: SEO-VS-2020
ms.date: 03/29/2021
ms.prod: visual-studio-windows
ms.technology: vs-installation
ms.topic: conceptual
helpviewer_keywords:
- side-by-side installations [Visual Studio]
- Help [Visual Studio], installing
- install multiple versions of Visual Studio
author: ornellaalt
ms.author: ornella
manager: jmartens
ms.openlocfilehash: 0814b6ebfacd5b4cf24d0f451967903b9551808f
ms.sourcegitcommit: 22789927ec8e877b7d2b67a555d6df97d84103e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2021
ms.locfileid: "105981271"
---
# <a name="install-visual-studio-versions-side-by-side"></a>Instalar versões do Visual Studio lado a lado

É possível instalar o Visual Studio em um computador que já tenha uma versão anterior dele instalada.

::: moniker range="vs-2017"

Antes de instalar as versões lado a lado, revise as seguintes condições:

* Se você usar o Visual Studio 2017 para abrir uma solução que foi criada no Visual Studio 2015, você poderá, posteriormente, abrir e modificar a solução novamente na versão anterior desde que você não tenha implementado quaisquer recursos que são específicos do Visual Studio 2017.

* Se você tentar usar o Visual Studio 2017 para abrir uma solução que foi criada no Visual Studio 2015 ou em uma versão anterior, talvez você precise alterar seus projetos e arquivos para que fiquem compatíveis com o Visual Studio 2017. Para obter mais informações, veja a página [Portar, migrar e atualizar projetos do Visual Studio](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017&preserve-view=true).

::: moniker-end

::: moniker range=">= vs-2019"

Antes de instalar as versões lado a lado, revise as seguintes condições:

* Se você usar o Visual Studio 2019 para abrir uma solução que foi criada no Visual Studio 2017, você poderá, posteriormente, abrir e modificar a solução novamente na versão anterior desde que você não tenha implementado quaisquer recursos que são específicos do Visual Studio 2019.

* Se você tentar usar o Visual Studio 2019 para abrir uma solução que foi criada no Visual Studio 2017 ou em uma versão anterior, talvez você precise alterar seus projetos e arquivos para que fiquem compatíveis com o Visual Studio 2019. Para obter mais informações, veja a página [Portar, migrar e atualizar projetos do Visual Studio](../porting/port-migrate-and-upgrade-visual-studio-projects.md).

::: moniker-end

* Se você desinstalar uma versão do Visual Studio em um computador que tem mais de uma versão instalada, as associações de arquivo do Visual Studio serão removidas para todas as versões.

* O Visual Studio não atualiza automaticamente extensões porque nem todas as extensões são compatíveis. Você deverá reinstalar as extensões do [Visual Studio Marketplace](https://marketplace.visualstudio.com/) ou do fornecedor de software.

## <a name="install-minor-visual-studio-versions-side-by-side"></a>Instale as versões secundárias do Visual Studio lado a lado

Ao atualizar de uma versão secundária do Visual Studio para a próxima, o instalador do Visual Studio, por padrão, atualizará sua instalação atual para a versão mais recente nesse canal. Por exemplo, suponha que 16.9.4 acabou de ser lançado. O instalador tentará substituir sua instalação atual do 16.9.3 (ou inferior) por 16.9.4, já que ambas as versões fazem parte do [canal de lançamento do Visual Studio 2019](https://docs.microsoft.com/visualstudio/productinfo/release-rhythm). Substituir a versão mais antiga pela versão mais recente durante a atualização ajuda a garantir que as versões mais antigas do Visual Studio não estejam ocupando espaço no seu computador. No entanto, em alguns casos específicos, pode ser útil instalar diferentes versões secundárias de lançamento do Visual Studio lado a lado. Por exemplo, talvez você queira ter 16.9.3 e 16.9.4 no mesmo computador. 

::: moniker range="vs-2017"

1. Baixe o bootstrapper mais recente para o Visual Studio 2017 versão 15,9 da página [versões anteriores do Visual Studio](https://visualstudio.microsoft.com/vs/older-downloads/) para a versão que você deseja instalar lado a lado com a versão existente do Visual Studio.

::: moniker-end

::: moniker range="vs-2019"

1. Baixe o arquivo bootstrapper do Visual Studio 2019 na [página de downloads do Visual Studio](https://visualstudio.microsoft.com/downloads) ou na página de [versões do Visual Studio 2019](https://docs.microsoft.com/visualstudio/releases/2019/history#installing-an-earlier-release) para a versão secundária que você deseja instalar lado a lado com a versão existente do Visual Studio.

::: moniker-end


2. Abra o prompt de comando no modo de administrador. Para fazer isso, abra o menu Iniciar do Windows, digite "cmd", clique com o botão direito do mouse no resultado da pesquisa do prompt de comando e selecione **Executar como administrador**. No prompt de comando, altere o diretório para a pasta onde o arquivo de bootstrapper do Visual Studio está localizado.

::: moniker range="vs-2017"

3. Execute o comando a seguir, especificando um novo caminho de pasta para o local de instalação e substituindo o nome do arquivo. exe pelo nome de bootstrapper apropriado para a versão do Visual Studio que você está instalando. O nome do arquivo. exe deve corresponder ou ser semelhante a um dos seguintes arquivos:

   * vs_enterprise.exe para Visual Studio Enterprise
   * vs_professional.exe para Visual Studio Professional

::: moniker-end

::: moniker range="vs-2019"

3. Execute o comando a seguir, especificando um novo caminho de pasta para o local de instalação e substituindo o nome do arquivo. exe pelo nome de bootstrapper apropriado para a versão do Visual Studio que você está instalando. O nome do arquivo. exe deve corresponder ou ser semelhante a um dos seguintes arquivos:

   * vs_enterprise.exe para Visual Studio Enterprise
   * vs_professional.exe para Visual Studio Professional
   * vs_community.exe para Visual Studio Community

::: moniker-end 
  
   ```
   vs_Enterprise.exe --installPath "C:\Program Files (x86)\Microsoft Visual Studio\<AddNewPath>"
   ```

4. Siga as caixas de diálogo do instalador para selecionar os componentes necessários para a instalação. Para obter mais informações, consulte [instalar o Visual Studio](install-visual-studio.md#step-4---choose-workloads).

## <a name="net-framework-versions-and-side-by-side-installations"></a>Versões do .NET Framework e instalações lado a lado

Os projetos Visual Basic, Visual C# e Visual F# usam a opção **Estrutura de Destino** no **Designer de Projeto** para especificar qual versão do .NET Framework um projeto usa. Para um projeto do C++, é possível alterar manualmente a estrutura de destino alterando o arquivo .vcxproj. Para obter mais informações, veja a página [Compatibilidade de versão no .NET Framework](/dotnet/framework/migration-guide/version-compatibility).

Ao criar um projeto, você pode especificar a qual versão do .NET Framework o projeto é direcionado na lista **.NET Framework** na caixa de diálogo **Novo Projeto**.

Para informações específicas do idioma, consulte o tópico apropriado na tabela a seguir.

::: moniker range="vs-2017"

| Idioma | Tópico |
|--------------|-----------|
| Visual Basic | [Página de Aplicativo, Designer de Projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md?view=vs-2017&preserve-view=true) |
| Visual C# | [Página Aplicativo, Designer de Projeto (C#)](../ide/reference/application-page-project-designer-csharp.md?view=vs-2017&preserve-view=true) |
| Visual F# | [Desenvolver com o Visual F# no Visual Studio](../ide/fsharp-visual-studio.md?view=vs-2017&preserve-view=true) |
|C++ | [Como: Modificar a estrutura de destino e o conjunto de ferramentas da plataforma](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/) |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar o Visual Studio](install-visual-studio.md?view=vs-2017&preserve-view=true)
* [Portar, migrar e atualizar projetos do Visual Studio](../porting/port-migrate-and-upgrade-visual-studio-projects.md?view=vs-2017&preserve-view=true)
* [Como compilar assemblies lado a lado e aplicativos isolados do C/C++](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end

::: moniker range=">= vs-2019"

| Idioma | Tópico |
|--------------|-----------|
| Visual Basic | [Página de Aplicativo, Designer de Projeto (Visual Basic)](../ide/reference/application-page-project-designer-visual-basic.md) |
| Visual C# | [Página Aplicativo, Designer de Projeto (C#)](../ide/reference/application-page-project-designer-csharp.md) |
| Visual F# | [Desenvolver com o Visual F# no Visual Studio](../ide/fsharp-visual-studio.md) |
| C++ | [Como: Modificar a estrutura de destino e o conjunto de ferramentas da plataforma](/cpp/build/how-to-modify-the-target-framework-and-platform-toolset/) |

[!INCLUDE[install_get_support_md](includes/install_get_support_md.md)]

## <a name="see-also"></a>Confira também

* [Instalar o Visual Studio](install-visual-studio.md)
* [Portar, migrar e atualizar projetos do Visual Studio](../porting/port-migrate-and-upgrade-visual-studio-projects.md)
* [Como compilar assemblies lado a lado e aplicativos isolados do C/C++](/cpp/build/building-c-cpp-isolated-applications-and-side-by-side-assemblies/)

::: moniker-end
