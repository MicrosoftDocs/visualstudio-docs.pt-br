---
title: Corrigir os erros de programa e melhorar o código
description: Este artigo descreve algumas maneiras básicas pelas quais o Visual Studio pode ajudá-lo a encontrar e corrigir problemas em seu código, incluindo erros de build, análise de código, ferramentas de depuração e testes de unidade.
ms.date: 05/02/2018
ms.topic: conceptual
ms.assetid: c3a14d28-d811-4ff3-bd09-21dce14025ca
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5af76de5dbcc7a70722acf0ee01cfed93dbad761
ms.sourcegitcommit: 5fb4a67a8208707e79dc09601e8db70b16ba7192
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2021
ms.locfileid: "112308253"
---
# <a name="make-code-work-in-visual-studio"></a>Fazer o código funcionar no Visual Studio

O Visual Studio fornece um poderoso conjunto integrado de ferramentas de depuração e build do projeto. Neste artigo, descubra como o Visual Studio pode ajudar você a localizar problemas no código usando a saída de build, a análise de código, ferramentas de depuração e testes de unidade.

Você descobriu o editor e criou alguns códigos. Agora, você deseja ter certeza de que o código funciona corretamente. No Visual Studio, assim como acontece com a maioria dos IDEs, há duas fases para fazer com que o código funcione: criar o código para capturar e resolver erros do compilador e de projeto e executar o código no ambiente para localizar erros dinâmicos e em tempo de execução.

## <a name="build-your-code"></a>Compilar o código

Há dois tipos básicos de configuração de build: **Depuração** e **Versão**. A configuração **Depuração** produz um executável maior e mais lento que permite uma experiência de depuração em tempo de execução interativa e mais avançada. O executável **Depuração** nunca deve ser enviado. A configuração **Versão** cria um executável mais rápido e otimizado, apropriado para envio (pelo menos da perspectiva do compilador). A configuração de build padrão é **Depuração**.

A maneira mais fácil de criar o projeto é pressionar **F7**, mas você também pode iniciar o build selecionando **Compilar** > **Compilar Solução** no menu principal.

![Seleção do menu de projeto de build do Visual Studio](../ide/media/vs_ide_gs_debug_build_menu_item.png)

Observe o processo de build na janela **Saída** na parte inferior da interface do usuário do Visual Studio. Os erros, avisos e operações de build são exibidos aqui. Se você tiver erros (ou se tiver avisos acima de um nível configurado), haverá falha no build. Você pode clicar nos erros e avisos para ir para a linha em que eles ocorreram. Recrie o projeto pressionando **F7** novamente (para recompilar apenas os arquivos com erros) ou **Ctrl**+**Alt**+**F7** (para uma recriação completa e limpa).

Há duas janelas com guias na janela de resultados abaixo do editor: a janela **Saída**, que contém a saída bruta do compilador (incluindo mensagens de erro) e a janela **Lista de Erros**, que fornece uma lista filtrável e classificável de todos os erros e avisos.

Quando o build for bem-sucedido, você verá os resultados desta maneira na janela **Saída**:

![Saída de build bem-sucedido do Visual Studio](../ide/media/vs_ide_gs_debug_success_build.png)

## <a name="review-the-error-list"></a>Examinar a Lista de Erros

A menos que não tenha feito nenhuma modificação no código compilado com êxito anteriormente, provavelmente haverá um erro. Se você não estiver familiarizado com a codificação, provavelmente haverá muitos deles. Às vezes os erros são óbvios, como um erro de sintaxe simples ou um nome de variável incorreto e às vezes eles são difíceis de entender, com apenas um código confuso para orientá-lo. Para uma exibição mais limpa dos problemas, navegue até a parte inferior da janela **Saída** do build e clique na guia **Lista de** Erros. Isso leva você a uma exibição mais organizada dos erros e avisos para seu projeto e também oferece algumas opções adicionais.

![Lista de Erros e Saída do Visual Studio](../ide/media/vs_ide_gs_debug_bad_build_error_list.png)

Clique na linha de erro na janela **Lista de Erros** e vá para a linha em que ocorre o erro. (Ou ativar números de linha pressionando **Ctrl** + **P,** digitando **números de linha** e, em seguida, escolhendo Ativar ou desativar números de **linha** dos resultados. Essa é a maneira mais rápida para acessar a caixa de diálogo **Opções**, em que é possível ativar os números de linha.

![Editor do Visual Studio com números de linha](../ide/media/vs_ide_gs_debug_line_numbers.png)

![Opção de números de linha do Visual Studio](../ide/media/vs_ide_gs_debug_options_line_numbers.png)

Pressione **Ctrl** + **G** para ir rapidamente para o número de linha em que o erro ocorreu.

O erro é identificado por um sublinhado vermelho de "rabisco". Passe o mouse sobre ele para obter detalhes adicionais. Faça a correção e ele desaparecerá, embora você possa inserir um novo erro com a correção. (Isso é chamado de "regressão".)

![Foco de erro do Visual Studio](../ide/media/vs_ide_gs_debug_error_hover1.png)

Percorra a lista de erros e resolva todos os erros em seu código.

![Janela Depurar erros do Visual Studio](../ide/media/vs_ide_gs_debug_error_list.png)

### <a name="review-errors-in-detail"></a>Examinar os erros detalhadamente

Muitos erros podem não fazem sentido para você, formulados como eles estão nos termos do compilador. Nesses casos, você precisará de informações adicionais. Na janela **Lista de Erros**, você pode fazer uma pesquisa automática do Bing para obter mais informações sobre o erro ou o aviso. Clique com o botão direito do mouse na linha de entrada correspondente e selecione **Mostrar Ajuda para Erros** no menu de contexto ou clique no valor do código de erro vinculado por hiperlink na coluna **Código** da **Lista de Erros**.

![Lista de erros do Visual Studio da pesquisa do Bing](../ide/media/vs_ide_gs_debug_error_list_error_help.png)

Dependendo das configurações, o navegador da Web exibe os resultados da pesquisa para o código de erro e o texto ou uma guia é aberta no Visual Studio, que mostra os resultados da pesquisa do Bing. Os resultados são de muitas origens diferentes na Internet e nem todos podem ser úteis.

## <a name="use-code-analysis"></a>Usar a análise de código

Os analisadores de código procuram problemas comuns de código que podem levar a erros em tempo de execução ou a problemas no gerenciamento de códigos.

### <a name="c-and-visual-basic-code-analysis"></a>Análise de código do C# e do Visual Basic

O Visual Studio inclui um conjunto interno de [analisadores do .NET Compiler Platform](../code-quality/roslyn-analyzers-overview.md) que examinam o código C# e Visual Basic durante a digitação. Instale outros analisadores como uma extensão do Visual Studio, ou como um pacote NuGet. Se as violações de regra são encontradas, elas são relatadas na Lista de Erros e no editor de códigos como uma alternância sob o código ofensivo.

### <a name="c-code-analysis"></a>Análise de código C++

Para analisar o código C++, execute a [análise de código estático](/cpp/code-quality/quick-start-code-analysis-for-c-cpp). Crie o hábito de executá-lo depois de limpar os erros óbvios que impediam um build bem-sucedido e reserve um tempo para resolver os avisos que ele pode produzir. Você evitará algumas dores de cabeça no futuro, bem como aprenderá algumas técnicas de estilo de código.

Pressione **Alt** + **F11** (ou selecione **Analisar** Executar Code Analysis na Solução no menu  >   superior) para iniciar a análise de código estático.

![Item de menu Análise de Código do Visual Studio](../ide/media/vs_ide_gs_debug_run_code_analysis.png)

Os avisos novos ou atualizados são exibidos na guia **Lista de Erros** na parte inferior do IDE. Clique nos avisos para ir para eles no código.

![Lista de Erros do Visual Studio com Avisos](../ide/media/cpp-code-analysis-warning.png)

## <a name="use-quick-actions-to-fix-or-refactor-code"></a>Usar as Ações Rápidas para corrigir ou refatorar o código

As [Ações Rápidas](../ide/quick-actions.md), disponíveis nos ícones de lâmpada ou chave de fenda, permitem refatorar o código embutido. Elas são uma maneira fácil de corrigir avisos comuns com rapidez e eficiência no código C#, C++ e Visual Basic. Para acessá-las, clique com o botão direito do mouse em uma linha ondulada de aviso e selecione **Ações Rápidas e refatorações**. Ou, quando o cursor estiver na linha com a alternância colorida, pressione **Ctrl** + **.** ou selecionar o ícone de lâmpada, lâmpada de erro ou chave de fenda na margem. Você verá uma lista de possíveis correções ou refatorações que podem ser aplicadas àquela linha de código.

![Visualização da lâmpada do Visual Studio](../ide/media/quick-actions-options.png)

As Ações Rápidas podem ser usadas sempre que os analisadores de código determinam que há uma oportunidade para corrigir, refatorar ou melhorar o código. Clique em qualquer linha de código, clique com o botão direito do mouse para abrir o menu de contexto e selecione **Ações Rápidas e refatorações**. Se opções de refatoração ou melhoria estiverem disponíveis, elas serão exibidas. Caso contrário, a mensagem **Nenhuma ação rápida disponível aqui** é exibida no canto inferior esquerdo do IDE.

![Texto "Nenhuma ação rápida disponível aqui"](../ide/media/vs_ide_gs_debug_light_bulb_no_options.png)

Com a experiência, você pode usar rapidamente as teclas de direção e **Ctrl** + **.** para verificar se há oportunidades fáceis de refatoração e limpar seu código.

::: moniker range=">=vs-2019"

## <a name="run-code-cleanup"></a>Executar Limpeza de Código

Visual Studio fornece formatação sob demanda do arquivo de código [C#,](code-styles-and-code-cleanup.md#apply-code-styles)incluindo  preferências de estilo de código, por meio do botão Limpeza de Código na parte inferior do editor.

![Botão de Limpeza de código no Visual Studio 2019](media/execute-code-cleanup.png)

Além de formatar seu arquivo para espaços, recuos e **outros,** a Limpeza de Código também aplica um conjunto de convenções de estilo de código que você define. Suas preferências para cada estilo de código são lidas no [arquivo EditorConfig](code-styles-and-code-cleanup.md#code-styles-in-editorconfig-files), caso tenha um para o projeto ou das [configurações de estilo de código](code-styles-and-code-cleanup.md#code-styles-in-the-options-dialog-box) na caixa de diálogo **Opções**.

::: moniker-end

## <a name="debug-your-running-code"></a>Depurar seu código em execução

Agora que você criou seu código com êxito e realizou uma pequena limpeza, execute-o pressionando **F5** ou selecionando **Depurar**  >  **Iniciar Depuração**. Isso inicia o aplicativo em um ambiente de depuração, para que você possa observar seu comportamento em detalhes. O IDE do Visual Studio muda enquanto o aplicativo é executado: a janela **Saída** é substituída por duas novas (na configuração de janela padrão), a janela com guias **Autos/Locais/Inspeção** e a janela com guias **Pilha de Chamadas/Pontos de Interrupção/Configuração de Exceção/Saída**. Essas janelas têm várias guias que permitem inspecionar e avaliar as variáveis, os threads, as pilhas de chamadas e vários outros comportamentos do aplicativo enquanto ele é executado.

![Janelas Automáticas e Pilha de Chamadas do Visual Studio](../ide/media/vs_ide_gs_debug_autos_and_call_stack.png)

Pare o aplicativo pressionando **Shift** + **F5** ou clicando no **botão** Parar. Ou você pode apenas fechar a janela principal do aplicativo (ou a caixa de diálogo de linha de comando).

Se seu código for executado perfeitamente e exatamente como esperado, parabéns! No entanto, se ele parar de responder ou tiver problemas ou tiver dado alguns resultados estranho, você precisará encontrar a origem desses problemas e corrigir os bugs.

### <a name="set-simple-breakpoints"></a>Definir pontos de interrupção simples

[Pontos de interrupção](../debugger/using-breakpoints.md) são o recurso mais básico e essencial da depuração confiável. Um ponto de interrupção indica quando o Visual Studio deve suspender o código em execução para que você possa examinar os valores das variáveis ou o comportamento de memória ou se uma ramificação de código está sendo executada ou não. Você não precisa recriar um projeto depois de configurar e remover pontos de interrupção.

Defina um ponto de interrupção clicando na margem distante da linha em que você deseja que a interrupção ocorra ou pressione **F9** para definir um ponto de interrupção na linha de código atual. Quando você executar o código, ele será pausado (ou *interrompido*) antes das instruções para esta linha de código serem executadas.

![Ponto de interrupção do Visual Studio](../ide/media/vs_ide_gs_debug_breakpoint1.png)

Os usos comuns para os pontos de interrupção incluem:

- Para restringir a origem de um programa com falha ou sem resposta, os pontos de interrupção de dispersão em todo o código da chamada de método que você acha que está causando a falha. Conforme você executa o código no depurador, remova e redefina os pontos de interrupção mais próximos até encontrar a linha de código incorreta. Consulte a próxima seção para aprender a executar o código no depurador.

- Ao introduzir um novo código, defina um ponto de interrupção no início dele e execute o código para verificar se ele está se comportando conforme o esperado.

- Se você implementou um comportamento complicado, defina pontos de interrupção para o código de algoritmo, de modo que você possa inspecionar os valores das variáveis e dos dados quando o programa for interrompido.

- Se estiver escrevendo um código C ou C++, use pontos de interrupção para interromper o código, de modo que você possa inspecionar os valores de endereço (procure NULL) e as contagens de referência durante a depuração devido a falhas relacionadas à memória.

Para obter mais informações sobre como usar pontos de interrupção, leia [Usando pontos de interrupção](../debugger/using-breakpoints.md).

### <a name="inspect-your-code-at-run-time"></a>Inspecionar seu código no tempo de execução

Quando seu código em execução atinge um ponto de interrupção e pausa, a linha de código marcada em amarelo (a instrução atual) não foi executada ainda. Neste ponto, pode ser útil executar a instrução atual e, em seguida, inspecionar os valores alterados. Você pode usar vários comandos *step* para executar o código no depurador. Se o código marcado for uma chamada de método, você poderá entrar nele pressionando **F11**. Você também pode *passar sobre* a linha de código pressionando **F10**. Para obter detalhes sobre como percorrer o código e comandos adicionais, leia [Navegar pelo código com o depurador](../debugger/navigating-through-code-with-the-debugger.md).

![Captura de tela da Visual Studio de código. Um ponto vermelho na medianiz esquerda indica um ponto de interrupção na linha de código marcada em amarelo.](../ide/media/vs_ide_gs_debug_hit_breakpoint.png)

Na ilustração anterior, você pode avançar uma instrução do depurador pressionando **F10** ou **F11** (como não há nenhuma chamada de método, os dois comandos têm o mesmo resultado).

Quando o depurador entra em pausa, você pode inspecionar suas variáveis e pilhas de chamadas para determinar o que está acontecendo. Os valores estão nos intervalos que você espera ver? As chamadas estão sendo feitas na ordem correta?

![Captura de tela da Visual Studio de código. Na linha de código marcada em amarelo, uma variável é selecionada e uma lista suspenso mostra seu valor e referências atuais.](../ide/media/vs_ide_gs_debug_inspect_value.png)

Focalize uma variável para ver seu valor atual e suas referências. Se você observar um valor que não esperava, provavelmente, haverá um bug no código anterior ou de chamada. Para obter informações mais detalhadas sobre depuração, [saiba mais](../debugger/debugger-feature-tour.md) sobre como usar o depurador.

Além disso, Visual Studio exibe **a** Ferramentas de Diagnóstico, em que você pode observar o uso de CPU e memória do aplicativo ao longo do tempo. Mais tarde no desenvolvimento do seu aplicativo, você pode usar essas ferramentas para procurar uso intenso da CPU ou alocação de memória inesperada. Use-o em conjunto com **a** janela De relógio e pontos de interrupção para determinar o que está causando uso intenso inesperado ou recursos não lançados. Para obter mais informações, consulte [Tour do recurso de criação de perfil](../profiling/profiling-feature-tour.md).

## <a name="run-unit-tests"></a>Executar testes de unidade

Testes de unidade são a primeira linha de defesa contra bugs no código porque, quando realizados corretamente, eles testam uma única "unidade" de código, normalmente uma única função, e geralmente são muito mais fáceis de serem depurados do que o programa completo. O Visual Studio instala as estruturas de teste de unidade da Microsoft para código gerenciado e nativo. Use uma estrutura de teste de unidade para criar testes de unidade, executá-los e relatar os resultados desses testes. Execute os testes de unidade novamente quando fizer alterações para testar se o código ainda está funcionando corretamente. Com o Visual Studio Enterprise Edition, você pode executar testes automaticamente após cada build.

Para começar, leia [Gerar testes de unidade para seu código com IntelliTest](../test/generate-unit-tests-for-your-code-with-intellitest.md).

Para saber mais sobre testes de unidade no Visual Studio e como eles podem ajudá-lo a criar código de melhor qualidade, leia [Noções básicas de teste de unidade](../test/unit-test-basics.md).

## <a name="see-also"></a>Confira também

- [Introdução ao depurador](../debugger/debugger-feature-tour.md)
- [Saiba mais sobre como usar o depurador](../debugger/index.yml)
- [Gerar e corrigir código](../ide/code-generation-in-visual-studio.md)
