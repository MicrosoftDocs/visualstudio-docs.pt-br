---
title: Criando o XAML
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 288e2415-9fcf-408e-bc35-9848315e14fd
caps.latest.revision: 6
author: gewarren
ms.author: gewarren
manager: ghogen
ms.openlocfilehash: 3ef644984b7c7fd364d389fb437b04f02d96b566
ms.sourcegitcommit: 708f77071c73c95d212645b00fa943d45d35361b
ms.translationtype: MTE95
ms.contentlocale: pt-BR
ms.lasthandoff: 12/07/2018
ms.locfileid: "53056315"
---
# <a name="designing-xaml-in-visual-studio"></a>Criando o XAML no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

O Visual Studio e o Blend for Visual Studio fornecem ferramentas visuais para criar interfaces do usuário envolventes e experiências de mídia avançada para aplicativos da área de trabalho do Windows baseados em XAML, Web, [Windows Phone](http://msdn.microsoft.com/library/windowsphone/develop/jj683071.aspx) e da [Windows Store](http://msdn.microsoft.com/library/windows/apps/jj129478.aspx). Ambos compartilham um conjunto comum de janelas de design e ferramentas e um editor XAML; porém, o Blend for Visual Studio fornece ferramentas de design adicionais para tarefas mais avançadas, como animações e comportamentos.

## <a name="choosing-the-right-tool"></a>Escolhendo a ferramenta certa
 Sua escolha de ferramentas de design depende, em grande parte, de seu conjunto de competências. Se você estiver mais orientado a código, poderá escrever o código XAML no Visual Studio para realizar até mesmo tarefas de design avançadas. Se você estiver mais orientado a design, o Blend for Visual Studio permitirá que você realize tarefas avançadas sem escrever nenhum código.

 É possível mudar entre o Visual Studio e o Blend for Visual Studio e até mesmo ter o mesmo projeto aberto nos dois ao mesmo tempo. As alterações feitas nos arquivos XAML em uma IDE podem ser aplicadas por meio de recarregamento automático ao mudar para a outra IDE. É possível controlar o comportamento de recarregamento por meio de opções na caixa de diálogo **Ferramentas**, **Opções** em uma das IDEs.

### <a name="shared-capabilities"></a>Funcionalidades compartilhadas
 Para tarefas mais básicas, a IDE do Visual Studio e do Blend for Visual Studio compartilham o mesmo conjunto de janelas e funcionalidades, com algumas diferenças sutis. Alguns destaques incluem:

-   **Uma interface de usuário consistente:** Você pode criar seus aplicativos no contexto conhecido da interface de usuário do Visual Studio, o que torna a alternância entre IDEs uma experiência mais agradável e produtiva. O Blend for Visual Studio usa o tema Escuro do Visual Studio, que ajuda você a se concentrar no conteúdo que está criando, melhorando o contraste entre o conteúdo e a interface do usuário. Consulte [Criando uma interface do usuário usando o Designer XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md).

     ![A IDE do Blend for Visual Studio](../designers/media/blendide.png "BlendIDE")

-   IntelliSense XAML Ambos os IDEs dão suporte a todos os recursos comuns que você esperaria do IntelliSense, incluindo preenchimento de declaração, suporte para operações comuns do editor como comentário e formatação de código e navegação para recursos, associação e código.

-   Capacidades básicas de depuração Agora você pode depurar no Blend, incluindo pontos de interrupção em seu código para depurar seu aplicativo em execução. Para manter uma experiência de depuração consistente com o Visual Studio, o Blend for Visual Studio inclui a maioria das janelas de depuração e barras de ferramentas do Visual Studio. Funcionalidades de depuração avançadas, como diagnóstico e análise de código, somente estão disponíveis no Visual Studio. Consulte [Depurando no Visual Studio](../debugger/debugging-in-visual-studio.md).

-   Experiência de recarregar arquivo Você pode editar os arquivos XAML no Blend for Visual Studio ou Visual Studio e ter os arquivos editados sejam recarregados automaticamente conforme você muda entre eles. Para minimizar as interrupções de fluxo de trabalho, agora é possível definir suas preferências de recarregamento de arquivos na caixa de diálogo de recarregamento de arquivos.

     ![Experiência de recarregamento de arquivos](../designers/media/blendfilereload.png "BlendFileReload")

-   **Layouts sincronizados e configurações:** Layouts personalizados permitem salvar e aplicar as personalizações de layout de janela de ferramenta. O Visual Studio sincronizará essas personalizações e preferências para o Visual Studio e o Blend for Visual Studio entre os computadores, quando você se conectar com a mesma conta da Microsoft. Consulte [Personalizando configurações de desenvolvimento no Visual Studio](http://msdn.microsoft.com/en-us/22c4debb-4e31-47a8-8f19-16f328d7dcd3).

-   **Um Gerenciador de soluções comuns:** O Gerenciador de soluções fornece uma exibição organizada de seus projetos e seus arquivos, bem como acesso imediato aos comandos associados a eles. Com o Gerenciador de Soluções, fica mais fácil trabalhar com projetos corporativos grandes. Consulte [Soluções e projetos](../ide/solutions-and-projects-in-visual-studio.md).

-   **Team Explorer:** com o Team Explorer, você pode gerenciar seus projetos com repositórios GIT ou TFS para facilitar a colaboração em equipe. Consulte [Trabalhar no Team Explorer](http://msdn.microsoft.com/library/fd7a5cf7-7916-4fa0-b5e6-5a83cf377a02).

-   NuGet Você pode gerenciar pacotes NuGet no Visual Studio e no Blend para Visual Studio. O NuGet é um gerenciador de pacotes do .NET Framework que simplifica a instalação e remoção de pacotes de uma solução.

## <a name="advanced-capabilities-in-blend-for-visual-studio"></a>Funcionalidades avançadas do Blend for Visual Studio
 Para aumentar sua produtividade, considere o uso do Blend for Visual Studio para as tarefas a seguir. Essas são as áreas em que o Blend for Visual Studio oferece mais velocidade e funcionalidade do que o designer do Visual Studio ou o código isolado.

|Para|Visual Studio|Blend for Visual Studio|Mais informações|
|--------|-------------------|-----------------------------|----------------------|
|**Criar animações**|Não há nenhuma ferramenta de design para animações; você precisa criá-las de forma programática. Isso exige noções básicas da animação e do sistema de tempo no WPF, além de amplas competências em codificação.|Você cria animações visualmente e pode visualizá-las no Blend for Visual Studio. Isso é mais rápido e mais preciso do que criar as animações em código. É possível adicionar gatilhos para manipular a interação do usuário e mudar para o código para adicionar manipuladores de eventos e outras funcionalidades.|[Animar objetos](../designers/animate-objects-in-xaml-designer.md)|
|**Transformar formas e texto em demarcadores para facilitar a manipulação**|Sem suporte.|Você pode fazer alterações sutis ou drásticas em formas (como retângulos e elipses) convertendo-as em demarcadores, que fornecem um melhor controle de edição.  É possível alterar a forma ou combinar demarcadores, além de criar demarcadores compostos com base em várias formas.<br /><br /> Você também pode converter blocos de texto em demarcadores para manipulá-los como imagens vetoriais.|[Desenhar formas e demarcadores](../designers/draw-shapes-and-paths.md)|
|**Adicionar interatividade a seus designs de interface do usuário**|Exige um código C#, Visual Basic ou C++.|Arraste e solte comportamentos em controles para adicionar interatividade aos designs estáticos. Os comportamentos são snippets de código prontos para uso que encapsulam funcionalidades como arrastar/soltar, zoom e alterações de estado visual. Há um conjunto cada vez maior de comportamentos que você pode escolher, além de poder criar seus próprios.<br /><br /> Em seguida, você pode personalizar cada comportamento alterando suas propriedades no Blend for Visual Studio ou adicionando manipuladores de eventos ao código.|[Inserir controles e modificar seu comportamento](../designers/insert-controls-and-modify-their-behavior-in-xaml-designer.md)|
|**Usar a arte da Adobe**|Sem suporte.|Importe a arte do Adobe FXG, PhotoShop ou Illustrator e implemente a interface do usuário no Blend for Visual Studio.|[Inserir imagens, vídeos e clipes de áudio](../designers/insert-images-videos-and-audio-clips-in-xaml-designer.md)|
|**Editar controles, modelos e estilos**|Exige a codificação e o conhecimento de estilos e modelos do WPF.|Transforme qualquer imagem em um controle.<br /><br /> Use as ferramentas de edição de modelo para fazer alterações em controles, estilos e modelos com apenas alguns cliques do mouse.<br /><br /> Por exemplo, é possível usar os recursos de estilo do Blend for Visual Studio para implementar controles WPF comuns (como botões, caixas de listagem, barras de rolagem, menus, etc.) e alterar a cor, o estilo ou o modelo subjacente diretamente no Blend for Visual Studio. Você pode mudar para o código para dar os toques finais, se desejar.|[Modificar o estilo de objetos](../designers/modify-the-style-of-objects-in-blend.md)|
|**Conectar a interface do usuário aos dados**|É possível criar uma fonte de dados com base em recursos, como bancos de dados SQL Server, o WCF ou serviços Web, objetos ou listas do SharePoint e associar a fonte de dados aos controles da interface do usuário.<br /><br /> Dados de tempo de design devem ser criados manualmente para proporcionar uma experiência de design interativa.|Crie dados de amostra facilmente para a criação de protótipo e testes. Muda para dados dinâmicos quando você está pronto.<br /><br /> As funcionalidades de geração de dados do Blend for Visual Studio são impressionantes (é possível adicionar nomes, números, URLs e fotos de maneira fácil e imediata) e podem economizar muito tempo.<br /><br /> Para dados dinâmicos, é possível associar os controles da interface do usuário a um arquivo XML ou a qualquer fonte de dados CLR.|[Exibir dados](../designers/display-data-in-blend.md)|

 Para obter mais informações sobre o design XAML avançado, consulte. [Criando uma interface do usuário usando o Blend for Visual Studio](../designers/creating-a-ui-by-using-blend-for-visual-studio.md)
