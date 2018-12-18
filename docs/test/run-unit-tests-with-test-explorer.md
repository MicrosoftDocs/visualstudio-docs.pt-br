---
title: Executar, criar e depurar testes de unidade com o Gerenciador de Testes
description: Saiba como executar testes com o Gerenciador de Testes no Visual Studio. Este tópico aborda como habilitar execuções de teste automáticas após o build, exibir resultados do teste, agrupar e filtrar a lista de testes, criar playlists, depurar testes e usar atalhos de teste.
ms.date: 11/04/2016
ms.prod: visual-studio-dev15
ms.technology: vs-ide-test
ms.topic: conceptual
f1_keywords:
- vs.unittesting.testexplorer.overview
ms.author: gewarren
manager: douge
ms.workload:
- multiple
author: gewarren
ms.openlocfilehash: dc918adb6a66f64cdcda46ea535cd0ab017c0676
ms.sourcegitcommit: 240c8b34e80952d00e90c52dcb1a077b9aff47f6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2018
ms.locfileid: "49939494"
---
# <a name="run-unit-tests-with-test-explorer"></a>Executar testes de unidade com o Gerenciador de Testes

Use o **Gerenciador de Testes** para executar testes de unidade do Visual Studio ou projetos de teste de unidade de terceiros. Você também pode usar o **Gerenciador de Testes** para agrupar os testes em categorias, filtrar a lista de testes, criar, salvar e executar playlists de testes. É possível depurar testes e analisar um teste de desempenho e cobertura de código.

O Visual Studio instala as estruturas de teste de unidade da Microsoft para código gerenciado e nativo. No entanto, o **Gerenciador de Testes** também pode executar qualquer estrutura de teste de unidade que implementou um adaptador de Gerenciador de Testes. Para obter mais informações sobre como instalar estruturas de teste de unidade de terceiros, consulte [Instalar estruturas de teste de unidade de terceiros](../test/install-third-party-unit-test-frameworks.md)

O **Gerenciador de Testes** pode executar testes de vários projetos de teste em uma solução e de classes de teste que fazem parte dos projetos de código de produção. Projetos de teste podem usar estruturas de teste de unidade diferente. Quando o código em teste é escrito para o .NET Framework, o projeto de teste pode ser escrito em qualquer linguagem que tem como alvo o .NET Framework, independentemente do idioma de código de destino. Projetos de código C/C++ nativos devem ser testados usando uma estrutura de teste de unidade C++. Para obter mais informações, confira [Escrever testes de unidade para C/C++](writing-unit-tests-for-c-cpp.md).

## <a name="run-tests-in-test-explorer"></a>Executar testes de unidade no Gerenciador de Testes

Quando você compila o projeto de teste, os testes são exibidos no Gerenciador de Testes. Se o Gerenciador de Testes não estiver visível, escolha **Teste** no menu do Visual Studio, escolha **Windows** e, em seguida, escolha **Gerenciador de Testes**.

![Gerenciador de Testes de Unidade](../test/media/ute_failedpassednotrunsummary.png)

Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados nos grupos padrão de **Testes com Falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. Você pode alterar a forma como o Gerenciador de Testes agrupa seus testes.

Você pode executar a maior parte do trabalho de encontrar, organizar e executar testes usando a barra de ferramentas do **Gerenciador de Testes**.

![Executar testes na barra de ferramentas do Gerenciador de Testes](../test/media/ute_toolbar.png)

### <a name="run-tests"></a>Executar testes

Você pode executar todos os testes na solução, todos os testes em um grupo ou um conjunto de testes que você selecionar. Realize um dos seguintes procedimentos:

- Para executar todos os testes em uma solução, escolha **Executar Todos**.

- Para executar todos os testes em um grupo padrão, escolha **Executar** e, em seguida, escolha o grupo no menu.

- Selecione os testes individuais que deseja executar, abra o menu de contexto para um teste selecionado e escolha **Executar Testes Selecionados**.

- Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o ![UTE&#95;parallelicon&#45;small](../test/media/ute_parallelicon-small.png) botão de alternância na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.

A **barra de aprovação/reprovação** na parte superior da janela do **Gerenciador de Testes** é animada conforme os testes são executados. Na conclusão da execução de teste, a **barra de aprovação/reprovação** ficará verde se todos os testes forem aprovados ou vermelha se algum deles for reprovado.

### <a name="run-tests-after-every-build"></a>Executar testes depois de cada compilação

|Botão|Descrição|
|-|-|
|![Executar após o build](../test/media/ute_runafterbuild_btn.png)|Para executar os testes de unidade após cada build local, escolha **Teste** no menu padrão e, em seguida, **Executar Testes após Build** na barra de ferramentas do **Gerenciador de Testes**.|

## <a name="view-test-results"></a>Exibir resultados do teste

Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados em grupos **Testes com falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. O painel de detalhes na parte inferior do Gerenciador de Testes exibe um resumo da execução de teste.

### <a name="view-test-details"></a>Exibir detalhes do teste

Para exibir os detalhes de um teste individual, selecione o teste.

![Detalhes da execução do teste](../test/media/ute_testdetails.png)

O painel de detalhes de teste exibe as seguintes informações:

- O nome do arquivo de origem e o número de linha do método de teste.

- O status do teste.

- O tempo decorrido que o método de teste levou para ser executado.

Se o teste falhar, o painel de detalhes também exibe:

- A mensagem retornada pela estrutura de teste de unidade para o teste.

- O rastreamento de pilha no momento em que o teste falhou.

### <a name="view-the-source-code-of-a-test-method"></a>Exibir o código-fonte de um método de teste

 Para exibir o código-fonte para um método de teste no editor do Visual Studio, selecione o teste e, em seguida, escolha **Abrir teste** no menu de contexto (teclado: **F12**).

## <a name="group-and-filter-the-test-list"></a>Agrupar e filtrar a lista de testes

O Gerenciador de Testes permite agrupar os testes em categorias predefinidas. A maioria das estruturas de teste de unidade executados no Gerenciador de Testes permitem que você defina suas próprias categorias e pares de valor/categoria para agrupar os testes. Você também pode filtrar a lista de testes por correspondência de cadeias de caracteres em relação a propriedades de teste.

### <a name="group-tests-in-the-test-list"></a>Agrupar testes na lista de testes

 Para alterar a maneira como os testes são organizados, escolha a seta para baixo ao lado do botão **Agrupar por** ![botão de grupo do Gerenciador de Testes](../test/media/ute_groupby_btn.png) e selecione novos critérios de agrupamento.

 ![Agrupar testes por categoria no Gerenciador de Testes](../test/media/ute_groupbycategory.png)

### <a name="test-explorer-groups"></a>Grupos de Gerenciador de Testes

|Grupo|Descrição|
|-|-----------------|
|**Duração**|Agrupa teste pelo tempo de execução: **rápido**, **médio** e **lento**.|
|**Resultado**|Agrupa testes por resultados da execução: **testes com falha**, **testes ignorados**, **testes aprovados**.|
|**Características**|Agrupa teste por pares de categoria/valor que você define. A sintaxe para especificar valores e categorias de característica é definida pela estrutura de teste de unidade.|
|**Projeto**|Agrupa teste por nome dos projetos.|

### <a name="group-by-traits"></a>Agrupar por características

 Uma característica é geralmente um par de nome/valor de categoria, mas também pode ser uma única categoria. Características podem ser atribuídas aos métodos que são identificados como um método de teste pela estrutura de teste de unidade. Uma estrutura de teste de unidade pode definir categorias de característica. Você pode adicionar valores para as categorias de característica para definir seus próprios pares de nome/valor de categoria. A sintaxe para especificar valores e categorias de característica é definida pela estrutura de teste de unidade.

 **Características na Estrutura de Teste da Unidade Microsoft para código gerenciado**

 Na estrutura de teste de unidade da Microsoft para aplicativos gerenciados, você define um par nome/valor de característica no atributo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>. A estrutura de teste também contém essas características predefinidas:

|Característica|Descrição|
|-|-----------------|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.OwnerAttribute>|A categoria do proprietário é definida pela estrutura de teste de unidade e exige que você forneça um valor de cadeia de caracteres do proprietário.|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.PriorityAttribute>|A categoria Prioridade é definida pela estrutura de teste de unidade e exige que você forneça um valor inteiro da prioridade.|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCategoryAttribute>|O atributo TestCategory permite que você forneça uma categoria sem um valor. Uma categoria definida pelo atributo TestCategory também pode ser a categoria de um atributo TestProperty.|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>|O atributo TestProperty permite que você defina o par de categoria/valor da característica.|

 **Características na Estrutura de Teste da Unidade da Microsoft para C++** Consulte [Como usar a Estrutura de Teste da Unidade da Microsoft para C++](how-to-use-microsoft-test-framework-for-cpp.md).

### <a name="search-and-filter-the-test-list"></a>Pesquisar e filtrar a lista de testes

Você pode usar o Gerenciador de Testes filtros para limitar os métodos de teste em seus projetos que você exibe e executa.

Quando você digita uma cadeia de caracteres na caixa de pesquisa do **Gerenciador de Testes** e escolhe **Enter**, a lista de testes é filtrada para exibir somente os testes cujos nomes totalmente qualificados contêm a cadeia de caracteres.

Para filtrar por um critério diferente:

1. Abra a lista suspensa à direita da caixa de pesquisa.

2. Escolha um novo critério.

3. Insira o valor do filtro entre aspas.

![Filtrar testes no Gerenciador de Testes](../test/media/ute_filtertestlist.png)

> [!NOTE]
> As pesquisas não diferenciam maiúsculas de minúsculas e correspondem a cadeia especificada para qualquer parte do valor de critérios.

|Qualificador|Descrição|
|-|-----------------|
|**Característica**|Procura categoria de característica e valor para correspondência. A sintaxe para especificar valores e categorias de característica é definida pela estrutura de teste de unidade.|
|**Projeto**|Procura os nomes de projeto de teste para correspondências.|
|**Mensagem de erro**|Procura nas mensagens de erro definidas pelo usuário retornadas por falhas para encontrar correspondências.|
|**Caminho do arquivo**|Procura o nome de arquivo totalmente qualificado dos arquivos de origem do teste para encontrar correspondências.|
|**Nome Totalmente Qualificado**|Procura o nome de arquivo totalmente qualificado dos namespaces de teste, classes e métodos para encontrar correspondências.|
|**Saída**|Procura as mensagens de erro definidas pelo usuário que são gravadas para a saída padrão (stdout) ou erro padrão (stderr). A sintaxe para especificar mensagens de saúde é definida pela estrutura de teste de unidade.|
|**Resultado**|Procura os nomes de categoria do Gerenciador de Testes para encontrar correspondências: **testes com falha**, **testes ignorados**, **testes aprovados**.|

Para excluir um subconjunto dos resultados de um filtro, use a seguinte sintaxe:

```cpp
FilterName:"Criteria" -FilterName:"SubsetCriteria"
```

Por exemplo, `FullName:"MyClass" - FullName:"PerfTest"` retorna todos os testes que incluem "MyClass" em seu nome, exceto os testes que também incluem "PerfTest" em seu nome.

## <a name="create-custom-playlists"></a>Criar playlists personalizadas

 É possível criar e salvar uma lista de teste que você deseje executar ou exibir como um grupo. Quando você seleciona uma playlist, os testes na lista são exibidos no Gerenciador de Testes. É possível adicionar um teste a mais de uma lista de reprodução e todos os testes no projeto estarão disponíveis quando você escolher a lista de reprodução **Todos os Testes**.

 ![Escolher uma playlist](../test/media/ute_playlist.png)

 **Para criar uma lista de reprodução**, escolha um ou mais testes no Gerenciador de Testes. No menu de contexto, escolha **Adicionar à Playlist** > **NewPlaylist**. Salve o arquivo com o nome e local que você especificar na caixa de diálogo **Criar nova lista de reprodução**.

 **Para adicionar testes a uma lista de reprodução**, escolha um ou mais testes no Gerenciador de Testes. No menu de contexto, escolha **Adicionar à lista de reprodução**e, em seguida, escolha a lista de reprodução que você deseja adicionar os testes.

 **Para abrir uma playlist**, escolha **Teste** > **Playlist** no menu do Visual Studio e escolha uma opção na lista de playlists usadas recentemente ou escolha **Abrir Playlist** para especificar o nome e o local da playlist.

 Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o ![UTE&#95;parallelicon&#45;small](../test/media/ute_parallelicon-small.png) botão de alternância na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.

## <a name="debug-and-analyze-unit-tests"></a>Depurar e analisar testes de unidade

### <a name="debug-unit-tests"></a>Depurar testes de unidade

Você pode usar o Gerenciador de Testes para iniciar uma sessão de depuração para os testes. Passar pelo código com o depurador do Visual Studio permite-lhe navegar facilmente entre os testes de unidade e o projeto sendo testado. Para iniciar a depuração:

1. No editor do Visual Studio, defina um ponto de interrupção em um ou mais métodos de teste que deseje depurar.

    > [!NOTE]
    > Como os métodos de teste podem ser executados em qualquer ordem, defina pontos de interrupção em todos os métodos de teste que deseje depurar.

2. No Gerenciador de Testes, selecione os métodos de teste e escolha **Depurar Testes Selecionados** no menu de contexto.

   Para obter mais informações sobre o depurador, confira [Depuração no Visual Studio](../debugger/debugging-in-visual-studio.md).

### <a name="diagnose-test-method-performance-issues"></a>Diagnosticar problemas de desempenho do método de teste

 Para diagnosticar o motivo pelo qual um método de teste leva muito tempo para ser executado, selecione o método no Gerenciador de Testes e, em seguida, escolha **Perfil** no menu de contexto. Consulte [Gerenciador de Desempenho](../profiling/performance-explorer.md).

### <a name="analyze-unit-test-code-coverage"></a>Analisar a cobertura de código de teste de unidade

Você pode determinar a quantidade de seu código de produto que realmente está sendo testado por seus testes de unidade usando a ferramenta de cobertura de código do Visual Studio. Você pode executar a cobertura de código em testes selecionados ou em todos os testes em uma solução.

Para executar a cobertura de código para métodos de teste em uma solução:

1. Escolha **Testes** no menu do Visual Studio e, em seguida, escolha **Analisar cobertura de código**.

2. Escolha um dos seguintes comandos do submenu:

    - **Testes selecionados** executa os métodos de teste que você selecionou no Gerenciador de Testes.

    - **Todos os testes** executa todos os métodos de teste na solução.

A janela **Resultados da Cobertura de Código** exibe o percentual dos blocos de código de produto que foram exercidos por linha, função, classe, namespace e módulo.

Para obter mais informações, confira [Usar a cobertura de código para determinar quanto do código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).

## <a name="test-shortcuts"></a>Atalhos de teste

Testes podem ser executados do **Gerenciador de Testes** clicando com o botão direito do mouse no editor de código em um teste e selecionando **Executar teste** ou usando os [Atalhos padrão do Gerenciador de Testes](../ide/default-keyboard-shortcuts-in-visual-studio.md#bkmk_testexplorerGLOBAL) no Visual Studio. Alguns dos atalhos são baseados em contexto. Isso significa que eles executam ou depuram testes com base em onde o cursor está no editor de código. Se o cursor estiver dentro de um método de teste, esse método de teste será executado. Se o cursor estiver no nível de classe, todos os testes na classe serão executados. O mesmo vale para o nível do namespace.

|Comandos frequentes| Atalhos de teclado|
|-|------------------------|
|TestExplorer.DebugAllTestsInContext|**Ctrl**+**R**, **Ctrl**+**T**|
|TestExplorer.RunAllTestsInContext|**Ctrl**+**R**, **T**|

> [!NOTE]
> Não é possível executar um teste em uma classe abstrata, porque os testes são apenas definidos nas classes abstratas e não instanciados. Para executar testes em classes abstratas, crie uma classe que deriva da classe abstrata.

## <a name="see-also"></a>Consulte também

- [Efetuar teste de unidade em seu código](../test/unit-test-your-code.md)
- [Executar um teste de unidade como um processo de 64 bits](../test/run-a-unit-test-as-a-64-bit-process.md)
