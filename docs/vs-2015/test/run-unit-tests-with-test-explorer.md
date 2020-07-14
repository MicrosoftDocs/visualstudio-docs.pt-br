---
title: Executar testes de unidade com o Gerenciador de Testes | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
f1_keywords:
- vs.unittesting.testexplorer.overview
ms.assetid: 91b167a3-280a-498b-8fc2-f67859a2c64e
caps.latest.revision: 29
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d6c6ebe39cf0d32480aee1019aa5ea47496bd793
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85548129"
---
# <a name="run-unit-tests-with-test-explorer"></a>Executar testes de unidade com o Gerenciador de Testes
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Use o Gerenciador de Testes para executar testes de unidade do Visual Studio ou projetos de teste de unidade de terceiros, agrupar testes em categorias, filtre a lista de testes, criar, salvar e executar as listas de reprodução de testes. Você também pode depurar testes e analisar um teste de desempenho e cobertura de código.

## <a name="contents"></a><a name="BKMK_Contents"></a>Índice
 [Estruturas de teste de unidade e projetos de teste](#BKMK_Unit_test_frameworks_and_test_projects)

 [Executar testes no Gerenciador de testes](#BKMK_Run_tests_in_Test_Explorer)

 [Exibir resultados de teste](#BKMK_View_test_results)

 [Agrupar e filtrar a lista de testes](#BKMK_Group_and_filter_the_test_list)

 [Criar listas de reprodução personalizadas](#BKMK_Create_custom_playlists)

 [Depurar e analisar testes de unidade](#BKMK_Debug_and_analyze_unit_tests)

 [Recursos externos](#BKMK_External_resources)

## <a name="unit-test-frameworks-and-test-projects"></a><a name="BKMK_Unit_test_frameworks_and_test_projects"></a>Estruturas de teste de unidade e projetos de teste
 O Visual Studio instala as estruturas de teste de unidade da Microsoft para código gerenciado e nativo. No entanto, o Gerenciador de Testes também pode executar qualquer estrutura de teste de unidade que implementou um adaptador de Gerenciador de Testes. Para obter mais informações sobre como instalar estruturas de teste de unidade de terceiros, consulte [Instalar estruturas de teste de unidade de terceiros](../test/install-third-party-unit-test-frameworks.md)

 O Gerenciador de Testes pode executar testes de vários projetos de teste em uma solução e de classes de teste que fazem parte dos projetos de código de produção. Projetos de teste podem usar estruturas de teste de unidade diferente. Quando o código em teste é escrito para o .NET Framework, o projeto de teste pode ser escrito em qualquer linguagem que tem como alvo o .NET Framework, independentemente do idioma de código de destino. Projetos de código C/C++ nativos devem ser testados usando uma estrutura de teste de unidade C++.

 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

## <a name="run-tests-in-test-explorer"></a><a name="BKMK_Run_tests_in_Test_Explorer"></a> Executar testes no Gerenciador de Testes
 [Executar Testes](#BKMK_Run_tests) **&#124;** [Executar testes após cada build](#BKMK_Run_tests_after_every_build)

 Quando você compila o projeto de teste, os testes são exibidos no Gerenciador de Testes. Se o Gerenciador de Testes não estiver visível, escolha **Teste** no menu do Visual Studio, **Windows** e, em seguida, **Gerenciador de Testes**.

 ![Gerenciador de Testes de Unidade](../ide/media/ute-failedpassednotrunsummary.png "UTE_FailedPassedNotRunSummary")

 Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados nos grupos padrão de **Testes com Falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. Você pode alterar a forma como o Gerenciador de Testes agrupa seus testes.

 Você pode executar a maior parte do trabalho de encontrar, organizar e executar testes usando a barra de ferramentas do Gerenciador de Testes.

 ![Executar testes na barra de ferramentas do Gerenciador de Testes](../test/media/ute-toolbar.png "UTE_ToolBar")

 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

### <a name="run-tests"></a><a name="BKMK_Run_tests"></a>Executar testes
 Você pode executar todos os testes na solução, todos os testes em um grupo ou um conjunto de testes que você selecionar. Realize um dos seguintes procedimentos:

- Para executar todos os testes em uma solução, escolha **Executar Todos**.

- Para executar todos os testes em um grupo padrão, escolha **executar...** e, em seguida, escolha o grupo no menu.

- Selecione os testes individuais que deseja executar, abra o menu de contexto para um teste selecionado e escolha **Executar Testes Selecionados**.

- Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o botão de alternância ![UTE&#95;parallelicon&#45;small](../test/media/ute-parallelicon-small.png "UTE_parallelicon-pequeno") na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.

  A barra de aprovação/reprovação na parte superior da janela do Gerenciador de Testes é animada conforme os testes são executados. Na conclusão da execução de teste, a barra de aprovação/reprovação ficará verde se todos os testes forem aprovados ou vermelha se algum deles for reprovado.

  ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

### <a name="run-tests-after-every-build"></a><a name="BKMK_Run_tests_after_every_build"></a> Executar testes depois de cada compilação

> [!WARNING]
> Executar testes de unidade após cada build tem suporte no Visual Studio Enterprise.

|Imagem|Descrição|
|-|-|
|![Executar após o build](../test/media/ute-runafterbuild-btn.png "UTE_RunAfterBuild_btn")|Para executar os testes de unidade após cada build local, escolha **Teste** no menu padrão e, em seguida, **Executar Testes após Build** na barra de ferramentas do Gerenciador de Testes.|

 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

## <a name="view-test-results"></a><a name="BKMK_View_test_results"></a>Exibir resultados de teste
 [Exibir detalhes do teste](#BKMK_View_test_details) **&#124;** [Exibir código-fonte de um método de teste](#BKMK_View_the_source_code_of_a_test_method)

 Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados em grupos **Testes com falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. O painel de detalhes na parte inferior do Gerenciador de Testes exibe um resumo da execução de teste.

### <a name="view-test-details"></a><a name="BKMK_View_test_details"></a> Exibir detalhes do teste
 Para exibir os detalhes de um teste individual, selecione o teste.

 ![Detalhes da execução do teste](../test/media/ute-testdetails.png "UTE_TestDetails")

 O painel de detalhes de teste exibe as seguintes informações:

- O nome do arquivo de origem e o número de linha do método de teste.

- O status do teste.

- O tempo decorrido que o método de teste levou para ser executado.

  Se o teste falhar, o painel de detalhes também exibe:

- A mensagem retornada pela estrutura de teste de unidade para o teste.

- O rastreamento de pilha no momento em que o teste falhou.

  ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

### <a name="view-the-source-code-of-a-test-method"></a><a name="BKMK_View_the_source_code_of_a_test_method"></a> Exibir o código-fonte de um método de teste
 Para exibir o código-fonte de um método de teste no editor do Visual Studio, selecione o teste e, em seguida, escolha **abrir teste** no menu de contexto (teclado: F12).

 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

## <a name="group-and-filter-the-test-list"></a><a name="BKMK_Group_and_filter_the_test_list"></a>Agrupar e filtrar a lista de testes
 [Agrupar a lista de testes](#BKMK_Grouping_the_test_list) **&#124;** [Agrupar por características](#BKMK_Group_by_traits) **&#124;** [Pesquisar e filtrar a lista de testes](#BKMK_Search_and_filter_the_test_list)

 O Gerenciador de Testes permite agrupar os testes em categorias predefinidas. A maioria das estruturas de teste de unidade executados no Gerenciador de Testes permitem que você defina suas próprias categorias e pares de valor/categoria para agrupar os testes. Você também pode filtrar a lista de testes por correspondência de cadeias de caracteres em relação a propriedades de teste.

### <a name="grouping-the-test-list"></a><a name="BKMK_Grouping_the_test_list"></a> Agrupar a lista de testes
 Para alterar a maneira como os testes são organizados, escolha a seta para baixo ao lado do botão **Agrupar por**![botão de grupo do Gerenciador de Testes](../test/media/ute-groupby-btn.png "UTE_GroupBy_btn") e selecione novos critérios de agrupamento.

 ![Agrupar testes por categoria no Gerenciador de Testes](../test/media/ute-groupbycategory.png "UTE_GroupByCategory")

### <a name="test-explorer-groups"></a>Grupos de Gerenciador de Testes

|Agrupar|Descrição|
|-----------|-----------------|
|**Duration**|Agrupa teste pelo tempo de execução: **rápido**, **médio** e **lento**.|
|**Resultado**|Agrupa testes por resultados da execução: **testes com falha**, **testes ignorados**, **testes aprovados**.|
|**Características**|Agrupa teste por pares de categoria/valor que você define. A sintaxe para especificar valores e categorias de característica é definida pela estrutura de teste de unidade.|
|**Projeto**|Agrupa teste por nome dos projetos.|

 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

### <a name="group-by-traits"></a><a name="BKMK_Group_by_traits"></a> Agrupar por características
 Uma característica é geralmente um par de nome/valor de categoria, mas também pode ser uma única categoria. Características podem ser atribuídas aos métodos que são identificados como um método de teste pela estrutura de teste de unidade. Uma estrutura de teste de unidade pode definir categorias de característica. Você pode adicionar valores para as categorias de característica para definir seus próprios pares de nome/valor de categoria. A sintaxe para especificar valores e categorias de característica é definida pela estrutura de teste de unidade.

 **Características na Estrutura de Teste da Unidade Microsoft para código gerenciado**

 Na estrutura de teste de unidade da Microsoft para aplicativos gerenciados, você define um par nome/valor de característica no atributo <xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>. A estrutura de teste também contém essas características predefinidas:

|Característica|Descrição|
|-----------|-----------------|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.OwnerAttribute>|A categoria do proprietário é definida pela estrutura de teste de unidade e exige que você forneça um valor de cadeia de caracteres do proprietário.|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.PriorityAttribute>|A categoria Prioridade é definida pela estrutura de teste de unidade e exige que você forneça um valor inteiro da prioridade.|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestCategoryAttribute>|O atributo TestCategory permite que você forneça uma categoria sem um valor. Uma categoria definida pelo atributo TestCategory também pode ser a categoria de um atributo TestProperty.|
|<xref:Microsoft.VisualStudio.TestTools.UnitTesting.TestPropertyAttribute>|O atributo TestProperty permite que você defina o par de categoria/valor da característica.|

 **Características na Estrutura de Teste da Unidade Microsoft para C++**

 Para definir uma característica, use a macro `TEST_METHOD_ATTRIBUTE`. Por exemplo, para definir uma característica chamada de `TEST_MY_TRAIT`:

```cpp
#define TEST_MY_TRAIT(traitValue) TEST_METHOD_ATTRIBUTE(L"MyTrait", traitValue)
```

 Para usar a característica definida em seus testes de unidade:

```
BEGIN_TEST_METHOD_ATTRIBUTE(Method1)
    TEST_OWNER(L"OwnerName")
    TEST_PRIORITY(1)
    TEST_MY_TRAIT(L"thisTraitValue")
END_TEST_METHOD_ATTRIBUTE()

TEST_METHOD(Method1)
{
    Logger::WriteMessage("In Method1");
    Assert::AreEqual(0, 0);
}
```

### <a name="c-trait-attribute-macros"></a>Macros de atributo de característica do C++

|Macro|Descrição|
|-----------|-----------------|
|`TEST_METHOD_ATTRIBUTE(attributeName, attributeValue)`|Use a macro TEST_METHOD_ATTRIBUTE para definir uma característica.|
|`TEST_OWNER(ownerAlias)`|Use a característica de proprietário predefinida para especificar um proprietário do método de teste.|
|`TEST_PRIORITY(priority)`|Use a característica de prioridade predefinida para atribuir prioridades relativas a seus métodos de teste.|

 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

### <a name="search-and-filter-the-test-list"></a><a name="BKMK_Search_and_filter_the_test_list"></a> Pesquisar e filtrar a lista de testes
 Você pode usar o Gerenciador de Testes filtros para limitar os métodos de teste em seus projetos que você exibe e executa.

 Quando você digita uma cadeia de caracteres na caixa de pesquisa do Gerenciador de Testes e escolhe a tecla ENTER, a lista de testes é filtrada para exibir somente os testes cujos nomes totalmente qualificados contêm a cadeia de caracteres.

 Para filtrar por um critério diferente:

1. Abra a lista suspensa à direita da caixa de pesquisa.

2. Escolha um novo critério.

3. Insira o valor do filtro entre aspas.

   ![Filtrar testes no Gerenciador de Testes](../test/media/ute-filtertestlist.png "UTE_FilterTestList")

> [!NOTE]
> As pesquisas não diferenciam maiúsculas de minúsculas e correspondem a cadeia especificada para qualquer parte do valor de critérios.

|Qualificador|Descrição|
|---------------|-----------------|
|**Característica**|Procura categoria de característica e valor para correspondência. A sintaxe para especificar valores e categorias de característica é definida pela estrutura de teste de unidade.|
|**Projeto**|Procura os nomes de projeto de teste para correspondências.|
|**Mensagem de erro**|Procura nas mensagens de erro definidas pelo usuário retornadas por falhas para encontrar correspondências.|
|**Caminho do arquivo**|Procura o nome de arquivo totalmente qualificado dos arquivos de origem do teste para encontrar correspondências.|
|**Nome Totalmente Qualificado**|Procura o nome de arquivo totalmente qualificado dos namespaces de teste, classes e métodos para encontrar correspondências.|
|**Saída**|Procura as mensagens de erro definidas pelo usuário que são gravadas para a saída padrão (stdout) ou erro padrão (stderr). A sintaxe para especificar mensagens de saúde é definida pela estrutura de teste de unidade.|
|**Resultado**|Procura os nomes de categoria do Gerenciador de Testes para encontrar correspondências: **testes com falha**, **testes ignorados**, **testes aprovados**.|

 Para excluir um subconjunto dos resultados de um filtro, use a seguinte sintaxe:

```
FilterName:"Criteria" -FilterName:"SubsetCriteria"
```

 Por exemplo,

```
FullName:"MyClass" - FullName:"PerfTest"
```

 retorna todos os testes que incluem "MyClass" em seu nome, exceto os testes que também incluem "PerfTest" em seu nome.

 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

## <a name="create-custom-playlists"></a><a name="BKMK_Create_custom_playlists"></a>Criar listas de reprodução personalizadas
 É possível criar e salvar uma lista de teste que você deseje executar ou exibir como um grupo. Ao selecionar uma lista de reprodução, os testes na lista são exibidos no Gerenciador de Testes. É possível adicionar um teste a mais de uma lista de reprodução e todos os testes no projeto estarão disponíveis quando você escolher a lista de reprodução **Todos os Testes**.

 ![Escolher uma playlist](../test/media/ute-playlist.png "UTE_Playlist")

 **Para criar uma lista de reprodução**, escolha um ou mais testes no Gerenciador de Testes. No menu de contexto, escolha **Adicionar à lista de reprodução**, **NewPlaylist**. Salve o arquivo com o nome e local que você especificar na caixa de diálogo **Criar nova lista de reprodução**.

 **Para adicionar testes a uma lista de reprodução**, escolha um ou mais testes no Gerenciador de Testes. No menu de contexto, escolha **Adicionar à lista de reprodução**e, em seguida, escolha a lista de reprodução que você deseja adicionar os testes.

 **Para abrir uma lista de reprodução**, escolha o teste, a lista de reprodução no menu do Visual Studio e escolha na lista de listas de reprodução usadas recentemente ou escolha Abrir a lista de reprodução para especificar o nome e o local da lista de reprodução.

 Se os testes individuais não tiverem dependências que os impeçam de serem executados em qualquer ordem, ative a execução de teste em paralelo com o botão de alternância ![UTE&#95;parallelicon&#45;small](../test/media/ute-parallelicon-small.png "UTE_parallelicon-pequeno") na barra de ferramentas. Isso pode reduzir consideravelmente o tempo necessário para executar todos os testes.

 ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

## <a name="debug-and-analyze-unit-tests"></a><a name="BKMK_Debug_and_analyze_unit_tests"></a> Depurar e analisar testes de unidade
 [Depurar testes de unidade](#BKMK_Debug_unit_tests) **&#124** [Diagnosticar problemas de desempenho de método de teste](#BKMK_Diagnose_test_method_performance_issues) **&#124** [Analisar cobertura de código de teste de unidade](#BKMK_Analyzeunit_test_code_coverage)

### <a name="debug-unit-tests"></a><a name="BKMK_Debug_unit_tests"></a> Depurar testes de unidade
 Você pode usar o Gerenciador de Testes para iniciar uma sessão de depuração para os testes. Passar pelo código com o depurador do Visual Studio permite-lhe navegar facilmente entre os testes de unidade e o projeto sendo testado. Para iniciar a depuração:

1. No editor do Visual Studio, defina um ponto de interrupção em um ou mais métodos de teste que deseje depurar.

   > [!NOTE]
   > Como os métodos de teste podem ser executados em qualquer ordem, defina pontos de interrupção em todos os métodos de teste que deseje depurar.

2. No Gerenciador de Testes, selecione os métodos de teste e escolha **Depurar Testes Selecionados** no menu de contexto.

   Para obter mais informações sobre o depurador, consulte [Depuração no Visual Studio](../debugger/debugging-in-visual-studio.md).

   ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

### <a name="diagnose-test-method-performance-issues"></a><a name="BKMK_Diagnose_test_method_performance_issues"></a> Diagnosticar problemas de desempenho do método de teste
 Para diagnosticar por que um método de teste está levando muito tempo, selecione o método no Gerenciador de Testes e, em seguida, escolha o perfil no menu de contexto. Consulte [Gerenciador de Desempenho](../profiling/performance-explorer.md).

### <a name="analyze-unit-test-code-coverage"></a><a name="BKMK_Analyzeunit_test_code_coverage"></a> Analisar a cobertura de código de teste de unidade

> [!NOTE]
> Cobertura de código de teste de unidade está disponível apenas no Visual Studio Enterprise.

 Você pode determinar a quantidade de seu código de produto que realmente está sendo testado por seus testes de unidade usando a ferramenta de cobertura de código do Visual Studio. Você pode executar a cobertura de código em testes selecionados ou em todos os testes em uma solução.

 Para executar a cobertura de código para métodos de teste em uma solução:

1. Escolha **Testes** no menu do Visual Studio e, em seguida, escolha **Analisar cobertura de código**.

2. Escolha um dos seguintes comandos do submenu:

   - **Testes selecionados** executa os métodos de teste que você selecionou no Gerenciador de Testes.

   - **Todos os testes** executa todos os métodos de teste na solução.

   A janela Resultados de Cobertura do Código exibe a porcentagem dos blocos que foram exercidos por linha, função, classe, namespace e módulo de código do produto.

   Para obter mais informações, consulte [Usando cobertura de código para determinar quanto código está sendo testado](../test/using-code-coverage-to-determine-how-much-code-is-being-tested.md).

   ![Voltar ao](../debugger/media/pcs-backtotop.png "PCS_BackToTop") [conteúdo](#BKMK_Contents) superior

## <a name="external-resources"></a><a name="BKMK_External_resources"></a>Recursos externos

### <a name="guidance"></a><a name="BKMK_Guidance"></a>Guia
 [Testes de Entrega Contínua com o Visual Studio 2012 – Capítulo 2: Teste de Unidade: Testando o Interior](https://msdn.microsoft.com/library/jj159340.aspx)

## <a name="see-also"></a>Consulte Também
 [Teste de unidade seu código](../test/unit-test-your-code.md) [Execute um teste de unidade como um processo de 64 bits](../test/run-a-unit-test-as-a-64-bit-process.md)
