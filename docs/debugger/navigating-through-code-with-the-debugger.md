---
title: Navegar pelo código com o depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 11/12/2018
ms.topic: conceptual
f1_keywords:
- vs.debug.execution
helpviewer_keywords:
- stepping
- debugging [Visual Studio], execution control
- execution, controlling in debugger
ms.assetid: 759072ba-4aaa-447e-8e51-0dd1456fe896
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e07e2612e01453115cf4cd6120d92bfd5b0168bd
ms.sourcegitcommit: fe212f8960d7882a1b0fdae9e22f008996aacf3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/03/2019
ms.locfileid: "70222645"
---
# <a name="navigate-through-code-with-the-visual-studio-debugger"></a>Navegar pelo código com o depurador do Visual Studio

O depurador do Visual Studio pode ajudá-lo a navegar pelo código para inspecionar o estado de um aplicativo e mostrar seu fluxo de execução. Você pode usar atalhos de teclado, comandos de depuração, pontos de interrupção e outros recursos para obter rapidamente o código que você deseja examinar. A familiaridade com os comandos e atalhos de navegação do depurador torna mais rápida e fácil localizar e resolver problemas do aplicativo.  Se esta for a primeira vez que você tentou depurar o código, talvez você queira ler [depuração para iniciantes absolutos](../debugger/debugging-absolute-beginners.md) e [ferramentas e técnicas de depuração antes de](../debugger/write-better-code-with-visual-studio.md) passar por este artigo.

## <a name="basic-debugging"></a>Depuração básica

Para iniciar seu aplicativo com o depurador anexado, pressione **F5**, selecione **depurar** > **Iniciar Depuração**ou selecione a seta verde na barra de ferramentas do Visual Studio.

 ![DBG&#95;Basics&#95;Start&#95;Debugging](../debugger/media/dbg_basics_start_debugging.png "DBG_Basics_Start_Debugging")

Enquanto você estiver Depurando, um realce amarelo mostrará a linha de código que será executada em seguida.

 ![Modo&#95;de&#95;interrupção&#95;dos fundamentos do DBG](../debugger/media/dbg_basics_break_mode.png "Modo de interrupção")

A maioria das janelas do depurador, como os **módulos** e as janelas de **inspeção** , está disponível somente enquanto o depurador está em execução. Alguns recursos do depurador, como a exibição de valores de variáveis na janela **locais** ou a avaliação de expressões na janela **Watch** , estão disponíveis somente enquanto o depurador é pausado em um ponto de interrupção, também chamado de *modo de interrupção*.

No modo de interrupção, a execução do aplicativo é suspensa enquanto as funções, variáveis e objetos permanecem na memória. Você pode examinar as posições e os Estados dos elementos para procurar violações ou bugs. Para alguns tipos de projeto, você também pode fazer ajustes no aplicativo enquanto estiver no modo de interrupção. Para ver um vídeo mostrando esses recursos, consulte [introdução com o depurador](https://www.youtube.com/watch?v=FtGCi5j30YU&list=PLReL099Y5nRfw6VNvzMkv0sabT2crbSpK&index=6).

Se você interromper o código que não tem arquivos de origem ou símbolo ( *. pdb*) carregados, o depurador exibirá uma página **arquivos de origem não encontrados** ou **símbolos não encontrados** que pode ajudá-lo a localizar e carregar os arquivos. Confira [Especificar arquivos de símbolo (.pdb) e de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md). Se você não puder carregar o símbolo ou os arquivos de origem, ainda poderá depurar as instruções do assembly na janela de desmontagem.

Você nem sempre precisa iniciar a depuração iniciando um aplicativo no início. Você também pode pressionar **F11** para entrar [no código](#BKMK_Step_into__over__or_out_of_the_code), pressionar **F10** para [passar pelo código](#BKMK_Step_over_Step_out)ou [Executar para uma função ou local específico](#BKMK_Break_into_code_by_using_breakpoints_or_Break_All).

## <a name="step-through-code"></a>Percorrer o código

Os comandos de etapa do depurador ajudam a inspecionar o estado do aplicativo ou a saber mais sobre seu fluxo de execução.

Se você precisar localizar o ponto de entrada em seu aplicativo, comece com **F10** ou **F11**.

### <a name="BKMK_Step_into__over__or_out_of_the_code"></a>Passar para o código linha por linha

Para parar em cada linha de código ou instrução durante a depuração, use **depurar** > **etapa para**ou pressione **F11**.

O depurador percorre instruções de código, não linhas físicas. Por exemplo, uma cláusula `if` pode ser escrita em uma linha:

  ```csharp
  int x = 42;
  string s = "Not answered";
  if( int x == 42) s = "Answered!";
  ```

  ```vb
  Dim x As Integer = 42
  Dim s As String = "Not answered"
  If x = 42 Then s = "Answered!"
  ```

No entanto, quando você entrar nessa linha, o depurador tratará a condição como uma etapa e a conseqüência como outra. No exemplo anterior, a condição é verdadeira.

Em uma chamada de função aninhada, a **Depuração Completa** intervém na função aninhada mais profunda. Por exemplo, se você usar **Step Into** em uma chamada como `Func1(Func2())`, o depurador percorre a função. `Func2`

>[!TIP]
>Ao executar cada linha de código, você pode passar o mouse sobre variáveis para ver seus valores ou usar as janelas [locais](autos-and-locals-windows.md) e [assistir](watch-and-quickwatch-windows.md) para observar os valores alterados. Você também pode rastrear visualmente a pilha de chamadas durante a depuração de funções. Consulte [métodos de mapeamento na pilha de chamadas durante a depuração](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).

### <a name="BKMK_Step_over_Step_out"></a>Percorrer o código e ignorar algumas funções

Talvez você não se preocupa com uma função durante a depuração, ou você sabe que ela funciona, como um código de biblioteca bem testado. Você pode usar os comandos a seguir para ignorar o código. As funções ainda são executadas, mas o depurador as ignora.

|Comando de teclado|Comando de menu Depurar|Descrição|
|----------------------|------------------|-----------------|
|**F10**|**Depuração Parcial**|Se a linha atual contiver uma chamada de função, a **etapa** executará o código e suspenderá a execução na primeira linha de código depois que a função chamada retornar.|
|**Shift**+**F11**|**Depuração Circular**|O **Step Out** continua executando o código e suspende a execução quando a função atual retorna. O depurador ignora a função atual.|

## <a name="BKMK_Break_into_code_by_using_breakpoints_or_Break_All"></a>Executar para uma função ou local específico

Você pode preferir executar diretamente em um local ou uma função específica quando souber exatamente qual código você deseja inspecionar ou se você souber onde deseja iniciar a depuração.

### <a name="run-to-a-breakpoint-in-code"></a>Executar para um ponto de interrupção no código

Para definir um ponto de interrupção simples em seu código, clique na margem esquerda extrema ao lado da linha de código em que você deseja suspender a execução. Você também pode selecionar a linha e pressionar **F9** > , selecionar**ponto de interrupção de alternância**de **depuração** > , ou clicar com o botão direito do mouse e selecionar ponto de interrupção**Inserir ponto**de interrupção. O ponto de interrupção aparece como vermelho na margem esquerda ao lado da linha de código. O depurador suspende a execução logo antes da execução da linha.

![Definir um ponto de interrupção](../debugger/media/dbg_basics_setbreakpoint.png "Definir um ponto de interrupção")

Os pontos de interrupção no Visual Studio fornecem um conjunto rico de funcionalidades adicionais, como pontos de interrupção e pontos de monitoramento condicionais. Para obter detalhes, consulte [usando pontos de interrupção](../debugger/using-breakpoints.md).

### <a name="run-to-a-function-breakpoint"></a>Executar para um ponto de interrupção de função

Você pode instruir o depurador a ser executado até atingir uma função especificada. É possível especificar a função por nome ou escolhê-la na pilha de chamadas.

**Para especificar um ponto de interrupção de função por nome**

1. Selecione **depurar** > novo ponto de interrupção da**função** de**ponto de interrupção** > 

1. Na caixa de diálogo **novo ponto de interrupção de função** , digite o nome da função e selecione seu idioma.

   ![Caixa de diálogo Nova função de ponto de interrupção](../debugger/media/dbg_execution_newbreakpoint.png "Novo ponto de interrupção de função")

1. Selecione **OK**.

Se a função estiver sobrecarregada ou em mais de um namespace, você poderá escolher aquela desejada na janela pontos de **interrupção** .

![Pontos de interrupção de função] sobrecarregados (../debugger/media/dbg_execution_overloadedbreakpoints.png "Pontos de interrupção de função") sobrecarregados

**Para selecionar um ponto de interrupção de função da pilha de chamadas**

1. Durante a depuração, abra a janela **pilha de chamadas** selecionando **depurar** > **pilha de chamadas**do**Windows** > .

1. Na janela **pilha de chamadas** , clique com o botão direito do mouse em uma função e selecione **executar até o cursor**ou pressione **Ctrl**+**F10**.

Para rastrear visualmente a pilha de chamadas, consulte [métodos de mapeamento na pilha de chamadas durante a depuração](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).

### <a name="run-to-a-cursor-location"></a>Executar em um local de cursor

Para executar o local do cursor, no código-fonte ou na janela **pilha de chamadas** , selecione a linha que você deseja interromper, clique com o botão direito do mouse e selecione **executar até o cursor**ou pressione **Ctrl**+**F10**. Selecionar **executar até o cursor** é como definir um ponto de interrupção temporário.

### <a name="run-to-click"></a>Executar com um Clique

Enquanto estiver em pausa no depurador, você pode focalizar uma instrução no código-fonte ou na janela de desmontagem e selecionar o ícone de seta **executar execução para aqui** verde. O uso **de executar para clicar** elimina a necessidade de definir um ponto de interrupção temporário.

![Executar com um Clique](../debugger/media/dbg-run-to-click.png "Executar com um Clique")

> [!NOTE]
> **Executar para clicar** está disponível a partir [!include[vs_dev15](../misc/includes/vs_dev15_md.md)]de.

### <a name="manually-break-into-code"></a>Interromper manualmente o código

Para interromper a próxima linha de código disponível em um aplicativo em execução, selecione **depurar** > **quebra de tudo**ou pressione **Ctrl**+**ALT**+**Break**.

## <a name="BKMK_Set_the_next_statement_to_execute"></a>Mover o ponteiro para alterar o fluxo de execução

Enquanto o depurador é pausado, uma ponta de seta amarela na margem da janela código- fonte ou desmontagem marca o local da próxima instrução a ser executada. Você pode alterar a próxima instrução a ser executada movendo essa ponta de seta. Você pode ignorar uma parte do código ou retornar a uma linha anterior. Mover o ponteiro é útil para situações como ignorar uma seção de código que contém um bug conhecido.

 ![Mover o ponteiro](../debugger/media/dbg_basics_example3.gif "Mover o ponteiro")

Para alterar a próxima instrução a ser executada, o depurador deve estar no modo de interrupção. Na janela código-fonte ou desmontagem, arraste a ponta de seta amarela para uma linha diferente ou clique com o botão direito do mouse na linha que você deseja executar em seguida e selecione **definir próxima instrução**.

O contador de programa salta diretamente para o novo local e as instruções entre os pontos de execução antigo e novo não são executadas. No entanto, se você mover o ponto de execução para trás, as instruções intermediárias não serão desfeitas.

>[!CAUTION]
>- Mover a instrução seguinte para outra função ou escopo normalmente resulta em danos à pilha de chamadas, causando um erro em tempo de execução ou uma exceção. Se você tentar mover a instrução seguinte para outro escopo, o depurador abrirá uma caixa de diálogo com um aviso e dará uma chance de cancelar a operação.
>- No Visual Basic, você não pode mover a instrução seguinte para outro escopo ou função.
>- No C++ nativo, se você tiver as verificações de tempo de execução ativadas, definir a instrução seguinte poderá fazer com que uma exceção seja gerada quando a execução chegar ao final do método.
>- Quando a opção Editar e Continuar está habilitada, **Definir Próxima Instrução** falha caso você tenha feito edições que Editar e Continuar não pode remapear imediatamente. Isso pode ocorrer, por exemplo, se você editou o código dentro de um bloco catch. Quando isso acontece, uma mensagem de erro informa que a operação não tem suporte.
>- No código gerenciado, você não poderá mover a próxima instrução se:
>   - A instrução a seguir é um método diferente do que a instrução atual.
>   - A depuração foi iniciada pela depuração Just-in-time.
>   - Um desenrolamento de pilha de chamadas está em andamento.
>   - Uma exceção System.StackOverflowException ou System.Threading.ThreadAbortException foi lançada.

## <a name="BKMK_Restrict_stepping_to_Just_My_Code"></a>Depurar código de não usuário

Por padrão, o depurador tenta Depurar apenas o código do aplicativo, habilitando uma configuração chamada *apenas meu código*. Para obter mais detalhes sobre como esse recurso funciona para diferentes tipos de projeto e linguagens, e como você pode personalizá-lo, consulte [apenas meu código](../debugger/just-my-code.md).

Para examinar o código de estrutura, o código de biblioteca de terceiros ou as chamadas do sistema durante a depuração, você pode desabilitar Apenas Meu Código. Em **ferramentas** (ou **depurar**) >**depuração**de **Opções** > , desmarque a caixa de seleção **habilitar apenas meu código** . Quando Apenas Meu Código está desabilitado, o código que não é do usuário aparece nas janelas do depurador e o depurador pode entrar no código que não é do usuário.

> [!NOTE]
> Apenas Meu Código não é suportada para projetos de dispositivo.

### <a name="debug-system-code"></a>Depurar código do sistema

Se você carregou símbolos de depuração para o código do sistema da Microsoft e estiver desabilitado Apenas Meu Código, poderá entrar em uma chamada do sistema da mesma forma que qualquer outra chamada.

Para carregar os símbolos da Microsoft, consulte [Configurar locais de símbolo e opções de carregamento](specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md#configure-symbol-locations-and-loading-options).

**Para carregar símbolos para um componente do sistema específico:**

1. Enquanto estiver Depurando, abra a janela **módulos** selecionando **depurar** > **módulos**do**Windows** > ou pressionando **Ctrl**+**ALT**+**U**.

1. Na janela **módulos** , você pode saber quais módulos têm símbolos carregados na coluna **status do símbolo** . Clique com o botão direito do mouse no módulo para o qual você deseja carregar símbolos e selecione **carregar símbolos**.

## <a name="BKMK_Step_into_properties_and_operators_in_managed_code"></a> Intervir em propriedades e operadores no código gerenciado
 O depurador considera propriedades e operadores no código gerenciado por padrão. Na maioria dos casos, isso proporciona uma melhor experiência de depuração. Para habilitar a depuração em Propriedades ou operadores, escolha**Opções**de **depuração** > . Na página **depuração** > **geral** , desmarque a caixa de seleção **passar por propriedades e operadores (somente gerenciados)** .

## <a name="see-also"></a>Consulte também
- [O que é depuração?](../debugger/what-is-debugging.md)
- [Ferramentas e técnicas de depuração](../debugger/write-better-code-with-visual-studio.md)
- [Primeira olhada na depuração](../debugger/debugger-feature-tour.md)
