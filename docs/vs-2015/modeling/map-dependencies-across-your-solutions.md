---
title: Mapear dependências em suas soluções | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.progression.codemap
- vs.progression.standardgraphsdialog
helpviewer_keywords:
- Visual Studio Ultimate, dependency graphs
- code exploration, dependency graphs
- dependency graphs, exporting
- code exploration, relationships
- DGML
- graph documents
- code visualization [Visual Studio ALM]
- graph documents, saving
- dependencies, visualizing
- dependency graphs, saving
- Visual Studio Ultimate, code visualization
- code, visualizing
- dependency graphs, creating
- dependency graphs
- graph documents, exporting
- code exploration, visualizing
ms.assetid: e04850a2-17c5-459b-93ec-6c74143b3292
caps.latest.revision: 245
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d70016229ad9599c7ededbefaf08744f2bb6f351
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548077"
---
# <a name="map-dependencies-across-your-solutions"></a>Mapear as dependências nas soluções
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você quiser entender as dependências em seu código, visualize-as criando mapas de código. Isso ajuda você a ver como o código se ajusta sem ler nos arquivos e linhas de código.

 ![Exibir dependências em suas soluções](../modeling/media/codemapsmainintro.png "CodeMapsMainIntro")

 **Aqui estão alguns vídeos**:

- [Entenda suas dependências de código por meio de visualização](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Understand-your-code-dependencies-through-visualization)

- [Visualizar o impacto de uma alteração](https://s.ch9.ms/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Visualize-the-impact-of-a-change)

- [Compreendendo o código complexo com mapas de código](https://channel9.msdn.com/Series/Visual-Studio-2012-Premium-and-Ultimate-Overview/Visual-Studio-Ultimate-2012-Understanding-complex-code-with-Code-Map-ENU)

## <a name="get-started-with-code-maps"></a><a name="GetStarted"></a>Introdução aos mapas de código
 **Para usar mapas de código, você precisará**de:

- Visual Studio Enterprise: crie mapas de código do editor de código, Gerenciador de Soluções, Modo de Exibição de Classe ou pesquisador de objetos.

- Visual Studio Professional: Abra mapas de código, faça edições limitadas e navegue pelo código.

> [!WARNING]
> Antes de compartilhar mapas criados em Visual Studio Enterprise com outras pessoas que usam Visual Studio Professional, certifique-se de que todos os itens no mapa (como itens ocultos, grupos expandidos e links entre grupos) sejam visíveis.

 **Você pode mapear as dependências para o código nestes idiomas**:

- Visual C# .NET ou Visual Basic .NET em uma solução ou assemblies (. dll ou. exe)

- Código C ou C++ nativo ou gerenciado em projetos do Visual C++, arquivos de cabeçalho (. h ou `#include`) ou binários

- Projetos e assemblies do X++ feitos com base nos módulos do .NET para Microsoft AX Dynamics

  **Observação:** Para projetos diferentes de C# ou Visual Basic .NET, há menos opções para iniciar um mapa de código ou adicionar itens a um mapa de código existente. Por exemplo, você não pode clicar com o botão direito do mouse em um objeto no editor de texto de um projeto C++ e adicioná-lo a um mapa de código. No entanto, você pode arrastar e soltar elementos de código individuais ou arquivos de Gerenciador de Soluções, Modo de Exibição de Classe e pesquisador de objetos.

#### <a name="to-see-the-overall-dependencies-across-your-solution"></a>Para ver as dependências gerais em sua solução

1. Abra o menu **arquitetura** .

2. Se você acabou de abrir a solução e ainda não o criou, ou se o código foi alterado desde a última vez que o criou, escolha **gerar mapa de código para solução**.

3. Se o código não tiver sido alterado desde a última vez que você o criou, escolha **gerar mapa de código para solução sem compilar** para obter um desempenho mais rápido ao criar o mapa.

4. [Consulte as dependências gerais](#SeeOverviewSource) para entender como você pode usar mapas de código para exibir as dependências gerais em toda a sua solução.

#### <a name="to-see-specific-dependencies-within-your-solution"></a>Para ver dependências específicas dentro de sua solução

1. Com sua solução carregada, abra **Gerenciador de soluções**.

2. Selecione todos os projetos, referências de assembly, pastas, arquivos, tipos ou membros que você deseja mapear.

3. Na barra de ferramentas **Gerenciador de soluções** , escolha **Mostrar no mapa de códigos**![criar novo grafo a partir do botão nós selecionados](../modeling/media/createnewgraphfromselectedbutton.gif "CreateNewGraphFromSelectedButton"). Ou abra o menu de atalho e escolha **Mostrar no mapa de códigos**. Você também pode arrastar itens de Modo de Exibição de Classe ou pesquisador de objetos para um mapa de código novo ou existente.

4. [Consulte dependências específicas](#SeeSpecificSource) para entender como você pode usar mapas de código para exibir dependências específicas dentro de sua solução.

### <a name="to-add-a-new-empty-code-map-to-your-solution"></a><a name="CreateEmptyMap"></a>Para adicionar um novo mapa de código vazio à sua solução

1. No **Gerenciador de soluções**, abra o menu de atalho para o nó de solução de nível superior. Escolha **Adicionar** e escolha **novo item**.

2. Em **instalado**, escolha **geral**.

3. No painel direito, escolha **documento gráfico direcionado** e, em seguida, escolha **Adicionar**.

     Agora você tem um mapa em branco, que aparece na pasta de **itens de solução** da solução.

#### <a name="to-create-a-new-empty-code-map-without-adding-it-to-your-solution"></a>Para criar um novo mapa de código vazio sem adicioná-lo à sua solução

1. Abra o menu **arquitetura** e escolha **novo mapa de código**.

     \- ou –

2. Abra o menu **arquivo** e escolha **novo** e, em seguida, escolha **arquivo**.

3. Em **instalado**, escolha **geral**.

4. No painel direito, escolha **documento gráfico direcionado** e, em seguida, escolha **abrir**.

     Agora você tem um mapa em branco, que não aparece nas pastas da solução.

## <a name="see-overall-dependencies"></a><a name="SeeOverviewSource"></a>Ver dependências gerais

### <a name="see-dependencies-across-your-solution"></a><a name="OverviewSource"></a>Confira dependências em sua solução

1. No menu **arquitetura** , escolha **gerar mapa de código para solução**.

    ![Gerar um comando de mapa de código](../modeling/media/codemapsarchitecturemenu.png "CodeMapsArchitectureMenu")

    Você Obtém um mapa que mostra os assemblies de nível superior e os links agregados entre eles. Quanto maior o vínculo agregado, mais dependências ele representa.

2. Use o botão **legenda** na barra de ferramentas do mapa de códigos para mostrar ou ocultar a lista de ícones de tipo de projeto (como projeto de teste, Web e telefone), itens de código (como classes, métodos e propriedades) e tipos de relação (como herda de, implementações e chamadas).

    ![Grafo de dependência de nível superior&#45;de assemblies](../modeling/media/dependencygraph-toplevelassemblies.png "DependencyGraph_TopLevelAssemblies")

    Esta solução de exemplo contém pastas de solução (**testes** e **componentes**), projetos de teste, projetos Web e assemblies. Por padrão, todas as relações de confinamento aparecem como *grupos*, que podem ser expandidas e recolhidas. O grupo **externo** contém qualquer coisa fora da sua solução, incluindo dependências de plataforma. Os assemblies externos mostram apenas os itens usados. Por padrão, os tipos de base do sistema ficam ocultos no mapa para reduzir a desordem.

3. Para fazer uma busca detalhada no mapa, expanda os grupos que representam projetos e assemblies. Você pode expandir tudo pressionando **Ctrl + a** para selecionar todos os nós e, em seguida, escolhendo **Agrupar**, **expandir** no menu de atalho.

    ![Expandindo todos os grupos em um mapa de códigos](../modeling/media/codemapsexpandallgroups.png "CodeMapsExpandAllGroups")

4. No entanto, isso pode não ser útil para uma solução grande. Na verdade, para soluções complexas, as limitações de memória podem impedi-lo de expandir todos os grupos. Em vez disso, para ver dentro de um nó individual, expanda-o. Mova o ponteiro do mouse sobre o nó e, em seguida, clique na divisa (seta para baixo) quando ela aparecer.

    ![Expandindo um nó em um mapa de código](../modeling/media/dependencygraph-containment.png "DependencyGraph_Containment")

    Ou use o teclado selecionando o item e pressionando a tecla de adição ( **+** ). Para explorar níveis mais profundos do código, faça o mesmo para namespaces, tipos e membros.

   > [!TIP]
   > Para obter mais detalhes sobre como trabalhar com mapas de código usando o mouse, o teclado e o toque, consulte [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).

5. Para simplificar o mapa e concentrar-se em partes individuais, escolha **filtros** na barra de ferramentas do mapa de códigos e selecione apenas os tipos de nós e links nos quais você está interessado. Por exemplo, você pode ocultar todos os contêineres de pasta de solução e assembly.

    ![Simplificar o mapa filtrando contêineres](../modeling/media/codemapsfilterfoldersassemblies.png "CodeMapsFilterFoldersAssemblies")

    Você também pode simplificar o mapa ocultando ou removendo grupos e itens individuais do mapa, sem afetar o código de solução subjacente.

6. Para ver as relações entre os itens, selecione-os no mapa. As cores dos links indicam os tipos de relação, conforme mostrado no painel de **legenda** .

    ![Exibir dependências em suas soluções](../modeling/media/codemapsmainintro.png "CodeMapsMainIntro")

    Neste exemplo, os links roxos são chamadas, os links pontilhados são referências e os links azuis claros são acesso ao campo. Links verdes podem ser heranças ou podem ser *links de agregação* que indicam mais de um tipo de relação (ou *categoria*).

   > [!TIP]
   > Se você vir um link verde, ele pode não significar que exista apenas uma relação de herança. Também podem ser chamadas de método, mas estão ocultas pela relação de herança. Para ver tipos específicos de links, use as caixas de seleção no painel **filtros** para ocultar os tipos nos quais você não está interessado.

7. Para obter mais informações sobre um item ou link, mova o ponteiro sobre ele até que uma dica de ferramenta seja exibida. Isso mostra detalhes de um elemento de código ou das categorias que um link representa.

    ![Mostrar as categorias de uma relação](../modeling/media/codemapsshowlinkcatgories.png "CodeMapsShowLinkCatgories")

8. Para examinar itens e dependências representados por um link de agregação, primeiro selecione o link e, em seguida, abra o menu de atalho. Escolha **Mostrar links contribuintes** (ou **Mostrar links contribuintes no novo mapa de código**). Isso expande os grupos em ambas as extremidades do link e mostra somente os itens e as dependências que participam do link.

9. Para se concentrar em partes específicas do mapa, você pode continuar a remover itens dos quais não está interessado. Por exemplo, para detalhar a exibição de classe e membro, basta filtrar todos os nós de namespace no painel **filtros** .

     ![Detalhamento para nível de classe e de membro](../modeling/media/dependencygraph-expandedselectedgroups-2012.png "DependencyGraph_ExpandedSelectedGroups_2012")

10. Outra maneira de se concentrar em um mapa de solução complexo é gerar um novo mapa que contém os itens selecionados de um mapa existente. Mantenha **Ctrl** ao selecionar os itens nos quais você deseja se concentrar, abra o menu de atalho e escolha **novo grafo na seleção**.

     ![Mostrar itens selecionados em um novo mapa de código](../ide/media/codemapsshowonnewmap.png "CodeMapsShowOnNewMap")

11. O contexto de contenção é transportado para o novo mapa. Oculte pastas de solução e quaisquer outros contêineres que você não queira ver usando o painel **filtros** .

     ![Filtrar os contêineres para simplificar a exibição](../modeling/media/codemapsexpandnewgroups.png "CodeMapsExpandNewGroups")

12. Expanda os grupos e selecione os itens no mapa para exibir as relações.

     ![Selecionar itens para exibir as relações](../modeling/media/codemapsviewnewrelationships.png "CodeMapsViewNewRelationships")

    Consulte também:

- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)

- [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)

- Encontre possíveis problemas em seu código [executando um analisador](../modeling/find-potential-problems-using-code-map-analyzers.md).

### <a name="see-dependencies-across-assemblies-or-binaries"></a><a name="OverviewCompiled"></a>Ver dependências entre assemblies ou binários

1. [Crie um mapa de código vazio](#GetStarted)ou abra um mapa de código existente (arquivo. dgml).

2. Arraste os assemblies ou os binários que você deseja mapear de fora do Visual Studio para o mapa. Por exemplo, arraste assemblies ou binários do Windows Explorer ou explorador de arquivos.

> [!NOTE]
> Você pode arrastar assemblies ou binários do Windows Explorer ou explorador de arquivos somente se estiver executando-o e o Visual Studio no mesmo nível de permissões do UAC (controle de acesso do usuário). Por exemplo, se o UAC estiver ativado e você estiver executando o Visual Studio como administrador, o Windows Explorer ou o explorador de arquivos bloqueará a operação de arrastar. Para contornar isso, verifique se ambos estão em execução com o mesmo nível de permissão ou desative o UAC.

## <a name="see-specific-dependencies"></a><a name="SeeSpecificSource"></a>Consulte dependências específicas
 Por exemplo, suponha que você tem uma revisão de código para executar em alguns arquivos com alterações pendentes. Para ver as dependências dessas alterações, você pode criar um mapa de código a partir desses arquivos.

 ![Mostrar dependências específicas em um mapa de códigos](../modeling/media/codemapsspecificdependenciesintro.png "CodeMapsSpecificDependenciesIntro")

### <a name="see-specific-dependencies-in-your-solution"></a>Consulte as dependências específicas na solução

1. Abra o **Gerenciador de Soluções**. Selecione os projetos, referências do assembly, pastas, arquivos, tipos e membros de seu interesse. Para localizar itens que tenham dependências de tipos ou membros, abra o menu de atalho tipo ou membro em **Gerenciador de soluções**. Escolha o tipo de dependência e, em seguida, selecione os resultados.

2. Mapeie seus itens e seus membros. Na barra de ferramentas **Gerenciador de soluções** , clique em **Mostrar no mapa de códigos**![criar novo grafo a partir do botão nós selecionados](../modeling/media/createnewgraphfromselectedbutton.gif "CreateNewGraphFromSelectedButton").

     ![Selecione os itens que você deseja mapear](../modeling/media/codemapsselectinsolutionexplorer.png "CodeMapsSelectInSolutionExplorer")

3. O mapa mostra os itens selecionados dentro dos assemblies que os contêm.

     ![Itens selecionados mostrados como grupos no mapa](../modeling/media/codemapsshowitemsfromsolnexplorer.png "CodeMapsShowItemsFromSolnExplorer")

     Você também pode arrastar itens de Gerenciador de Soluções, Modo de Exibição de Classe ou pesquisador de objetos para um mapa de código em branco ou existente. Para criar um mapa em branco, consulte [criar um mapa de código vazio](#GetStarted). Para incluir a hierarquia pai de seus itens, pressione e segure a tecla **Ctrl** enquanto arrasta os itens ou use o botão **incluir pais** na barra de ferramentas do mapa de códigos para especificar a ação padrão.

    > [!NOTE]
    > Quando você adicionar itens de um projeto compartilhado entre vários aplicativos, como Windows Phone ou Windows Store, esses itens são exibidos no mapa com o projeto de aplicativo ativo no momento. Se você alterar o contexto para outro projeto de aplicativo e adicionar mais itens do projeto compartilhado, esses itens agora serão exibidos com o projeto de aplicativo recém-ativo. Operações realizadas com um item no mapa se aplicam apenas aos itens que compartilham o mesmo contexto.

4. Para explorar itens, expanda-os. Mova o ponteiro do mouse sobre um item e clique no ícone de divisa (seta para baixo) quando ele for exibido.

     ![Expandindo um nó em um mapa de código](../modeling/media/dependencygraph-containment.png "DependencyGraph_Containment")

     Para expandir todos os itens, selecione-os usando **Ctrl + A**e, em seguida, abra o menu de atalho para o mapa e escolha **Agrupar**, **expanda**. No entanto, essa opção não estará disponível se a expansão de todos os grupos criar um mapa inutilizável ou problemas de memória.

5. Continue a expandir os itens nos quais você está interessado, logo abaixo do nível de classe e de membro, se necessário.

     ![Expandir grupos para nível de classe e de membro](../modeling/media/codemapsexpandtoclassandmember.png "CodeMapsExpandToClassAndMember")

     Para ver os membros que estão no código, mas não aparecem no mapa, clique no ícone **rebuscar filhos** ícone ![rebuscar filhos](../modeling/media/dependencygraph-deletednodesicon.png "DependencyGraph_DeletedNodesIcon") no canto superior esquerdo de um grupo.

6. Para ver mais itens relacionados àqueles no mapa, selecione um e escolha **Mostrar relacionados** na barra de ferramentas do mapa de códigos e selecione o tipo de itens relacionados a serem adicionados ao mapa. Como alternativa, selecione um ou mais itens, abra o menu de atalho e escolha a opção **mostrar...** opção para o tipo de itens relacionados a serem adicionados ao mapa. Por exemplo:

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

     ![Mostrar métodos chamados por este membro](../modeling/media/codemapsshowrelatedmethods.png "CodeMapsShowRelatedMethods")

7. O mapa mostra as relações. Neste exemplo, os métodos chamados pelo `Find` método e sua localização na solução ou externamente.

     ![Mostrar dependências específicas em um mapa de códigos](../modeling/media/codemapsspecificdependenciesintro.png "CodeMapsSpecificDependenciesIntro")

8. Para simplificar o mapa e concentrar-se em partes individuais, escolha **filtros** na barra de ferramentas do mapa de códigos e selecione apenas os tipos de nós e links nos quais você está interessado. Por exemplo, desative a exibição de pastas de solução, assemblies e namespaces.

     ![Use o painel de filtro para simplificar a exibição](../modeling/media/almcodemapfilterpane.png "ALMCodeMapFilterPane")

## <a name="see-dependencies-between-c-and-c-source-files-and-header-files"></a><a name="SeeSourceHeader"></a>Consulte as dependências entre arquivos de origem C e C++ e arquivos de cabeçalho
 Se você quiser criar mapas mais completos para projetos C++, defina a opção de compilador de informações de procura (**/fr**) nesses projetos. Consulte [/fr,/fr (criar. Arquivo SBR)](https://msdn.microsoft.com/library/3fd8f88b-3924-4feb-9393-287036a28896). Do contrário, uma mensagem é exibida e solicita a definição dessa opção. Se você selecionar **OK**, isso definirá a opção apenas para o mapa atual. Você pode optar por ocultar a mensagem para todos os mapas posteriores. Se você ocultar essa mensagem, poderá exibi-la novamente. Defina a seguinte chave do registro como `0` ou exclua a chave:

 **HKEY_CURRENT_USER \Software\Microsoft\VisualStudio\14.0\NativeProvider: AutoEnableSbr**

 Quando você abre uma solução que contém projetos do Visual C++, pode demorar algum tempo para atualizar o banco de dados do IntelliSense. Durante esse tempo, talvez você não consiga criar mapas de código para arquivos de cabeçalho (. h ou `#include` ) até que o banco de dados do IntelliSense termine a atualização. É possível monitorar o andamento da atualização na barra de status do Visual Studio. Para resolver problemas ou mensagens que aparecem porque determinadas configurações do IntelliSense estão desabilitadas, consulte [solucionar problemas de mapas para código C e C++](#Troubleshooting).

- Para ver as dependências entre todos os arquivos de origem e arquivos de cabeçalho em sua solução, no menu **arquitetura** , escolha **gerar grafo de arquivos de inclusão**.

     ![Grafo de dependência para código nativo](../modeling/media/dependencygraphgeneral-nativecode.png "DependencyGraphGeneral_NativeCode")

- Para ver as dependências entre os arquivos abertos atualmente, os arquivos de origem relacionados e os arquivos de cabeçalho, abra o arquivo de origem ou o arquivo de cabeçalho. Abra o menu de atalho do arquivo em qualquer lugar dentro do arquivo. Escolha **gerar grafo de arquivos de inclusão**.

     ![Primeiro&#45;grafo de dependência de nível para o arquivo. h](../modeling/media/dependencygraph-native-firstlevel.png "DependencyGraph_Native_FirstLevel")

### <a name="troubleshoot-maps-for-c-and-c-code"></a><a name="Troubleshooting"></a>Solucionar problemas de mapas para código C e C++
 Esses itens não são suportados para os códigos C e C++:

- Os tipos base não aparecem em mapas que incluem a hierarquia pai.

- A **maioria** dos itens de menu não estão disponíveis para código C e C++.

  Esses problemas podem ocorrer quando você cria mapas de código para código C e C++:

|**Problema**|**Causa possível**|**Resolução**|
|---------------|------------------------|--------------------|
|Falha ao gerar o mapa de códigos.|Nenhum projeto na solução foi compilado com êxito.|Corrija os erros de compilação que ocorreram e, em seguida, gere o mapa novamente.|
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]torna-se sem resposta quando você tenta gerar um mapa de código no menu **arquitetura** .|O arquivo de banco de dados do programa (.pdb) pode estar corrompido.<br /><br /> Um arquivo .pdb armazena informações de depuração, como o tipo, o método e as informações do arquivo de origem.|Recompile a solução e, em seguida, tente novamente.|
|Determinadas configurações do banco de dados de navegação do IntelliSense estão desabilitadas.|Determinadas configurações do IntelliSense podem ser desabilitadas na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] caixa de diálogo **Opções** .|Ative as configurações para habilitá-las.<br /><br /> Consulte [Opções, editor de texto, C/C++, avançado](../ide/reference/options-text-editor-c-cpp-advanced.md).|
|A mensagem **métodos desconhecidos** aparece em um nó de método.<br /><br /> Esse problema ocorre porque o nome do método não pode ser resolvido.|O arquivo binário não pode ter uma tabela de realocação de base.|Ative a opção **/Fixed:** no do vinculador.<br /><br /> Consulte [/Fixed (endereço base fixo)](https://msdn.microsoft.com/library/929bba5e-b7d8-40ed-943e-056aa3710fc5).|
||Talvez o arquivo de banco de dados do programa (.pdb) não tenha sido compilado.<br /><br /> Um arquivo .pdb armazena informações de depuração, como o tipo, o método e as informações do arquivo de origem.|Ative a opção **/debug** no vinculador.<br /><br /> Consulte [/debug (gerar informações de depuração)](https://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103).|
||Não é possível abrir ou encontrar o arquivo .pdb em locais esperados.|Verifique se o arquivo .pdb existe nos locais esperados.|
||As informações de depuração foram removidas do arquivo .pdb.|Se a opção **/PDBSTRIPPED** foi usada no vinculador, inclua o arquivo. pdb completo.<br /><br /> Consulte [/PDBSTRIPPED (símbolos privados de faixa)](https://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55).|
||O chamador não é uma função, e é uma conversão no arquivo binário ou um ponteiro na seção de dados.|Quando o chamador for uma conversão, tente usar `_declspec(dllimport)` para evitá-la.<br /><br /> Consulte:<br /><br /> -   [Regras e limitações gerais](https://msdn.microsoft.com/library/6c48902d-4259-4761-95d4-e421d69aa050)<br />-   [Importando chamadas de função usando __declspec (dllimport)](https://msdn.microsoft.com/library/6b53c616-0c6d-419a-8e2a-d2fff20510b3)<br />-   [dllexport, DllImport](https://msdn.microsoft.com/library/ff95b645-ef55-4e72-b848-df44657b3208)|

## <a name="make-code-maps-render-more-quickly"></a><a name="RenderMoreQuickly"></a>Fazer com que os mapas de código sejam renderizados mais rapidamente
 Quando você gera um mapa pela primeira vez, o Visual Studio indexa todas as dependências que ele encontra. Esse processo pode levar algum tempo, especialmente para soluções grandes, mas melhorará o desempenho mais tarde. Se seu código for alterado, o Visual Studio reindexará apenas o código atualizado. Para minimizar o tempo necessário para o mapa concluir a renderização, considere o seguinte:

- [Mapeie somente as dependências que lhe interessam.](#SeeSpecificSource)

- Antes de gerar o mapa para uma solução inteira, reduza o escopo da solução.

- Desative a compilação automática da solução com o botão **ignorar compilação** na barra de ferramentas do mapa de códigos.

- Desative a adição automática de itens pai com o botão **incluir pais** na barra de ferramentas do mapa de códigos.

- Edite o arquivo de mapa de código diretamente para remover nós e links desnecessários. A alteração do mapa não afeta o código subjacente. Consulte [Personalizar mapas de código editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).

  ![Ignorar os botões criar e incluir pais](../modeling/media/codemapsfilterskipbuildicons.png "CodeMapsFilterSkipBuildIcons")

  Embora o Visual Studio possa ser executado com 1 GB de memória, recomendamos que seu computador tenha pelo menos 2 GB de memória para evitar longos atrasos enquanto o Visual Studio cria o índice de código e gera o mapa.

  Pode levar mais tempo para criar mapas ou adicionar itens a um mapa de Gerenciador de Soluções quando a propriedade **copiar para o diretório de saída** de um item de projeto é definida como **copiar sempre**. Isso pode causar problemas em compilações incrementais e fazer o Visual Studio recompilar o projeto sempre. Para aumentar o desempenho, altere essa propriedade para **copiar se mais recente** ou `PreserveNewest` . Consulte [Builds incrementais](../msbuild/incremental-builds.md).

  O mapa concluído mostrará dependências somente para código criado com êxito. Se ocorrerem erros de compilação para determinados componentes, esses erros aparecerão no mapa. Certifique-se de que um componente realmente cria e tem dependências nele antes de tomar decisões arquitetônicas com base no mapa.

## <a name="share-code-maps"></a><a name="SavingExporting"></a>Compartilhar mapas de código

### <a name="share-the-map-with-other-visual-studio-users"></a>Compartilhar o mapa com outros usuários do Visual Studio
 Use o menu **arquivo** para salvar o mapa.

 -ou-

 Para salvar o mapa como parte do projeto específico, na barra de ferramentas do mapa, escolha **compartilhar**, **mover** \<*CodeMapName*> **. dgml para**e, em seguida, escolha o projeto no qual você deseja salvar o mapa.

 ![Mover um mapa para outro projeto](../modeling/media/codemapsmovemapmenu.png "CodeMapsMoveMapMenu")

 O Visual Studio salva o mapa como um arquivo. dgml que você pode compartilhar com outros usuários de Visual Studio Enterprise e Visual Studio Professional.

> [!NOTE]
> Antes de compartilhar um mapa com aqueles que usam Visual Studio Professional, certifique-se de expandir todos os grupos, mostrar nós ocultos e links entre grupos e recuperar os nós excluídos que você deseja que outras pessoas vejam no mapa. Do contrário, outros usuários não poderão consultar esses itens.
>
> O erro a seguir pode ocorrer quando você salva um mapa que está em um projeto de modelagem ou foi copiado de um projeto de modelagem para outro local:
>
> "Não é possível salvar o *nome de arquivo* fora do diretório do projeto. Itens vinculados não são compatíveis."
>
> O Visual Studio mostra o erro, mas cria a versão salva de qualquer maneira. Para evitar o erro, crie o mapa fora do projeto de modelagem. Em seguida, é possível salvá-lo no local desejado. Apenas copiar o arquivo para outro local na solução e, em seguida, tentar salvá-lo não funcionará.

### <a name="export-the-map-as-an-image-so-you-can-copy-it-into-other-applications-such-as-microsoft-word-or-powerpoint"></a>Exporte o mapa como uma imagem para que você possa copiá-lo em outros aplicativos, como o Microsoft Word ou o PowerPoint

1. Na barra de ferramentas do mapa de códigos, escolha **compartilhar**, **email como imagem** ou **copiar imagem**.

2. Cole a imagem em outro aplicativo.

### <a name="export-the-map-as-an-xps-file-so-you-can-see-it-in-xml-or-xaml-viewers-like-internet-explorer"></a>Exporte o mapa como um arquivo XPS para que você possa vê-lo em visualizadores XML ou XAML como o Internet Explorer

1. Na barra de ferramentas do mapa de códigos, escolha **compartilhar**, **email como XPS portátil** ou **salvar como XPS portátil**.

2. Navegue para onde você deseja salvar o arquivo.

3. Nomeie o mapa de código. Verifique se a caixa **salvar como tipo** está definida como **arquivos XPS ( \* . XPS)**. Selecione **Salvar**.

## <a name="what-else-can-i-do"></a>O que mais posso fazer?

- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)

- [Mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)

- [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)

- [Procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md)

- [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
