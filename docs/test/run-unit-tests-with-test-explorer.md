---
title: Executar e executar testes de unidade com o Gerenciador de Testes
description: Saiba como executar testes com o Gerenciador de Testes no Visual Studio. Este tópico aborda como habilitar execuções de teste automáticas após o build, exibir resultados do teste, agrupar e filtrar a lista de testes, criar playlists, depurar testes e usar atalhos de teste.
ms.date: 07/29/2019
ms.topic: how-to
f1_keywords:
- vs.unittesting.testexplorer.overview
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 35bd6f26b56ea7c3a1d578e5721504a91f60b74c
ms.sourcegitcommit: 46547f0bf3fc1a81e1a906762106dec5855e6e4a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86156826"
---
# <a name="run-unit-tests-with-test-explorer"></a>Executar testes de unidade com o Gerenciador de Testes

Use o Gerenciador de Testes para executar testes de unidade do Visual Studio ou projetos de teste de unidade de terceiros. Você também pode usar o Gerenciador de Testes para agrupar os testes em categorias, filtrar a lista de testes, criar, salvar e executar playlists de testes. É possível depurar testes e analisar um teste de desempenho e cobertura de código.

O Visual Studio instala as estruturas de teste de unidade da Microsoft para código gerenciado e nativo. No entanto, o Gerenciador de Testes também pode executar qualquer estrutura de teste de unidade que implementou um adaptador de Gerenciador de Testes. Para obter mais informações sobre como instalar estruturas de teste de unidade de terceiros, consulte [Instalar estruturas de teste de unidade de terceiros](../test/install-third-party-unit-test-frameworks.md)

O **Gerenciador de testes** pode executar testes de vários projetos de teste em uma solução e de classes de teste que fazem parte dos projetos de código de produção. Projetos de teste podem usar estruturas de teste de unidade diferente. Quando o código em teste é escrito para o .NET, o projeto de teste pode ser escrito em qualquer linguagem que também seja direcionada ao .NET, independentemente da linguagem do código de destino. Projetos de código C/C++ nativos devem ser testados usando uma estrutura de teste de unidade C++. Para obter mais informações, confira [Escrever testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md).

## <a name="run-tests-in-test-explorer"></a>Executar testes de unidade no Gerenciador de Testes

Quando você [cria o projeto de teste](../test/getting-started-with-unit-testing.md), os testes aparecem no Gerenciador de testes. Se o Gerenciador de Testes não estiver visível, escolha **Teste** no menu do Visual Studio, **Windows** e, em seguida, **Gerenciador de Testes**.

::: moniker range="vs-2017"
![Gerenciador de Testes de Unidade](../test/media/ute_failedpassednotrunsummary.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Gerenciador de Testes](../test/media/vs-2019/test-explorer-16-2.png)
::: moniker-end

::: moniker range="vs-2017"
Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados nos grupos padrão de **Testes com Falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. Você pode alterar a forma como o Gerenciador de Testes agrupa seus testes.
::: moniker-end
::: moniker range=">=vs-2019"
À medida que você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados em um agrupamento padrão de **Projeto**, **Namespace** e **Classe**. Você pode alterar a forma como o Gerenciador de Testes agrupa seus testes.
::: moniker-end

Você pode executar a maior parte do trabalho de encontrar, organizar e executar testes usando a barra de ferramentas do **Gerenciador de Testes**.

::: moniker range="vs-2017"
![Executar testes na barra de ferramentas do Gerenciador de Testes](../test/media/ute_toolbar.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Executar testes na barra de ferramentas do Gerenciador de Testes](../test/media/vs-2019/test-explorer-toolbar-diagram-16-2.png)
::: moniker-end

### <a name="run-tests"></a>Executar testes

::: moniker range="vs-2017"
Você pode executar todos os testes na solução, todos os testes em um grupo ou um conjunto de testes que você selecionar. Realize um dos seguintes procedimentos:

- Para executar todos os testes em uma solução, escolha **Executar Todos**.

- Para executar todos os testes em um grupo padrão, escolha **Executar** e, em seguida, escolha o grupo no menu.

- Selecione os testes individuais que deseja executar, abra o menu do clique com o botão direito para o teste selecionado e, em seguida, escolha **Executar Testes Selecionados**.

- Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o ![UTE&#95;parallelicon&#45;small](../test/media/ute_parallelicon-small.png) botão de alternância na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.

A **barra de aprovação/reprovação** na parte superior da janela do **Gerenciador de Testes** é animada conforme os testes são executados. Na conclusão da execução de teste, a **barra de aprovação/reprovação** ficará verde se todos os testes forem aprovados ou vermelha se algum deles for reprovado.
::: moniker-end
::: moniker range=">=vs-2019"
Você pode executar todos os testes na solução, todos os testes em um grupo ou um conjunto de testes que você selecionar. Realize um dos seguintes procedimentos:

- Para executar todos os testes de uma solução, escolha o ícone **Executar Todos**.

- Para executar todos os testes de um grupo padrão, escolha o ícone **Executar** e, em seguida, escolha o grupo no menu.

- Selecione os testes individuais que deseja executar, abra o menu do clique com o botão direito para o teste selecionado e, em seguida, escolha **Executar Testes Selecionados**.

- Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo no menu de configurações da barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.
::: moniker-end

### <a name="run-tests-after-every-build"></a>Executar testes depois de cada compilação
::: moniker range="vs-2017"
|Botão|Descrição|
|-|-|
|![Executar após o build](../test/media/ute_runafterbuild_btn.png)|Para executar os testes de unidade após cada build local, escolha **Teste** no menu padrão e, em seguida, **Executar Testes após Build** na barra de ferramentas do **Gerenciador de Testes**.|

> [!NOTE]
> Executar testes de unidade após cada build requer o Visual Studio 2017 Enterprise ou o Visual Studio 2019. No Visual Studio 2019, ele é incluído nas edições Community, Professional e Enterprise.
::: moniker-end
::: moniker range=">=vs-2019"
Para executar os testes de unidade após cada build local, abra o ícone de configurações na barra de ferramentas do Gerenciador de Testes e selecione **Executar Testes após Build**.
::: moniker-end

## <a name="view-test-results"></a>Exibir resultados do teste

Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados em grupos **Testes com falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. O painel de detalhes na parte inferior ou lateral do Gerenciador de Testes exibe um resumo da execução de teste.

### <a name="view-test-details"></a>Exibir detalhes do teste

Para exibir os detalhes de um teste individual, selecione o teste.

::: moniker range="vs-2017"
![Detalhes da execução do teste](../test/media/ute_testdetails.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Detalhes da execução do teste](../test/media/vs-2019/test-explorer-detail.png)
::: moniker-end

O painel de detalhes de teste exibe as seguintes informações:

- O nome do arquivo de origem e o número de linha do método de teste.

- O status do teste.

- O tempo decorrido que o método de teste levou para ser executado.

Se o teste falhar, o painel de detalhes também exibe:

- A mensagem retornada pela estrutura de teste de unidade para o teste.

- O rastreamento de pilha no momento em que o teste falhou.

### <a name="view-the-source-code-of-a-test-method"></a>Exibir o código-fonte de um método de teste

Para exibir o código-fonte de um método de teste no editor do Visual Studio, selecione o teste e, em seguida, escolha **abrir teste** no menu do botão direito do mouse (teclado: **F12**).

## <a name="group-and-filter-the-test-list"></a>Agrupar e filtrar a lista de testes

O Gerenciador de Testes permite agrupar os testes em categorias predefinidas. A maioria das estruturas de teste de unidade executados no Gerenciador de Testes permitem que você defina suas próprias categorias e pares de valor/categoria para agrupar os testes. Você também pode filtrar a lista de testes por correspondência de cadeias de caracteres em relação a propriedades de teste.

### <a name="group-tests-in-the-test-list"></a>Agrupar testes na lista de testes

::: moniker range="vs-2017"
Para alterar a maneira como os testes são organizados, escolha a seta para baixo ao lado do botão **Agrupar por**![botão de grupo do Gerenciador de Testes](../test/media/ute_groupby_btn.png) e selecione novos critérios de agrupamento.

![Agrupar testes por categoria no Gerenciador de Testes](../test/media/ute_groupbycategory.png)
::: moniker-end
::: moniker range=">=vs-2019"
O Gerenciador de Testes permite agrupar os testes em uma hierarquia. O agrupamento de hierarquia padrão é **Projeto**, **Namespace** e, em seguida, **Classe**. Para alterar a maneira como os testes são organizados, escolha o botão **Agrupar por**![botão de grupo do Gerenciador de Testes](../test/media/ute_groupby_btn.png) e selecione novos critérios de agrupamento.

![Agrupar testes por categoria no Gerenciador de Testes](../test/media/vs-2019/test-explorer-groupby-162.png)

Você pode definir seus próprios níveis de hierarquia e de grupo por **Estado** e, em seguida, **Classe**, por exemplo, selecionando as opções Agrupar por em sua ordem preferida.

![Agrupar por Estado e, em seguida, Classe](../test/media/vs-2019/test-explorer-groupby-state-16-2.png)
::: moniker-end

### <a name="test-explorer-groups"></a>Grupos de Gerenciador de Testes

::: moniker range="vs-2017"
|Grupo|Descrição|
|-|-----------------|
|**Duration**|Agrupa teste pelo tempo de execução: **rápido**, **médio** e **lento**.|
|**Resultado**|Agrupa testes por resultados da execução: **testes com falha**, **testes ignorados**, **testes aprovados**.|
|**Características**|Agrupa teste por pares de categoria/valor que você define. A sintaxe para especificar valores e categorias de característica é definida pela estrutura de teste de unidade.|
|**Projeto**|Agrupa teste por nome dos projetos.|
::: moniker-end
::: moniker range=">=vs-2019"
|Grupo|Descrição|
|-|-----------------|
|**Duration**|Agrupa testes por tempo de execução: **rápido**, **médio**e **lento**.|
|**State**|Agrupa testes por resultados de execução: **testes com falha**, **testes ignorados**, **testes aprovados**, **não executados**|
|**Estrutura de destino** | Agrupa testes pela estrutura de seus projetos de destino |
|**Namespace**|Agrupa testes pelo namespace contido.|
|**Projeto**|Agrupa testes pelo projeto contido.|
|**Classe**|Agrupa testes pela classe contida.|
::: moniker-end

### <a name="traits"></a>Características

Uma característica é geralmente um par de nome/valor de categoria, mas também pode ser uma única categoria. Características podem ser atribuídas aos métodos que são identificados como um método de teste pela estrutura de teste de unidade. Uma estrutura de teste de unidade pode definir categorias de característica. Você pode adicionar valores para as categorias de característica para definir seus próprios pares de nome/valor de categoria. A sintaxe para especificar valores e categorias de característica é definida pela estrutura de teste de unidade.

**Características na Estrutura de Teste da Unidade Microsoft para código gerenciado**

Na estrutura de teste de unidade da Microsoft para aplicativos gerenciados, você define um par nome/valor de característica no atributo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>. A estrutura de teste também contém essas características predefinidas:

|Característica|Descrição|
|-|-----------------|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.OwnerAttribute>|A categoria do proprietário é definida pela estrutura de teste de unidade e exige que você forneça um valor de cadeia de caracteres do proprietário.|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.PriorityAttribute>|A categoria Prioridade é definida pela estrutura de teste de unidade e exige que você forneça um valor inteiro da prioridade.|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCategoryAttribute>|O atributo TestCategory permite que você forneça uma categoria sem um valor.|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>|O atributo TestProperty permite que você defina o par de categoria/valor da característica.|


**Características na Estrutura de Teste da Unidade Microsoft para C++**

Consulte [Como usar o Microsoft Unit Testing Framework para C++](how-to-use-microsoft-test-framework-for-cpp.md).

## <a name="create-custom-playlists"></a>Criar playlists personalizadas

::: moniker range="vs-2017"
É possível criar e salvar uma lista de teste que você deseje executar ou exibir como um grupo. Quando você seleciona uma playlist, os testes na lista são exibidos no Gerenciador de Testes. É possível adicionar um teste a mais de uma lista de reprodução e todos os testes no projeto estarão disponíveis quando você escolher a lista de reprodução **Todos os Testes**.

![Escolher uma playlist](../test/media/ute_playlist.png)

**Para criar uma lista de reprodução**, escolha um ou mais testes no Gerenciador de Testes. No menu do clique com o botão direito do mouse, escolha **Adicionar à lista de reprodução**  >  **NewPlaylist**. Salve o arquivo com o nome e local que você especificar na caixa de diálogo **Criar nova lista de reprodução**.

**Para adicionar testes a uma lista de reprodução**, escolha um ou mais testes no Gerenciador de Testes. No menu do clique com o botão direito, escolha **Adicionar à Lista de Reprodução** e, em seguida, escolha a lista de reprodução à qual deseja adicionar os testes.

**Para abrir uma playlist**, escolha **Teste** > **Playlist** no menu do Visual Studio e escolha uma opção na lista de playlists usadas recentemente ou escolha **Abrir Playlist** para especificar o nome e o local da playlist.

Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o ![UTE&#95;parallelicon&#45;small](../test/media/ute_parallelicon-small.png) botão de alternância na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.
::: moniker-end
::: moniker range=">=vs-2019"
É possível criar e salvar uma lista de teste que você deseje executar ou exibir como um grupo. Quando você seleciona uma playlist, os testes na lista são exibidos em uma nova guia do Gerenciador de testes. Você pode adicionar um teste a mais de uma lista de reprodução.

**Para criar uma lista de reprodução**, escolha um ou mais testes no Gerenciador de Testes. No menu do clique com o botão direito do mouse, escolha **Adicionar à lista de**reprodução nova lista de reprodução  >  **New Playlist**.

![Criar uma playlist](../test/media/vs-2019/test-explorer-playlist-16-2.png)

A lista de reprodução é aberta em uma nova guia do Gerenciador de testes. Você pode usar essa playlist uma vez e descartá-la, ou pode clicar no botão **salvar** na barra de ferramentas da janela da lista de reprodução e, em seguida, selecionar um nome e um local para salvar a lista de reprodução.

![A playlist é aberta em uma guia separada do Gerenciador de Testes](../test/media/vs-2019/test-explorer-playlist-tab-16-7.png)

**Para criar uma lista de reprodução**, escolha um ou mais testes no Gerenciador de Testes. Clique com o botão direito do mouse e escolha **Adicionar à lista de**reprodução nova lista de reprodução  >  **New playlist**.

**Para abrir uma playlist**, escolha o ícone da playlist na barra de ferramentas do Visual Studio e selecione no menu um arquivo de playlist salvo anteriormente.

**Para editar uma lista de reprodução**, você pode clicar com o botão direito do mouse em qualquer teste e usar as opções de menu para adicioná-lo ou removê-lo de uma lista de reprodução.

A partir do Visual Studio 2019 versão 16,7, você pode escolher o botão **Editar** na barra de ferramentas. As caixas de seleção serão exibidas ao lado de seus testes mostrando quais testes são incluídos e excluídos na playlist. Edite os grupos conforme desejado.

![Botão Editar playlist](../test/media/vs-2019/test-explorer-playlist-edit-16-7.png)

Você também pode marcar ou desmarcar as caixas dos grupos pai na hierarquia. Essa ação cria uma lista de reprodução dinâmica que sempre atualiza a lista de reprodução com base nos testes que estão nesse grupo. Por exemplo, se você posicionar uma marca de seleção ao lado de uma classe, qualquer teste adicionado dessa classe se tornará parte dessa lista de reprodução. Se você excluir um teste dessa classe, ele será removido da lista de reprodução. Você pode saber mais sobre as regras salvando a lista de reprodução com o botão salvar na barra de ferramentas e abrindo o arquivo *. playlist* criado no disco. Esse arquivo lista todas as regras e testes individuais que compõem uma lista de reprodução.

![Arquivo XML de playlist](../test/media/vs-2019/test-explorer-playlist-xml-file.png)
::: moniker-end

::: moniker range=">=vs-2019"
### <a name="test-explorer-columns"></a>Colunas do Gerenciador de Testes

Os [grupos](#test-explorer-groups) também estão disponíveis como colunas no Gerenciador de Testes, com a Característica, Rastreamento de Pilha, Mensagem de Erro e Nome Totalmente Qualificado. A maioria das colunas não fica visível por padrão, e você pode personalizar quais colunas verá e a ordem de exibição.

![Agrupar por Estado e, em seguida, Classe](../test/media/vs-2019/test-explorer-columns-16-2.png)

### <a name="filter-sort-and-rearrange-test-columns"></a>Filtrar, classificar e reorganizar colunas de testes

É possível filtrar, classificar e reorganizar as colunas.
* Para filtrar para características específicas, clique no ícone de filtro na parte superior da coluna Características.

  ![Filtro de coluna](../test/media/vs-2019/test-explorer-filter-column-16-2.png)

* Para alterar a ordem das colunas, clique no cabeçalho de uma coluna e arraste-o para a esquerda ou para a direita.

* Para classificar uma coluna, clique no cabeçalho dessa coluna. Nem todas as colunas podem ser classificadas. Faça também a classificação por uma coluna secundária mantendo a tecla **Shift** pressionada e clicando em um cabeçalho de coluna adicional.

  ![Classificação de coluna](../test/media/vs-2019/test-explorer-sort-column-16-2.png)
::: moniker-end

## <a name="search-and-filter-the-test-list"></a>Pesquisar e filtrar a lista de testes

Você também pode usar os filtros de pesquisa do Gerenciador de Testes para limitar os métodos de testes nos projetos que você exibe e executa.

Quando você digita uma cadeia de caracteres na caixa de pesquisa do **Gerenciador de Testes** e escolhe **Enter**, a lista de testes é filtrada para exibir somente os testes cujos nomes totalmente qualificados contêm a cadeia de caracteres.

Para filtrar por um critério diferente:

1. Abra a lista suspensa à direita da caixa de pesquisa.

2. Escolha um novo critério.

3. Insira o valor do filtro entre aspas. Caso deseje pesquisar uma correspondência exata na cadeia de caracteres em vez de uma correspondência que contenha um dos nomes, use um sinal de igual (=) em vez dos dois-pontos (:).

::: moniker range="vs-2017"
![Filtrar testes no Gerenciador de Testes](../test/media/ute_filtertestlist.png)
::: moniker-end
::: moniker range=">=vs-2019"
![Filtrar testes no Gerenciador de Testes](../test/media/vs-2019/test-explorer-search-filter-16-2.png)
::: moniker-end

> [!NOTE]
> As pesquisas não diferenciam maiúsculas de minúsculas e correspondem a cadeia especificada para qualquer parte do valor de critérios.

::: moniker range="vs-2017"
|Qualificador|Descrição|
|-|-----------------|
|**Característica**|Procura categoria de característica e valor para correspondência. A sintaxe para especificar valores e categorias de característica é definida pela estrutura de teste de unidade.|
|**Projeto**|Procura os nomes de projeto de teste para correspondências.|
|**Mensagem de erro**|Procura nas mensagens de erro definidas pelo usuário retornadas por falhas para encontrar correspondências.|
|**Caminho do arquivo**|Procura o nome de arquivo totalmente qualificado dos arquivos de origem do teste para encontrar correspondências.|
|**Nome Totalmente Qualificado**|Pesquisa o nome totalmente qualificado de namespaces de teste, classes e métodos para encontrar correspondências.|
|**Saída**|Procura as mensagens de erro definidas pelo usuário que são gravadas para a saída padrão (stdout) ou erro padrão (stderr). A sintaxe para especificar mensagens de saúde é definida pela estrutura de teste de unidade.|
|**Resultado**|Procura os nomes de categoria do Gerenciador de Testes para encontrar correspondências: **testes com falha**, **testes ignorados**, **testes aprovados**.|
::: moniker-end
::: moniker range=">=vs-2019"
|Qualificador|Descrição|
|-|-----------------|
|**State**|Procura os nomes de categoria do Gerenciador de Testes para encontrar correspondências: **testes com falha**, **testes ignorados**, **testes aprovados**.|
|**Características**|Procura categoria de característica e valor para correspondência. A sintaxe para especificar valores e categorias de característica é definida pela estrutura de teste de unidade.|
|**Nome Totalmente Qualificado**|Pesquisa o nome totalmente qualificado de namespaces de teste, classes e métodos para encontrar correspondências.|
|**Projeto**|Procura os nomes de projeto de teste para correspondências.|
|**Estrutura de destino**|Procura os nomes de categoria do Gerenciador de Testes para encontrar correspondências: **testes com falha**, **testes ignorados**, **testes aprovados**.|
|**Namespace**|Pesquisa os namespaces de teste para encontrar correspondências.|
|**Classe**|Pesquisa os nomes de classes de teste para encontrar correspondências.|
::: moniker-end

Para excluir um subconjunto dos resultados de um filtro, use a seguinte sintaxe:

```
FilterName:"Criteria" -FilterName:"SubsetCriteria"
```

Por exemplo, `FullName:"MyClass" - FullName:"PerfTest"` retorna todos os testes que incluem "MyClass" em seu nome, exceto os testes que também incluem "PerfTest" em seu nome.

## <a name="debug-and-analyze-unit-tests"></a>Depurar e analisar testes de unidade

Você pode usar o Gerenciador de Testes para iniciar uma sessão de depuração para os testes. Passar pelo código com o depurador do Visual Studio permite-lhe navegar facilmente entre os testes de unidade e o projeto sendo testado. Para iniciar a depuração:

1. No editor do Visual Studio, defina um ponto de interrupção em um ou mais métodos de teste que deseje depurar.

    > [!NOTE]
    > Como os métodos de teste podem ser executados em qualquer ordem, defina pontos de interrupção em todos os métodos de teste que deseje depurar.

2. No Gerenciador de Testes, selecione os métodos de teste e, em seguida, escolha **Depurar Testes Selecionados** no menu do clique com o botão direito.

   Para obter mais informações sobre o depurador, confira [Depuração no Visual Studio](../debugger/debugger-feature-tour.md).

### <a name="diagnose-test-method-performance-issues"></a>Diagnosticar problemas de desempenho do método de teste

Para diagnosticar por que um método de teste está demorando para ser executado, selecione o método no Gerenciador de Testes e, em seguida, escolha **Analisar o Teste Selecionado** no menu de clique com o botão direito. Consulte [relatório de criação de perfil de instrumentação](../profiling/understanding-instrumentation-data-values.md?view=vs-2017).

### <a name="analyze-unit-test-code-coverage"></a>Analisar a cobertura de código de teste de unidade

É possível determinar a quantidade do código de produto que realmente está sendo testada por seus testes de unidade com a ferramenta de cobertura de código do Visual Studio que está disponível na edição Enterprise do Visual Studio. Você pode executar a cobertura de código em testes selecionados ou em todos os testes em uma solução.

Para executar a cobertura de código para métodos de teste em uma solução:

::: moniker range="vs-2017"

1. Escolha **Testes** na barra de menus superior e, em seguida, escolha **Analisar cobertura de código**.

2. Escolha um dos seguintes comandos do submenu:

    - **Testes selecionados** executa os métodos de teste que você selecionou no Gerenciador de Testes.

    - **Todos os testes** executa todos os métodos de teste na solução.

::: moniker-end

::: moniker range=">=vs-2019"

* Clique com o botão direito do mouse no Gerenciador de testes e selecione **analisar cobertura de código para testes selecionados**

::: moniker-end

A janela **Resultados da Cobertura de Código** exibe o percentual dos blocos de código de produto que foram exercidos por linha, função, classe, namespace e módulo.

Para obter mais informações, confira [Usar a cobertura de código para determinar quanto do código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).

## <a name="test-shortcuts"></a>Atalhos de teste

Os testes podem ser executados no Gerenciador de testes clicando com o botão direito do mouse no editor de código em um teste e selecionando **Executar teste** ou usando os atalhos padrão do [Gerenciador de testes](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_testexplorerGLOBAL) no Visual Studio. Alguns dos atalhos são baseados em contexto. Isso significa que eles executam ou depuram testes com base em onde o cursor está no editor de código. Se o cursor estiver dentro de um método de teste, esse método de teste será executado. Se o cursor estiver no nível de classe, todos os testes na classe serão executados. O mesmo vale para o nível do namespace.

|Comandos frequentes| Atalhos do teclado|
|-|------------------------|
|TestExplorer.DebugAllTestsInContext|**Ctrl** + **R**, **Ctrl** + **T**|
|TestExplorer.RunAllTestsInContext|**Ctrl** + **R**, **T**|
|TestExplorer.RunAllTests|**Ctrl** + **R**, **A**|
|TestExplorer.RepeatLastRun|**Ctrl** + **R**, **L**|

> [!NOTE]
> Não é possível executar um teste em uma classe abstrata, porque os testes são apenas definidos nas classes abstratas e não instanciados. Para executar testes em classes abstratas, crie uma classe que deriva da classe abstrata.

## <a name="see-also"></a>Veja também

- [Teste de unidade em seu código](../test/unit-test-your-code.md)
- [Executar um teste de unidade como um processo de 64 bits](../test/run-a-unit-test-as-a-64-bit-process.md)
- [Perguntas Frequentes sobre o Gerenciador de Testes](test-explorer-faq.md)
