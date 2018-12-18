---
title: Procurar e reorganizar mapas de código | Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-tfs-dev14
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
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
ms.assetid: 08f65f77-6ca7-4b25-b060-3f6c9f5847a4
caps.latest.revision: 91
author: gewarren
ms.author: gewarren
manager: douge
ms.openlocfilehash: d931082dff95a8afe71eda94f37f0e0849811ac2
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51747587"
---
# <a name="browse-and-rearrange-code-maps"></a>Procurar e reorganizar mapa de códigos
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Reorganize itens em mapas de código para torná-los mais fáceis de ler e melhorar seu desempenho.  
  
 Você pode personalizar os mapas de código sem afetar o código subjacente em uma solução. Isso é útil quando você deseja se concentrar em elementos de código de chave ou informar ideias sobre o código. Por exemplo, para realçar áreas interessantes, você pode selecionar elementos no mapa de código e filtrá-los, alterar o estilo dos elementos de código e links, ocultar ou excluir elementos de código e organizar os elementos de código usando as propriedades, categorias ou grupos.  
  
 **Requisitos**  
  
-   Para criar mapas de código, você deve ter o Visual Studio Enterprise.  
  
-   Você pode exibir mapas de código e fazer edições limitadas em mapas de código no Visual Studio Professional.  
  
##  <a name="ManageLargeGraphs"></a> Começar a trabalhar com mapas de código  
 Criar um mapa de código (consulte [mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md) para obter mais detalhes). Se você não quiser esperar para o mapa concluir a geração, clique o **Cancelar** link a qualquer momento para parar o processo de geração. No entanto, você não verá os detalhes de todas as dependências e links se você fizer isso.  
  
 Depois de gerar o mapa, comece com estas dicas para revisar seu código:  
  
-   Examinar os clusters natural de dependência no código. Na barra de ferramentas do mapa, escolha **Layout**, **Clusters rápidos**![botão Clusters rápidos na barra de ferramentas de gráfico](../modeling/media/quickclustersicon.gif "QuickClustersIcon"). Ver [alterar o layout do mapa](#Selecting).  
  
     ![Gráfico de dependência &#45; layout de Clusters rápidos](../modeling/media/dependencygraph-quickclusters.png "DependencyGraph_QuickClusters")  
  
-   Organize o mapa em áreas pequenas, agrupando nós relacionados. Recolha esses grupos para ver apenas as dependências intergroup, que são exibidos automaticamente. Ver [agrupar nós](#OrganizeGroups).  
  
-   Use filtros para simplificar o mapa e concentre-se nos tipos de nós ou links que você está interessado. Ver [filtrar nós e links](#FilterNodes).  
  
-   Maximize o desempenho de grandes mapas. Ver [mapear as dependências nas soluções](../modeling/map-dependencies-across-your-solutions.md) para obter mais informações. Por exemplo, ative **Skip Build** na barra de ferramentas da mapa para que o Visual Studio não recompilar sua solução quando você atualiza os itens no mapa.  
  
##  <a name="Selecting"></a> Alterar o layout do mapa  
  
|**To**|**Execute estas etapas**|  
|------------|-----------------------------|  
|Organize o fluxo de dependência para o mapa inteiro em uma direção específica. Isso pode ajudar você a ver as camadas arquitetônicas no código.|Na barra de ferramentas do mapa, escolha **Layout**e, em seguida:<br /><br /> -   **De cima para baixo** ![superior do botão de gráfico inferior](../modeling/media/topbottomgraphbutton.gif "TopBottomGraphButton")<br />-   **Baixo para cima** ![inferior ao botão gráfico superior](../modeling/media/bottomtopgraphbutton.gif "BottomTopGraphButton")<br />-   **Da esquerda para a direita** ![da esquerda para o botão direito do layout](../modeling/media/leftrightgraphbutton.gif "LeftRightGraphButton")<br />-   **Direita para a esquerda** ![direita para o botão esquerdo do grafo](../modeling/media/rightleftgraphbutton.gif "RightLeftGraphButton")|  
|Veja clusters natural de dependência no código com os nós mais dependentes no centro dos clusters e nós menos dependentes na parte externa desses clusters.|Na barra de ferramentas do mapa, escolha **Layout**e então **Clusters rápidos**![botão Clusters rápidos na barra de ferramentas de gráfico](../modeling/media/quickclustersicon.gif "QuickClustersIcon").|  
|Selecione um ou mais nós no mapa.|Clique em um nó para selecioná-lo. Para marcar ou desmarcar a mais de um nó, mantenha **CTRL** enquanto clica.<br /><br /> Teclado: pressione **guia** ou use as teclas de direção para mover o retângulo de foco pontilhado para um nó e pressione **espaço** para selecioná-lo. Pressione **CTRL** + **espaço** fazer seleção múltipla ou desmarque os nós.|  
|Mova os nós específicos no mapa.|Arrastar nós para movê-los. Para mover os outros nós e links fora do caminho ao arrastar nós, pressione e segure a **SHIFT** chave.<br /><br /> Teclado: mantenha **CTRL** e pressione as teclas de direção.|  
|Altere o layout dentro de um grupo, independentemente de outros nós e grupos no mapa.|Selecione um nó e abra o menu de atalho. Escolher **Layout** e selecione um estilo de layout.<br /><br /> - ou -<br /><br /> Selecione um nó e expandi-lo e mostra os nós filhos. Clique no título de nó para mostrar a barra de ferramentas pop-up do grupo e, em seguida, abra o **alterar o estilo de layout do grupo**![grafo de dependência &#45; barra de ferramentas do grupo &#45; layout](../modeling/media/dependencygraph-grouptoolbar.gif "DependencyGraph_ GroupToolbar") lista. Selecione um dos layouts de árvore, **Clusters rápidos**, ou **exibição de lista** (que organiza o conteúdo de grupo em uma lista).<br /><br /> Ver [agrupar nós](#OrganizeGroups) para obter mais detalhes.|  
|Desfazer uma ação no mapa.|Pressione **CTRL** + **Z** ou usar o Visual Studio **desfazer** comando.|  
  
##  <a name="Explore"></a> Procurar o mapa  
  
|**To**|**Execute estas etapas**|  
|------------|-----------------------------|  
|Verificar o mapa.|Arraste o mapa em qualquer direção usando o mouse.<br /><br /> - ou -<br /><br /> Mantenha **SHIFT** e gire a roda do mouse para rolar horizontalmente. Mantenha **SHIFT** + **CTRL** e gire a roda do mouse para rolar horizontalmente.|  
|Amplie ou reduzir o mapa.|Gire a roda do mouse.<br /><br /> - ou -<br /><br /> Use o **Zoom** lista suspensa na barra de ferramentas de mapa de código.<br /><br /> - ou -<br /><br /> Use os atalhos de teclado. Para aumentar o zoom, pressione **CTRL + SHIFT +.** (ponto). Para reduzir, pressione **CTRL + SHIFT +,** (vírgula).|  
|Aplicar zoom em uma área específica usando o mouse.|Mantenha o botão direito do mouse ao desenhar um retângulo em torno dessa área que você está interessado.|  
|Redimensione e ajustar o mapa em sua janela.|Escolher **Ajustar nível de Zoom** da **Zoom** lista na barra de ferramentas de mapa de código.<br /><br /> - ou -<br /><br /> Clique o **Aplicar Zoom para ajustar** ícone ![ícone de Zoom na barra de ferramentas do mapa](../modeling/media/almcodemapzoomicon.png "ALMCodeMapZoomIcon") na barra de ferramentas de mapa de código. Teclado: pressione **CTRL + 0** (zero).|  
|Localize um nó no mapa por seu nome. **Dica:** isso funciona somente para itens no mapa. Para localizar itens em sua solução, mas não no mapa, encontrá-los no **Gerenciador de soluções**e, em seguida, arraste-os para o mapa. (Arraste sua seleção, ou na barra de ferramentas do Gerenciador de soluções, clique em **Mostrar no mapa de códigos**).|1.  Escolha o **encontrar** ícone ![ícone localizar na barra de ferramentas do mapa](../modeling/media/almcodemapfindicon.png "ALMCodeMapFindIcon") na barra de ferramentas de mapa de código (teclado: pressione **CTRL + F**) para mostrar caixa de pesquisa no canto superior direito do mapa.<br />2.  Digite o nome do item e pressione **retornar** ou clique no ícone "Lupa". O primeiro item que corresponde à sua pesquisa aparece selecionado no mapa.<br />3.  Para personalizar sua pesquisa, abra a lista suspensa e escolha uma opção de pesquisa. As opções são **Localizar próxima**, **Localizar anterior**, e **Selecionar tudo**. Em seguida, clique no botão correspondente ao lado da caixa de texto de pesquisa.<br />     ![Lista de opções de pesquisa&#45;para baixo na lista](../modeling/media/almcodemapssearchdropdown.png "ALMCodeMapsSearchDropDown")<br />     Como alternativa, use o teclado: pressione **F3** para selecionar o próximo nó correspondente ou **SHIFT + F3** para selecionar o nó correspondente anterior.<br />4.  Selecione qualquer uma das opções que especificam como os termos de pesquisa são tratados clicando nos ícones abaixo da caixa de texto de pesquisa.<br />     ![Opções de correspondência de pesquisa](../modeling/media/almcodemapssearchmatchicons.png "ALMCodeMapsSearchMatchIcons")<br />     As opções são, da esquerda para a direita, case de correspondência confidenciais, coincidir somente palavras inteiras, usar sintaxe de expressão regular do .NET, expandir automaticamente os grupos para mostrar as correspondências entre itens. **Importante:** você pode usar a caixa de pesquisa para localizar correspondências em grupos recolhidos somente se esses grupos foram previamente expandidos. Para localizar essas correspondências e expandir automaticamente o dos grupos pai, escolha esta opção na caixa de pesquisa.|  
|Selecione todos os nós não selecionados.|Abra o menu de atalho para os nós selecionados. Escolher **selecionar**, **Inverter seleção**.|  
|Selecione nós adicionais vinculados aos selecionados.|Abra o menu de atalho para os nós selecionados. Escolher **selecionar** e uma destas opções:<br /><br /> -Para selecionar nós adicionais vinculados diretamente ao nó selecionado, escolha **dependências de entrada**.<br />-Para selecionar nós adicionais vinculados diretamente do nó selecionado, escolha **dependências de saída**.<br />-Para selecionar nós adicionais vinculados diretamente para e do nó selecionado, escolha **ambos**.<br />-Para selecionar todos os nós vinculados ao e do nó selecionado, escolha **subgráfico conectado**.<br />-Para selecionar todos os filhos do nó selecionado, escolha **filhos**.|  
  
##  <a name="FilterNodes"></a> Filtrar nós e links  
  
|**To**|**Execute estas etapas**|  
|------------|-----------------------------|  
|Mostrar ou ocultar o painel filtros.|Escolha o **filtros** na barra de ferramentas de mapa de código. Por padrão, o painel filtros é exibido como uma página com guias na janela do Gerenciador de soluções.|  
|Filtre os tipos de nós que são mostrados no mapa.|Defina ou desmarque as caixas de seleção na **elementos de código** lista no painel de filtros.|  
|Filtre os tipos de links que são mostrados no mapa.|Defina ou desmarque as caixas de seleção na **relações** lista no painel de filtros.|  
|Mostrar ou ocultar nós de projeto de teste no mapa.|Definir ou limpar os **ativos de teste** caixa de seleção na **diversos** lista no painel de filtros.|  
  
 Os ícones mostrados no painel de legenda do mapa de refletem as configurações feitas na lista. Para mostrar ou ocultar o painel de legenda, clique o **legenda** na barra de ferramentas de mapa de código.  
  
##  <a name="Inspect"></a> Examine nós e links  
 Mapas de código mostram esses tipos de links:  
  
-   Um link individual representa uma única relação entre dois nós.  
  
-   Um link de grupo cruzado representa uma relação entre dois nós em grupos diferentes.  
  
-   Um link agregado representa todas as relações de ponto na mesma direção entre dois grupos.  
  
> [!TIP]
>  Por padrão, o mapa mostra os links de grupo cruzado apenas para nós selecionados. Para alterar esse comportamento para mostrar ou ocultar links agregados entre grupos, clique em **Layout** no código da barra de ferramentas do mapa e escolha **avançado**, em seguida, **Mostrar todos os Links de grupo cruzado** ou **Ocultar todos os Links de grupo cruzado**. Ver [ocultar ou Mostrar nós e links](#HidingShowing) para obter mais detalhes.  
  
|**To**|**Execute estas etapas**|  
|------------|-----------------------------|  
|Obter mais informações sobre um nó ou um link.|Mova o ponteiro do mouse sobre o nó ou link até que uma dica de ferramenta seja exibida.<br /><br /> Dica de ferramenta para um link agregado lista as dependências individuais que ele representa.<br /><br /> - ou -<br /><br /> Abra o menu de atalho do nó ou o link. Escolher **edite**, **propriedades**.|  
|Mostrar ou ocultar o conteúdo de um grupo.|-Para expandir um grupo, abra o menu de atalho para o nó e escolha **grupo**, **expandir**.<br />     - ou -<br />     Mova o ponteiro do mouse sobre o nó até que apareça no botão de divisa (seta para baixo). Clique neste botão para expandir o grupo. Teclado: para expandir ou recolher o grupo selecionado, pressione a **PLUS** chave (**+**) ou o **menos** chave (**-**).<br />-Para recolher um grupo, abra o menu de atalho para o nó e escolha **grupo**, **recolher**.<br />     - ou -<br />     Mova o ponteiro do mouse sobre um grupo até que apareça no botão de divisa (seta para cima). Clique neste botão para recolher o grupo.<br />-Para expandir todos os grupos, pressione **CTRL** + **um** para selecionar todos os nós. Abra o menu de atalho para o mapa e escolha **grupo**, **expandir**. **Observação:** esse comando não estará disponível se a expansão de todos os grupos gera um mapa inutilizável ou problemas de memória. É recomendável que você expandir o mapa somente para o nível de detalhe que você se preocupa.<br />-Para recolher todos os grupos, abra o menu de atalho para um nó ou para o mapa. Escolher **grupo**, **Recolher tudo**.|  
|Consulte a definição de código para um namespace, tipo ou membro.|Abra o menu de atalho para o nó e escolha **ir para definição**.<br /><br /> -ou-<br /><br /> Clique duas vezes no nó. Para grupos expandidos, clique duas vezes o cabeçalho de grupo.<br /><br /> -ou-<br /><br /> Selecione o nó e pressione **F12**.<br /><br /> Por exemplo:<br /><br /> – Para um namespace que contém uma classe, o arquivo de código para a classe é aberto para mostrar a definição dessa classe. Em outros casos, o **Find Symbol Results** janela mostra uma lista de arquivos de código. **Observação:** quando você executar essa tarefa em um namespace do Visual Basic .NET, o arquivo de código por trás do namespace não abre. Esse problema também ocorre quando você executar essa tarefa em um grupo de nós selecionados que incluem um namespace do Visual Basic .NET. Para contornar esse problema, navegar manualmente até o arquivo de código por trás do namespace ou omita o nó para o namespace da sua seleção.<br />– Para uma classe ou uma classe parcial, o arquivo de código para essa classe é aberto para mostrar a definição de classe.<br />– Para um método, o arquivo de código para a classe pai é aberto para mostrar a definição do método.|  
|Examine as dependências e os itens que participam de um link agregado.|Selecione os links que você está interessado e abra o menu de atalho para a sua seleção. Escolher **Mostrar Links participantes** ou **Mostrar Links participantes no novo mapa de códigos**.<br /><br /> O Visual Studio expande os grupos em ambas as extremidades do link e mostra apenas esses itens e dependências que participam do link. **Observação:** ao examinar as dependências entre os itens em grupos parciais, você poderá ver esse comportamento: <ul><li>Links para itens que não participam de seu exame desaparecem do mapa, mesmo que esses links ainda existem.</li><li>Suponha que você examinar um link para um item em um grupo parcial e, em seguida, posteriormente, examina um link diferente no mesmo item. Durante o exame de segundo, o grupo de destino parcial mostra apenas os itens de seu primeiro exame. Links e itens de destino que não participam de seu primeiro exame mas participar de seu segundo exame não são exibidos.</li></ul> Para ver itens de um grupo ausentes, escolha **buscar novamente filhos**![buscar novamente filhos ícone](../modeling/media/dependencygraph-deletednodesicon.png "DependencyGraph_DeletedNodesIcon") (que indica que nem todos os membros de um grupo aparecem no mapa). Você também pode tentar desfazer suas ações (teclado: pressione **CTRL + Z**) e examinar as dependências em um novo mapa.|  
|Examine as dependências em vários nós em grupos diferentes.|Expanda os grupos para que você possa ver todos os seus filhos. Selecione todos os nós que interessam a você, incluindo seus filhos. O mapa mostra os links de grupo cruzado entre os nós selecionados.<br /><br /> Para selecionar todos os nós em um grupo, pressione e segure **SHIFT** e o botão esquerdo do mouse enquanto desenha um retângulo em torno desse grupo. Para selecionar todos os nós em um mapa, pressione **CTRL**+**um**. **Dica:** para mostrar os links de grupo cruzado em todos os momentos, escolha **Layout** na barra de ferramentas do mapa **avançado**, **Mostrar todos os Links de grupo cruzado**.|  
|Ver os itens que faz referência a um nó ou link.|Abra o menu de atalho para o nó e escolha **localizar todas as referências**. **Observação:** isso se aplica somente quando o `Reference` atributo é definido para o nó ou link no arquivo. dgml do mapa. Para adicionar referências a itens de nós ou links, consulte [mapas de código de personalizar, editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).|  
  
##  <a name="HidingShowing"></a> Ocultar ou Mostrar nós e links  
 Ocultar nós os impede de participar de algoritmos de layout. Por padrão, links de grupo cruzado permanecem ocultos. Links de grupo cruzado são links individuais que conectam nós entre os grupos. Quando os grupos são recolhidos, o mapa agrega todos os links de grupo cruzado em links únicos entre grupos. Quando você expande um grupo e seleciona nós dentro do grupo, os links de grupo cruzado são exibidos e mostram as dependências nesse grupo.  
  
> [!CAUTION]
>  Antes de compartilhar um mapa que foi criado no Visual Studio Enterprise com aqueles que usam o Visual Studio Professional, certifique-se reexibir todos os nós ou links de grupo cruzado que você deseja que outras pessoas vejam. Do contrário, os usuários não poderão reexibir esses itens.  
  
### <a name="to-hide-or-show-nodes"></a>Para ocultar ou mostrar nós  
  
|**To**|**Execute estas etapas**|  
|------------|-----------------------------|  
|Oculte nós selecionados.|1.  Selecione os nós que você deseja ocultar.<br />2.  Abra o menu de atalho para os nós selecionados ou para o mapa. Escolher **selecionar**, **ocultar selecionados**.|  
|Oculte nós não selecionados.|1.  Selecione nós que você deseja manter visíveis.<br />2.  Abra o menu de atalho para os nós selecionados ou para o mapa. Escolher **selecionar**, **ocultar desmarcado**.|  
|Mostra nós ocultos.|-Para mostrar todos os nós ocultos dentro de um grupo, primeiro verifique se que o grupo é expandido. Abra o menu de atalho e escolha **selecionar**, **reexibir filhos**.<br />     - ou -<br />     Clique o **reexibir filhos**![reexibir filhos ícone](../modeling/media/dependencygraph-filtericon-hiddennodes.gif "DependencyGraph_FilterIcon_HiddenNodes") ícone no canto superior esquerdo do grupo (isso só está visível quando Há nós filhos ocultos).<br />-Para mostrar todos os nós ocultos, abra o menu de atalho para o mapa ou um nó e escolha **selecionar**, **reexibir todos os**.|  
  
### <a name="to-hide-or-show-links"></a>Para ocultar ou Mostrar links  
  
|**To**|**Na barra de ferramentas do mapa, escolha o Layout, Avançado e, em seguida, escolha**|  
|------------|----------------------------------------------------------------------|  
|Mostra links de grupo cruzado em todos os momentos.|**Mostrar todos os Links de grupo cruzado**. Isso oculta links agregados entre grupos.|  
|Oculte links de grupo cruzado em todos os momentos.|**Ocultar todos os Links de grupo cruzado**|  
|Mostra apenas os links de grupo cruzado para nós selecionados.|**Mostrar Links de grupo cruzado em nós selecionados**|  
|Oculte todos os links.|**Ocultar todos os Links**. Para exibir links novamente, escolha uma das opções listadas acima.|  
  
##  <a name="OrganizeGroups"></a> Nós de grupo  
  
|**To**|**Execute estas etapas**|  
|------------|-----------------------------|  
|Mostra nós de contêiner como nós de grupo ou nós folha.|Para mostrar nós de contêiner como nós folha: selecione os nós, abra o menu de atalho para a sua seleção e escolha **grupo**, **converter para a folha**.<br /><br /> Para mostrar nós de contêiner como nós de grupo: selecione os nós, abra o menu de atalho para a sua seleção e escolha **grupo**, **converter para o grupo**.|  
|Altere o layout dentro de um grupo.|Selecione o grupo, abra o menu de atalho, escolha **Layout**e selecione o estilo de layout desejado.<br /><br /> - ou -<br /><br /> 1.  Selecione o grupo e verifique se que ele é expandido.<br />2.  Clique no cabeçalho de grupo novamente e a barra de ferramentas do grupo é exibida.<br />     ![Gráfico de dependência &#45; barra de ferramentas do grupo](../modeling/media/dependencygraph-group.png "DependencyGraph_Group")<br />3.  Abra o **alterar o estilo de layout do grupo** lista ![grafo de dependência &#45; barra de ferramentas do grupo &#45; layout](../modeling/media/dependencygraph-grouptoolbar.gif "DependencyGraph_GroupToolbar") e escolha o estilo de layout desejado.<br /><br /> **Exibição de lista** reorganiza os membros do grupo na lista. **Padrão de grafo** redefine o layout do grupo para o layout padrão de mapa. Para obter outras opções, consulte [alterar o layout do mapa](#Selecting).|  
|Adicione um nó a um grupo.|Arraste o nó para o grupo.<br /><br /> Ao arrastar o nó, o Visual Studio exibe um indicador para mostrar que você está movendo o nó.<br /><br /> Também é possível arrastar nós para fora de um grupo.|  
|Adicione um nó a um nó de grupo.|Arraste o nó para o nó de destino. Você pode converter qualquer nó de destino em um grupo com a adição de nós.|  
|Agrupe nós selecionados.|1.  Selecione os nós que você deseja agrupar. Uma barra de ferramentas pop-up aparece acima o último nó que você selecionar.<br />     ![Barra de ferramentas de gráfico de dependência](../modeling/media/depedencygraph-toolbar.png "DepedencyGraph_Toolbar")<br />2.  Na barra de ferramentas, escolha o ícone de quarto **agrupar os nós selecionados** (se o nó é expandido ele terá cinco em vez de quatro ícones). Digite o nome para o novo grupo e pressione **retornar**.<br />     - ou -<br />     Selecione os nós que você deseja agrupar e abra o menu de atalho para a sua seleção. Escolher **grupo**, **adicionar grupo do pai**, digite o nome para o novo grupo e pressione **retornar**.<br /><br /> Você pode renomear um grupo. Abra o menu de atalho para o grupo e escolha **edite**, **propriedades** para abrir a janela de propriedades do Visual Studio. No **rótulo** propriedade, renomeie o grupo conforme necessário.|  
|Remova os grupos.|Selecione o grupo ou os grupos que você deseja remover. Abra o menu de atalho para a sua seleção e escolha **grupo**, **remover grupo**.|  
|Remova nós do grupo pai.|Selecione os nós que você deseja mover. Abra o menu de atalho para a sua seleção e escolha **grupo**, **remover do pai**. Isso remove nós de backup para seu avô, ou para fora do grupo se eles tiverem nenhum grupo avô.<br /><br /> - ou -<br /><br /> Selecione os nós e arrastá-los fora do grupo.|  
  
##  <a name="AddRemoveNodesLinks"></a> Adicionar, remover ou renomear nós, links e comentários  
 Você pode exibir mais ou menos itens em um mapa para fazer uma busca detalhada ou para simplificar o mapa. Você também pode renomear itens e adicionar comentários aos itens.  
  
> [!CAUTION]
>  Antes de compartilhar um mapa que foi criado usando o Visual Studio Enterprise com aqueles que usam Visual Professional, verifique se quaisquer elementos de código que você deseja que outras pessoas vejam estão visíveis no mapa. Caso contrário, os usuários não poderão recuperar os elementos de código excluído.  
  
### <a name="add-a-node-for-a-code-element"></a>Adicionar um nó para um elemento de código  
  
|**To**|**Execute estas etapas**|  
|------------|-----------------------------|  
|Adicione um novo nó genérico no local atual do ponteiro do mouse.|1.  Mova o ponteiro do mouse para o local no mapa de onde você deseja colocar o novo elemento de código e pressione **inserir**.<br />     - ou -<br />     Abra o menu de atalho para o mapa e escolha **edite**, **Add**, **nó genérico**.<br />2.  Digite o nome para o novo nó e pressione **retornar**.|  
|Adicione um tipo específico de nó de elemento de código no local atual do ponteiro do mouse.|1.  Mova o ponteiro do mouse para o local no mapa de onde você deseja colocar o novo elemento de código e abra o menu de atalho para o mapa.<br />2.  Escolher **edite**, **Add**e selecione o tipo de nó que você deseja.<br />3.  Digite o nome para o novo nó e pressione **retornar**.|  
|Adicione um genérico ou um tipo de nó de elemento de código específico a um grupo.|1.  Selecione o nó do grupo e abra o menu de atalho.<br />2.  Escolher **edite**, **Add**e selecione o tipo de nó que você deseja.<br />3.  Digite o nome para o novo nó e pressione **retornar**.|  
|Adicionar um novo nó do mesmo tipo e vinculadas de um nó existente.|1.  Selecione o elemento de código. Uma barra de ferramentas pop-up aparece acima dele.<br />     ![Barra de ferramentas de gráfico de dependência](../modeling/media/depedencygraph-toolbar.png "DepedencyGraph_Toolbar")<br />2.  Na barra de ferramentas, escolha o segundo ícone **criar um nó com a mesma categoria deste nó e adicionar um novo link para ele**.<br />3.  Escolha um local no mapa para colocar o novo elemento de código e clique no botão esquerdo do mouse.<br />4.  Digite o nome para o novo nó e pressione **retornar**.|  
|Adicione um novo nó genérico que esteja vinculado de um elemento de código existente que tem o foco.|1.  Usando o teclado, pressione **guia** até que o elemento de código para link do tem o foco (retângulo pontilhado).<br />2.  Pressione **Alt**+**inserir**.<br />3.  Digite o nome para o novo nó e pressione **retornar**.|  
|Adicione um novo nó genérico que vincula a um elemento de código existente que tem o foco.|1.  Usando o teclado, pressione **guia** até que o elemento de código para vincular a tem o foco (retângulo pontilhado).<br />2.  Pressione **Alt**+**Shift**+**inserir**.<br />3.  Digite o nome para o novo nó e pressione **retornar**.|  
  
|**Para adicionar elementos de código para**|**Execute estas etapas**|  
|----------------------------------|-----------------------------|  
|Elementos de código na solução.|1.  Localize o elemento de código em **Gerenciador de soluções**. Use o **Gerenciador de soluções** caixa de pesquisa ou procurar a solução. **Dica:** para localizar os elementos de código que têm dependências em um tipo ou membro, abra o menu de atalho para o tipo ou membro na **Gerenciador de soluções**. Escolha a relação que lhe interessa. **Gerenciador de soluções** mostra apenas os elementos de código com as dependências especificadas.<br />2.  Arraste os elementos de código que lhe interessam para a superfície do mapa. Você também pode arrastar elementos de código do modo de exibição de classe ou Pesquisador de objetos.<br />     - ou -<br />     Na **Gerenciador de soluções**, selecione os elementos de código que você deseja mapear. Em seguida, na **Gerenciador de soluções** barra de ferramentas, clique em **Mostrar no mapa de códigos**.<br /><br /> Por padrão, a hierarquia do contêiner pai para os novos elementos de código é mostrada no mapa. Use o **pais incluem** na barra de ferramentas de mapa de código de alterar esse comportamento. Quando desativado, apenas o elemento de código em si é adicionado ao mapa. Para reverter esse comportamento para apenas um de arrastar e soltar ação, pressione e segure a **CTRL** pressionada ao arrastar os elementos de código para o mapa.<br /><br /> O Visual Studio adiciona elementos de código para os elementos de código de nível superior na sua seleção. Para ver se um elemento de código contém outros elementos de código, mova o ponteiro do mouse sobre o elemento de código para que apareça na divisa (seta para baixo). Escolha a divisa para expandir o elemento de código. Para expandir todos os elementos de código, pressione **CTRL**+**um** para selecionar todos os elementos, abra o menu de atalho para o mapa e escolha **grupo**, **expandir** . Esse comando não estará disponível se expandir todos os grupos seria produzir um mapa inutilizável ou causar insuficiência de problemas de memória.|  
|Elementos de código relacionados aos elementos de código no mapa.|Clique o **Mostrar relacionados** botão na barra de ferramentas de mapa de código e escolha o tipo de itens relacionados que lhe interessam.<br /><br /> - ou -<br /><br /> Abra o menu de atalho para o elemento de código. Escolha uma da **Mostrar...** itens no menu, dependendo do tipo de relação que lhe interessa. Por exemplo, você pode ver os itens que referencia o item atual, os itens que referenciam o item atual, os tipos de base e derivados para classes, os chamadores do método e que contém classes, namespaces e assemblies.<br /><br /> Para obter mais detalhes, consulte [neste tópico](../modeling/map-dependencies-across-your-solutions.md).|  
|Assemblies compilados do .NET (. dll ou .exe) ou binários.|Arraste os assemblies ou os binários de fora do Visual Studio para um mapa.<br /><br /> Você pode arrastar do Windows Explorer ou o Explorador de arquivos somente se você estiver executando no mesmo nível de permissões de controle de acesso de usuário (UAC) ele e o Visual Studio. Por exemplo, se UAC estiver ativado e você estiver executando o Visual Studio como administrador, o Windows Explorer ou o Explorador de arquivos bloqueará a operação de arrastamento.|  
  
###  <a name="AddNodes"></a>   
##### <a name="add-a-link-between-existing-code-elements"></a>Adicionar um link entre os elementos de código existentes  
  
1. Selecione o elemento de código de origem. Uma barra de ferramentas é exibida acima do elemento de código.  
  
    ![Barra de ferramentas de gráfico de dependência](../modeling/media/depedencygraph-toolbar.png "DepedencyGraph_Toolbar")  
  
2. Na barra de ferramentas, escolha o primeiro ícone, **criar novo link deste nó para nó em que você clicar em Avançar**.  
  
3. Selecione o elemento de código de destino. Um link será exibido entre os elementos de código de dois.  
  
   \- ou -  
  
4. Selecione o elemento de código fonte no mapa.  
  
5. Se você tiver um mouse instalado, mova o ponteiro do mouse fora dos limites do mapa.  
  
6. Abra o menu de atalho do elemento de código e escolha **edite**, **Add**, **Link genérico**.  
  
7. Pressionar TAB até e selecione o elemento de código de destino para o link.  
  
8. Pressione **retornar**.  
  
###  <a name="AddComments"></a>   
##### <a name="add-a-comment-to-an-existing-node-on-the-map"></a>Adicionar um comentário a um nó existente no mapa  
  
1.  Selecione o elemento de código. Uma barra de ferramentas aparece acima dele.  
  
     ![Barra de ferramentas de gráfico de dependência](../modeling/media/depedencygraph-toolbar.png "DepedencyGraph_Toolbar")  
  
2.  Na barra de ferramentas, escolha o ícone de terceiro **criar um novo nó de comentário com um novo link para o nó selecionado**.  
  
     \- ou -  
  
     Abra o menu de atalho para o elemento de código e escolha **edite**, **novo comentário**.  
  
3.  Digite os comentários. Para digitar em uma nova linha, pressione **SHIFT** + **retornar**.  
  
##### <a name="add-a-comment-to-the-map-itself"></a>Adicionar um comentário para o mapa em si  
  
1.  Abra o menu de atalho para o mapa e escolha **edite**, **novo comentário**.  
  
2.  Digite os comentários. Para digitar em uma nova linha, pressione **SHIFT** + **retornar**.  
  
###  <a name="RenameNodes"></a>   
##### <a name="rename-a-code-element-or-link"></a>Renomear um elemento de código ou link  
  
1.  Selecione o elemento de código ou o link que você deseja renomear.  
  
2.  Pressione **F2**, ou abra o menu de atalho e escolha **editar**, **Renomear**.  
  
3.  Quando a caixa de edição é exibida no mapa, renomeie o elemento de código ou o link.  
  
     \- ou -  
  
4.  Abra o menu de atalho e escolha **edite**, **propriedades**.  
  
5.  Editar o **rótulo** propriedade na janela Propriedades do Visual Studio.  
  
##### <a name="remove-a-code-element-or-link-from-the-map"></a>Remover um elemento de código ou link de mapa  
  
1.  Selecione o elemento de código ou link e pressione a **excluir** chave.  
  
     \- ou -  
  
     Abra o menu de atalho para o elemento de código ou link e escolha **edite**, **remover**.  
  
2.  Se o elemento ou o link fizer parte de um grupo, o **buscar novamente filhos** botão ![buscar novamente filhos ícone](../modeling/media/dependencygraph-deletednodesicon.png "DependencyGraph_DeletedNodesIcon") aparece dentro do grupo. Clique aqui para recuperar os links e elementos ausentes.  
  
-   Você pode remover elementos de código e links de um mapa sem afetar o código subjacente. Quando você exclui-los, as definições serão removidas do arquivo DGML (. dgml).  
  
-   Mapas criados editando o DGML, adicionando os elementos de código indefinido ou por meio de algumas versões anteriores do Visual Studio, não há suporte para esse recurso.  
  
##### <a name="flag-a-code-element-for-follow-up"></a>Um elemento de código para acompanhamento do sinalizador  
  
1.  Selecione o elemento de código ou link que você deseja sinalizar para acompanhamento.  
  
2.  Abra o menu de atalho e escolha **edite**, **sinalizador para acompanhamento**.  
  
-   Por padrão, o elemento de código obtém um plano de fundo vermelho. Considere [adicionando um comentário](#AddComments) a ele com as informações apropriadas de acompanhamento.  
  
-   Alterar a cor do plano de fundo do elemento ou limpar o sinalizador de acompanhamento, escolhendo **edite**, **outras cores de sinalizador**.  
  
##  <a name="ChangeStyleCodeOrLink"></a> Alterar o estilo de um elemento de código ou link  
 Você pode alterar os ícones em elementos de código e as cores de elementos de código e links usando cores e ícones predefinidos. Por exemplo, você pode escolher uma cor para realçar os elementos de código e links que tenham uma determinada categoria ou propriedade. Isso permite identificar e enfocar áreas específicas do mapa. Você pode especificar cores e ícones personalizados editando o arquivo. dgml do mapa; ver [mapas de código de personalizar, editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).  
  
#### <a name="to-apply-a-predefined-color-or-icon-to-code-elements-or-links-with-a-certain-category-or-property"></a>Para aplicar uma cor predefinida ou o ícone a elementos de código ou links com uma determinada categoria ou propriedade  
  
1.  Na barra de ferramentas do mapa, escolha **legenda**.  
  
2.  No **legenda** caixa, consulte se a categoria de elemento de código ou a propriedade já aparece na lista.  
  
3.  Se a lista não inclui a categoria ou propriedade, escolha **+** no **legenda** caixa e, em seguida, escolha **propriedade nó**, **categoria do nó** , **Vincular a propriedade**, ou **vincular categoria**. Em seguida, escolha a categoria ou propriedade. A categoria ou propriedade aparece agora o **legenda** caixa.  
  
    > [!NOTE]
    >  Para criar e atribuir uma categoria ou uma propriedade a um elemento de código, você pode editar o arquivo. dgml do mapa; ver [mapas de código de personalizar, editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md).  
  
4.  No **legenda** caixa, clique no ícone ao lado de categoria ou propriedade que você adicionou ou você deseja alterar.  
  
5.  Use a tabela a seguir para selecionar o estilo que você deseja alterar:  
  
    |**Para alterar o**|**Choose**|  
    |-----------------------|----------------|  
    |Cor do plano de fundo|**Tela de Fundo**|  
    |Cor do contorno|**Traço**|  
    |Cor do texto (uma letra "f" for exibida para mostrar o resultado)|**Em primeiro plano**|  
    |Ícone|**Ícones**|  
  
     O **seletor do conjunto de cores** ou **seletor do conjunto de ícone** caixa de diálogo é exibida para você selecionar uma cor ou um ícone.  
  
6.  No **seletor do conjunto de cores** ou **seletor do conjunto de ícone** caixa de diálogo, faça o seguinte:  
  
    |**Para aplicar um**|**Execute estas etapas**|  
    |--------------------|-----------------------------|  
    |Conjunto de cores ou ícones|Abra o **selecionar cor** (ou **ícone**) **definir** lista. Selecione um conjunto de cores ou ícones.|  
    |Cor específica ou ícone|Abra a categoria ou a lista de valores da propriedade. Selecione uma cor ou um ícone.|  
  
    > [!NOTE]
    >  Você pode reorganizar, excluir ou Inativar temporariamente estilos na **legenda** caixa. Ver [editar a caixa legenda](#ModifyLegend).  
  
##  <a name="ModifyLegend"></a> Editar a caixa de legenda  
 Você pode reorganizar, excluir ou Inativar temporariamente estilos na **legenda** caixa:  
  
1.  Abra o menu de atalho para um estilo na **legenda** caixa.  
  
2.  Realize uma das seguintes tarefas:  
  
    |**To**|**Choose**|  
    |------------|----------------|  
    |Desativar o elemento de código|**Desabilitar**|  
    |Excluir o elemento de código|**Excluir**|  
    |Mover o estilo para cima|**Mover para cima**|  
    |Mover o elemento de código para baixo|**Mover para baixo**|  
  
##  <a name="CopyLegend"></a> Copiar estilos de um mapa para outro  
  
1.  Verifique se o **legenda** caixa é exibida no mapa de código-fonte. Se não estiver visível, na barra de ferramentas do mapa, clique em **legenda**.  
  
2.  Abra o menu de atalho para o **legenda** caixa. Escolher **copiar legenda**.  
  
3.  Cole a legenda para o mapa de destino.  
  
##  <a name="MergeMaps"></a> Mesclar mapas de código  
 Você pode mesclar mapas, copiando e colando os elementos de código entre mapas. Se os identificadores de elemento de código corresponderem, funções de elementos de código de colá-lo como uma operação de mesclagem. Para facilitar essa tarefa, coloque todos os assemblies ou binários que você deseja visualizar na mesma pasta para que o caminho completo de cada assembly ou binário seja o mesmo para cada mapa que você deseja mesclar.  
  
 Como alternativa, você pode arrastar esses assemblies ou binários ao mesmo mapa nessa pasta.  
  
## <a name="see-also"></a>Consulte também  
 [Mapear dependências em suas soluções](../modeling/map-dependencies-across-your-solutions.md)   
 [Usar mapas de códigos para depurar seus aplicativos](../modeling/use-code-maps-to-debug-your-applications.md)   
 [Localizar possíveis problemas usando analisadores de mapa de código](../modeling/find-potential-problems-using-code-map-analyzers.md)   
 [Personalizar mapa de códigos editando os arquivos DGML](../modeling/customize-code-maps-by-editing-the-dgml-files.md)   
 [Referência DGML (Directed Graph Markup Language)](../modeling/directed-graph-markup-language-dgml-reference.md)