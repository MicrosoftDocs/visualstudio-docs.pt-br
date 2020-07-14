---
title: Exibir a pilha de chamadas no depurador | Microsoft Docs
ms.custom: seodec18
ms.date: 10/29/2018
ms.topic: how-to
f1_keywords:
- vs.debug.callstack
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
- aspx
helpviewer_keywords:
- threading [Visual Studio], displaying calls to or from
- functions [debugger], viewing code on call stack
- disassembly code
- breakpoints, Call Stack window
- debugging [Visual Studio], switching to another stack frame
- debugging [Visual Studio], Call Stack window
- Call Stack window, viewing source code for functions on the call stack
- stack, switching stack frames
- Call Stack window, viewing disassembly code for functions on the call stack
ms.assetid: 5154a2a1-4729-4dbb-b675-db611a72a731
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aa91807459ea5c2d8f576891d0eafc35336347bc
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348737"
---
# <a name="view-the-call-stack-and-use-the-call-stack-window-in-the-debugger"></a>Exibir a pilha de chamadas e usar a janela pilha de chamadas no depurador

Ao usar a janela **Pilha de Chamadas**, você pode exibir chamadas de função ou procedimento que estão na pilha atualmente. A janela **Pilha de Chamadas** mostra a ordem em que os métodos e as funções são chamados. A pilha de chamadas é uma boa maneira de examinar e entender o fluxo de execução de um aplicativo.

Quando os [símbolos de depuração](#bkmk_symbols) não estão disponíveis para parte de uma pilha de chamadas, a janela pilha de **chamadas** pode não ser capaz de exibir as informações corretas para essa parte da pilha de chamadas, exibindo em vez disso:

`[Frames below may be incorrect and/or missing, no symbols loaded for name.dll]`

> [!NOTE]
> A janela **Pilha de Chamadas** é semelhante à perspectiva de Depuração em alguns IDEs, como o Eclipse.

> [!NOTE]
> As caixas de diálogo e os comandos de menu vistos podem ser diferentes daqueles descritos aqui, dependendo da edição ou das configurações ativas. Para alterar as configurações, selecione **Importar e Exportar Configurações** no menu **Ferramentas**.  Consulte [Redefinir configurações](../ide/environment-settings.md#reset-settings).

## <a name="view-the-call-stack-while-in-the-debugger"></a>Exibir a pilha de chamadas enquanto estiver no depurador

- Durante a depuração, no menu **depurar** , selecione **Windows > pilha de chamadas**.

  ![Janela Pilha de Chamadas](../debugger/media/dbg_basics_callstack_window.png "CallStackWindow")

Uma seta amarela identifica o quadro de pilha onde o ponteiro de execução está localizado atualmente. Por padrão, as informações do quadro de pilhas são exibidas nas janelas origem, **locais**, **automáticos**, **inspecionar**e **desmontagem** . Para alterar o contexto do depurador para outro quadro na pilha, [alterne para outro quadro de pilhas](#bkmk_switch).

## <a name="display-non-user-code-in-the-call-stack-window"></a>Exibir código que não seja de usuário na janela pilha de chamadas

- Clique com o botão direito do mouse na janela **Pilha de Chamadas** e selecione **Mostrar Código Externo**.

Código de não usuário é qualquer código que não seja mostrado quando [apenas meu código](../debugger/just-my-code.md) estiver habilitado. No código gerenciado, os quadros de código que não são de usuário ficam ocultos por padrão. A seguinte notação aparece no lugar dos quadros de código que não são de usuário:

`[<External Code>]`

## <a name="switch-to-another-stack-frame-change-the-debugger-context"></a><a name="bkmk_switch"></a>Alternar para outro quadro de pilha (alterar o contexto do depurador)

1. Na janela **pilha de chamadas** , clique com o botão direito do mouse no registro de ativação cujo código e dados você deseja exibir.

    Ou, você pode clicar duas vezes em um quadro na janela **pilha de chamadas** para alternar para esse quadro.

2. Selecione **Alternar para Quadro**.

     Uma seta verde com uma parte de baixo é exibida ao lado do quadro de pilhas que você selecionou. O ponteiro de execução permanece no quadro original, que ainda está marcado com a seta amarela. Se você selecionar **Etapa** ou **Continuar** no menu **Depurar**, a execução continuará no quadro original, não no quadro selecionado.

## <a name="view-the-source-code-for-a-function-on-the-call-stack"></a>Exibir o código-fonte de uma função na pilha de chamadas

- Na janela **Pilha de Chamadas**, clique com o botão direito do mouse na função cujo código-fonte você deseja ver e selecione **Ir para Código-Fonte**.

## <a name="run-to-a-specific-function-from-the-call-stack-window"></a>Executar para uma função específica da janela pilha de chamadas

- Na janela **pilha de chamadas** , selecione a função, clique com o botão direito do mouse e escolha **executar até o cursor**.

## <a name="set-a-breakpoint-on-the-exit-point-of-a-function-call"></a>Definir um ponto de interrupção no momento de saída de uma chamada de função

- Consulte [definir um ponto de interrupção em uma função de pilha de chamadas](../debugger/using-breakpoints.md#BKMK_Set_a_breakpoint_from_debugger_windows).

## <a name="display-calls-to-or-from-another-thread"></a>Exibir chamadas de ou para outro thread

- Clique com o botão direito do mouse na janela **Pilha de Chamadas** e selecione **Incluir chamadas para/de outros threads**.

## <a name="visually-trace-the-call-stack"></a>Rastreie visualmente a pilha de chamadas

Em Visual Studio Enterprise (somente), você pode exibir mapas de código para a pilha de chamadas durante a depuração.

- Na janela **Pilha de Chamadas**, abra o menu de atalho. Escolha **Mostrar pilha de chamadas no mapa de códigos** (**Ctrl**  +  **Shift**  +  **`** ).

    Para obter mais informações, consulte [mapear métodos na pilha de chamadas durante a depuração](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md).

![Mostrar pilha de chamadas no mapa de códigos](../debugger/media/dbg_basics_show_call_stack_on_code_map.gif "ShowCallStackOnCodeMap")

## <a name="view-the-disassembly-code-for-a-function-on-the-call-stack-c-c-visual-basic-f"></a>Exibir o código de desmontagem de uma função na pilha de chamadas (C#, C++, Visual Basic, F #)

- Na janela **Pilha de Chamadas**, clique com o botão direito do mouse na função cujo código de desmontagem você deseja ver e selecione **Ir para Desmontagem**.

## <a name="change-the-optional-information-displayed"></a>Alterar as informações opcionais exibidas

- Clique com o botão direito do mouse na janela **pilha de chamadas** e defina ou desmarque **Mostrar \<**_the information that you want_**> **.

## <a name="load-symbols-for-a-module-c-c-visual-basic-f"></a><a name="bkmk_symbols"></a>Carregar símbolos para um módulo (C#, C++, Visual Basic, F #)

Na janela **Pilha de Chamadas**, você pode carregar símbolos de depuração para o código que atualmente não tem símbolos carregados. Esses símbolos podem ser .NET ou símbolos do sistema baixados dos servidores de símbolos públicos da Microsoft ou símbolos em um caminho de símbolo no computador que você está depurando.

Consulte [especificar símbolo (. pdb) e arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md).

### <a name="to-load-symbols"></a>Para carregar símbolos

1. Na janela **pilha de chamadas** , clique com o botão direito do mouse no quadro de pilha para o qual os símbolos não estão carregados. O quadro ficará esmaecido.

2. Aponte para **carregar símbolos** e, em seguida, selecione **servidores de símbolos da Microsoft** (se disponíveis) ou navegue até o caminho do símbolo.

### <a name="to-set-the-symbol-path"></a>Para definir o caminho do símbolo

1. Na janela **Pilha de Chamadas**, escolha **Configurações de Símbolo** no menu de atalho.

     A caixa de diálogo **Opções** abre e a página **Símbolos** é exibida.

2. Selecione **configurações de símbolo**.

3. Na caixa de diálogo **Opções**, clique no ícone da Pasta.

     Na caixa **Locais do arquivo de símbolo (.pdb)**, um cursor será exibido.

4. Insira um nome de caminho de diretório para o local do símbolo no computador que você está depurando. Para depuração local e remota, esse é um caminho no computador local.

5. Selecione **OK** para fechar a caixa de diálogo **Opções** .

## <a name="see-also"></a>Veja também

- [Código misto e informações ausentes na janela pilha de chamadas](../debugger/mixed-code-and-missing-information-in-the-call-stack-window.md)
- [Exibindo dados no depurador](../debugger/viewing-data-in-the-debugger.md)
- [Especificar o símbolo (. pdb) e os arquivos de origem](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)
- [Usando pontos de interrupção](../debugger/using-breakpoints.md)