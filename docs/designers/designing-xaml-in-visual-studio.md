---
title: Criando o XAML no Visual Studio
ms.date: 07/17/2017
ms.prod: visual-studio-dev15
ms.technology: vs-ide-designers
ms.topic: conceptual
ms.assetid: 288e2415-9fcf-408e-bc35-9848315e14fd
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- uwp
ms.openlocfilehash: c23a73302e5d4771b3372b8f4534b42806156da0
ms.sourcegitcommit: dd839de3aa24ed7cd69f676293648c6c59c6560a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52389611"
---
# <a name="design-xaml-in-visual-studio"></a>Criar XAML no Visual Studio

O Visual Studio e o Blend for Visual Studio fornecem ferramentas visuais para criar interfaces do usuário envolventes e experiências de mídia avançadas com XAML para vários tipos de aplicativos. As duas ferramentas compartilham um conjunto comum de recursos, incluindo um editor XAML visual, mas o Blend for Visual Studio fornece ferramentas de design adicionais para tarefas mais avançadas como animação e comportamentos.

O processo de criação de um aplicativo depende da ferramenta que você escolher e sua plataforma de destino. Este artigo compara as ferramentas de design de XAML no Visual Studio e no Blend for Visual Studio. Para passo a passos do uso da ferramenta mais detalhados, consulte os tópicos a seguir:

- [Criar uma interface de usuário usando o XAML Designer no Visual Studio](creating-a-ui-by-using-xaml-designer-in-visual-studio.md)
- [Criar uma interface do usuário usando o Blend for Visual Studio](creating-a-ui-by-using-blend-for-visual-studio.md)

## <a name="choose-the-right-tool"></a>Escolher a ferramenta certa

Sua escolha de ferramentas de design depende, em grande parte, de seu conjunto de competências. Se você estiver mais direcionado a código, escreva o código XAML no Visual Studio para realizar tarefas de design avançadas. Se você estiver mais orientado a design, o Blend for Visual Studio permitirá que você realize tarefas avançadas sem escrever nenhum código.

É possível mudar entre o Visual Studio e o Blend for Visual Studio e até mesmo ter o mesmo projeto aberto nos dois ao mesmo tempo. As alterações feitas nos arquivos XAML em uma IDE podem ser aplicadas por meio de recarregamento automático ao mudar para a outra IDE. É possível controlar o comportamento de recarregamento por meio das opções na caixa de diálogo **Ferramentas** > **Opções** em um dos IDEs.

### <a name="shared-capabilities"></a>Funcionalidades compartilhadas

Para tarefas mais básicas, a IDE do Visual Studio e do Blend for Visual Studio compartilham o mesmo conjunto de janelas e funcionalidades, com algumas diferenças sutis. Alguns destaques incluem:

- **Uma interface do usuário consistente:** você pode criar seus aplicativos no contexto conhecido da interface do usuário do Visual Studio, que torna a alternância entre IDEs uma experiência mais agradável e produtiva. O Blend for Visual Studio usa o tema Escuro do Visual Studio, que ajuda você a se concentrar no conteúdo que está criando, melhorando o contraste entre o conteúdo e a interface do usuário. Confira [Criar uma interface do usuário usando o Designer XAML](../designers/creating-a-ui-by-using-xaml-designer-in-visual-studio.md).

     ![A IDE do Blend para Visual Studio](../designers/media/blendide.png)

- **XAML IntelliSense:** as IDEs dão suporte a todas as funcionalidades comuns que você espera do IntelliSense, incluindo preenchimento de declaração, suporte para operações comuns do editor como comentário e formatação de código, bem como navegação para recursos, associação e código.

- **Funcionalidades básicas de depuração:** agora é possível depurar no Blend, incluindo a configuração de pontos de interrupção no código para depurar o aplicativo em execução. Para manter uma experiência de depuração consistente com o Visual Studio, o Blend for Visual Studio inclui a maioria das janelas de depuração e barras de ferramentas do Visual Studio. Funcionalidades de depuração avançadas, como diagnóstico e análise de código, somente estão disponíveis no Visual Studio. Confira [Depurar no Visual Studio](../debugger/debugging-in-visual-studio.md).

- **Experiência de recarregamento de arquivos:** você pode editar os arquivos XAML no Blend for Visual Studio ou no Visual Studio e fazer com que os arquivos editados sejam recarregados automaticamente conforme você muda entre eles. Para minimizar as interrupções de fluxo de trabalho, agora é possível definir suas preferências de recarregamento de arquivos na caixa de diálogo de recarregamento de arquivos.

     ![Experiência de recarregar arquivo](../designers/media/blendfilereload.png)

- **Layouts e configurações sincronizados:** layouts personalizados permitem salvar e aplicar as personalizações de layout da janela de ferramentas. O Visual Studio sincroniza essas personalizações e preferências entre o Visual Studio e o Blend para Visual Studio entre os computadores quando você se conecta com a mesma conta Microsoft. Confira [Sincronizar configurações em vários computadores](../ide/synchronized-settings-in-visual-studio.md).

- **Um Gerenciador de Soluções comum:** o **Gerenciador de Soluções** fornece uma exibição organizada dos projetos e de seus arquivos, bem como o acesso imediato aos comandos associados a eles. Com o Gerenciador de Soluções, fica mais fácil trabalhar com projetos corporativos grandes. Confira [Soluções e projetos](../ide/solutions-and-projects-in-visual-studio.md).

- **Team Explorer:** com o Team Explorer, você pode gerenciar seus projetos com repositórios GIT ou TFS para facilitar a colaboração em equipe. Consulte [Trabalhar no Team Explorer](/azure/devops/user-guide/work-team-explorer).

- **NuGet:** é possível gerenciar pacotes NuGet no Visual Studio e no Blend for Visual Studio. O NuGet é um gerenciador de pacotes do .NET Framework que simplifica a instalação e remoção de pacotes de uma solução.

## <a name="advanced-capabilities-in-blend-for-visual-studio"></a>Funcionalidades avançadas do Blend for Visual Studio

Para aumentar sua produtividade, considere o uso do Blend for Visual Studio para as tarefas a seguir. Essas são as áreas em que o Blend for Visual Studio oferece mais velocidade e funcionalidade do que o designer do Visual Studio ou o código isolado.

|Para|Visual Studio|Blend for Visual Studio|Mais informações|
|--------|-------------------| - | - |
|**Criar animações**|Não há nenhuma ferramenta de design para animações; você precisa criá-las de forma programática. Isso exige noções básicas da animação e do sistema de tempo no WPF, além de amplas competências em codificação.|Você cria animações visualmente e pode visualizá-las no Blend for Visual Studio. Isso é mais rápido e mais preciso do que criar as animações em código. É possível adicionar gatilhos para manipular a interação do usuário e mudar para o código para adicionar manipuladores de eventos e outras funcionalidades.|[Animar objetos](../designers/animate-objects-in-xaml-designer.md)|
|**Transformar formas e texto em demarcadores para facilitar a manipulação**|Sem suporte.|Você pode fazer alterações sutis ou drásticas em formas (como retângulos e elipses) convertendo-as em demarcadores, que fornecem um melhor controle de edição. É possível alterar a forma ou combinar demarcadores, além de criar demarcadores compostos com base em várias formas.<br /><br /> Você também pode converter blocos de texto em demarcadores para manipulá-los como imagens vetoriais.|[Desenhar formas e demarcadores](../designers/draw-shapes-and-paths.md)|
|**Adicionar interatividade a seus designs de interface do usuário**|Exige um código C#, Visual Basic ou C++.|Arraste e solte comportamentos em controles para adicionar interatividade aos designs estáticos. Os comportamentos são snippets de código prontos para uso que encapsulam funcionalidades como arrastar/soltar, zoom e alterações de estado visual. Há um conjunto cada vez maior de comportamentos que você pode escolher, e também é possível criar os seus próprios.<br /><br /> Em seguida, você pode personalizar cada comportamento alterando suas propriedades no Blend for Visual Studio ou adicionando manipuladores de eventos ao código.|[Inserir controles e modificar seu comportamento](../designers/insert-controls-and-modify-their-behavior-in-xaml-designer.md)|
|**Usar a arte da Adobe**|Sem suporte.|Importe a arte do Adobe FXG, PhotoShop ou Illustrator e implemente a interface do usuário no Blend for Visual Studio.|[Inserir imagens, vídeos e clipes de áudio](../designers/insert-images-videos-and-audio-clips-in-xaml-designer.md)|
|**Editar controles, modelos e estilos**|Exige a codificação e o conhecimento de estilos e modelos do WPF.|Transforme qualquer imagem em um controle.<br /><br /> Use as ferramentas de edição de modelo para fazer alterações em controles, estilos e modelos com apenas alguns cliques do mouse.<br /><br /> Por exemplo, é possível usar os recursos de estilo do Blend for Visual Studio para implementar controles WPF comuns (como botões, caixas de listagem, barras de rolagem, menus, etc.) e alterar a cor, o estilo ou o modelo subjacente diretamente no Blend for Visual Studio. Você pode mudar para o código para dar os toques finais, se desejar.|[Modificar o estilo de objetos](../designers/modify-the-style-of-objects-in-blend.md)|
|**Conectar a interface do usuário aos dados**|É possível criar uma fonte de dados com base em recursos, como bancos de dados SQL Server, o WCF ou serviços Web, objetos ou listas do SharePoint e associar a fonte de dados aos controles da interface do usuário.<br /><br /> Dados de tempo de design devem ser criados manualmente para proporcionar uma experiência de design interativa.|Crie dados de amostra facilmente para a criação de protótipo e testes. Mude para dados dinâmicos quando você estiver pronto.<br /><br /> As funcionalidades de geração de dados do Blend para Visual Studio são impressionantes (é possível adicionar nomes, números, URLs e fotos de maneira fácil e imediata) e podem economizar um bom tempo.<br /><br /> Para dados dinâmicos, é possível associar os controles da interface do usuário a um arquivo XML ou a qualquer fonte de dados CLR.|[Exibir dados](../designers/display-data-in-blend.md)|

Para obter mais informações sobre design avançado de XAML, confira [Criar uma interface do usuário usando o Blend para Visual Studio](../designers/creating-a-ui-by-using-blend-for-visual-studio.md).
