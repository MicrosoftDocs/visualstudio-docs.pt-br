---
title: Procurar e reorganizar mapas de código
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.progression.dgmlgraph.layouthelp
- vs.progression.graphdocument
- vs.progression.dgmlgraph.message.notUlt.noexpandgroup
- vs.progression.colorsetpicker
- vs.progression.iconsetpicker
helpviewer_keywords:
- Visual Studio Ultimate, dependency graphs
- code visualization [Visual Studio ALM]
- graph documents, browsing
- Visual Studio ALM, dependency graphs
- code visualization
- Visual Studio ALM, graph documents
- Visual Studio Ultimate, graph documents
- dependency graphs, browsing
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2683ec839d8eae41d3f4ab59112a31ba6d893848
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85541968"
---
# <a name="browse-and-rearrange-code-maps"></a>Procurar e reorganizar mapas de código

Reorganize os itens em mapas de código para torná-los mais fáceis de ler e melhorar seu desempenho.

Você pode personalizar mapas de código sem afetar o código subjacente em uma solução. Isso é útil quando você deseja se concentrar em elementos de código-chave ou comunicar ideias sobre o código. Por exemplo, para realçar áreas interessantes, você pode selecionar elementos de código no mapa e filtrá-los, alterar o estilo de elementos de código e links, ocultar ou excluir elementos de código e organizar elementos de código usando propriedades, categorias ou grupos.

 **Requisitos**

- Para criar mapas de código, você deve ter Visual Studio Enterprise.

- Você pode exibir mapas de código e fazer edições limitadas para mapas de código em Visual Studio Professional.

## <a name="get-started-working-with-code-maps"></a><a name="ManageLargeGraphs"></a>Introdução ao trabalho com mapas de código

Crie um mapa de código (Confira [dependências de mapa em suas soluções](../modeling/map-dependencies-across-your-solutions.md) para obter mais detalhes). Se você não quiser aguardar a geração do mapa terminar, clique no link **Cancelar** a qualquer momento para interromper o processo de geração. No entanto, você não verá os detalhes de todas as dependências e links se fizer isso.

Depois de gerar o mapa, comece com estas dicas para examinar seu código:

- Examine os clusters de dependência natural no código. Na barra de ferramentas do mapa, escolha o **layout**, botão clusters rápidos de **clusters** ![ na barra de ferramentas do grafo ](../modeling/media/quickclustersicon.gif) . Consulte [alterar o layout do mapa](#Selecting).

     ![Gráfico de dependência &#45; layout de clusters rápidos](../modeling/media/dependencygraph_quickclusters.png)

- Organize o mapa em áreas menores agrupando nós relacionados. Recolha esses grupos para ver apenas as dependências entre os grupos, que aparecem automaticamente. Consulte [nós de grupo](#OrganizeGroups).

- Use filtros para simplificar o mapa e concentrar-se nos tipos de nós ou links nos quais você está interessado. Consulte [Filtrar nós e links](#FilterNodes).

- Maximize o desempenho de mapas grandes. Consulte [mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md) para obter mais informações. Por exemplo, ative **ignorar compilação** na barra de ferramentas do mapa para que o Visual Studio não reconstrua sua solução quando você atualizar itens no mapa.

## <a name="change-the-map-layout"></a><a name="Selecting"></a>Alterar o layout do mapa

|**Para**|**Realizar estas etapas**|
|-|-|
|Organize o fluxo de dependência para todo o mapa em uma direção específica. Isso pode ajudá-lo a ver camadas arquitetônicas no código.|Na barra de ferramentas do mapa, escolha **layout**e, em seguida:<br /><br /> -   **De cima para baixo** ![ Botão de cima para baixo do gráfico](../modeling/media/topbottomgraphbutton.gif)<br />-   **De baixo para cima** ![ Botão do gráfico de baixo para cima](../modeling/media/bottomtopgraphbutton.gif)<br />-   Da **esquerda para a direita** ![ Botão de layout da esquerda para a direita](../modeling/media/leftrightgraphbutton.gif)<br />-   Da **direita para a esquerda** ![ Botão de gráfico da direita para a esquerda](../modeling/media/rightleftgraphbutton.gif)|
|Consulte clusters de dependência natural no código com os nós mais dependentes no centro dos clusters e os nós menos dependentes, fora desses clusters.|Na barra de ferramentas do mapa, escolha **layout**e, **em seguida,** o botão clusters rápidos ![ na barra de ferramentas do grafo ](../modeling/media/quickclustersicon.gif) .|
|Selecione um ou mais nós no mapa.|Clique em um nó para selecioná-lo. Para selecionar ou desmarcar mais de um nó, mantenha **Ctrl** ao clicar.<br /><br /> Teclado: pressione **Tab** ou use as teclas de direção para mover o retângulo de foco pontilhado para um nó e pressione **espaço** para selecioná-lo. Pressione **Ctrl**  +  **espaço** para selecionar vários nós ou desmarcar.|
|Mova os nós específicos pelo mapa.|Arraste os nós para movê-los. Para mover outros nós e links para fora do caminho enquanto arrasta os nós, pressione e segure a tecla **Shift** .<br /><br /> Teclado: Mantenha **Ctrl** pressionado e pressione as teclas de direção.|
|Altere o layout dentro de um grupo independentemente dos outros nós e grupos no mapa.|Selecione um nó e abra o menu de atalho. Escolha **layout** e selecione um estilo de layout.<br /><br /> - ou -<br /><br /> Selecione um nó e expanda-o para mostrar os nós filho. Clique no título do nó para mostrar a barra de ferramentas pop-up de grupo e abra a barra de ferramentas **alterar o estilo de layout do grafo de dependência de grupo** ![ &#45; grupo &#45; lista de layouts ](../modeling/media/dependencygraph_grouptoolbar.gif) . Selecione um dos layouts de árvore, **clusters rápidos**ou **modo de exibição de lista** (que organiza o conteúdo do grupo em uma lista).<br /><br /> Consulte [nós de grupo](#OrganizeGroups) para obter mais detalhes.|
|Desfaz uma ação no mapa.|Pressione **Ctrl**  +  **Z** ou use o comando **desfazer** do Visual Studio.|

## <a name="browse-the-map"></a><a name="Explore"></a>Procurar o mapa

|**Para**|**Realizar estas etapas**|
|-|-|
|Examine o mapa.|Arraste o mapa em qualquer direção usando o mouse.<br /><br /> - ou -<br /><br /> Mantenha **Shift** e gire a roda do mouse para rolar horizontalmente. Mantenha a **tecla Shift**pressionada  +  **CTRL** e gire a roda do mouse para rolar horizontalmente.|
|Ampliar ou reduzir o mapa.|Gire a roda do mouse.<br /><br /> - ou -<br /><br /> Use a lista suspensa **zoom** na barra de ferramentas do mapa de códigos.<br /><br /> - ou -<br /><br /> Use os atalhos de teclado. Para ampliar, pressione **Ctrl + Shift +.** (ponto). Para reduzir, pressione **Ctrl + Shift +,** (vírgula).|
|Ampliar uma área específica usando o mouse.|Mantenha o botão direito do mouse enquanto desenha um retângulo em volta da área em que você está interessado.|
|Redimensione e ajuste o mapa em sua janela.|Escolha **zoom para caber** na lista **zoom** na barra de ferramentas do mapa de códigos.<br /><br /> - ou -<br /><br /> Clique no ícone Zoom **para ajustar** o ![ ícone de zoom na barra de ferramentas do mapa ](../modeling/media/almcodemapzoomicon.png) na barra de ferramentas do mapa de códigos. Teclado: pressione **Ctrl + 0** (zero).|
|Localize um nó no mapa por seu nome. **Dica:**  Isso funciona apenas para itens no mapa. Para localizar itens em sua solução, mas não no mapa, encontre-os em **Gerenciador de soluções**e arraste-os para o mapa. (Arraste sua seleção ou, na barra de ferramentas **Gerenciador de soluções** , clique em **Mostrar no mapa de códigos**).|1. **escolha o ícone encontrar ícone** ![ Localizar na barra de ferramentas do mapa ](../modeling/media/almcodemapfindicon.png) na barra de ferramentas do mapa de códigos (teclado: pressione **Ctrl + F**) para mostrar a caixa de pesquisa no canto superior direito do mapa.<br />2. Digite o nome do item e pressione **retornar** ou clique no ícone de "lupa". O primeiro item que corresponde à sua pesquisa aparece selecionado no mapa.<br />3. para personalizar sua pesquisa, abra a lista suspensa e escolha uma opção de pesquisa. As opções são **Localizar próximo**, **Localizar anterior**e **selecionar tudo**. Em seguida, clique no botão correspondente ao lado da caixa de texto Pesquisar.<br />     ![Lista suspensa de opções de pesquisa&#45;](../modeling/media/almcodemapssearchdropdown.png)<br />     Como alternativa, use o teclado: pressione **F3** para selecionar o próximo nó correspondente ou **Shift + F3** para selecionar o nó correspondente anterior.<br />4. Selecione qualquer uma das opções que especificam como os termos de pesquisa são manipulados clicando nos ícones abaixo da caixa de texto de pesquisa.<br />     ![Opções de correspondência de pesquisa](../modeling/media/almcodemapssearchmatchicons.png)<br />     As opções são, da esquerda para a direita, correspondência com distinção de maiúsculas e minúsculas, somente palavras inteiras, usar a sintaxe de expressão regular do .NET, expandir automaticamente os grupos para mostrar correspondências a itens incluídos. **Importante:**  Você poderá usar a caixa de pesquisa para localizar correspondências em grupos recolhidos somente se esses grupos tiverem sido expandidos anteriormente. Para localizar essas correspondências e expandir seus grupos pai automaticamente, escolha essa opção na caixa de pesquisa.|
|Selecione todos os nós não selecionados.|Abra o menu de atalho para os nós selecionados. Escolha **selecionar**e **inverter seleção**.|
|Selecione nós adicionais que se vinculam aos selecionados.|Abra o menu de atalho para os nós selecionados. Escolha **selecionar** e um destes:<br /><br /> -Para selecionar nós adicionais que se vinculam diretamente ao nó selecionado, escolha **dependências de entrada**.<br />-Para selecionar nós adicionais que se vinculam diretamente do nó selecionado, escolha **dependências de saída**.<br />-Para selecionar nós adicionais que se vinculam diretamente a e do nó selecionado, escolha **ambos**.<br />-Para selecionar todos os nós vinculados a e do nó selecionado, escolha **subgrafo conectado**.<br />-Para selecionar todos os filhos do nó selecionado, escolha **filhos**.|

## <a name="filter-nodes-and-links"></a><a name="FilterNodes"></a>Filtrar nós e links

|**Para**|**Realizar estas etapas**|
|-|-|
|Mostrar ou ocultar o painel filtros.|Escolha o botão **filtros** na barra de ferramentas do mapa de códigos. O painel **filtros** é exibido como uma página com guias no **Gerenciador de soluções**, por padrão.|
|Filtre os tipos de nós mostrados no mapa.|Defina ou desmarque as caixas de seleção na lista **elementos de código** no painel filtros.|
|Filtre os tipos de links que são mostrados no mapa.|Defina ou desmarque as caixas de seleção na lista **relações** no painel filtros.|
|Mostrar ou ocultar nós de projeto de teste no mapa.|Defina ou desmarque a caixa de seleção **ativos de teste** na lista **diversos** no painel filtros.|

Os ícones mostrados no painel de legenda do mapa refletem as configurações feitas na lista. Para mostrar ou ocultar o painel Legenda, clique no botão **legenda** na barra de ferramentas do mapa de códigos.

## <a name="examine-nodes-and-links"></a><a name="Inspect"></a>Examinar nós e links

Os mapas de código mostram estes tipos de links:

- Um link individual representa uma única relação entre dois nós.

- Um link entre grupos representa uma relação entre dois nós em grupos diferentes.

- Um link de agregação representa todas as relações que apontam na mesma direção entre dois grupos.

> [!TIP]
> Por padrão, o mapa mostra links entre grupos somente para os nós selecionados. Para alterar esse comportamento para mostrar ou ocultar links agregados entre grupos, clique em **layout** na barra de ferramentas do mapa de códigos e escolha **avançado**e, em seguida, **Mostrar todos os links entre** grupos ou **ocultar todos os links entre grupos**. Consulte [ocultar ou mostrar nós e links](#HidingShowing) para obter mais detalhes.

|**Para**|**Realizar estas etapas**|
|-|-|
|Veja mais informações sobre um nó ou um link.|Mova o ponteiro do mouse sobre o nó ou o link até que uma dica de ferramenta seja exibida.<br /><br /> A dica de ferramenta para um link agregado lista as dependências individuais que ela representa.<br /><br /> - ou -<br /><br /> Abra o menu de atalho para o nó ou o link. Escolha **Editar**, **Propriedades**.|
|Mostrar ou ocultar o conteúdo de um grupo.|-Para expandir um grupo, abra o menu de atalho para o nó e escolha **Agrupar**, **expanda**.<br />     - ou -<br />     Mova o ponteiro do mouse sobre a parte superior do nó até que o botão de divisa (seta para baixo) seja exibido. Clique neste botão para expandir o grupo. Teclado: para expandir ou recolher o grupo selecionado, pressione a tecla de **adição** ( **+** ) ou a tecla **menos** ( **-** ).<br />-Para recolher um grupo, abra o menu de atalho do nó e escolha **Agrupar**, **recolher**.<br />     - ou -<br />     Mova o ponteiro do mouse sobre o início de um grupo até que o botão de divisa (seta para cima) seja exibido. Clique neste botão para recolher o grupo.<br />-Para expandir todos os grupos, pressione **Ctrl**  +  **a** para selecionar todos os nós. Abra o menu de atalho para o mapa e escolha **Agrupar**, **expanda**. **Observação:**      Esse comando não estará disponível se a expansão de todos os grupos gerar um mapeamento inutilizável ou problemas de memória. É recomendável que você expanda o mapa somente para o nível de detalhe sobre o qual você se preocupa.<br />-Para recolher todos os grupos, abra o menu de atalho para um nó ou para o mapa. Escolha **grupo**, **recolher tudo**.|
|Consulte a definição de código para um namespace, tipo ou membro.|Abra o menu de atalho para o nó e escolha **ir para definição**.<br /><br /> -ou-<br /><br /> Clique duas vezes no nó. Para grupos expandidos, clique duas vezes no cabeçalho do grupo.<br /><br /> -ou-<br /><br /> Selecione o nó e pressione **F12**.<br /><br /> Por exemplo:<br /><br /> -Para um namespace que contém uma classe, o arquivo de código para a classe é aberto para mostrar a definição dessa classe. Em outros casos, a janela **Localizar resultados de símbolo** mostra uma lista de arquivos de código. **Observação:**      Quando você executa essa tarefa em um namespace Visual Basic, o arquivo de código por trás do namespace não abre. Esse problema também ocorre quando você executa essa tarefa em um grupo de nós selecionados que incluem um namespace Visual Basic. Para contornar esse problema, navegue manualmente até o arquivo de código por trás do namespace ou omita o nó do namespace da sua seleção.<br />-Para uma classe ou uma classe parcial, o arquivo de código para essa classe é aberto para mostrar a definição de classe.<br />-Para um método, o arquivo de código para a classe pai é aberto para mostrar a definição do método.|
|Examine as dependências e os itens que participam de um link de agregação.|Selecione os links nos quais você está interessado e abra o menu de atalho para sua seleção. Escolha **Mostrar links contribuintes** ou **Mostrar links contribuintes no novo mapa de código**.<br /><br /> O Visual Studio expande os grupos em ambas as extremidades do link e mostra apenas esses itens e dependências que participam do link. **Observação:**  Ao examinar as dependências entre os itens em grupos parciais, você poderá ver esse comportamento: <ul><li>Os links para itens que não participam de seu exame desaparecem do mapa, embora esses links ainda existam.</li><li>Suponha que você examine um link para um item em um grupo parcial e, posteriormente, examine um link diferente para o mesmo item. Durante o segundo exame, o grupo de destino parcial mostra apenas os itens de seu primeiro exame. Os links e itens de destino que não participaram de seu primeiro exame, mas que participam do segundo exame não aparecem.</li></ul> Para ver os itens ausentes de um grupo, escolha o ícone de **rebusca de filhos** ![ rebuscar filhos ](../modeling/media/dependencygraph_deletednodesicon.png) (que indica que nem todos os membros de um grupo aparecem no mapa). Você também pode tentar desfazer suas ações (teclado: pressione **Ctrl + Z**) e examine as dependências em um novo mapa.|
|Examine as dependências em vários nós em grupos diferentes.|Expanda os grupos para que você possa ver todos os seus filhos. Selecione todos os nós que lhe interessam, incluindo seus filhos. O mapa mostra os links entre grupos entre os nós selecionados.<br /><br /> Para selecionar todos os nós em um grupo, pressione e mantenha pressionada a **tecla Shift** e o botão esquerdo do mouse enquanto desenha um retângulo em volta desse grupo. Para selecionar todos os nós em um mapa, pressione **Ctrl** + **a**. **Dica:**  Para mostrar os links entre grupos em todos os momentos, escolha **layout** na barra de ferramentas do mapa, **avançado**, **Mostrar todos os links entre grupos**.|
|Consulte os itens referenciados por um nó ou link.|Abra o menu de atalho para o nó e escolha **Localizar todas as referências**. **Observação:**  Isso se aplica somente quando o `Reference` atributo é definido para o nó ou link no arquivo. dgml do mapa. Para adicionar referências a itens de nós ou links, consulte [Personalizar mapas de código editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).|

## <a name="hide-or-show-nodes-and-links"></a><a name="HidingShowing"></a>Ocultar ou mostrar nós e links

Ocultar nós os impede de participar de algoritmos de layout. Por padrão, links de grupo cruzado permanecem ocultos. Links de grupo cruzado são links individuais que conectam nós entre os grupos. Quando os grupos são recolhidos, o mapa agrega todos os links entre grupos em links únicos entre grupos. Quando você expande um grupo e seleciona nós dentro do grupo, os links de grupo cruzado são exibidos e mostram as dependências nesse grupo.

> [!CAUTION]
> Antes de compartilhar um mapa criado em Visual Studio Enterprise com aqueles que usam Visual Studio Professional, certifique-se de reexibir os nós ou links entre grupos que você deseja que outras pessoas vejam. Do contrário, os usuários não poderão reexibir esses itens.

### <a name="to-hide-or-show-nodes"></a>Para ocultar ou mostrar nós

|**Para**|**Realizar estas etapas**|
|-|-|
|Ocultar nós selecionados.|1. Selecione os nós que você deseja ocultar.<br />2. Abra o menu de atalho para os nós selecionados ou para o mapa. Escolha **selecionar**, **ocultar selecionado**.|
|Ocultar nós não selecionados.|1. Selecione os nós que você deseja que permaneçam visíveis.<br />2. Abra o menu de atalho para os nós selecionados ou para o mapa. Escolha **selecionar**, **ocultar desmarcado**.|
|Mostrar nós ocultos.|-Para mostrar todos os nós ocultos dentro de um grupo, primeiro verifique se o grupo está expandido. Abra o menu de atalho e escolha **selecionar**, **Reexibir filhos**.<br />     - ou -<br />     Clique no ícone **Reexibir filhos**para ![ Reexibir filhos ](../modeling/media/dependencygraph_filtericon_hiddennodes.gif) no canto superior esquerdo do grupo (isso só é visível quando há nós filho ocultos).<br />-Para mostrar todos os nós ocultos, abra o menu de atalho para o mapa ou um nó e escolha **selecionar**, **Reexibir tudo**.|

### <a name="to-hide-or-show-links"></a>Para ocultar ou mostrar links

|**Para**|**Na barra de ferramentas do mapa, escolha layout, avançado e, em seguida, escolha**|
|-|-|
|Mostrar links entre grupos em todos os momentos.|**Mostrar todos os links entre grupos**. Isso oculta links agregados entre grupos.|
|Oculte os links entre grupos em todos os momentos.|**Ocultar todos os links entre grupos**|
|Mostrar somente links entre grupos para os nós selecionados.|**Mostrar Links de Grupo Cruzado em Nós Selecionados**|
|Ocultar todos os links.|**Ocultar todos os links**. Para mostrar os links novamente, escolha uma das opções listadas acima.|

## <a name="group-nodes"></a><a name="OrganizeGroups"></a>Nós de grupo

|**Para**|**Realizar estas etapas**|
|-|-|
|Mostrar nós de contêiner como nós de grupo ou nós folha.|Para mostrar nós de contêiner como nós folha: selecione os nós, abra o menu de atalho para sua seleção e escolha **Agrupar**, **converter em folha**.<br /><br /> Para mostrar nós de contêiner como nós de Grupo: selecione os nós, abra o menu de atalho para sua seleção e escolha **Agrupar**, **converter em grupo**.|
|Alterar o layout dentro de um grupo.|Selecione o grupo, abra o menu de atalho, escolha **layout**e selecione o estilo de layout desejado.<br /><br /> - ou -<br /><br /> 1. Selecione o grupo e verifique se ele está expandido.<br />2. Clique no cabeçalho do grupo novamente e a barra de ferramentas do grupo será exibida.<br />     ![Barra de ferramentas de &#45; grupo de gráficos de dependência](../modeling/media/dependencygraph_group.png)<br />3. Abra o gráfico **de dependência alterar o estilo do layout da lista de grupos** ![ &#45; barra de ferramentas do grupo &#45; layout ](../modeling/media/dependencygraph_grouptoolbar.gif) e escolha o estilo de layout desejado.<br /><br /> A **exibição de lista** reorganiza os membros do grupo na lista. O **grafo padrão** redefine o layout do grupo para o layout padrão do mapa. Para outras opções, consulte [alterar o layout do mapa](#Selecting).|
|Adicione um nó a um grupo.|Arraste o nó para o grupo.<br /><br /> Enquanto você arrasta o nó, o Visual Studio exibe um indicador para mostrar que você está movendo o nó.<br /><br /> Também é possível arrastar nós para fora de um grupo.|
|Adicione um nó a um nó que não seja de grupo.|Arraste o nó para o nó de destino. Você pode converter qualquer nó de destino em um grupo adicionando nós a ele.|
|Agrupar nós selecionados.|1. Selecione os nós que você deseja agrupar. Uma barra de ferramentas pop-up aparece acima do último nó selecionado.<br />     ![Barra de ferramentas do grafo de dependência](../modeling/media/depedencygraph_toolbar.png)<br />2. na barra de ferramentas, escolha o quarto **grupo de ícones dos nós selecionados** (se o nó for expandido, ele terá cinco em vez de quatro ícones). Digite o nome do novo grupo e pressione **retornar**.<br />     - ou -<br />     Selecione os nós que você deseja agrupar e abra o menu de atalho para sua seleção. Escolha **grupo**, **Adicionar grupo pai**, digite o nome do novo grupo e pressione **retornar**.<br /><br /> Você pode renomear um grupo. Abra o menu de atalho do grupo e escolha **Editar**, **Propriedades** para abrir o janela Propriedades do Visual Studio. Na propriedade **Label** , renomeie o grupo conforme necessário.|
|Remover grupos.|Selecione o grupo ou os grupos que você deseja remover. Abra o menu de atalho para sua seleção e escolha **Agrupar**, **remover grupo**.|
|Remova os nós de seu grupo pai.|Selecione os nós que você deseja mover. Abra o menu de atalho para sua seleção e escolha **grupo**, **remover do pai**. Isso removerá os nós até o avô ou para fora do grupo se eles não tiverem um grupo avô.<br /><br /> - ou -<br /><br /> Selecione os nós e arraste-os para fora do grupo.|

## <a name="add-remove-or-rename-nodes-links-and-comments"></a><a name="AddRemoveNodesLinks"></a>Adicionar, remover ou renomear nós, links e comentários

Você pode exibir mais ou menos itens em um mapa para fazer uma busca detalhada ou simplificar o mapa. Você também pode renomear itens e adicionar comentários a itens.

> [!CAUTION]
> Antes de compartilhar um mapa criado usando Visual Studio Enterprise com aqueles que usam o Visual Professional, verifique se os elementos de código que você deseja que outras pessoas vejam estão visíveis no mapa. Caso contrário, esses usuários não poderão recuperar elementos de código excluídos.

### <a name="add-a-node-for-a-code-element"></a>Adicionar um nó para um elemento de código

|**Para**|**Realizar estas etapas**|
|-|-|
|Adicione um novo nó genérico no local do ponteiro do mouse atual.|1. Mova o ponteiro do mouse para o local no mapa em que você deseja colocar o novo elemento de código e pressione **Inserir**.<br />     - ou -<br />     Abra o menu de atalho para o mapa e escolha **Editar**, **Adicionar**, **nó genérico**.<br />2. Digite o nome do novo nó e pressione **Return**.|
|Adicione um tipo específico de nó de elemento de código no local do ponteiro do mouse atual.|1. Mova o ponteiro do mouse para o local no mapa em que você deseja colocar o novo elemento de código e abra o menu de atalho para o mapa.<br />2. escolha **Editar**, **Adicionar**e selecione o tipo de nó desejado.<br />3. Digite o nome do novo nó e pressione **Return**.|
|Adicione um tipo genérico ou específico de nó de elemento de código a um grupo.|1. Selecione o nó do grupo e abra o menu de atalho.<br />2. escolha **Editar**, **Adicionar**e selecione o tipo de nó desejado.<br />3. Digite o nome do novo nó e pressione **Return**.|
|Adicione um novo nó do mesmo tipo e vinculado a um nó existente.|1. Selecione o elemento de código. Uma barra de ferramentas pop-up aparece acima dela.<br />     ![Barra de ferramentas do grafo de dependência](../modeling/media/depedencygraph_toolbar.png)<br />2. na barra de ferramentas, escolha o segundo ícone **criar um nó com a mesma categoria deste nó e adicionar um novo link a ele**.<br />3. escolha um local no mapa para colocar o novo elemento de código e clique no botão esquerdo do mouse.<br />4. Digite o nome do novo nó e pressione **Return**.|
|Adicione um novo nó genérico que esteja vinculado a partir de um elemento de código existente que tenha foco.|1. usando o teclado, pressione **Tab** até que o elemento de código a ser vinculado tenha o foco (retângulo pontilhado).<br />2. Pressione **ALT** + **Insert**.<br />3. Digite o nome do novo nó e pressione **Return**.|
|Adicione um novo nó genérico que se vincule a um elemento de código existente que tenha foco.|1. usando o teclado, pressione **Tab** até que o elemento de código para vincular tenha o foco (retângulo pontilhado).<br />2. Pressione **ALT** + **Shift** + **Insert**.<br />3. Digite o nome do novo nó e pressione **Return**.|

|**Para adicionar elementos de código para**|**Realizar estas etapas**|
|-|-|
|Elementos de código na solução.|1. Localize o elemento de código em **Gerenciador de soluções**. Use a caixa de pesquisa **Gerenciador de soluções** ou procure a solução. **Dica:**      Para localizar elementos de código que têm dependências em um tipo ou membro, abra o menu de atalho para o tipo ou o membro em **Gerenciador de soluções**. Escolha a relação que lhe interessa. **Gerenciador de soluções** mostra apenas os elementos de código com as dependências especificadas.<br />2. Arraste os elementos de código que lhe interessam com a superfície do mapa. Você também pode arrastar elementos de código de Modo de Exibição de Classe ou pesquisador de objetos.<br />     - ou -<br />     Em **Gerenciador de soluções**, selecione os elementos de código que você deseja mapear. Em seguida, na barra de ferramentas **Gerenciador de soluções** , clique em **Mostrar no mapa de códigos**.<br /><br /> Por padrão, a hierarquia de contêineres pai para os novos elementos de código é mostrada no mapa. Use o botão **incluir pais** na barra de ferramentas do mapa de códigos para alterar esse comportamento. Quando desativado, somente o elemento de código em si é adicionado ao mapa. Para reverter esse comportamento para apenas uma ação de arrastar e soltar, pressione e mantenha pressionada a tecla **Ctrl** enquanto arrasta os elementos de código para o mapa.<br /><br /> O Visual Studio adiciona elementos de código para os elementos de código de nível superior na sua seleção. Para ver se um elemento de código contém outros elementos de código, mova o ponteiro do mouse sobre o elemento de código para que a divisa (seta para baixo) seja exibida. Escolha a divisa para expandir o elemento de código. Para expandir todos os elementos de código, pressione **Ctrl** + **a** para selecionar todos os elementos, abra o menu de atalho para o mapa e escolha **Agrupar**, **expanda**. Esse comando não estará disponível se a expansão de todos os grupos produzir um mapa inutilizável ou causar insuficiência de problemas de memória.|
|Elementos de código relacionados a elementos de código no mapa.|Clique no botão **Mostrar relacionado** na barra de ferramentas do mapa de códigos e escolha o tipo de itens relacionados nos quais você está interessado.<br /><br /> - ou -<br /><br /> Abra o menu de atalho para o elemento de código. Escolha um dos itens **mostrar...** no menu, dependendo do tipo de relação que lhe interessa. Por exemplo, você pode ver os itens que o item atual referencia, os itens que referenciam o item atual, os tipos base e derivados para classes, chamadores de método e as classes, namespaces e assemblies que a contêm.<br /><br /> Para obter mais detalhes, consulte [Este tópico](../modeling/map-dependencies-across-your-solutions.md).|
|Assemblies .NET compilados (. dll ou. exe) ou binários.|Arraste os assemblies ou binários de fora do Visual Studio para um mapa.<br /><br /> Você pode arrastar do Windows Explorer ou explorador de arquivos somente se estiver executando-o e o Visual Studio no mesmo nível de permissões do UAC (controle de acesso do usuário). Por exemplo, se o UAC estiver ativado e você estiver executando o Visual Studio como administrador, o Windows Explorer ou o explorador de arquivos bloqueará a operação de arrastar.|

### <a name="AddNodes"></a>

#### <a name="add-a-link-between-existing-code-elements"></a>Adicionar um link entre elementos de código existentes

1. Selecione o elemento de código-fonte. Uma barra de ferramentas é exibida acima do elemento de código.

    ![Barra de ferramentas do grafo de dependência](../modeling/media/depedencygraph_toolbar.png)

2. Na barra de ferramentas, escolha o primeiro ícone, **criar novo link desse nó no qual o nó em que você clicou em Avançar**.

3. Selecione o elemento de código de destino. Um link aparece entre os dois elementos de código.

**OR**

1. Selecione o elemento de código-fonte no mapa.

2. Se você tiver um mouse instalado, mova o ponteiro do mouse para fora dos limites do mapa.

3. Abra o menu de atalho do elemento de código e escolha **Editar**  >  **Adicionar**  >  **link genérico**.

4. Tab para e selecione o elemento de código de destino para o link.

5. Pressione **Enter**.

### <a name="AddComments"></a>

#### <a name="add-a-comment-to-an-existing-node-on-the-map"></a>Adicionar um comentário a um nó existente no mapa

1. Selecione o elemento de código. Uma barra de ferramentas aparece acima dela.

     ![Barra de ferramentas do grafo de dependência](../modeling/media/depedencygraph_toolbar.png)

2. Na barra de ferramentas, escolha o terceiro ícone, **crie um novo nó de comentário com um novo link para o nó selecionado**.

     \- ou –

     Abra o menu de atalho para o elemento de código e escolha **Editar**  >  **novo comentário**.

3. Digite os comentários. Para digitar em uma nova linha, pressione **Shift**  +  **Enter**.

#### <a name="add-a-comment-to-the-map-itself"></a>Adicionar um comentário ao mapa em si

1. Abra o menu de atalho para o mapa e escolha **Editar**  >  **novo comentário**.

2. Digite os comentários. Para digitar em uma nova linha, pressione **Shift**  +  **Enter**.

### <a name="RenameNodes"></a>

#### <a name="rename-a-code-element-or-link"></a>Renomear um elemento de código ou link

1. Selecione o elemento de código ou o link que você deseja renomear.

2. Pressione **F2**ou abra o menu de atalho e escolha **Editar**  >  **renomear**.

3. Quando a caixa de edição aparecer no mapa, renomeie o elemento de código ou o link.

**OR**

1. Abra o menu de atalho e escolha **Editar**  >  **Propriedades**.

2. Edite a propriedade **Label** no janela Propriedades do Visual Studio.

#### <a name="remove-a-code-element-or-link-from-the-map"></a>Remover um elemento de código ou um link do mapa

1. Selecione o elemento de código ou o link e pressione a tecla **delete** .

     \- ou –

     Abra o menu de atalho para o elemento de código ou link e escolha **Editar**  >  **remover**.

2. Se o elemento ou link fizer parte de um grupo, o ícone **rebuscar filhos** botão ![ recuperar filhos ](../modeling/media/dependencygraph_deletednodesicon.png) será exibido dentro do grupo. Clique aqui para recuperar elementos e links ausentes.

- Você pode remover elementos de código e links de um mapa sem afetar o código subjacente. Quando você os exclui, suas definições são removidas do arquivo DGML (. dgml).

- Mapas criados editando o DGML, adicionando elementos de código indefinidos ou usando algumas versões anteriores do Visual Studio, não dão suporte a esse recurso.

#### <a name="flag-a-code-element-for-follow-up"></a>Sinalizar um elemento de código para acompanhamento

1. Selecione o elemento de código ou o link que você deseja sinalizar para acompanhamento.

2. Abra o menu de atalho e escolha **Editar**  >  **sinalizador para acompanhamento**.

- Por padrão, o elemento de código obtém um plano de fundo vermelho. Considere [Adicionar um comentário](#AddComments) a ele com as informações apropriadas de acompanhamento.

- Altere a cor do plano de fundo do elemento ou desmarque o sinalizador de acompanhamento escolhendo **Editar**  >  **outras cores do sinalizador**.

## <a name="change-the-style-of-a-code-element-or-link"></a><a name="ChangeStyleCodeOrLink"></a>Alterar o estilo de um elemento de código ou link

Você pode alterar os ícones em elementos de código e as cores de elementos de código e links usando cores e ícones predefinidos. Por exemplo, você pode escolher uma cor para realçar elementos de código e links que têm uma determinada categoria ou propriedade. Isso permite que você identifique e concentre-se em áreas específicas do mapa. Você pode especificar ícones e cores personalizadas editando o arquivo. dgml do mapa; consulte [Personalizar mapas de código editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).

### <a name="to-apply-a-predefined-color-or-icon-to-code-elements-or-links-with-a-certain-category-or-property"></a>Para aplicar uma cor predefinida ou um ícone a elementos de código ou links com uma determinada categoria ou propriedade

1. Na barra de ferramentas do mapa, escolha **legenda**.

2. Na caixa **legenda** , veja se a categoria ou a propriedade do elemento de código já aparece na lista.

3. Se a lista não incluir a categoria ou propriedade, escolha **+** na caixa **legenda** e escolha **Propriedade do nó**, categoria do **nó**, Propriedade do **link**ou **categoria do link**. Em seguida, escolha a propriedade ou categoria. A categoria ou propriedade agora aparece na caixa **legenda** .

    > [!NOTE]
    > Para criar e atribuir uma categoria ou uma propriedade a um elemento de código, você pode editar o arquivo. dgml do mapa; consulte [Personalizar mapas de código editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).

4. Na caixa **legenda** , clique no ícone ao lado da categoria ou propriedade que você adicionou ou que deseja alterar.

5. Use a tabela a seguir para selecionar o estilo que você deseja alterar:

    |**Para alterar a**|**Escolha**|
    |-|-|
    |Cor da tela de fundo|**Tela de fundo**|
    |Cor do contorno|**Pincel**|
    |Cor do texto (uma letra "f" é exibida para mostrar o resultado)|**Primeiro plano**|
    |Ícone|**Ícones**|

     A caixa de diálogo **seletor de conjunto de cores** ou **seletor de conjunto de ícones** é exibida para que você selecione uma cor ou um ícone.

6. Na caixa de diálogo Seletor de **conjunto de cores** ou **seletor de conjunto de ícones** , siga um destes procedimentos:

    |**Para aplicar um**|**Realizar estas etapas**|
    |-|-|
    |Conjunto de cores ou ícones|Abra a lista **selecionar cor** (ou **ícone**) do **conjunto** . Selecione um conjunto de cores ou ícones.|
    |Cor ou ícone específico|Abra a categoria ou a lista de valores da propriedade. Selecione uma cor ou um ícone.|

    > [!NOTE]
    > Você pode reorganizar, excluir ou desativar temporariamente os estilos na caixa **legenda** . Consulte [Editar a caixa legenda](#ModifyLegend).

## <a name="edit-the-legend-box"></a><a name="ModifyLegend"></a>Editar a caixa de legenda

Você pode reorganizar, excluir ou desativar temporariamente os estilos na caixa **legenda** :

1. Abra o menu de atalho para um estilo na caixa **legenda** .

2. Realize uma das seguintes tarefas:

    |**Para**|**Escolha**|
    |-|-|
    |Desativar o elemento de código|**Desabilitar**|
    |Excluir o elemento de código|**Excluir**|
    |Mover o estilo para cima|**Mover para Cima**|
    |Mover o elemento de código para baixo|**Mover para Baixo**|

## <a name="copy-styles-from-one-map-to-another"></a><a name="CopyLegend"></a>Copiar estilos de um mapa para outro

1. Verifique se a caixa **legenda** aparece no mapa de origem. Se não estiver visível, na barra de ferramentas do mapa, clique em **legenda**.

2. Abra o menu de atalho da caixa **legenda** . Escolha **copiar legenda**.

3. Cole a legenda no mapa de destino.

## <a name="merge-code-maps"></a><a name="MergeMaps"></a>Mesclar mapas de código

Você pode mesclar mapas copiando e colando elementos de código entre mapas. Se os identificadores de elemento de código corresponderem, colar elementos de código funcionará como uma operação de mesclagem. Para facilitar essa tarefa, coloque todos os assemblies ou binários que você deseja visualizar na mesma pasta para que o caminho completo de cada assembly ou binário seja o mesmo para cada mapa que você deseja mesclar.

Como alternativa, você pode arrastar esses assemblies ou binários para o mesmo mapa dessa pasta.

## <a name="see-also"></a>Consulte também

- [Mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md)
- [Usar mapas de códigos para depurar aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)
- [Encontrar possíveis problemas usando analisadores de mapa de códigos](../modeling/find-potential-problems-using-code-map-analyzers.md)
- [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)
- [Referência DGML](../modeling/directed-graph-markup-language-dgml-reference.md)
