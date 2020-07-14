---
title: Novidades no Visual Studio 2019
titleSuffix: ''
description: Saiba mais sobre os novos recursos do Visual Studio 2019.
ms.date: 05/20/2020
helpviewer_keywords:
- Visual Studio, what's new
- what's new [Visual Studio]
ms.assetid: 00bec66b-bcee-46f5-91d9-f73a2b469744
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: 6b5058e0f1fabbf834a1adfb20d4f3a9a11094f5
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/23/2020
ms.locfileid: "85283587"
---
# <a name="whats-new-in-visual-studio-2019"></a>Novidades no Visual Studio 2019

**Atualizado para a [versão 16,6](/visualstudio/releases/2019/release-notes/)**

>[!div class="button"]
>[Baixar o Visual Studio 2019](https://visualstudio.microsoft.com/downloads)

O Visual Studio está mudando constantemente para atender às demandas dos desenvolvedores. No vídeo a seguir da biblioteca do **[Microsoft Build](https://mybuild.microsoft.com/)** , junte-se a nós para obter um tour por alguns dos [recursos mais recentes](/visualstudio/releases/2019/release-notes/) [e uma espiada no](/visualstudio/releases/2019/release-notes-preview/) que é fornecido: <br><br>*Tamanho do vídeo: 44,58 minutos*

> [!VIDEO https://channel9.msdn.com/Events/Build/2020/BOD111/player]

O Visual Studio 2019 fornece os melhores serviços e ferramentas do mercado para desenvolvedores, aplicativos e plataformas. Se você estiver usando o Visual Studio pela primeira vez ou estiver usando-o por anos, há muito a ser gostado em nossa versão mais recente!

Aqui está uma recapitulação de alto nível do que há de novo, tudo:

* **[Desenvolver](#develop)**: Mantenha-se focado e produtivo com desempenho aprimorado, limpeza instantânea de código e melhores resultados da pesquisa.
* **[Colaborar](#collaborate)**: Aproveite a colaboração natural por meio de um fluxo de trabalho do git, edição e depuração em tempo real e análises de código diretamente no Visual Studio.
* **[Depurar](#debug)**: realçar e navegar para valores específicos, otimizar o uso da memória e obter instantâneos automáticos da execução do seu aplicativo.

Para obter uma lista completa de todas as novidades incluídas nesta versão, confira as [notas de versão](/visualstudio/releases/2019/release-notes/).

## <a name="develop"></a>Desenvolver

Veja o vídeo a seguir para saber mais sobre como economizar tempo com novos recursos. <br><br>*Tamanho do vídeo: 3, 0 minutos*

> [!VIDEO https://www.youtube.com/embed/n5sJ4EewKGk]

### <a name="improved-search"></a>Pesquisa aprimorada

Anteriormente conhecida como Início Rápido, nossa nova experiência de pesquisa é mais rápida e eficaz. Agora, os resultados da pesquisa são exibidos dinamicamente conforme você digita. Além disso, os resultados da pesquisa podem incluir atalhos de teclado para comandos, de modo que você possa memorizá-los facilmente para uso futuro.

   ![Animação da nova experiência de pesquisa do Visual Studio 2019](media/vs-2019/new-search-feature.gif)

A nova lógica de pesquisa difusa localizará tudo o que você precisa, mesmo com erros de digitação. Se está procurando por comandos, configurações, documentação ou outras coisas úteis, o novo recurso de pesquisa facilita a localização de itens.

### <a name="refactorings"></a>Refatorações

Há muitas refatorações novas e altamente úteis no C# que facilitam a organizar seu código. Elas aparecem como sugestões na lâmpada e incluem ações como mover membros para classe base ou interface, ajustar os namespaces para coincidir com a estrutura de pastas, converter loops foreach em consultas Linq e muito mais.

   ![Animação da nova experiência de refatorações do Visual Studio 2019](media/vs-2019/refactorings.gif)

Basta invocar as refatorações pressionando **Ctrl+** e selecionar a ação desejada.

### <a name="intellicode"></a>IntelliCode

O [IntelliCode do Visual Studio](/visualstudio/intellicode/) aprimora os esforços de desenvolvimento de software, usando IA (inteligência artificial). O IntelliCode treina em 2.000 projetos de código-fonte aberto no GitHub, sendo cada um com mais de 100 estrelas, para gerar suas recomendações.

![Animação do IntelliCode no Visual Studio 2019](media/vs-2019/IntelliCode.gif)

Aqui estão algumas maneiras em que o Visual Studio IntelliCode pode ajudar a aumentar sua produtividade:

* Fornecer conclusões de código com percepção de contexto
* Orientar os desenvolvedores a aderir aos padrões e estilos de sua equipe
* Encontrar problemas de código difíceis de detectar
* Concentrar revisões de código chamando atenção para áreas que realmente importam

Quando fizemos a primeira versão prévia do IntelliCode como uma extensão para Visual Studio, ela era inicialmente compatível apenas com C#. Agora, **como uma novidade na versão 16.1**, adicionamos suporte para C# e XAML integrados. (No entanto, o suporte para C++ e TypeScript/JavaScript ainda está em versão prévia.)

E se você usa C#, também adicionamos a capacidade de treinar um modelo personalizado em seu próprio código.

Para obter mais informações sobre o IntelliCode, consulte as postagens no blog [Anunciando a disponibilidade geral do IntelliCode com mais uma espiada](https://devblogs.microsoft.com/visualstudio/announcing-the-general-availability-of-intellicode-plus-a-sneak-peek/) e [Codifique mais, role menos com o Visual Studio IntelliCode](https://devblogs.microsoft.com/visualstudio/code-more-scroll-less-with-visual-studio-intellicode/).

### <a name="code-cleanup"></a>Limpeza de Código

Juntamente com um novo indicador de integridade do documento, temos um novo comando de limpeza de código. Você pode usar esse novo comando para identificar e depois corrigir avisos e sugestões com o clique de um botão.

A limpeza formata o código e aplica todas as correções de código conforme sugerido pelas [configurações atuais](code-styles-and-code-cleanup.md) e [arquivos .editorconfig](create-portable-custom-editor-options.md).

   ![Captura de tela do novo controle de limpeza de código no Visual Studio 2019](media/vs-2019/code-cleanup-profile.png)

É possível também salvar coleções de reparadores como um perfil. Por exemplo, se você tem um pequeno conjunto de reparadores direcionados, que aplica com frequência durante a codificação, e se tem também outro conjunto abrangente de reparadores para aplicar antes de uma revisão de código, configure os perfis para realizar essas tarefas diferentes.

   ![Captura de tela do controle de configuração de limpeza de código no Visual Studio 2019](media/vs-2019/code-cleanup-profile-configure.png)

### <a name="per-monitor-aware-pma-rendering"></a>Renderização PMA (com reconhecimento por monitor)

Se você usa monitores configurados com fatores de escala de exibição diferentes ou se conecta remotamente a um computador com fatores de escala de exibição diferentes daqueles do seu dispositivo principal, você pode notar que o Visual Studio parece desfocado ou é renderizado na escala errada.

Com o lançamento do Visual Studio 2019, estamos tornando o Visual Studio um aplicativo PMA (com reconhecimento por monitor). Agora, o Visual Studio renderiza de modo correto, independentemente dos fatores de escala de exibição que você usa.

   ![Renderização PMA (com reconhecimento por monitor) no Visual Studio 2019](media/vs-2019/pma-dpi-scaling.png)

Para saber mais, confira a postagem no blog [Better multi-monitor experience with Visual Studio 2019 (Experiência ideal de Vários Monitores com o Visual Studio 2019)](https://devblogs.microsoft.com/visualstudio/a-better-multi-monitor-experience-with-visual-studio-2019/).

### <a name="test-explorer"></a>Gerenciador de Testes

**Novidade no 16,2**: atualizamos o Gerenciador de testes para fornecer melhor manipulação de grandes conjuntos de testes, filtragem mais fácil, comandos detectáveis, exibições com guias de playlist e colunas personalizáveis que permitem ajustar quais informações de teste são exibidas.

   ![Uma captura de tela que mostra os aprimoramentos da interface do usuário no Gerenciador de Testes](media/vs-2019/test-explorer-ui.png)

### <a name="net-core"></a>.NET Core

**Novidade no 16,3**: incluímos o suporte para o .net Core 3,0. Entre plataformas, software livre &mdash; e com suporte total da Microsoft.

Para obter mais informações, consulte a postagem no blog [anunciando o .NET Core 3,0](https://devblogs.microsoft.com/dotnet/announcing-net-core-3-0/) .

## <a name="collaborate"></a>Colaborar

Veja o vídeo a seguir para saber mais sobre como trabalhar em equipe para resolver problemas. <br><br>*Tamanho do vídeo: 4,22 minutos*

> [!VIDEO https://www.youtube.com/embed/dKLJsiK1QU8]

### <a name="git-first-workflow"></a>Fluxo de trabalho do git-First

Você observará a nova janela de início quando abrir o Visual Studio 2019.

   ![Captura de tela da nova janela de início do Visual Studio 2019](media/vs-2019/start-window-dark.png)

A janela de início apresenta várias opções para você começar a codificar rapidamente. Adicionamos a opção de primeiro clonar ou verificar o código de em um repositório.

   ![Animação da nova experiência "focada no Git" do Visual Studio 2019](media/vs-2019/git-first.gif)

A janela de início também inclui opções para abrir projetos ou soluções, abrir pastas locais ou criar novos projetos.

Para obter mais informações, consulte a postagem de blog [obter código: como projetamos a nova janela inicial do Visual Studio](https://devblogs.microsoft.com/visualstudio/get-to-code-how-we-designed-the-new-visual-studio-start-window/) .

### <a name="live-share"></a>Live Share

O [Visual Studio Live Share](https://visualstudio.microsoft.com/services/live-share/) é um serviço para desenvolvedores que permite compartilhar uma base de código e seu contexto com um membro da equipe e ter uma colaboração bidirecional instantânea diretamente no Visual Studio. Com o Live Share, um membro da equipe pode ler, navegar, editar e depurar um projeto compartilhado com ele de forma fácil e segura.

Com o Visual Studio 2019, esse serviço é instalado por padrão.

![Animação que mostra o recurso de colaboração Live Share no Visual Studio 2019](media/vs-2019/live-share.gif)

Para saber mais, confira as postagem no blog [Visual Studio Live Share for real-time code reviews and interactive education (Visual Studio Live Share para revisões de código em tempo real e educação interativa)](https://devblogs.microsoft.com/visualstudio/visual-studio-live-share-for-real-time-code-reviews-and-interactive-education/) e [Live Share now included with Visual Studio 2019 (O Live Share agora vem incluído no Visual Studio 2019)](https://devblogs.microsoft.com/visualstudio/live-share-now-included-with-visual-studio-2019/).

### <a name="integrated-code-reviews"></a>Revisões de código integradas

Estamos introduzindo uma nova extensão que você pode baixar para usar com o Visual Studio 2019. Com essa nova extensão, você pode revisar, executar e até mesmo depurar solicitações de pull da equipe sem sair do Visual Studio. Temos suporte para codificação nos repositórios do GitHub e do Azure DevOps.

   ![Captura de tela da nova janela de início do Visual Studio 2019](media/vs-2019/pr-experience.png)

Para obter mais informações, consulte a postagem no blog [Revisões de código usando a extensão Solicitações de Pull do Visual Studio](https://devblogs.microsoft.com/visualstudio/code-reviews-using-the-visual-studio-pull-requests-extension/).

## <a name="debug"></a>Depurar

Veja o vídeo a seguir para saber mais sobre como zerar com a segmentação precisa enquanto depura. <br><br>*Tamanho do vídeo: 3,54 minutos*

> [!VIDEO https://www.youtube.com/embed/hr72Fs8n_9c]

### <a name="performance-gains"></a>Benefícios no desempenho

Aproveitamos os pontos de interrupção de dados em C++ exclusivos e os adaptamos para aplicativos .NET Core.

   ![Animação que mostra os pontos de interrupção de dados de depuração no Visual Studio 2019](media/vs-2019/debug-data-breakpoints.gif)

Portanto, pontos de interrupção de dados podem ser uma ótima alternativa para a simples colocação de pontos de interrupção regulares, quando você está codificando em C++ ou no .NET Core. Pontos de interrupção de dados também são excelentes para cenários como localizar onde um objeto global está sendo modificado, adicionado, ou removido de uma lista.

Além disso, se você for um desenvolvedor de C++ que trabalha com grandes aplicativos, o Visual Studio 2019 cria símbolos fora do processo, o que permite depurar esses aplicativos sem passar por problemas relacionados à memória.

### <a name="search-while-debugging"></a>Pesquisar durante a depuração

Você provavelmente já esteve lá antes, procurando na janela Inspeção por uma cadeia de caracteres entre um conjunto de valores. No Visual Studio 2019, adicionamos uma pesquisa às janelas Inspeção, Locais e Autos para ajudá-lo a encontrar os objetos e os valores que você está procurando.

   ![Animação que mostra a janela de pesquisa de depuração no Visual Studio 2019](media/vs-2019/debug-window-search.gif)

Você também pode formatar o modo como um valor é exibido dentro das janelas Inspeção, Locais e Autos.  Clique duas vezes em um dos itens em qualquer uma das janelas e adicione uma vírgula (",") para acessar a lista suspensa de especificadores de formato possíveis, cada um dos quais inclui uma descrição de seu efeito pretendido.

   ![A nova janela Inspeção e o novo recurso de formatação de valores no Visual Studio 2019](media/search-watch-window.png)

Para obter mais informações, consulte [aprimorado no Visual Studio 2019: Pesquisar objetos e propriedades na postagem do blog assistir, automático e locals do Windows](https://devblogs.microsoft.com/visualstudio/enhanced-in-visual-studio-2019-search-for-objects-and-properties-in-the-watch-autos-and-locals-windows/) .

### <a name="snapshot-debugger"></a>Depurador de instantâneo

Obtenha um instantâneo da execução do aplicativo na nuvem para ver exatamente o que está acontecendo. Este recurso está disponível apenas no Visual Studio Enterprise.

   ![Animação que mostra o Depurador de Instantâneos no Visual Studio Enterprise 2019](media/vs-2019/snapshot-debugger.gif)

Adicionamos suporte para direcionamento de aplicativos do ASP.NET (Core e área de trabalho) que são executados em uma Máquina Virtual do Azure. Incluímos suporte para aplicativos executados em um Serviço de Kubernetes do Azure. O Depurador de Instantâneo pode ajudar a reduzir drasticamente o tempo que leva para resolver problemas que ocorrem em ambientes de produção.

Para saber mais, confira a página [Depurar aplicativos ASP.NET dinâmicos usando o Depurador de Instantâneos](../debugger/debug-live-azure-applications.md) e a postagem no blog [Apresentação da depuração de viagem no tempo para o Visual Studio Enterprise 2019](https://devblogs.microsoft.com/visualstudio/introducing-time-travel-debugging-for-visual-studio-enterprise-2019/).

### <a name="microsoft-edge-insider-support"></a>Suporte ao Microsoft Edge Insider

**Novidade em 16,2**: você pode definir um ponto de interrupção em um aplicativo JavaScript e iniciar uma sessão de depuração usando o navegador do [Microsoft Edge Insider](https://www.microsoftedgeinsider.com/) . Ao fazê-lo, o Visual Studio abre uma nova janela do navegador com a depuração habilitada, que você pode então usar para percorrer o aplicativo JavaScript dentro do Visual Studio.

   ![Uma captura de tela que mostra a renderização de código JavaScript em um navegador](media/vs-2019/edge-chromium-breakpoint.png)

### <a name="pinnable-properties-tool"></a>Ferramenta de propriedades fixas

**Novidade no 16,4**: agora, é mais fácil identificar objetos por suas propriedades durante a depuração com a nova ferramenta fixas Properties. Basta focalizar o cursor sobre uma propriedade que você deseja exibir na janela do depurador das janelas inspeção, automáticos e locais, selecionar o ícone de pino e ver imediatamente as informações que você está procurando na parte superior da janela!

   ![Uma animação que mostra como fixar Propriedades no depurador do Visual Studio usando a ferramenta de propriedades fixas](media/vs-2019/debugger-pinnable-properties.gif)

Para obter mais informações, consulte as [Propriedades fixas: Debug & exibir objetos gerenciados da sua](https://devblogs.microsoft.com/visualstudio/pinnable-properties-debug-display-managed-objects-your-way/) postagem no blog.

## <a name="whats-next"></a>O que vem a seguir

O Visual Studio 2019 é atualizado frequentemente com novos recursos que melhoram ainda mais a experiência de desenvolvimento. Para saber mais sobre nossas inovações mais recentes, confira o [blog do Visual Studio](https://devblogs.microsoft.com/visualstudio/). Para obter um registro do que lançamos em versão prévia até o momento, veja as [notas de versão de visualização](/visualstudio/releases/2019/release-notes-preview/). Para obter uma lista do que estamos planejando lançar em seguida, consulte o [mapa do Visual Studio](/visualstudio/productinfo/vs-roadmap).

Quer saber mais sobre as novidades do Visual Studio 2019? Confira o [Roteiro do Visual Studio](/visualstudio/productinfo/vs-roadmap/).

## <a name="give-us-feedback"></a>Fornecer comentários

Por que enviar comentários à equipe do Visual Studio? Porque nós levamos a sério os comentários dos clientes. Eles motivam muito do que fazemos.

* Se quiser fazer sugestões sobre como podemos melhorar o Visual Studio, você poderá fazer isso usando a ferramenta [Sugerir um Recurso](suggest-a-feature.md).

* Se você tiver um travamento, uma falha ou outro problema de desempenho, você poderá compartilhar facilmente conosco as etapas de reprodução e os arquivos de suporte usando a ferramenta [Relatar um Problema](how-to-report-a-problem-with-visual-studio.md).

## <a name="see-also"></a>Veja também

* [Notas de versão do Visual Studio 2019](/visualstudio/releases/2019/release-notes/)
* [Notas de versão do Visual Studio 2019 para Mac](/visualstudio/releasenotes/vs2019-mac-relnotes/)
* [O que há de novo no SDK do Visual Studio 2019](../extensibility/whats-new-visual-studio-2019-sdk.md)
* [Novidades do C++ no Visual Studio](/cpp/overview/what-s-new-for-visual-cpp-in-visual-studio.md)
* [O que há de novo no C# 8,0](/dotnet/csharp/whats-new/csharp-8.md)
* [Novidades do .NET Core 3.1](/dotnet/core/whats-new/dotnet-core-3-1.md)
* [O que há de novo no .NET Framework](/dotnet/framework/whats-new.md)
* [Conferência do Microsoft Build](https://www.microsoft.com/build)
* [Conferência do Microsoft Ignite](https://www.microsoft.com/ignite)
