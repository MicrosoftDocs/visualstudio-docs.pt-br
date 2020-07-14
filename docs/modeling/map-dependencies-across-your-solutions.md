---
title: Mapas de código
ms.date: 05/16/2018
ms.topic: how-to
f1_keywords:
- vs.progression.codemap
- vs.progression.standardgraphsdialog
helpviewer_keywords:
- DGML
- graph documents
- code visualization [Visual Studio]
- dependencies, visualizing
- dependency graphs
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 771a6ccf4749a3464204d3da75f4d403d1ab2dd5
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85532711"
---
# <a name="map-dependencies-with-code-maps"></a>Mapear dependências com mapas de código

Você pode visualizar as dependências em seu código criando um mapa de código. Os mapas de código ajudam você a ver como o código se encaixa sem ler arquivos e linhas de código.

![Exibir dependências com mapas de código no Visual Studio](../modeling/media/codemapsmainintro.png)

Para criar e editar mapas de código, você precisa de Visual Studio Enterprise edição. Nas edições Visual Studio Community e Professional, você pode abrir diagramas gerados no Enterprise Edition, mas não pode editá-los.

> [!NOTE]
> Antes de compartilhar mapas criados em Visual Studio Enterprise com outras pessoas que usam Visual Studio Professional, verifique se todos os itens no mapa (como itens ocultos, grupos expandidos e links entre grupos) estão visíveis.

Você pode mapear as dependências para o código nestes idiomas:

- Visual C# ou Visual Basic em uma solução ou assemblies (*. dll* ou *. exe*)

- Código C ou C++ gerenciado ou nativo em projetos Visual C++, arquivos de cabeçalho (*. h* ou `#include` ) ou binários

- Projetos e assemblies do X++ feitos com base nos módulos do .NET para Microsoft AX Dynamics

> [!NOTE]
> Para projetos diferentes de C# ou Visual Basic, há menos opções para iniciar um mapa de código ou adicionar itens a um mapa de código existente. Por exemplo, você não pode clicar com o botão direito do mouse em um objeto no editor de texto de um projeto C++ e adicioná-lo a um mapa de código. No entanto, você pode arrastar e soltar elementos de código individuais ou arquivos de **Gerenciador de soluções**, **modo de exibição de classe**e **pesquisador de objetos**.

## <a name="install-code-map-and-live-dependency-validation"></a>Instalar mapa de código e validação de dependência ao vivo

Para criar um mapa de código no Visual Studio, primeiro instale o **mapa de código** e os componentes de validação de **dependência ao vivo** :

1. Abra **instalador do Visual Studio**. Você pode abri-lo no menu Iniciar do Windows ou no Visual Studio selecionando **ferramentas**  >  **obter ferramentas e recursos**.

1. Selecione a guia **Componentes individuais**.

1. Role para baixo até a seção **ferramentas de código** e selecione **mapa de código** e **validação de dependência ao vivo**.

   ![Mapa de códigos e componentes de validação de dependência ao vivo no Instalador do Visual Studio](media/modeling-components.png)

1. Selecione **Modificar**.

   Os componentes **mapa de código** e validação de **dependência ao vivo** começam a ser instalados. Talvez seja solicitado que você feche o Visual Studio.

## <a name="add-a-code-map"></a>Adicionar um mapa de código

Você pode criar um mapa de código vazio e arrastar itens para ele, incluindo referências de assembly, arquivos e pastas, ou você pode gerar um mapa de código para toda ou parte de sua solução.

Para adicionar um mapa de código vazio:

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó de solução de nível superior. Escolha **Adicionar**  >  **novo item**.

2. Na caixa de diálogo **Adicionar novo item** , em **instalado**, escolha a categoria **geral** .

3. Escolha o modelo de **documento gráfico direcionado (. dgml)** e, em seguida, selecione **Adicionar**.

   > [!TIP]
   > Esse modelo pode não aparecer em ordem alfabética, portanto, role para baixo até a parte inferior da lista de modelos, se você não o vir.

   Um mapa em branco aparece na pasta de **itens de solução** da solução.

Da mesma forma, você pode criar um novo arquivo de mapa de código sem adicioná-lo à sua solução selecionando **arquitetura**  >  **novo mapa de código** ou **arquivo**  >  **novo**  >  **arquivo**.

## <a name="generate-a-code-map-for-your-solution"></a>Gerar um mapa de código para sua solução

Para ver todas as dependências em sua solução:

1. Na barra de menus, escolha **arquitetura**  >  **gerar mapa de código para solução**. Se o código não foi alterado desde a última vez que você o criou, você pode selecionar a **arquitetura**  >  **gerar mapa de código para solução sem compilar** em vez disso.

   ![Gerar um comando de mapa de código](../modeling/media/codemapsarchitecturemenu.png)

   É gerado um mapa que mostra os assemblies de nível superior e os links agregados entre eles. Quanto maior o vínculo agregado, mais dependências ele representa.

2. Use o botão **legenda** na barra de ferramentas do mapa de códigos para mostrar ou ocultar a lista de ícones de tipo de projeto (como projeto de teste, Web e telefone), itens de código (como classes, métodos e propriedades) e tipos de relação (como herda de, implementações e chamadas).

   ![Grafo de dependência de nível superior de assemblies](../modeling/media/dependencygraph_toplevelassemblies.png)

   Esta solução de exemplo contém pastas de solução (**testes** e **componentes**), projetos de teste, projetos Web e assemblies. Por padrão, todas as relações de confinamento aparecem como *grupos*, que podem ser expandidas e recolhidas. O grupo **externo** contém qualquer coisa fora da sua solução, incluindo dependências de plataforma. Os assemblies externos mostram apenas os itens usados. Por padrão, os tipos de base do sistema ficam ocultos no mapa para reduzir a desordem.

3. Para fazer uma busca detalhada no mapa, expanda os grupos que representam projetos e assemblies. Você pode expandir tudo pressionando **Ctrl + a** para selecionar todos os nós e, em seguida, escolhendo **Agrupar**, **expandir** no menu de atalho.

   ![Expandindo todos os grupos em um mapa de códigos](../modeling/media/codemapsexpandallgroups.png)

4. No entanto, isso pode não ser útil para uma solução grande. Na verdade, para soluções complexas, as limitações de memória podem impedi-lo de expandir todos os grupos. Em vez disso, para ver dentro de um nó individual, expanda-o. Mova o ponteiro do mouse sobre o nó e, em seguida, clique na divisa (seta para baixo) quando ela aparecer.

   ![Expandindo um nó em um mapa de código](../modeling/media/dependencygraph_containment.png)

   Ou use o teclado selecionando o item e pressionando a tecla de adição ( **+** ). Para explorar níveis mais profundos do código, faça o mesmo para namespaces, tipos e membros.

   > [!TIP]
   > Para obter mais detalhes sobre como trabalhar com mapas de código usando o mouse, o teclado e o toque, consulte [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).

5. Para simplificar o mapa e concentrar-se em partes individuais, escolha **filtros** na barra de ferramentas do mapa de códigos e selecione apenas os tipos de nós e links nos quais você está interessado. Por exemplo, você pode ocultar todos os contêineres de pasta de solução e assembly.

   ![Simplificar o mapa filtrando contêineres](../modeling/media/codemapsfilterfoldersassemblies.png)

   Você também pode simplificar o mapa ocultando ou removendo grupos e itens individuais do mapa, sem afetar o código de solução subjacente.

6. Para ver as relações entre os itens, selecione-os no mapa. As cores dos links indicam os tipos de relação, conforme mostrado no painel de **legenda** .

   ![Exibir dependências em suas soluções](../modeling/media/codemapsmainintro.png)

   Neste exemplo, os links roxos são chamadas, os links pontilhados são referências e os links azuis claros são acesso ao campo. Links verdes podem ser heranças ou podem ser *links de agregação* que indicam mais de um tipo de relação (ou *categoria*).

   > [!TIP]
   > Se você vir um link verde, ele pode não significar que exista apenas uma relação de herança. Também podem ser chamadas de método, mas estão ocultas pela relação de herança. Para ver tipos específicos de links, use as caixas de seleção no painel **filtros** para ocultar os tipos nos quais você não está interessado.

7. Para obter mais informações sobre um item ou link, mova o ponteiro sobre ele até que uma dica de ferramenta seja exibida. Isso mostra detalhes de um elemento de código ou das categorias que um link representa.

   ![Mostrar as categorias de uma relação](../modeling/media/codemapsshowlinkcatgories.png)

8. Para examinar itens e dependências representados por um link de agregação, primeiro selecione o link e, em seguida, abra o menu de atalho. Escolha **Mostrar links contribuintes** (ou **Mostrar links contribuintes no novo mapa de código**). Isso expande os grupos em ambas as extremidades do link e mostra somente os itens e as dependências que participam do link.

9. Para se concentrar em partes específicas do mapa, você pode continuar a remover itens dos quais não está interessado. Por exemplo, para detalhar a exibição de classe e membro, basta filtrar todos os nós de namespace no painel **filtros** .

   ![Detalhamento para nível de classe e de membro](../modeling/media/dependencygraph_expandedselectedgroups_2012.png)

10. Outra maneira de se concentrar em um mapa de solução complexo é gerar um novo mapa que contém os itens selecionados de um mapa existente. Mantenha **Ctrl** ao selecionar os itens nos quais você deseja se concentrar, abra o menu de atalho e escolha **novo grafo na seleção**.

    ![Mostrar itens selecionados em um novo mapa de código](../modeling/media/codemapsshowonnewmap.png)

11. O contexto de contenção é transportado para o novo mapa. Oculte pastas de solução e quaisquer outros contêineres que você não queira ver usando o painel **filtros** .

    ![Filtrar os contêineres para simplificar a exibição](../modeling/media/codemapsexpandnewgroups.png)

12. Expanda os grupos e selecione os itens no mapa para exibir as relações.

    ![Selecionar itens para exibir as relações](../modeling/media/codemapsviewnewrelationships.png)

Veja também:

- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)
- [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
- Encontre possíveis problemas em seu código [executando um analisador](../modeling/find-potential-problems-using-code-map-analyzers.md)

## <a name="view-specific-dependencies-in-a-code-map"></a>Exibir dependências específicas em um mapa de códigos

Suponha que você tenha uma revisão de código para executar em alguns arquivos com alterações pendentes. Para ver as dependências dessas alterações, você pode criar um mapa de código a partir desses arquivos.

   ![Mostrar dependências específicas em um mapa de códigos](../modeling/media/codemapsspecificdependenciesintro.png)

1. Em **Gerenciador de soluções**, selecione os projetos, referências de assembly, pastas, arquivos, tipos ou membros que você deseja mapear.

   ![Selecione os itens que você deseja mapear](../modeling/media/codemapsselectinsolutionexplorer.png)

1. Na barra de ferramentas **Gerenciador de soluções** , escolha **Mostrar no mapa de códigos** ![ criar novo grafo a partir do botão nós selecionados ](../modeling/media/createnewgraphfromselectedbutton.gif) . Ou abra o menu de atalho para um ou um grupo de itens e escolha **Mostrar no mapa de códigos**.

   Você também pode arrastar itens de **Gerenciador de soluções**, **modo de exibição de classe**ou **pesquisador de objetos**, em um mapa de código [novo](#add-a-code-map) ou existente. Para incluir a hierarquia pai de seus itens, pressione e segure a tecla **Ctrl** enquanto arrasta os itens ou use o botão **incluir pais** na barra de ferramentas do mapa de códigos para especificar a ação padrão. Você também pode arrastar arquivos de assembly de fora do Visual Studio, como no **Windows Explorer**.

   > [!NOTE]
   > Quando você adiciona itens de um projeto que é compartilhado entre vários aplicativos, como Windows Phone ou Microsoft Store, esses itens aparecem no mapa com o projeto de aplicativo ativo no momento. Se você alterar o contexto para outro projeto de aplicativo e adicionar mais itens do projeto compartilhado, esses itens agora serão exibidos com o projeto de aplicativo recém-ativo. Operações realizadas com um item no mapa se aplicam apenas aos itens que compartilham o mesmo contexto.

3. O mapa mostra os itens selecionados dentro dos assemblies que os contêm.

   ![Itens selecionados mostrados como grupos no mapa](../modeling/media/codemapsshowitemsfromsolnexplorer.png)

4. Para explorar itens, expanda-os. Mova o ponteiro do mouse sobre um item e clique no ícone de divisa (seta para baixo) quando ele for exibido.

   ![Expandir um nó em um mapa de código](../modeling/media/dependencygraph_containment.png)

   Para expandir todos os itens, selecione-os usando **Ctrl** + **A**e, em seguida, abra o menu de atalho para o mapa e escolha **Agrupar**  >  **expandir**. No entanto, essa opção não estará disponível se a expansão de todos os grupos criar um mapa inutilizável ou problemas de memória.

5. Continue a expandir os itens nos quais você está interessado, logo abaixo do nível de classe e de membro, se necessário.

   ![Expandir grupos para nível de classe e de membro](../modeling/media/codemapsexpandtoclassandmember.png)

   Para ver os membros que estão no código, mas não aparecem no mapa, clique no ícone **rebuscar filhos** ícone ![ rebuscar filhos ](../modeling/media/dependencygraph_deletednodesicon.png) no canto superior esquerdo de um grupo.

6. Para ver mais itens relacionados àqueles no mapa, selecione um e escolha **Mostrar relacionados** na barra de ferramentas do mapa de códigos e selecione o tipo de itens relacionados a serem adicionados ao mapa. Como alternativa, selecione um ou mais itens, abra o menu de atalho e, em seguida, escolha a opção **Mostrar** para o tipo de itens relacionados a serem adicionados ao mapa. Por exemplo:

    Para um **assembly**, escolha:

    |Opção|Descrição|
    |-|-|
    |**Mostrar assemblies referenciados por este**|Adicione assemblies a que este assembly faz referência. Os assemblies externos aparecem no grupo **externa** .|
    |**Mostrar assemblies que fazem referência a este**|Adicione assemblies na solução que fazem referência a este assembly.|

    Para um **namespace**, escolha **Mostrar assembly contendo**, se não estiver visível.

    Para uma **classe** ou **interface**, escolha:

    |Opção|Descrição|
    |-|-|
    |**Mostrar Tipos Base**|Para obter uma classe, adicione a classe base e as interfaces implementadas.<br /><br /> Para obter uma interface, adicione as interfaces de base.|
    |**Mostrar Tipos Derivados**|Para obter uma classe, adicione as classes derivadas.<br /><br /> Para obter uma interface, adicione as interfaces derivadas e as classes de implementação ou structs.|
    |**Mostrar tipos referenciados por este**|Adicione todas as classes e os membros que essa classe usa.|
    |**Mostrar tipos que fazem referência a este**|Adicione todas as classes e seus membros que usam essa classe.|
    |**Mostrar namespace recipiente**|Adicione o namespace pai.|
    |**Mostrar namespace e assembly de contêiner**|Adicione a hierarquia do contêiner pai.|
    |**Mostrar todos os tipos base**|Adicione a classe base ou a hierarquia de interface recursivamente.|
    |**Mostrar todos os tipos derivados**|Para obter uma classe, adicione todas as classes derivadas recursivamente.<br /><br /> Para obter uma interface, adicione todas as interfaces derivadas e as classes de implementação ou structs recursivamente.|

     Para um **método**, escolha:

    |Opção|Descrição|
    |-|-|
    |**Mostrar métodos chamados por este**|Adicione métodos que esse método chama.|
    |**Mostrar campos referenciados por este**|Adicione campos a que este método faz referência.|
    |**Mostrar tipo recipiente**|Adicione o tipo de pai.|
    |**Mostrar tipo, namespace e assembly recipiente**|Adicione a hierarquia do contêiner pai.|
    |**Mostrar métodos substituídos**|Para obter um método que substitui outros métodos ou implementa o método de uma interface, adicione todos os métodos abstratos ou virtuais em classes base que sejam substituídas e, se houver algum, o método da interface implementado.|

     Para um **campo** ou **Propriedade**, escolha:

    |Opção|Descrição|
    |-|-|
    |**Mostrar tipo recipiente**|Adicione o tipo de pai.|
    |**Mostrar tipo, namespace e assembly recipiente**|Adicione a hierarquia do contêiner pai.|

    ![Mostrar métodos chamados por este membro](../modeling/media/codemapsshowrelatedmethods.png)

7. O mapa mostra as relações. Neste exemplo, o mapa mostra os métodos chamados pelo `Find` método e sua localização na solução ou externamente.

   ![Mostrar dependências específicas em um mapa de códigos](../modeling/media/codemapsspecificdependenciesintro.png)

8. Para simplificar o mapa e concentrar-se em partes individuais, escolha **filtros** na barra de ferramentas do mapa de códigos e selecione apenas os tipos de nós e links nos quais você está interessado. Por exemplo, desative a exibição de pastas de solução, assemblies e namespaces.

   ![Use o painel de filtro para simplificar a exibição](../modeling/media/almcodemapfilterpane.png)

## <a name="see-also"></a>Confira também

- [Vídeo: entenda o design do código com os mapas de código do Visual Studio 2015](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2015/502)
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)
- [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)
- [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
