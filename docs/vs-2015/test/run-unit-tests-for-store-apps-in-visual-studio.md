---
title: Executar testes de unidade para aplicativos da loja
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 5a6f5b32-bfce-4a63-81e9-02d54c592539
caps.latest.revision: 14
author: alexhomer1
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b70e3a24cd4cb05dc1a28ff855498496f5665ddc
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/30/2020
ms.locfileid: "85542851"
---
# <a name="run-unit-tests-for-store-apps-in-visual-studio"></a>Executar testes de unidade de aplicativos da Store no Visual Studio
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Este tópico descreve como executar testes de unidade usando o Gerenciador de Testes no Microsoft Visual Studio

> [!NOTE]
> Os tópicos nesta seção descrevem a funcionalidade do Visual Studio Express para Windows 8. O Visual Studio Community, Enterprise e Professional fornecem funcionalidades adicionais para teste de unidade.
>
> - Use qualquer estrutura de teste de unidade de software livre ou de terceiros que tenham criado um adaptador complementar para o Gerenciador de Testes da Microsoft. Você também pode analisar e exibir informações de cobertura de código para seus testes.
>   - Execute os testes depois de cada compilação. Você também pode usar Microsoft Fakes, uma estrutura de isolamento para código gerenciado que ajuda a focar seus testes no seu próprio código, substituindo o código de teste pela funcionalidade do sistema e de terceiros.
>
>   Para obter mais informações, consulte [Executar o teste de unidade em seu código](../test/unit-test-your-code.md) na Biblioteca do MSDN.

## <a name="in-this-topic"></a><a name="BKMK_In_this_topic"></a>Neste tópico
 [Estruturas de teste de unidade e projetos de teste](#BKMK_Unit_test_frameworks_and_test_projects)

 [Executando testes no Gerenciador de Testes](#BKMK_Running_tests_in_Test_Explorer)

- [Executando testes](#BKMK_Running_tests)

  [Exibindo resultados de teste](#BKMK_Viewing_test_results)

- [Exibindo detalhes do teste](#BKMK_Viewing_test_details)

- [Exibindo o código-fonte de um método de teste](#BKMK_Viewing_the_source_code_of_a_test_method)

  [Organizando a lista de testes](#BKMK_Organizing_the_test_list)

- [Agrupamento de testes](#BKMK_Grouping_tests)

- [Pesquisando e filtrando a lista de testes](#BKMK_Searching_and_filtering_the_test_list)

  [Depuração de testes de unidade](#BKMK_Debugging_unit_tests)

## <a name="unit-test-frameworks-and-test-projects"></a><a name="BKMK_Unit_test_frameworks_and_test_projects"></a>Estruturas de teste de unidade e projetos de teste
 O Visual Studio Express para aplicativos da Windows Store inclui as estruturas de teste de unidade da Microsoft para código C++ gerenciado e nativo. O Gerenciador de Testes pode executar testes de vários projetos de teste em uma solução e de classes de teste que fazem parte dos projetos de código de produção. Os projetos de teste podem ser qualquer combinação de Visual C++ ou estruturas de teste de unidade Visual C# e Visual Basic. Quando o código em teste é escrito para o .NET Framework, o projeto de teste pode ser escrito em qualquer linguagem do .NET Framework, independentemente do idioma de código de destino. Projetos de código C/C++ nativos devem ser testados usando uma estrutura de teste de unidade C++.

## <a name="running-tests-in-test-explorer"></a><a name="BKMK_Running_tests_in_Test_Explorer"></a>Executando testes no Gerenciador de testes
 Quando você compila o projeto de teste, os testes são exibidos no Gerenciador de Testes. Se o Gerenciador de Testes não estiver visível, escolha **Teste** no menu do Visual Studio, **Windows** e, em seguida, **Gerenciador de Testes**.

 ![Gerenciador de Testes de Unidade](../ide/media/ute-failedpassednotrunsummary.png "UTE_FailedPassedNotRunSummary")

 Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados nos grupos padrão de **Testes com Falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. Você pode alterar a forma como o Gerenciador de Testes agrupa seus testes.

 Você pode executar a maior parte do trabalho de encontrar, organizar e executar testes usando a barra de ferramentas do Gerenciador de Testes.

 ![Executar testes na barra de ferramentas do Gerenciador de Testes](../test/media/ute-toolbar.png "UTE_ToolBar")

### <a name="running-tests"></a><a name="BKMK_Running_tests"></a>Executando testes
 Você pode executar todos os testes na solução, todos os testes em um grupo ou um conjunto de testes que você selecionar. Realize um dos seguintes procedimentos:

- Para executar todos os testes em uma solução, escolha **Executar Todos**.

- Para executar todos os testes em um grupo padrão, escolha **executar...** e, em seguida, escolha o grupo no menu.

- Selecione os testes individuais que deseja executar, abra o menu de atalho para um teste selecionado e escolha **Executar Testes Selecionados**.

  A barra de aprovação/reprovação na parte superior da janela do Gerenciador de Testes é animada conforme os testes são executados. Na conclusão da execução de teste, a barra de aprovação/reprovação ficará verde se todos os testes forem aprovados ou vermelha se algum deles for reprovado.

## <a name="viewing-test-results"></a><a name="BKMK_Viewing_test_results"></a>Exibindo resultados de teste
 Conforme você executa, grava e executa novamente os testes, o Gerenciador de Testes exibe os resultados em grupos **Testes com falha**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**. O painel de detalhes na parte inferior do Gerenciador de Testes exibe um resumo da execução de teste.

### <a name="viewing-test-details"></a><a name="BKMK_Viewing_test_details"></a> Exibindo detalhes do teste
 Para exibir os detalhes de um teste individual, selecione o teste.

 O painel de detalhes de teste exibe as seguintes informações:

- O nome do arquivo de origem e o número de linha do método de teste.

- O status do teste.

- O tempo decorrido que o método de teste levou para ser executado.

  Se o teste falhar, o painel de detalhes também exibe:

- A mensagem retornada pela estrutura de teste de unidade para o teste.

- O rastreamento de pilha no momento em que o teste falhou.

### <a name="viewing-the-source-code-of-a-test-method"></a><a name="BKMK_Viewing_the_source_code_of_a_test_method"></a> Exibindo o código-fonte de um método de teste
 Para exibir o código-fonte para um método de teste no editor do Visual Studio, selecione o teste e, em seguida, escolha **Abrir teste** no menu de atalho (teclado: F12).

## <a name="organizing-the-test-list"></a><a name="BKMK_Organizing_the_test_list"></a> Organizando a lista de testes

### <a name="grouping-tests"></a><a name="BKMK_Grouping_tests"></a> Agrupando testes
 Por padrão, o Gerenciador de Testes exibe os testes como nós filhos de **Testes Reprovados**, **Testes Aprovados**, **Testes Ignorados** e **Testes Não Executados**.

|Imagem|Descrição|
|-|-|
|![Botão de grupo do Gerenciador de Testes](../test/media/ute-groupby-btn.png "UTE_GroupBy_btn")|Para agrupar os testes pelo tempo necessário para executá-los, abra a lista **Agrupar por** e escolha **Duração**. Escolha **Resultado do Teste** para mudar para o agrupamento original.|

### <a name="searching-and-filtering-the-test-list"></a><a name="BKMK_Searching_and_filtering_the_test_list"></a> Pesquisando e filtrando a lista de testes
 Quando você tiver um grande número de testes, poderá digitar na caixa de pesquisa do Gerenciador de Testes para filtrar a lista por cadeia de caracteres especificada. Você pode restringir o filtro a tipos específicos de cadeias de caracteres escolhendo na lista de filtros antes de inserir a cadeia de caracteres de pesquisa.

 ![Pesquisar categorias de filtro](../test/media/ute-searchfilter.png "UTE_SearchFilter")

## <a name="debugging-unit-tests"></a><a name="BKMK_Debugging_unit_tests"></a> Depurando testes de unidade
 Você pode usar o Gerenciador de Testes para iniciar uma sessão de depuração para os testes. Passar pelo código com o depurador do Visual Studio permite-lhe navegar facilmente entre os testes de unidade e o projeto sendo testado. Para iniciar a depuração:

1. No editor do Visual Studio, defina um ponto de interrupção em um ou mais métodos de teste que deseje depurar.

   > [!NOTE]
   > Como os métodos de teste podem ser executados em qualquer ordem, defina pontos de interrupção em todos os métodos de teste que deseje depurar.

2. No Gerenciador de Testes, selecione os métodos de teste e escolha **Depurar Testes Selecionados** no menu de atalho.

   Para obter mais informações sobre o depurador, consulte [Depuração no Visual Studio](../debugger/debugging-in-visual-studio.md).
