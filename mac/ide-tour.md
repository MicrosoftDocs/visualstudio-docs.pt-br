---
title: Tour do Visual Studio para Mac
description: O Visual Studio para Mac fornece um ambiente de desenvolvimento integrado para compilar aplicativos .NET no macOS, incluindo sites ASP.NET Core e projetos Xamarin para iOS, Android, Mac e Xamarin.Forms.
zone_pivot_groups: mac-ide-version
author: conceptdev
ms.author: crdun
ms.date: 11/03/2018
ms.assetid: 7DC64A52-AA41-4F3A-A8A1-8A20BCD81CC7
ms.openlocfilehash: e1787f6d396121263d91633a4ee6d4dd8ed2c35f
ms.sourcegitcommit: ae46be4a2b2b63da7e7049e9ed67cd80897c8102
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2018
ms.locfileid: "52895789"
---
# <a name="visual-studio-for-mac-tour"></a>Tour do Visual Studio para Mac

O Visual Studio para Mac evolui o IDE voltado para plataformas móveis do Xamarin, Xamarin Studio, em um ambiente de desenvolvimento primeiramente móvel e na nuvem no Mac. Essa ferramenta para desenvolvedores permite que você use a potência do .NET para criar aplicativos para todas as plataformas exigidas pelos usuários.

A UX (experiência do usuário) do Visual Studio para Mac é semelhante de seu equivalente do Windows, porém com uma aparência de macOS nativa. Criar, abrir e desenvolver um aplicativo será uma experiência familiar para qualquer pessoa que já tenha usado o Visual Studio no Windows. Além disso, o Visual Studio para Mac emprega muitas das ferramentas avançadas que fazem do seu equivalente no Windows um IDE tão avançado. A Roslyn Compiler Platform é usada para refatoração e IntelliSense. Seu sistema de projeto e mecanismo de build usam o MSBuild e seu editor de código-fonte dá suporte a pacotes TextMate. Ele usa os mesmos mecanismos de depuração para aplicativos Xamarin e .NET Core, e os mesmos designers para Xamarin.iOS e Xamarin.Android.

Este artigo explora várias seções do Visual Studio para Mac, mostrando alguns dos recursos que o tornam uma ferramenta avançada para criar aplicativos de plataforma cruzada.

## <a name="ide-tour"></a>Tour do IDE

O Visual Studio para Mac está organizado em várias seções para gerenciar configurações e arquivos de aplicativo, criar código do aplicativo e depuração.

::: zone pivot="vsmac2019"

## <a name="visual-studio-for-mac-2019-start-window"></a>Janela de Início do Visual Studio para Mac 2019

> [!TIP]
> A versão prévia do Visual Studio 2019 para Mac agora está [disponível para download](install-preview.md) e teste.

Quando você iniciar a versão prévia do Visual Studio para Mac 2019, novos usuários verão uma janela de entrada. Entre com sua conta Microsoft para ativar uma licença paga (se tiver uma) ou um link para assinaturas do Azure. Você pode pressionar **Ignorar** e entrar mais tarde pelo item de menu **Visual Studio > Entrar**:

![Entrar com sua conta Microsoft](media/ide-tour-2019-start-signin.png)

Usuários conectados verão a nova _janela de início_, que mostra uma lista de projetos recentes e botões para abrir um projeto existente ou criar um novo:

![Escolher entre projetos recentes ou criar algo novo](media/ide-tour-2019-start-projects.png)

::: zone-end
::: zone pivot="vsmac2017"

## <a name="welcome-screen-in-visual-studio-for-mac-2017"></a>Tela de boas-vindas no Visual Studio para Mac 2017

Quando iniciado, o Visual Studio para Mac exibe uma *Tela de boas-vindas*:

![Tela de boas-vindas](media/ide-tour-image1.png)

Esta Tela de boas-vindas contém as seguintes seções:

- **Barra de ferramentas** – Fornece acesso rápido à barra de pesquisa. Quando uma solução é carregada, a barra de ferramentas é usada para definir as configurações de aplicativo, para depuração e para a exibição de erros.
- **Introdução** – Fornece acesso rápido aos tópicos úteis para apresentar os desenvolvedores ao Visual Studio para Mac.
- **Soluções Recentes** – Fornece acesso rápido a soluções recém-abertas, bem como botões convenientes para abrir ou criar projetos.
- **Notícias do Desenvolvedor** – um feed de notícias que mantém você atualizado sobre as informações mais recentes do desenvolvedor Microsoft.

::: zone-end

## <a name="solutions-and-projects"></a>Soluções e Projetos

A imagem abaixo mostra o Visual Studio para Mac com um aplicativo carregado:

![Visual Studio para Mac com um aplicativo carregado](media/ide-tour-image17.png)

As seções a seguir fornecem uma visão geral das principais áreas no Visual Studio para Mac.

## <a name="solution-pad"></a>Painel de Soluções

O Painel de Soluções organiza os projetos em uma solução:

![Projetos organizados no Painel de Soluções](media/ide-tour-image18.png)

É aqui que os arquivos para o código-fonte, recursos, interface do usuário e dependências são organizados em Projetos específicos da plataforma.

Para saber mais sobre como usar os Projetos e Soluções no Visual Studio para Mac, veja o artigo [Projetos e Soluções](projects-and-solutions.md).

## <a name="assembly-references"></a>Referências de Assembly

As referências de assembly para cada projeto estão disponíveis na pasta Referências:

![Pasta Referências no painel de soluções](media/ide-tour-image19.png)

As referências adicionais são adicionadas usando a caixa de diálogo **Editar Referências**, que é exibida clicando duas vezes na pasta Referências ou selecionando **Editar Referências** em suas ações de menu de contexto:

![Caixa de diálogo Editar Referências](media/ide-tour-image20.png)

Para saber mais sobre como usar Referências no Visual Studio para Mac, veja o artigo [Gerenciando referências em um projeto](managing-references-in-a-project.md).

## <a name="dependencies--packages"></a>Dependências / Pacotes

Todas as dependências externas usadas em seu aplicativo são armazenadas nas pastas Dependências ou Pacotes, dependendo se você está em um projeto .Net Core ou Xamarin.iOS/Xamarin.Android. Geralmente, eles são fornecidos na forma de um NuGet.

NuGet é o gerenciador de pacote mais popular para desenvolvimento .NET. Com a compatibilidade do NuGet no Visual Studio, você pode facilmente pesquisar e adicionar pacotes ao seu projeto para o aplicativo.

Para adicionar uma dependência ao seu aplicativo, clique com botão direito do mouse sobre a pasta Dependências / Pacotes e selecione **Adicionar Pacotes**:

![Adicionar um pacote NuGet](media/ide-tour-image21.png)

As informações sobre como usar um pacote do NuGet em um aplicativo podem ser encontradas no artigo [Incluindo um projeto NuGet em seu projeto](nuget-walkthrough.md).

## <a name="refactoring"></a>Refatoração

O Visual Studio para Mac fornece duas maneiras úteis de refatorar o código: ações de contexto e análise de código-fonte. Leia mais sobre elas no artigo [Refatoração](refactoring.md).

## <a name="debugging"></a>Depuração

O Visual Studio para Mac tem um depurador nativo para dar suporte à depuração de aplicativos Xamarin.iOS, Xamarin.Mac e Xamarin.Android. O Visual Studio para Mac usa o Mono Soft Debugger, que foi implementado no tempo de execução Mono, permitindo que o IDE depure código gerenciado em todas as plataformas. Para saber mais adicionais sobre a depuração, visite o artigo [Depuração](debugging.md).

O depurador contém visualizadores avançados para tipos especiais, como cadeias de caracteres, cores e URLs, bem como tamanhos, coordenadas e curvas de bézier.

Para saber mais sobre visualizações de dados do depurador, visite o artigo [Visualizações de dados](data-visualizations.md).

## <a name="version-control"></a>Controle de versão

O Visual Studio para Mac integra-se aos sistemas de controle do código-fonte Git e Subversion. Projetos com controle do código-fonte são marcados com o branch listado ao lado do nome da Solução:

![Nome do branch para indicar o projeto com controle do código-fonte](media/ide-tour-image22.png)

Os arquivos com alterações não confirmadas têm uma anotação em seus ícones no Painel de Soluções, como mostrado na imagem abaixo:

![Arquivos não confirmados no painel de soluções](media/ide-tour-image23.png)

Para saber mais sobre como usar o controle de versão no Visual Studio, veja o artigo [Controle de Versão](version-control.md).

## <a name="see-also"></a>Consulte também

- [IDE do Visual Studio (no Windows)](/visualstudio/ide/visual-studio-ide)