---
title: Mapas de código
ms.date: 05/16/2018
ms.topic: conceptual
f1_keywords:
- vs.progression.codemap
- vs.progression.standardgraphsdialog
helpviewer_keywords:
- DGML
- graph documents
- code visualization [Visual Studio]
- dependencies, visualizing
- dependency graphs
author: gewarren
ms.author: gewarren
manager: douge
ms.workload:
- multiple
ms.prod: visual-studio-dev15
ms.technology: vs-ide-modeling
ms.openlocfilehash: 51b03ce504b2fe8f588cf3e360882f97d61664f8
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49896933"
---
# <a name="map-dependencies-with-code-maps"></a>Mapear dependências com mapas de código

Você pode visualizar as dependências em seu código, criando um mapa de código. Mapas de código ajudam que você a ver como o código se ajusta sem ler nos arquivos e linhas de código.

![Exibir dependências com mapas de código no Visual Studio](../modeling/media/codemapsmainintro.png)

Para criar e editar os mapas de código, é necessário o Visual Studio Enterprise edition. No Visual Studio Community e Professional Edition, você pode abrir diagramas gerados no Enterprise edition, mas você não pode editá-los.

> [!NOTE]
> Antes de compartilhar mapas criados no Visual Studio Enterprise com outras pessoas que usam o Visual Studio Professional, certifique-se de que todos os itens no mapa (como itens ocultos, grupos expandidos e links de grupo cruzado) são visíveis.

Você pode mapear as dependências para código nestes idiomas:

- Visual c# ou Visual Basic em uma solução ou assemblies (*. dll* ou *.exe*)

- Código C ou C++ nativo ou gerenciado em projetos do Visual C++, arquivos de cabeçalho (*. h* ou `#include`), ou binários

- Projetos e assemblies do X++ feitos com base nos módulos do .NET para Microsoft AX Dynamics

> [!NOTE]
> Para projetos que não sejam c# ou Visual Basic, há menos opções para o início de um mapa de código ou adicionar itens a um mapa de código existente. Por exemplo, você não é um objeto no editor de texto de um projeto C++ com o botão direito e adicioná-lo a um mapa de código. No entanto, você pode arrastar e soltar elementos de código individuais ou arquivos a partir **Gerenciador de soluções**, **Class View**, e **Pesquisador de objetos**.

## <a name="install-code-map-and-live-dependency-validation"></a>Mapa de código de instalação e validação de dependência dinâmica

Para criar um mapa de código no Visual Studio 2017, primeiro instale o **mapa de códigos** e **validação de dependência dinâmica** componentes:

1. Abra **instalador do Visual Studio**. Você pode abri-lo no menu Iniciar do Windows ou no Visual Studio, selecionando **ferramentas** > **obter ferramentas e recursos**.

1. Selecione a guia **Componentes individuais**.

1. Role para baixo até a **ferramentas de código** seção e selecione **mapa de códigos** e **validação de dependência dinâmica**.

   ![Componentes de mapa de código e validação de dependência dinâmica no instalador do Visual Studio](media/modeling-components.png)

1. Selecione **Modificar**.

   O **mapa de códigos** e **validação de dependência dinâmica** componentes começam a instalação. Você pode ser solicitado a fechar o Visual Studio.

## <a name="add-a-code-map"></a>Adicionar um mapa de código

Você pode criar um mapa de código vazio e arrastar itens para ele, incluindo referências de assembly, arquivos e pastas, ou você pode gerar um mapa de códigos para todos ou parte de sua solução.

Para adicionar um mapa de código vazio:

1. Na **Gerenciador de soluções**, abra o menu de atalho do nó de solução de nível superior. Escolher **adicione** > **Novo Item**.

2. No **Adicionar Novo Item** caixa de diálogo, em **instalado**, escolha o **geral** categoria.

3. Escolha o **Directed Graph Document(.dgml)** modelo e selecione **Add**.

   > [!TIP]
   > Portanto, esse modelo pode não aparecer em ordem alfabética, role até o final da lista de modelos, se você não estiver visível.

   Um mapa em branco é exibido em sua solução **itens de solução** pasta.

Da mesma forma, você pode criar um novo arquivo de mapa de código sem adicioná-lo à sua solução, selecionando **arquitetura** > **novo mapa de códigos** ou **arquivo**  >  **Novos** > **arquivo**.

## <a name="generate-a-code-map-for-your-solution"></a>Gerar um mapa de código para sua solução

Para ver todas as dependências em sua solução:

1. Na barra de menus, escolha **arquitetura** > **gerar mapa de código para solução**. Se seu código não foi alterado desde a última vez que você o criou, você poderá selecionar **arquitetura** > **gerar mapa de código para a solução sem compilação** em vez disso.

   ![Gerar um comando de mapa de código](../modeling/media/codemapsarchitecturemenu.png)

   É gerado um mapa que mostra os assemblies de nível superior e os links agregados entre eles. Quanto maior o vínculo agregado, mais dependências ele representa.

2. Use o **legenda** botão na barra de ferramentas de mapa de código para mostrar ou ocultar a lista de ícones do tipo de projeto (por exemplo, teste, Web e projeto do Phone), itens de código (como Classes, métodos e propriedades) e tipos de relação (por exemplo, herda de Implementa e chamadas).

   ![Gráfico de dependência de nível superior de assemblies](../modeling/media/dependencygraph_toplevelassemblies.png)

   Essa solução de exemplo contém pastas de solução (**testes** e **componentes**), assemblies, projetos da Web e projetos de teste. Por padrão, todas as relações de confinamento pareçam *grupos*, que você pode expandir e recolher. O **Externals** grupo contém nada fora da sua solução, incluindo dependências de plataforma. Os assemblies externos mostram apenas os itens usados. Por padrão, os tipos de base do sistema estão ocultos no mapa para reduzir a desordem.

3. Para fazer drill down no mapa, expanda os grupos que representam projetos e assemblies. Você pode expandir tudo pressionando **CTRL + T** para selecionar todos os nós e, em seguida, escolhendo **grupo**, **expandir** no menu de atalho.

   ![Expansão de todos os grupos em um mapa de código](../modeling/media/codemapsexpandallgroups.png)

4. No entanto, isso não pode ser útil para uma solução grande. Na verdade, para soluções complexas, limitações de memória podem impedir que você expandir todos os grupos. Em vez disso, para ver dentro de um nó individual, expandi-lo. Mova o ponteiro do mouse sobre o nó e, em seguida, clique na divisa (seta para baixo) quando ele for exibido.

   ![Expandir um nó em um mapa de código](../modeling/media/dependencygraph_containment.png)

   Ou use o teclado selecionando o item, em seguida, pressionar a tecla de mais (**+**). Para explorar níveis mais profundos do código, faça o mesmo para namespaces, tipos e membros.

   > [!TIP]
   > Para obter mais detalhes sobre como trabalhar com o código de mapas usando o mouse, teclado e toque, consulte [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).

5. Para simplificar o mapa e se concentrar em partes individuais, escolha **filtros** na barra de ferramentas de mapa de código e selecione apenas os tipos de nós e links que lhe interessam. Por exemplo, você pode ocultar todas as pastas de solução e Assembly recipientes.

   ![Simplificar o mapa pela filtragem de contêineres](../modeling/media/codemapsfilterfoldersassemblies.png)

   Você também pode simplificar o mapa, ocultar ou removendo grupos individuais e itens do mapa, sem afetar o código subjacente da solução.

6. Para ver as relações entre itens, selecione-os no mapa. As cores dos links indicam os tipos de relação, conforme mostrado na **legenda** painel.

   ![Exibir dependências nas soluções](../modeling/media/codemapsmainintro.png)

   Neste exemplo, os links de roxos são chamadas, os links pontilhados são referências e os links de azuis claras são acesso de campo. Links de verde pode ser herança ou podem ser *agregar links* que indicam que mais de um tipo de relação (ou *categoria*).

   > [!TIP]
   > Se você vir um link verde, ele pode não significar que exista apenas uma relação de herança. Também podem ser chamadas de método, mas estão ocultas pela relação de herança. Para ver tipos específicos de links, use as caixas de seleção na **filtros** painel para ocultar os tipos que não esteja interessado em.

7. Para obter mais informações sobre um item ou link, mova o ponteiro sobre ele, até que uma dica de ferramenta seja exibida. Isso mostra detalhes de um elemento de código ou as categorias que representa um link.

   ![Mostrar as categorias de uma relação](../modeling/media/codemapsshowlinkcatgories.png)

8. Para examinar itens e dependências representados por um link agregado, primeiro selecione o link e, em seguida, abra o menu de atalho. Escolher **Mostrar Links participantes** (ou **Mostrar Links participantes no novo mapa de códigos**). Isso expande os grupos em ambas as extremidades do link e mostra somente os itens e as dependências que participam no link.

9. Para focalizar em partes específicas do mapa, você pode continuar a remover itens que não esteja interessado em. Por exemplo, para detalhar o modo de exibição de classe e membro, simplesmente filtrar todos os nós de namespace na **filtros** painel.

   ![Busca detalhada em nível de classe e membro](../modeling/media/dependencygraph_expandedselectedgroups_2012.png)

10. Outra maneira de se concentrar em um mapa de solução complexa é gerar um novo mapa que contém os itens selecionados de um mapa existente. Mantenha **Ctrl** enquanto seleciona os itens que você deseja se concentrar em, abra o menu de atalho e escolha **da seleção de um novo gráfico**.

    ![Mostrar itens selecionados em um novo mapa de código](../modeling/media/codemapsshowonnewmap.png)

11. O contexto de recipiente é transportado para o novo mapa. Ocultar pastas de solução e quaisquer outros contêineres que você não deseja ver usando o **filtros** painel.

    ![Os contêineres para simplificar a exibição de filtro](../modeling/media/codemapsexpandnewgroups.png)

12. Expanda os grupos e selecionar itens no mapa para exibir as relações.

    ![Selecionar itens para exibir as relações](../modeling/media/codemapsviewnewrelationships.png)

Consulte também:

- [Procurar e reorganizar mapas de códigos](../modeling/browse-and-rearrange-code-maps.md)
- [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
- Localizar possíveis problemas no seu código por [executando um analisador](../modeling/find-potential-problems-using-code-map-analyzers.md)

## <a name="view-specific-dependencies-in-a-code-map"></a>Exibir dependências específicas em um mapa de código

Suponha que você tenha uma revisão de código para executar em alguns arquivos com alterações pendentes. Para ver as dependências nessas alterações, você pode criar um mapa de código dos arquivos.

   ![Mostrar as dependências específicas em um mapa de código](../modeling/media/codemapsspecificdependenciesintro.png)

1. Na **Gerenciador de soluções**, selecione os projetos, referências de assembly, pastas, arquivos, tipos ou membros que você deseja mapear.

   ![Selecione os itens que você deseja mapear](../modeling/media/codemapsselectinsolutionexplorer.png)

1. Sobre o **Gerenciador de soluções** barra de ferramentas, escolha **Mostrar no mapa de códigos** ![criar novo gráfico selecionado nós botão de](../modeling/media/createnewgraphfromselectedbutton.gif). Ou, abra o menu de atalho para um ou um grupo de itens e escolha **Mostrar no mapa de códigos**.

   Você também pode arrastar itens da **Gerenciador de soluções**, **Class View**, ou **Pesquisador de objetos**, em um [novo](#add-a-code-map) ou código existente do mapa. Para incluir a hierarquia pai para seus itens, pressione e segure a **Ctrl** pressionada enquanto você arrasta itens, ou usar o **pais incluem** botão na barra de ferramentas de mapa de código para especificar a ação padrão. Você também pode arrastar arquivos de assembly de fora do Visual Studio, como da **Windows Explorer**.

   > [!NOTE]
   > Quando você adiciona itens de um projeto que é compartilhado entre vários aplicativos, como Windows Phone ou da Microsoft Store, esses itens são exibidos no mapa com o projeto de aplicativo ativo no momento. Se você alterar o contexto para outro projeto de aplicativo e adicionar mais itens do projeto compartilhado, esses itens agora serão exibidos com o projeto de aplicativo recém-ativo. Operações realizadas com um item no mapa se aplicam apenas aos itens que compartilham o mesmo contexto.

3. O mapa mostra os itens selecionados em seus assemblies de recipientes.

   ![Itens selecionados, mostrados como grupos no mapa](../modeling/media/codemapsshowitemsfromsolnexplorer.png)

4. Para explorar itens, expanda-os. Mova o ponteiro do mouse sobre um item e, em seguida, clique no ícone de divisa (seta para baixo) quando ele for exibido.

   ![Expanda um nó em um mapa de código](../modeling/media/dependencygraph_containment.png)

   Para expandir todos os itens, selecione-os usando **Ctrl**+**um**, em seguida, abra o menu de atalho para o mapa e escolha **grupo**  >   **Expanda**. No entanto, essa opção não estará disponível se a expansão de todos os grupos cria um mapa inutilizável ou problemas de memória.

5. Continue a expandir os itens que você está interessado, chegando até o nível de classe e membro, se necessário.

   ![Expandir grupos para o nível de classe e membro](../modeling/media/codemapsexpandtoclassandmember.png)

   Para ver os membros que estão no código, mas não são exibidos no mapa, clique o **buscar novamente filhos** ícone ![buscar novamente filhos ícone](../modeling/media/dependencygraph_deletednodesicon.png) no canto superior esquerdo de um grupo.

6. Para ver mais itens relacionados a esses no mapa, selecione um e escolha **Mostrar relacionados** na barra de ferramentas de mapa de código, selecione o tipo de itens relacionados para adicionar ao mapa. Como alternativa, selecione um ou mais itens, abra o menu de atalho e, em seguida, escolha o **Mostrar** opção para o tipo de itens relacionados para adicionar ao mapa. Por exemplo:

    Para um **assembly**, escolha:

    |||
    |-|-|
    |**Mostrar Assemblies referenciados por este**|Adicione assemblies a que este assembly faz referência. Assemblies externos são exibidos na **Externals** grupo.|
    |**Mostrar Assemblies fazendo referência a esse**|Adicione assemblies na solução que fazem referência a este assembly.|

    Para um **namespace**, escolha **Mostrar Assembly que contém**, se não estiver visível.

    Para um **classe** ou **interface**, escolha:

    |||
    |-|-|
    |**Mostrar Tipos Base**|Para obter uma classe, adicione a classe base e as interfaces implementadas.<br /><br /> Para obter uma interface, adicione as interfaces de base.|
    |**Mostrar Tipos Derivados**|Para obter uma classe, adicione as classes derivadas.<br /><br /> Para obter uma interface, adicione as interfaces derivadas e as classes de implementação ou structs.|
    |**Mostrar tipos referenciados por este**|Adicione todas as classes e os membros que essa classe usa.|
    |**Mostrar tipos fazendo referência a esse**|Adicione todas as classes e seus membros que usam essa classe.|
    |**Mostrar que contém o Namespace**|Adicione o namespace pai.|
    |**Mostrar Assembly e Namespace que contém**|Adicione a hierarquia do contêiner pai.|
    |**Mostrar todos os tipos Base**|Adicione a classe base ou a hierarquia de interface recursivamente.|
    |**Mostrar todos os tipos derivados**|Para obter uma classe, adicione todas as classes derivadas recursivamente.<br /><br /> Para obter uma interface, adicione todas as interfaces derivadas e as classes de implementação ou structs recursivamente.|

     Para um **método**, escolha:

    |||
    |-|-|
    |**Mostrar métodos chamados por este**|Adicione métodos que esse método chama.|
    |**Mostrar campos referenciados por este**|Adicione campos a que este método faz referência.|
    |**Mostrar tipo recipiente**|Adicione o tipo de pai.|
    |**Mostrar tipo recipiente, Namespace e Assembly**|Adicione a hierarquia do contêiner pai.|
    |**Mostrar métodos substituídos**|Para obter um método que substitui outros métodos ou implementa o método de uma interface, adicione todos os métodos abstratos ou virtuais em classes base que sejam substituídas e, se houver algum, o método da interface implementado.|

     Para um **campo** ou **propriedade**, escolha:

    |||
    |-|-|
    |**Mostrar tipo recipiente**|Adicione o tipo de pai.|
    |**Mostrar tipo recipiente, Namespace e Assembly**|Adicione a hierarquia do contêiner pai.|

    ![Mostrar métodos chamados por este membro](../modeling/media/codemapsshowrelatedmethods.png)

7. O mapa mostra as relações. Neste exemplo, o mapa mostra os métodos chamados `Find` método e sua localização na solução ou externamente.

   ![Mostrar as dependências específicas em um mapa de código](../modeling/media/codemapsspecificdependenciesintro.png)

8. Para simplificar o mapa e se concentrar em partes individuais, escolha **filtros** na barra de ferramentas de mapa de código e selecione apenas os tipos de nós e links que lhe interessam. Por exemplo, desative a exibição de pastas de solução, Assemblies e Namespaces.

   ![Use o painel de filtro para simplificar a exibição](../modeling/media/almcodemapfilterpane.png)

## <a name="see-also"></a>Consulte também

- [Vídeo: entenda design de código com mapas de código do Visual Studio 2015](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2015/502)]
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
- [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [Procurar e reorganizar mapas de códigos](../modeling/browse-and-rearrange-code-maps.md)
- [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
