---
title: Mapear dependências nas soluções | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
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
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: 20122a1b254eee15efb557b5899e59fc914fda3a
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51740043"
---
# <a name="map-dependencies-across-your-solutions"></a>Mapear as dependências nas soluções
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Quando você quer entender dependências em seu código, exiba-os Criando mapas de código. Isso ajuda você a ver como o código se ajusta sem ler nos arquivos e linhas de código.  
  
 ![Exibir as dependências nas soluções](../modeling/media/codemapsmainintro.png "CodeMapsMainIntro")  
  
 **Aqui estão alguns vídeos**:  
  
-   [Entender as dependências do seu código por meio da visualização](http://go.microsoft.com/fwlink/?LinkID=252065)  
  
-   [Visualizar o impacto de uma alteração](http://go.microsoft.com/fwlink/?LinkID=252068)  
  
-   [Noções básicas sobre o código complexo com mapas de código](http://go.microsoft.com/fwlink/?LinkID=259869)  
  
##  <a name="GetStarted"></a> Comece com mapas de código  
 **Usar mapas de código você será necessário**:  
  
-   Visual Studio Enterprise: Crie mapas de código do editor de códigos, o Gerenciador de soluções, exibição de classe ou Pesquisador de objetos.  
  
-   Visual Studio Professional: Abrir mapas de código, criar edições limitadas e navegar pelo código.  
  
> [!WARNING]
>  Antes de compartilhar mapas criados no Visual Studio Enterprise com outras pessoas que usam o Visual Studio Professional, certifique-se de que todos os itens no mapa (como itens ocultos, grupos expandidos e links de grupo cruzado) ficam visíveis.  
  
 **Você pode mapear as dependências para o código nesses idiomas**:  
  
- Visual c# .NET ou Visual Basic .NET em uma solução ou assemblies (. dll ou .exe)  
  
- Código C ou C++ nativo ou gerenciado em projetos do Visual C++, arquivos de cabeçalho (. h ou `#include`) ou binários  
  
- Projetos e assemblies do X++ feitos com base nos módulos do .NET para Microsoft AX Dynamics  
  
  **Observação:** para projetos que não sejam c# ou Visual Basic .NET, há poucas opções para o início de um mapa de código ou adicionar itens a um mapa de código existente. Por exemplo, você não é um objeto no editor de texto de um projeto C++ com o botão direito e adicioná-lo a um mapa de código. No entanto, você pode arrastar e soltar elementos de código individuais ou arquivos de Gerenciador de soluções, exibição de classe e Pesquisador de objetos.  
  
#### <a name="to-see-the-overall-dependencies-across-your-solution"></a>Para ver as dependências gerais em sua solução  
  
1.  Abra o **arquitetura** menu.  
  
2.  Se você acabou de abrir a solução e ainda não tiver criado ou se seu código foi alterado desde a última vez que você criou, escolha **gerar mapa de código para solução**.  
  
3.  Se seu código não foi alterado desde a última vez que você o criou, escolha **gerar mapa de código para a solução sem compilação** para obter um desempenho mais rápido ao criar o mapa.  
  
4.  [Consultar dependências gerais](#SeeOverviewSource) para entender como você pode usar mapas de código para exibir as dependências gerais entre sua solução.  
  
#### <a name="to-see-specific-dependencies-within-your-solution"></a>Para ver as dependências específicas em sua solução  
  
1.  Com sua solução carregada, abra **Gerenciador de soluções**.  
  
2.  Selecione todos os de projetos, referências de assembly, pastas, arquivos, tipos ou membros que você deseja mapear.  
  
3.  No **Gerenciador de soluções** barra de ferramentas, escolha **Mostrar no mapa de códigos**![criar novo grafo de selecionado nós botão](../modeling/media/createnewgraphfromselectedbutton.gif "CreateNewGraphFromSelectedButton "). Ou abra o menu de atalho e escolha **Mostrar no mapa de códigos**. Você também pode arrastar itens da exibição de classe ou Pesquisador de objetos em um novo ou um mapa de código existente.  
  
4.  [Consulte as dependências específicas](#SeeSpecificSource) para entender como você pode usar mapas de código para exibir as dependências específicas em sua solução.  
  
###  <a name="CreateEmptyMap"></a> Para adicionar um novo mapa de código vazio à sua solução  
  
1.  Na **Gerenciador de soluções**, abra o menu de atalho do nó de solução de nível superior. Escolher **Add** , em seguida, escolha **Novo Item**.  
  
2.  Sob **Installed**, escolha **geral**.  
  
3.  No painel direito, escolha **documento gráfico direcionado** e, em seguida, escolha **Add**.  
  
     Agora você tem um mapa em branco, que aparece em sua solução **itens de solução** pasta.  
  
#### <a name="to-create-a-new-empty-code-map-without-adding-it-to-your-solution"></a>Para criar um novo mapa de código vazio sem adicioná-lo à sua solução  
  
1.  Abra o **arquitetura** menu e escolha **novo mapa de códigos**.  
  
     \- ou -  
  
2.  Abra o **arquivo** menu e escolha **New** , em seguida, escolha **arquivo**.  
  
3.  Sob **Installed**, escolha **geral**.  
  
4.  No painel direito, escolha **documento gráfico direcionado** e, em seguida, escolha **abrir**.  
  
     Agora você tem um mapa em branco, o que não aparecem nas pastas da sua solução.  
  
##  <a name="SeeOverviewSource"></a> Consultar dependências gerais  
  
###  <a name="OverviewSource"></a> Consulte as dependências em sua solução  
  
1. Sobre o **arquitetura** menu, escolha **gerar mapa de código para solução**.  
  
    ![Gerar um comando de mapa de código](../modeling/media/codemapsarchitecturemenu.png "CodeMapsArchitectureMenu")  
  
    Você obtém um mapa que mostra os assemblies de nível superior e os links agregados entre eles. Quanto maior o vínculo agregado, mais dependências ele representa.  
  
2. Use o **legenda** botão na barra de ferramentas de mapa de código para mostrar ou ocultar a lista de ícones do tipo de projeto (por exemplo, teste, Web e projeto do Phone), itens de código (como Classes, métodos e propriedades) e tipos de relação (por exemplo, herda de Implementa e chamadas).  
  
    ![Top&#45;grafo de dependência de nível de assemblies](../modeling/media/dependencygraph-toplevelassemblies.png "DependencyGraph_TopLevelAssemblies")  
  
    Essa solução de exemplo contém pastas de solução (**testes** e **componentes**), assemblies, projetos da Web e projetos de teste. Por padrão, todas as relações de confinamento pareçam *grupos*, que você pode expandir e recolher. O **Externals** grupo contém nada fora da sua solução, incluindo dependências de plataforma. Os assemblies externos mostram apenas os itens usados. Por padrão, os tipos de base do sistema estão ocultos no mapa para reduzir a desordem.  
  
3. Para fazer drill down no mapa, expanda os grupos que representam projetos e assemblies. Você pode expandir tudo pressionando **CTRL + T** para selecionar todos os nós e, em seguida, escolhendo **grupo**, **expandir** no menu de atalho.  
  
    ![Expandir todos os grupos em um mapa de códigos](../modeling/media/codemapsexpandallgroups.png "CodeMapsExpandAllGroups")  
  
4. No entanto, isso não pode ser útil para uma solução grande. Na verdade, para soluções complexas, limitações de memória podem impedir que você expandir todos os grupos. Em vez disso, para ver dentro de um nó individual, expandi-lo. Mova o ponteiro do mouse sobre o nó e, em seguida, clique na divisa (seta para baixo) quando ele for exibido.  
  
    ![Expandir um nó em um mapa de códigos](../modeling/media/dependencygraph-containment.png "DependencyGraph_Containment")  
  
    Ou use o teclado selecionando o item, em seguida, pressionar a tecla de mais (**+**). Para explorar níveis mais profundos do código, faça o mesmo para namespaces, tipos e membros.  
  
   > [!TIP]
   >  Para obter mais detalhes de como trabalhar com o código de mapas usando o mouse, teclado e toque, consulte [procurar e reorganizar mapas de código](../modeling/browse-and-rearrange-code-maps.md).  
  
5. Para simplificar o mapa e se concentrar em partes individuais, escolha **filtros** na barra de ferramentas de mapa de código e selecione apenas os tipos de nós e links que lhe interessam. Por exemplo, você pode ocultar todas as pastas de solução e Assembly recipientes.  
  
    ![Simplificar o mapa pela filtragem de recipientes](../modeling/media/codemapsfilterfoldersassemblies.png "CodeMapsFilterFoldersAssemblies")  
  
    Você também pode simplificar o mapa, ocultar ou removendo grupos individuais e itens do mapa, sem afetar o código subjacente da solução.  
  
6. Para ver as relações entre itens, selecione-os no mapa. As cores dos links indicam os tipos de relação, conforme mostrado na **legenda** painel.  
  
    ![Exibir as dependências nas soluções](../modeling/media/codemapsmainintro.png "CodeMapsMainIntro")  
  
    Neste exemplo, os links de roxos são chamadas, os links pontilhados são referências e os links de azuis claras são acesso de campo. Links de verde pode ser herança ou podem ser *agregar links* que indicam que mais de um tipo de relação (ou *categoria*).  
  
   > [!TIP]
   >  Se você vir um link verde, ele pode não significar que exista apenas uma relação de herança. Também podem ser chamadas de método, mas estão ocultas pela relação de herança. Para ver tipos específicos de links, use as caixas de seleção na **filtros** painel para ocultar os tipos que não esteja interessado em.  
  
7. Para obter mais informações sobre um item ou link, mova o ponteiro sobre ele, até que uma dica de ferramenta seja exibida. Isso mostra detalhes de um elemento de código ou as categorias que representa um link.  
  
    ![Mostrar as categorias de um relacionamento](../modeling/media/codemapsshowlinkcatgories.png "CodeMapsShowLinkCatgories")  
  
8. Para examinar itens e dependências representados por um link agregado, primeiro selecione o link e, em seguida, abra o menu de atalho. Escolher **Mostrar Links participantes** (ou **Mostrar Links participantes no novo mapa de códigos**). Isso expande os grupos em ambas as extremidades do link e mostra somente os itens e as dependências que participam no link.  
  
9. Para focalizar em partes específicas do mapa, você pode continuar a remover itens que não esteja interessado em. Por exemplo, para detalhar o modo de exibição de classe e membro, simplesmente filtrar todos os nós de namespace na **filtros** painel.  
  
     ![Busca detalhada em nível de classe e membro](../modeling/media/dependencygraph-expandedselectedgroups-2012.png "DependencyGraph_ExpandedSelectedGroups_2012")  
  
10. Outra maneira de se concentrar em um mapa de solução complexa é gerar um novo mapa que contém os itens selecionados de um mapa existente. Mantenha **CTRL** enquanto seleciona os itens que você deseja se concentrar em, abra o menu de atalho e escolha **da seleção de um novo gráfico**.  
  
     ![Mostrar itens selecionados em um novo mapa de códigos](../ide/media/codemapsshowonnewmap.png "CodeMapsShowOnNewMap")  
  
11. O contexto de recipiente é transportado para o novo mapa. Ocultar pastas de solução e quaisquer outros contêineres que você não deseja ver usando o **filtros** painel.  
  
     ![Os contêineres para simplificar a exibição de filtro](../modeling/media/codemapsexpandnewgroups.png "CodeMapsExpandNewGroups")  
  
12. Expanda os grupos e selecionar itens no mapa para exibir as relações.  
  
     ![Selecionar itens para exibir as relações](../modeling/media/codemapsviewnewrelationships.png "CodeMapsViewNewRelationships")  
  
    Confira também:   
  
-   [Procurar e reorganizar mapas de códigos](../modeling/browse-and-rearrange-code-maps.md)  
  
-   [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)  
  
-   Localizar possíveis problemas no seu código por [executando um analisador](../modeling/find-potential-problems-using-code-map-analyzers.md).  
  
###  <a name="OverviewCompiled"></a> Consulte as dependências entre assemblies ou binários  
  
1.  [Criar um mapa de código vazio](#GetStarted), ou abra um mapa de código existente (arquivo. dgml).  
  
2.  Arraste os assemblies ou binários que você deseja mapear de fora do Visual Studio para o mapa. Por exemplo, arraste assemblies ou binários do Windows Explorer ou o Explorador de arquivos.  
  
> [!NOTE]
>  Você pode arrastar assemblies ou binários do Windows Explorer ou o Explorador de arquivos somente se você estiver executando no mesmo nível de permissões de controle de acesso de usuário (UAC) ele e o Visual Studio. Por exemplo, se UAC estiver ativado e você estiver executando o Visual Studio como administrador, o Windows Explorer ou o Explorador de arquivos bloqueará a operação de arrastamento. Para resolver esse problema, certifique-se de que ambos estão em execução com o mesmo nível de permissão ou desative o UAC.  
  
##  <a name="SeeSpecificSource"></a> Consulte as dependências específicas  
 Por exemplo, suponha que você tem uma revisão de código para executar em alguns arquivos com alterações pendentes. Para ver as dependências nessas alterações, você pode criar um mapa de código dos arquivos.  
  
 ![Mostrar as dependências específicas em um mapa de código](../modeling/media/codemapsspecificdependenciesintro.png "CodeMapsSpecificDependenciesIntro")  
  
### <a name="see-specific-dependencies-in-your-solution"></a>Consulte as dependências específicas na solução  
  
1.  Abra **Gerenciador de soluções**. Selecione os projetos, referências do assembly, pastas, arquivos, tipos e membros de seu interesse. Para encontrar itens que têm dependências em tipos ou membros, abra o tipo ou o menu de atalho do membro da **Gerenciador de soluções**. Escolha o tipo de dependência e, em seguida, selecione os resultados.  
  
2.  Mapeie os itens e seus membros. No **Gerenciador de soluções** barra de ferramentas clique **Mostrar no mapa de códigos**![criar novo grafo de selecionado nós botão](../modeling/media/createnewgraphfromselectedbutton.gif "CreateNewGraphFromSelectedButton").  
  
     ![Selecione os itens que você deseja mapear](../modeling/media/codemapsselectinsolutionexplorer.png "CodeMapsSelectInSolutionExplorer")  
  
3.  O mapa mostra os itens selecionados em seus assemblies de recipientes.  
  
     ![Itens mostrados como grupos no mapa selecionados](../modeling/media/codemapsshowitemsfromsolnexplorer.png "CodeMapsShowItemsFromSolnExplorer")  
  
     Você também pode arrastar itens do Gerenciador de soluções, exibição de classe ou Pesquisador de objetos para um espaço em branco ou um mapa de código existente. Para criar um mapa em branco, consulte [criar um mapa de código vazio](#GetStarted). Para incluir a hierarquia pai para seus itens, pressione e segure a **CTRL** pressionada enquanto você arrasta itens, ou usar o **pais incluem** botão na barra de ferramentas de mapa de código para especificar a ação padrão.  
  
    > [!NOTE]
    >  Quando você adicionar itens de um projeto compartilhado entre vários aplicativos, como Windows Phone ou Windows Store, esses itens são exibidos no mapa com o projeto de aplicativo ativo no momento. Se você alterar o contexto para outro projeto de aplicativo e adicionar mais itens do projeto compartilhado, esses itens agora serão exibidos com o projeto de aplicativo recém-ativo. Operações realizadas com um item no mapa se aplicam apenas aos itens que compartilham o mesmo contexto.  
  
4.  Para explorar itens, expanda-os. Mova o ponteiro do mouse sobre um item e, em seguida, clique no ícone de divisa (seta para baixo) quando ele for exibido.  
  
     ![Expandir um nó em um mapa de códigos](../modeling/media/dependencygraph-containment.png "DependencyGraph_Containment")  
  
     Para expandir todos os itens, selecione-os usando **CTRL + T**, em seguida, abra o menu de atalho para o mapa e escolha **grupo**, **expandir**. No entanto, essa opção não estará disponível se a expansão de todos os grupos cria um mapa inutilizável ou problemas de memória.  
  
5.  Continue a expandir os itens que você está interessado, chegando até o nível de classe e membro, se necessário.  
  
     ![Expandir grupos para o nível de classe e membro](../modeling/media/codemapsexpandtoclassandmember.png "CodeMapsExpandToClassAndMember")  
  
     Para ver os membros que estão no código, mas não são exibidos no mapa, clique o **buscar novamente filhos** ícone ![buscar novamente filhos ícone](../modeling/media/dependencygraph-deletednodesicon.png "DependencyGraph_DeletedNodesIcon") na parte superior canto esquerdo de um grupo.  
  
6.  Para ver mais itens relacionados a esses no mapa, selecione um e escolha **Mostrar relacionados** na barra de ferramentas de mapa de código, selecione o tipo de itens relacionados para adicionar ao mapa. Como alternativa, selecione um ou mais itens, abra o menu de atalho e, em seguida, escolha o **Mostrar...** opção para o tipo de itens relacionados para adicionar ao mapa. Por exemplo:  
  
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
  
     ![Mostrar métodos chamados por este membro](../modeling/media/codemapsshowrelatedmethods.png "CodeMapsShowRelatedMethods")  
  
7.  O mapa mostra as relações. Neste exemplo, os métodos chamados `Find` método e sua localização na solução ou externamente.  
  
     ![Mostrar as dependências específicas em um mapa de código](../modeling/media/codemapsspecificdependenciesintro.png "CodeMapsSpecificDependenciesIntro")  
  
8.  Para simplificar o mapa e se concentrar em partes individuais, escolha **filtros** na barra de ferramentas de mapa de código e selecione apenas os tipos de nós e links que lhe interessam. Por exemplo, desative a exibição de pastas de solução, Assemblies e Namespaces.  
  
     ![Use o painel de filtro para simplificar a exibição](../modeling/media/almcodemapfilterpane.png "ALMCodeMapFilterPane")  
  
##  <a name="SeeSourceHeader"></a> Ver as dependências entre arquivos de código-fonte C e C++ e arquivos de cabeçalho  
 Se você quiser criar mapas mais completos para projetos do C++, defina a opção de compilador de informações de procura (**/FR**) nesses projetos. Consulte [/FR, /Fr (criar. Arquivo SBR)](http://msdn.microsoft.com/library/3fd8f88b-3924-4feb-9393-287036a28896). Do contrário, uma mensagem é exibida e solicita a definição dessa opção. Se você selecionar **Okey**, isso define a opção para o map atual. Você pode optar por ocultar a mensagem para todos os mapas posteriores. Se você ocultar essa mensagem, poderá exibi-la novamente. Defina a seguinte chave do registro `0` ou exclua a chave:  
  
 **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\14.0\NativeProvider: AutoEnableSbr**  
  
 Quando você abre uma solução que contém projetos do Visual C++, pode demorar algum tempo para atualizar o banco de dados do IntelliSense. Durante esse tempo, talvez você não conseguir criar mapas de código para o cabeçalho (. h ou `#include`) até que o banco de dados do IntelliSense conclui a atualização de arquivos. É possível monitorar o andamento da atualização na barra de status do Visual Studio. Para resolver problemas ou mensagens exibidas porque determinadas configurações do IntelliSense estão desabilitadas, consulte [solucionar problemas de mapas de código C e C++](#Troubleshooting).  
  
-   Para ver as dependências entre todos os arquivos de origem e arquivos de cabeçalho em sua solução, nos **arquitetura** menu, escolha **gerar grafo de arquivos de inclusão**.  
  
     ![Gráfico de dependência para código nativo](../modeling/media/dependencygraphgeneral-nativecode.png "DependencyGraphGeneral_NativeCode")  
  
-   Para ver as dependências entre os arquivos abertos atualmente, os arquivos de origem relacionados e os arquivos de cabeçalho, abra o arquivo de origem ou o arquivo de cabeçalho. Abra o menu de atalho do arquivo em qualquer lugar dentro do arquivo. Escolher **gerar grafo de arquivos de inclusão**.  
  
     ![Primeiro&#45;gráfico de dependência de nível de arquivo. h](../modeling/media/dependencygraph-native-firstlevel.png "DependencyGraph_Native_FirstLevel")  
  
###  <a name="Troubleshooting"></a> Solucionar problemas de mapas de código C e C++  
 Esses itens não são suportados para os códigos C e C++:  
  
- Tipos de base não são exibidos em mapas que incluem a hierarquia pai.  
  
- A maioria dos **Mostrar** itens de menu não estão disponíveis para código C e C++.  
  
  Esses problemas podem ocorrer quando você cria mapas de código para código C e C++:  
  
|**Problema**|**Possível causa**|**Resolução**|  
|---------------|------------------------|--------------------|  
|O mapa de código falha ao gerar.|Nenhum projeto na solução foi compilado com êxito.|Corrija os erros de compilação que ocorreram e, em seguida, gere novamente o mapa.|  
|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] se torna sem resposta quando você tenta gerar um mapa de códigos do **arquitetura** menu.|O arquivo de banco de dados do programa (.pdb) pode estar corrompido.<br /><br /> Um arquivo .pdb armazena informações de depuração, como o tipo, o método e as informações do arquivo de origem.|Recompile a solução e, em seguida, tente novamente.|  
|Determinadas configurações do banco de dados de navegação do IntelliSense estão desabilitadas.|Determinadas configurações do IntelliSense podem ser desabilitadas na [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **opções** caixa de diálogo.|Ative as configurações para habilitá-las.<br /><br /> Ver [opções, Editor de texto, C/C++, avançado](../ide/reference/options-text-editor-c-cpp-advanced.md).|  
|A mensagem **métodos desconhecidos** aparece em um nó de método.<br /><br /> Esse problema ocorre porque o nome do método não pode ser resolvido.|O arquivo binário não pode ter uma tabela de realocação de base.|Ativar o **/fixed: no** opção no vinculador.<br /><br /> Ver [/FIXED (endereço básico fixo)](http://msdn.microsoft.com/library/929bba5e-b7d8-40ed-943e-056aa3710fc5).|  
||Talvez o arquivo de banco de dados do programa (.pdb) não tenha sido compilado.<br /><br /> Um arquivo .pdb armazena informações de depuração, como o tipo, o método e as informações do arquivo de origem.|Ativar o **/Debug** opção no vinculador.<br /><br /> Ver [/Debug (gerar informações de depuração)](http://msdn.microsoft.com/library/1af389ae-3f8b-4d76-a087-1cdf861e9103).|  
||Não é possível abrir ou encontrar o arquivo .pdb em locais esperados.|Verifique se o arquivo .pdb existe nos locais esperados.|  
||As informações de depuração foram removidas do arquivo .pdb.|Se o **/PDBSTRIPPED** opção foi usada no vinculador, inclua o arquivo. PDB completo em vez disso.<br /><br /> Ver [/PDBSTRIPPED (remover símbolos privados)](http://msdn.microsoft.com/library/9b9e0070-6a13-4142-8180-19c003fbbd55).|  
||O chamador não é uma função, e é uma conversão no arquivo binário ou um ponteiro na seção de dados.|Quando o chamador for uma conversão, tente usar `_declspec(dllimport)` para evitá-la.<br /><br /> Consulte:<br /><br /> -   [Regras e limitações gerais](http://msdn.microsoft.com/library/6c48902d-4259-4761-95d4-e421d69aa050)<br />-   [Importando chamadas de função usando __declspec(dllimport)](http://msdn.microsoft.com/library/6b53c616-0c6d-419a-8e2a-d2fff20510b3)<br />-   [dllexport, dllimport](http://msdn.microsoft.com/library/ff95b645-ef55-4e72-b848-df44657b3208)|  
  
##  <a name="RenderMoreQuickly"></a> Tornar o código mapas renderizam mais rapidamente  
 Quando você gera um mapa pela primeira vez, o Visual Studio indexa todas as dependências que encontra. Esse processo pode levar algum tempo, especialmente para grandes soluções, mas melhorará o desempenho mais tarde. Se seu código for alterado, o Visual Studio indexa novamente o código atualizado. Para minimizar o tempo necessário para o mapa concluir a renderização, considere o seguinte:  
  
- [Mapear as dependências que lhe interessam.](#SeeSpecificSource)  
  
- Antes de gerar o mapa para uma solução inteira, reduza o escopo da solução.  
  
- Desativar a compilação automática para a solução com o **Skip Build** na barra de ferramentas de mapa de código.  
  
- Desativar a adição automática de itens pai com o **pais incluem** na barra de ferramentas de mapa de código.  
  
- Edite o arquivo de mapa de código diretamente para remover os nós e links que você não precisa. Alterar o mapeamento não afeta o código subjacente. Consulte [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).  
  
  ![Botões de Skip Build e incluir pais](../modeling/media/codemapsfilterskipbuildicons.png "CodeMapsFilterSkipBuildIcons")  
  
  Embora o Visual Studio pode ser executado com 1 GB de memória, é recomendável que o computador tenha pelo menos 2 GB de memória para evitar longos atrasos enquanto o Visual Studio cria o índice de código e gera o mapa.  
  
  Pode levar mais tempo para criar mapas ou adicionar itens a um mapa no Gerenciador de soluções quando um item de projeto **Copy to Output Directory** estiver definida como **copiar sempre**. Isso pode causar problemas em compilações incrementais e fazer o Visual Studio recompilar o projeto sempre. Para aumentar o desempenho, altere essa propriedade para **copiar se mais recente** ou `PreserveNewest`. Ver [compilações incrementais](../msbuild/incremental-builds.md).  
  
  O mapa concluído mostrará dependências apenas para códigos criados com êxito. Se ocorrerem erros de compilação para determinados componentes, esses erros são exibidos no mapa. Certifique-se de que um componente é efetivamente compilado e tem dependências nele antes de tomar decisões arquitetônicas com base no mapa.  
  
##  <a name="SavingExporting"></a> Compartilhar mapas de código  
  
### <a name="share-the-map-with-other-visual-studio-users"></a>Compartilhar o mapa com outros usuários do Visual Studio  
 Use o **arquivo** menu para salvar o mapa.  
  
 -ou-  
  
 Para salvar o mapa como parte do projeto específico, na barra de ferramentas do mapa, escolha **compartilhamento**, **mover** \< *CodeMapName*>**. dgml em**e, em seguida, escolha o projeto onde você deseja salvar o mapa.  
  
 ![Mover um mapa em outro projeto](../modeling/media/codemapsmovemapmenu.png "CodeMapsMoveMapMenu")  
  
 O Visual Studio salva o mapa como um arquivo. dgml que você pode compartilhar com outros usuários do Visual Studio Enterprise e Professional do Visual Studio.  
  
> [!NOTE]
>  Antes de compartilhar um mapa com aqueles que usam o Visual Studio Professional, certifique-se expandir todos os grupos, Mostrar nós ocultos e links de grupo cruzado e recuperar todos os nós excluídos que você deseja que outras pessoas vejam no seu mapa. Do contrário, outros usuários não poderão consultar esses itens.  
>   
>  O seguinte erro poderá ocorrer quando você salva um mapa que está em um projeto de modelagem ou foi copiado de um projeto de modelagem para outro local:  
>   
>  "Não é possível salvar *fileName* fora do diretório do projeto. Itens vinculados não são compatíveis."  
>   
>  O Visual Studio mostra o erro, mas cria a versão salva de qualquer maneira. Para evitar o erro, crie o mapa fora do projeto de modelagem. Em seguida, é possível salvá-lo no local desejado. Apenas copiar o arquivo para outro local na solução e, em seguida, tentar salvá-lo não funcionará.  
  
### <a name="export-the-map-as-an-image-so-you-can-copy-it-into-other-applications-such-as-microsoft-word-or-powerpoint"></a>Exportar o mapa como uma imagem, de forma que você pode copiá-lo para outros aplicativos, como Microsoft Word ou PowerPoint  
  
1.  Na barra de ferramentas de mapa de código, escolha **compartilhamento**, **Email como imagem** ou **Copiar imagem**.  
  
2.  Cole a imagem em outro aplicativo.  
  
### <a name="export-the-map-as-an-xps-file-so-you-can-see-it-in-xml-or-xaml-viewers-like-internet-explorer"></a>Exportar o mapa como um arquivo XPS, portanto, você pode vê-lo em visualizadores XML ou XAML como o Internet Explorer  
  
1.  Na barra de ferramentas de mapa de código, escolha **compartilhamento**, **Email como XPS portátil** ou **Salvar como XPS portátil**.  
  
2.  Navegue para onde você deseja salvar o arquivo.  
  
3.  Nome do mapa de código. Certifique-se de que o **Salvar como tipo** caixa é definida como **arquivos XPS (\*. XPS)**. Escolher **salvar**.  
  
## <a name="what-else-can-i-do"></a>O que mais posso fazer?  
  
-   [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)  
  
-   [Mapear métodos na pilha de chamadas ao depurar](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)  
  
-   [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)  
  
-   [Procurar e reorganizar mapas de códigos](../modeling/browse-and-rearrange-code-maps.md)  
  
-   [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)



